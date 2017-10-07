---
title: "datos de aaaMove de Amazon Redshift con factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomove datos de Amazon Redshift con Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a>Movimiento de datos de Amazon Redshift mediante Azure Data Factory
Este artículo explica cómo toouse Hola actividad de copia de datos de toomove de Data Factory de Azure de Amazon Redshift. artículo de Hola se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola. 

Puede copiar datos de almacén de datos de Amazon Redshift tooany admitida receptor. Para obtener una lista de almacenes de datos que se admiten como receptores por actividad de copia de hello, consulte [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Factoría de datos actualmente admite la migración de datos de almacenes de datos de Amazon Redshift tooother, pero no para mover datos desde otro tooAmazon de almacenes de datos Redshift.

## <a name="prerequisites"></a>Requisitos previos
* Si va a mover datos tooan un almacén de datos local, instale [Data Management Gateway](data-factory-data-management-gateway.md) en un equipo local. A continuación, conceder Data Management Gateway (usar una dirección IP de la máquina de hello) hello tooAmazon Redshift clúster de acceso. Vea [clúster de autorizar acceso toohello](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) para obtener instrucciones.
* Si va a mover el almacén de datos tooan datos de Azure, consulte [intervalos de IP de centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653) para los intervalos SQL utilizados por los centros de datos de Azure de Hola y dirección IP de proceso de Hola.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con actividad de copia que mueva los datos desde un origen de Amazon Redshift mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos: 

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de Amazon Redshift, consulte [ejemplo de JSON: copiar los datos de Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAmazon Redshift: 

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona la descripción de JSON elementos específico tooAmazon servicio Redshift vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **AmazonRedshift**. |Sí |
| Servidor |IP dirección o nombre de host del servidor de Amazon Redshift Hola. |Sí |
| puerto |número de Hola de puerto TCP Hola Hola Amazon Redshift server usa toolisten para las conexiones de cliente. |No, valor predeterminado: 5439 |
| database |Nombre de base de datos de Amazon Redshift Hola. |Sí |
| nombre de usuario |Nombre de usuario que tenga la base de datos de access toohello. |Sí |
| Contraseña |Contraseña de cuenta de usuario de Hola. |Sí |

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy son similares para todos los tipos de conjunto de datos (Azure SQL, Azure Blob, Azure Table, etc.).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos. Proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. sección typeProperties Hello para el conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos de Amazon Redshift) tiene Hola propiedades siguientes

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de hello en base de datos de Amazon Redshift de hello servicio vinculado que hace referencia a. |No (si se especifica **query** de **RelationalSource**) |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Cuando el origen de la actividad de copia es del tipo **RelationalSource** (que incluye Amazon Redshift), Hola propiedades siguientes está disponible en la sección typeProperties:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| query |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: select * from MyTable. |No (si se especifica **tableName** de **dataset**) |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a>Ejemplo de JSON: copiar los datos de Amazon Redshift tooAzure Blob
Este ejemplo muestra cómo la base de datos toocopy desde un Amazon Redshift datos tooan almacenamiento de blobs de Azure. Sin embargo, se pueden copiar datos **directamente** tooany de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.  

ejemplo de Hola tiene Hola después de entidades de la factoría de datos:

* Un servicio vinculado de tipo [AmazonRedshift](#linked-service-properties).
* Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).
* Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).

ejemplo de Hola copia datos de un resultado de consulta en el blob de Amazon Redshift tooa cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado de Amazon Redshift:**

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

**Servicio vinculado de Almacenamiento de Azure:**

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
**Conjunto de datos de entrada de Amazon Redshift:**

Establecer `"external": true` informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola. Establecer esta propiedad tootrue en un conjunto de datos de entrada que no se crea una actividad de canalización de Hola.

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Actividad de copia en una canalización con el origen de Azure Redshift (RelationalSource) y el receptor de blob:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
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
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a>Asignación de tipos para Amazon Redshift
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos:

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Al mover datos tooAmazon Redshift, Hola siguiendo las asignaciones se usa desde tipos de Amazon Redshift too.NET tipos.

| Tipo Amazon Redshift | Tipo basado en .NET |
| --- | --- |
| SMALLINT |Int16 |
| INTEGER |Int32 |
| BIGINT |Int64 |
| DECIMAL |DECIMAL |
| REAL |Single |
| DOUBLE PRECISION |Doble |
| BOOLEAN |String |
| CHAR |String |
| VARCHAR |String |
| DATE |DateTime |
| TIMESTAMP |DateTime |
| TEXT |String |

## <a name="map-source-toosink-columns"></a>Asignar columnas de origen toosink
toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lectura repetible de orígenes relacionales
Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento. Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.

## <a name="next-steps"></a>Pasos siguientes
Vea Hola siguientes artículos:

* [Tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso para la creación de una canalización con una actividad de copia.
