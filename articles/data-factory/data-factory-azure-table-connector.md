---
title: aaaMove datos hacia y desde la tabla de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos hacia y desde almacenamiento de tabla de Azure mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a>Mover tooand de datos de la tabla de Azure mediante Data Factory de Azure
Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde el almacenamiento de tabla de Azure. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola. 

Puede copiar datos desde cualquier origen compatible datos almacenan tooAzure almacenamiento de tabla o de datos de receptor de almacenamiento de tablas Azure tooany admitida almacenan. Para obtener una lista de almacenes de datos admite como orígenes o receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. 

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva datos con Azure Table Storage como origen o destino mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos: 

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia/desde un almacenamiento de tablas de Azure, vea [ejemplos JSON](#json-examples) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAzure almacenamiento de tabla: 

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hay dos tipos de servicios vinculados que se puede usar toolink un generador de datos de Azure de tooan de almacenamiento de blobs de Azure. Se trata del servicio vinculado **AzureStorage** y el servicio vinculado **AzureStorageSas**. Hola servicio vinculado de almacenamiento de Azure proporciona factoría de datos de hello con acceso global toohello almacenamiento de Azure. Mientras que vinculado hello Azure almacenamiento SAS (firma de acceso compartido) servicio proporciona factoría de datos de hello con acceso restringido tiempo enlazadas toohello almacenamiento de Azure. No existen otras diferencias entre estos dos servicios vinculados. Elegir servicio de hello vinculado que se adapte a sus necesidades. Hello las secciones siguientes proporcionan más detalles sobre estos dos servicios vinculados.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. Hola **typeProperties** sección Hola conjunto de datos de tipo **AzureTable** tiene Hola propiedades siguientes.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de hello en la instancia de base de datos de tabla de Azure de Hola que servicio vinculado que hace referencia a. |Sí. Cuando se especifica un nombre de tabla sin un azureTableSourceQuery, todos los registros de la tabla de hello son destino toohello copiada. Si también se especifica un azureTableSourceQuery, los registros de tabla de Hola que satisface la consulta de hello son destino toohello copiada. |

### <a name="schema-by-data-factory"></a>Esquema de Data Factory
En los almacenes de datos sin esquema como tabla de Azure, Hola servicio Data Factory deduce el esquema de hello en uno de hello siguientes maneras:

1. Si especifica estructura Hola de datos mediante el uso de hello **estructura** propiedad en la definición de conjunto de datos de hello, Hola servicio Data Factory respeta esta estructura como esquema de Hola. En este caso, si una fila no contiene un valor para una columna, se proporciona un valor nulo para ella.
2. Si no especifica la estructura de Hola de datos mediante el uso de hello **estructura** propiedad en la definición de conjunto de datos de hello, factoría de datos deduce el esquema de hello utilizando Hola primera fila de datos de Hola. En este caso, si la primera fila de hello no contiene el esquema completo de hello, algunas columnas se omiten en el resultado de hello de operación de copia.

Por lo tanto, para orígenes de datos sin esquemas, se recomienda Hola es toospecify estructura de Hola de datos mediante Hola **estructura** propiedad.

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, conjuntos de datos de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Propiedades disponibles en la sección de typeProperties Hola de actividad de hello en hello otra parte varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

**AzureTableSource** admite Hola propiedades en la sección typeProperties siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta de tabla de Azure. Vea los ejemplos en la sección siguiente Hola. |No. Cuando se especifica un nombre de tabla sin un azureTableSourceQuery, todos los registros de la tabla de hello son destino toohello copiada. Si también se especifica un azureTableSourceQuery, los registros de tabla de Hola que satisface la consulta de hello son destino toohello copiada. |
| azureTableSourceIgnoreTableNotFound |Indica si debe Hola excepción de tabla no existe. |TRUE<br/>FALSE |No |

### <a name="azuretablesourcequery-examples"></a>ejemplos de azureTableSourceQuery
Si la columna de la Tabla de Azure es de tipo cadena:

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

Si la columna de la Tabla de Azure es de tipo datetime:

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink** admite Hola propiedades en la sección typeProperties siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Partición clave valor predeterminado que se puede usar en el receptor de Hola. |Valor de cadena. |No |
| azureTablePartitionKeyName |Especifique el nombre de columna de hello cuyos valores se usan como claves de partición. Si no se especifica, AzureTableDefaultPartitionKeyValue se usa como clave de partición de Hola. |Un nombre de columna. |No |
| azureTableRowKeyName |Especifique el nombre de columna de hello cuyos valores de columna se utilizan como clave de fila. Si no se especifica, use un GUID para cada fila. |Un nombre de columna. |No |
| azureTableInsertType |datos de tooinsert de modo de saludo en tabla de Azure.<br/><br/>Esta propiedad controla si las filas existentes en la tabla de salida de hello con claves de partición y fila coincidentes tienen sus valores reemplazará o se combinará. <br/><br/>toolearn acerca de cómo funcionan estas configuraciones (combinación y reemplazo), consulte [Insert o Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) y [insertar o reemplazar entidades](https://msdn.microsoft.com/library/azure/hh452242.aspx) temas. <br/><br> Esta configuración se aplica a nivel de fila de hello, no nivel de tabla de hello, y ninguna de estas opciones eliminan las filas de tabla de salida de hello que no existen en la entrada de Hola. |merge (predeterminado)<br/>replace |No |
| writeBatchSize |Inserta datos en hello tabla de Azure cuando se alcanza el valor de hello writeBatchSize o writeBatchTimeout. |Entero (número de filas) |No (valor predeterminado = 10000) |
| writeBatchTimeout |Inserta datos en hello tabla de Azure cuando se alcanza el valor de hello writeBatchSize o writeBatchTimeout |timespan<br/><br/>Ejemplo: "00:20:00" (20 minutos) |No (valor de tiempo de espera predeterminado toostorage cliente predeterminado 90 seg) |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
Asignar una columna de destino tooa de columna de origen mediante la propiedad JSON de traductor de Hola para poder usar las columnas de destino hello como Hola azureTablePartitionKeyName.

En el siguiente ejemplo de Hola, columna de origen DivisionID es toohello asignado las columnas de destino: DivisionID.  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
Hola DivisionID se especifica como clave de partición de Hola.

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>Ejemplos de JSON
Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestran cómo toocopy tooand de datos de almacenamiento de tabla de Azure y base de datos de Blob de Azure. Sin embargo, se pueden copiar datos **directamente** desde cualquiera de hello orígenes tooany de receptores de hello compatible. Para obtener más información, consulte sección de Hola "almacenes de datos admitidos y formatos" en [mover datos mediante la actividad de copia](data-factory-data-movement-activities.md).

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a>Ejemplo: Copiar los datos de tabla de Azure tooAzure Blob
Hola el siguiente ejemplo se muestra:

1. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabla y blob).
2. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureTable](#dataset-properties).
3. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [AzureTableSource](#activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia los datos que pertenecen a partición predeterminada de toohello en un blob de tooa de la tabla de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado de Almacenamiento de Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**. Para Hola primero, especificar cadena de conexión de Hola que incluye la clave de la cuenta de hello y para hello uno posterior, especificar Hola Uri de firma de acceso compartido (SAS). Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).  

**Conjunto de datos de entrada de tabla de Azure:**

ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en la tabla de Azure.

Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Actividad de copia en una canalización con AzureTableSource y BlobSink:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**AzureTableSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada con **AzureTableSourceQuery** propiedad selecciona datos de Hola de partición predeterminada de hello toocopy de cada hora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },                
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
            }
         ]    
    }
}
```

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a>Ejemplo: Copiar los datos de Blob de Azure tooAzure tabla
Hola el siguiente ejemplo se muestra:

1. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabla y blob)
2. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
3. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureTable](#dataset-properties).
4. Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [AzureTableSink](#copy-activity-properties).

ejemplo de Hola copia datos de serie temporal de una tabla de Azure tooan de blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado de Azure Storage (para tabla y blob de Azure):**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

Azure Data Factory admite dos tipos de servicios vinculados de Azure Storage: **AzureStorage** y **AzureStorageSas**. Para Hola primero, especificar cadena de conexión de Hola que incluye la clave de la cuenta de hello y para hello uno posterior, especificar Hola Uri de firma de acceso compartido (SAS). Para más información, consulte la sección [Servicios vinculados](#linked-service-properties).

**Conjunto de datos de entrada de blob de Azure:**

Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1). Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola. "externo": "true" configuración informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Conjunto de datos de salida de tabla de Azure:**

ejemplo Hello copia la tabla de tooa de datos denominada "MyTable" en la tabla de Azure. Crear una tabla de Azure con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola. Se agregan nuevas filas toohello tabla cada hora.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Actividad de copia en una canalización con BlobSource y AzureTableSink:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**AzureTableSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
          }
        },
        "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },                        
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
## <a name="type-mapping-for-azure-table"></a>Asignación de tipos para tabla de Azure
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos.

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Cuando se mueven datos demasiado & de tabla de Azure, Hola después [asignaciones definidas por el servicio tabla de Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) sirven del tipo de too.NET de tipos de OData de la tabla de Azure y viceversa.

| Tipo de datos OData | Tipo .NET | Detalles |
| --- | --- | --- |
| Edm.Binary |byte[] |Una matriz de bytes de too64 KB. |
| Edm.Boolean |booleano |Valor booleano. |
| Edm.DateTime |DateTime |Valor de 64 bits expresado como hora universal coordinada (UTC). Hola admite DateTime intervalo comienza desde 12:00 de la medianoche del 1 de enero de 1601 D.C. (E.C.), UTC. intervalo de Hello finaliza en 31 de diciembre de 9999. |
| Edm.Double |double |Valor de punto flotante de 64 bits. |
| Edm.Guid |Guid |Identificador único global de 128 bits. |
| Edm.Int32 |Int32 |Entero de 32 bits. |
| Edm.Int64 |Int64 |Entero de 64 bits. |
| Edm.String |String |Valor codificado mediante UTF-16. Valores de cadena pueden ser up too64 KB. |

### <a name="type-conversion-sample"></a>Ejemplo de conversión de tipo
Hola según muestra es para copiar datos de una tabla de tooAzure de Blob de Azure con conversiones de tipos.

Suponga que el conjunto de datos de hello Blob está en formato CSV y contiene tres columnas. Uno de ellos es una columna de fecha y hora con un formato de fecha y hora personalizado mediante francés abreviaturas para el día de la semana de Hola.

Definir el conjunto de datos de origen de blobs de hello como se indica a continuación junto con las definiciones de tipo para las columnas de Hola.

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Proporciona asignación de tipos de Hola de OData de la tabla de Azure tipo too.NET, tendría que definir tabla hello en la tabla de Azure con hello después de esquema.

**Esquema de tabla de Azure:**

| Nombre de la columna | Tipo |
| --- | --- |
| userid |Edm.Int64 |
| name |Edm.String |
| lastlogindate |Edm.DateTime |

A continuación, definir el conjunto de datos de tabla de Azure de Hola de como se indica a continuación. No es necesario toospecify sección de "estructura" con la información de tipo hello puesto que ya se ha especificado información de tipo hello Hola subyacente de almacén de datos.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

En este caso, el generador de datos automáticamente conversiones de tipos incluidos los campos de fecha y hora de hello con formato de fecha y hora personalizado hello mediante una referencia cultural "fr-fr" hello al mover los datos de Blob tooAzure tabla.

> [!NOTE]
> columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas formas, consulte [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md).
