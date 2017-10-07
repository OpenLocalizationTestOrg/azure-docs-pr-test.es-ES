---
title: las transacciones de aaaOptimizing de almacenamiento de datos SQL | Documentos de Microsoft
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
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="3f4cb-103">Optimización de transacciones para Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3f4cb-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="3f4cb-104">Este artículo explica cómo toooptimize Hola rendimiento del código transaccional al minimizar el riesgo de reversión largo.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-104">This article explains how toooptimize hello performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="3f4cb-105">Transacciones y registro</span><span class="sxs-lookup"><span data-stu-id="3f4cb-105">Transactions and logging</span></span>
<span data-ttu-id="3f4cb-106">Las transacciones son un componente importante de un motor de base de datos relacional.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="3f4cb-107">Almacenamiento de datos SQL usa transacciones durante la modificación de los datos.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="3f4cb-108">Estas transacciones pueden ser explícitas o implícitas.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="3f4cb-109">Las instrucciones `INSERT`, `UPDATE` y `DELETE` son ejemplos de transacciones implícitas.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="3f4cb-110">Las transacciones explícitas se escriben explícitamente por un desarrollador que utiliza `BEGIN TRAN`, `COMMIT TRAN` o `ROLLBACK TRAN` y se usan normalmente cuando varias instrucciones de modificación necesitan toobe unido entre sí en una unidad atómica única.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need toobe tied together in a single atomic unit.</span></span> 

<span data-ttu-id="3f4cb-111">Almacenamiento de datos de SQL Azure confirma la base de datos de cambios toohello mediante registros de transacciones.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-111">Azure SQL Data Warehouse commits changes toohello database using transaction logs.</span></span> <span data-ttu-id="3f4cb-112">Cada distribución tiene su propio registro de transacciones.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="3f4cb-113">Las escrituras en el registro de transacciones son automáticas.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="3f4cb-114">No es necesario realizar ninguna configuración.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-114">There is no configuration required.</span></span> <span data-ttu-id="3f4cb-115">Sin embargo, mientras que este proceso garantiza la escritura de hello agrega una sobrecarga en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-115">However, whilst this process guarantees hello write it does introduce an overhead in hello system.</span></span> <span data-ttu-id="3f4cb-116">Para minimizar este impacto, puede escribir código transaccionalmente eficiente.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="3f4cb-117">De forma amplia, un código transaccionalmente eficiente pertenece en dos categorías.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="3f4cb-118">Aproveche las construcciones con registro mínimo, siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="3f4cb-119">Procesamiento de datos con ámbito singular de lotes tooavoid transacciones de larga ejecución</span><span class="sxs-lookup"><span data-stu-id="3f4cb-119">Process data using scoped batches tooavoid singular long running transactions</span></span>
* <span data-ttu-id="3f4cb-120">Adoptar un modelo para tooa grandes modificaciones dada la partición de conmutación de particiones</span><span class="sxs-lookup"><span data-stu-id="3f4cb-120">Adopt a partition switching pattern for large modifications tooa given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="3f4cb-121">Registro mínimo frente a registro completo</span><span class="sxs-lookup"><span data-stu-id="3f4cb-121">Minimal vs. full logging</span></span>
<span data-ttu-id="3f4cb-122">A diferencia de las operaciones de registro completo, que usan Hola transacciones registro tookeep realizar un seguimiento de cada cambio en la fila, realizar un seguimiento de las operaciones registradas al mínimo las asignaciones de extensiones y solo los cambios de metadatos.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-122">Unlike fully logged operations, which use hello transaction log tookeep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="3f4cb-123">Por lo tanto, el registro mínimo implica registrar únicamente la información de Hola que sea necesario toorollback Hola transacciones en caso de hello de un error o una solicitud explícita (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="3f4cb-123">Therefore, minimal logging involves logging only hello information that is required toorollback hello transaction in hello event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="3f4cb-124">Como mucho menos se realiza un seguimiento de información de registro de transacciones de hello, una operación registrada al mínimo se comporta mejor que una operación completamente registrada dimensiones similares.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-124">As much less information is tracked in hello transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="3f4cb-125">Además, dado que escribe menos dejan de registro de transacciones de hello, se genera una menor cantidad de datos de registro y por lo que es más i/OS eficaz.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-125">Furthermore, because fewer writes go hello transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="3f4cb-126">límites de seguridad de transacciones de Hello solo aplican operaciones toofully iniciado.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-126">hello transaction safety limits only apply toofully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="3f4cb-127">Las operaciones con registro mínimo pueden participar en transacciones explícitas.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="3f4cb-128">Tal y como se realiza el seguimiento de todos los cambios en las estructuras de asignación, es posible tooroll back mínimamente las operaciones registradas.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-128">As all changes in allocation structures are tracked, it is possible tooroll back minimally logged operations.</span></span> <span data-ttu-id="3f4cb-129">Es importante toounderstand que el cambio de hello es "mínimo" optimizado no se ha iniciado sin.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-129">It is important toounderstand that hello change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="3f4cb-130">Operaciones con registro mínimo</span><span class="sxs-lookup"><span data-stu-id="3f4cb-130">Minimally logged operations</span></span>
<span data-ttu-id="3f4cb-131">Hello operaciones siguientes son capaces de que se va a registrar mínimamente:</span><span class="sxs-lookup"><span data-stu-id="3f4cb-131">hello following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="3f4cb-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="3f4cb-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="3f4cb-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="3f4cb-133">INSERT..SELECT</span></span>
* <span data-ttu-id="3f4cb-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="3f4cb-134">CREATE INDEX</span></span>
* <span data-ttu-id="3f4cb-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="3f4cb-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="3f4cb-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="3f4cb-136">DROP INDEX</span></span>
* <span data-ttu-id="3f4cb-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="3f4cb-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="3f4cb-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="3f4cb-138">DROP TABLE</span></span>
* <span data-ttu-id="3f4cb-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="3f4cb-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="3f4cb-140">Las operaciones de movimiento de datos internos (como `BROADCAST` y `SHUFFLE`) no se ven afectadas por el límite de seguridad de transacciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by hello transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="3f4cb-141">Registro mínimo con carga masiva</span><span class="sxs-lookup"><span data-stu-id="3f4cb-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="3f4cb-142">`CTAS` y `INSERT...SELECT` son operaciones de carga masiva.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="3f4cb-143">Sin embargo, ambas se ven afectadas por la definición de tabla de destino de Hola y dependen de escenario de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-143">However, both are influenced by hello target table definition and depend on hello load scenario.</span></span> <span data-ttu-id="3f4cb-144">A continuación se muestra una tabla que explica si la operación masiva tendrá un registro completo o mínimo:</span><span class="sxs-lookup"><span data-stu-id="3f4cb-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="3f4cb-145">Índice principal</span><span class="sxs-lookup"><span data-stu-id="3f4cb-145">Primary Index</span></span> | <span data-ttu-id="3f4cb-146">Escenario de carga</span><span class="sxs-lookup"><span data-stu-id="3f4cb-146">Load Scenario</span></span> | <span data-ttu-id="3f4cb-147">Modo de registro</span><span class="sxs-lookup"><span data-stu-id="3f4cb-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f4cb-148">Montón</span><span class="sxs-lookup"><span data-stu-id="3f4cb-148">Heap</span></span> |<span data-ttu-id="3f4cb-149">Cualquiera</span><span class="sxs-lookup"><span data-stu-id="3f4cb-149">Any</span></span> |<span data-ttu-id="3f4cb-150">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="3f4cb-150">**Minimal**</span></span> |
| <span data-ttu-id="3f4cb-151">Índice agrupado</span><span class="sxs-lookup"><span data-stu-id="3f4cb-151">Clustered Index</span></span> |<span data-ttu-id="3f4cb-152">Tabla de destino vacía</span><span class="sxs-lookup"><span data-stu-id="3f4cb-152">Empty target table</span></span> |<span data-ttu-id="3f4cb-153">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="3f4cb-153">**Minimal**</span></span> |
| <span data-ttu-id="3f4cb-154">Índice agrupado</span><span class="sxs-lookup"><span data-stu-id="3f4cb-154">Clustered Index</span></span> |<span data-ttu-id="3f4cb-155">Las filas cargadas no se superponen a páginas existentes en el destino</span><span class="sxs-lookup"><span data-stu-id="3f4cb-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="3f4cb-156">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="3f4cb-156">**Minimal**</span></span> |
| <span data-ttu-id="3f4cb-157">Índice agrupado</span><span class="sxs-lookup"><span data-stu-id="3f4cb-157">Clustered Index</span></span> |<span data-ttu-id="3f4cb-158">Las filas cargadas se superponen a páginas existentes en el destino</span><span class="sxs-lookup"><span data-stu-id="3f4cb-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="3f4cb-159">Completo</span><span class="sxs-lookup"><span data-stu-id="3f4cb-159">Full</span></span> |
| <span data-ttu-id="3f4cb-160">Índice de almacén de columnas agrupado</span><span class="sxs-lookup"><span data-stu-id="3f4cb-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="3f4cb-161">Tamaño del lote > = 102.400 por cada distribución con particiones alineadas</span><span class="sxs-lookup"><span data-stu-id="3f4cb-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="3f4cb-162">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="3f4cb-162">**Minimal**</span></span> |
| <span data-ttu-id="3f4cb-163">Índice de almacén de columnas agrupado</span><span class="sxs-lookup"><span data-stu-id="3f4cb-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="3f4cb-164">Tamaño del lote < = 102.400 por cada distribución con particiones alineadas</span><span class="sxs-lookup"><span data-stu-id="3f4cb-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="3f4cb-165">Completo</span><span class="sxs-lookup"><span data-stu-id="3f4cb-165">Full</span></span> |

<span data-ttu-id="3f4cb-166">Merece la pena indicar que todas las escrituras tooupdate secundaria o no clúster índices siempre estará totalmente las operaciones registran.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-166">It is worth noting that any writes tooupdate secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f4cb-167">Almacenamiento de datos SQL tiene 60 distribuciones.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="3f4cb-168">Por lo tanto, suponiendo que todas las filas se distribuyen uniformemente y de inicio en una sola partición, el lote deberá toocontain 6,144,000 filas o toobe mayor mínimamente registrados al escribir tooa Clustered Columnstore Index.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need toocontain 6,144,000 rows or larger toobe minimally logged when writing tooa Clustered Columnstore Index.</span></span> <span data-ttu-id="3f4cb-169">Si tiene particiones tabla hello y filas de Hola que se insertan abarcan límites de la partición, deberá 6,144,000 filas por límite de la partición suponiendo que incluso la distribución de datos.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-169">If hello table is partitioned and hello rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="3f4cb-170">Cada partición de cada distribución independientemente debe sobrepasan el umbral de fila 102.400 de Hola para hello insert toobe mínimamente en distribución Hola.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-170">Each partition in each distribution must independently exceed hello 102,400 row threshold for hello insert toobe minimally logged into hello distribution.</span></span>
> 
> 

<span data-ttu-id="3f4cb-171">A menudo, la carga de datos en una tabla no vacía con un índice agrupado puede contener una mezcla de filas con registro completo y filas con registro mínimo.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="3f4cb-172">Un índice agrupado es un árbol equilibrado (árbol B) de las páginas.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="3f4cb-173">Si se escribe página hello tooalready contiene filas de otra transacción, a continuación, estas escrituras totalmente registrarán.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-173">If hello page being written tooalready contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="3f4cb-174">Sin embargo, si Hola página está vacía, a continuación, página de toothat de escritura de hello mínimamente registrará.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-174">However, if hello page is empty then hello write toothat page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="3f4cb-175">Optimización de eliminaciones</span><span class="sxs-lookup"><span data-stu-id="3f4cb-175">Optimizing deletes</span></span>
<span data-ttu-id="3f4cb-176">`DELETE` es una operación con registro completo.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="3f4cb-177">Si necesita toodelete una gran cantidad de datos en una tabla o una partición, resulta más conveniente demasiado`SELECT` datos Hola desea tookeep, que se puede ejecutar como una operación registrada al mínimo.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-177">If you need toodelete a large amount of data in a table or a partition, it often makes more sense too`SELECT` hello data you wish tookeep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="3f4cb-178">tooaccomplish esto, cree una nueva tabla con [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="3f4cb-178">tooaccomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="3f4cb-179">Una vez creado, use [cambiar el nombre de] [ RENAME] tooswap fuera de la tabla anterior con la tabla de hello recién creado.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-179">Once created, use [RENAME][RENAME] tooswap out your old table with hello newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
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

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="3f4cb-180">Optimización de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="3f4cb-180">Optimizing updates</span></span>
<span data-ttu-id="3f4cb-181">`UPDATE` es una operación con registro completo.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="3f4cb-182">Si necesita tooupdate un gran número de filas de una tabla o una partición suele ser mucho más eficaz toouse una operación registrada al mínimo como [CTAS] [ CTAS] toodo para.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-182">If you need tooupdate a large number of rows in a table or a partition it can often be far more efficient toouse a minimally logged operation such as [CTAS][CTAS] toodo so.</span></span>

<span data-ttu-id="3f4cb-183">Hola ejemplo a continuación de una actualización de tabla completa ha sido convertido tooa `CTAS` para que el registro mínimo es posible.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-183">In hello example below a full table update has been converted tooa `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="3f4cb-184">En este caso retrospectivamente estamos agregando una venta de toohello de importe de descuento en la tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="3f4cb-184">In this case we are retrospectively adding a discount amount toohello sales in hello table:</span></span>

```sql
--Step 01. Create a new table containing hello "Update". 
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

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="3f4cb-185">Volver a crear tablas de gran tamaño puede beneficiarse del uso de las características de administración de cargas de trabajo de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="3f4cb-186">Para obtener más detalles, consulte la sección de administración de cargas de trabajo de toohello en hello [simultaneidad] [ concurrency] artículo.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-186">For more details please refer toohello workload management section in hello [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="3f4cb-187">Optimización con modificación de particiones</span><span class="sxs-lookup"><span data-stu-id="3f4cb-187">Optimizing with partition switching</span></span>
<span data-ttu-id="3f4cb-188">Cuando se enfrenta a modificaciones a gran escala dentro de una [partición de tabla][table partition], un patrón de modificación de particiones constituye un buen enfoque.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="3f4cb-189">Si hello modificación de datos es importante e intervalos logra varias particiones, a continuación, recorrer simplemente particiones Hola Hola mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-189">If hello data modification is significant and spans multiple partitions, then simply iterating over hello partitions achieves hello same result.</span></span>

<span data-ttu-id="3f4cb-190">Hola pasos tooperform un cambio de partición son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="3f4cb-190">hello steps tooperform a partition switch are as follows:</span></span>

1. <span data-ttu-id="3f4cb-191">Crear una partición vacía de salida</span><span class="sxs-lookup"><span data-stu-id="3f4cb-191">Create an empty out partition</span></span>
2. <span data-ttu-id="3f4cb-192">Realizar actualización' hello' como un CTAS</span><span class="sxs-lookup"><span data-stu-id="3f4cb-192">Perform hello 'update' as a CTAS</span></span>
3. <span data-ttu-id="3f4cb-193">Hola toohello existente de datos tabla de desactivación</span><span class="sxs-lookup"><span data-stu-id="3f4cb-193">Switch out hello existing data toohello out table</span></span>
4. <span data-ttu-id="3f4cb-194">Intercambiar datos nuevos de Hola</span><span class="sxs-lookup"><span data-stu-id="3f4cb-194">Switch in hello new data</span></span>
5. <span data-ttu-id="3f4cb-195">Limpiar los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="3f4cb-195">Clean up hello data</span></span>

<span data-ttu-id="3f4cb-196">Sin embargo, toohelp identificar Hola particiones tooswitch primero necesitamos toobuild un procedimiento auxiliar como Hola uno a continuación.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-196">However, toohelp identify hello partitions tooswitch we will first need toobuild a helper procedure such as hello one below.</span></span> 

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

<span data-ttu-id="3f4cb-197">Este procedimiento maximiza la reutilización de código y mantiene modificación más compacta del ejemplo de la partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-197">This procedure maximizes code re-use and keeps hello partition switching example more compact.</span></span>

<span data-ttu-id="3f4cb-198">código de Hello siguiente muestra cinco pasos de hello mencionadas anteriormente tooachieve una rutina de modificación de la partición completa.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-198">hello code below demonstrates hello five steps mentioned above tooachieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
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

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
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

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="3f4cb-199">Minimización del registro con lotes pequeños</span><span class="sxs-lookup"><span data-stu-id="3f4cb-199">Minimize logging with small batches</span></span>
<span data-ttu-id="3f4cb-200">Para las operaciones de modificación de datos de gran tamaño, puede tener sentido toodivide Hola el funcionamiento en unidad de hello tooscope fragmentos o lotes de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-200">For large data modification operations, it may make sense toodivide hello operation into chunks or batches tooscope hello unit of work.</span></span>

<span data-ttu-id="3f4cb-201">A continuación, se proporciona un ejemplo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-201">A working example is provided below.</span></span> <span data-ttu-id="3f4cb-202">se ha establecido el tamaño del lote de Hello tooa trivial técnica número toohighlight Hola.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-202">hello batch size has been set tooa trivial number toohighlight hello technique.</span></span> <span data-ttu-id="3f4cb-203">En realidad, el tamaño del lote de Hola sería mucho mayor.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-203">In reality hello batch size would be significantly larger.</span></span> 

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

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="3f4cb-204">Instrucciones de operaciones de pausa y escalado</span><span class="sxs-lookup"><span data-stu-id="3f4cb-204">Pause and scaling guidance</span></span>
<span data-ttu-id="3f4cb-205">Almacenamiento de datos SQL de Azure permite pausar, reanudar y escalar su almacenamiento de datos a petición.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="3f4cb-206">Al pausar o escalar el almacenamiento de datos de SQL es toounderstand importante que las transacciones en curso terminan inmediatamente; haciendo que las transacciones abiertas toobe revierte.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-206">When you pause or scale your SQL Data Warehouse it is important toounderstand that any in-flight transactions are terminated immediately; causing any open transactions toobe rolled back.</span></span> <span data-ttu-id="3f4cb-207">Si la carga de trabajo había emitido una larga ejecución y la modificación de datos incompletos anterior toohello pausa u operación de escala, este trabajo será necesario toobe deshacer.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-207">If your workload had issued a long running and incomplete data modification prior toohello pause or scale operation, then this work will need toobe undone.</span></span> <span data-ttu-id="3f4cb-208">Esto puede afectar a Hola tarda toopause o escalar la base de datos de almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-208">This may impact hello time it takes toopause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3f4cb-209">`UPDATE` y `DELETE` son operaciones con registro completo y, por tanto, estas operaciones de deshacer y rehacer pueden tardar bastante más que las operaciones con registro mínimo equivalentes.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="3f4cb-210">escenario "mejor" Hello es toolet en vuelo datos modificación transacciones completa anterior toopausing o escala almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-210">hello best scenario is toolet in flight data modification transactions complete prior toopausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="3f4cb-211">Sin embargo, esto no siempre es posible.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-211">However, this may not always be practical.</span></span> <span data-ttu-id="3f4cb-212">riesgo de hello toomitigate de una reversión largo, considere la posibilidad de una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="3f4cb-212">toomitigate hello risk of a long rollback, consider one of hello following options:</span></span>

* <span data-ttu-id="3f4cb-213">Vuelva a escribir las operaciones de ejecución prolongada con [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="3f4cb-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="3f4cb-214">Operación de Hola se dividen en fragmentos; operar en un subconjunto de filas de Hola</span><span class="sxs-lookup"><span data-stu-id="3f4cb-214">Break hello operation down into chunks; operating on a subset of hello rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f4cb-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f4cb-215">Next steps</span></span>
<span data-ttu-id="3f4cb-216">Vea [las transacciones en el almacén de datos de SQL] [ Transactions in SQL Data Warehouse] toolearn más información acerca de los niveles de aislamiento y límites transaccionales.</span><span class="sxs-lookup"><span data-stu-id="3f4cb-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] toolearn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="3f4cb-217">Para obtener información general de otros procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="3f4cb-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

