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
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a><span data-ttu-id="1bfbd-103">Asignar columnas de conjunto de toodestination de columnas de conjunto de datos de origen</span><span class="sxs-lookup"><span data-stu-id="1bfbd-103">Map source dataset columns toodestination dataset columns</span></span>
<span data-ttu-id="1bfbd-104">Asignación de columnas puede ser usado toospecify cómo especifican las columnas especificadas en hello "estructura" de toocolumns de asignación de tabla de origen de estructura"hello" de la tabla de receptor.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-104">Column mapping can be used toospecify how columns specified in hello “structure” of source table map toocolumns specified in hello “structure” of sink table.</span></span> <span data-ttu-id="1bfbd-105">Hola **columnMapping** propiedad está disponible en hello **typeProperties** sección de hello actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-105">hello **columnMapping** property is available in hello **typeProperties** section of hello Copy activity.</span></span>

<span data-ttu-id="1bfbd-106">Asignación de columnas admite Hola los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="1bfbd-106">Column mapping supports hello following scenarios:</span></span>

* <span data-ttu-id="1bfbd-107">Todas las columnas de estructura de conjunto de datos de origen de hello son columnas de tooall asignada en la estructura de conjunto de datos del receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-107">All columns in hello source dataset structure are mapped tooall columns in hello sink dataset structure.</span></span>
* <span data-ttu-id="1bfbd-108">Un subconjunto de columnas de hello en la estructura del conjunto de datos de origen de hello es asignada tooall columnas de estructura de conjunto de datos del receptor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-108">A subset of hello columns in hello source dataset structure is mapped tooall columns in hello sink dataset structure.</span></span>

<span data-ttu-id="1bfbd-109">siguiente Hola es condiciones de error que se producen una excepción:</span><span class="sxs-lookup"><span data-stu-id="1bfbd-109">hello following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="1bfbd-110">Columnas menos o más columnas en hello "estructura" de receptor tabla que especifica en asignación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-110">Either fewer columns or more columns in hello “structure” of sink table than specified in hello mapping.</span></span>
* <span data-ttu-id="1bfbd-111">Asignación duplicada.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-111">Duplicate mapping.</span></span>
* <span data-ttu-id="1bfbd-112">Resultado de la consulta SQL no tiene un nombre de columna que se especifica en la asignación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-112">SQL query result does not have a column name that is specified in hello mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="1bfbd-113">Hello en los ejemplos siguientes son para SQL Azure y Azure Blob pero tooany aplicables almacén de datos que admite conjuntos de datos rectangular.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-113">hello following samples are for Azure SQL and Azure Blob but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="1bfbd-114">Ajustar el conjunto de datos y las definiciones de servicio vinculado en ejemplos toopoint toodata en origen de datos correspondiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-114">Adjust dataset and linked service definitions in examples toopoint toodata in hello relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a><span data-ttu-id="1bfbd-115">Ejemplo 1: asignación de blob de Azure SQL tooAzure de columna</span><span class="sxs-lookup"><span data-stu-id="1bfbd-115">Sample 1 – column mapping from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="1bfbd-116">En este ejemplo, tabla de entrada de hello tiene una estructura y señala tooa table de SQL en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-116">In this sample, hello input table has a structure and it points tooa SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="1bfbd-117">En este ejemplo, tabla de salida de hello tiene una estructura y señala tooa blob en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-117">In this sample, hello output table has a structure and it points tooa blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="1bfbd-118">Hola después JSON define una actividad de copia de una canalización.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-118">hello following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="1bfbd-119">las columnas de Hola de origen asignan toocolumns en el receptor (**columnMappings**) mediante el uso de hello **traductor** propiedad.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-119">hello columns from source mapped toocolumns in sink (**columnMappings**) by using hello **Translator** property.</span></span>

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
<span data-ttu-id="1bfbd-120">**Flujo de asignación de columnas:**</span><span class="sxs-lookup"><span data-stu-id="1bfbd-120">**Column mapping flow:**</span></span>

![Flujo de asignación de columnas](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a><span data-ttu-id="1bfbd-122">Ejemplo 2: columna asignación con la consulta SQL desde blob tooAzure de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1bfbd-122">Sample 2 – column mapping with SQL query from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="1bfbd-123">En este ejemplo, una consulta SQL es tooextract usa datos de SQL Azure en lugar de especificar simplemente el nombre de la tabla de Hola y nombres de columna de hello en la sección "estructura".</span><span class="sxs-lookup"><span data-stu-id="1bfbd-123">In this sample, a SQL query is used tooextract data from Azure SQL instead of simply specifying hello table name and hello column names in “structure” section.</span></span> 

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
<span data-ttu-id="1bfbd-124">En este caso, resultados de la consulta de hello son primera toocolumns asignada especificada en "estructura" de origen.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-124">In this case, hello query results are first mapped toocolumns specified in “structure” of source.</span></span> <span data-ttu-id="1bfbd-125">A continuación, las columnas de Hola de origen "estructura" son toocolumns asignada en el receptor "estructura" con las reglas especificadas en columnMappings.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-125">Next, hello columns from source “structure” are mapped toocolumns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="1bfbd-126">Supongamos que la consulta de hello devuelve 5 columnas, dos columnas más de las especificadas en hello "estructura" de origen.</span><span class="sxs-lookup"><span data-stu-id="1bfbd-126">Suppose hello query returns 5 columns, two more columns than those specified in hello “structure” of source.</span></span>

<span data-ttu-id="1bfbd-127">**Flujo de asignación de columnas**</span><span class="sxs-lookup"><span data-stu-id="1bfbd-127">**Column mapping flow**</span></span>

![Flujo de asignación de columnas 2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="1bfbd-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1bfbd-129">Next steps</span></span>
<span data-ttu-id="1bfbd-130">Vea el artículo de Hola para obtener un tutorial sobre el uso de la actividad de copia:</span><span class="sxs-lookup"><span data-stu-id="1bfbd-130">See hello article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="1bfbd-131">Copiar los datos de almacenamiento de blobs tooSQL base de datos</span><span class="sxs-lookup"><span data-stu-id="1bfbd-131">Copy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
