---
title: "Asignación de columnas de conjunto de datos de Azure Data Factory | Microsoft Docs"
description: "Obtenga información acerca de cómo asignar columnas de origen a columnas de destino."
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
ms.openlocfilehash: a50661b377cfbbff3f1f762342cb275d5da82cea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="map-source-dataset-columns-to-destination-dataset-columns"></a><span data-ttu-id="340c7-103">Asignación de columnas de conjunto de datos de origen a columnas del conjunto de datos de destino</span><span class="sxs-lookup"><span data-stu-id="340c7-103">Map source dataset columns to destination dataset columns</span></span>
<span data-ttu-id="340c7-104">La asignación de columnas puede usarse para especificar cómo se asignan las columnas especificadas en "structure" de la tabla de origen a las columnas especificadas en "structure" de la tabla receptora.</span><span class="sxs-lookup"><span data-stu-id="340c7-104">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span></span> <span data-ttu-id="340c7-105">La propiedad **columnMapping** está disponible en la sección **typeProperties** de la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="340c7-105">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span></span>

<span data-ttu-id="340c7-106">La asignación de columnas admite los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="340c7-106">Column mapping supports the following scenarios:</span></span>

* <span data-ttu-id="340c7-107">Todas las columnas del conjunto de datos "structure" están asignadas a todas las columnas del conjunto de datos receptor "structure".</span><span class="sxs-lookup"><span data-stu-id="340c7-107">All columns in the source dataset structure are mapped to all columns in the sink dataset structure.</span></span>
* <span data-ttu-id="340c7-108">Un subconjunto de columnas del conjunto de datos de origen "structure" está asignado a todas las columnas del conjunto de datos receptor "structure".</span><span class="sxs-lookup"><span data-stu-id="340c7-108">A subset of the columns in the source dataset structure is mapped to all columns in the sink dataset structure.</span></span>

<span data-ttu-id="340c7-109">Las siguientes son las condiciones de error que tienen como resultado una excepción:</span><span class="sxs-lookup"><span data-stu-id="340c7-109">The following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="340c7-110">O bien menos columnas o más columnas en "structure" de la tabla receptora de las que se especifican en la asignación.</span><span class="sxs-lookup"><span data-stu-id="340c7-110">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span></span>
* <span data-ttu-id="340c7-111">Asignación duplicada.</span><span class="sxs-lookup"><span data-stu-id="340c7-111">Duplicate mapping.</span></span>
* <span data-ttu-id="340c7-112">El resultado de la consulta SQL no tiene un nombre de columna que esté especificado en la asignación.</span><span class="sxs-lookup"><span data-stu-id="340c7-112">SQL query result does not have a column name that is specified in the mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="340c7-113">Los ejemplos siguientes son para Azure SQL y Azure Blob, pero resultan aplicables a cualquier almacén de datos que admita conjuntos de datos rectangulares.</span><span class="sxs-lookup"><span data-stu-id="340c7-113">The following samples are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="340c7-114">Ajuste el conjunto de datos y las definiciones de servicios vinculados en los ejemplos para que apunten a datos del origen de datos pertinente.</span><span class="sxs-lookup"><span data-stu-id="340c7-114">Adjust dataset and linked service definitions in examples to point to data in the relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-to-azure-blob"></a><span data-ttu-id="340c7-115">Ejemplo 1: asignación de columnas de SQL Server a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="340c7-115">Sample 1 – column mapping from Azure SQL to Azure blob</span></span>
<span data-ttu-id="340c7-116">En este ejemplo la tabla de entrada tiene una estructura y apunta a una tabla SQL en una base de datos de SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="340c7-116">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="340c7-117">En este ejemplo, la tabla de salida tiene una estructura y apunta a un blob en un almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="340c7-117">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="340c7-118">El siguiente fragmento JSON define una actividad de copia en una canalización.</span><span class="sxs-lookup"><span data-stu-id="340c7-118">The following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="340c7-119">Las columnas del origen se asignan a columnas del receptor (**columnMappings**) usando la propiedad **Translator**.</span><span class="sxs-lookup"><span data-stu-id="340c7-119">The columns from source mapped to columns in sink (**columnMappings**) by using the **Translator** property.</span></span>

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
<span data-ttu-id="340c7-120">**Flujo de asignación de columnas:**</span><span class="sxs-lookup"><span data-stu-id="340c7-120">**Column mapping flow:**</span></span>

![Flujo de asignación de columnas](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-to-azure-blob"></a><span data-ttu-id="340c7-122">Ejemplo 2: asignación de columnas con una consulta SQL de SQL de Azure a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="340c7-122">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span></span>
<span data-ttu-id="340c7-123">En este ejemplo, se usa una consulta SQL para extraer datos de SQL de Azure en lugar de especificar simplemente el nombre de tabla y los nombres de columna en la sección "structure".</span><span class="sxs-lookup"><span data-stu-id="340c7-123">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span></span> 

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
<span data-ttu-id="340c7-124">En este caso, los resultados de consulta se asignan primero a las columnas especificadas en "structure" del origen.</span><span class="sxs-lookup"><span data-stu-id="340c7-124">In this case, the query results are first mapped to columns specified in “structure” of source.</span></span> <span data-ttu-id="340c7-125">A continuación, las columnas dev"structure" de origen se asignan a columnas "structure" de receptor con las reglas especificadas en columnMappings.</span><span class="sxs-lookup"><span data-stu-id="340c7-125">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="340c7-126">Supongamos que la consulta devuelve cinco columnas, dos columnas más que las especificas en el elemento "structure" de origen.</span><span class="sxs-lookup"><span data-stu-id="340c7-126">Suppose the query returns 5 columns, two more columns than those specified in the “structure” of source.</span></span>

<span data-ttu-id="340c7-127">**Flujo de asignación de columnas**</span><span class="sxs-lookup"><span data-stu-id="340c7-127">**Column mapping flow**</span></span>

![Flujo de asignación de columnas 2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="340c7-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="340c7-129">Next steps</span></span>
<span data-ttu-id="340c7-130">Vea el artículo para acceder a un tutorial sobre el uso de la actividad de copia:</span><span class="sxs-lookup"><span data-stu-id="340c7-130">See the article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="340c7-131">Copia de datos de Blob Storage en SQL Database</span><span class="sxs-lookup"><span data-stu-id="340c7-131">Copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)