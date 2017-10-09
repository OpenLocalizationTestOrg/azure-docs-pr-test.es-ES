---
title: "directrices de ajuste del rendimiento de aaaAzure aluvión de almacén de datos Lake | Documentos de Microsoft"
description: "Guía para la optimización del rendimiento de Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: 5412fd46cf2373f5877030913df4fe1fc6f5473a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-storm-on-hdinsight-and-azure-data-lake-store"></a>Guía para la optimización del rendimiento de Storm en HDInsight y Azure Data Lake Store

Entender los factores de Hola que deben tenerse en cuenta al optimizar el rendimiento de Hola de una topología de aluvión de Azure. Por ejemplo, es importante toounderstand características de Hola de trabajo de Hola Hola spouts y tornillos hello (si el trabajo de hello está intensivo de memoria o E/S). En este artículo se describen varias directrices de optimización del rendimiento y se incluyen soluciones a problemas comunes.

## <a name="prerequisites"></a>Requisitos previos

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Una cuenta de Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md).
* **Un clúster de HDInsight de Azure** con acceso tooa cuenta de almacén de Data Lake. Consulte [Creación de un clúster de HDInsight con Data Lake Store mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Asegúrese de que habilitar Escritorio remoto para el clúster de Hola.
* **Ejecución de un clúster de Storm en Data Lake Store**. Para más información, consulte [Storm en HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-overview).
* **Guía para la optimización del rendimiento en Data Lake Store**.  Para conocer los conceptos generales sobre rendimiento, consulte [Guía para la optimización del rendimiento de Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="tune-hello-parallelism-of-hello-topology"></a>Optimizar el paralelismo de Hola de topología de Hola

Es posible que pueda tooimprove rendimiento por la simultaneidad de hello creciente de hello tooand de E/S de almacén de Data Lake. Una topología de Storm tiene un conjunto de configuraciones que determinan el paralelismo de hello:
* Número de procesos de trabajo (trabajadores de Hola se distribuyen uniformemente entre las máquinas virtuales de hello).
* Número de instancias de ejecutor de spout
* Número de instancias de ejecutor de bolt
* Número de tareas de spout
* Número de tareas de bolt

Por ejemplo, en un clúster con 4 VM y 4 procesos de trabajo, ejecutor pitorro 32 y 32 pitorro tareas y 256 ejecutor de rayo y tareas de rayo 512, tenga en cuenta Hola siguiente:

Cada supervisor, que es un nodo de trabajo, tiene un solo proceso de trabajo de máquina virtual Java (JVM). Este proceso de JVM administra 4 subprocesos de spout y 64 subprocesos de bolt. Dentro de cada subproceso, las tareas se ejecutan secuencialmente. Con hello anterior configuración, cada subproceso pitorro tiene 1 tarea y, cada subproceso de rayo tiene 2 tareas.

En Storm, presentamos Hola diversos componentes implicados y cómo afectan al nivel de Hola de paralelismo que tiene:
* Hola y nodo principal (llamado Nimbus en Storm) usado toosubmit administrar trabajos. Estos nodos tienen ningún impacto en el grado de paralelismo Hola.
* nodos de supervisor de Hola. En HDInsight, esto corresponde el nodo de trabajo tooa máquina virtual de Azure.
* tareas del trabajador Hola son procesos de Storm que se ejecutan en máquinas virtuales de Hola. Cada tarea de trabajo corresponde la instancia JVM tooa. Storm distribuye número Hola de procesos de trabajo especificar nodos de trabajador toohello lo más uniformemente posible.
* Instancias de ejecutor de bolt y spout. Cada instancia del ejecutor corresponde tooa subproceso que se ejecuta dentro de los trabajadores de hello (JVMs).
* Tareas de Storm. Son tareas lógicas que ejecuta cada uno de estos subprocesos. Esto no cambia el nivel de Hola de paralelismo, por lo que se debe evaluar si tiene varias tareas por ejecutor o no.

### <a name="get-hello-best-performance-from-data-lake-store"></a>Obtenga un rendimiento mejor Hola del almacén de Data Lake

Cuando se trabaja con el almacén de Data Lake, obtendrá un rendimiento mejor Hola si Hola siguientes:
* Fusione sus anexos más pequeños en tamaños más grandes (lo ideal son 4 MB).
* Realice tantas solicitudes simultáneas como pueda. Dado que cada subproceso de rayo está realizando lecturas bloqueo, es conveniente toohave en algún lugar de intervalo de Hola de 8 a 12 subprocesos por núcleo. Esto impide que la CPU de hello y formación de hello también utilizado. Una máquina virtual más grande permite más solicitudes simultáneas.  

### <a name="example-topology"></a>Topología de ejemplo

Supongamos que tiene un clúster de 8 nodos de trabajo con una máquina virtual de Azure D13v2. Esta VM tiene 8 núcleos, por lo que entre Hola 8 nodos de trabajador, tendrá que 64 núcleos total.

Digamos que hacemos 8 subprocesos de bolt por núcleo. Como hay 64 núcleos, significa que queremos 512 instancias de ejecutor de bolt (es decir, subprocesos) en total. En este caso, supongamos que se inicie con una JVM por máquina virtual y utiliza principalmente la simultaneidad de subprocesos de hello dentro de simultaneidad de hello JVM tooachieve. Esto significa que necesitamos 8 tareas de trabajo (una por cada VM de Azure) y 512 ejecutores de bolt. Dada esta configuración, Storm intenta toodistribute Hola los trabajadores de manera uniforme entre los nodos de trabajo (también conocidos como nodos de supervisor), dando a cada nodo de trabajo 1 JVM. Ahora en los supervisores de hello, Storm intenta ejecutor de hello toodistribute uniformemente entre los supervisores, lo que proporciona cada supervisor (es decir, JVM) 8 subprocesos cada uno.

## <a name="tune-additional-parameters"></a>Ajuste de parámetros adicionales
Una vez haya topología básica de hello, tenga en cuenta si desea tootweak alguno de los parámetros de hello:
* **Number of JVMs per worker node** (Número total de JVM por nodo de trabajo). Si tiene una estructura de datos de gran tamaño (por ejemplo, una tabla de búsqueda) que se hospeda en memoria, cada JVM requiere una copia independiente. Como alternativa, puede utilizar estructura de datos de hello en muchos subprocesos si tiene menos JVMs. Para la E/S del rayo hello, número de Hola de JVMs no tiene tanta una diferencia como número de Hola de subprocesos que se agregan a través de esas JVMs. Para simplificar, es un toohave buena idea una JVM por trabajo. Dependiendo de lo que está haciendo el rayo o la aplicación de procesamiento necesita, sin embargo, puede que necesite toochange este número.
* **Number of spout executors** (Número de ejecutores de spout) Dado que hello en el ejemplo anterior se utiliza tornillos para escribir tooData Lake almacén, el número de Hola de spouts no es rendimiento de rayo toohello directamente relevante. Sin embargo, dependiendo de la cantidad de Hola de procesamiento o E/S ocurre en pitorro hello, es una buena idea hello tootune spouts para mejorar el rendimiento. Asegúrese de que tiene suficiente spouts toobe tookeep capaz de hello tornillos ocupado. tasas de salida de Hello de hello spouts deben coincidir con rendimiento Hola de hello tornillos. configuración real de Hello depende pitorro Hola.
* **Number of tasks** (Número de tareas) Cada bolt se ejecuta como un único subproceso. Las tareas adicionales por bolt no proporcionan ninguna simultaneidad adicional. Hola única ocasión en que son de beneficio es si el proceso de confirmación de tupla hello tiene una gran proporción del tiempo de ejecución de rayo. Es un toogroup buena idea que muchos tuplas en un mayor anexar antes de enviar una confirmación de rayo Hola. Por lo tanto, en la mayoría de los casos, varias tareas no proporcionan ninguna ventaja adicional.
* **Local or shuffle grouping** (Agrupación local o aleatoria) Cuando esta opción está habilitada, las tuplas se envían toobolts dentro de hello mismo proceso de trabajo. Esta opción reduce las llamadas de red y la comunicación entre procesos. Se recomienda su uso para la mayoría de las topologías.

Este escenario básico es un buen punto de partida. Pruebe con su propio hello tootweak de datos anterior a un rendimiento óptimo tooachieve parámetros.

## <a name="tune-hello-spout"></a>Optimizar pitorro Hola

Puede modificar Hola después configuración tootune Hola pitorro.

- **Tuple timeout (Tiempo de espera de tupla): topology.message.timeout.secs**. Esta configuración determina Hola tiempo tarda un mensaje toocomplete y recibir la confirmación, antes de que se considere error.

- **Max memory per worker process (Memoria máxima por proceso de trabajo): worker.childopts**. Esta configuración permite especificar los trabajadores de Java de toohello de parámetros de línea de comandos adicionales. Hola más frecuente establecer aquí es XmX, que determina el montón de JVM de hello memoria máxima asignada tooa.

- **Max spout pending (Spouts máximos pendientes): topology.max.spout.pending**. Esta configuración determina el número de Hola de tuplas que se pueden en vuelo (aún no se ha confirmado en todos los nodos de la topología de hello) por subproceso pitorro en cualquier momento.

 Un buen cálculo toodo es el tamaño de Hola de tooestimate de cada uno de sus tuplas. Después, averigüe cuánta memoria tiene un subproceso de spout. Hello memoria total asignada tooa subproceso, dividido por este valor, debe darle límite superior de Hola para pitorro max de hello pendiente de parámetro.

## <a name="tune-hello-bolt"></a>Optimizar rayo Hola
Cuando escriba tooData Lake almacén, establecer una directiva de sincronización de tamaño (el búfer en el lado del cliente de hello) too4 MB. A continuación, se realiza un vaciado o hsync() sólo cuando el tamaño del búfer de hello es hello en este valor. controlador de almacén de Data Lake Hello en el trabajo de hello VM realiza automáticamente este almacenamiento en búfer, a menos que realice explícitamente un hsync().

rayo de Hello predeterminado aluvión de almacén de datos Lake tiene un parámetro de directiva de sincronización de tamaño (fileBufferSize) que puede ser tootune usa este parámetro.

En estas topologías intensivas de entrada, es una buena idea toohave cada subproceso de rayo escribir archivo propio tooits y tooset una directiva de rotación de archivo (fileRotationSize). Cuando el archivo hello alcanza un determinado tamaño, automáticamente se vacía en el flujo de Hola y se escribe un nuevo archivo en. Hola tamaño de archivo para el giro recomendado es 1 GB.

### <a name="handle-tuple-data"></a>Administración de los datos de la tupla

En Storm, un pitorro contiene en tooa tupla hasta que se confirman de forma explícita por el rayo Hola. Si una tupla ha sido leída por el rayo Hola pero no se han confirmado aún, podría pitorro hello no se conservan en back-end de almacén de Data Lake. Después de que se confirma una tupla, pitorro Hola puede garantizarse persistencia por rayo de hello y, a continuación, puede eliminar datos de origen de Hola de cualquier origen que se está leyendo.  

Para obtener el mejor rendimiento en el almacén de Data Lake, tienen rayo Hola búfer de 4 MB de datos de la tupla. A continuación, escribir toohello nuevo almacén de Data Lake terminan siendo una escritura de 4 MB. Después de los datos de hello toohello correctamente escrito almacén (mediante hflush()) que realiza la llamada, rayo Hola puede reconocer Hola datos toohello atrás pitorro. Este es el ejemplo hello tornillo proporcionado hace aquí. También es aceptable toohold un mayor número de tuplas antes de que se realiza la llamada de hflush() de Hola y Hola tuplas confirmado. Sin embargo, esto aumenta el número de Hola de tuplas en vuelo que pitorro Hola necesita toohold, y, por tanto, aumenta Hola cantidad de memoria necesaria por JVM.

> [!NOTE]
Las aplicaciones pueden presentar un tuplas de tooacknowledge de requisito con más frecuencia (en tamaños de datos es menor que 4 MB) por otras razones de rendimiento no. Sin embargo, que podrían afectar a Hola E/S rendimiento toohello almacenamiento back-end. Detenidamente esta compensación con respecto al rendimiento de E/S del rayo Hola.

Si la velocidad de entrada de Hola de tuplas es no alta, por lo que el búfer de 4 MB de hello toma un toofill mucho tiempo, considere la posibilidad de mitigar este problema si:
* Reducir el número de Hola de tornillos, por lo que hay menos toofill de búferes.
* Tener una directiva basada en tiempo o basadas en recuento, donde es un hflush() desencadena cada x vaciados o cada milisegundos y y tuplas Hola acumulados hasta ahora se envía una confirmación.

Tenga en cuenta que rendimiento hello en este caso es inferior, pero con una velocidad lenta de eventos, el rendimiento máximo no es Hola mayor objetivo todos modos. Estas soluciones le ayudarán a reducir Hola el tiempo total que tarda en un tooflow tupla a través de la tienda de toohello. Esto podría ser importante si quiere una canalización en tiempo real incluso con una tasa baja de eventos. Tenga en cuenta también que si la tasa entrante de la tupla es baja, debe ajustar parámetro topology.message.timeout_secs de hello, por lo que las tuplas de hello no tiempo de espera mientras está obteniendo almacenando en búfer o procesar.

## <a name="monitor-your-topology-in-storm"></a>Supervisión de la topología en Storm  
Mientras se ejecuta la topología, se puede supervisar en interfaz de usuario de Storm Hola. Estos son toolook parámetros principales de hello en:

* **Total process execution latency (Latencia total de ejecución de procesos).** Se trata de tiempo promedio de hello una tupla toma toobe emitidos por pitorro hello, procesados por el rayo de Hola y confirmado.

* **Total bolt process latency (Latencia total de proceso del bolt).** Se trata de hello tiempo medio por tupla de hello en el rayo Hola hasta que recibe una confirmación.

* **Total bolt execute latency (Latencia total de ejecución del bolt).** Se trata de promedio de hello tiempo invertido por el rayo de Hola Hola execute (método).

* **Number of failures (Número de errores).** Esto refiere toohello número de tuplas que no se pudo toobe procesado totalmente antes de que agotó el tiempo.

* **Capacity (Capacidad).** Se trata de una medida de lo ocupado que está su sistema. Si este número es 1, los bolts trabajan tan rápido como pueden. Si es menor que 1, aumentar el paralelismo de Hola. Si es mayor que 1, reducir el paralelismo de Hola.

## <a name="troubleshoot-common-problems"></a>Solución de problemas comunes
Estos son algunos escenarios comunes de solución de problemas.
* **El tiempo de espera de muchas tuplas se está agotando.** Buscar en cada nodo de hello topología toodetermine donde es el cuello de botella de Hola. razón más común de Hola para este es que Hola tornillos no son tookeep capaz de seguridad con spouts Hola. Esto conduce tootuples atascada por los búferes internos de hello mientras toobe espera procesados. Considere la posibilidad de aumentar el valor de tiempo de espera de Hola o reduciendo pitorro max de hello pendientes.

* **Existe una latencia alta total en la ejecución de los procesos, pero una latencia baja en los procesos de bolt.** En este caso, es posible que Hola tuplas no son va a reconocer suficientemente rápido. Compruebe que hay un número suficiente de elementos de reconocimiento. Otra posibilidad es que están esperando en la cola de Hola durante demasiado tiempo antes de hello tornillos inicio procesarlos. Disminuir pitorro max de hello pendientes.

* **Existe una latencia alta en la ejecución de bolts.** Esto significa que Hola método Execute () de su rayo está tardando demasiado. Optimizar el código de hello, o buscar en tamaños de escritura y vaciar el comportamiento.

### <a name="data-lake-store-throttling"></a>Limitación de Data Lake Store
Si alcanza los límites de Hola de ancho de banda proporcionada por el almacén de Data Lake, podrá ver los errores de la tarea. Compruebe los registros de la tarea para ver los errores de limitación. Puede reducir el paralelismo de hello al aumentar el tamaño del contenedor.    

toocheck si están obteniendo limitados, habilitar el registro en el lado del cliente de Hola de depuración de hello:

1. En **Ambari** > **Storm** > **Config** > **avanzada storm-worker-log4j**, cambiar  **&lt;raíz nivel = "info"&gt;**  demasiado**&lt;raíz nivel = "debug"&gt;**. Reiniciar todos los nodos de Hola/servicio con efecto de tootake de configuración de Hola.
2. Registros de monitor Hola Storm topología en nodos de trabajador (bajo /var/log/storm/worker-artifacts /&lt;TopologyName&gt;/&lt;puerto&gt;/worker.log) para el almacén de Data Lake excepciones de limitación.

## <a name="next-steps"></a>Pasos siguientes
Puede consultar este [blog](https://blogs.msdn.microsoft.com/shanyu/2015/05/14/performance-tuning-for-hdinsight-storm-and-microsoft-azure-eventhubs/) para saber más sobre la optimización del rendimiento adicional de Storm.

Para una toorun ejemplo adicional, vea [ésta en GitHub](https://github.com/hdinsight/storm-performance-automation).
