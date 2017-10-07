---
title: "Azure Premium Storage: diseño de alto rendimiento | Microsoft Docs"
description: "Diseñe aplicaciones de alto rendimiento con Almacenamiento premium de Azure. El Almacenamiento premium le ofrece compatibilidad con discos de alto rendimiento y baja latencia para cargas de trabajo con un uso intensivo de E/S, que se ejecutan en máquinas virtuales de Azure."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: e6a409c3-d31a-4704-a93c-0a04fdc95960
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: aungoo
ms.openlocfilehash: 75845eb4707e8e5606153a5e1a7c10b4113ee121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-premium-storage-design-for-high-performance"></a>Almacenamiento premium de Azure: diseño de alto rendimiento
## <a name="overview"></a>Información general
Este artículo proporciona instrucciones para crear aplicaciones de alto rendimiento con Almacenamiento premium de Azure. Puede usar instrucciones de hello proporcionadas en este documento combinado con mejor tootechnologies de aplicable de prácticas rendimiento que usa la aplicación. directrices de hello tooillustrate, hemos usado SQL Server que se ejecutan en almacenamiento Premium como ejemplo a lo largo de este documento.

Mientras se tratan los escenarios de rendimiento para capas de almacenamiento de hello en este artículo, deberá toooptimize capa de aplicación de Hola. Por ejemplo, si está hospedando una granja de SharePoint en el almacenamiento de Azure Premium, puede usar los ejemplos de SQL Server de Hola desde este servidor de base de datos de artículo toooptimize Hola. Optimizar el Además, servidor Web de la granja de SharePoint de Hola y Hola de aplicación servidor tooget máximo rendimiento.

Este artículo le ayudará a responder a las siguientes preguntas habituales acerca de cómo optimizar el rendimiento de las aplicaciones en Almacenamiento premium de Azure:

* ¿Cómo toomeasure el rendimiento de la aplicación?  
* ¿Por qué no se ve el alto rendimiento esperado?  
* ¿Qué factores influyen en el rendimiento de las aplicaciones en Almacenamiento premium?  
* ¿Cómo influyen estos factores en el rendimiento de las aplicaciones en Almacenamiento premium?  
* ¿Cómo puede optimizar para IOPS, el ancho de banda y la latencia?  

Proporcionamos estas directrices específicamente para Almacenamiento premium porque las cargas de trabajo que se ejecutan en Almacenamiento premium dependen mucho del rendimiento. Se proporcionan ejemplos donde corresponda. También puede aplicar algunos de estos tooapplications instrucciones que se ejecutan en máquinas virtuales de IaaS con discos de almacenamiento estándar.

Antes de comenzar, si está tooPremium nuevo almacenamiento, lea primero hello [almacenamiento Premium: almacenamiento de alto rendimiento para cargas de trabajo de máquina Virtual de Azure](storage-premium-storage.md) y [escalabilidad de almacenamiento de Azure y objetivos de rendimiento](storage-scalability-targets.md)artículos.

## <a name="application-performance-indicators"></a>Indicadores del rendimiento de las aplicaciones
Se evaluar si una aplicación está realizando correctamente o no con como indicadores de rendimiento, ¿con qué rapidez una aplicación procesa una solicitud de usuario, la cantidad de datos que procesa la aplicación por solicitud, la cantidad de solicitudes que realiza el procesamiento de una aplicación en un determinado período de tiempo, que un usuario tiene toowait tooget una respuesta después de enviar su solicitud. son términos técnicos de Hola para estos indicadores de rendimiento, IOPS, el rendimiento o el ancho de banda y latencia.

En esta sección, veremos los indicadores de rendimiento comunes de hello en el contexto de Hola de almacenamiento Premium. Hola pasos de la sección, recopilación de requisitos de la aplicación, obtendrá información sobre cómo toomeasure estos indicadores de rendimiento de la aplicación. Más adelante en optimizar el rendimiento de la aplicación, obtendrá información acerca de los factores de Hola que afectan a estas toooptimize de indicadores y recomendaciones de rendimiento ellos.

## <a name="iops"></a>E/S
E/s por segundo es el número de solicitudes que la aplicación está enviando toohello discos de almacenamiento en un segundo. Una operación de entrada y salida se puede de lectura o escritura, secuencial o aleatoria. Las aplicaciones de OLTP como una tienda en línea en línea deben tooprocess muchos usuarios simultáneos solicita inmediatamente. las solicitudes de usuario de Hello son insert y actualizan las transacciones de uso intensivo de la base de datos, qué aplicación Hola debe procesar rápidamente. Por lo tanto, las aplicaciones OLTP requieren IOPS muy alta. Dichas aplicaciones controlan millones de solicitudes de E/S pequeñas y aleatorias. Si tiene este tipo de aplicación, debe diseñar toooptimize de infraestructura de aplicación Hola para e/s por segundo. Hola sección más adelante, *optimizar el rendimiento de la aplicación*, analizaremos en detalle todos los factores de Hola que debe tener en cuenta tooget índice elevado de IOPS.

Cuando se adjunta una premium almacenamiento disco tooyour gran escala VM, Azure aprovisiona automáticamente un número de IOPS garantizado según la especificación de disco Hola. Por ejemplo, un disco P50 aprovisiona 7500 IOPS. Cada tamaño de máquina virtual a gran escala también tiene un límite de IOPS específico que puede admitir. Por ejemplo, una máquina virtual GS5 estándar tiene un límite de 80.000 IOPS.

## <a name="throughput"></a>Rendimiento
Rendimiento o ancho de banda es la cantidad de Hola de datos que la aplicación está enviando toohello discos de almacenamiento en un intervalo especificado. Si la aplicación está realizando operaciones de entrada y salida con  tamaños de unidad de E/S grandes, requiere un alto rendimiento. Las aplicaciones de almacenamiento de datos tienden a operaciones intensivas de tooissue examen que acceden a grandes porciones de datos a la vez y se suele realizan operaciones masivas. En otras palabras, estas aplicaciones requieren un mayor rendimiento. Si tiene este tipo de aplicación, debe diseñar su infraestructura toooptimize para el rendimiento. En la siguiente sección hello, analizamos en factores de Hola de detalle debe optimizar tooachieve esto.

Cuando se adjunta una premium almacenamiento disco tooa gran escala VM, Azure aprovisiona rendimiento según esa especificación de disco. Por ejemplo, un disco P50 aprovisiona 250 MB por capacidad de proceso del segundo disco. Cada tamaño de máquina virtual a gran escala también tiene un límite de rendimiento específico que puede admitir. Por ejemplo, la máquina virtual GS5 estándar tiene un rendimiento máximo de 2.000 MB por segundo. 

Hay una relación entre el rendimiento y e/s por segundo, como se muestra en la siguiente fórmula de saludo.

![](media/storage-premium-storage-performance/image1.png)

Por lo tanto, es importante toodetermine Hola rendimiento e IOPS valores óptimos que requiera la aplicación. Cuando intente toooptimize uno, también obtiene afectado Hola otro. En una sección posterior, *Optimización del rendimiento de las aplicaciones*, trataremos con más detalle cómo optimizar el rendimiento y la IOPS.

## <a name="latency"></a>Latency
Latencia es Hola que tarda una aplicación tooreceive una sola solicitud, enviar los discos de almacenamiento de toohello y enviando a Hola respuesta toohello cliente. Se trata de una medida de rendimiento de la aplicación en tooIOPS de suma y el rendimiento crítica. Hola latencia de un disco de almacenamiento premium es el momento de Hola se toma tooretrieve Hola información para una solicitud y se comunican tooyour aplicación de nuevo. Almacenamiento premium proporciona latencias bajas coherentes. Si habilita el almacenamiento en caché de host ReadOnly en discos de almacenamiento premium, puede obtener una latencia de lectura mucho menor. Trataremos el almacenamiento en caché de disco con más detalle en la sección *Optimización del rendimiento de las aplicaciones*.

Cuando se optimizan los tooget aplicación mayor rendimiento y el IOPS afectará Hola latencia de la aplicación. Después de optimizar el rendimiento de la aplicación hello, siempre se evalúan Hola latencia de hello aplicación tooavoid comportamiento inesperado de latencia alta.

## <a name="gather-application-performance-requirements"></a>Reunión de los requisitos de rendimiento de las aplicaciones
Hola primer paso para diseñar aplicaciones de alto rendimiento que se ejecutan en el almacenamiento de Azure Premium es, requisitos de rendimiento de hello toounderstand de la aplicación. Después de recopilar los requisitos de rendimiento, puede optimizar el rendimiento de aplicación tooachieve Hola óptimo.

En la sección anterior de hello, se explican Hola indicadores comunes de rendimiento, IOPS, rendimiento y latencia. Debe identificar cuál de estos indicadores de rendimiento son críticos tooyour la experiencia del usuario toodeliver Hola deseado de la aplicación. Por ejemplo, IOPS alto es importante la mayoría de las aplicaciones de tooOLTP procesar millones de transacciones en un segundo. Por otra parte, un alto rendimiento es fundamental para las aplicaciones de Almacenamiento de datos que procesan grandes cantidades de datos en un segundo. Una latencia extremadamente baja es fundamental para las aplicaciones en tiempo real, como sitios web de streaming de vídeo en directo.

A continuación, medir los requisitos de rendimiento máximo de hello de la aplicación a lo largo de su duración. Utilice la lista de comprobación de ejemplo de Hola a continuación como un tutorial de inicio. Requisitos de rendimiento máximo de registro Hola durante normal, los períodos de carga de trabajo de las horas punta y fuera del horario comercial. Mediante la identificación de requisitos para todos los niveles de las cargas de trabajo, será capaz de toodetermine Hola requisito de rendimiento general de la aplicación. Por ejemplo, hello carga de trabajo normal de un sitio Web de comercio electrónico estará transacciones Hola atienda durante casi todos los días en un año. carga de trabajo de Hello máxima del sitio Web de hello será transacciones Hola atienda durante la temporada de vacaciones o eventos de venta especial. carga de trabajo de Hello máxima es normalmente con experiencia durante un período limitado, pero puede requerir la tooscale aplicación dos o más veces su funcionamiento normal. Averigüe percentil 50 de hello, como percentiles 90 y requisitos de percentil 99. Esto ayuda a filtrar los valores atípicos en los requisitos de rendimiento de Hola y pueda centrar sus esfuerzos en optimizar para valores correctos de Hola.

**Lista de comprobación de requisitos de rendimiento de las aplicaciones**

| **Requisitos de rendimiento** | **Percentil 50** | **Percentil 90** | **Percentil 99** |
| --- | --- | --- | --- |
| Máx. Transacciones por segundo | | | |
| Porcentaje de operaciones de lectura | | | |
| Porcentaje de operaciones de escritura | | | |
| Porcentaje de operaciones aleatorias | | | |
| Porcentaje de operaciones secuenciales | | | |
| Tamaño de las solicitudes de E/S | | | |
| Rendimiento medio | | | |
| Máx. Rendimiento | | | |
| Mín. Latency | | | |
| Latencia media | | | |
| Máx. CPU | | | |
| Promedio de CPU | | | |
| Máx. Memoria | | | |
| Promedio de memoria | | | |
| Profundidad de la cola | | | |

> [!NOTE]
> Debe considerar la posibilidad de escalar estos números en función del crecimiento futuro previsto de la aplicación. Es un tooplan buena idea crecimiento adelantado, porque podría ser más difíciles de infraestructura de hello toochange para mejorar el rendimiento más adelante.
>
>

Si tiene una aplicación existente y desea toomove tooPremium almacenamiento, crear lista de comprobación de Hola por encima de la aplicación existente de Hola. A continuación, crear un prototipo de la aplicación en almacenamiento Premium y diseñar la aplicación hello en función de las directrices descritas en *optimizar el rendimiento de la aplicación* en una sección posterior de este documento. Hola próxima sección describe herramientas de Hola que puede usar medidas de rendimiento de toogather Hola.

Crear una lista de comprobación tooyour existente aplicación similar de prototipo de Hola. Con herramientas de Benchmarking puede simular cargas de trabajo de Hola y medir el rendimiento en aplicaciones de prototipo de Hola. Vea la sección de hello en [Benchmarking](#benchmarking) toolearn más. Gracias a ello, puede determinar si Almacenamiento premium puede alcanzar o superar los requisitos de rendimiento de las aplicaciones. A continuación, puede implementar Hola mismas directrices para la aplicación de producción.

### <a name="counters-toomeasure-application-performance-requirements"></a>Contadores de toomeasure requisitos de rendimiento de aplicaciones
Hola requisitos de rendimiento de toomeasure de mejor manera de la aplicación, herramientas de supervisión del rendimiento de toouse proporcionadas por sistema operativo de saludo del servidor de Hola. Puede usar PerfMon para Windows e iostat para Linux. Estas herramientas capturan contadores medida tooeach correspondiente se explica en hello por encima de la sección. Debe capturar valores de hello de estos contadores cuando la aplicación está ejecutando su normal, las cargas de trabajo de las horas punta y fuera del horario comercial.

contadores de rendimiento de Hello están disponibles para el procesador, memoria y, en cada disco lógico y disco físico del servidor. Cuando se utilizan discos de almacenamiento premium con una máquina virtual, los contadores de disco físico de hello son para cada disco de almacenamiento premium y contadores de disco lógico son para cada volumen creado en discos de almacenamiento de hello premium. Debe capturar valores de hello para discos de Hola que hospedan la carga de trabajo de la aplicación. Si hay una asignación de tooone uno entre los discos lógicos y físicos, puede consultar los contadores de disco toophysical; en caso contrario, consulte toohello los contadores de disco lógico. En Linux, comando iostat de hello genera un informe de uso de CPU y disco. informe de uso de disco de Hello proporciona estadísticas por partición o dispositivo físico. Si tiene un servidor de bases de datos con sus datos e inicia sesión en discos independientes, recopile estos datos para ambos discos. La tabla siguiente describe los contadores de los discos, el procesador y la memoria:

| Contador | Description | PerfMon | Iostat |
| --- | --- | --- | --- |
| **E/S por segundo o transacciones por segundo** |Número de solicitudes de E/S emitidas toohello de disco de almacenamiento por segundo. |Lecturas de disco/s  <br> Escrituras en disco/s |tps  <br> r/s  <br> w/s |
| **Escrituras y lecturas de disco** |% de lectura y escritura de las operaciones realizadas en el disco de Hola. |% de tiempo de lectura de disco  <br> % de tiempo de escritura de disco |r/s  <br> w/s |
| **Rendimiento** |Cantidad de datos de lectura o escritura de disco toohello por segundo. |Bytes de lectura de disco/s  <br>  Bytes de escritura en disco/s |kB_read/s <br> kB_wrtn/s |
| **Latency** |Número total de tiempo toocomplete una solicitud de E/S de disco. |Promedio de segundos de disco/lectura  <br> Promedio de segundos de disco/escritura |await  <br> svctm |
| **Tamaño de E/S** |tamaño de Hola de solicitudes de E/S emite toohello discos de almacenamiento. |Promedio de bytes de disco/lectura  <br> Promedio de bytes de disco/escritura |avgrq-sz |
| **Profundidad de la cola** |Número de operaciones de E/S pendientes solicitudes espera toobe formulario de lectura o escritura toohello disco de almacenamiento. |Longitud actual de cola de disco |avgqu-sz |
| **Máx. memoria** |Cantidad de memoria necesaria toorun aplicación sin problemas |% de bytes confirmados en uso |Use vmstat |
| **Máx. CPU** |Cantidad de CPU necesario toorun aplicación sin problemas |% de tiempo de procesador |%util |

Obtenga más información sobre [iostat](http://linuxcommand.org/man_pages/iostat1.html) y [PerfMon](https://msdn.microsoft.com/library/aa645516.aspx).

## <a name="optimizing-application-performance"></a>Optimización del rendimiento de las aplicaciones
factores principales de Hola que influyen en el rendimiento de una aplicación que se ejecutan en almacenamiento Premium son naturaleza de las solicitudes de E/S, tamaño de máquina virtual, el tamaño de disco, el número de discos, el almacenamiento en caché de disco, el subprocesamiento múltiple y profundidad de cola. Puede controlar algunos de estos factores con botones proporcionados por sistema Hola. Mayoría de las aplicaciones puede no conseguir un Hola de tooalter opción tamaño de E/S y la profundidad de cola directamente. Por ejemplo, si está utilizando SQL Server, no puede elegir la profundidad de cola y el tamaño de E/S de Hola. SQL Server elige Hola óptimo E/S tamaño y la cola de profundidad valores tooget Hola máximo rendimiento. Es importante toounderstand efectos de Hola de ambos tipos de factores en el rendimiento de la aplicación, por lo que puede aprovisionar los recursos adecuados toomeet las necesidades de rendimiento.

A lo largo de esta sección, consulte toohello aplicación requisitos lista de comprobación que ha creado, tooidentify cuánto debe toooptimize el rendimiento de la aplicación. En función de que, será capaz de toodetermine que factores de esta sección será necesario tootune. toowitness Hola efectos de cada factor en el rendimiento de la aplicación, ejecutar pruebas comparativas de herramientas de la configuración de la aplicación. Consulte toohello [Benchmarking](#Benchmarking) sección Hola final de este artículo para toorun de pasos comunes de pruebas comparativas herramientas en Windows y máquinas virtuales de Linux.

### <a name="optimizing-iops-throughput-and-latency-at-a-glance"></a>Optimización de IOPS, rendimiento y latencia de un vistazo
tabla de Hola a continuación resumen todos los factores de rendimiento de Hola y Hola pasos toooptimize IOPS, rendimiento y latencia. Hello las secciones siguientes de este resumen describen cada factor es mucho más minuciosa.

| &nbsp; | **E/S** | **Rendimiento** | **Latency** |
| --- | --- | --- | --- |
| **Escenario de ejemplo** |Aplicación OLTP empresarial que requiere una tasa muy alta de transacciones por segundo. |Aplicación de Almacenamiento de datos de empresa que procesa grandes cantidades de datos. |Cerca de aplicaciones en tiempo real que requieren las solicitudes de toouser de respuestas de instantánea, como juegos en línea. |
| Factores de rendimiento | &nbsp; | &nbsp; | &nbsp; |
| **Tamaño de E/S** |Un tamaño de E/S menor produce una mayor IOPS. |Mayor tooyields de tamaño de E/S un mayor rendimiento. | &nbsp;|
| **Tamaño de VM** |Use un tamaño de máquina virtual que ofrezca una IOPS mayor que los requisitos de la aplicación. Consulte los tamaños de las máquinas virtuales y sus límites de IOPS aquí. |Use un tamaño de máquina virtual con un límite de rendimiento mayor que los requisitos de la aplicación. Consulte los tamaños de máquinas virtuales y sus límites de rendimiento aquí. |Use un tamaño de máquina virtual que ofrezca una escala de límites mayor que los requisitos de la aplicación. Consulte los tamaños de máquinas virtuales y sus límites aquí. |
| **Tamaño del disco** |Use un tamaño de disco que ofrezca una IOPS mayor que los requisitos de la aplicación. Consulte los tamaños de disco y sus límites de IOPS aquí. |Use un tamaño de disco con un límite de rendimiento mayor que los requisitos de la aplicación. Consulte los tamaños de disco y sus límites de rendimiento aquí. |Use un tamaño de disco que ofrezca una escala de límites mayor que los requisitos de la aplicación. Consulte los tamaños de disco y sus límites aquí. |
| **Máquina virtual y límites de escala de disco** |Límite de IOPS de elección de tamaño VM de hello debe ser mayor que las IOPS totales depende de los discos de almacenamiento premium adjunta tooit. |Límite de rendimiento de elección de tamaño VM de hello debe ser mayor que el rendimiento total depende de los discos de almacenamiento premium adjunta tooit. |Límites de escala de elección de tamaño VM de hello deben ser mayores que los límites de escala total de discos de almacenamiento premium adjunto. |
| **Almacenamiento en caché de disco** |Habilitar la memoria caché de solo lectura en los discos de almacenamiento premium con lectura operaciones intensivas tooget superior IOPS de lectura. | &nbsp; |Habilitar la memoria caché de solo lectura en los discos de almacenamiento premium con latencias de lectura de operaciones intensivas listo tooget muy bajas. |
| **Seccionamiento del disco** |Usar varios discos y crear bandas ellos tooget junto un combinado de IOPS superior y límite de rendimiento. Tenga en cuenta que Hola límite combinado por máquina virtual debe ser superior a Hola combinados límites de discos premium adjunto. | &nbsp; | &nbsp; |
| **Tamaño de franja** |Un menor tamaño de franja para un patrón de E/S pequeño y aleatorio visto en las aplicaciones OLTP. Por ejemplo, puede usar un tamaño de franja de 64 KB para aplicaciones OLTP de SQL Server. |Un mayor tamaño de franja para un patrón de E/ grande y secuencial visto en las aplicaciones de Almacenamiento de datos. Por ejemplo, puede usar un tamaño de franja de 256 KB para aplicaciones de Almacenamiento de datos de SQL Server. | &nbsp; |
| **Multithreading** |Utilice el subprocesamiento múltiple toopush aumentar el número de solicitudes tooPremium almacenamiento que ocasionarán toohigher IOPS y el rendimiento. Por ejemplo, en SQL Server establece una alta tooallocate valor MAXDOP más CPU tooSQL Server. | &nbsp; | &nbsp; |
| **Profundidad de la cola** |Una profundidad de la cola mayor produce una IOPS mayor. |Una profundidad de la cola mayor produce un mayor rendimiento. |Una profundidad de la cola menor produce latencias más bajas. |

## <a name="nature-of-io-requests"></a>Naturaleza de las solicitudes de E/S
Una solicitud de E/S es una unidad de operación de entrada y salida que la aplicación va a realizar. Identificar la naturaleza de Hola de las solicitudes de E/S aleatorias o secuenciales, lectura o escritura, pequeña o grande, le ayudará a determinar los requisitos de rendimiento de saludo de la aplicación. Es muy importante toounderstand naturaleza de Hola de solicitudes de E/S, toomake Hola tome las decisiones correctas al diseñar la infraestructura de aplicación.

Tamaño de E/S es uno de hello factores más importantes. Hola tamaño de E/S es tamaño Hola de solicitud de operación de entrada/salida de hello generado por la aplicación. Hola tamaño de E/S tiene un efecto significativo en el rendimiento, especialmente en hello IOPS y ancho de banda que Hola aplicación es capaz de tooachieve. Hello siguiente fórmula muestra hello relación entre IOPS, ancho de banda/rendimiento y tamaño de E/S.  
    ![](media/storage-premium-storage-performance/image1.png)

Algunas aplicaciones permiten tooalter sus E/S tamaño, mientras que algunas aplicaciones no. Por ejemplo, SQL Server determina el tamaño óptimo de hello IO propio y no proporciona a los usuarios con cualquier toochange botones se. En Hola otra parte, Oracle proporciona un parámetro denominado [DB\_bloquear\_tamaño](https://docs.oracle.com/cd/B19306_01/server.102/b14211/iodesign.htm#i28815) usando lo que puede configurar Hola el tamaño de la solicitud de E/S de base de datos de Hola.

Si está utilizando una aplicación, que no permite toochange Hola tamaño de E/S, utilice instrucciones de hello en este artículo toooptimize Hola de rendimiento KPI que es la aplicación tooyour más relevante. Por ejemplo,

* Una aplicación OLTP genera millones de solicitudes de E/S pequeñas y aleatorias. solicita toohandle estos tipo de E/S, debe diseñar su tooget de infraestructura de aplicación mayor e/s por segundo.  
* Una aplicación de almacenamiento de datos genera solicitudes de E/S grandes y secuenciales. toohandle estos tipo de solicitudes de E/S, debe diseñar su tooget de infraestructura de aplicación mayor ancho de banda o rendimiento.

Si está utilizando una aplicación, que permite el tamaño de E/S de hello toochange, usar esta regla general para hello E/S además tamaño tooother directrices de rendimiento,

* Tooget de tamaño de E/S más pequeño mayor e/s por segundo. Por ejemplo, 8 KB para una aplicación OLTP.  
* Tooget de tamaño de E/S mayor ancho de banda y un rendimiento mayor. Por ejemplo, 1024 KB para una aplicación de Almacenamiento de datos.

Este es un ejemplo de cómo se pueden calcular hello IOPS y ancho de banda y el rendimiento de la aplicación. Considere una aplicación con un disco P30. Hello rendimiento/ancho de banda puede lograr un disco P30 y número máximo de IOPS es 5000 e/s por segundo y 200 MB por segundo respectivamente. Ahora, si la aplicación requiere Hola que número máximo de IOPS de disco de hello P30 y usar un tamaño más pequeño de E/S como 8 KB, hello resultante será el ancho de banda puede tooget es 40 MB por segundo. Sin embargo, si la aplicación requiere Hola rendimiento/ancho de banda máximo del disco P30 y usar un tamaño de E/S como 1024 KB, hello IOPS resultante será menor, 200 e/s por segundo. Por lo tanto, ajustar tamaño de E/S de hello, que cumple el requisito de IOPS y ancho de banda y el rendimiento de ambos de su aplicación. Siguiente tabla resume los diferentes tamaños de E/S hello y sus correspondientes IOPS y rendimiento para un disco P30.

| Requisito de la aplicación | Tamaño de E/S | E/S | Rendimiento/ancho de banda |
| --- | --- | --- | --- |
| IOPS máx. |8 KB |5.000 |40 MB por segundo |
| Rendimiento máx. |1024 KB |200 |200 MB por segundo |
| Rendimiento máx.+ IOPS alta |64 KB |3.200 |200 MB por segundo |
| IOPS máx. + alto rendimiento |32 KB |5.000 |160 MB por segundo |

tooget IOPS y ancho de banda mayor que el valor máximo de Hola de un disco de almacenamiento premium solo, utilice varios discos premium seccionados juntos. Por ejemplo, cree franjas de dos P30 discos tooget un combinado de IOPS de 10.000 e/s por segundo o un rendimiento combinado de 400 MB por segundo. Como se explica en la sección siguiente de hello, debe usar un tamaño de memoria virtual que admita Hola combinan IOPS del disco y el rendimiento.

> [!NOTE]
> Aumentar cualquiera IOPS u otro Hola de rendimiento también aumenta, asegúrese de que no se alcanza el rendimiento o los límites IOPS de disco de Hola o máquina virtual al aumentar cualquiera de los.
>
>

toowitness Hola efectos de tamaño de E/S en el rendimiento de la aplicación, puede ejecutar pruebas comparativas de herramientas en la máquina virtual y los discos. Crear varias series de pruebas y usar tamaño de E/S diferente para cada ejecución toosee su impacto Hola. Consulte toohello [Benchmarking](#Benchmarking) sección Hola final de este artículo para obtener más detalles.

## <a name="high-scale-vm-sizes"></a>Tamaños de máquina virtual a gran escala
Al empezar a diseñar una aplicación, una de hello primera cosas toodo es, elija un toohost de máquina virtual de la aplicación. Almacenamiento premium viene con tamaños de máquina virtual a gran escala que pueden ejecutar aplicaciones que requieren una mayor capacidad de proceso y un alto rendimiento de E/S del disco local. Estas máquinas virtuales proporcionan procesadores más rápidos, una mayor proporción de memoria a núcleo y una unidad de Solid-State (SSD) para el disco local de Hola. Ejemplos de máquinas virtuales de alta escala admiten almacenamiento Premium son series de DS, DSv2 y GS de hello las máquinas virtuales.

Las máquinas virtuales a gran escala están disponibles en distintos tamaños con un número diferente de núcleos de CPU, memoria, sistema operativo y tamaño del disco temporal. Cada tamaño de máquina virtual también tiene el número máximo de discos de datos que puede adjuntar toohello máquina virtual. Por lo tanto, tamaño de máquina virtual de hello elegido afectará cuánta capacidad de procesamiento, memoria y almacenamiento está disponible para la aplicación. También afecta al proceso Hola y el costo de almacenamiento. Por ejemplo, a continuación se muestran las especificaciones de Hola de mayor tamaño VM hello en una serie de DS, DSv2 serie y una serie de GS:

| Tamaño de VM | Núcleos de CPU | Memoria | Tamaños de disco de VM | Máx. discos de datos | Tamaño de memoria caché | E/S | Límites de E/S de la memoria caché de ancho de banda |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS14 |16 |112 GB |OS = 1.023 GB  <br> SSD Local = 224 GB |32 |576 GB |50.000 E/S por segundo  <br> 512 MB por segundo |4.000 IOPS y 33 MB por segundo |
| Standard_GS5 |32 |448 GB |OS = 1.023 GB  <br> SSD Local = 896 GB |64 |4224 GB |80.000 E/S por segundo  <br> 2000 MB por segundo |5.000 IOPS y 50 MB por segundo |

tooview obtener una lista completa de todos los tamaños de máquina virtual de Azure disponibles, consulte demasiado[tamaños de máquina virtual de Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [tamaños de VM de Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Elija un tamaño de memoria virtual que se puede cumplir y escalar los requisitos de rendimiento de aplicaciones de tooyour deseado. Además toothis, tenga en cuenta las siguientes consideraciones importantes cuando se elige tamaños de máquina virtual.

*Límites de escala*  
Hola máximos límites de IOPS por máquina virtual y por disco son diferentes e independientes entre sí. Asegúrese de que la aplicación hello está impulsando IOPS dentro de los límites de Hola de hello VM, así como Hola premium discos conectados tooit. En caso contrario, el rendimiento de las aplicaciones experimentará una limitación.

Por ejemplo, suponga que el requisito de la aplicación es un máximo de 4.000 IOPS. tooachieve, aprovisionar un disco P30 en una máquina virtual de DS1. disco de Hello P30 puede ofrecer hasta too5, IOPS 000. Sin embargo, Hola DS1 VM es too3 limitado, 200 e/s por segundo. Por lo tanto, límite de la máquina virtual de hello en las 3.200 IOPS restringirá el rendimiento de la aplicación hello y habrá un rendimiento degradado. tooprevent esta situación, elija una máquina virtual y el tamaño que los requisitos de la aplicación cumple de disco.

*Costo de operación*  
En muchos casos, es posible que el costo general de operación con Almacenamiento premium sea inferior al uso del almacenamiento estándar.

Por ejemplo, considere una aplicación que requiere más de 16.000 IOPS. tooachieve este rendimiento, necesitará un estándar\_D14 IaaS máquina virtual de Azure, que puede permitir que un número máximo de IOPS de 16.000 con 32 discos de 1 TB de almacenamiento estándar. Cada disco de almacenamiento estándar de 1 TB puede alcanzar un máximo de 500 IOPS. Hola se calcula el costo de esta máquina virtual al mes será 1,570 $. costo mensual de Hola de 32 discos de almacenamiento estándar será 1,638 $. Hola estimado total mensual será 3,208 $.

Sin embargo, si hospeda Hola misma aplicación en almacenamiento Premium, necesitará una VM de menor tamaño y menos de los discos de almacenamiento premium, lo que reduce el costo total de Hola. Un estándar\_DS13 VM pueda cumplir los requisitos de IOPS de hello 16.000 con cuatro discos P30. Hola DS13 VM tiene un número máximo de IOPS de 25,600 y cada disco P30 tiene un número máximo de IOPS de 5.000. En general, esta configuración puede lograr 5.000 x 4 = 20.000 IOPS. Hola se calcula el costo de esta máquina virtual al mes será 1,003 $. costo mensual de Hola de cuatro discos de almacenamiento premium de P30 será 544.34 $. Hola estimado total mensual será 1,544 $.

Siguiente tabla resume el análisis de costos Hola de este escenario para Standard Edition y almacenamiento Premium.

| &nbsp; | **Standard** | **Premium** |
| --- | --- | --- |
| **Costo de máquina virtual al mes** |1570,58 USD (Standard\_D14) |1003,66 USD (Standard\_DS13) |
| **Costo de discos al mes** |1.638,40 USD (32 discos x 1 TB) |544,34 USD (4 discos x P30) |
| **Costo total al mes** |3.208,98 USD |1.544,34 USD  |

*Linux Distros*  

Con el almacenamiento de Azure Premium, obtendrá Hola mismo nivel de rendimiento para máquinas virtuales que ejecutan Windows y Linux. Se admiten muchos tipos de distribuciones de Linux, y puede ver la lista completa de hello [aquí](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Es importante toonote que diferentes distribuciones son mejores adecuado para los diferentes tipos de cargas de trabajo. Verá diferentes niveles de rendimiento en función de distribución de Hola en que la carga de trabajo se ejecuta. Hola distribuciones de Linux con la aplicación de prueba y elija Hola uno que funciona mejor.

Cuando se ejecuta Linux con el almacenamiento Premium, comprobar actualizaciones más recientes de hello sobre controladores necesarios tooensure de alto rendimiento.

## <a name="premium-storage-disk-sizes"></a>Tamaños de disco de Almacenamiento premium
Azure Premium Storage ofrece actualmente siete tamaños de disco. Cada tamaño de disco tiene un límite de escala diferente de IOPS, ancho de banda y almacenamiento. Elegir tamaño de disco de almacenamiento Premium adecuado de hello según los requisitos de la aplicación hello y tamaño de máquina virtual de gran escala de Hola. tabla de Hello siguiente muestra los tamaños de siete discos hello y sus capacidades. Los tamaños P4 y P6 solo se admiten actualmente para Managed Disks.

| Tipo de discos Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamaño del disco           | 32 GB | 64 GB | 128 GB| 512 GB            | 1.024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS por disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Rendimiento de disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo | 


El número de discos que elija depende de disco Hola tamaño elegido. Puede usar un único disco P50 o varios P10 discos toomeet el requisito de la aplicación. Tenga en cuenta consideraciones figuran al realizar la elección de Hola.

*Límites de escala (IOPS y rendimiento)*  
límites IOPS y el rendimiento de Hola de cada tamaño de disco Premium es diferente e independientes de los límites de escalado VM de Hola. Asegúrese de Hola IOPS total y el rendimiento de los discos de Hola se eligen dentro de los límites de escala del programa Hola a tamaño de máquina virtual.

Por ejemplo, si un requisito de la aplicación es un máximo de 250 MB/s de rendimiento y usa una máquina virtual DS4 con un solo disco P30. Hola DS4 VM puede abandonar el rendimiento de MB/s too256. Sin embargo, un solo disco P30 tiene límite de rendimiento de 200 MB por segundo. Por lo tanto, se restringirá aplicación hello en 200 MB/s. debido toohello límite en disco. tooovercome este límite, aprovisionar toohello de discos de datos más de una máquina virtual o cambiar el tamaño de los discos tooP40 o P50.

> [!NOTE]
> Lecturas atendidas por la memoria caché de hello no se incluyen en el disco Hola IOPS y el rendimiento, por lo tanto, no del firmante toodisk límites. La caché tiene su límite de IOPS y rendimiento independiente de la máquina virtual.
>
> Por ejemplo, inicialmente sus lecturas y escrituras son 60MB/s y 40MB/s respectivamente. Con el tiempo, caché Hola calienta y sirve cada vez más Hola lecturas de caché de Hola. A continuación, puede obtener escritura mayor rendimiento de disco de Hola.
>
>

*Número de discos*  
Determinar el número de Hola de discos que se debe al evaluar los requisitos de la aplicación. Cada tamaño de máquina virtual también tiene un límite en número de Hola de discos que puede conectar toohello máquina virtual. Normalmente, esto es dos veces el Hola número de núcleos. Asegúrese de que Hola tamaño de máquina virtual que elija puede admitir Hola número de discos necesarios.

Recuerde que los discos de almacenamiento Premium Hola tener mayor rendimiento en comparación con las capacidades tooStandard almacenamiento discos. Por lo tanto, si va a migrar la aplicación de la máquina virtual de IaaS de Azure con almacenamiento estándar tooPremium almacenamiento, probablemente, necesitará menos discos premium tooachieve Hola un rendimiento igual o superior para la aplicación.

## <a name="disk-caching"></a>Almacenamiento en caché de disco
Las máquinas virtuales a gran escala que aprovechan Almacenamiento premium de Azure tienen una tecnología de almacenamiento en caché de niveles múltiples denominada BlobCache. BlobCache utiliza una combinación de hello RAM de máquina Virtual y SSD local para almacenar en caché. Esta memoria caché está disponible para discos persistentes de almacenamiento Premium de Hola y los discos locales de VM de Hola. De forma predeterminada, esta configuración de caché se establece tooRead/escritura de discos de sistema operativo y ReadOnly para discos de datos hospedadas en almacenamiento Premium. Con disco habilitada la caché en discos de almacenamiento Premium de hello, las máquinas virtuales de gran escala de hello puede lograr muy altos niveles de rendimiento que superan el rendimiento de disco subyacente Hola.

> [!WARNING]
> Cambiar configuración de la memoria caché de Hola de un disco de Azure se desasocia y vuelve a conecta el disco de destino de Hola. Si es el disco del sistema operativo de hello, Hola VM se reinicia. Detener todas las aplicaciones o servicios que podrían verse afectados por esta interrupción antes de cambiar la configuración de caché de disco de Hola.
>
>

toolearn más información acerca de cómo funciona la BlobCache, consulte toohello dentro de [almacenamiento de Azure Premium](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/) entrada de blog.

Es importante tooenable caché en el conjunto correcto de Hola de discos. Si debe habilitar almacenamiento en caché de disco en un disco de premium o no dependerá de patrón de carga de trabajo de hello ese disco vaya a procesar. Tabla siguiente muestra la configuración de caché para discos de datos y de sistema operativo predeterminada de Hola.

| **Tipo de disco** | **Configuración de la memoria caché predeterminada** |
| --- | --- |
| Disco del sistema operativo |ReadWrite |
| Disco de datos |None |

A continuación se Hola configuración de la caché de disco recomendado para los discos de datos,

| **Configuración de almacenamiento en caché de disco** | **Recomendación sobre cuándo toouse esta configuración** |
| --- | --- |
| None |Configure la caché de host como Ninguno para los discos de solo escritura y con escritura intensiva. |
| ReadOnly |Configure la caché de host como ReadOnly para discos de solo lectura y lectura y escritura. |
| ReadWrite |Configurar la caché de host ya ReadWrite sólo si la aplicación controla correctamente la escritura en memoria caché de los discos de datos toopersistent cuando sea necesario. |

*ReadOnly*  
Mediante la configuración del almacenamiento en caché ReadOnly en discos de datos de Almacenamiento premium, puede lograr una baja latencia de lectura y obtener una IOPS de lectura y un rendimiento de la aplicación muy altos. Esto se debe a dos razones:

1. Lecturas realizadas desde la memoria caché, que está almacenados en memoria VM de Hola y SSD local, son mucho más rápidas que las lecturas de disco de datos de hello, que se encuentra en hello almacenamiento de blobs de Azure.  
2. Almacenamiento Premium no considera Hola lecturas atender las solicitudes de caché, hacia el disco de hello IOPS y el rendimiento. Por lo tanto, la aplicación es capaz de tooachieve superior total de e/s por segundo y el rendimiento.

*ReadWrite*  
De forma predeterminada, los discos de sistemas operativos de hello tienen habilitada la caché de lectura y escritura. Recientemente hemos agregado también compatibilidad para el almacenamiento en caché ReadWrite en los discos de datos. Si usa el almacenamiento en caché de lectura y escritura, debe tener una manera adecuada toowrite Hola de datos de los discos de toopersistent de caché. Por ejemplo, identificadores SQL Server escribir en memoria caché los discos de almacenamiento persistente de datos toohello por sí mismo. Usar caché de lectura y escritura con una aplicación que no controla Hola de persistencia necesaria datos puede provocar la pérdida de toodata, si se bloquea Hola VM.

Por ejemplo, puede aplicar estos tooSQL directrices Server con almacenamiento Premium haciendo Hola siguiente,

1. Configure la caché "ReadOnly" de los discos de Premium Storage que hospedan archivos de datos.  
   a.  Hola rápido lecturas de tiempo de consulta de caché inferior Hola SQL Server desde páginas de datos se recuperan mucho más rápidamente de hello caché en comparación con toodirectly de discos de datos de Hola.  
   b.  Atender las lecturas de la caché significa que hay un rendimiento adicional de los discos de datos premium. SQL Server puede usar este rendimiento adicional para recuperar más páginas de datos y otras operaciones, como copia de seguridad/restauración, cargas por lotes y volver a generar un índice.  
2. Configurar "None" archivos de registro de hospedaje Hola de discos de caché en almacenamiento premium.  
   a.  Los archivos de registro tienen sobre todo muchas operaciones de escritura. Por lo tanto, no se benefician de hello caché de solo lectura.

## <a name="disk-striping"></a>Seccionamiento del disco
Cuando puede ser una gran escala que máquina virtual esté conectada con varias premium almacenamiento persistente, discos Hola seccionados juntos tooaggregate sus IOPs, el ancho de banda y la capacidad de almacenamiento.

En Windows, puede usar discos de espacios de almacenamiento toostripe conjuntamente. Debe configurar una columna para cada disco de un grupo. En caso contrario, hello rendimiento total de volumen seccionado puede ser inferior al esperado, debido a toouneven distribución del tráfico en varios discos de Hola.

Importante: Con la UI del Administrador de servidor, puede establecer Hola número total de columnas de too8 para un volumen seccionado. Al asociar más de 8 discos, utilice volumen de hello toocreate de PowerShell. Uso de PowerShell, puede establecer a Hola número de columnas toohello igual número de discos. Por ejemplo, si hay 16 discos en un conjunto de bandas único; Especifique 16 columnas en hello *NumberOfColumns* parámetro de hello *New-VirtualDisk* cmdlet de PowerShell.

En Linux, use discos de hello MDADM utilidad toostripe conjuntamente. Para obtener pasos detallados para discos de creación de bandas en Linux, consulte demasiado[configurar RAID de Software en Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

*Tamaño de franja*  
Una configuración importante en la creación de bandas en disco es el tamaño de la sección de Hola. tamaño de sección de Hola o el tamaño de bloque es fragmento más pequeño de Hola de datos que pueda direccionar la aplicación en un volumen seccionado. tamaño de stripe de Hello que configurar depende de tipo hello de aplicación y su patrón de solicitud. Si elige un tamaño de partición incorrecto hello, podría causar desalineación tooIO, lo que conduce toodegraded rendimiento de la aplicación.

Por ejemplo, si una solicitud de E/S generada por la aplicación es mayor que el tamaño de bandas de disco de hello, sistema de almacenamiento de hello escribe en bandas los límites de la unidad en más de un disco. Cuando es tiempo tooaccess esos datos, tendrán tooseek en más de una solicitud de hello toocomplete de stripe unidades. efecto acumulado de Hola de este comportamiento puede provocar una degradación del rendimiento toosubstantial. En hello en otra parte, si Hola tamaño de la solicitud de E/S es inferior al tamaño de stripe, y si es aleatoria por naturaleza, las solicitudes de E/S de hello pueden sumar en hello mismo disco causando un cuello de botella y degradar el rendimiento de E/S de hello en última instancia.

En función del tipo hello de carga de trabajo ejecuta la aplicación, elija un tamaño de stripe adecuado. Para solicitudes de E/S pequeñas aleatorias, use un tamaño de franja más pequeño. Por otra parte, para solicitudes de E/S secuenciales grandes, use un tamaño de franja mayor. Averigüe recomendaciones de tamaño de stripe de Hola para aplicación hello que va a ejecutar en almacenamiento Premium. Para SQL Server, configure el tamaño de franja de 64 KB para cargas de trabajo OLTP y 256 KB para cargas de trabajo de almacenamiento de datos. Vea [prácticas recomendadas de rendimiento para SQL Server en máquinas virtuales de Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md#disks-guidance) toolearn más.

> [!NOTE]
> Puede seccionar conjuntamente un máximo de 32 discos de almacenamiento premium en una serie de máquinas virtuales DS y 64 discos de almacenamiento premium en una serie de máquinas virtuales GS.
>
>

## <a name="multi-threading"></a>Multithreading
Azure ha diseñado toobe de plataforma de almacenamiento Premium paralelo masivo. Por lo tanto, una aplicación multiproceso logra un rendimiento mucho mayor que una aplicación uniproceso. Una aplicación multiproceso sus tareas se divide en varios subprocesos y aumenta la eficacia de su ejecución por hello usando máquinas virtuales y toohello de recursos de disco máximo.

Por ejemplo, si la aplicación se ejecuta en un solo núcleo de máquina virtual con dos subprocesos, Hola CPU puede cambiar entre la eficacia de hello dos subprocesos tooachieve. Mientras un subproceso está esperando un toocomplete de E/S de disco, Hola CPU puede cambiar toohello otro subproceso. De esta manera, dos subprocesos pueden lograr más que un único subproceso. Si Hola VM tiene más de un núcleo, reduce aún más tiempo de ejecución ya que cada núcleo puede ejecutar tareas en paralelo.

Es posible no que forma de hello toochange capaz de una aplicación estándar implementa único subprocesos o multithreading. Por ejemplo, SQL Server es capaz de manejar varios núcleos y CPU. Sin embargo, SQL Server decide en qué condiciones aprovecharán uno o más subprocesos tooprocess una consulta. Puede ejecutar consultas y generar los índices mediante el multi-threading. Para una consulta que implica combinar tablas grandes y ordenando los datos antes de devolver el usuario toohello, SQL Server utilizará es probable que varios subprocesos. Sin embargo, un usuario no puede controlar si SQL Server se ejecuta una consulta con un único subproceso o varios subprocesos.

Hay valores de configuración que puede modificar tooinfluence este subproceso múltiple o en paralelo el procesamiento de una aplicación. Por ejemplo, en el caso de SQL Server es configuración de grado de paralelismo máxima Hola. Esta configuración llama MAXDOP, le permite el número máximo de hello tooconfigure de procesadores que se puede usar SQL Server al procesamiento en paralelo. Puede configurar MAXDOP para consultas individuales u operaciones de índice. Esto resulta útil cuando desea toobalance recursos del sistema para una aplicación crítica de rendimiento.

Por ejemplo, suponga que su aplicación mediante SQL Server ejecuta una consulta de gran tamaño y una operación de índice en hello mismo tiempo. Supongamos que deseaba toobe de operación de índice de hello más rendimiento en comparación con toohello grandes consultas. En tal caso, puede establecer el valor MAXDOP de hello toobe de operación de índice mayor que el valor MAXDOP para consulta de Hola Hola. De esta manera, SQL Server tenga un mayor número de procesadores que pueden aprovechar para hello índice operación compara toohello número de procesadores puede dedicar toohello consulta de gran tamaño. Recuerde que no se controla número Hola de subprocesos que se va a utilizar SQL Server para cada operación. Puede controlar Hola número máximo de procesadores que se va a dedicados para multithreading.

Obtenga más información sobre [Grados de paralelismo](https://technet.microsoft.com/library/ms188611.aspx) en SQL Server. Averigüe dicha configuración que influyen en los múltiples subprocesos en la aplicación y su rendimiento toooptimize de configuraciones.

## <a name="queue-depth"></a>Profundidad de la cola
Hola profundidad de cola o la longitud de cola o tamaño de la cola es el número de Hola de solicitudes de E/S pendientes en el sistema de Hola. valor de Hola de profundidad de cola determina cuántas operaciones de E/S puede alinear la aplicación, los discos de almacenamiento de Hola se van a procesar. Afecta a todos los Hola tres aplicaciones indicadores de rendimiento que se describen en este como artículo, IOPS, rendimiento y latencia.

La profundidad de la cola y multi-threading están estrechamente relacionados. Hola valor de profundidad de cola indica cuánto subprocesamiento múltiple puede lograrse mediante la aplicación hello. Si la profundidad de cola de hello es grande, aplicación pueda ejecutar más operaciones al mismo tiempo, en otras palabras, más los múltiples subprocesos. Si Hola profundidad de cola es pequeño, incluso si la aplicación es multiproceso, no tendrá suficientes solicitudes alineados para la ejecución simultánea.

Por lo general, desactivar Hola estante aplicaciones no permiten profundidad de cola de toochange hello, porque si establecido incorrectamente que va a hacer más daño que beneficio. Las aplicaciones establecerán el valor de derecho de Hola de cola profundidad tooget Hola obtener un rendimiento óptimo. Sin embargo, es importante toounderstand este concepto de modo que puede solucionar los problemas de rendimiento de la aplicación. También puede observar los efectos de Hola de profundidad de cola mediante la ejecución de pruebas comparativas de herramientas en el sistema.

Algunas aplicaciones proporcionan configuración tooinfluence Hola profundidad de cola. Por ejemplo, configuración de MAXDOP (grado máximo de paralelismo) de hello en SQL Server se explica en la sección anterior. MAXDOP es una profundidad de cola de manera tooinfluence y multithreading, aunque no cambia valor de profundidad de cola de Hola de SQL Server directamente.

*Profundidad de cola alta*  
Una profundidad de cola alta se alinee más operaciones en el disco de Hola. disco de Hello sabe siguiente solicitud de hello en su cola de antemano. Por lo tanto, disco de hello puede programar las operaciones de antemano y procesarlos en una secuencia óptimo. Puesto que la aplicación hello está enviando más capacidad de disco toohello solicitudes, disco de hello puede procesar más IOs paralelas. En última instancia, aplicación hello será capaz de tooachieve IOPS superior. Puesto que la aplicación está procesando solicitudes más, hello total de la aplicación hello también aumenta el rendimiento.

Normalmente, una aplicación puede lograr un rendimiento máximo con 8-16+ E/S pendientes para cada disco conectado. Si una profundidad de cola es uno, aplicación no se presiona un rendimiento suficiente toohello de sistema de IOs y procesará menos cantidad de en un período determinado. En otras palabras, menor rendimiento.

Por ejemplo, en SQL Server, Hola opción MAXDOP valor para una consulta demasiado "4" informa a SQL Server que puede usar una consulta de toofour núcleos tooexecute Hola. SQL Server determinará lo que es mejor cola profundidad hello y el valor de número de núcleos para la ejecución de la consulta de Hola.

*Profundidad de la cola óptima*  
Un valor de profundidad de la cola muy alto también tiene sus inconvenientes. Si el valor de profundidad de cola es demasiado alto, la aplicación hello intentará toodrive IOPS muy alto. A menos que la aplicación tiene discos persistentes con suficientes IOPS aprovisionada, esto puede afectar negativamente a las latencias de la aplicación. Después de fórmula muestran la relación de hello entre IOPS, latencia y la profundidad de cola.  
    ![](media/storage-premium-storage-performance/image6.png)

No debe configurar valor de profundidad de cola tooany alto, pero el valor óptimo de tooan, que puede entregar suficientes IOPS para la aplicación hello sin que afecte a las latencias. Por ejemplo, si la latencia de aplicación Hola necesita toobe 1 milisegundo, Hola profundidad de cola necesaria tooachieve 5.000 e/s por segundo es, PC = 5000 x 0,001 = 5.

*Profundidad de la cola para un volumen seccionado*  
Para un volumen seccionado, mantenga una profundidad de la cola lo suficientemente alta para que cada disco tenga una profundidad de la cola máxima individual. Por ejemplo, considere una aplicación que inserta una profundidad de cola de 2 y hay 4 discos en bandas de Hola. dos solicitudes de E/S Hola irá tootwo discos y restantes dos discos estará inactiva. Por lo tanto, configure la profundidad de cola Hola de manera que todos los discos de hello pueden estar ocupados. Fórmula siguiente muestra cómo toodetermine Hola profundidad de cola de un volumen seccionado.  
    ![](media/storage-premium-storage-performance/image7.png)

## <a name="throttling"></a>Limitaciones
Disposiciones de almacenamiento Premium de Azure especifica número de IOPS y el rendimiento dependiendo de los tamaños de máquinas virtuales de Hola y tamaños de disco que elija. Cada vez que la aplicación intenta toodrive e/s por segundo o un rendimiento por encima de estos límites de puede controlar qué Hola VM o un disco, se limitará almacenamiento Premium. Esto se manifiesta en forma de Hola de reducción del rendimiento de la aplicación. Esto puede significar una latencia mayor, un rendimiento menor o una IOPS menor. Si Almacenamiento premium no lo limita, la aplicación podría fallar completamente al exceder lo que sus recursos son capaces de conseguir. Por lo tanto, los problemas de rendimiento de tooavoid due toothrottling, siempre aprovisionar suficientes recursos para la aplicación. Tenga en cuenta lo que analizamos en tamaños de máquinas virtuales de Hola y secciones de tamaños de disco anteriores. Pruebas comparativas son Hola mejor manera toofigure qué recursos debe toohost la aplicación.

## <a name="benchmarking"></a>Pruebas comparativas
Pruebas comparativas son el proceso de Hola de simular diferentes cargas de trabajo en la aplicación y medir el rendimiento de la aplicación de Hola para cada carga de trabajo. Siguiendo los pasos de hello descritos en una sección anterior, que recopile requisitos de rendimiento de aplicaciones de Hola. Al ejecutar pruebas comparativas herramientas en máquinas virtuales de Hola que hospeda la aplicación hello, puede determinar los niveles de rendimiento de Hola que la aplicación puede lograr con almacenamiento Premium. En esta sección se proporcionan ejemplos de pruebas comparativas realizados con una máquina virtual estándar de DS14 aprovisionada con discos de Almacenamiento premium de Azure.

Hemos usado las herramientas de pruebas comparativas comunes Iometer y FIO, para Windows y Linux respectivamente. Estas herramientas generan varios subprocesos simulando una carga de trabajo y rendimiento del sistema de medida Hola de producción. Usar herramientas de hello también puede configurar parámetros como profundidad tamaño y la cola del bloque, que normalmente no se puede cambiar de una aplicación. Esto le ofrece más flexibilidad toodrive Hola obtener el máximo rendimiento en una máquina virtual proporcionado con discos premium para diferentes tipos de cargas de trabajo de aplicación de gran escala. toolearn sobre cada herramienta de pruebas comparativas, visite [Iometer](http://www.iometer.org/) y [FIO](http://freecode.com/projects/fio).

ejemplos de hello toofollow siguientes, cree una VM de DS14 estándar y adjuntar 11 toohello de discos de almacenamiento Premium máquina virtual. De los discos de hello 11, configurar 10 discos con almacenamiento en caché como "None" de host y crear bandas de ellos en un volumen denominado NoCacheWrites. Configurar almacenamiento en caché como "ReadOnly" en disco restante Hola de host y crear un volumen denominado CacheReads con este disco. Con esta configuración, es posible que pueda toosee Hola de lectura y escritura rendimiento máximo de una máquina virtual de DS14 estándar. Para obtener pasos detallados acerca de cómo crear una máquina virtual DS14 con discos premium, vaya demasiado[crear y usar un almacenamiento Premium de cuenta para un disco de datos de la máquina virtual](storage-premium-storage.md).

*Preparando Hola caché*  
Hola disco con almacenamiento en caché de host de solo lectura va a ser capaz de toogive IOPS mayor que el límite de hello en disco. tooget este valor máximo rendimiento de las lecturas de caché de host de hello, primero debe caliente caché Hola de este disco. Esto garantiza que ese Hola IOs de lectura provoquen qué herramienta de pruebas comparativas en volumen de CacheReads realmente aciertos de caché hello y no el disco de hello directamente. resultado de aciertos de caché de Hello en adicionales de IOPS desde la memoria caché única Hola habilitado disco.

> **Importante:**  
> Debe calentar la memoria caché de hello antes de ejecutar pruebas comparativas, cada vez que se reinicia la máquina virtual.
>
>

#### <a name="iometer"></a>Iometer
[Descargar la herramienta de hello Iometer](http://sourceforge.net/projects/iometer/files/iometer-stable/2006-07-27/iometer-2006.07.27.win32.i386-setup.exe/download) en hello máquina virtual.

*Archivo de prueba*  
Iometer usa un archivo de prueba que se almacena en el volumen de hello en el que se ejecutará Hola pruebas comparativas de prueba. Unidades de lecturas y escrituras en el objeto de prueba IOPS del disco de toomeasure Hola de archivo y el rendimiento. Iometer crea este archivo de prueba si no proporcionó ninguno. Crear un archivo de prueba de 200GB llamado iobw.tst en volúmenes de hello CacheReads y NoCacheWrites.

*Especificaciones de acceso*  
Hello especificaciones, solicitud de tamaño de E/S, % de lectura/escritura, % aleatorias o secuenciales se configuran con pestaña de "Especificaciones de Access" hello en Iometer. Crear una especificación de acceso para cada uno de los escenarios de Hola que se describe a continuación. Crear las especificaciones de acceso de Hola y "Guardar" con un nombre como – RandomWrites\_8K, RandomReads\_8 K. Seleccionar especificación correspondiente hello cuando ejecute el escenario de prueba de Hola.

A continuación se muestra un ejemplo de especificaciones de acceso para el escenario de IOPS de escritura máxima:   
    ![](media/storage-premium-storage-performance/image8.png)

*Especificaciones de prueba de IOPS máxima*  
toodemonstrate máximo IOPs, utilice el menor tamaño de la solicitud. Use el tamaño de solicitud de 8K y cree especificaciones de lecturas y escrituras aleatorias.

| Especificación de acceso | Tamaño de la solicitud | % aleatorio | % lectura |
| --- | --- | --- | --- |
| RandomWrites\_8K |8 K |100 |0 |
| RandomReads\_8K |8 K |100 |100 |

*Especificaciones de prueba de rendimiento máximo*  
toodemonstrate rendimiento máximo, el tamaño de solicitud de uso. Use el tamaño de la solicitud de 64 KB y cree especificaciones de lecturas y escrituras aleatorias.

| Especificación de acceso | Tamaño de la solicitud | % aleatorio | % lectura |
| --- | --- | --- | --- |
| RandomWrites\_64K |64 K |100 |0 |
| RandomReads\_64K |64 K |100 |100 |

*Ejecutando prueba Iometer Hola*  
Realizar estos pasos hello toowarm la memoria caché

1. Cree dos especificaciones de acceso con los valores que se muestran a continuación:

   | Nombre | Tamaño de la solicitud | % aleatorio | % lectura |
   | --- | --- | --- | --- |
   | RandomWrites\_1MB |1MB |100 |0 |
   | RandomReads\_1MB |1MB |100 |100 |
2. Ejecutar prueba de Iometer Hola para inicializar el disco de la caché con los siguientes parámetros. Utilice tres subprocesos de trabajo para el volumen de destino de hello y una profundidad de cola de 128. Establecer Hola "Tiempo de ejecución" duración de hello too2hrs de prueba en la pestaña de "Probar el programa de instalación" Hola.

   | Escenario | Volumen de destino | Nombre | Duración |
   | --- | --- | --- | --- |
   | Inicializar caché de disco |CacheReads |RandomWrites\_1MB |2 horas |
3. Ejecutar prueba de Iometer Hola para preparar el disco de la caché con los siguientes parámetros. Utilice tres subprocesos de trabajo para el volumen de destino de hello y una profundidad de cola de 128. Establecer Hola "Tiempo de ejecución" duración de hello too2hrs de prueba en la pestaña de "Probar el programa de instalación" Hola.

   | Escenario | Volumen de destino | Nombre | Duración |
   | --- | --- | --- | --- |
   | Preparación de la caché de disco |CacheReads |RandomReads\_1MB |2 horas |

Después de disco de la caché se activa, continúe con los escenarios de prueba de hello enumerados a continuación. Hola toorun Iometer prueba, utilice al menos tres subprocesos de trabajo para **cada** volumen de destino. Para cada subproceso de trabajo, seleccione el volumen de destino hello, establecer la profundidad de cola y seleccione una de las especificaciones de prueba Hola guarda, como se muestra en la tabla de Hola a continuación el escenario de prueba de toorun Hola correspondiente. Hola tabla también muestra resultados esperados para IOPS y el rendimiento al ejecutar estas pruebas. Para todos los escenarios, se usa un tamaño pequeño de E/S de 8 KB y una profundidad de la cola alta de 128.

| Escenario de prueba | Volumen de destino | Nombre | Resultado |
| --- | --- | --- | --- |
| Máx. IOPS de lectura |CacheReads |RandomWrites\_8K |50.000 E/S por segundo  |
| Máx. IOPS de escritura |NoCacheWrites |RandomReads\_8K |64.000 IOPS |
| Máx. IOPS combinado |CacheReads |RandomWrites\_8K |100.000 IOPS |
| NoCacheWrites |RandomReads\_8K | &nbsp; | &nbsp; |
| Máx. MB/s de lectura |CacheReads |RandomWrites\_64K |524 MB/s |
| Máx. Escritura MB/s |NoCacheWrites |RandomReads\_64K |524 MB/s |
| Combinado MB/s |CacheReads |RandomWrites\_64K |1000 MB/s |
| NoCacheWrites |RandomReads\_64K | &nbsp; | &nbsp; |

A continuación se muestran capturas de pantalla de hello Iometer resultados de pruebas para escenarios combinados de IOPS y el rendimiento.

*IOPS máxima de lectura y escritura combinada*  
![](media/storage-premium-storage-performance/image9.png)

*Rendimiento máximo de lectura y escritura combinado*  
![](media/storage-premium-storage-performance/image10.png)

### <a name="fio"></a>FIO
FIO es una herramienta popular toobenchmark de almacenamiento en hello máquinas virtuales de Linux. Tiene tooselect de flexibilidad de Hola de diferentes tamaños de E/S, lecturas aleatorias o secuenciales y escrituras. Genera subprocesos de trabajo u Hola de procesos tooperform especifica las operaciones de E/S. Puede especificar tipo de Hola de operaciones de E/S que cada subproceso de trabajo debe realizar al usar archivos de trabajo. Hemos creado un archivo de trabajo por escenario mostrado en los ejemplos de hello siguientes. Puede cambiar las especificaciones de hello en estos trabajos archivos toobenchmark diferentes cargas de trabajo almacenamiento Premium. En los ejemplos de hello, estamos usando una ejecución de una máquina de 14 DS estándar **Ubuntu**. Hola use el mismo programa de instalación se describe en principio Hola de hello [pruebas comparativas sección](#Benchmarking) y activa la memoria caché de hello antes de ejecutar Hola pruebas comparativas de pruebas.

Antes de comenzar, [descargue FIO](https://github.com/axboe/fio) e instálelo en la máquina virtual.

Ejecute hello siguiente comando para Ubuntu,

```
apt-get install fio
```

Usaremos cuatro subprocesos de trabajo para controlar las operaciones de escritura y cuatro subprocesos de trabajo para las operaciones de lectura determinante en discos de Hola. Hello los trabajadores de la escritura se se imponen el tráfico en el volumen nocache"hello", que tiene 10 discos con memoria caché establecida demasiado "None". Hello los trabajadores de la lectura se se imponen el tráfico en volumen de readcache"hello", que tiene 1 disco con la memoria caché demasiado "ReadOnly".

*IOPS de escritura máxima*  
Crear archivo de trabajo de hello con tooget de las especificaciones siguientes máximo de IOPS de escritura. Asígnele el nombre "fiowrite.ini".

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[writer1]
rw=randwrite
directory=/mnt/nocache
[writer2]
rw=randwrite
directory=/mnt/nocache
[writer3]
rw=randwrite
directory=/mnt/nocache
[writer4]
rw=randwrite
directory=/mnt/nocache
```

Hola Nota siga conceptos clave que hay que estén en consonancia con las instrucciones de diseño de Hola se describe en secciones anteriores. Estas especificaciones son esencial toodrive número máximo de IOPS,  

* Una profundidad de la cola alta de 256.  
* Un tamaño de bloque pequeño de 8 KB.  
* Varios subprocesos que realizan escrituras aleatorias.

Ejecute hello después tookick comando desactivar hello FIO de prueba de 30 segundos,  

```
sudo fio --runtime 30 fiowrite.ini
```

Mientras se ejecuta la prueba de hello, será capaz de toosee número de Hola de entrega de los discos de máquina virtual y Premium de Hola IOPS de escritura. Como se muestra en el siguiente ejemplo de Hola, hello DS14 VM está proporcionando su límite de IOPS de 50.000 IOPS máxima de escritura.  
    ![](media/storage-premium-storage-performance/image11.png)

*IOPS de lectura máxima*  
Crear archivo de trabajo de hello con tooget de las especificaciones siguientes número máximo de IOPS de lectura. Asígnele el nombre "fioread.ini".

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache
```

Hola Nota siga conceptos clave que hay que estén en consonancia con las instrucciones de diseño de Hola se describe en secciones anteriores. Estas especificaciones son esencial toodrive número máximo de IOPS,

* Una profundidad de la cola alta de 256.  
* Un tamaño de bloque pequeño de 8 KB.  
* Varios subprocesos que realizan escrituras aleatorias.

Ejecute hello después tookick comando desactivar hello FIO de prueba de 30 segundos,

```
sudo fio --runtime 30 fioread.ini
```

Mientras se ejecuta la prueba de hello, usted será el número de hello toosee capaz de lectura de e/s por segundo de hello VM y discos Premium se entrega. Como se muestra en el siguiente ejemplo de Hola, hello DS14 VM está proporcionando 64.000 más de IOPS de lectura. Se trata de una combinación de disco de Hola y el rendimiento de la caché de Hola.  
    ![](media/storage-premium-storage-performance/image12.png)

*IOPS de lectura y escritura máxima*  
Crear archivo de trabajo de hello con siguiente tooget especificaciones máximo combinado de lectura y escritura de e/s por segundo. Asígnele el nombre "fioreadwrite.ini".

```
[global]
size=30g
direct=1
iodepth=128
ioengine=libaio
bs=4k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache

[writer1]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer2]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer3]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer4]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
```

Hola Nota siga conceptos clave que hay que estén en consonancia con las instrucciones de diseño de Hola se describe en secciones anteriores. Estas especificaciones son esencial toodrive número máximo de IOPS,

* Una profundidad de la cola alta de 128.  
* Un tamaño de bloque pequeño de 4 KB.  
* Varios subprocesos que realizan lecturas y escrituras aleatorias.

Ejecute hello después tookick comando desactivar hello FIO de prueba de 30 segundos,

```
sudo fio --runtime 30 fioreadwrite.ini
```

Mientras se ejecuta la prueba de hello, se ser capaz de toosee Hola número de lectura combinado y IOPS de escritura Hola VM y entrega los discos Premium. Tal y como se muestra en el siguiente ejemplo de Hola, hello DS14 VM ofrece más de 100.000 lectura combinado e IOPS de escritura. Se trata de una combinación de disco de Hola y el rendimiento de la caché de Hola.  
    ![](media/storage-premium-storage-performance/image13.png)

*Rendimiento máximo combinado*  
Hola tooget máximo combina lectura y la velocidad de escritura, use un tamaño de bloque mayor y la profundidad de cola grande con varios subprocesos realizar lecturas y escrituras. Puede usar un tamaño de bloque de 64 KB y una profundidad de la cola de 128.

## <a name="next-steps"></a>Pasos siguientes
Más información sobre Almacenamiento premium de Azure:

* [Almacenamiento premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](storage-premium-storage.md)  

Para los usuarios de SQL Server, lea artículos sobre procedimientos recomendados para SQL Server:

* [Procedimientos recomendados para SQL Server en Máquinas virtuales de Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)
* [Almacenamiento premium de Azure proporciona el máximo rendimiento para SQL Server en una máquina virtual de Azure](http://blogs.technet.com/b/dataplatforminsider/archive/2015/04/23/azure-premium-storage-provides-highest-performance-for-sql-server-in-azure-vm.aspx)
