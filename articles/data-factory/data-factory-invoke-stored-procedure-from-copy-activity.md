---
title: "Invocación del procedimiento almacenado desde la actividad de copia de Azure Data Factory | Microsoft Docs"
description: "Obtenga información sobre cómo invocar un procedimiento almacenado en Azure SQL Database o SQL Server desde una actividad de copia de Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: af6e4a57e726598c266ee766656aa2cc22e374e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="f2e3d-103">Invocación del procedimiento almacenado desde la actividad de copia en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f2e3d-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="f2e3d-104">Cuando se copian datos en [SQL Server](data-factory-sqlserver-connector.md) o [Azure SQL Database](data-factory-azure-sql-connector.md), puede configurar **SqlSink** en la actividad de copia para invocar un procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span></span> <span data-ttu-id="f2e3d-105">Es posible que desee usar el procedimiento almacenado para realizar cualquier procesamiento adicional (combinar columnas, buscar valores, inserciones en varias tablas, etc.) necesario antes de insertar datos en la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span></span> <span data-ttu-id="f2e3d-106">Esta característica aprovecha los [parámetros con valores de tabla](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2e3d-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="f2e3d-107">En el ejemplo siguiente se muestra cómo invocar un procedimiento almacenado en una base de datos SQL Server desde una canalización de Data Factory (actividad de copia):</span><span class="sxs-lookup"><span data-stu-id="f2e3d-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="f2e3d-108">JSON de conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="f2e3d-108">Output dataset JSON</span></span>
<span data-ttu-id="f2e3d-109">En el JSON de conjunto de datos de salida, establezca el **tipo** en **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="f2e3d-110">Establézcalo en **AzureSqlTable** para usarlo con una base de datos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span></span> <span data-ttu-id="f2e3d-111">El valor de la propiedad **tableName** debe coincidir con el nombre del primer parámetro del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span></span>  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="f2e3d-112">Sección SqlSink del JSON de actividad de copia</span><span class="sxs-lookup"><span data-stu-id="f2e3d-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="f2e3d-113">Defina la sección **SqlSink** en el JSON de actividad de copia como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-113">Define the **SqlSink** section in the copy activity JSON as follows.</span></span> <span data-ttu-id="f2e3d-114">Para invocar un procedimiento almacenado mientras se insertan datos en la base de datos de receptor/destino, especifique los valores de las propiedades **SqlWriterStoredProcedureName** y **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="f2e3d-115">Para las descripciones de estas propiedades, consulte la [sección SqlSink del artículo sobre el conector de SQL Server](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="f2e3d-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a><span data-ttu-id="f2e3d-116">Definición del procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="f2e3d-116">Stored procedure definition</span></span> 
<span data-ttu-id="f2e3d-117">En la base de datos, defina el procedimiento almacenado con el mismo nombre que **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="f2e3d-118">El procedimiento almacenado controla los datos de entrada desde el almacén de datos de origen e inserta datos en una tabla en la base de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span></span> <span data-ttu-id="f2e3d-119">El nombre del primer parámetro del procedimiento almacenado debe coincidir con el valor tableName definido en el JSON de base de datos (marketing).</span><span class="sxs-lookup"><span data-stu-id="f2e3d-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="f2e3d-120">Definición de tipo de tabla</span><span class="sxs-lookup"><span data-stu-id="f2e3d-120">Table type definition</span></span>
<span data-ttu-id="f2e3d-121">En la base de datos, defina el tipo de tabla con el mismo nombre como **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="f2e3d-122">El esquema del tipo de tabla debe coincidir con el esquema del conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-122">The schema of the table type must match the schema of the input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="f2e3d-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f2e3d-123">Next steps</span></span>
<span data-ttu-id="f2e3d-124">Revise los siguientes artículos de conectores para ver ejemplos completos de JSON:</span><span class="sxs-lookup"><span data-stu-id="f2e3d-124">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="f2e3d-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f2e3d-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="f2e3d-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="f2e3d-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
