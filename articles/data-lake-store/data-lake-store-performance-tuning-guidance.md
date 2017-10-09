---
title: "Directrices de ajuste de rendimiento de datos Lake almacén aaaAzure | Documentos de Microsoft"
description: "Directrices para la optimización del rendimiento de Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: cgronlun
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: stewu
ms.openlocfilehash: 939faa068c0f81d18d9533956f4d336bc4d0cbe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-azure-data-lake-store-for-performance"></a>Optimización del rendimiento de Azure Data Lake Store

Data Lake Store permite un alto rendimiento en el movimiento de datos y el análisis de consumo de la entrada y salida.  En el almacén de Data Lake de Azure, el uso de rendimiento disponible: cantidad de Hola de datos que pueden leer o escritos por segundo: es un rendimiento óptimo hello tooget importante.  Se consigue realizando tantas lecturas y escrituras en paralelo como sea posible.

![Rendimiento de Data Lake Store](./media/data-lake-store-performance-tuning-guidance/throughput.png)

Almacén de Azure Data Lake puede escalar tooprovide hello es necesario el rendimiento para todos los escenario de análisis. De forma predeterminada, una cuenta de almacén de Data Lake de Azure proporciona automáticamente suficiente rendimiento necesidades de hello toomeet de una categoría amplia de casos de uso. Para los casos de Hola donde los clientes se ejecutan en el límite predeterminado de hello, Hola cuenta ADLS puede ser tooprovide configurado más rendimiento por ponerse en contacto con soporte técnico de Microsoft.

## <a name="data-ingestion"></a>Ingesta de datos

Cuando se recopila datos de un tooADLS de sistema de origen, es importante tooconsider que Hola tooADLS de conectividad de red, hardware de red de origen y hardware de origen puede ser un cuello de botella de Hola.  

![Rendimiento de Data Lake Store](./media/data-lake-store-performance-tuning-guidance/bottleneck.png)

Es importante tooensure que Hola movimiento de datos no se ve afectado por estos factores.

### <a name="source-hardware"></a>Hardware de origen

Si usas máquinas locales o máquinas virtuales en Azure, debe seleccionar cuidadosamente hardware adecuado Hola. Para Hardware de disco de origen, prefiera SSD tooHDDs y elegir el hardware del disco con ejes más rápidos. Para el Hardware de red de origen, utilice más rápido posible de NIC Hola.  En Azure, se recomienda que las máquinas virtuales de Azure D14 que tienen disco adecuadamente eficaz de Hola y hardware de red.

### <a name="network-connectivity-tooazure-data-lake-store"></a>Almacén de Data Lake de tooAzure de conectividad de red

conectividad de red de Hello entre los datos de origen y el almacén de Azure Data Lake a veces puede ser un cuello de botella de Hola. Cuando los datos de origen están en local, considere el uso de un vínculo dedicado con [Azure ExpressRoute](https://azure.microsoft.com/en-us/services/expressroute/). Si los datos de origen están en Azure, el rendimiento de hello será mejor cuando los datos de Hola Hola misma región de Azure como almacén de Data Lake Hola.

### <a name="configure-data-ingestion-tools-for-maximum-parallelization"></a>Configuración de herramientas de ingesta de datos para lograr una paralelización máxima

Una vez que se ha solucionado el hardware de origen de Hola y anteriores cuellos de botella de conectividad de red, está listo tooconfigure las herramientas de recopilación. Hello tabla siguiente resume las opciones de clave de hello varias herramientas de ingesta populares y ofrece un rendimiento detallado para la optimización de artículos para ellos.  toolearn más acerca de qué herramienta toouse para su escenario, visite este [artículo](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-data-scenarios).

| Herramienta               | Configuración     | Más detalles                                                                 |
|--------------------|------------------------------------------------------|------------------------------|
| PowerShell       | PerFileThreadCount, ConcurrentFileCount |  [Vínculo](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-powershell#performance-guidance-while-using-powershell)   |
| AdlCopy    | Unidades de Azure Data Lake Analytics  |   [Vínculo](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob#performance-considerations-for-using-adlcopy)         |
| DistCp            | -m (mapper)   | [Vínculo](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-wasb-distcp#performance-considerations-while-using-distcp)                             |
| Azure Data Factory| parallelCopies    | [Vínculo](../data-factory/data-factory-copy-activity-performance.md)                          |
| Sqoop           | fs.azure.block.size, -m (mapper)    |   [Vínculo](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)        |

## <a name="structure-your-data-set"></a>Estructuración del conjunto de datos

Cuando los datos se almacenan en el almacén de Data Lake, tamaño del archivo hello, número de archivos y la estructura de carpetas tiene un impacto en el rendimiento.  Hello siguiente sección describe los procedimientos recomendados en estas áreas.  

### <a name="file-size"></a>Tamaño de archivo

Normalmente, los motores de análisis como HDInsight y Azure Data Lake Analytics tienen una sobrecarga por cada archivo.  Si los datos se almacenan en muchos archivos pequeños, puede afectar desfavorablemente al rendimiento.  

En general, organice los datos en archivos de un tamaño mayor para mejorar el rendimiento.  Como regla general, organice los conjuntos de datos en archivos de 256 MB o más. En algunos casos, como imágenes y datos binarios, no es posible tooprocess ellas en paralelo.  En estos casos, se recomienda archivos individuales de tookeep menos de 2GB.

A veces, las canalizaciones de datos tiene un control limitado sobre datos sin procesar de hello, que tiene una gran cantidad de archivos pequeños.  Se recomienda toohave proceso "cocina" que genera más grandes archivos toouse para aplicaciones de nivel inferior.  

### <a name="organizing-time-series-data-in-folders"></a>Organización de los datos de serie temporal en carpetas

Las cargas de trabajo de Hive y ADLA, eliminación de la partición de datos de series temporales puede ayudar a algunas consultas solo un subconjunto de datos de Hola que mejora el rendimiento de lectura.    

Aquellas canalizaciones que ingieren datos de serie temporal suelen ubicar sus archivos con una nomenclatura muy estructurada para los archivos y las carpetas. A continuación se muestra un ejemplo muy común para los datos estructurados por fecha:

    \DataSet\YYYY\MM\DD\datafile_YYYY_MM_DD.tsv

Observe que la información de fecha y hora de hello aparece como carpetas y en el nombre de archivo de Hola.

Fecha y hora, de hello aquí te mostramos un patrón común

    \DataSet\YYYY\MM\DD\HH\mm\datafile_YYYY_MM_DD_HH_mm.tsv

De nuevo, elección de Hola que haga con la organización de carpetas y archivos de hello debería optimizar para los tamaños de archivo más grandes de Hola y un número razonable de archivos de cada carpeta.

## <a name="optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight"></a>Optimización de trabajos con muchas operaciones de E/S en las cargas de trabajo de Hadoop y Spark en HDInsight

Los trabajos se dividen en uno de los siguientes tres categorías de hello:

* **Gran uso de CPU.**  Estos trabajos tienen tiempos de cálculo largos con tiempos de E/S mínimos.  Algunos ejemplos son los trabajos de procesamiento del lenguaje natural y el aprendizaje automático.  
* **Gran uso de memoria.**  Estos trabajos usan una gran cantidad de memoria.  Algunos ejemplos son los trabajos de análisis en tiempo real y PageRank.  
* **Gran uso de operaciones de E/S.**  Estos trabajos dedican la mayor parte de su tiempo a realizar operaciones de E/S.  Un ejemplo común es un trabajo de copia que solo realice operaciones de lectura y escritura.  Otros ejemplos incluyen los trabajos de preparación de datos que leer una gran cantidad de datos, realice alguna transformación de datos y, a continuación, escribe Hola almacén de datos de back-toohello.  

Hola instrucciones es solo es aplicable tooI/O intensivo los trabajos.

### <a name="general-considerations-for-an-hdinsight-cluster"></a>Consideraciones generales para un clúster de HDInsight

* **Versiones de HDInsight.** Para obtener el mejor rendimiento, usar Hola última versión de HDInsight.
* **Regiones.** Coloque el almacén de Data Lake de hello en hello misma región que el clúster de HDInsight Hola.  

Un clúster de HDInsight se compone de dos nodos principales y algunos nodos de trabajo. Cada nodo de trabajo proporciona un número específico de núcleos y memoria, lo que viene determinada por hello tipo de máquina virtual.  Cuando se ejecuta un trabajo, YARN es negociador de recursos de Hola que asigna memoria disponible de Hola y contenedores de toocreate de núcleos.  Cada contenedor ejecuta trabajo Hola de hello tareas toocomplete necesarios.  Los contenedores se ejecutan en paralelo tooprocess tareas rápidamente. Por lo tanto, el rendimiento se mejora ejecutando tantos contenedores en paralelo como sea posible.

Hay tres capas dentro de un clúster de HDInsight que pueden estar atento tooincrease Hola número de contenedores y usar rendimiento todas disponible.  

* **Nivel físico**
* **Nivel de YARN**
* **Nivel de carga de trabajo**

### <a name="physical-layer"></a>Nivel físico

**Ejecute el clúster con más nodos o máquinas virtuales de un tamaño mayor.**  Un clúster mayor permitirá toorun más contenedores YARN tal como se muestra en figura Hola siguiente.

![Rendimiento de Data Lake Store](./media/data-lake-store-performance-tuning-guidance/VM.png)

**Use máquinas virtuales con más ancho de banda de red.**  cantidad de Hola de ancho de banda de red puede ser un cuello de botella si hay menos ancho de banda de red que el rendimiento de almacén de Data Lake.  Diferentes máquinas virtuales tendrán varios tamaños de ancho de banda de red.  Elija un tipo de máquina virtual que tiene hello más grande posible el ancho de banda.

### <a name="yarn-layer"></a>Nivel de YARN

**Use contenedores de YARN menores.**  Reducir tamaño de Hola de cada toocreate de contenedor YARN más contenedores con hello misma cantidad de recursos.

![Rendimiento de Data Lake Store](./media/data-lake-store-performance-tuning-guidance/small-containers.png)

En función de la carga de trabajo, siempre habrá un tamaño de contenedor de YARN mínimo que se necesite. Si elige un contenedor demasiado pequeño, los trabajos no tendrán memoria suficiente. Normalmente, los contenedores de YARN no deben ser menores de 1 GB. Es común contenedores YARN de toosee / 3GB. Para algunas cargas de trabajo, puede que necesite contenedores de YARN mayores.  

**Aumente los núcleos para cada contenedor de YARN.**  Aumentar el número de Hola de núcleos tooeach contenedor tooincrease Hola número de tareas en paralelo que se ejecutan en cada contenedor asignado.  Funciona en las aplicaciones como Spark que ejecutan varias tareas por contenedor.  Para aplicaciones como Hive que ejecutan un solo subproceso en cada contenedor, es mejor toohave más contenedores en lugar de varios núcleos por contenedor.   

### <a name="workload-layer"></a>Nivel de carga de trabajo

**Use todos los contenedores disponibles.**  Establecer número de Hola de tareas toobe igual o mayor que el número de Hola de contenedores disponibles para que se utilizan todos los recursos.

![Rendimiento de Data Lake Store](./media/data-lake-store-performance-tuning-guidance/use-containers.png)

**Los errores de las tareas son costosos.** Si cada tarea tiene una gran cantidad de datos tooprocess, a continuación, error de una tarea produce un reintento costoso.  Por lo tanto, es mejor toocreate más tareas, cada uno de ellos procesa una pequeña cantidad de datos.

En suma toohello general directrices indicadas anteriormente, cada aplicación tiene parámetros diferentes tootune disponibles para esa aplicación específica. tabla de Hello siguiente muestra algunas de hello tooget de parámetros y los vínculos a trabajar con el ajuste del rendimiento para cada aplicación.

| Carga de trabajo               | Tareas de tooset de parámetro                                                         |
|--------------------|-------------------------------------------------------------------------------------|
| [Spark en HDInisight](data-lake-store-performance-tuning-spark.md)       | <ul><li>Num-executors</li><li>Memoria del ejecutor</li><li>Executor-cores</li></ul> |
| [Hive en HDInsight](data-lake-store-performance-tuning-hive.md)    | <ul><li>hive.tez.container.size</li></ul>         |
| [MapReduce en HDInsight](data-lake-store-performance-tuning-mapreduce.md)            | <ul><li>Mapreduce.map.memory</li><li>Mapreduce.job.maps</li><li>Mapreduce.reduce.memory</li><li>Mapreduce.job.reduces</li></ul> |
| [Storm en HDInsight](data-lake-store-performance-tuning-storm.md)| <ul><li>Número de procesos de trabajo</li><li>Número de instancias de ejecutor de spout</li><li>Número de instancias de ejecutor de bolt </li><li>Número de tareas de spout</li><li>Número de tareas de bolt</li></ul>|

## <a name="see-also"></a>Consulte también
* [Información general del Almacén de Azure Data Lake](data-lake-store-overview.md)
* [Tutorial: Introducción a Análisis de Azure Data Lake mediante el Portal de vista previa de Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
