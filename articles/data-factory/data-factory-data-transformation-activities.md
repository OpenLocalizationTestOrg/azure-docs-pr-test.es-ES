---
title: "Transformación de datos: procesamiento y transformación de datos| Microsoft Docs"
description: "Obtenga información acerca de cómo tootransform datos o procesar los datos de Data Factory de Azure con Hadoop, aprendizaje automático o análisis de Data Lake de Azure."
keywords: "transformación de datos, procesar datos, transformar datos, actividad de transformación"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 917d617259699b0e71de3a0e0c17463d00f2e0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-in-azure-data-factory"></a>Transformar datos en Azure Data Factory
> [!div class="op_single_selector"]
> * [Hive](data-factory-hive-activity.md)  
> * [Pig](data-factory-pig-activity.md)  
> * [MapReduce](data-factory-map-reduce.md)  
> * [Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
> * [Aprendizaje automático](data-factory-azure-ml-batch-execution-activity.md) 
> * [Procedimiento almacenado](data-factory-stored-proc-activity.md)
> * [U-SQL de análisis con Data Lake](data-factory-usql-activity.md)
> * [.NET personalizado](data-factory-use-custom-activities.md)

## <a name="overview"></a>Información general
Este artículo explica las actividades de transformación de datos en la factoría de datos de Azure que puede usar tootransform y procesa los datos sin formato en las predicciones y visión. Una actividad de transformación se ejecuta en un entorno informático, como clúster de HDInsight de Azure o un Lote de Azure. Proporciona vínculos tooarticles con información detallada sobre cada actividad de transformación.

Factoría de datos admite Hola siguiendo las actividades de transformación de datos que se pueden agregar demasiado[canalizaciones](data-factory-create-pipelines.md) ya sea individualmente o se encadenan con otra actividad.

> [!NOTE]
> Para obtener un tutorial con instrucciones paso a paso, consulte el artículo [Crear una canalización con la transformación de Hive](data-factory-build-your-first-pipeline.md) .  
> 
> 

## <a name="hdinsight-hive-activity"></a>Actividad de HDInsight Hive
Hola actividad de HDInsight Hive en una canalización de factoría de datos ejecuta consultas de Hive por su cuenta o clúster de HDInsight basados en Windows/Linux a petición. Consulte el artículo [Actividad de Hive](data-factory-hive-activity.md) para obtener más información acerca de esta actividad. 

## <a name="hdinsight-pig-activity"></a>Actividad de HDInsight Pig
Hola actividad de HDInsight Pig en una canalización de factoría de datos ejecuta consultas de Pig por su cuenta o clúster de HDInsight basados en Windows/Linux a petición. Consulte el artículo [Actividad de Pig](data-factory-pig-activity.md) para obtener más información acerca de esta actividad. 

## <a name="hdinsight-mapreduce-activity"></a>Actividad de MapReduce de HDInsight
Hola actividad de HDInsight MapReduce en una canalización de factoría de datos ejecuta programas de MapReduce por su cuenta o clúster de HDInsight basados en Windows/Linux a petición. Consulte el artículo [Actividad de MapReduce](data-factory-map-reduce.md) para obtener más información acerca de esta actividad.

## <a name="hdinsight-streaming-activity"></a>Actividad de HDInsight Streaming
Hola actividad de transmisión por secuencias de HDInsight en una canalización de factoría de datos ejecuta programas de Streaming de Hadoop por su cuenta o clúster de HDInsight basados en Windows/Linux a petición. Vea [Actividad de HDInsight Streaming](data-factory-hadoop-streaming-activity.md) para obtener información sobre esta actividad.

## <a name="hdinsight-spark-activity"></a>Actividad de HDInsight Spark
Hola actividad de HDInsight Spark en una canalización de factoría de datos ejecuta programas de Spark en su propio clúster de HDInsight. Consulte [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) (Invocar programas Spark desde Data Factory de Azure) para obtener información detallada. 

## <a name="machine-learning-activities"></a>Actividades de Machine Learning
Azure factoría de datos permite tooeasily crear canalizaciones que usan un aprendizaje automático de Azure publicada web service para realizar análisis predictivos. Con hello [actividad de ejecución de lotes](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) en una canalización del generador de datos de Azure, puede invocar un predicciones de toomake de servicio de web de aprendizaje automático en los datos de hello en lote.

Con el tiempo, los modelos de predicción de Hola Hola aprendizaje automático de experimentos puntuación necesitan toobe volver a entrenar con nueva entrada de conjuntos de datos. Cuando termine con reciclaje, desea hello tooupdate la puntuación del servicio web con hello volver a entrenar el modelo de aprendizaje automático. Puede usar hello [actividades de actualización de recursos](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) servicio de web de hello tooupdate con hello recién entrenado.  

Consulte [Usar actividades de Machine Learning](data-factory-azure-ml-batch-execution-activity.md) para obtener más información sobre estas actividades de Machine Learning. 

## <a name="stored-procedure-activity"></a>Actividad de procedimiento almacenado
Puede usar la actividad de SQL Server Stored Procedure hello en un tooinvoke de canalización de factoría de datos en un procedimiento almacenado en uno de hello siguientes almacenes de datos: SQL de Azure, almacenamiento de datos de SQL Azure, base de datos de SQL Server en su empresa o una máquina virtual de Azure. Consulte el artículo [Actividad de procedimiento almacenado](data-factory-stored-proc-activity.md) para obtener más información.  

## <a name="data-lake-analytics-u-sql-activity"></a>Actividad de U-SQL de Data Lake Analytics 
La actividad de U-SQL de Data Lake Analytics ejecuta un script de U-SQL en un clúster de Azure Data Lake Analytics. Consulte el artículo [Actividad de U-SQL de Data Analytics](data-factory-usql-activity.md) para obtener más información. 

## <a name="net-custom-activity"></a>Actividad personalizada de .NET
Si necesita datos de tootransform de forma que no es compatible con la factoría de datos, puede crear una actividad personalizada con su propia lógica de procesamiento de datos y usar actividad hello en canalización Hola. Puede configurar Hola personalizada .NET actividad toorun mediante un servicio Azure Batch o un clúster de HDInsight de Azure. Consulte el artículo [Utilizar actividades personalizadas](data-factory-use-custom-activities.md) para obtener más información. 

Puede crear una actividad personalizada toorun R scripts en el clúster de HDInsight con R instalado. Consulte [Run R Script using Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)(Ejecutar script de R con Data Factory de Azure). 

## <a name="compute-environments"></a>Entornos de proceso
Crear un servicio vinculado para el entorno de proceso de hello y, a continuación, usar servicio de hello vinculado al definir una actividad de transformación. La Factoría de datos admite dos tipos de entornos de proceso. 

1. **Petición**: en este caso, entorno informático de hello es completamente administrado por el generador de datos. Automáticamente se crea por hello servicio factoría de datos antes de que un trabajo se tooprocess enviado datos y quitan cuando se completa el trabajo de Hola. Puede configurar y controlar la configuración granular de entorno de proceso a petición de hello para la ejecución de trabajo, administración del clúster y las acciones de arranque. 
2. **Traiga el suyo propio**: en este caso, puede registrar su propio entorno informático (por ejemplo, clúster de HDInsight) como servicio vinculado en la Factoría de datos. Administre el entorno informático de Hello propio usuario y lo Hola servicio factoría de datos utiliza las actividades de hello tooexecute. 

Vea [servicios vinculados de proceso](data-factory-compute-linked-services.md) artículo toolearn acerca de servicios admitidos por factoría de datos de proceso. 

## <a name="summary"></a>Resumen
Azure admite factoría de datos Hola siguiendo las actividades de transformación de datos y Hola entornos de proceso para las actividades de Hola. las actividades de transformación de Hello pueden ser agregado toopipelines individualmente o se encadenan con otra actividad.

| Actividad de transformación de datos | Entorno de procesos |
|:--- |:--- |
| [Hive](data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop Streaming](data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Actividades de Machine Learning: ejecución de Batch y recurso de actualización](data-factory-azure-ml-batch-execution-activity.md) |MV de Azure |
| [Procedimiento almacenado](data-factory-stored-proc-activity.md) |SQL Azure, Almacenamiento de datos SQL de Azure o SQL Server |
| [U-SQL de análisis con Data Lake](data-factory-usql-activity.md) |Análisis con Azure Data Lake |
| [DotNet](data-factory-use-custom-activities.md) |HDInsight [Hadoop] o Lote de Azure |

