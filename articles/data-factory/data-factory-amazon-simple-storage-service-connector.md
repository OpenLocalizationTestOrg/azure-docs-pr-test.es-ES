---
title: "datos de aaaMove de Amazon Simple Storage Service mediante el uso de la factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomove datos de Amazon Simple Storage Service (S3) mediante el uso de Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Movimiento de datos desde Amazon Simple Storage Service mediante Azure Data Factory
Este artículo explica cómo toouse Hola actividad de copia de datos de Data Factory de Azure toomove de Amazon Simple Storage Service (S3). Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.

Puede copiar datos de almacén de datos de Amazon S3 tooany admitida receptor. Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. Factoría de datos admite actualmente solo migración de datos de almacenes de datos de Amazon S3 tooother, pero no mover los datos de otros datos almacena tooAmazon S3.

## <a name="required-permissions"></a>Permisos necesarios
toocopy datos de Amazon S3, asegúrese de que se le ha concedido Hola los siguientes permisos:

* `s3:GetObject` y `s3:GetObjectVersion` para operaciones de objeto de Amazon S3.
* `s3:ListBucket` para operaciones de depósito de Amazon S3. Si usas Hola Asistente para copia de generador de datos, `s3:ListAllMyBuckets` también es necesario.

Para obtener más información acerca de la lista completa de Hola de Amazon S3 permisos, consulte [especificación de permisos en una directiva de](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva los datos desde un origen de Amazon S3 mediante diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Para ver un tutorial rápido, consulte el [tutorial sobre la creación de una canalización mediante el Asistente para copia](data-factory-copy-data-wizard-tutorial.md).

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia, consulte hello [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Si usa herramientas o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas o las API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola. Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de Amazon S3, vea hello [ejemplo de JSON: copiar los datos de Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) sección de este artículo.

> [!NOTE]
> Para información sobre los formatos de compresión y de archivo compatibles para una actividad de copia, consulte [Formatos de archivo y de compresión admitidos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAmazon S3.

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Un servicio vinculado vincula una factoría de datos de tooa de almacén de datos. Crear un servicio vinculado de tipo **AwsAccessKey** toolink tooyour factoría de datos del almacén de los datos de Amazon S3. Hello en la tabla siguiente proporciona el servicio de descripción para JSON elementos específico tooAmazon S3 (AwsAccessKey) que se vincula.

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| accessKeyID |Id. de clave de acceso de los secretos de Hola. |cadena |Sí |
| secretAccessKey |clave de acceso de los secretos de Hello propio. |Cadena secreta cifrada |Sí |

Este es un ejemplo:

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
toospecify toorepresent de un conjunto de datos de entrada de datos en el almacenamiento de blobs de Azure, propiedad de tipo de conjunto Hola del conjunto de datos de hello demasiado**AmazonS3**. Conjunto hello **linkedServiceName** servicio vinculado de propiedad del nombre de toohello de conjunto de datos de Hola de hello S3 de Amazon. Para ver una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, consulte [Creación de conjuntos de datos](data-factory-create-datasets.md). 

Las secciones como structure, availability y policy son similares para todos los tipos de conjunto de datos (como base de datos SQL, blob de Azure y tabla de Azure). Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y se proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. Hola **typeProperties** sección para un conjunto de datos de tipo **AmazonS3** (que incluye el conjunto de datos de hello Amazon S3) tiene Hola propiedades siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| bucketName |nombre del depósito de Hello S3. |String |Sí |
| key |clave del objeto Hola S3. |String |No |
| prefix |Prefijo para la clave del objeto Hola S3. Se seleccionan objetos cuyas claves comienzan por este prefijo. Se aplica solo cuando la clave está vacía. |string |No |
| versión |versión de Hola del objeto de hello S3, si está habilitado el control de versiones de S3. |String |No |
| formato | se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Conjunto hello **tipo** propiedad en formato tooone de estos valores. Para obtener más información, vea hello [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [el formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), y [formato Parquet ](data-factory-supported-file-and-compression-formats.md#parquet-format) secciones. <br><br> Si desea que los archivos de toocopy como-está entre los almacenes basados en archivos (copia binaria), sección de formato de hello skip en ambas definiciones de conjunto de datos de entrada y salida. |No | |
| compresión | Especificar tipo de Hola y el nivel de compresión para datos de Hola. tipos de Hello admitido son: **GZip**, **Deflate**, **BZip2**, y **ZipDeflate**. Hola admitida niveles son: **óptimo** y **más rápido**. Para obtener más información, consulte el artículo sobre [formatos de archivo y compresión en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No | |


> [!NOTE]
> **bucketName + tecla** especifica la ubicación de Hola Hola S3 de objeto de, donde depósitos es el contenedor de raíz de Hola para S3 objetos, y la clave es objeto de toohello S3 de ruta de acceso completa de Hola.

### <a name="sample-dataset-with-prefix"></a>Conjunto de datos de ejemplo con prefijo

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>Conjunto de datos de ejemplo (con versión)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>Rutas de acceso dinámicas para S3
Hello en el ejemplo anterior utiliza valores fijos para hello **clave** y **bucketName** propiedades de conjunto de datos de hello S3 de Amazon.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

Puede hacer que Data Factory calcule estas propiedades dinámicamente en tiempo de ejecución mediante variables del sistema como SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Puede hacer Hola igual para hello **prefijo** propiedad de un conjunto de datos de Amazon S3. Para ver una lista de funciones y variables admitidas, consulte [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md).

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte [Creación de canalizaciones](data-factory-create-pipelines.md). Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades. Propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad. Para la actividad de copia de hello, propiedades varían en función de tipos de Hola de orígenes y receptores. Cuando un origen de la actividad de copia de hello es del tipo **FileSystemSource** (que incluye Amazon S3), Hola después de la propiedad está disponible en **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| recursive |Especifica si toorecursively lista S3 objetos en el directorio de Hola. |true/false |No |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>Ejemplo de JSON: copiar los datos de Amazon S3 tooAzure almacenamiento de blobs
Este ejemplo se muestra cómo toocopy datos de Amazon S3 tooan almacenamiento de blobs de Azure. Sin embargo, se pueden copiar datos directamente demasiado[cualquiera de los receptores de Hola que se admiten](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante el uso de actividad de copia de hello de factoría de datos.

ejemplo de Hola proporciona definiciones de JSON para hello siguiendo las entidades de la factoría de datos. Puede usar estos toocreate definiciones una toocopy de datos de canalización desde el almacenamiento de Amazon S3 tooBlob, mediante el uso de hello [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).   

* Un servicio vinculado de tipo [AwsAccessKey](#linked-service-properties).
* Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Un [conjunto de datos](data-factory-create-datasets.md) de tipo [AmazonS3](#dataset-properties).
* Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [canalización](data-factory-create-pipelines.md) con actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de Amazon S3 tooan blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

### <a name="amazon-s3-linked-service"></a>Servicio vinculado de Amazon S3

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Servicio vinculado de Almacenamiento de Azure

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="amazon-s3-input-dataset"></a>Conjunto de datos de entrada de Amazon S3

Establecer **"externo": true** informa servicio Data Factory de hello ese conjunto de datos de hello es externo toohello factoría de datos. Establecer esta propiedad tootrue en un conjunto de datos de entrada que no se crea una actividad de canalización de Hola.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Conjunto de datos de salida de blob de Azure

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de Hola Hola hora de inicio.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>Actividad de copia en una canalización con un origen de Amazon S3 y un receptor de blob

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida, y es toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**FileSystemSource**, y **receptor** tipo está establecido demasiado**BlobSink**.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> columnas de toomap de un toocolumns de conjunto de datos de origen de un conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).


## <a name="next-steps"></a>Pasos siguientes
Vea Hola siguientes artículos:

* toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos y toooptimize de diversas formas, vea hello [copiar actividad Guía de rendimiento y optimización](data-factory-copy-activity-performance.md).

* Para obtener instrucciones paso a paso para crear una canalización con una actividad de copia, consulte hello [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
