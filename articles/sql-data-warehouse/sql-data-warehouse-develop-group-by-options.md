---
title: Opciones de Group by en SQL Data Warehouse | Microsoft Docs
description: Sugerencias para implementar opciones de Group by en Almacenamiento de datos SQL de Azure para el desarrollo de soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: da71cb834c13da5d0f5690f471efc6c696163f30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="eef43-103">Opciones de Group by en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="eef43-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="eef43-104">La cláusula [GROUP BY][GROUP BY] se usa para agregar datos a un conjunto de filas de resumen.</span><span class="sxs-lookup"><span data-stu-id="eef43-104">The [GROUP BY][GROUP BY] clause is used to aggregate data to a summary set of rows.</span></span> <span data-ttu-id="eef43-105">También cuenta con algunas opciones que amplían su funcionalidad y que es necesario solucionar ya que no son directamente compatibles con Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="eef43-105">It also has a few options that extend it's functionality that need to be worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="eef43-106">Estas opciones son:</span><span class="sxs-lookup"><span data-stu-id="eef43-106">These options are</span></span>

* <span data-ttu-id="eef43-107">GROUP BY con ROLLUP</span><span class="sxs-lookup"><span data-stu-id="eef43-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="eef43-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="eef43-108">GROUPING SETS</span></span>
* <span data-ttu-id="eef43-109">GROUP BY con CUBE</span><span class="sxs-lookup"><span data-stu-id="eef43-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="eef43-110">Opciones Rollup y Grouping sets</span><span class="sxs-lookup"><span data-stu-id="eef43-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="eef43-111">Aquí, la opción más sencilla consiste en usar `UNION ALL` en su lugar para realizar la acumulación en lugar de depender de la sintaxis explícita.</span><span class="sxs-lookup"><span data-stu-id="eef43-111">The simplest option here is to use `UNION ALL` instead to perform the rollup rather than relying on the explicit syntax.</span></span> <span data-ttu-id="eef43-112">El resultado es exactamente el mismo</span><span class="sxs-lookup"><span data-stu-id="eef43-112">The result is exactly the same</span></span>

<span data-ttu-id="eef43-113">A continuación se muestra un ejemplo de una instrucción Group by mediante el uso de la opción `ROLLUP` :</span><span class="sxs-lookup"><span data-stu-id="eef43-113">Below is an example of a group by statement using the `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="eef43-114">Mediante el uso de ROLLUP hemos solicitado las agregaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="eef43-114">By using ROLLUP we have requested the following aggregations:</span></span>

* <span data-ttu-id="eef43-115">País y región</span><span class="sxs-lookup"><span data-stu-id="eef43-115">Country and Region</span></span>
* <span data-ttu-id="eef43-116">País</span><span class="sxs-lookup"><span data-stu-id="eef43-116">Country</span></span>
* <span data-ttu-id="eef43-117">Total general</span><span class="sxs-lookup"><span data-stu-id="eef43-117">Grand Total</span></span>

<span data-ttu-id="eef43-118">Para reemplazar esta operación, deberá usar `UNION ALL`y especificar las agregaciones necesarias explícitamente para devolver los mismos resultados:</span><span class="sxs-lookup"><span data-stu-id="eef43-118">To replace this you will need to use `UNION ALL`; specifying the aggregations required explicitly to return the same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="eef43-119">Para GROUPING SETS, todo lo que tenemos que hacer es adoptar la misma entidad de seguridad pero solo crear secciones UNION ALL para los niveles de agregación que queramos ver.</span><span class="sxs-lookup"><span data-stu-id="eef43-119">For GROUPING SETS all we need to do is adopt the same principal but only create UNION ALL sections for the aggregation levels we want to see</span></span>

## <a name="cube-options"></a><span data-ttu-id="eef43-120">Opciones de Cube</span><span class="sxs-lookup"><span data-stu-id="eef43-120">Cube options</span></span>
<span data-ttu-id="eef43-121">Es posible crear una cláusula GROUP BY WITH CUBE con el método UNION ALL.</span><span class="sxs-lookup"><span data-stu-id="eef43-121">It is possible to create a GROUP BY WITH CUBE using the UNION ALL approach.</span></span> <span data-ttu-id="eef43-122">El problema es que el código puede volverse rápidamente complicado y difícil de manejar.</span><span class="sxs-lookup"><span data-stu-id="eef43-122">The problem is that the code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="eef43-123">Para mitigar esta situación, puede usar este enfoque más avanzado.</span><span class="sxs-lookup"><span data-stu-id="eef43-123">To mitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="eef43-124">Vamos a usar el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="eef43-124">Let's use the example above.</span></span>

<span data-ttu-id="eef43-125">El primer paso es definir el 'cubo' que define todos los niveles de agregación que se van a crear.</span><span class="sxs-lookup"><span data-stu-id="eef43-125">The first step is to define the 'cube' that defines all the levels of aggregation that we want to create.</span></span> <span data-ttu-id="eef43-126">Es importante tomar nota de la cláusula CROSS JOIN de las dos tablas derivadas.</span><span class="sxs-lookup"><span data-stu-id="eef43-126">It is important to take note of the CROSS JOIN of the two derived tables.</span></span> <span data-ttu-id="eef43-127">De esta forma se nos generan todos los niveles.</span><span class="sxs-lookup"><span data-stu-id="eef43-127">This generates all the levels for us.</span></span> <span data-ttu-id="eef43-128">El resto del código está realmente ahí para dar formato.</span><span class="sxs-lookup"><span data-stu-id="eef43-128">The rest of the code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="eef43-129">Los resultados de CTAS pueden verse a continuación:</span><span class="sxs-lookup"><span data-stu-id="eef43-129">The results of the CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="eef43-130">El segundo paso es especificar una tabla de destino para almacenar los resultados temporales:</span><span class="sxs-lookup"><span data-stu-id="eef43-130">The second step is to specify a target table to store interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="eef43-131">El tercer paso es recorrer el cubo de columnas al realizar la agregación.</span><span class="sxs-lookup"><span data-stu-id="eef43-131">The third step is to loop over our cube of columns performing the aggregation.</span></span> <span data-ttu-id="eef43-132">La consulta se ejecuta una vez para cada fila de la tabla temporal #Cube y almacena los resultados en la tabla temporal #Results</span><span class="sxs-lookup"><span data-stu-id="eef43-132">The query will run once for every row in the #Cube temporary table and store the results in the #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="eef43-133">Por último, podemos devolver los resultados simplemente leyendo en la tabla temporal #Results</span><span class="sxs-lookup"><span data-stu-id="eef43-133">Lastly we can return the results by simply reading from the #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="eef43-134">Al dividir el código en secciones y generar una construcción de bucle, el código resulta más fácil de administrar y mantener.</span><span class="sxs-lookup"><span data-stu-id="eef43-134">By breaking the code up into sections and generating a looping construct the code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eef43-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eef43-135">Next steps</span></span>
<span data-ttu-id="eef43-136">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="eef43-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
