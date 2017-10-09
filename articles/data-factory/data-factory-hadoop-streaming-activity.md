---
title: datos de aaaTransform con Hadoop Streaming Activity - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo puede utilizar hello Hadoop Streaming Activity en un datos tootransform de factoría de datos de Azure mediante la ejecución de programas de Streaming de Hadoop en un clúster de HDInsight en-petición/su propio."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>Transformación de datos mediante Hadoop Streaming Activity en Azure Data Factory
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

Puede usar hello HDInsightStreamingActivity actividad invocar un trabajo de Streaming de Hadoop desde una canalización de factoría de datos de Azure. Hello siguiente fragmento JSON muestra sintaxis de Hola para usar hello HDInsightStreamingActivity en un archivo de canalización JSON. 

Hola actividad de transmisión por secuencias de HDInsight en una factoría de datos [canalización](data-factory-create-pipelines.md) ejecuta programas de Streaming de Hadoop en [su propio](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) o [a petición](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight basados en Windows/Linux clúster. En este artículo se basa en hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) artículo, que presenta una descripción general de transformación de datos y las actividades de transformación de hello compatible.

> [!NOTE] 
> Si es nuevo tooAzure factoría de datos, lea [tooAzure Introducción factoría de datos](data-factory-introduction.md) y Hola tutorial: [crear la canalización de datos primer](data-factory-build-your-first-pipeline.md) antes de leer este artículo. 

## <a name="json-sample"></a>Ejemplo de JSON
clúster de HDInsight de Hola se rellena automáticamente con los programas de ejemplo (wc.exe y cat.exe) y los datos (davinci.txt). De forma predeterminada, nombre de contenedor de Hola que se usa por clúster de HDInsight de Hola es nombre de hello del propio clúster Hola. Por ejemplo, si el nombre de clúster es myhdicluster, nombre del contenedor de blob de hello asociado sería myhdicluster. 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

Tenga en cuenta Hola siguientes puntos:

1. Conjunto hello **linkedServiceName** toohello nombre del saludo servicio vinculado que apunta el clúster de HDInsight tooyour en qué Hola streaming mapreduce se ejecuta el trabajo.
2. Establecer tipo de Hola de actividad hello demasiado**HDInsightStreaming**.
3. Para hello **asignador** propiedad, especifique Hola nombre del ejecutable del asignador de. En el ejemplo de Hola, cat.exe es el asignador de hello ejecutable.
4. Para hello **reductor** propiedad, especifique Hola nombre del ejecutable del reductor. En el ejemplo de Hola, wc.exe es reductor Hola ejecutable.
5. Para hello **entrada** type (propiedad), especifique el archivo de entrada de hello (incluida la ubicación de hello) para el asignador de Hola. En el ejemplo de Hola: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample es el contenedor de blob de hello, ejemplo/data/Gutenberg es la carpeta de Hola y davinci.txt es blob Hola.
6. Para hello **salida** type (propiedad), especifique el archivo de salida de hello (incluida la ubicación de hello) para reductor Hola. salida de Hello de trabajo de Streaming de Hadoop de Hola se escribe ubicación toohello especificado para esta propiedad.
7. Hola **filePaths** sección, especifique las rutas de acceso de Hola para los ejecutables de asignador y reductor Hola. En el ejemplo de Hola: "adfsample/example/apps/wc.exe", adfsample es el contenedor de blob de hello, example/apps es la carpeta de Hola y wc.exe es ejecutable hello.
8. Para hello **fileLinkedService** propiedad, especifique Hola Hola de servicio vinculado que representa el almacenamiento de Azure que contiene archivos de hello especificados en la sección de hello filePaths el almacenamiento de Azure.
9. Para hello **argumentos** propiedad, especifique los argumentos de Hola para hello trabajo de transmisión por secuencias.
10. Hola **getDebugInfo** propiedad es un elemento opcional. Cuando se establece tooFailure, registros de Hola se descargan solo en caso de error. Cuando se establece tooAlways, registros siempre se descargan independientemente del estado de ejecución de Hola.

> [!NOTE]
> Como se muestra en el ejemplo de Hola, especificar un conjunto de datos de salida de hello Hadoop Streaming Activity para hello **genera** propiedad. Este conjunto de datos es simplemente un dataset ficticio que es necesario toodrive Hola canalización programación. No es necesario ningún conjunto de datos de entrada de toospecify de actividad de Hola de hello **entradas** propiedad.  
> 
> 

## <a name="example"></a>Ejemplo
canalización de Hello en este tutorial ejecuta el programa de asignación y reducción de transmisión por secuencias de hello contar palabras en el clúster de HDInsight de Azure. 

### <a name="linked-services"></a>Servicios vinculados
#### <a name="azure-storage-linked-service"></a>Servicio vinculado de Azure Storage
En primer lugar, cree un Hola de toolink almacenamiento de Azure que se usa por factoría de datos de Azure de toohello de clúster de HDInsight de Azure de Hola de servicio vinculado. Si copiar y pegar los Hola siguiente código, no olvide tooreplace cuenta nombre y clave de cuenta con el nombre de Hola y la clave de su almacenamiento de Azure. 

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
A continuación, cree un servicio vinculado toolink su factoría de datos de Azure de toohello de clúster de HDInsight de Azure. Si copiar y pegar los Hola después de código, reemplace el nombre del clúster de HDInsight por nombre de Hola de su clúster de HDInsight y cambiar los valores de nombre y la contraseña de usuario. 

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
canalización de Hello en este ejemplo no tiene ninguna entrada. Especifique un conjunto de datos de salida de hello actividad de transmisión por secuencias de HDInsight. Este conjunto de datos es simplemente un dataset ficticio que es necesario toodrive Hola canalización programación. 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>Canalización
canalización de Hello en este ejemplo tiene sólo una actividad que es de tipo: **HDInsightStreaming**. 

clúster de HDInsight de Hola se rellena automáticamente con los programas de ejemplo (wc.exe y cat.exe) y los datos (davinci.txt). De forma predeterminada, nombre de contenedor de Hola que se usa por clúster de HDInsight de Hola es nombre de hello del propio clúster Hola. Por ejemplo, si el nombre de clúster es myhdicluster, nombre del contenedor de blob de hello asociado sería myhdicluster.  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a>Otras referencias
* [Actividad de Hive](data-factory-hive-activity.md)
* [Actividad de Pig](data-factory-pig-activity.md)
* [Actividad MapReduce](data-factory-map-reduce.md)
* [Invocar programas Spark](data-factory-spark.md)
* [Invocar scripts de R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

