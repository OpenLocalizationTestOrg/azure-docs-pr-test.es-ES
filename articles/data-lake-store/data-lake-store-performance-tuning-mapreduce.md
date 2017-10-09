---
title: "aaaAzure datos Lake almacén MapReduce Performance Tuning Guidelines | Documentos de Microsoft"
description: "Directrices para la optimización del rendimiento de MapReduce en Azure Data Lake Store"
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
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a>Guía para optimizar el rendimiento de MapReduce en HDInsight y Azure Data Lake Store


## <a name="prerequisites"></a>Requisitos previos

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Una cuenta de Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)
* **Clúster de HDInsight de Azure** con acceso tooa cuenta de almacén de Data Lake. Consulte [Creación de un clúster de HDInsight con Data Lake Store mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Asegúrese de que habilitar Escritorio remoto para el clúster de Hola.
* **Uso de MapReduce en HDInsight**.  Para más información, consulte [Uso de MapReduce en Hadoop en HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce).  
* **Directrices para la optimización del rendimiento en ADLS**.  Para conocer los conceptos generales de rendimiento, consulte [Guía para la optimización del rendimiento de Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="parameters"></a>parameters

Al ejecutar los trabajos de MapReduce, estos son parámetros de hello más importantes que se puede configurar rendimiento tooincrease en ADLS:

* **MapReduce.Map.Memory.MB** : cantidad de Hola de asignador de memoria tooallocate tooeach
* **MapReduce.job.Maps** : Hola número de tareas de asignación por trabajo
* **MapReduce.reduce.Memory.MB** : cantidad de Hola de reductor de memoria tooallocate tooeach
* **MapReduce.job.reduces** : Hola número de tareas de reducción por trabajo

**MapReduce.Map.Memory / Mapreduce.reduce.memory** este número debe ajustarse según la cantidad de memoria se necesita para asignación de Hola o reducir la tarea.  valores predeterminados de Hola de mapreduce.map.memory y mapreduce.reduce.memory pueden verse en Ambari mediante la configuración de Yarn Hola.  En Ambari, navegue tooYARN y ver la ficha de configuraciones de Hola.  Hola memoria YARN se mostrará.  

**MapReduce.job.Maps / Mapreduce.job.reduces** Esto determinará el número máximo de Hola de asignadores o reductores toobe creado.  número de Hola de divisiones determinará cuántas asignadores se creará para el trabajo de MapReduce Hola.  Por lo tanto, es posible que obtenga a menos asignadores que solicitado si hay menos divisiones que número Hola de asignadores solicitado.       

## <a name="guidance"></a>Guía

**Paso 1: Determinar el número de trabajos que se ejecutan** : de forma predeterminada, MapReduce usará clúster completo de hello para el trabajo.  Puede utilizar menos del clúster de hello mediante menos asignadores de contenedores disponibles.  Guía de Hello en este documento se da por supuesto que la aplicación es la única aplicación hello en ejecución en el clúster.      

**Paso 2: Configurar mapreduce.map.memory/mapreduce.reduce.memory** : Hola tamaño de memoria de Hola de mapa y reducir las tareas estarán depende de su trabajo específico.  Puede reducir el tamaño de la memoria de Hola si desea tooincrease simultaneidad.  número de Hola de tareas en ejecución al mismo tiempo depende de número de Hola de contenedores.  Reduciendo la cantidad de Hola de memoria por el asignador o reductor, pueden crearse varios contenedores, que hacen más toorun asignadores o reductores simultáneamente.  Cantidad de hello en disminución de memoria demasiado puede provocar algunos toorun de procesos, memoria insuficiente.  Si recibe un error de montón cuando se ejecuta el trabajo, debe aumentar la memoria de Hola por el asignador o reductor.  Debe tener en cuenta que agregar más contenedores supondrá una sobrecarga adicional para cada contenedor de más, lo que podría reducir el rendimiento.  Otra alternativa es tooget más memoria usando un clúster que tiene la mayor cantidad de memoria o aumentar el número de Hola de nodos en el clúster.  Más memoria, habilitará más toobe contenedores usado, lo que significa más de simultaneidad.  

**Paso 3: Determinar la memoria Total YARN** -tootune mapreduce.job.maps/mapreduce.job.reduces, conviene cantidad Hola de memoria YARN total disponible para su uso.  Esta información está disponible en Ambari.  Navegue tooYARN y ver la ficha de configuraciones de Hola.  Hola memoria YARN se muestra en esta ventana.  Debe multiplicar memoria YARN Hola con número de Hola de nodos en la memoria total de hilo de clúster tooget Hola.

    Total YARN memory = nodes * YARN memory per node
Si está usando un clúster vacío, la memoria puede ser Hola hilo de memoria total para el clúster.  Si otras aplicaciones están utilizando la memoria, puede elegir usar tooonly parte de la memoria de su clúster reduciendo el número de Hola de asignadores o reductores toohello el número de contenedores que desee toouse.  

**Paso 4: Calcular el número de contenedores YARN** : contenedores de hilo dictan cantidad Hola de simultaneidad disponible para el trabajo de Hola.  Tome la memoria de YARN total y divídala entre el valor de mapreduce.map.memory.  

    # of YARN containers = total YARN memory / mapreduce.map.memory

**Paso 5: Establecer mapreduce.job.maps/mapreduce.job.reduces** establecer mapreduce.job.maps/mapreduce.job.reduces tooat menor número de Hola de contenedores disponibles.  Puede experimentar más si aumenta el número de Hola de asignadores y reductores toosee si obtener un mejor rendimiento.  Tenga en cuenta que cuantos más asignadores más sobrecarga, por lo que tener demasiados asignadores puede reducir el rendimiento.  

Programación de CPU y el aislamiento de CPU están desactivadas de forma predeterminada para que el número de Hola de contenedores YARN está restringido por la memoria.

## <a name="example-calculation"></a>Cálculo de ejemplo

Supongamos que tiene actualmente un clúster compuesto de 8 nodos D14 y desea toorun un trabajo de uso intensivo de E/S.  Estos son los cálculos de Hola que se debe realizar:

**Paso 1: Determinar el número de trabajos que se ejecutan** -en nuestro ejemplo, suponemos que nuestro trabajo es Hola único en ejecución.  

**Paso 2: Configuración de mapreduce.map.memory/mapreduce.reduce.memory**: en nuestro ejemplo, está ejecutando un trabajo de uso intensivo de E/S y decide que 3 GB de memoria para las tareas de asignación será suficiente.

    mapreduce.map.memory = 3GB
**Paso 3: Determinación de la memoria de YARN total**

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
**Paso 4: Cálculo del número de contenedores de YARN**

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

**Paso 5: Establecer mapreduce.job.maps/mapreduce.job.reduces**

    mapreduce.map.jobs = 256

## <a name="limitations"></a>Limitaciones

**Limitación de ADLS**

Como servicio multiinquilino, ADLS establece los límites de ancho de banda de nivel de cuenta.  Si se produce estos límites, se iniciará toosee errores en la tarea. Para identificar esta situación, observe los errores de limitación en los registros de tareas.  Si necesita más ancho de banda para su trabajo, póngase en contacto con nosotros.   

toocheck si están obteniendo limitados, deberá tooenable Hola registro de depuración en el lado del cliente de Hola. Así es cómo debe hacerlo:

1. Put hello después de propiedad en las propiedades de log4j hello en Ambari > YARN > Configuración > avanzado log4j hilo: log4j.logger.com.microsoft.azure.datalake.store=DEBUG

2. Reiniciar todos los nodos de Hola/servicio con efecto de hello config tootake.

3. Si están obteniendo limitados, verá el código de error HTTP 429 hello en el archivo de registro de hello YARN. archivo de registro de Hello YARN está en /tmp/&lt;usuario&gt;/yarn.log

## <a name="examples-toorun"></a>Ejemplos tooRun

toodemonstrate cómo MapReduce se ejecuta en el almacén de Data Lake de Azure, a continuación se muestra algún código de ejemplo que se ha ejecutado en un clúster con hello después de configuración:

* 16 nodos D14v2
* Clúster de Hadoop con HDI 3.6

Para un punto de partida, estas son algunas toorun de comandos de ejemplo MapReduce Teragen, Terasort y Teravalidate.  Puede ajustar estos comandos en función de los recursos.

**Teragen**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

**Terasort**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

**Teravalidate**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
