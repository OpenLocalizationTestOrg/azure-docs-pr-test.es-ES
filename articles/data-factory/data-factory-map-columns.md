---
title: columnas de conjunto de datos de aaaMapping de Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomap columnas toodestination columnas de origen."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a>Asignar columnas de conjunto de toodestination de columnas de conjunto de datos de origen
Asignación de columnas puede ser usado toospecify cómo especifican las columnas especificadas en hello "estructura" de toocolumns de asignación de tabla de origen de estructura"hello" de la tabla de receptor. Hola **columnMapping** propiedad está disponible en hello **typeProperties** sección de hello actividad de copia.

Asignación de columnas admite Hola los escenarios siguientes:

* Todas las columnas de estructura de conjunto de datos de origen de hello son columnas de tooall asignada en la estructura de conjunto de datos del receptor de Hola.
* Un subconjunto de columnas de hello en la estructura del conjunto de datos de origen de hello es asignada tooall columnas de estructura de conjunto de datos del receptor de Hola.

siguiente Hola es condiciones de error que se producen una excepción:

* Columnas menos o más columnas en hello "estructura" de receptor tabla que especifica en asignación de Hola.
* Asignación duplicada.
* Resultado de la consulta SQL no tiene un nombre de columna que se especifica en la asignación de Hola.

> [!NOTE]
> Hello en los ejemplos siguientes son para SQL Azure y Azure Blob pero tooany aplicables almacén de datos que admite conjuntos de datos rectangular. Ajustar el conjunto de datos y las definiciones de servicio vinculado en ejemplos toopoint toodata en origen de datos correspondiente de Hola.

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a>Ejemplo 1: asignación de blob de Azure SQL tooAzure de columna
En este ejemplo, tabla de entrada de hello tiene una estructura y señala tooa table de SQL en una base de datos de SQL Azure.

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

En este ejemplo, tabla de salida de hello tiene una estructura y señala tooa blob en el almacenamiento de blobs de Azure.

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
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
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Hola después JSON define una actividad de copia de una canalización. las columnas de Hola de origen asignan toocolumns en el receptor (**columnMappings**) mediante el uso de hello **traductor** propiedad.

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
**Flujo de asignación de columnas:**

![Flujo de asignación de columnas](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a>Ejemplo 2: columna asignación con la consulta SQL desde blob tooAzure de SQL Azure
En este ejemplo, una consulta SQL es tooextract usa datos de SQL Azure en lugar de especificar simplemente el nombre de la tabla de Hola y nombres de columna de hello en la sección "estructura". 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
En este caso, resultados de la consulta de hello son primera toocolumns asignada especificada en "estructura" de origen. A continuación, las columnas de Hola de origen "estructura" son toocolumns asignada en el receptor "estructura" con las reglas especificadas en columnMappings.  Supongamos que la consulta de hello devuelve 5 columnas, dos columnas más de las especificadas en hello "estructura" de origen.

**Flujo de asignación de columnas**

![Flujo de asignación de columnas 2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a>Pasos siguientes
Vea el artículo de Hola para obtener un tutorial sobre el uso de la actividad de copia: 

- [Copiar los datos de almacenamiento de blobs tooSQL base de datos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
