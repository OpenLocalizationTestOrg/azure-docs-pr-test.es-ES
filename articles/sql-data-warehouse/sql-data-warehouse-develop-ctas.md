---
title: Create table as select (CTAS) en SQL Data Warehouse | Microsoft Docs
description: "Sugerencias para la codificación con la instrucción Create table as select (CTAS) en Almacenamiento de datos SQL de Azure para el desarrollo de soluciones."
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
ms.openlocfilehash: cb08313726e8135feaa9b413937c2197ea397f4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="2a38c-103">Create Table As Select (CTAS) en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="2a38c-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="2a38c-104">Create table as select o `CTAS` es una de las características más importantes de T-SQL disponibles.</span><span class="sxs-lookup"><span data-stu-id="2a38c-104">Create table as select or `CTAS` is one of the most important T-SQL features available.</span></span> <span data-ttu-id="2a38c-105">Se trata de una operación completamente en paralelo que crea una nueva tabla basada en la salida de una instrucción SELECT.</span><span class="sxs-lookup"><span data-stu-id="2a38c-105">It is a fully parallelized operation that creates a new table based on the output of a SELECT statement.</span></span> <span data-ttu-id="2a38c-106">`CTAS` es el modo más sencillo y rápido de crear una copia de una tabla.</span><span class="sxs-lookup"><span data-stu-id="2a38c-106">`CTAS` is the simplest and fastest way to create a copy of a table.</span></span> <span data-ttu-id="2a38c-107">Este documento incluye ejemplos y procedimientos recomendados para `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2a38c-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="2a38c-108">SELECT..INTO frente a CTAS</span><span class="sxs-lookup"><span data-stu-id="2a38c-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="2a38c-109">Puede considerar `CTAS` como una versión muy cargada de `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="2a38c-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="2a38c-110">Aquí tiene un ejemplo de una instrucción `SELECT..INTO` sencilla:</span><span class="sxs-lookup"><span data-stu-id="2a38c-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="2a38c-111">En el ejemplo anterior, `[dbo].[FactInternetSales_new]` se crearía como una tabla ROUND_ROBIN distribuida con un ÍNDICE CLUSTERED COLUMNSTORE en ella, ya que se trata de los valores predeterminados de tabla en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2a38c-111">In the example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are the table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="2a38c-112">`SELECT..INTO`, sin embargo, no permite cambiar el método de distribución o el tipo de índice como parte de la operación.</span><span class="sxs-lookup"><span data-stu-id="2a38c-112">`SELECT..INTO` however does not allow you to change either the distribution method or the index type as part of the operation.</span></span> <span data-ttu-id="2a38c-113">Aquí es donde `CTAS` entra en juego.</span><span class="sxs-lookup"><span data-stu-id="2a38c-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="2a38c-114">La conversión de esto a `CTAS` es bastante simple:</span><span class="sxs-lookup"><span data-stu-id="2a38c-114">To convert the above to `CTAS` is quite straight-forward:</span></span>

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

<span data-ttu-id="2a38c-115">Con `CTAS` puede cambiar la distribución de los datos de tabla, así como el tipo de tabla.</span><span class="sxs-lookup"><span data-stu-id="2a38c-115">With `CTAS` you are able to change both the distribution of the table data as well as the table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="2a38c-116">Si solo intenta cambiar el índice en la operación `CTAS` y la tabla de origen presenta una distribución hash, la operación `CTAS` ofrece mejores resultados si mantiene el mismo tipo de datos y de columna de distribución.</span><span class="sxs-lookup"><span data-stu-id="2a38c-116">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span></span> <span data-ttu-id="2a38c-117">Esto evitará el movimiento cruzado de los datos de distribución durante la operación que es más eficaz.</span><span class="sxs-lookup"><span data-stu-id="2a38c-117">This will avoid cross distribution data movement during the operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-to-copy-a-table"></a><span data-ttu-id="2a38c-118">Uso de CTAS para copiar una tabla</span><span class="sxs-lookup"><span data-stu-id="2a38c-118">Using CTAS to copy a table</span></span>
<span data-ttu-id="2a38c-119">Quizás uno de los usos más comunes de `CTAS` es el de crear una copia de una tabla, con el fin de poder cambiar el DDL.</span><span class="sxs-lookup"><span data-stu-id="2a38c-119">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span></span> <span data-ttu-id="2a38c-120">Por ejemplo, si originalmente creó la tabla como `ROUND_ROBIN` y ahora quiere convertirla en una tabla distribuida en una columna, `CTAS` le permitiría cambiar la columna de distribución.</span><span class="sxs-lookup"><span data-stu-id="2a38c-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span></span> <span data-ttu-id="2a38c-121">`CTAS` también se puede usar para cambiar las particiones, el indexado o los tipos de columnas.</span><span class="sxs-lookup"><span data-stu-id="2a38c-121">`CTAS` can also be used to change partitioning, indexing, or column types.</span></span>

<span data-ttu-id="2a38c-122">Supongamos que creó esta tabla con el tipo de distribución predeterminado, `ROUND_ROBIN` distribuido, ya que no se especificó ninguna columna de distribución en `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="2a38c-122">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span></span>

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

<span data-ttu-id="2a38c-123">Ahora desea crear una copia nueva de esta tabla con un índice de almacén de columnas en clúster, a fin de poder aprovechar el rendimiento de las tablas de almacén de columnas en clúster.</span><span class="sxs-lookup"><span data-stu-id="2a38c-123">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="2a38c-124">También desea distribuir esta tabla en ProductKey, ya que prevé combinaciones en esta columna y desea evitar el movimiento de datos durante las mismas.</span><span class="sxs-lookup"><span data-stu-id="2a38c-124">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="2a38c-125">Por último, también desea agregar la creación de particiones en OrderDateKey, con el fin de eliminar rápidamente datos antiguos mediante la anulación de particiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="2a38c-125">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="2a38c-126">Esta es la instrucción CTAS que copiaría la tabla antigua en una nueva.</span><span class="sxs-lookup"><span data-stu-id="2a38c-126">Here is the CTAS statement which would copy your old table into a new table.</span></span>

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

<span data-ttu-id="2a38c-127">Finalmente, puede cambiar el nombre de las tablas y ponerle a la tabla nueva el nombre de la antigua, para luego anular esta última.</span><span class="sxs-lookup"><span data-stu-id="2a38c-127">Finally you can rename your tables to swap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="2a38c-128">Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="2a38c-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="2a38c-129">Con la finalidad de obtener el mejor rendimiento a partir de las consultas, es importante crear estadísticas en todas las columnas de todas las tablas después de la primera carga o después de que se realiza cualquier cambio importante en los datos.</span><span class="sxs-lookup"><span data-stu-id="2a38c-129">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="2a38c-130">Si desea ver una explicación detallada de las estadísticas, consulte el tema [Estadísticas][Statistics] en el grupo de temas relacionados con el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="2a38c-130">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-to-work-around-unsupported-features"></a><span data-ttu-id="2a38c-131">Uso de CTAS para solucionar características no admitidas</span><span class="sxs-lookup"><span data-stu-id="2a38c-131">Using CTAS to work around unsupported features</span></span>
<span data-ttu-id="2a38c-132">`CTAS` para solucionar algunas de las características no admitidas que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="2a38c-132">`CTAS` can also be used to work around a number of the unsupported features listed below.</span></span> <span data-ttu-id="2a38c-133">A menudo, esto puede resultar ser una situación ventajosa para todos dado que no solo el código será compatible sino que con frecuencia se ejecutará más rápido en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="2a38c-133">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="2a38c-134">El motivo es su diseño completamente en paralelo.</span><span class="sxs-lookup"><span data-stu-id="2a38c-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="2a38c-135">Algunas situaciones que se pueden solucionar con CTAS incluyen:</span><span class="sxs-lookup"><span data-stu-id="2a38c-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="2a38c-136">ANSI JOINS en UPDATE</span><span class="sxs-lookup"><span data-stu-id="2a38c-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="2a38c-137">ANSI JOINS en DELETE</span><span class="sxs-lookup"><span data-stu-id="2a38c-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="2a38c-138">Instrucción MERGE</span><span class="sxs-lookup"><span data-stu-id="2a38c-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="2a38c-139">Intente pensar: "primero CTAS".</span><span class="sxs-lookup"><span data-stu-id="2a38c-139">Try to think "CTAS first".</span></span> <span data-ttu-id="2a38c-140">Si cree que puede resolver un problema mediante `CTAS` , este puede ser el mejor enfoque, incluso si como consecuencia escribe más datos.</span><span class="sxs-lookup"><span data-stu-id="2a38c-140">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="2a38c-141">Sustitución de una combinación ANSI en instrucciones update</span><span class="sxs-lookup"><span data-stu-id="2a38c-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="2a38c-142">Puede encontrarse con que tiene una actualización compleja que combina más de dos tablas con una sintaxis de combinación ANSI para realizar una operación UPDATE o DELETE.</span><span class="sxs-lookup"><span data-stu-id="2a38c-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span></span>

<span data-ttu-id="2a38c-143">Imagine que hubiera que actualizar esta tabla:</span><span class="sxs-lookup"><span data-stu-id="2a38c-143">Imagine you had to update this table:</span></span>

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

<span data-ttu-id="2a38c-144">La consulta original podría haber tenido esta apariencia:</span><span class="sxs-lookup"><span data-stu-id="2a38c-144">The original query might have looked something like this:</span></span>

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

<span data-ttu-id="2a38c-145">Dado que SQL Data Warehouse no admite combinaciones ANSI en la cláusula `FROM` de una instrucción `UPDATE`, no puede copiar este código sin cambiarlo ligeramente.</span><span class="sxs-lookup"><span data-stu-id="2a38c-145">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="2a38c-146">Puede usar una mezcla de un `CTAS` y una combinación implícita para reemplazar este código:</span><span class="sxs-lookup"><span data-stu-id="2a38c-146">You can use a combination of a `CTAS` and an implicit join to replace this code:</span></span>

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

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="2a38c-147">Sustitución de una combinación ANSI en instrucciones delete</span><span class="sxs-lookup"><span data-stu-id="2a38c-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="2a38c-148">A veces el mejor enfoque para eliminar los datos es el uso de `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2a38c-148">Sometimes the best approach for deleting data is to use `CTAS`.</span></span> <span data-ttu-id="2a38c-149">En lugar de eliminar los datos, simplemente seleccione los datos que desea conservar.</span><span class="sxs-lookup"><span data-stu-id="2a38c-149">Rather than deleting the data simply select the data you want to keep.</span></span> <span data-ttu-id="2a38c-150">Esto resulta especialmente cierto para las instrucciones `DELETE` que usan la sintaxis de unión ansi, ya que SQL Data Warehouse no admite combinaciones ANSI en la cláusula `FROM` de una instrucción `DELETE`.</span><span class="sxs-lookup"><span data-stu-id="2a38c-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="2a38c-151">A continuación se muestra un ejemplo de una instrucción DELETE convertida:</span><span class="sxs-lookup"><span data-stu-id="2a38c-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="2a38c-152">Sustitución de instrucciones MERGE</span><span class="sxs-lookup"><span data-stu-id="2a38c-152">Replace merge statements</span></span>
<span data-ttu-id="2a38c-153">Las instrucciones merge se pueden sustituir, al menos en parte, mediante el uso de `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2a38c-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="2a38c-154">Puede consolidar `INSERT` y `UPDATE` en una única instrucción.</span><span class="sxs-lookup"><span data-stu-id="2a38c-154">You can consolidate the `INSERT` and the `UPDATE` into a single statement.</span></span> <span data-ttu-id="2a38c-155">Sería necesario que los registros eliminados se bloquearan en una segunda instrucción.</span><span class="sxs-lookup"><span data-stu-id="2a38c-155">Any deleted records would need to be closed off in a second statement.</span></span>

<span data-ttu-id="2a38c-156">Un ejemplo de un `UPSERT` está disponible a continuación:</span><span class="sxs-lookup"><span data-stu-id="2a38c-156">An example of an `UPSERT` is available below:</span></span>

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

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="2a38c-157">Recomendación de CTAS: establezca explícitamente el tipo de datos y la nulabilidad de salida</span><span class="sxs-lookup"><span data-stu-id="2a38c-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="2a38c-158">Al migrar código, podría encontrarse ejecutando este tipo modelo de codificación:</span><span class="sxs-lookup"><span data-stu-id="2a38c-158">When migrating code you might find you run across this type of coding pattern:</span></span>

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

<span data-ttu-id="2a38c-159">Instintivamente, puede pensar que debería migrar este código a CTAS y sería correcto.</span><span class="sxs-lookup"><span data-stu-id="2a38c-159">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span></span> <span data-ttu-id="2a38c-160">Sin embargo, hay un problema oculto aquí.</span><span class="sxs-lookup"><span data-stu-id="2a38c-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="2a38c-161">El siguiente código NO produce el mismo resultado:</span><span class="sxs-lookup"><span data-stu-id="2a38c-161">The following code does NOT yield the same result:</span></span>

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

<span data-ttu-id="2a38c-162">Observe que la columna "resultado" traslada los valores de tipo y nulabilidad de los datos de la expresión.</span><span class="sxs-lookup"><span data-stu-id="2a38c-162">Notice that the column "result" carries forward the data type and nullability values of the expression.</span></span> <span data-ttu-id="2a38c-163">Esto puede provocar sutiles variaciones en los valores si no tiene cuidado.</span><span class="sxs-lookup"><span data-stu-id="2a38c-163">This can lead to subtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="2a38c-164">Intente lo siguiente como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2a38c-164">Try the following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="2a38c-165">El valor almacenado para el resultado es diferente.</span><span class="sxs-lookup"><span data-stu-id="2a38c-165">The value stored for result is different.</span></span> <span data-ttu-id="2a38c-166">Como el valor persistente en la columna de resultados se usa en otras expresiones, el error se vuelve más importante incluso.</span><span class="sxs-lookup"><span data-stu-id="2a38c-166">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="2a38c-167">Esto es especialmente importante para las migraciones de datos.</span><span class="sxs-lookup"><span data-stu-id="2a38c-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="2a38c-168">Aunque se puede decir que la segunda consulta es más precisa, hay un problema.</span><span class="sxs-lookup"><span data-stu-id="2a38c-168">Even though the second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="2a38c-169">Los datos serán diferentes en comparación con el sistema de origen y eso conduce a preguntas sobre la integridad de la migración.</span><span class="sxs-lookup"><span data-stu-id="2a38c-169">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span></span> <span data-ttu-id="2a38c-170">Éste es uno de esos casos raros en los que la respuesta "incorrecta" es realmente la adecuada.</span><span class="sxs-lookup"><span data-stu-id="2a38c-170">This is one of those rare cases where the "wrong" answer is actually the right one!</span></span>

<span data-ttu-id="2a38c-171">El motivo de que veamos esta disparidad entre los dos resultados se debe a la conversión implícita de los tipos.</span><span class="sxs-lookup"><span data-stu-id="2a38c-171">The reason we see this disparity between the two results is down to implicit type casting.</span></span> <span data-ttu-id="2a38c-172">En el primer ejemplo, la tabla define la definición de columna.</span><span class="sxs-lookup"><span data-stu-id="2a38c-172">In the first example the table defines the column definition.</span></span> <span data-ttu-id="2a38c-173">Cuando se inserta la fila, se produce una conversión implícita de los tipos.</span><span class="sxs-lookup"><span data-stu-id="2a38c-173">When the row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="2a38c-174">En el segundo ejemplo, no hay ninguna conversión de tipos implícita ya que la expresión define el tipo de datos de la columna.</span><span class="sxs-lookup"><span data-stu-id="2a38c-174">In the second example there is no implicit type conversion as the expression defines data type of the column.</span></span> <span data-ttu-id="2a38c-175">Observe también que la columna del segundo ejemplo se ha definido como una columna que acepta valores NULL mientras que en el primer ejemplo no.</span><span class="sxs-lookup"><span data-stu-id="2a38c-175">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span></span> <span data-ttu-id="2a38c-176">Cuando se creó la tabla en el primer ejemplo, la nulabilidad se definió explícitamente.</span><span class="sxs-lookup"><span data-stu-id="2a38c-176">When the table was created in the first example column nullability was explicitly defined.</span></span> <span data-ttu-id="2a38c-177">En el segundo ejemplo, simplemente se dejó con la expresión y, de forma predeterminada, esto dará lugar a una definición de NULL.</span><span class="sxs-lookup"><span data-stu-id="2a38c-177">In the second example it was just left to the expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="2a38c-178">Para resolver estos problemas, debe establecer explícitamente la conversión de tipos y la nulabilidad en la parte `SELECT` de la instrucción `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2a38c-178">To resolve these issues you must explicitly set the type conversion and nullability in the `SELECT` portion of the `CTAS` statement.</span></span> <span data-ttu-id="2a38c-179">No se pueden establecer estas propiedades en la parte create table.</span><span class="sxs-lookup"><span data-stu-id="2a38c-179">You cannot set these properties in the create table part.</span></span>

<span data-ttu-id="2a38c-180">En el ejemplo siguiente se muestra cómo corregir el código:</span><span class="sxs-lookup"><span data-stu-id="2a38c-180">The example below demonstrates how to fix the code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="2a38c-181">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a38c-181">Note the following:</span></span>

* <span data-ttu-id="2a38c-182">Se podría haber usado CAST o CONVERT.</span><span class="sxs-lookup"><span data-stu-id="2a38c-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="2a38c-183">ISNULL se usa para forzar la nulabilidad no COALESCE.</span><span class="sxs-lookup"><span data-stu-id="2a38c-183">ISNULL is used to force NULLability not COALESCE</span></span>
* <span data-ttu-id="2a38c-184">ISNULL es la función más externa.</span><span class="sxs-lookup"><span data-stu-id="2a38c-184">ISNULL is the outermost function</span></span>
* <span data-ttu-id="2a38c-185">La segunda parte de ISNULL es una constante, es decir, 0.</span><span class="sxs-lookup"><span data-stu-id="2a38c-185">The second part of the ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="2a38c-186">Para que la nulabilidad se establezca correctamente, es fundamental usar `ISNULL` y no `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="2a38c-186">For the nullability to be correctly set it is vital to use `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="2a38c-187">`COALESCE` no es una función determinista y, por tanto, el resultado de la expresión siempre será NULLable.</span><span class="sxs-lookup"><span data-stu-id="2a38c-187">`COALESCE` is not a deterministic function and so the result of the expression will always be NULLable.</span></span> <span data-ttu-id="2a38c-188">`ISNULL` es diferente.</span><span class="sxs-lookup"><span data-stu-id="2a38c-188">`ISNULL` is different.</span></span> <span data-ttu-id="2a38c-189">Es determinista.</span><span class="sxs-lookup"><span data-stu-id="2a38c-189">It is deterministic.</span></span> <span data-ttu-id="2a38c-190">Por lo tanto, cuando la segunda parte de la función `ISNULL` es una constante o un literal, el valor resultante será NOT NULL.</span><span class="sxs-lookup"><span data-stu-id="2a38c-190">Therefore when the second part of the `ISNULL` function is a constant or a literal then the resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="2a38c-191">Esta sugerencia no solo es útil para garantizar la integridad de los cálculos.</span><span class="sxs-lookup"><span data-stu-id="2a38c-191">This tip is not just useful for ensuring the integrity of your calculations.</span></span> <span data-ttu-id="2a38c-192">También es importante para la modificación de particiones de tabla.</span><span class="sxs-lookup"><span data-stu-id="2a38c-192">It is also important for table partition switching.</span></span> <span data-ttu-id="2a38c-193">Imagine que tiene esta tabla definida como hecho:</span><span class="sxs-lookup"><span data-stu-id="2a38c-193">Imagine you have this table defined as your fact:</span></span>

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

<span data-ttu-id="2a38c-194">Sin embargo, el campo de valor es una expresión calculada que no forma parte de los datos de origen.</span><span class="sxs-lookup"><span data-stu-id="2a38c-194">However, the value field is a calculated expression it is not part of the source data.</span></span>

<span data-ttu-id="2a38c-195">Para crear el conjunto de datos particionado, podría hacer esto:</span><span class="sxs-lookup"><span data-stu-id="2a38c-195">To create your partitioned dataset you might want to do this:</span></span>

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

<span data-ttu-id="2a38c-196">La consulta se ejecutaría perfectamente.</span><span class="sxs-lookup"><span data-stu-id="2a38c-196">The query would run perfectly fine.</span></span> <span data-ttu-id="2a38c-197">El problema se produce al intentar realizar el cambio de partición.</span><span class="sxs-lookup"><span data-stu-id="2a38c-197">The problem comes when you try to perform the partition switch.</span></span> <span data-ttu-id="2a38c-198">Las definiciones de tabla no coinciden.</span><span class="sxs-lookup"><span data-stu-id="2a38c-198">The table definitions do not match.</span></span> <span data-ttu-id="2a38c-199">Para que las definiciones de tabla coincidan, CTAS debe modificarse.</span><span class="sxs-lookup"><span data-stu-id="2a38c-199">To make the table definitions match the CTAS needs to be modified.</span></span>

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

<span data-ttu-id="2a38c-200">Por lo tanto, puede ver que la coherencia de los tipos y el mantenimiento de las propiedades de nulabilidad en CTAS es una buena práctica de ingeniería.</span><span class="sxs-lookup"><span data-stu-id="2a38c-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="2a38c-201">Ayuda a mantener la integridad de los cálculos y también garantiza que la modificación de particiones es posible.</span><span class="sxs-lookup"><span data-stu-id="2a38c-201">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="2a38c-202">Consulte MSDN para obtener más información sobre el uso de [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="2a38c-202">Please refer to MSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="2a38c-203">Es una de las instrucciones más importantes de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="2a38c-203">It is one of the most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2a38c-204">Asegúrese de que la comprende perfectamente.</span><span class="sxs-lookup"><span data-stu-id="2a38c-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a38c-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a38c-205">Next steps</span></span>
<span data-ttu-id="2a38c-206">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="2a38c-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
