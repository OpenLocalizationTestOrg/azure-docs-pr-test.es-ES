---
title: "tabla de aaaCreate como seleccione (CTAS) en el almacén de datos de SQL | Documentos de Microsoft"
description: "Sugerencias para codificar con hello crear tabla de la opción de instrucción (CTAS) en el almacén de datos de SQL Azure para desarrollar soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="86a0e-103">Create Table As Select (CTAS) en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="86a0e-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="86a0e-104">Crear tabla como select o `CTAS` es uno de hello más importantes características de T-SQL disponibles.</span><span class="sxs-lookup"><span data-stu-id="86a0e-104">Create table as select or `CTAS` is one of hello most important T-SQL features available.</span></span> <span data-ttu-id="86a0e-105">Es una operación de ejecución en paralelo totalmente que crea una nueva tabla en función de la salida de hello de una instrucción SELECT.</span><span class="sxs-lookup"><span data-stu-id="86a0e-105">It is a fully parallelized operation that creates a new table based on hello output of a SELECT statement.</span></span> <span data-ttu-id="86a0e-106">`CTAS`es una copia de una tabla de hello toocreate de forma más sencilla y rápida.</span><span class="sxs-lookup"><span data-stu-id="86a0e-106">`CTAS` is hello simplest and fastest way toocreate a copy of a table.</span></span> <span data-ttu-id="86a0e-107">Este documento incluye ejemplos y procedimientos recomendados para `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="86a0e-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="86a0e-108">SELECT..INTO frente a CTAS</span><span class="sxs-lookup"><span data-stu-id="86a0e-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="86a0e-109">Puede considerar `CTAS` como una versión muy cargada de `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="86a0e-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="86a0e-110">Aquí tiene un ejemplo de una instrucción `SELECT..INTO` sencilla:</span><span class="sxs-lookup"><span data-stu-id="86a0e-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="86a0e-111">En el ejemplo de Hola anterior `[dbo].[FactInternetSales_new]` se crearán como tabla distribuida de ROUND_ROBIN con un índice de almacén de columnas en clúster en el se trata de valores predeterminados de la tabla de hello en el almacén de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="86a0e-111">In hello example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are hello table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="86a0e-112">`SELECT..INTO`Sin embargo no podrá toochange cualquier índice hello, distribución, método o hello escribe como parte de la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a0e-112">`SELECT..INTO` however does not allow you toochange either hello distribution method or hello index type as part of hello operation.</span></span> <span data-ttu-id="86a0e-113">Aquí es donde `CTAS` entra en juego.</span><span class="sxs-lookup"><span data-stu-id="86a0e-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="86a0e-114">tooconvert Hola anteriormente demasiado`CTAS` es bastante sencilla:</span><span class="sxs-lookup"><span data-stu-id="86a0e-114">tooconvert hello above too`CTAS` is quite straight-forward:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<span data-ttu-id="86a0e-115">Con `CTAS` es capaz de toochange ambos Hola distribución de datos de la tabla de hello, así como el tipo de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="86a0e-115">With `CTAS` you are able toochange both hello distribution of hello table data as well as hello table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="86a0e-116">Si solo está tratando de índice de hello toochange en su `CTAS` hello y operación de tabla de origen es hash distribuida la `CTAS` llevará a cabo operación mejor si mantiene Hola el mismo tipo de columna y los datos de distribución.</span><span class="sxs-lookup"><span data-stu-id="86a0e-116">If you are only trying toochange hello index in your `CTAS` operation and hello source table is hash distributed then your `CTAS` operation will perform best if you maintain hello same distribution column and data type.</span></span> <span data-ttu-id="86a0e-117">Esto evitará cross movimiento de datos de distribución durante la operación de Hola que es más eficaz.</span><span class="sxs-lookup"><span data-stu-id="86a0e-117">This will avoid cross distribution data movement during hello operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-toocopy-a-table"></a><span data-ttu-id="86a0e-118">Usar CTAS toocopy una tabla</span><span class="sxs-lookup"><span data-stu-id="86a0e-118">Using CTAS toocopy a table</span></span>
<span data-ttu-id="86a0e-119">Quizás uno de hello más comunes usos del `CTAS` es crear una copia de una tabla para que pueda cambiar Hola DDL.</span><span class="sxs-lookup"><span data-stu-id="86a0e-119">Perhaps one of hello most common uses of `CTAS` is creating a copy of a table so that you can change hello DDL.</span></span> <span data-ttu-id="86a0e-120">Si por ejemplo creó originalmente la tabla como `ROUND_ROBIN` y ahora desea cambiarla tooa tabla distribuida en una columna, `CTAS` es ¿cómo cambiaría la columna de distribución de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a0e-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it tooa table distributed on a column, `CTAS` is how you would change hello distribution column.</span></span> <span data-ttu-id="86a0e-121">`CTAS`También puede ser usado toochange tipos de particiones, la indización o la columna.</span><span class="sxs-lookup"><span data-stu-id="86a0e-121">`CTAS` can also be used toochange partitioning, indexing, or column types.</span></span>

<span data-ttu-id="86a0e-122">Supongamos que creó esta tabla utilizando el tipo de distribución de hello predeterminado de `ROUND_ROBIN` distribuidas porque se especificó ninguna columna de distribución en hello `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="86a0e-122">Let's say you created this table using hello default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in hello `CREATE TABLE`.</span></span>

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

<span data-ttu-id="86a0e-123">Ahora desea toocreate una nueva copia de esta tabla con un índice de almacén de columnas agrupado por lo que puede aprovechar las ventajas de rendimiento de Hola de tablas de almacén de columnas clúster.</span><span class="sxs-lookup"><span data-stu-id="86a0e-123">Now you want toocreate a new copy of this table with a Clustered Columnstore Index so that you can take advantage of hello performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="86a0e-124">También puede toodistribute esta tabla en ProductKey desde que se anticipan combinaciones en esta columna y desea que el movimiento de datos tooavoid durante las combinaciones en ProductKey.</span><span class="sxs-lookup"><span data-stu-id="86a0e-124">You also want toodistribute this table on ProductKey since you are anticipating joins on this column and want tooavoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="86a0e-125">Por último también es conveniente tooadd creación de particiones en OrderDateKey para que pueda eliminar rápidamente los datos antiguos colocando particiones antiguas.</span><span class="sxs-lookup"><span data-stu-id="86a0e-125">Lastly you also want tooadd partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="86a0e-126">Aquí es instrucción CTAS de Hola que copiaría la tabla anterior en una nueva tabla.</span><span class="sxs-lookup"><span data-stu-id="86a0e-126">Here is hello CTAS statement which would copy your old table into a new table.</span></span>

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

<span data-ttu-id="86a0e-127">Por último, puede cambiar el nombre de su tooswap de tablas en la nueva tabla y, a continuación, elimine la tabla anterior.</span><span class="sxs-lookup"><span data-stu-id="86a0e-127">Finally you can rename your tables tooswap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="86a0e-128">Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="86a0e-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="86a0e-129">En orden tooget Hola un mejor rendimiento de las consultas, es importante que las estadísticas se crean en todas las columnas de todas las tablas después de la primera carga de Hola o se producen cambios sustanciales en datos Hola.</span><span class="sxs-lookup"><span data-stu-id="86a0e-129">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="86a0e-130">Para obtener una explicación detallada de las estadísticas, vea hello [estadísticas] [ Statistics] tema en el grupo de desarrollo de Hola de temas.</span><span class="sxs-lookup"><span data-stu-id="86a0e-130">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a><span data-ttu-id="86a0e-131">Usar toowork CTAS según las características no admitidas</span><span class="sxs-lookup"><span data-stu-id="86a0e-131">Using CTAS toowork around unsupported features</span></span>
<span data-ttu-id="86a0e-132">`CTAS`También se puede ser usado toowork alrededor de un número de características no admitida de Hola enumeradas a continuación.</span><span class="sxs-lookup"><span data-stu-id="86a0e-132">`CTAS` can also be used toowork around a number of hello unsupported features listed below.</span></span> <span data-ttu-id="86a0e-133">Esto puede a menudo demostrar toobe una situación favorece como no solo el código serán compatible, pero a menudo se ejecutará más rápido en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="86a0e-133">This can often prove toobe a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="86a0e-134">El motivo es su diseño completamente en paralelo.</span><span class="sxs-lookup"><span data-stu-id="86a0e-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="86a0e-135">Algunas situaciones que se pueden solucionar con CTAS incluyen:</span><span class="sxs-lookup"><span data-stu-id="86a0e-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="86a0e-136">ANSI JOINS en UPDATE</span><span class="sxs-lookup"><span data-stu-id="86a0e-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="86a0e-137">ANSI JOINS en DELETE</span><span class="sxs-lookup"><span data-stu-id="86a0e-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="86a0e-138">Instrucción MERGE</span><span class="sxs-lookup"><span data-stu-id="86a0e-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="86a0e-139">Intente toothink "CTAS primera".</span><span class="sxs-lookup"><span data-stu-id="86a0e-139">Try toothink "CTAS first".</span></span> <span data-ttu-id="86a0e-140">Si cree que puede resolver un problema mediante `CTAS` , a continuación, que suele ser tooapproach de manera mejor de hello, incluso si se escribe como resultado más datos.</span><span class="sxs-lookup"><span data-stu-id="86a0e-140">If you think you can solve a problem using `CTAS` then that is generally hello best way tooapproach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="86a0e-141">Sustitución de una combinación ANSI en instrucciones update</span><span class="sxs-lookup"><span data-stu-id="86a0e-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="86a0e-142">Es posible que tener una actualización compleja que combina más de dos tablas juntos mediante unión hello tooperform de sintaxis de ANSI UPDATE o DELETE.</span><span class="sxs-lookup"><span data-stu-id="86a0e-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax tooperform hello UPDATE or DELETE.</span></span>

<span data-ttu-id="86a0e-143">Imagine que había tooupdate esta tabla:</span><span class="sxs-lookup"><span data-stu-id="86a0e-143">Imagine you had tooupdate this table:</span></span>

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

<span data-ttu-id="86a0e-144">consulta de Hello original podría han consultado algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="86a0e-144">hello original query might have looked something like this:</span></span>

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

<span data-ttu-id="86a0e-145">Puesto que el almacenamiento de datos SQL no es compatible con ANSI combinaciones en hello `FROM` cláusula de una `UPDATE` (instrucción), no se puede copiar este código a través sin cambiar ligeramente.</span><span class="sxs-lookup"><span data-stu-id="86a0e-145">Since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="86a0e-146">Puede usar una combinación de un `CTAS` y un modo implícito unir tooreplace este código:</span><span class="sxs-lookup"><span data-stu-id="86a0e-146">You can use a combination of a `CTAS` and an implicit join tooreplace this code:</span></span>

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="86a0e-147">Sustitución de una combinación ANSI en instrucciones delete</span><span class="sxs-lookup"><span data-stu-id="86a0e-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="86a0e-148">A veces mejor método para eliminar datos de hello es toouse `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="86a0e-148">Sometimes hello best approach for deleting data is toouse `CTAS`.</span></span> <span data-ttu-id="86a0e-149">En lugar de eliminar datos de hello basta con seleccionar datos de Hola que desee tookeep.</span><span class="sxs-lookup"><span data-stu-id="86a0e-149">Rather than deleting hello data simply select hello data you want tookeep.</span></span> <span data-ttu-id="86a0e-150">Este especialmente cierto para `DELETE` las instrucciones que utilizan ansi unir sintaxis puesto que el almacenamiento de datos SQL no admite combinaciones ANSI en hello `FROM` cláusula de una `DELETE` instrucción.</span><span class="sxs-lookup"><span data-stu-id="86a0e-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="86a0e-151">A continuación se muestra un ejemplo de una instrucción DELETE convertida:</span><span class="sxs-lookup"><span data-stu-id="86a0e-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="86a0e-152">Sustitución de instrucciones MERGE</span><span class="sxs-lookup"><span data-stu-id="86a0e-152">Replace merge statements</span></span>
<span data-ttu-id="86a0e-153">Las instrucciones merge se pueden sustituir, al menos en parte, mediante el uso de `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="86a0e-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="86a0e-154">Es posible consolidar hello `INSERT` hello y `UPDATE` en una única instrucción.</span><span class="sxs-lookup"><span data-stu-id="86a0e-154">You can consolidate hello `INSERT` and hello `UPDATE` into a single statement.</span></span> <span data-ttu-id="86a0e-155">Los registros eliminados necesitaría toobe cerrado en una segunda instrucción.</span><span class="sxs-lookup"><span data-stu-id="86a0e-155">Any deleted records would need toobe closed off in a second statement.</span></span>

<span data-ttu-id="86a0e-156">Un ejemplo de un `UPSERT` está disponible a continuación:</span><span class="sxs-lookup"><span data-stu-id="86a0e-156">An example of an `UPSERT` is available below:</span></span>

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="86a0e-157">Recomendación de CTAS: establezca explícitamente el tipo de datos y la nulabilidad de salida</span><span class="sxs-lookup"><span data-stu-id="86a0e-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="86a0e-158">Al migrar código, podría encontrarse ejecutando este tipo modelo de codificación:</span><span class="sxs-lookup"><span data-stu-id="86a0e-158">When migrating code you might find you run across this type of coding pattern:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

<span data-ttu-id="86a0e-159">Instintivamente que piense debería migrar este tooa código CTAS y se correcto.</span><span class="sxs-lookup"><span data-stu-id="86a0e-159">Instinctively you might think you should migrate this code tooa CTAS and you would be correct.</span></span> <span data-ttu-id="86a0e-160">Sin embargo, hay un problema oculto aquí.</span><span class="sxs-lookup"><span data-stu-id="86a0e-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="86a0e-161">Hello siguiente código no produce Hola el mismo resultado:</span><span class="sxs-lookup"><span data-stu-id="86a0e-161">hello following code does NOT yield hello same result:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

<span data-ttu-id="86a0e-162">Tenga en cuenta que Hola columna "resultado" traslada los valores de tipo y la nulabilidad de datos Hola de expresión de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a0e-162">Notice that hello column "result" carries forward hello data type and nullability values of hello expression.</span></span> <span data-ttu-id="86a0e-163">Esto puede provocar toosubtle varianzas en valores si no tiene cuidado.</span><span class="sxs-lookup"><span data-stu-id="86a0e-163">This can lead toosubtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="86a0e-164">Intente Hola siguiente como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86a0e-164">Try hello following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="86a0e-165">valor de Hello almacenado para el resultado es diferente.</span><span class="sxs-lookup"><span data-stu-id="86a0e-165">hello value stored for result is different.</span></span> <span data-ttu-id="86a0e-166">Dado que el valor almacenado en la columna de resultados de Hola Hola se utiliza una en otro error Hola de expresiones se convierte en incluso más significativo.</span><span class="sxs-lookup"><span data-stu-id="86a0e-166">As hello persisted value in hello result column is used in other expressions hello error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="86a0e-167">Esto es especialmente importante para las migraciones de datos.</span><span class="sxs-lookup"><span data-stu-id="86a0e-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="86a0e-168">Aunque la segunda consulta de hello es sin duda más precisa, hay un problema.</span><span class="sxs-lookup"><span data-stu-id="86a0e-168">Even though hello second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="86a0e-169">datos de Hello sería toohello en comparación con otro sistema de origen y conduce tooquestions de integridad en migración Hola.</span><span class="sxs-lookup"><span data-stu-id="86a0e-169">hello data would be different compared toohello source system and that leads tooquestions of integrity in hello migration.</span></span> <span data-ttu-id="86a0e-170">Este es uno de los pocos casos donde la respuesta "incorrecto" hello es realmente Hola derecha.</span><span class="sxs-lookup"><span data-stu-id="86a0e-170">This is one of those rare cases where hello "wrong" answer is actually hello right one!</span></span>

<span data-ttu-id="86a0e-171">Hello motivo vemos esta disparidad entre los resultados de hello dos está inactivo tooimplicit conversión de tipos.</span><span class="sxs-lookup"><span data-stu-id="86a0e-171">hello reason we see this disparity between hello two results is down tooimplicit type casting.</span></span> <span data-ttu-id="86a0e-172">Hola primera tabla de ejemplo Hola define la definición de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a0e-172">In hello first example hello table defines hello column definition.</span></span> <span data-ttu-id="86a0e-173">Cuando se inserta la fila de Hola se realiza una conversión de tipos implícita.</span><span class="sxs-lookup"><span data-stu-id="86a0e-173">When hello row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="86a0e-174">En el segundo ejemplo de Hola no hay ninguna conversión de tipos implícita como expresión de hello define el tipo de datos de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a0e-174">In hello second example there is no implicit type conversion as hello expression defines data type of hello column.</span></span> <span data-ttu-id="86a0e-175">Tenga en cuenta que también esa columna hello en el segundo ejemplo de Hola se ha definido como una columna que acepta valores NULL, mientras que en el primer ejemplo de Hola no tiene.</span><span class="sxs-lookup"><span data-stu-id="86a0e-175">Notice also that hello column in hello second example has been defined as a NULLable column whereas in hello first example it has not.</span></span> <span data-ttu-id="86a0e-176">Cuando se crea la tabla de hello en hello primer ejemplo nulabilidad en las columnas se define explícitamente.</span><span class="sxs-lookup"><span data-stu-id="86a0e-176">When hello table was created in hello first example column nullability was explicitly defined.</span></span> <span data-ttu-id="86a0e-177">En el segundo ejemplo de Hola simplemente quedó toohello expresión y de forma predeterminada, esto se creará en una definición de NULL.</span><span class="sxs-lookup"><span data-stu-id="86a0e-177">In hello second example it was just left toohello expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="86a0e-178">tooresolve estos aspectos que debe establecer explícitamente la conversión de tipos de Hola y la nulabilidad en hello `SELECT` parte de hello `CTAS` instrucción.</span><span class="sxs-lookup"><span data-stu-id="86a0e-178">tooresolve these issues you must explicitly set hello type conversion and nullability in hello `SELECT` portion of hello `CTAS` statement.</span></span> <span data-ttu-id="86a0e-179">No se puede establecer estas propiedades en hello crear elemento de tabla.</span><span class="sxs-lookup"><span data-stu-id="86a0e-179">You cannot set these properties in hello create table part.</span></span>

<span data-ttu-id="86a0e-180">ejemplo de Hola siguiente muestra cómo toofix Hola código:</span><span class="sxs-lookup"><span data-stu-id="86a0e-180">hello example below demonstrates how toofix hello code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="86a0e-181">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="86a0e-181">Note hello following:</span></span>

* <span data-ttu-id="86a0e-182">Se podría haber usado CAST o CONVERT.</span><span class="sxs-lookup"><span data-stu-id="86a0e-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="86a0e-183">ISNULL es tooforce usado nulabilidad no COALESCE</span><span class="sxs-lookup"><span data-stu-id="86a0e-183">ISNULL is used tooforce NULLability not COALESCE</span></span>
* <span data-ttu-id="86a0e-184">ISNULL es la función más externo Hola</span><span class="sxs-lookup"><span data-stu-id="86a0e-184">ISNULL is hello outermost function</span></span>
* <span data-ttu-id="86a0e-185">Hola segunda parte del programa Hola ISNULL es una constante, es decir, 0</span><span class="sxs-lookup"><span data-stu-id="86a0e-185">hello second part of hello ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="86a0e-186">Para hello nulabilidad toobe establece correctamente es vital toouse `ISNULL` y no `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="86a0e-186">For hello nullability toobe correctly set it is vital toouse `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="86a0e-187">`COALESCE`no es una función determinista y así Hola será resultado de expresión Hola siempre acepta valores NULL.</span><span class="sxs-lookup"><span data-stu-id="86a0e-187">`COALESCE` is not a deterministic function and so hello result of hello expression will always be NULLable.</span></span> <span data-ttu-id="86a0e-188">`ISNULL` es diferente.</span><span class="sxs-lookup"><span data-stu-id="86a0e-188">`ISNULL` is different.</span></span> <span data-ttu-id="86a0e-189">Es determinista.</span><span class="sxs-lookup"><span data-stu-id="86a0e-189">It is deterministic.</span></span> <span data-ttu-id="86a0e-190">Por lo tanto, cuando Hola segunda parte del programa Hola `ISNULL` función es una constante o un literal, a continuación, el valor resultante hello no NULL.</span><span class="sxs-lookup"><span data-stu-id="86a0e-190">Therefore when hello second part of hello `ISNULL` function is a constant or a literal then hello resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="86a0e-191">Esta sugerencia no es sólo es útil para garantizar la integridad de Hola de los cálculos.</span><span class="sxs-lookup"><span data-stu-id="86a0e-191">This tip is not just useful for ensuring hello integrity of your calculations.</span></span> <span data-ttu-id="86a0e-192">También es importante para la modificación de particiones de tabla.</span><span class="sxs-lookup"><span data-stu-id="86a0e-192">It is also important for table partition switching.</span></span> <span data-ttu-id="86a0e-193">Imagine que tiene esta tabla definida como hecho:</span><span class="sxs-lookup"><span data-stu-id="86a0e-193">Imagine you have this table defined as your fact:</span></span>

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

<span data-ttu-id="86a0e-194">Sin embargo, el campo de valor de Hola es una expresión calculada no es parte de los datos de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a0e-194">However, hello value field is a calculated expression it is not part of hello source data.</span></span>

<span data-ttu-id="86a0e-195">toocreate el conjunto de datos con particiones puede toodo esto:</span><span class="sxs-lookup"><span data-stu-id="86a0e-195">toocreate your partitioned dataset you might want toodo this:</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

<span data-ttu-id="86a0e-196">consulta de Hello llevarían a cabo perfectamente correcto.</span><span class="sxs-lookup"><span data-stu-id="86a0e-196">hello query would run perfectly fine.</span></span> <span data-ttu-id="86a0e-197">problema de Hello aparece cuando intenta tooperform cambio de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a0e-197">hello problem comes when you try tooperform hello partition switch.</span></span> <span data-ttu-id="86a0e-198">las definiciones de tabla de Hello no coinciden.</span><span class="sxs-lookup"><span data-stu-id="86a0e-198">hello table definitions do not match.</span></span> <span data-ttu-id="86a0e-199">definiciones de tabla toomake Hola encontrar Hola que ctas necesita toobe modificado.</span><span class="sxs-lookup"><span data-stu-id="86a0e-199">toomake hello table definitions match hello CTAS needs toobe modified.</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

<span data-ttu-id="86a0e-200">Por lo tanto, puede ver que la coherencia de los tipos y el mantenimiento de las propiedades de nulabilidad en CTAS es una buena práctica de ingeniería.</span><span class="sxs-lookup"><span data-stu-id="86a0e-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="86a0e-201">Le ayuda a toomaintain de integridad en los cálculos y también garantiza que la modificación de particiones es posible.</span><span class="sxs-lookup"><span data-stu-id="86a0e-201">It helps toomaintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="86a0e-202">Consulte tooMSDN para obtener más información sobre el uso de [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="86a0e-202">Please refer tooMSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="86a0e-203">Es una de las instrucciones de más importantes de hello en el almacén de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="86a0e-203">It is one of hello most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="86a0e-204">Asegúrese de que la comprende perfectamente.</span><span class="sxs-lookup"><span data-stu-id="86a0e-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a0e-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86a0e-205">Next steps</span></span>
<span data-ttu-id="86a0e-206">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="86a0e-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
