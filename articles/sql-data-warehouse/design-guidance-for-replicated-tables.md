---
title: "Guía de aaaDesign para replica tablas - almacenamiento de datos de SQL Azure | Documentos de Microsoft"
description: "Recomendaciones para el diseño de tablas replicadas en el esquema de Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="9f42d-103">Instrucciones de diseño para el uso de tablas replicadas en Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9f42d-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="9f42d-104">En este artículo se proporcionan recomendaciones para el diseño de tablas replicadas en el esquema de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9f42d-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="9f42d-105">Utilice estas recomendaciones tooimprove consulta las del rendimiento al reducir la complejidad de movimiento y la consulta de datos.</span><span class="sxs-lookup"><span data-stu-id="9f42d-105">Use these recommendations tooimprove query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="9f42d-106">característica de tabla replicada Hola está actualmente en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="9f42d-106">hello replicated table feature is currently in public preview.</span></span> <span data-ttu-id="9f42d-107">Algunos comportamientos son toochange de asunto.</span><span class="sxs-lookup"><span data-stu-id="9f42d-107">Some behaviors are subject toochange.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="9f42d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9f42d-108">Prerequisites</span></span>
<span data-ttu-id="9f42d-109">En este artículo se da por supuesto que está familiarizado con los conceptos de distribución y movimiento de datos en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9f42d-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="9f42d-110">Para más información, vea [Datos distribuidos](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="9f42d-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="9f42d-111">Como parte del diseño de tabla, comprender tanto como sea posible sobre los datos y cómo se consultan datos Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-111">As part of table design, understand as much as possible about your data and how hello data is queried.</span></span>  <span data-ttu-id="9f42d-112">Por ejemplo, considere estas preguntas:</span><span class="sxs-lookup"><span data-stu-id="9f42d-112">For example, consider these questions:</span></span>

- <span data-ttu-id="9f42d-113">¿Qué tamaño tiene tabla Hola?</span><span class="sxs-lookup"><span data-stu-id="9f42d-113">How large is hello table?</span></span>   
- <span data-ttu-id="9f42d-114">¿Con qué frecuencia se actualiza la tabla de hello?</span><span class="sxs-lookup"><span data-stu-id="9f42d-114">How often is hello table refreshed?</span></span>   
- <span data-ttu-id="9f42d-115">¿Tiene tablas de hechos y dimensiones en un almacenamiento de datos?</span><span class="sxs-lookup"><span data-stu-id="9f42d-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="9f42d-116">¿Qué es una tabla replicada?</span><span class="sxs-lookup"><span data-stu-id="9f42d-116">What is a replicated table?</span></span>
<span data-ttu-id="9f42d-117">Una tabla replicada tiene una copia completa de la tabla de hello accesible en cada nodo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f42d-117">A replicated table has a full copy of hello table accessible on each Compute node.</span></span> <span data-ttu-id="9f42d-118">Replicación de una tabla quita los datos de tootransfer de necesidad de hello entre los nodos de proceso antes de una combinación o una agregación.</span><span class="sxs-lookup"><span data-stu-id="9f42d-118">Replicating a table removes hello need tootransfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="9f42d-119">Puesto que la tabla de hello tiene varias copias, las tablas replicadas funcionan mejor cuando el tamaño de la tabla de hello es inferior a 2 GB comprimido.</span><span class="sxs-lookup"><span data-stu-id="9f42d-119">Since hello table has multiple copies, replicated tables work best when hello table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="9f42d-120">Hello siguiente diagrama muestra una tabla replicada que sea accesible en cada nodo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f42d-120">hello following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="9f42d-121">En el almacén de datos de SQL, tabla replicada hello es tooa copiado totalmente la base de datos de distribución en cada nodo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f42d-121">In SQL Data Warehouse, hello replicated table is fully copied tooa distribution database on each Compute node.</span></span> 

<span data-ttu-id="9f42d-122">![Tabla replicada](media/guidance-for-using-replicated-tables/replicated-table.png "Tabla replicada")</span><span class="sxs-lookup"><span data-stu-id="9f42d-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="9f42d-123">Las tablas replicadas funcionan correctamente para tablas de dimensiones pequeñas de un esquema de estrella.</span><span class="sxs-lookup"><span data-stu-id="9f42d-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="9f42d-124">Tablas de dimensiones suelen ser de un tamaño que hace más factible toostore y mantienen varias copias.</span><span class="sxs-lookup"><span data-stu-id="9f42d-124">Dimension tables are usually of a size that makes it feasible toostore and maintain multiple copies.</span></span> <span data-ttu-id="9f42d-125">Las dimensiones almacenan datos descriptivos que cambian lentamente, como el nombre y la dirección del cliente, y detalles del producto.</span><span class="sxs-lookup"><span data-stu-id="9f42d-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="9f42d-126">Hola de variación lenta la naturaleza de los datos de hello conduce toofewer vuelve a generar de tabla replicada Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-126">hello slowly changing nature of hello data leads toofewer rebuilds of hello replicated table.</span></span> 

<span data-ttu-id="9f42d-127">Considere la posibilidad de usar una tabla replicada cuando:</span><span class="sxs-lookup"><span data-stu-id="9f42d-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="9f42d-128">tamaño de la tabla de Hello en el disco es inferior a 2 GB, independientemente del número de Hola de filas.</span><span class="sxs-lookup"><span data-stu-id="9f42d-128">hello table size on disk is less than 2 GB, regardless of hello number of rows.</span></span> <span data-ttu-id="9f42d-129">tamaño de hello toofind de una tabla, puede usar hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) comando: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="9f42d-129">toofind hello size of a table, you can use hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="9f42d-130">tabla de Hola se utiliza en las combinaciones que en caso contrario requerirían el movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="9f42d-130">hello table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="9f42d-131">Por ejemplo, una combinación en las tablas hash distribuida requiere el movimiento de datos cuando las columnas de combinación de hello no son Hola misma columna de distribución.</span><span class="sxs-lookup"><span data-stu-id="9f42d-131">For example, a join on hash-distributed tables requires data movement when hello joining columns are not hello same distribution column.</span></span> <span data-ttu-id="9f42d-132">Si una de las tablas hash está distribuido de Hola es pequeña, considere la posibilidad de una tabla replicada.</span><span class="sxs-lookup"><span data-stu-id="9f42d-132">If one of hello hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="9f42d-133">Una combinación en una tabla Round Robin requiere movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="9f42d-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="9f42d-134">Se recomienda usar tablas replicadas en lugar de tablas Round Robin en la mayoría de los casos.</span><span class="sxs-lookup"><span data-stu-id="9f42d-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="9f42d-135">Considere la posibilidad de convertir una existente distribuidas tooa tabla replicada tabla cuando:</span><span class="sxs-lookup"><span data-stu-id="9f42d-135">Consider converting an existing distributed table tooa replicated table when:</span></span>

- <span data-ttu-id="9f42d-136">Operaciones de movimiento de datos de uso que difunden nodos de proceso de hello datos tooall Hola los planes de consulta.</span><span class="sxs-lookup"><span data-stu-id="9f42d-136">Query plans use data movement operations that broadcast hello data tooall hello Compute nodes.</span></span> <span data-ttu-id="9f42d-137">Hola BroadcastMoveOperation es caro y reduce el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="9f42d-137">hello BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="9f42d-138">tooview las operaciones de movimiento de datos en los planes de consulta, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="9f42d-138">tooview data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="9f42d-139">Las tablas replicadas no pueden obtener el mejor rendimiento de consultas hello cuando:</span><span class="sxs-lookup"><span data-stu-id="9f42d-139">Replicated tables may not yield hello best query performance when:</span></span>

- <span data-ttu-id="9f42d-140">tabla de Hello tiene frecuentes de inserción, actualización y eliminación de las operaciones.</span><span class="sxs-lookup"><span data-stu-id="9f42d-140">hello table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="9f42d-141">Estas operaciones de DML (lenguaje) de manipulación de datos requieren una recompilación de la tabla de hello replicado.</span><span class="sxs-lookup"><span data-stu-id="9f42d-141">These data manipulation language (DML) operations require a rebuild of hello replicated table.</span></span> <span data-ttu-id="9f42d-142">La recompilación puede provocar con frecuencia un rendimiento más lento.</span><span class="sxs-lookup"><span data-stu-id="9f42d-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="9f42d-143">almacenamiento de datos de Hola se escala con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="9f42d-143">hello data warehouse is scaled frequently.</span></span> <span data-ttu-id="9f42d-144">Ajuste de escala en un almacén de datos cambia el número de Hola de nodos de cálculo, que implica una recompilación.</span><span class="sxs-lookup"><span data-stu-id="9f42d-144">Scaling a data warehouse changes hello number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="9f42d-145">tabla de Hello tiene un gran número de columnas, pero las operaciones de datos normalmente tienen acceso a solo un número pequeño de columnas.</span><span class="sxs-lookup"><span data-stu-id="9f42d-145">hello table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="9f42d-146">En este escenario, en lugar de replicar Hola toda la tabla, puede que sea más eficaz toohash distribuir tabla hello y, a continuación, crear un índice en columnas de hello accede con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="9f42d-146">In this scenario, instead of replicating hello entire table, it might be more effective toohash distribute hello table, and then create an index on hello frequently accessed columns.</span></span> <span data-ttu-id="9f42d-147">Si una consulta requiere el movimiento de datos, almacenamiento de datos de SQL solo mueve los datos en hello solicitan columnas.</span><span class="sxs-lookup"><span data-stu-id="9f42d-147">When a query requires data movement, SQL Data Warehouse only moves data in hello requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="9f42d-148">Usar tablas replicadas con predicados de consulta simples</span><span class="sxs-lookup"><span data-stu-id="9f42d-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="9f42d-149">Antes de elegir toodistribute o duplica una tabla, piense en tipos de Hola de consultas que tiene previsto toorun contra la tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-149">Before you choose toodistribute or replicate a table, think about hello types of queries you plan toorun against hello table.</span></span> <span data-ttu-id="9f42d-150">Siempre que sea posible,</span><span class="sxs-lookup"><span data-stu-id="9f42d-150">Whenever possible,</span></span>

- <span data-ttu-id="9f42d-151">Use tablas replicadas para consultas con predicados de consulta simples, como los de igualdad o desigualdad.</span><span class="sxs-lookup"><span data-stu-id="9f42d-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="9f42d-152">Use tablas replicadas para consultas con predicados de consulta complejos, como los de LIKE o NOT LIKE.</span><span class="sxs-lookup"><span data-stu-id="9f42d-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="9f42d-153">Las consultas que consumen más CPU demostrar un mejor cuándo se distribuye el trabajo de hello en todos los nodos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-153">CPU-intensive queries perform best when hello work is distributed across all of hello Compute nodes.</span></span> <span data-ttu-id="9f42d-154">Por ejemplo, las consultas que ejecutan cálculos en todas las filas de una tabla funcionan mejor en tablas distribuidas que en tablas replicadas.</span><span class="sxs-lookup"><span data-stu-id="9f42d-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="9f42d-155">Puesto que una tabla replicada se almacena por completo en cada nodo de proceso, una consulta de la CPU en una tabla replicada se ejecuta en toda la tabla hello en cada nodo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f42d-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against hello entire table on every Compute node.</span></span> <span data-ttu-id="9f42d-156">Hello cálculo adicional puede ralentizar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="9f42d-156">hello extra computation can slow query performance.</span></span>

<span data-ttu-id="9f42d-157">Por ejemplo, esta consulta tiene un predicado complejo.</span><span class="sxs-lookup"><span data-stu-id="9f42d-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="9f42d-158">Se ejecuta con mayor rapidez cuando el proveedor está una tabla distribuida en lugar de una tabla replicada.</span><span class="sxs-lookup"><span data-stu-id="9f42d-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="9f42d-159">En este ejemplo, el proveedor se puede distribuir por hash o mediante el método Round Robin.</span><span class="sxs-lookup"><span data-stu-id="9f42d-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a><span data-ttu-id="9f42d-160">Convertir tablas de tooreplicated round robin tablas existentes</span><span class="sxs-lookup"><span data-stu-id="9f42d-160">Convert existing round-robin tables tooreplicated tables</span></span>
<span data-ttu-id="9f42d-161">Si ya tiene tablas round robin, se recomienda convertirlas tooreplicated tablas si cumplen con los criterios que se describen en este artículo.</span><span class="sxs-lookup"><span data-stu-id="9f42d-161">If you already have round-robin tables, we recommend converting them tooreplicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="9f42d-162">Las tablas replicadas mejoran el rendimiento en tablas de round-robin porque eliminan la necesidad de hello para el movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="9f42d-162">Replicated tables improve performance over round-robin tables because they eliminate hello need for data movement.</span></span>  <span data-ttu-id="9f42d-163">Una tabla Round Robin siempre requiere movimiento de datos para las combinaciones.</span><span class="sxs-lookup"><span data-stu-id="9f42d-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="9f42d-164">Este ejemplo se utiliza [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory tabla tooa tabla replicada.</span><span class="sxs-lookup"><span data-stu-id="9f42d-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa replicated table.</span></span> <span data-ttu-id="9f42d-165">Este ejemplo funciona independientemente de si DimSalesTerritory se distribuye por hash o Round Robin.</span><span class="sxs-lookup"><span data-stu-id="9f42d-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="9f42d-166">Ejemplo de rendimiento de consultas para tablas Round Robin frente a tablas replicadas</span><span class="sxs-lookup"><span data-stu-id="9f42d-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="9f42d-167">Una tabla replicada no requiere ningún movimiento de datos para las combinaciones porque toda la tabla Hola ya está presente en cada nodo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f42d-167">A replicated table does not require any data movement for joins because hello entire table is already present on each Compute node.</span></span> <span data-ttu-id="9f42d-168">Si las tablas de dimensiones Hola son round-robin distribuida, una combinación copia tabla de dimensiones de hello en el nodo de proceso de tooeach completa.</span><span class="sxs-lookup"><span data-stu-id="9f42d-168">If hello dimension tables are round-robin distributed, a join copies hello dimension table in full tooeach Compute node.</span></span> <span data-ttu-id="9f42d-169">datos de hello toomove, plan de consulta de hello contiene una operación llamada BroadcastMoveOperation.</span><span class="sxs-lookup"><span data-stu-id="9f42d-169">toomove hello data, hello query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="9f42d-170">Este tipo de operación de movimiento de datos reduce el rendimiento de las consultas y se elimina mediante el uso de tablas replicadas.</span><span class="sxs-lookup"><span data-stu-id="9f42d-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="9f42d-171">pasos del plan de consulta de tooview, usar hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) vista de catálogo del sistema.</span><span class="sxs-lookup"><span data-stu-id="9f42d-171">tooview query plan steps, use hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="9f42d-172">Por ejemplo, en la siguiente consulta en el esquema de AdventureWorks de hello, Hola ` FactInternetSales` tabla es distribuidas de hash.</span><span class="sxs-lookup"><span data-stu-id="9f42d-172">For example, in following query against hello AdventureWorks schema, hello ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="9f42d-173">Hola `DimDate` y `DimSalesTerritory` tablas son tablas de dimensión más pequeñas.</span><span class="sxs-lookup"><span data-stu-id="9f42d-173">hello `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="9f42d-174">Esta consulta devuelve las ventas totales de hello en América del Norte para el año fiscal 2004:</span><span class="sxs-lookup"><span data-stu-id="9f42d-174">This query returns hello total sales in North America for fiscal year 2004:</span></span>
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
<span data-ttu-id="9f42d-175">Se vuelve a crear `DimDate` y `DimSalesTerritory` como tablas Round Robin.</span><span class="sxs-lookup"><span data-stu-id="9f42d-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="9f42d-176">Como resultado, consulta Hola mostró Hola siguiendo el plan de consulta, que tiene varios difusión mover operaciones:</span><span class="sxs-lookup"><span data-stu-id="9f42d-176">As a result, hello query showed hello following query plan, which has multiple broadcast move operations:</span></span> 
 
![Plan de consulta de round robin](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="9f42d-178">Se vuelve a crear `DimDate` y `DimSalesTerritory` como tablas replicadas y se ejecutó consulta Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="9f42d-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran hello query again.</span></span> <span data-ttu-id="9f42d-179">plan de consulta resultante de Hello es mucho más corta y no haya ninguno emita se mueve.</span><span class="sxs-lookup"><span data-stu-id="9f42d-179">hello resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Plan de consulta replicado](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="9f42d-181">Consideraciones de rendimiento para modificar tablas replicadas</span><span class="sxs-lookup"><span data-stu-id="9f42d-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="9f42d-182">Almacenamiento de datos de SQL se implementa una tabla replicada manteniendo una versión principal de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-182">SQL Data Warehouse implements a replicated table by maintaining a master version of hello table.</span></span> <span data-ttu-id="9f42d-183">Copia Hola de base de datos de distribución de tooone versión maestra en cada nodo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f42d-183">It copies hello master version tooone distribution database on each Compute node.</span></span> <span data-ttu-id="9f42d-184">Cuando se produce un cambio, almacenamiento de datos de SQL actualiza primero la tabla maestra de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-184">When there is a change, SQL Data Warehouse first updates hello master table.</span></span> <span data-ttu-id="9f42d-185">Requiere una recompilación de las tablas de hello en cada nodo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9f42d-185">Then it requires a rebuild of hello tables on each Compute node.</span></span> <span data-ttu-id="9f42d-186">Una recompilación de una tabla replicada incluye copiar Hola tabla tooeach de nodos de proceso y, a continuación, volver a generar índices Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-186">A rebuild of a replicated table includes copying hello table tooeach Compute node and then rebuilding hello indexes.</span></span>

<span data-ttu-id="9f42d-187">Las recompilaciones son necesarias después de que:</span><span class="sxs-lookup"><span data-stu-id="9f42d-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="9f42d-188">Se carguen o modifiquen datos.</span><span class="sxs-lookup"><span data-stu-id="9f42d-188">Data is loaded or modified</span></span>
- <span data-ttu-id="9f42d-189">almacén de datos de Hello es configuración diferente de la unidad de escala tooa</span><span class="sxs-lookup"><span data-stu-id="9f42d-189">hello data warehouse is scaled tooa different DWU setting</span></span>
- <span data-ttu-id="9f42d-190">Se actualice la definición de tabla</span><span class="sxs-lookup"><span data-stu-id="9f42d-190">Table definition is updated</span></span>

<span data-ttu-id="9f42d-191">Las recompilaciones no son necesarias después de que:</span><span class="sxs-lookup"><span data-stu-id="9f42d-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="9f42d-192">Se pause la operación.</span><span class="sxs-lookup"><span data-stu-id="9f42d-192">Pause operation</span></span>
- <span data-ttu-id="9f42d-193">Se reanude la operación.</span><span class="sxs-lookup"><span data-stu-id="9f42d-193">Resume operation</span></span>

<span data-ttu-id="9f42d-194">Hola regeneración no se produce inmediatamente después de que se modifican los datos.</span><span class="sxs-lookup"><span data-stu-id="9f42d-194">hello rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="9f42d-195">En su lugar, se desencadena la regeneración de Hola Hola la primera vez que selecciona una consulta de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-195">Instead, hello rebuild is triggered hello first time a query selects from hello table.</span></span>  <span data-ttu-id="9f42d-196">Dentro de la instrucción select inicial de Hola de tabla de Hola son tabla replicada de pasos toorebuild Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-196">Within hello initial select statement from hello table are steps toorebuild hello replicated table.</span></span>  <span data-ttu-id="9f42d-197">Puesto Hola regeneración se realiza dentro de la consulta de hello, instrucción select de la inicial de toohello Hola impacto podría ser significativa en función del tamaño de Hola de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-197">Because hello rebuild is done within hello query, hello impact toohello initial select statement could be significant depending on hello size of hello table.</span></span>  <span data-ttu-id="9f42d-198">Si varias tablas replicadas intervienen que necesitan una recompilación, cada copia se vuelven a generar en serie como pasos dentro de la instrucción de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within hello statement.</span></span>  <span data-ttu-id="9f42d-199">coherencia de los datos toomaintain durante la regeneración de Hola de hello replica tabla que se toma un bloqueo exclusivo en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-199">toomaintain data consistency during hello rebuild of hello replicated table an exclusive lock is taken on hello table.</span></span>  <span data-ttu-id="9f42d-200">Hola bloqueo impide la tabla de toohello de acceso a todos los dure Hola Hola recompilación.</span><span class="sxs-lookup"><span data-stu-id="9f42d-200">hello lock prevents all access toohello table for hello duration of hello rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="9f42d-201">Usar índices de manera conservadora</span><span class="sxs-lookup"><span data-stu-id="9f42d-201">Use indexes conservatively</span></span>
<span data-ttu-id="9f42d-202">Prácticas recomendadas de indización estándares aplicarán tooreplicated tablas.</span><span class="sxs-lookup"><span data-stu-id="9f42d-202">Standard indexing practices apply tooreplicated tables.</span></span> <span data-ttu-id="9f42d-203">Almacenamiento de datos SQL se vuelve a generar cada índice de tabla replicada como parte de la reconstrucción de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-203">SQL Data Warehouse rebuilds each replicated table index as part of hello rebuild.</span></span> <span data-ttu-id="9f42d-204">Usar solo índices al aumento del rendimiento Hola supera con creces costo Hola de regeneración de índices de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-204">Only use indexes when hello performance gain outweighs hello cost of rebuilding hello indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="9f42d-205">Cargas de datos por lotes</span><span class="sxs-lookup"><span data-stu-id="9f42d-205">Batch data loads</span></span>
<span data-ttu-id="9f42d-206">Al cargar datos en las tablas replicadas, intente toominimize vuelve a generar por lotes cargas juntos.</span><span class="sxs-lookup"><span data-stu-id="9f42d-206">When loading data into replicated tables, try toominimize rebuilds by batching loads together.</span></span> <span data-ttu-id="9f42d-207">Realizar todas las cargas de Hola por lotes antes de ejecutar las instrucciones select.</span><span class="sxs-lookup"><span data-stu-id="9f42d-207">Perform all hello batched loads before running select statements.</span></span>

<span data-ttu-id="9f42d-208">Por ejemplo, en este modelo de carga se cargan datos de cuatro orígenes y se invocan cuatro recompilaciones.</span><span class="sxs-lookup"><span data-stu-id="9f42d-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="9f42d-209">Carga desde el origen 1.</span><span class="sxs-lookup"><span data-stu-id="9f42d-209">Load from source 1.</span></span>
- <span data-ttu-id="9f42d-210">La instrucción de selección desencadena la recompilación 1.</span><span class="sxs-lookup"><span data-stu-id="9f42d-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="9f42d-211">Carga desde el origen 2.</span><span class="sxs-lookup"><span data-stu-id="9f42d-211">Load from source 2.</span></span>
- <span data-ttu-id="9f42d-212">La instrucción de selección desencadena la recompilación 2.</span><span class="sxs-lookup"><span data-stu-id="9f42d-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="9f42d-213">Carga desde el origen 3.</span><span class="sxs-lookup"><span data-stu-id="9f42d-213">Load from source 3.</span></span>
- <span data-ttu-id="9f42d-214">La instrucción de selección desencadena la recompilación 3.</span><span class="sxs-lookup"><span data-stu-id="9f42d-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="9f42d-215">Carga desde el origen 4.</span><span class="sxs-lookup"><span data-stu-id="9f42d-215">Load from source 4.</span></span>
- <span data-ttu-id="9f42d-216">La instrucción de selección desencadena la recompilación 4.</span><span class="sxs-lookup"><span data-stu-id="9f42d-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="9f42d-217">Por ejemplo, en este modelo de carga se cargan datos de cuatro orígenes pero solo se invoca una recompilación.</span><span class="sxs-lookup"><span data-stu-id="9f42d-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="9f42d-218">Carga desde el origen 1.</span><span class="sxs-lookup"><span data-stu-id="9f42d-218">Load from source 1.</span></span>
- <span data-ttu-id="9f42d-219">Carga desde el origen 2.</span><span class="sxs-lookup"><span data-stu-id="9f42d-219">Load from source 2.</span></span>
- <span data-ttu-id="9f42d-220">Carga desde el origen 3.</span><span class="sxs-lookup"><span data-stu-id="9f42d-220">Load from source 3.</span></span>
- <span data-ttu-id="9f42d-221">Carga desde el origen 4.</span><span class="sxs-lookup"><span data-stu-id="9f42d-221">Load from source 4.</span></span>
- <span data-ttu-id="9f42d-222">La instrucción de selección desencadena la recompilación.</span><span class="sxs-lookup"><span data-stu-id="9f42d-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="9f42d-223">Recompilar una tabla replicada después de una carga por lotes</span><span class="sxs-lookup"><span data-stu-id="9f42d-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="9f42d-224">tooensure los tiempos de ejecución de consulta coherentes, se recomienda forzar una actualización de tablas de saludo replican después de una carga por lotes.</span><span class="sxs-lookup"><span data-stu-id="9f42d-224">tooensure consistent query execution times, we recommend forcing a refresh of hello replicated tables after a batch load.</span></span> <span data-ttu-id="9f42d-225">En caso contrario, primera consulta de hello debe esperar Hola tablas toorefresh, que incluye volver a generar índices Hola.</span><span class="sxs-lookup"><span data-stu-id="9f42d-225">Otherwise, hello first query must wait for hello tables toorefresh, which includes rebuilding hello indexes.</span></span> <span data-ttu-id="9f42d-226">Según el tamaño de Hola y el número de tablas replicadas afectados, impacto en el rendimiento Hola puede ser significativa.</span><span class="sxs-lookup"><span data-stu-id="9f42d-226">Depending on hello size and number of replicated tables affected, hello performance impact can be significant.</span></span>  

<span data-ttu-id="9f42d-227">Esta consulta utiliza hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) Hola de toolist DMV replica tablas que se han modificado, pero no vuelve a generar.</span><span class="sxs-lookup"><span data-stu-id="9f42d-227">This query uses hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello replicated tables that have been modified, but not rebuilt.</span></span>

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
<span data-ttu-id="9f42d-228">tooforce una recompilación, ejecute hello sigue instrucción en cada tabla de hello anterior de salida.</span><span class="sxs-lookup"><span data-stu-id="9f42d-228">tooforce a rebuild, run hello following statement on each table in hello preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="9f42d-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f42d-229">Next steps</span></span> 
<span data-ttu-id="9f42d-230">toocreate una tabla replicada, use una de estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="9f42d-230">toocreate a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="9f42d-231">CREATE TABLE (Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="9f42d-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="9f42d-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9f42d-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="9f42d-233">Para obtener información general de las tablas distribuidas, vea [tablas distribuidas](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="9f42d-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



