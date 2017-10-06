---
title: "aaaInvoke el procedimiento almacenado de actividad de copia de factoría de datos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de la actividad de copia de tooinvoke un procedimiento almacenado en la base de datos de SQL Azure o SQL Server desde una factoría de datos de Azure."
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="9a68d-103">Invocación del procedimiento almacenado desde la actividad de copia en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9a68d-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="9a68d-104">Cuando se copian datos en [SQL Server](data-factory-sqlserver-connector.md) o [base de datos de SQL Azure](data-factory-azure-sql-connector.md), puede configurar hello **SqlSink** en tooinvoke de actividad de copia un procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="9a68d-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure.</span></span> <span data-ttu-id="9a68d-105">Puede que desee toouse Hola almacenado procedimiento tooperform es necesario ningún procesamiento adicional (combinar columnas, buscar valores, la inserción en varias tablas, etc.) antes de insertar datos en la tabla de destino de toohello.</span><span class="sxs-lookup"><span data-stu-id="9a68d-105">You may want toouse hello stored procedure tooperform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in toohello destination table.</span></span> <span data-ttu-id="9a68d-106">Esta característica aprovecha los [parámetros con valores de tabla](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="9a68d-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="9a68d-107">Hola siguiente ejemplo muestra cómo tooinvoke un procedimiento almacenado en un servidor SQL Server de base de datos de una canalización de factoría de datos (actividad de copia):</span><span class="sxs-lookup"><span data-stu-id="9a68d-107">hello following sample shows how tooinvoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="9a68d-108">JSON de conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="9a68d-108">Output dataset JSON</span></span>
<span data-ttu-id="9a68d-109">En el conjunto de datos de salida de hello JSON, establezca hello **tipo** a: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="9a68d-109">In hello output dataset JSON, set hello **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="9a68d-110">Establézcalo demasiado**AzureSqlTable** toouse con una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9a68d-110">Set it too**AzureSqlTable** toouse with an Azure SQL database.</span></span> <span data-ttu-id="9a68d-111">Hola valor para **tableName** propiedad debe coincidir con el nombre de hello del primer parámetro del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a68d-111">hello value for **tableName** property must match hello name of first parameter of hello stored procedure.</span></span>  

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

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="9a68d-112">Sección SqlSink del JSON de actividad de copia</span><span class="sxs-lookup"><span data-stu-id="9a68d-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="9a68d-113">Definir hello **SqlSink** sección JSON de la actividad de copia hello como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="9a68d-113">Define hello **SqlSink** section in hello copy activity JSON as follows.</span></span> <span data-ttu-id="9a68d-114">tooinvoke un procedimiento almacenado al insertar datos en la base de datos de receptor o el destino de hello, especifica los valores de **SqlWriterStoredProcedureName** y **SqlWriterTableType** propiedades.</span><span class="sxs-lookup"><span data-stu-id="9a68d-114">tooinvoke a stored procedure while inserting data into hello sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="9a68d-115">Para obtener descripciones de estas propiedades, vea [SqlSink sección en el artículo de conector de SQL Server de hello](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="9a68d-115">For descriptions of these properties, see [SqlSink section in hello SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

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

## <a name="stored-procedure-definition"></a><span data-ttu-id="9a68d-116">Definición del procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="9a68d-116">Stored procedure definition</span></span> 
<span data-ttu-id="9a68d-117">En la base de datos, definir el procedimiento de hello almacenado con hello mismo nombre como **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="9a68d-117">In your database, define hello stored procedure with hello same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="9a68d-118">procedimiento almacenado de Hello administra los datos de entrada de almacén de datos de origen de Hola e inserta datos en una tabla de base de datos de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a68d-118">hello stored procedure handles input data from hello source data store, and inserts data into a table in hello destination database.</span></span> <span data-ttu-id="9a68d-119">nombre de Hello del primer parámetro del procedimiento almacenado de hello debe coincidir con tableName Hola definido en el conjunto de datos de hello JSON (Marketing).</span><span class="sxs-lookup"><span data-stu-id="9a68d-119">hello name of hello first parameter of stored procedure must match hello tableName defined in hello dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="9a68d-120">Definición de tipo de tabla</span><span class="sxs-lookup"><span data-stu-id="9a68d-120">Table type definition</span></span>
<span data-ttu-id="9a68d-121">En la base de datos, definir el tipo de tabla de hello con hello mismo nombre como **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="9a68d-121">In your database, define hello table type with hello same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="9a68d-122">esquema de Hola Hola del tipo de tabla debe coincide Hola del conjunto de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a68d-122">hello schema of hello table type must match hello schema of hello input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="9a68d-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a68d-123">Next steps</span></span>
<span data-ttu-id="9a68d-124">Revisar los siguientes artículos de conector que para JSON ejemplos completos de Hola:</span><span class="sxs-lookup"><span data-stu-id="9a68d-124">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="9a68d-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9a68d-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="9a68d-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9a68d-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
