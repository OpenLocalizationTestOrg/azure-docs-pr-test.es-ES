---
title: aaaMove datos hacia y desde la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Aprenda a mover datos hacia y desde una colección de Azure Cosmos DB mediante Azure Data Factory"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>Mover datos tooand de base de datos de Azure Cosmos con Data Factory de Azure
Este artículo explica cómo toouse Hola actividad de copia de datos de Data Factory de Azure toomove de base de datos de Azure Cosmos (API de documentos). Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola. 

Puede copiar datos desde cualquier origen compatible datos almacenan tooAzure Cosmos DB o de datos de base de datos de Azure Cosmos tooany admitida receptores almacenan. Para obtener una lista de almacenes de datos admite como orígenes o receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla. 

> [!IMPORTANT]
> El conector de Azure Cosmos DB solo admite la API de DocumentDB.

datos de toocopy como-es hacia/desde archivos JSON o a otra colección de Cosmos DB, vea [documentos JSON de importación y exportación de](#importexport-json-documents).

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva datos hacia y desde Cosmos DB mediante diferentes herramientas o API.

toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.

También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos: 

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy hacia/desde la base de datos de Cosmos, vea [ejemplos JSON](#json-examples) sección de este artículo. 

Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específicas tooCosmos base de datos: 

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona la descripción de JSON elementos específico tooAzure servicio vinculado de base de datos de Cosmos.

| **Propiedad** | **Descripción** | **Obligatorio** |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **DocumentDb** |Sí |
| connectionString |Especifique la información necesaria de base de datos de tooconnect tooAzure Cosmos DB. |Sí |

Ejemplo:

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, consulte toohello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy de un conjunto de datos JSON son similares en todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. Hola typeProperties sección Hola conjunto de datos de tipo **DocumentDbCollection** tiene Hola propiedades siguientes.

| **Propiedad** | **Descripción** | **Obligatorio** |
| --- | --- | --- |
| collectionName |Nombre de la colección de documentos de base de datos de Cosmos Hola. |Sí |

Ejemplo:

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a>Esquema de Data Factory
En los almacenes de datos sin esquema como base de datos de Azure Cosmos, Hola servicio Data Factory deduce el esquema de hello en uno de hello siguientes maneras:  

1. Si especifica estructura Hola de datos mediante el uso de hello **estructura** propiedad en la definición de conjunto de datos de hello, Hola servicio Data Factory respeta esta estructura como esquema de Hola. En este caso, si una fila no contiene un valor para una columna, se le proporcionará un valor nulo.
2. Si no especifica estructura Hola de datos mediante el uso de hello **estructura** propiedad en la definición de conjunto de datos de hello, Hola servicio Data Factory deduce el esquema de hello utilizando Hola primera fila de datos de Hola. En este caso, si la primera fila de hello no contiene el esquema completo de hello, algunas columnas faltará en el resultado de hello de operación de copia.

Por lo tanto, para orígenes de datos sin esquemas, se recomienda Hola es toospecify estructura de Hola de datos mediante Hola **estructura** propiedad.

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, consulte toohello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

> [!NOTE]
> Hola actividad de copia toma solo una entrada y produce un único resultado.

Propiedades disponibles en la sección de typeProperties Hola de actividad de hello en hello otra parte varían con cada tipo de actividad y en el caso de actividad de copia varían en función de los tipos de Hola de orígenes y receptores.

En el caso de actividad de copia cuando el origen es de tipo **DocumentDbCollectionSource** Hola propiedades siguientes está disponible en **typeProperties** sección:

| **Propiedad** | **Descripción** | **Valores permitidos** | **Obligatorio** |
| --- | --- | --- | --- |
| query |Especifique los datos de hello consulta tooread. |Cadena de consulta admitida por Azure Cosmos DB. <br/><br/>Ejemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |No <br/><br/>Si no se especifica, Hola instrucción SQL que se ejecuta:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Tooindicate de carácter especial que Hola documento está anidada |Cualquier carácter. <br/><br/>Azure Cosmos DB es un almacén NoSQL para documentos JSON, en el que se permiten estructuras anidadas. Factoría de datos de Azure permite jerarquía toodenote de usuario a través de nestingSeparator, que es "." Hola por encima de los ejemplos. Con separador de hello, actividad de copia de hello generará un objeto de Hola "Name" con los elementos secundarios de tres too"Name.First primera, central y Last, función", "Name.Middle" y "Name.Last" Hola de definición de tabla. |No |

**DocumentDbCollectionSink** admite Hola propiedades siguientes:

| **Propiedad** | **Descripción** | **Valores permitidos** | **Obligatorio** |
| --- | --- | --- | --- |
| nestingSeparator |Se necesita un carácter especial en hello tooindicate de nombre de columna de origen que anidados de documento. <br/><br/>Por ejemplo anteriormente: `Name.First` en la salida de hello tabla genera Hola siguiendo la estructura JSON en el documento de base de datos de Cosmos hello:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Carácter que es usado tooseparate niveles de anidamiento.<br/><br/>El valor predeterminado es `.` (punto). |Carácter que es usado tooseparate niveles de anidamiento. <br/><br/>El valor predeterminado es `.` (punto). |
| writeBatchSize |Número de paralelo solicita documentos de toocreate de servicio de base de datos de Cosmos tooAzure.<br/><br/>Puede ajustar el rendimiento de hello cuando se copian datos de base de datos de Cosmos mediante esta propiedad. Puede esperar un rendimiento mejor al aumentar el valor writeBatchSize porque se envían más solicitudes paralelas tooCosmos base de datos. Sin embargo deberá tooavoid limitación que puede producir mensajes de bienvenida del error: "Solicitud velocidad es grande".<br/><br/>La limitación de solicitudes se decide mediante una serie de factores, incluidos tamaño de los documentos, número de términos en los documentos, directiva de indexación de colección de destino, etc. Para las operaciones de copia, puede usar una mejor hello toohave de colección (por ejemplo, S3) mayoría rendimiento disponible (2500 solicitud unidades/segundo). |Entero |No (valor predeterminado: 5) |
| writeBatchTimeout |Tiempo de espera para hello operación toocomplete antes de expirar. |timespan<br/><br/> Ejemplo: "00:30:00" (30 minutos). |No |

## <a name="importexport-json-documents"></a>Importación o exportación de documentos JSON
Con este conector de Cosmos DB, le resultará muy sencillo

* Importar documentos JSON desde varios orígenes en Cosmos DB, incluido Azure Blob, Azure Data Lake, el sistema de archivos local u otros almacenes basados en archivos compatibles con Azure Data Factory.
* Exportar documentos JSON de la colección de Cosmos DB a varios almacenes basados en archivos.
* Migrar datos entre dos colecciones de Cosmos DB como están.

copiar de este tipo independiente del esquema tooachieve, 
* Cuando utilice el Asistente para copiar, compruebe hello **"Exportar como-es tooJSON archivos o un conjunto de Cosmos DB"** opción.
* Cuando con la edición de JSON, no se especifican Hola "estructura" sección en conjuntos de datos de base de datos de Cosmos ni propiedad "nestingSeparator" en la base de datos de Cosmos origen/receptor en la actividad de copia. tooimport de / tooJSON archivos de exportación, en el conjunto de datos de almacén de archivos de hello especificar tipo de formato como "JsonFormat", "filePattern" de la configuración y omitir la configuración de formato de hello rest, vea [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format) sección de detalles.

## <a name="json-examples"></a>Ejemplos de JSON
Hello en los ejemplos siguientes proporcionan las definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Muestran cómo toocopy tooand de datos de la base de datos de Azure Cosmos y almacenamiento de blobs de Azure. Sin embargo, se pueden copiar datos **directamente** desde cualquiera de hello orígenes tooany de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>Ejemplo: Copiar los datos de base de datos de Azure Cosmos tooAzure Blob
ejemplo de Hola a continuación se muestra:

1. Un servicio vinculado de tipo [DocumentDb](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [DocumentDbCollection](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [DocumentDbCollectionSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia los datos en la base de datos de Azure Cosmos tooAzure Blob. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

**Servicio vinculado Azure Cosmos DB:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Servicio vinculado de Azure Blob Storage:**

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
**Conjunto de datos de entrada de DocumentDB de Azure:**

ejemplo de Hola se supone que tiene una colección denominada **persona** en una base de datos de la base de datos de Azure Cosmos.

Establecer "externo": "true" y especifica externalData información de directiva Hola Data Factory de Azure del servicio tabla Hola se factoría de datos externos toohello no producidos por una actividad de factoría de datos de Hola.

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Conjunto de datos de salida de blob de Azure:**

Datos son tooa copiado nuevo blob cada hora con la ruta de acceso de Hola para blob Hola reflejar Hola específico datetime con granularidad de hora.

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Documento JSON de ejemplo de Hola colección persona en una base de datos de la base de datos de Cosmos:

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
Cosmos DB admite la consulta de documentos mediante una sintaxis similar a la de SQL en documentos jerárquicos JSON.

Ejemplo: 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

siguiente Hola canalización copia datos de hello colección persona Hola tooan de base de datos de base de datos de Azure Cosmos blobs de Azure. Como parte de Hola Hola de actividad de copia se han especificado los conjuntos de datos de entrada y salidas.  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>Ejemplo: Copiar los datos de Blob de Azure tooAzure Cosmos DB 
ejemplo de Hola a continuación se muestra:

1. Un servicio vinculado de tipo [DocumentDb](#azure-documentdb-linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [DocumentDbCollection](#azure-documentdb-dataset-type-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).

ejemplo de Hola copia datos de blob de Azure tooAzure Cosmos DB. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

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
**Servicio vinculado Azure Cosmos DB:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Conjunto de datos de entrada de blob de Azure:**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
**Conjunto de datos de salida de Azure Cosmos DB:**

ejemplo de Hola copia la colección de tooa de datos denominado a "Persona".

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
siguiente Hola canalización copia datos de Blob de Azure toohello colección persona Hola Cosmos DB. Como parte de Hola Hola de actividad de copia se han especificado los conjuntos de datos de entrada y salidas.

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
Si la entrada de blob de ejemplo de Hola es como

```
1,John,,Doe
```
Hola, a continuación, la salida que JSON en la base de datos de Cosmos será como:

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
Azure Cosmos DB es un almacén NoSQL para documentos JSON, en el que se permiten estructuras anidadas. Factoría de datos de Azure permite jerarquía toodenote de usuario a través de **nestingSeparator**, que es "." en este ejemplo. Con separador de hello, actividad de copia de hello generará un objeto de Hola "Name" con los elementos secundarios de tres too"Name.First primera, central y Last, función", "Name.Middle" y "Name.Last" Hola de definición de tabla.

## <a name="appendix"></a>Anexo
1. **Pregunta:** Hola actualización de soporte técnico de la actividad de copia de los registros existentes?

    **Respuesta:** No.
2. **Pregunta:** como lo hace un reintento de una solución de base de datos de Cosmos tooAzure copia con ya copió registros?

    **Respuesta:** si registros tienen un campo de "ID" y la operación de copia de hello intenta tooinsert un registro con hello mismo Id. de operación de copia de hello produce un error.  
3. **Pregunta:** ¿Admite Data Factory el [intervalo o las particiones de datos basadas en hash](../documentdb/documentdb-partition-data.md)?

    **Respuesta:** No.
4. **Pregunta:** ¿Puedo especificar más de una colección de Azure Cosmos DB para una tabla?

    **Respuesta:** No. Solo se puede especificar una colección cada vez.

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
