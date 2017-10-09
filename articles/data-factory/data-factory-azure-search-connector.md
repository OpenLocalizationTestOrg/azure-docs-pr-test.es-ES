---
title: "índice de tooSearch aaaPush datos mediante el uso de la factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopush datos tooAzure índice de búsqueda mediante el uso de Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>Inserción de índice de búsqueda de Azure de tooan de datos mediante Data Factory de Azure
Este artículo describe cómo toouse Hola actividad de copia toopush los datos de un origen compatible datos almacenan tooAzure índice de búsqueda. Almacenes de datos de origen compatible se muestran en la columna de origen de Hola de hello [admite orígenes y receptores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. En este artículo se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia y combinaciones de almacén de datos admitidos.

## <a name="enabling-connectivity"></a>Habilitación de la conectividad
tooallow servicio Data Factory conectarse tooan un almacén de datos local, instale Data Management Gateway en su entorno local. Puerta de enlace se puede instalar en hello mismo equipo que hospeda los datos de origen de hello almacenar o en un tooavoid máquina independiente que compiten por los recursos con datos de hello almacenar.

Puerta de enlace de administración de datos se conecta a servicios de toocloud de orígenes de datos locales de forma segura y administrada. Consulte el artículo [Mover datos entre orígenes locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener más información acerca de Data Management Gateway.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con la actividad de copia que traslada los datos de un índice de búsqueda de tooAzure del almacén de datos de origen mediante el uso de distintas herramientas y API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos: 

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son el índice de búsqueda de tooAzure de toocopy usa datos, vea [ejemplo de JSON: copiar los datos de índice de búsqueda de tooAzure de SQL Server local](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAzure índice de búsqueda:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado

Hello en la tabla siguiente proporciona descripciones para los elementos JSON que son toohello específico del servicio Búsqueda de Azure vinculada.

| Propiedad | Descripción | Obligatorio |
| -------- | ----------- | -------- |
| type | propiedad de tipo Hello debe establecerse en: **AzureSearch**. | Sí |
| url | Dirección URL de hello servicio Búsqueda de Azure. | Sí |
| key | Clave de administrador de hello servicio Búsqueda de Azure. | Sí |

## <a name="dataset-properties"></a>Propiedades del conjunto de datos

Para obtener una lista completa de secciones y propiedades que están disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como estructura, disponibilidad y directiva de un JSON de conjunto de datos son similares para todos los tipos de conjunto de datos. Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos. Hola typeProperties sección un conjunto de datos de tipo hello **AzureSearchIndex** tiene Hola propiedades siguientes:

| Propiedad | Descripción | Obligatorio |
| -------- | ----------- | -------- |
| type | se debe establecer propiedad de tipo Hello demasiado**AzureSearchIndex**.| Sí |
| indexName | Nombre del índice de búsqueda de Azure Hola. Factoría de datos no crea el índice de Hola. índice de Hello debe existir en la búsqueda de Azure. | Sí |


## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades que están disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como el nombre, la descripción, las tablas de entrada y salida, y las distintas directivas) están disponibles en todos los tipos de actividades. Mientras que las propiedades disponibles en la sección de hello typeProperties varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Actividad de copia al receptor de hello es de tipo hello **AzureSearchIndexSink**, Hola propiedades siguientes está disponible en la sección typeProperties:

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Especifica si toomerge o reemplazar cuando un documento ya existe en el índice de Hola. Vea hello [WriteBehavior propiedad](#writebehavior-property).| Combinar (predeterminado)<br/>Cargar| No |
| WriteBatchSize | Carga datos en el índice de búsqueda de Azure de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize. Vea hello [propiedad valor WriteBatchSize](#writebatchsize-property) para obtener más información. | 1 too1, 000. El valor predeterminado es 1000. | No |

### <a name="writebehavior-property"></a>Propiedad WriteBehavior
AzureSearchSink realiza una operación upsert al escribir los datos. En otras palabras, al escribir un documento, si la clave de documento de hello ya existe en el índice de búsqueda de Azure de hello, búsqueda de Azure actualiza documento existente de hello en lugar de producir una excepción de conflicto.

Hola AzureSearchSink proporciona Hola siguiendo dos comportamientos upsert (mediante el uso de AzureSearch SDK):

- **Mezcla**: combinar todas las columnas de Hola de nuevo documento de hello con hello uno existente. Para las columnas con valor null en el nuevo documento de hello, se conserva el valor de Hola Hola uno existente.
- **Cargar**: reemplaza el documento nuevo Hola Hola uno ya existente. Para las columnas no especificadas en el nuevo documento de hello, Hola valor toonull si hay un valor distinto de null en el documento existente de Hola o no.

es el comportamiento predeterminado de Hello **mezcla**.

### <a name="writebatchsize-property"></a>Propiedad WriteBatchSize
Azure Search puede crear documentos como lotes. Un lote puede contener 1 too1, 000 acciones. Una acción controla una operación de carga/merge Hola de documento tooperform.

### <a name="data-type-support"></a>Compatibilidad con los tipos de datos
Hello siguiente tabla especifica si se admite un tipo de datos de búsqueda de Azure o no.

| Tipo de datos de Azure Search | Compatible con el receptor de Azure Search |
| ---------------------- | ------------------------------ |
| Cadena | Y |
| Int32 | Y |
| Int64 | Y |
| Double | Y |
| Booleano | Y |
| DataTimeOffset | Y |
| Matriz de cadenas | N |
| GeographyPoint | N |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>Ejemplo de JSON: copiar los datos de índice de búsqueda de tooAzure de SQL Server local

Hola el siguiente ejemplo se muestra:

1.  Un servicio vinculado de tipo [AzureSearch](#linked-service-properties).
2.  Un servicio vinculado de tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).
3.  Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
4.  Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureSearchIndex](#dataset-properties).
4.  Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) y [AzureSearchIndexSink](#copy-activity-properties).

ejemplo de Hola copia datos de serie temporal de un índice de búsqueda de Azure local tooan de base de datos de SQL Server cada hora. propiedades JSON de Hello utilizados en este ejemplo se describen en los apartados siguientes a los ejemplos de hello.

Como primer paso, configurar la puerta de enlace de hello datos administración en el equipo local. instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.

**Servicio vinculado de Azure Search**:

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

**Servicio vinculado de SQL Server**

```JSON
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

**Conjunto de datos de entrada de SQL Server**

ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en SQL Server y contiene una columna denominada "timestampcolumn" para los datos de serie temporal. Puede consultar a través de varias tablas dentro de hello misma mediante un único conjunto de datos, pero una sola tabla de base de datos debe utilizarse para typeProperty de nombre de tabla del conjunto de datos de Hola.

Establecer "externo": "true" informa a servicio de factoría de datos ese conjunto de datos de hello es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.

```JSON
{
  "name": "SqlServerDataset",
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

**Conjunto de datos de salida Azure Search**:

Hola copias datos tooan búsqueda de Azure índice de ejemplo denominado **productos**. Factoría de datos no crea el índice de Hola. Hola tootest de ejemplo, cree un índice con este nombre. Crear el índice de búsqueda de Azure de hello con hello mismo número de columnas como en el conjunto de datos de entrada de Hola. Se agregan entradas nuevas toohello índice de búsqueda de Azure cada hora.

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**Actividad de copia en una canalización con origen SQL y receptor de índice de Azure Search:**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**SqlSource** y **receptor** tipo está establecido demasiado**AzureSearchIndexSink**. consulta SQL Hola especificada para hello **SqlReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

Si va a copiar datos desde un almacén de datos en la nube a Azure Search, la propiedad `executionLocation` es obligatoria. Hello siguiente fragmento JSON muestra es necesario en la actividad de copia de cambio de hello `typeProperties` como ejemplo. Comprobar [copiar datos entre almacenes de datos en la nube](data-factory-data-movement-activities.md#global) para obtener más detalles y los valores admitidos.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>Copia desde un origen en la nube
Si va a copiar datos desde un almacén de datos en la nube a Azure Search, la propiedad `executionLocation` es obligatoria. Hello siguiente fragmento JSON muestra es necesario en la actividad de copia de cambio de hello `typeProperties` como ejemplo. Comprobar [copiar datos entre almacenes de datos en la nube](data-factory-data-movement-activities.md#global) para obtener más detalles y los valores admitidos.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

También puede asignar columnas de toocolumns de conjunto de datos de origen del conjunto de datos de receptor en la definición de actividad de copia de Hola. Para obtener más información, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Rendimiento y optimización  
Vea hello [actividad de copia Guía de rendimiento y optimización](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento del movimiento de datos (actividad de copia) y toooptimize de diversas maneras.

## <a name="next-steps"></a>Pasos siguientes
Vea Hola siguientes artículos:

* [Tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso para la creación de una canalización con una actividad de copia.
