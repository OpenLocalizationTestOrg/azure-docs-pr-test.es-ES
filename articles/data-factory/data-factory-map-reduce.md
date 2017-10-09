---
title: "aaaInvoke programa de MapReduce desde la factoría de datos de Azure"
description: "Obtenga información acerca de cómo agrupar tooprocess datos mediante la ejecución de programas de MapReduce en un HDInsight de Azure de un generador de datos de Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a>Invocar programas MapReduce desde la factoría de datos de Azure
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Actividad de Hive](data-factory-hive-activity.md) 
> * [Actividad de Pig](data-factory-pig-activity.md)
> * [Actividad MapReduce](data-factory-map-reduce.md)
> * [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Actividad de Spark](data-factory-spark.md)
> * [Actividad de ejecución de Batch de Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Actividad Actualizar recurso de Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Actividad de procedimiento almacenado](data-factory-stored-proc-activity.md)
> * [Actividad U-SQL de Data Lake Analytics](data-factory-usql-activity.md)
> * [Actividad personalizada de .NET](data-factory-use-custom-activities.md)

Hola actividad de HDInsight MapReduce en una factoría de datos [canalización](data-factory-create-pipelines.md) ejecuta programas MapReduce en [su propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) clúster de HDInsight basados en Windows/Linux. En este artículo se basa en hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) artículo, que presenta una descripción general de transformación de datos y las actividades de transformación de hello compatible.

> [!NOTE] 
> Si es nuevo tooAzure factoría de datos, lea [tooAzure Introducción factoría de datos](data-factory-introduction.md) y Hola tutorial: [crear la canalización de datos primer](data-factory-build-your-first-pipeline.md) antes de leer este artículo.  

## <a name="introduction"></a>Introducción
Una canalización en una factoría de datos de Azure procesa los datos de los servicios de almacenamiento vinculados mediante el uso de servicios de proceso vinculados. Contiene una secuencia de actividades donde cada actividad realiza una operación de procesamiento específica. En este artículo se describe el uso de hello HDInsight MapReduce actividad.

Consulte [Pig](data-factory-pig-activity.md) y [Hive](data-factory-hive-activity.md) para obtener detalles sobre la ejecución de scripts de Pig/Hive en un clúster de HDInsight basado en Windows/Linux desde una canalización mediante actividades de Pig y Hive para HDInsight. 

## <a name="json-for-hdinsight-mapreduce-activity"></a>JSON para la actividad MapReduce de HDInsight
Hola definición de JSON para hello actividad de HDInsight: 

1. Conjunto hello **tipo** de hello **actividad** demasiado**HDInsight**.
2. Especificar nombre de Hola de clase de Hola para **className** propiedad.
3. Especificar Hola ruta de acceso toohello JAR archivo, incluido el nombre de archivo de Hola de **jarFilePath** propiedad.
4. Especifique el servicio de hello vinculado que hace referencia toohello almacenamiento de blobs de Azure que contiene el archivo JAR de hello para **jarLinkedService** propiedad.   
5. Especifique los argumentos de programa de MapReduce Hola Hola **argumentos** sección. En tiempo de ejecución, verá que algunos argumentos adicionales (por ejemplo: mapreduce.job.tags) de marco de trabajo de MapReduce Hola. toodifferentiate los argumentos con argumentos de MapReduce hello, considere el uso de opción y valor como argumentos tal como se muestra en el siguiente ejemplo de Hola (- s,--entrada,--salida etc., son opciones seguidos inmediatamente por sus valores).

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
Puede usar Hola actividad de HDInsight MapReduce toorun cualquier archivo jar de MapReduce en un clúster de HDInsight. Hola siguiente definición de JSON de ejemplo de una canalización, Hola actividad de HDInsight está configurado toorun un archivo JAR Mahout.

## <a name="sample-on-github"></a>Ejemplo en GitHub
Puede descargar un ejemplo para el uso de la actividad de HDInsight MapReduce Hola desde: [ejemplos de generador de datos en GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).  

## <a name="running-hello-word-count-program"></a>Ejecutar programa de hello contar palabras
canalización de Hello en este ejemplo ejecuta Hola programa de asignación y reducción del número de palabras en el clúster de HDInsight de Azure.   

### <a name="linked-services"></a>Servicios vinculados
En primer lugar, cree un Hola de toolink almacenamiento de Azure que se usa por factoría de datos de Azure de toohello de clúster de HDInsight de Azure de Hola de servicio vinculado. Si copiar y pegar los Hola siguiente código, no olvide tooreplace **nombre-cuenta** y **clave de cuenta** con nombre hello y la clave de su almacenamiento de Azure. 

#### <a name="azure-storage-linked-service"></a>Servicio vinculado de Azure Storage

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a>Servicio vinculado de HDInsight de Azure
A continuación, cree un servicio vinculado toolink su factoría de datos de Azure de toohello de clúster de HDInsight de Azure. Si copiar y pegar los Hola después de código, reemplace **el nombre del clúster de HDInsight** con nombre hello del clúster de HDInsight y cambiar valores de nombre y la contraseña de usuario.   

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a>CONJUNTOS DE DATOS
#### <a name="output-dataset"></a>Conjunto de datos de salida
canalización de Hello en este ejemplo no tiene ninguna entrada. Especifique un conjunto de datos de salida para la actividad de HDInsight MapReduce Hola. Este conjunto de datos es simplemente un dataset ficticio que es necesario toodrive Hola canalización programación.  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Canalización
canalización de Hello en este ejemplo tiene sólo una actividad que es de tipo: HDInsightMapReduce. Algunas propiedades importantes de Hola Hola JSON son: 

| Propiedad | Notas |
|:--- |:--- |
| type |se debe establecer el tipo de Hello demasiado**HDInsightMapReduce**. |
| className |Nombre de clase hello es: **wordcount** |
| jarFilePath |Archivo de ruta de acceso toohello jar que contiene la clase hello. Si copiar y pegar los Hola siguiente código, no olvide toochange Hola nombre de hello clúster. |
| jarLinkedService |Servicio vinculado de almacenamiento Azure que contiene el archivo jar de Hola. Este servicio vinculado hace referencia a un almacenamiento toohello que está asociado con el clúster de HDInsight de Hola. |
| argumentos |programa de wordcount Hola toma dos argumentos, una entrada y salida. Hola entrada archivo es hello davinci.txt. |
| frecuencia/intervalo |valores de Hello para estas propiedades coincidan con conjunto de datos de salida de hello. |
| linkedServiceName |hace una referencia de servicio vinculado de HDInsight de toohello había creado anteriormente. |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a>Ejecutar programas Spark
Puede usar programas de MapReduce actividad toorun Spark en el clúster de HDInsight Spark. Consulte [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) (Invocar programas Spark desde Data Factory de Azure) para obtener información detallada.  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>Otras referencias
* [Actividad de Hive](data-factory-hive-activity.md)
* [Actividad de Pig](data-factory-pig-activity.md)
* [Actividad de streaming de Hadoop](data-factory-hadoop-streaming-activity.md)
* [Invocar programas Spark](data-factory-spark.md)
* [Invocar scripts de R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

