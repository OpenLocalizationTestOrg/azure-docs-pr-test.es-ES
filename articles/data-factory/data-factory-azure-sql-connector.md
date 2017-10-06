---
title: aaaCopy datos hacia y desde la base de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocopy datos hacia y desde la base de datos de SQL de Azure mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a>Copiar datos tooand de base de datos de SQL de Azure mediante Data Factory de Azure
Este artículo explica cómo toouse Hola actividad de copia de Data Factory de Azure toomove datos tooand de base de datos de SQL Azure. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.  

## <a name="supported-scenarios"></a>Escenarios admitidos
Puede copiar datos **de base de datos de SQL Azure** toohello siguientes almacenes de datos:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Puede copiar los datos de hello siguientes almacenes de datos **tooAzure base de datos SQL**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a>Tipos de autenticación que se admiten
El conector de Azure SQL Database admite la autenticación básica.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con actividad de copia que mueva los datos hacia Azure SQL Database y desde esta base de datos mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos: 

1. Crear una **factoría de datos**. Una factoría de datos puede contener una o más canalizaciones. 
2. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink. Por ejemplo, si va a copiar datos desde una base de datos de SQL Azure del tooan de almacenamiento blob de Azure, cree dos toolink servicios vinculados su cuenta de almacenamiento de Azure y la factoría de datos de tooyour de base de datos de SQL Azure. Para las propiedades de servicio vinculado que son específico tooAzure base de datos SQL, consulte [vinculado propiedades del servicio](#linked-service-properties) sección. 
3. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. En el ejemplo de Hola mencionado en el último paso de hello, se crea un contenedor de blobs de hello toospecify de conjunto de datos y la carpeta que contiene los datos de entrada de Hola. Y crear tabla de otro conjunto de datos toospecify Hola SQL en la base de datos de SQL Azure de Hola que contiene los datos de hello copiados desde el almacenamiento de blobs de Hola. Para las propiedades del conjunto de datos que son específico tooAzure almacén de Data Lake, consulte [propiedades de conjunto de datos](#dataset-properties) sección.
4. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. En el ejemplo de Hola que se ha mencionado anteriormente, use BlobSource como un origen y SqlSink como un receptor para la actividad de copia de Hola. De forma similar, si va a copiar desde la base de datos de SQL Azure tooAzure almacenamiento de blobs, utilice SqlSource y BlobSink en la actividad de copia de Hola. Para copiar propiedades de actividad que son específico tooAzure base de datos SQL, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección. Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia y desde una base de datos de SQL Azure, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-sql-database) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAzure base de datos SQL: 

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
SQL Azure había vinculado a los vínculos de servicio una factoría de datos de tooyour de base de datos de SQL Azure. Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooAzure SQL servicio vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **AzureSqlDatabase** |Sí |
| connectionString |Especifique la información necesaria la instancia de base de datos de SQL Azure toohello tooconnect para la propiedad connectionString de Hola. Solo se admite la autenticación básica. |Sí |

> [!IMPORTANT]
> Configurar [Firewall de base de datos de SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) Hola servidor de base de datos demasiado[permitir servidor de servicios de Azure tooaccess hello](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Además, si va a copiar datos tooAzure base de datos SQL de incluido Azure fuera de orígenes de datos local con la puerta de enlace de generador de datos, configurar el intervalo de direcciones IP adecuado para la máquina de Hola que está enviando datos tooAzure base de datos SQL.

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
toospecify un conjunto de datos toorepresent datos de entrada o salidas de una base de datos de SQL Azure, Establece Hola de propiedad de tipo de conjunto de datos de Hola para: **AzureSqlTable**. Conjunto hello **linkedServiceName** servicio vinculado de propiedad del nombre de toohello de conjunto de datos de Hola de hello SQL Azure.  

Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. Hola **typeProperties** sección Hola conjunto de datos de tipo **AzureSqlTable** tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola o vista en la instancia de base de datos de SQL Azure Hola que servicio vinculado hace referencia a. |Sí |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

> [!NOTE]
> Hola actividad de copia toma solo una entrada y produce un único resultado.

Mientras que propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Si va a mover datos desde una base de datos de SQL Azure, configure tipo de origen de hello en la actividad de copia de hello demasiado**SqlSource**. De forma similar, si va a mover la base de datos de SQL Azure de tooan de datos, Establece el tipo de receptor de hello en actividad de copia de hello demasiado**SqlSink**. Esta sección proporciona una lista de propiedades admitidas por SqlSource y SqlSink.

### <a name="sqlsource"></a>SqlSource
En la actividad de copia, cuando el origen de hello es de tipo **SqlSource**, Hola propiedades siguientes está disponible en **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Ejemplo: `select * from MyTable`. |No |
| sqlReaderStoredProcedureName |Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola. |Nombre del programa Hola a procedimiento almacenado. Hola última instrucción de SQL debe ser una instrucción SELECT en el procedimiento almacenado de Hola. |No |
| storedProcedureParameters |Parámetros de hello procedimiento almacenan. |Pares nombre-valor. Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola. |No |

Si hello **sqlReaderQuery** se especifica para hello SqlSource, hello actividad de copia ejecuta esta consulta en datos de Hola de hello base de datos de SQL Azure origen tooget. Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).

Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, columnas de hello definidas en la sección sobre la estructura del conjunto de datos de hello JSON Hola son toobuild usa una consulta (`select column1, column2 from mytable`) toorun contra Hola base de datos de SQL Azure. Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.

> [!NOTE]
> Cuando usas **sqlReaderStoredProcedureName**, seguirá necesitando toospecify un valor para hello **tableName** propiedad Hola de conjunto de datos JSON. Pero no se ha realizado ninguna validación en esta tabla.
>
>

### <a name="sqlsource-example"></a>Ejemplo de SqlSource

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

**Hola almacena la definición del procedimiento:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a>SqlSink
**SqlSink** admite Hola propiedades siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar. |timespan<br/><br/> Ejemplo: "00:30:00" (30 minutos). |No |
| writeBatchSize |Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize. |Entero (número de filas) |No (valor predeterminado = 10000) |
| sqlWriterCleanupScript |Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian. Para más información, consulte [Copia repetible](#repeatable-copy). |Una instrucción de consulta. |No |
| sliceIdentifierColumnName |Especifique un nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar. Para más información, consulte [Copia repetible](#repeatable-copy). |Nombre de columna de una columna con el tipo de datos binarios (32). |No |
| sqlWriterStoredProcedureName |Nombre del programa Hola a procedimiento almacenado que upserts (actualizaciones o inserciones) los datos en la tabla de destino de Hola. |Nombre del programa Hola a procedimiento almacenado. |No |
| storedProcedureParameters |Parámetros de hello procedimiento almacenan. |Pares nombre-valor. Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola. |No |
| sqlWriterTableType |Especifique un toobe de nombre de tipo de tabla utilizado en el procedimiento almacenado de Hola. Actividad de copia pone datos Hola que se mueven en una tabla temporal con este tipo de tabla. Código de procedimiento almacenado, a continuación, puede combinar datos de Hola se copian con los datos existentes. |Un nombre de tipo de tabla. |No |

#### <a name="sqlsink-example"></a>Ejemplo de SqlSink

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a>Ejemplos JSON para copiar datos tooand de base de datos de SQL
Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestran cómo toocopy tooand de datos de la base de datos de SQL Azure y almacenamiento de blobs de Azure. Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a>Ejemplo: Copiar los datos de base de datos de SQL Azure tooAzure Blob
Hello mismo define Hola siguiendo las entidades de la factoría de datos:

1. Un servicio vinculado de tipo [AzureSqlDatabase](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureSqlTable](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [blob de Azure](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [SqlSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de serie temporal (cada hora, diariamente, etc.) de una tabla de blob de tooa de base de datos de SQL Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.  

**Servicio vinculado a Azure SQL Database:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Vea hello [servicio vinculado de SQL Azure](#linked-service) sección para obtener lista de Hola de propiedades admitidas por este servicio vinculado.

**Servicio vinculado de almacenamiento de blobs de Azure:**

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
Vea hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) artículo para obtener lista de Hola de propiedades admitidas por este servicio vinculado.


**Conjunto de datos de entrada SQL de Azure:**

ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en SQL Azure y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.

Establecer "externo": "true" informa a servicio de Azure Data Factory de Hola ese conjunto de datos de hello es toohello externo factoría de datos y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

Vea hello [propiedades de tipo de conjunto de datos de SQL Azure](#dataset) sección para obtener lista de Hola de propiedades admitidas por este tipo de conjunto de datos.  

**Conjunto de datos de salida de blob de Azure:**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
Vea hello [propiedades de tipo de conjunto de datos de Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) sección para obtener lista de Hola de propiedades admitidas por este tipo de conjunto de datos.  

**Actividad de copia en una canalización con el origen SQL y el receptor de blob:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
En el ejemplo de Hola, **sqlReaderQuery** se especifica para hello SqlSource. Hola actividad de copia ejecuta esta consulta en datos de base de datos de SQL Azure origen tooget Hola Hola. Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).

Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura del conjunto de datos de hello JSON Hola son toobuild usado un toorun consulta contra Hola base de datos de SQL Azure. Por ejemplo: `select column1, column2 from mytable`. Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.

Vea hello [origen Sql](#sqlsource) sección y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de Hola de propiedades admitidas por SqlSource y BlobSink.

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a>Ejemplo: Copiar los datos de Blob de Azure tooAzure base de datos SQL
ejemplo de Hola define Hola siguiendo las entidades de la factoría de datos:  

1. Un servicio vinculado de tipo [AzureSqlDatabase](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSqlTable](#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [SqlSink](#copy-activity-properties).

ejemplo de Hola copia datos de serie temporal (cada hora, diariamente, etc.) de tabla de tooa de blobs de Azure en la base de datos SQL de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado SQL de Azure:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Vea hello [servicio vinculado de SQL Azure](#linked-service) sección para obtener lista de Hola de propiedades admitidas por este servicio vinculado.

**Servicio vinculado de almacenamiento de blobs de Azure:**

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
Vea hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) artículo para obtener lista de Hola de propiedades admitidas por este servicio vinculado.


**Conjunto de datos de entrada de blob de Azure:**

Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1). Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola. "externo": "true" configuración informa a servicio de factoría de datos de Hola que esta tabla es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
Vea hello [propiedades de tipo de conjunto de datos de Blob de Azure](data-factory-azure-blob-connector.md#dataset-properties) sección para obtener lista de Hola de propiedades admitidas por este tipo de conjunto de datos.

**Conjunto de datos de salida de Azure SQL Database:**

ejemplo Hello copia la tabla de tooa de datos denominada "MyTable" en SQL Azure. Crear tabla de hello en SQL Azure con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola. Se agregan nuevas filas toohello tabla cada hora.

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
Vea hello [propiedades de tipo de conjunto de datos de SQL Azure](#dataset) sección para obtener lista de Hola de propiedades admitidas por este tipo de conjunto de datos.

**Una actividad de copia en una canalización con el origen de blob y el receptor SQL:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**SqlSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
Vea hello [receptor de Sql](#sqlsink) sección y [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de Hola de propiedades admitidas por SqlSink y BlobSource.

## <a name="identity-columns-in-hello-target-database"></a>Columnas de identidad en la base de datos de destino de Hola
En esta sección se proporciona un ejemplo para copiar datos de una tabla de origen sin una tabla de destino de tooa de columna de identidad con una columna de identidad.

**Tabla de origen:**

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Tabla de destino:**

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
Tenga en cuenta que esa tabla de destino de hello tiene una columna de identidad.

**Definición de JSON del conjunto de datos de origen**

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**Definición de JSON del conjunto de datos de destino**

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

Tenga en cuenta que la tabla de origen y de destino tienen un esquema diferente (el destino tiene una columna adicional con identidad). En este escenario, necesita toospecify **estructura** propiedad en la definición de conjunto de datos de destino de hello, que no incluye la columna de identidad de Hola.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Invocación del procedimiento almacenado desde el receptor de SQL
Para obtener un ejemplo de invocación a un procedimiento almacenado de receptor SQL en una actividad de copia de una canalización, consulte el artículo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocación de un procedimiento almacenado para el receptor SQL en la actividad de copia). 

## <a name="type-mapping-for-azure-sql-database"></a>Asignación de tipos para Azure SQL Database
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Al mover datos tooand de base de datos de SQL Azure, hello siguientes usan las asignaciones son del tipo de too.NET de tipo SQL y viceversa. asignación de Hello es igual a la asignación de tipo de datos de SQL Server para ADO.NET Hola.

| Tipo de motor de base de datos SQL Server | Tipo .NET Framework |
| --- | --- |
| bigint |Int64 |
| binary |Byte[] |
| bit |Booleano |
| char |String, Char[] |
| fecha |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |Datetimeoffset |
| Decimal |Decimal |
| FILESTREAM attribute (varbinary(max)) |Byte[] |
| Float |Doble |
| imagen |Byte[] |
| int |Int32 |
| money |Decimal |
| nchar |String, Char[] |
| ntext |String, Char[] |
| numeric |Decimal |
| nvarchar |String, Char[] |
| real |Single |
| rowversion |Byte[] |
| smalldatetime |DateTime |
| smallint |Int16 |
| smallmoney |Decimal |
| sql_variant |Object * |
| text |String, Char[] |
| Twitter en tiempo |timespan |
| timestamp |Byte[] |
| tinyint |Byte |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String, Char[] |
| xml |xml |

## <a name="map-source-toosink-columns"></a>Asignar columnas de origen toosink
toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Copia repetible
Cuando se copian datos tooSQL base de datos de servidor, actividad de copia de hello anexa la tabla de datos toohello receptor de forma predeterminada. en su lugar, vea tooperform un UPSERT [tooSqlSink escritura repetible](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artículo. 

Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento. Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
