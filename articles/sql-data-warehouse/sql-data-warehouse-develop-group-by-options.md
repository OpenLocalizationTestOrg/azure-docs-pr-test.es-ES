---
title: "aaaGroup en Opciones en el almacén de datos de SQL | Documentos de Microsoft"
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
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="c5577-103">Opciones de Group by en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="c5577-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="c5577-104">Hola [GROUP BY] [ GROUP BY] se utiliza la cláusula tooaggregate tooa resumen conjunto de filas.</span><span class="sxs-lookup"><span data-stu-id="c5577-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="c5577-105">También tiene algunas opciones que extienden la funcionalidad del ese toobe necesidad solucionado no son compatibles directamente con almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c5577-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="c5577-106">Estas opciones son:</span><span class="sxs-lookup"><span data-stu-id="c5577-106">These options are</span></span>

* <span data-ttu-id="c5577-107">GROUP BY con ROLLUP</span><span class="sxs-lookup"><span data-stu-id="c5577-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="c5577-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="c5577-108">GROUPING SETS</span></span>
* <span data-ttu-id="c5577-109">GROUP BY con CUBE</span><span class="sxs-lookup"><span data-stu-id="c5577-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="c5577-110">Opciones Rollup y Grouping sets</span><span class="sxs-lookup"><span data-stu-id="c5577-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="c5577-111">Hola aquí la opción más sencilla es toouse `UNION ALL` en su lugar tooperform Hola rollup en lugar de depender de Hola sintaxis explícita.</span><span class="sxs-lookup"><span data-stu-id="c5577-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="c5577-112">resultado de Hello es exactamente Hola mismo</span><span class="sxs-lookup"><span data-stu-id="c5577-112">hello result is exactly hello same</span></span>

<span data-ttu-id="c5577-113">A continuación se muestra un ejemplo de un grupo por instrucción que usa hello `ROLLUP` opción:</span><span class="sxs-lookup"><span data-stu-id="c5577-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

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

<span data-ttu-id="c5577-114">Mediante el consolidado hemos solicitado Hola siguiendo las agregaciones:</span><span class="sxs-lookup"><span data-stu-id="c5577-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="c5577-115">País y región</span><span class="sxs-lookup"><span data-stu-id="c5577-115">Country and Region</span></span>
* <span data-ttu-id="c5577-116">País</span><span class="sxs-lookup"><span data-stu-id="c5577-116">Country</span></span>
* <span data-ttu-id="c5577-117">Total general</span><span class="sxs-lookup"><span data-stu-id="c5577-117">Grand Total</span></span>

<span data-ttu-id="c5577-118">tooreplace esto debe toouse `UNION ALL`; especificando las agregaciones de hello necesarias explícitamente tooreturn Hola los mismos resultados:</span><span class="sxs-lookup"><span data-stu-id="c5577-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

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

<span data-ttu-id="c5577-119">Para GROUPING SETS todo lo que necesitamos toodo es adoptar Hola mismo principal pero sólo puede crear secciones UNION ALL para hello niveles de agregación que deseamos toosee</span><span class="sxs-lookup"><span data-stu-id="c5577-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="c5577-120">Opciones de Cube</span><span class="sxs-lookup"><span data-stu-id="c5577-120">Cube options</span></span>
<span data-ttu-id="c5577-121">Es posible toocreate un GROUP BY WITH CUBE con el enfoque de UNION ALL de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5577-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="c5577-122">problema de Hello es que el código de hello puede volverse rápidamente complejo y difícil de manejar.</span><span class="sxs-lookup"><span data-stu-id="c5577-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="c5577-123">toomitigate esto ya puede utilizarla más avanzadas de enfoque.</span><span class="sxs-lookup"><span data-stu-id="c5577-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="c5577-124">Vamos a usar el ejemplo de Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="c5577-124">Let's use hello example above.</span></span>

<span data-ttu-id="c5577-125">Hola primer paso es toodefine hello 'cube' que define todos los niveles de Hola de agregación que deseamos toocreate.</span><span class="sxs-lookup"><span data-stu-id="c5577-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="c5577-126">Es importante tootake nota de hello CROSS JOIN de las dos tablas derivadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5577-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="c5577-127">Esto genera todos los niveles de Hola para nosotros.</span><span class="sxs-lookup"><span data-stu-id="c5577-127">This generates all hello levels for us.</span></span> <span data-ttu-id="c5577-128">resto de Hola de código de hello es realmente no existe para dar formato.</span><span class="sxs-lookup"><span data-stu-id="c5577-128">hello rest of hello code is really there for formatting.</span></span>

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

<span data-ttu-id="c5577-129">resultados de Hola de hello CTAS puede verse a continuación:</span><span class="sxs-lookup"><span data-stu-id="c5577-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="c5577-130">Hola segundo paso es toospecify da como resultado una versión preliminar toostore la tabla de destino:</span><span class="sxs-lookup"><span data-stu-id="c5577-130">hello second step is toospecify a target table toostore interim results:</span></span>

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

<span data-ttu-id="c5577-131">Hola tercer paso es tooloop sobre el cubo de columnas ejecutar Hola agregación.</span><span class="sxs-lookup"><span data-stu-id="c5577-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="c5577-132">consulta de Hola se ejecuta una vez para cada fila de tabla temporal de hello #Cube y almacenar resultados de hello en la tabla temporal de hello #Results</span><span class="sxs-lookup"><span data-stu-id="c5577-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

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

<span data-ttu-id="c5577-133">Por último, podemos devolvemos resultados Hola simplemente leyendo de tabla temporal de hello #Results</span><span class="sxs-lookup"><span data-stu-id="c5577-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="c5577-134">Interrumpa el código de hello en secciones y generando un bucle Hola de construcción código pasa a ser más fáciles de administrar y mantener.</span><span class="sxs-lookup"><span data-stu-id="c5577-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5577-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5577-135">Next steps</span></span>
<span data-ttu-id="c5577-136">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="c5577-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
