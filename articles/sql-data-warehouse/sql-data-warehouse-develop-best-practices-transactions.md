---
title: "Optimización de transacciones para SQL Data Warehouse | Microsoft Docs"
description: "Guía de procedimientos recomendados sobre la escritura de actualizaciones de transacciones eficientes en Almacenamiento de datos SQL de Azure"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: f9f19d75a37351b3562ce8c2f3629df14c5437c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="2336f-103">Optimización de transacciones para Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="2336f-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="2336f-104">En este artículo se explica cómo optimizar el rendimiento del código transaccional minimizando al mismo tiempo el riesgo de que se produzcan reversiones extensas.</span><span class="sxs-lookup"><span data-stu-id="2336f-104">This article explains how to optimize the performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="2336f-105">Transacciones y registro</span><span class="sxs-lookup"><span data-stu-id="2336f-105">Transactions and logging</span></span>
<span data-ttu-id="2336f-106">Las transacciones son un componente importante de un motor de base de datos relacional.</span><span class="sxs-lookup"><span data-stu-id="2336f-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="2336f-107">Almacenamiento de datos SQL usa transacciones durante la modificación de los datos.</span><span class="sxs-lookup"><span data-stu-id="2336f-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="2336f-108">Estas transacciones pueden ser explícitas o implícitas.</span><span class="sxs-lookup"><span data-stu-id="2336f-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="2336f-109">Las instrucciones `INSERT`, `UPDATE` y `DELETE` son ejemplos de transacciones implícitas.</span><span class="sxs-lookup"><span data-stu-id="2336f-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="2336f-110">Un desarrollador escribe explícitamente las transacciones explícitas con `BEGIN TRAN`, `COMMIT TRAN` o `ROLLBACK TRAN`; normalmente, estas transacciones se utilizan cuando es necesario vincular varias instrucciones de modificación entre sí en una unidad atómica única.</span><span class="sxs-lookup"><span data-stu-id="2336f-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need to be tied together in a single atomic unit.</span></span> 

<span data-ttu-id="2336f-111">Almacenamiento de datos SQL de Azure confirma los cambios en la base de datos con registros de transacciones.</span><span class="sxs-lookup"><span data-stu-id="2336f-111">Azure SQL Data Warehouse commits changes to the database using transaction logs.</span></span> <span data-ttu-id="2336f-112">Cada distribución tiene su propio registro de transacciones.</span><span class="sxs-lookup"><span data-stu-id="2336f-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="2336f-113">Las escrituras en el registro de transacciones son automáticas.</span><span class="sxs-lookup"><span data-stu-id="2336f-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="2336f-114">No es necesario realizar ninguna configuración.</span><span class="sxs-lookup"><span data-stu-id="2336f-114">There is no configuration required.</span></span> <span data-ttu-id="2336f-115">Sin embargo, si bien este proceso garantiza la escritura, introduce una sobrecarga en el sistema.</span><span class="sxs-lookup"><span data-stu-id="2336f-115">However, whilst this process guarantees the write it does introduce an overhead in the system.</span></span> <span data-ttu-id="2336f-116">Para minimizar este impacto, puede escribir código transaccionalmente eficiente.</span><span class="sxs-lookup"><span data-stu-id="2336f-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="2336f-117">De forma amplia, un código transaccionalmente eficiente pertenece en dos categorías.</span><span class="sxs-lookup"><span data-stu-id="2336f-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="2336f-118">Aproveche las construcciones con registro mínimo, siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="2336f-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="2336f-119">Procese datos con lotes con ámbito para evitar transacciones singulares de larga ejecución.</span><span class="sxs-lookup"><span data-stu-id="2336f-119">Process data using scoped batches to avoid singular long running transactions</span></span>
* <span data-ttu-id="2336f-120">Adopte un modelo de conmutación de particiones para realizar grandes modificaciones en una partición determinada.</span><span class="sxs-lookup"><span data-stu-id="2336f-120">Adopt a partition switching pattern for large modifications to a given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="2336f-121">Registro mínimo frente a registro completo</span><span class="sxs-lookup"><span data-stu-id="2336f-121">Minimal vs. full logging</span></span>
<span data-ttu-id="2336f-122">A diferencia de las operaciones con registro completo, que usan el registro de transacciones para realizar un seguimiento de cada cambio en las filas, las operaciones con registro mínimo solo realizan un seguimiento de las asignaciones de extensión y los cambios en los metadatos.</span><span class="sxs-lookup"><span data-stu-id="2336f-122">Unlike fully logged operations, which use the transaction log to keep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="2336f-123">Por lo tanto, el registro mínimo implica registrar solo la información necesaria para revertir la transacción si se produce un error o una solicitud explícita (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="2336f-123">Therefore, minimal logging involves logging only the information that is required to rollback the transaction in the event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="2336f-124">Puesto que se realiza un seguimiento de mucha menos información en el registro de transacciones, una operación con registro mínimo funciona mejor que una operación con registro completo de tamaño similar.</span><span class="sxs-lookup"><span data-stu-id="2336f-124">As much less information is tracked in the transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="2336f-125">Además, dado que menos escrituras van al registro de transacciones, se genera una cantidad mucho menor de datos de registro y sus operaciones de E/S son más eficientes.</span><span class="sxs-lookup"><span data-stu-id="2336f-125">Furthermore, because fewer writes go the transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="2336f-126">Los límites de seguridad de la transacción solo se aplican a las operaciones de registro completo.</span><span class="sxs-lookup"><span data-stu-id="2336f-126">The transaction safety limits only apply to fully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="2336f-127">Las operaciones con registro mínimo pueden participar en transacciones explícitas.</span><span class="sxs-lookup"><span data-stu-id="2336f-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="2336f-128">Puesto que se realiza el seguimiento de todos los cambios en las estructuras de asignación, es posible revertir las operaciones con registro mínimo.</span><span class="sxs-lookup"><span data-stu-id="2336f-128">As all changes in allocation structures are tracked, it is possible to roll back minimally logged operations.</span></span> <span data-ttu-id="2336f-129">Es importante comprender que el cambio se registra "mínimamente", no se elimina el registro.</span><span class="sxs-lookup"><span data-stu-id="2336f-129">It is important to understand that the change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="2336f-130">Operaciones con registro mínimo</span><span class="sxs-lookup"><span data-stu-id="2336f-130">Minimally logged operations</span></span>
<span data-ttu-id="2336f-131">Las siguientes operaciones admiten el registro mínimo:</span><span class="sxs-lookup"><span data-stu-id="2336f-131">The following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="2336f-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="2336f-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="2336f-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="2336f-133">INSERT..SELECT</span></span>
* <span data-ttu-id="2336f-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="2336f-134">CREATE INDEX</span></span>
* <span data-ttu-id="2336f-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="2336f-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="2336f-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="2336f-136">DROP INDEX</span></span>
* <span data-ttu-id="2336f-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="2336f-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="2336f-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="2336f-138">DROP TABLE</span></span>
* <span data-ttu-id="2336f-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="2336f-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="2336f-140">Las operaciones de movimiento de datos internos (como `BROADCAST` y `SHUFFLE`) no se ven afectados por el límite de seguridad de la transacción.</span><span class="sxs-lookup"><span data-stu-id="2336f-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by the transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="2336f-141">Registro mínimo con carga masiva</span><span class="sxs-lookup"><span data-stu-id="2336f-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="2336f-142">`CTAS` y `INSERT...SELECT` son operaciones de carga masiva.</span><span class="sxs-lookup"><span data-stu-id="2336f-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="2336f-143">Sin embargo, ambas se ven afectadas por la definición de la tabla de destino y dependen del escenario de carga.</span><span class="sxs-lookup"><span data-stu-id="2336f-143">However, both are influenced by the target table definition and depend on the load scenario.</span></span> <span data-ttu-id="2336f-144">A continuación se muestra una tabla que explica si la operación masiva tendrá un registro completo o mínimo:</span><span class="sxs-lookup"><span data-stu-id="2336f-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="2336f-145">Índice principal</span><span class="sxs-lookup"><span data-stu-id="2336f-145">Primary Index</span></span> | <span data-ttu-id="2336f-146">Escenario de carga</span><span class="sxs-lookup"><span data-stu-id="2336f-146">Load Scenario</span></span> | <span data-ttu-id="2336f-147">Modo de registro</span><span class="sxs-lookup"><span data-stu-id="2336f-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2336f-148">Montón</span><span class="sxs-lookup"><span data-stu-id="2336f-148">Heap</span></span> |<span data-ttu-id="2336f-149">Cualquiera</span><span class="sxs-lookup"><span data-stu-id="2336f-149">Any</span></span> |<span data-ttu-id="2336f-150">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="2336f-150">**Minimal**</span></span> |
| <span data-ttu-id="2336f-151">Índice agrupado</span><span class="sxs-lookup"><span data-stu-id="2336f-151">Clustered Index</span></span> |<span data-ttu-id="2336f-152">Tabla de destino vacía</span><span class="sxs-lookup"><span data-stu-id="2336f-152">Empty target table</span></span> |<span data-ttu-id="2336f-153">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="2336f-153">**Minimal**</span></span> |
| <span data-ttu-id="2336f-154">Índice agrupado</span><span class="sxs-lookup"><span data-stu-id="2336f-154">Clustered Index</span></span> |<span data-ttu-id="2336f-155">Las filas cargadas no se superponen a páginas existentes en el destino</span><span class="sxs-lookup"><span data-stu-id="2336f-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="2336f-156">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="2336f-156">**Minimal**</span></span> |
| <span data-ttu-id="2336f-157">Índice agrupado</span><span class="sxs-lookup"><span data-stu-id="2336f-157">Clustered Index</span></span> |<span data-ttu-id="2336f-158">Las filas cargadas se superponen a páginas existentes en el destino</span><span class="sxs-lookup"><span data-stu-id="2336f-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="2336f-159">Completo</span><span class="sxs-lookup"><span data-stu-id="2336f-159">Full</span></span> |
| <span data-ttu-id="2336f-160">Índice de almacén de columnas agrupado</span><span class="sxs-lookup"><span data-stu-id="2336f-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="2336f-161">Tamaño del lote > = 102.400 por cada distribución con particiones alineadas</span><span class="sxs-lookup"><span data-stu-id="2336f-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="2336f-162">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="2336f-162">**Minimal**</span></span> |
| <span data-ttu-id="2336f-163">Índice de almacén de columnas agrupado</span><span class="sxs-lookup"><span data-stu-id="2336f-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="2336f-164">Tamaño del lote < = 102.400 por cada distribución con particiones alineadas</span><span class="sxs-lookup"><span data-stu-id="2336f-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="2336f-165">Completo</span><span class="sxs-lookup"><span data-stu-id="2336f-165">Full</span></span> |

<span data-ttu-id="2336f-166">Conviene tener en cuenta que cualquier escritura para actualizar índices secundarios o no agrupados será siempre una operación con registro completo.</span><span class="sxs-lookup"><span data-stu-id="2336f-166">It is worth noting that any writes to update secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2336f-167">Almacenamiento de datos SQL tiene 60 distribuciones.</span><span class="sxs-lookup"><span data-stu-id="2336f-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="2336f-168">Por lo tanto, suponiendo que todas las filas tengan una distribución uniforme y una sola partición como destino, el lote deberá contener 6.144.000 filas o más para un registro mínimo cuando se escribe en un índice de almacén de columnas agrupado.</span><span class="sxs-lookup"><span data-stu-id="2336f-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need to contain 6,144,000 rows or larger to be minimally logged when writing to a Clustered Columnstore Index.</span></span> <span data-ttu-id="2336f-169">Si la tabla tiene particiones y las filas que se insertan traspasan los límites de las particiones, serán necesarias 6 144 000 filas por límite de partición, lo que supone una distribución de datos uniforme.</span><span class="sxs-lookup"><span data-stu-id="2336f-169">If the table is partitioned and the rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="2336f-170">Cada partición de cada distribución debe superar de forma independiente el umbral de 102.400 filas para que la inserción se registre mínimamente en la distribución.</span><span class="sxs-lookup"><span data-stu-id="2336f-170">Each partition in each distribution must independently exceed the 102,400 row threshold for the insert to be minimally logged into the distribution.</span></span>
> 
> 

<span data-ttu-id="2336f-171">A menudo, la carga de datos en una tabla no vacía con un índice agrupado puede contener una mezcla de filas con registro completo y filas con registro mínimo.</span><span class="sxs-lookup"><span data-stu-id="2336f-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="2336f-172">Un índice agrupado es un árbol equilibrado (árbol B) de las páginas.</span><span class="sxs-lookup"><span data-stu-id="2336f-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="2336f-173">Si la página que se escribe ya contiene filas de otra transacción, estas escrituras se registrarán completamente.</span><span class="sxs-lookup"><span data-stu-id="2336f-173">If the page being written to already contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="2336f-174">Sin embargo, si la página está vacía, la escritura en esa página se registrará mínimamente.</span><span class="sxs-lookup"><span data-stu-id="2336f-174">However, if the page is empty then the write to that page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="2336f-175">Optimización de eliminaciones</span><span class="sxs-lookup"><span data-stu-id="2336f-175">Optimizing deletes</span></span>
<span data-ttu-id="2336f-176">`DELETE` es una operación con registro completo.</span><span class="sxs-lookup"><span data-stu-id="2336f-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="2336f-177">Si necesita eliminar una gran cantidad de datos de una tabla o una partición, suele tener más sentido realizar una instrucción `SELECT` en los datos que desea conservar, que pueden ejecutarse como operación con registro completo.</span><span class="sxs-lookup"><span data-stu-id="2336f-177">If you need to delete a large amount of data in a table or a partition, it often makes more sense to `SELECT` the data you wish to keep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="2336f-178">Para ello, cree una nueva tabla con [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="2336f-178">To accomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="2336f-179">Cuando lo haga, utilice [RENAME][RENAME] para intercambiar la tabla por la que se acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="2336f-179">Once created, use [RENAME][RENAME] to swap out your old table with the newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only the records we want to kep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename the Tables to replace the 
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] TO [FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="2336f-180">Optimización de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="2336f-180">Optimizing updates</span></span>
<span data-ttu-id="2336f-181">`UPDATE` es una operación con registro completo.</span><span class="sxs-lookup"><span data-stu-id="2336f-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="2336f-182">Si necesita actualizar un gran número de filas de una tabla o una partición, suele ser mucho más eficiente utilizar una operación con registro mínimo, como [CTAS][CTAS], para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="2336f-182">If you need to update a large number of rows in a table or a partition it can often be far more efficient to use a minimally logged operation such as [CTAS][CTAS] to do so.</span></span>

<span data-ttu-id="2336f-183">En el ejemplo siguiente, se ha convertido la actualización de una tabla completa en una operación `CTAS` para que sea posible el registro mínimo.</span><span class="sxs-lookup"><span data-stu-id="2336f-183">In the example below a full table update has been converted to a `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="2336f-184">En este caso, estamos agregando retrospectivamente un importe de descuento a las ventas en la tabla:</span><span class="sxs-lookup"><span data-stu-id="2336f-184">In this case we are retrospectively adding a discount amount to the sales in the table:</span></span>

```sql
--Step 01. Create a new table containing the "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename the tables
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] TO [FactInternetSales];

--Step 03. Drop the old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="2336f-185">Volver a crear tablas de gran tamaño puede beneficiarse del uso de las características de administración de cargas de trabajo de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="2336f-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="2336f-186">Para obtener más información, consulte la sección de administración de cargas de trabajo en el artículo sobre [simultaneidad][concurrency].</span><span class="sxs-lookup"><span data-stu-id="2336f-186">For more details please refer to the workload management section in the [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="2336f-187">Optimización con modificación de particiones</span><span class="sxs-lookup"><span data-stu-id="2336f-187">Optimizing with partition switching</span></span>
<span data-ttu-id="2336f-188">Cuando se enfrenta a modificaciones a gran escala dentro de una [partición de tabla][table partition], un patrón de modificación de particiones constituye un buen enfoque.</span><span class="sxs-lookup"><span data-stu-id="2336f-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="2336f-189">Si la modificación de datos es importante y abarca varias particiones, basta con iterar en las particiones para obtener el mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="2336f-189">If the data modification is significant and spans multiple partitions, then simply iterating over the partitions achieves the same result.</span></span>

<span data-ttu-id="2336f-190">Los pasos para realizar una conmutación de particiones son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="2336f-190">The steps to perform a partition switch are as follows:</span></span>

1. <span data-ttu-id="2336f-191">Crear una partición vacía de salida</span><span class="sxs-lookup"><span data-stu-id="2336f-191">Create an empty out partition</span></span>
2. <span data-ttu-id="2336f-192">Realizar la actualización como una operación CTAS</span><span class="sxs-lookup"><span data-stu-id="2336f-192">Perform the 'update' as a CTAS</span></span>
3. <span data-ttu-id="2336f-193">Desactivar los datos existentes en la tabla de salida</span><span class="sxs-lookup"><span data-stu-id="2336f-193">Switch out the existing data to the out table</span></span>
4. <span data-ttu-id="2336f-194">Activar los datos nuevos</span><span class="sxs-lookup"><span data-stu-id="2336f-194">Switch in the new data</span></span>
5. <span data-ttu-id="2336f-195">Limpiar los datos</span><span class="sxs-lookup"><span data-stu-id="2336f-195">Clean up the data</span></span>

<span data-ttu-id="2336f-196">Sin embargo, para ayudar a identificar las particiones que se van a conmutar, primero necesitamos crear un procedimiento auxiliar como el siguiente.</span><span class="sxs-lookup"><span data-stu-id="2336f-196">However, to help identify the partitions to switch we will first need to build a helper procedure such as the one below.</span></span> 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

<span data-ttu-id="2336f-197">Este procedimiento maximiza la reutilización del código y mantiene el ejemplo de modificación de particiones más compacto.</span><span class="sxs-lookup"><span data-stu-id="2336f-197">This procedure maximizes code re-use and keeps the partition switching example more compact.</span></span>

<span data-ttu-id="2336f-198">El código siguiente muestra los cinco pasos mencionados anteriormente para conseguir una rutina de conmutación de particiones completa.</span><span class="sxs-lookup"><span data-stu-id="2336f-198">The code below demonstrates the five steps mentioned above to achieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table to switch out the data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update the data in the select portion of the CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use the helper procedure to identify the partitions
--The source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--The "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--The "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch the partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' TO [dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' TO [dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform the clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="2336f-199">Minimización del registro con lotes pequeños</span><span class="sxs-lookup"><span data-stu-id="2336f-199">Minimize logging with small batches</span></span>
<span data-ttu-id="2336f-200">Para operaciones de modificación de datos de gran tamaño, puede tener sentido dividir la operación en fragmentos o lotes para definir el ámbito de la unidad de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2336f-200">For large data modification operations, it may make sense to divide the operation into chunks or batches to scope the unit of work.</span></span>

<span data-ttu-id="2336f-201">A continuación, se proporciona un ejemplo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2336f-201">A working example is provided below.</span></span> <span data-ttu-id="2336f-202">El tamaño del lote se estableció en un número trivial para resaltar la técnica.</span><span class="sxs-lookup"><span data-stu-id="2336f-202">The batch size has been set to a trivial number to highlight the technique.</span></span> <span data-ttu-id="2336f-203">En realidad, el tamaño del lote sería mucho mayor.</span><span class="sxs-lookup"><span data-stu-id="2336f-203">In reality the batch size would be significantly larger.</span></span> 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="2336f-204">Instrucciones de operaciones de pausa y escalado</span><span class="sxs-lookup"><span data-stu-id="2336f-204">Pause and scaling guidance</span></span>
<span data-ttu-id="2336f-205">Almacenamiento de datos SQL de Azure permite pausar, reanudar y escalar su almacenamiento de datos a petición.</span><span class="sxs-lookup"><span data-stu-id="2336f-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="2336f-206">Al pausar o escalar Almacenamiento de datos SQL es importante entender que las transacciones en curso se terminan inmediatamente, lo que hace que las transacciones abiertas se reviertan.</span><span class="sxs-lookup"><span data-stu-id="2336f-206">When you pause or scale your SQL Data Warehouse it is important to understand that any in-flight transactions are terminated immediately; causing any open transactions to be rolled back.</span></span> <span data-ttu-id="2336f-207">Si la carga de trabajo había emitido una modificación de datos incompleta y de larga ejecución antes de la operación de pausa o escalado, será necesario deshacer este trabajo.</span><span class="sxs-lookup"><span data-stu-id="2336f-207">If your workload had issued a long running and incomplete data modification prior to the pause or scale operation, then this work will need to be undone.</span></span> <span data-ttu-id="2336f-208">Esto puede afectar al tiempo que tarda en pausar completamente la base de datos de Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="2336f-208">This may impact the time it takes to pause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2336f-209">`UPDATE` y `DELETE` son operaciones con registro completo y, por tanto, estas operaciones de deshacer y rehacer pueden tardar bastante más que las operaciones con registro mínimo equivalentes.</span><span class="sxs-lookup"><span data-stu-id="2336f-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="2336f-210">Lo mejor es dejar que las transacciones de modificación de datos en curso se completen antes de pausar o escalar Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="2336f-210">The best scenario is to let in flight data modification transactions complete prior to pausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="2336f-211">Sin embargo, esto no siempre es posible.</span><span class="sxs-lookup"><span data-stu-id="2336f-211">However, this may not always be practical.</span></span> <span data-ttu-id="2336f-212">Para mitigar el riesgo de que se produzca una reversión extensa, considere una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="2336f-212">To mitigate the risk of a long rollback, consider one of the following options:</span></span>

* <span data-ttu-id="2336f-213">Vuelva a escribir las operaciones de ejecución prolongada con [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="2336f-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="2336f-214">Divida la operación en fragmentos, lo que opera en un subconjunto de las filas</span><span class="sxs-lookup"><span data-stu-id="2336f-214">Break the operation down into chunks; operating on a subset of the rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="2336f-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2336f-215">Next steps</span></span>
<span data-ttu-id="2336f-216">Consulte [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] (Transacciones en SQL Data Warehouse) para obtener más información sobre los niveles de aislamiento y los límites transaccionales.</span><span class="sxs-lookup"><span data-stu-id="2336f-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] to learn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="2336f-217">Para obtener información general de otros procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="2336f-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

