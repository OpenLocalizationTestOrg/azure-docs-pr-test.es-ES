---
title: aaaMove tooand de datos de SQL Server | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos de SQL Server de base de datos que es local o en una máquina virtual de Azure mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>Mover tooand de datos de SQL Server local o en IaaS (VM de Azure) mediante Data Factory de Azure
Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de SQL Server local. Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola. 

## <a name="supported-scenarios"></a>Escenarios admitidos
Puede copiar datos **desde una base de datos de SQL Server** toohello siguientes almacenes de datos:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Puede copiar los datos de hello siguientes almacenes de datos **base de datos de SQL Server tooa**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>Versiones admitidas de SQL Server
Esta compatibilidad del conector de SQL Server copian datos de / toohello después de las versiones de instancia hospedada en local o en IaaS de Azure mediante la autenticación de Windows y autenticación de SQL: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005

## <a name="enabling-connectivity"></a>Habilitación de la conectividad
conceptos de Hola y los pasos necesarios para conectar con SQL Server hospedado en local o en Azure IaaS (infraestructura como-servicio) las máquinas virtuales se Hola mismo. En ambos casos, debe toouse Data Management Gateway para la conectividad.

Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola. La configuración de una instancia de puerta de enlace es un requisito previo para conectarse con SQL Server.

Durante la instalación de puerta de enlace en hello mismo local instancia de máquina virtual de máquina o en la nube como Hola SQL Server para mejorar el rendimiento, se recomienda instalarlos en equipos diferentes. Tener puerta de enlace de Hola y SQL Server en equipos diferentes reduce la contención de recursos.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con actividad de copia que mueva los datos desde una base de datos de SQL Server local o hacia ella mediante el uso de diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos: 

1. Crear una **factoría de datos**. Una factoría de datos puede contener una o más canalizaciones. 
2. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink. Por ejemplo, si va a copiar datos desde un tooan de base de datos de SQL Server almacenamiento de blobs de Azure, cree dos toolink servicios vinculados su base de datos de SQL Server y la factoría de datos de tooyour de cuenta de almacenamiento de Azure. Para las propiedades de servicio vinculado que son la base de datos de servidor tooSQL específicos, consulte [vinculado propiedades del servicio](#linked-service-properties) sección. 
3. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. En el ejemplo de Hola mencionado en el último paso de hello, cree una tabla SQL de conjunto de datos toospecify hello en la base de datos de SQL Server que contiene los datos de entrada de Hola. Crear contenedor de blobs Hola de otro conjunto de datos toospecify y carpeta Hola que contiene datos de hello copiados de Hola de base de datos de SQL Server. Para las propiedades de conjunto de datos que son la base de datos de servidor tooSQL específicos, consulte [propiedades de conjunto de datos](#dataset-properties) sección.
4. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. En el ejemplo de Hola que se ha mencionado anteriormente, use SqlSource como un origen y BlobSink como un receptor para la actividad de copia de Hola. De forma similar, si va a copiar desde el almacenamiento de blobs de Azure tooSQL base de datos del servidor, usar BlobSource y SqlSink de actividad de copia de Hola. Para copiar propiedades de actividad que son específico tooSQL base de datos de servidor, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección. Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia y desde una base de datos de SQL Server local, vea [ejemplos JSON](#json-examples-for-copying-data-from-and-to-sql-server) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooSQL Server: 

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Crear un servicio vinculado de tipo **onpremisessqlserver** toolink una factoría de datos local tooa de base de datos de SQL Server. Hello en la tabla siguiente proporciona la descripción del servicio de SQL Server vinculado de JSON elementos tooon local específico.

Hello en la tabla siguiente proporciona una descripción para JSON elementos específico tooSQL servicio del servidor vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **onpremisessqlserver**. |Sí |
| connectionString |Especificar información de connectionString necesaria tooconnect toohello en SQL Server base de datos local con autenticación de SQL o autenticación de Windows. |Sí |
| gatewayName |Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar la base de datos de SQL Server de tooconnect toohello local. |Sí |
| nombre de usuario |Especifique el nombre de usuario si usa la autenticación de Windows. Ejemplo: **nombreDeDominio\\nombreDeUsuario**. |No |
| Contraseña |Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola. |No |

Puede cifrar las credenciales con hello **New-AzureRmDataFactoryEncryptValue** cmdlet y usarlos en la cadena de conexión de hello tal y como se muestra en el siguiente ejemplo de Hola (**EncryptedCredential** propiedad):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a>Muestras
**JSON para usar autenticación de SQL**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**JSON para usar autenticación de Windows**

Data Management Gateway suplantará Hola especificada base de datos de usuario cuenta tooconnect toohello local SQL Server. 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
En los ejemplos de hello, ha utilizado un conjunto de datos de tipo **SqlServerTable** toorepresent una tabla en una base de datos de SQL Server.  

Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy de un conjunto de datos JSON son similares en todos los tipos de conjunto de datos (SQL Server, blob de Azure, tabla de Azure, etc.).

sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. Hola **typeProperties** sección Hola conjunto de datos de tipo **SqlServerTable** tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| tableName |Nombre de tabla de Hola o vista en la instancia de base de datos de SQL Server de Hola que servicio vinculado hace referencia a. |Sí |

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Si va a mover datos desde una base de datos de SQL Server, configure tipo de origen de hello en la actividad de copia de hello demasiado**SqlSource**. De forma similar, si va a mover la base de datos de SQL Server de tooa de datos, Establece el tipo de receptor de hello en actividad de copia de hello demasiado**SqlSink**. Esta sección proporciona una lista de propiedades admitidas por SqlSource y SqlSink.

Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

> [!NOTE]
> Hola actividad de copia toma solo una entrada y produce un único resultado.

Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

### <a name="sqlsource"></a>SqlSource
Cuando el origen de una actividad de copia es del tipo **SqlSource**, Hola propiedades siguientes está disponible en **typeProperties** sección:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Usar datos de tooread de hello consulta personalizada. |Cadena de consulta SQL. Por ejemplo: select * from MyTable. Puede hacer referencia a varias tablas de base de datos de hello al que hace referencia el conjunto de datos de entrada de Hola. Si no se especifica, Hola instrucción SQL ejecutada: select from MyTable. |No |
| sqlReaderStoredProcedureName |Nombre del programa Hola a procedimiento almacenado que lee los datos de la tabla de origen de Hola. |Nombre del programa Hola a procedimiento almacenado. Hola última instrucción de SQL debe ser una instrucción SELECT en el procedimiento almacenado de Hola. |No |
| storedProcedureParameters |Parámetros de hello procedimiento almacenan. |Pares nombre-valor. Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola. |No |

Si hello **sqlReaderQuery** se especifica para hello SqlSource, hello actividad de copia ejecuta esta consulta en datos de Hola de hello base de datos de SQL Server origen tooget.

Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros).

Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura Hola son toobuild usado un toorun de consulta select contra Hola base de datos de SQL Server. Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.

> [!NOTE]
> Cuando usas **sqlReaderStoredProcedureName**, seguirá necesitando toospecify un valor para hello **tableName** propiedad Hola de conjunto de datos JSON. Pero no se ha realizado ninguna validación en esta tabla.

### <a name="sqlsink"></a>SqlSink
**SqlSink** admite Hola propiedades siguientes:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar. |timespan<br/><br/> Ejemplo: "00:30:00" (30 minutos). |No |
| writeBatchSize |Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize. |Entero (número de filas) |No (valor predeterminado = 10000) |
| sqlWriterCleanupScript |Especificar la consulta para tooexecute de actividad de copia que se limpian los datos de un segmento específico. Para más información, consulte la sección [copia repetible](#repeatable-copy). |Una instrucción de consulta. |No |
| sliceIdentifierColumnName |Especifique el nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar. Para más información, consulte la sección [copia repetible](#repeatable-copy). |Nombre de columna de una columna con el tipo de datos binarios (32). |No |
| sqlWriterStoredProcedureName |Nombre del programa Hola a procedimiento almacenado que upserts (actualizaciones o inserciones) los datos en la tabla de destino de Hola. |Nombre del programa Hola a procedimiento almacenado. |No |
| storedProcedureParameters |Parámetros de hello procedimiento almacenan. |Pares nombre-valor. Nombres y mayúsculas y minúsculas de los parámetros deben coincidir con los nombres Hola y mayúsculas y minúsculas de los parámetros del procedimiento almacenado de Hola. |No |
| sqlWriterTableType |Especifique toobe de nombre de tipo de tabla utilizado en el procedimiento almacenado de Hola. Actividad de copia pone datos Hola que se mueven en una tabla temporal con este tipo de tabla. Código de procedimiento almacenado, a continuación, puede combinar datos de Hola se copian con los datos existentes. |Un nombre de tipo de tabla. |No |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>Ejemplos JSON para copiar datos desde y tooSQL Server
Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Hola siguientes ejemplos muestran cómo toocopy tooand de datos de SQL Server y el almacenamiento de blobs de Azure. Sin embargo, se pueden copiar datos **directamente** desde cualquiera de tooany orígenes de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>Ejemplo: Copiar los datos de SQL Server tooAzure Blob
Hola el siguiente ejemplo se muestra:

1. Un servicio vinculado de tipo [OnPremisesSqlServer](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [SqlServerTable](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [SqlSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de serie temporal de un tooan de tabla de SQL Server blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

Como primer paso, configurar la puerta de enlace de administración de datos de Hola. instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.

**Servicio vinculado de SQL Server**
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
**Servicio vinculado de almacenamiento de blobs de Azure**

```json
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
**Conjunto de datos de entrada de SQL Server**

ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en SQL Server y contiene una columna denominada "timestampcolumn" para los datos de serie temporal. Puede consultar a través de varias tablas dentro de hello misma mediante un único conjunto de datos, pero una sola tabla de base de datos debe utilizarse para typeProperty de nombre de tabla del conjunto de datos de Hola.

Establecer "externo": "true" informa a servicio de factoría de datos ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**Conjunto de datos de salida de blob de Azure**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1). ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.

```json
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
**Canalización con actividad de copia**

canalización de Hello contiene una actividad de copia que esté configurado toouse estos conjuntos de datos de entrada y salidas o toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlSource** y **receptor** tipo está establecido demasiado**BlobSink**. consulta SQL Hola especificada para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
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
En este ejemplo, **sqlReaderQuery** se especifica para hello SqlSource. Hola actividad de copia ejecuta esta consulta contra Hola datos de saludo de tooget de origen de base de datos de SQL Server. Como alternativa, puede especificar un procedimiento almacenado mediante la especificación de hello **sqlReaderStoredProcedureName** y **storedProcedureParameters** (si hello procedimiento almacenado toma parámetros). Hola sqlReaderQuery puede hacer referencia a varias tablas de base de datos de hello al que hace referencia el conjunto de datos de entrada de Hola. No es limitado tooonly Hola tabla establecido como Hola typeProperty de nombre de tabla del conjunto de datos.

Si no especifica sqlReaderQuery o sqlReaderStoredProcedureName, Hola se definieron las columnas en la sección sobre la estructura Hola son toobuild usado un toorun de consulta select contra Hola base de datos de SQL Server. Si definición de conjunto de datos de hello no tiene la estructura de hello, se seleccionan todas las columnas de tabla de Hola.

Vea hello [origen Sql](#sqlsource) sección y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de Hola de propiedades admitidas por SqlSource y BlobSink.

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>Ejemplo: Copiar los datos de Blob de Azure tooSQL Server
Hola el siguiente ejemplo se muestra:

1. Hola vinculado servicio del tipo [onpremisessqlserver](#linked-service-properties).
2. Hola vinculado servicio del tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
5. Hola [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [SqlSink](#sql-server-copy-activity-type-properties).

ejemplo de Hola copia datos de series temporales de una tabla de SQL Server tooa de blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado de SQL Server**

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
**Servicio vinculado de almacenamiento de blobs de Azure**

```json
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
**Conjunto de datos de entrada de blob de Azure**

Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1). Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando. ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola. "externo": "true" configuración informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```json
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
**Conjunto de datos de salida de SQL Server**

ejemplo Hello copia la tabla de tooa de datos denominada "MyTable" en SQL Server. Crear tabla de hello en SQL Server con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola. Se agregan nuevas filas toohello tabla cada hora.

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**Canalización con actividad de copia**

canalización de Hello contiene una actividad de copia que esté configurado toouse estos conjuntos de datos de entrada y salidas o toorun programada cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** y **receptor** tipo está establecido demasiado**SqlSink**.

```json
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
            "name": " SqlServerOutput "
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

## <a name="troubleshooting-connection-issues"></a>Solución de problemas de conexión
1. Configurar las conexiones remotas de SQL Server tooaccept. Inicie **SQL Server Management Studio**, haga clic con el botón derecho en **Servidor** y después en **Propiedades**. Seleccione **conexiones** en lista de Hola y verificación **server toohello de permitir conexiones remotas**.

    ![Habilitar conexiones remotas](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    Vea [configurar la opción de configuración de servidor de acceso remoto de hello](https://msdn.microsoft.com/library/ms191464.aspx) para obtener pasos detallados.
2. Inicie el **Administrador de configuración de SQL Server**. Expanda **configuración de red de SQL Server** para saludo de la instancia desee y seleccione **protocolos para MSSQLSERVER**. Debería ver los protocolos en el panel derecho de Hola. Para habilitar TCP/IP, haga clic con el botón derecho en **TCP/IP** y haga clic en **Habilitar**.

    ![Habilitar TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    Consulte [Habilitar o deshabilitar un protocolo de red de servidor](https://msdn.microsoft.com/library/ms191294.aspx) para ver información y maneras alternativas de habilitar el protocolo TCP/IP.
3. En la consulta Hola la misma ventana, haga doble clic en **TCP/IP** toolaunch **propiedades TCP/IP** ventana.
4. Cambiar toohello **direcciones IP** ficha. Desplácese hacia abajo toosee **IPAll** sección. Tome nota de Hola ** el puerto TCP ** (valor predeterminado es **1433**).
5. Crear un **regla de Firewall de Windows hello** en hello máquina tooallow el tráfico entrante a través de este puerto.  
6. **Compruebe la conexión**: tooconnect toohello SQL Server con el nombre completo, use SQL Server Management Studio desde un equipo diferente. Por ejemplo: <machine><domain>.corp<company>.com,1433.

   > [!IMPORTANT]

   > Vea [mover datos entre orígenes locales y en la nube Hola con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obtener información detallada.
   >
   > Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Columnas de identidad en la base de datos de destino de Hola
En esta sección se proporciona un ejemplo que copia datos de una tabla de origen con ninguna tabla de destino de tooa de columna de identidad con una columna de identidad.

**Tabla de origen:**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Tabla de destino:**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

Tenga en cuenta que esa tabla de destino de hello tiene una columna de identidad.

**Definición de JSON del conjunto de datos de origen**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
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

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
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
Para ver un ejemplo de invocación de un procedimiento almacenado desde el receptor de SQL en una actividad de copia de una canalización, consulte el artículo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocación de un procedimiento almacenado desde el receptor de SQL en la actividad de copia).

## <a name="type-mapping-for-sql-server"></a>Asignación de tipos para SQL Server
Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, Hola actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:

1. Convertir del tipo de origen nativo tipos too.NET
2. Convertir el tipo de receptor de toonative de tipo .NET

Al mover datos demasiado & de SQL server, Hola siguientes asignaciones se usan del tipo de too.NET de tipo SQL y viceversa.

asignación de Hello es igual a la asignación de tipo de datos de SQL Server para ADO.NET Hola.

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

## <a name="mapping-source-toosink-columns"></a>Asignar columnas de origen toosink
columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Copia repetible
Cuando se copian datos tooSQL base de datos de servidor, actividad de copia de hello anexa la tabla de datos toohello receptor de forma predeterminada. en su lugar, vea tooperform un UPSERT [tooSqlSink escritura repetible](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artículo. 

Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos. En Azure Data Factory, puede volver a ejecutar un segmento manualmente. También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error. Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento. Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
