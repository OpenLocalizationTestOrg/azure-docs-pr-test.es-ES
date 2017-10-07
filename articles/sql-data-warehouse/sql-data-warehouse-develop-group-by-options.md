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
# <a name="group-by-options-in-sql-data-warehouse"></a>Opciones de Group by en Almacenamiento de datos SQL
Hola [GROUP BY] [ GROUP BY] se utiliza la cláusula tooaggregate tooa resumen conjunto de filas. También tiene algunas opciones que extienden la funcionalidad del ese toobe necesidad solucionado no son compatibles directamente con almacenamiento de datos de SQL Azure.

Estas opciones son:

* GROUP BY con ROLLUP
* GROUPING SETS
* GROUP BY con CUBE

## <a name="rollup-and-grouping-sets-options"></a>Opciones Rollup y Grouping sets
Hola aquí la opción más sencilla es toouse `UNION ALL` en su lugar tooperform Hola rollup en lugar de depender de Hola sintaxis explícita. resultado de Hello es exactamente Hola mismo

A continuación se muestra un ejemplo de un grupo por instrucción que usa hello `ROLLUP` opción:

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

Mediante el consolidado hemos solicitado Hola siguiendo las agregaciones:

* País y región
* País
* Total general

tooreplace esto debe toouse `UNION ALL`; especificando las agregaciones de hello necesarias explícitamente tooreturn Hola los mismos resultados:

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

Para GROUPING SETS todo lo que necesitamos toodo es adoptar Hola mismo principal pero sólo puede crear secciones UNION ALL para hello niveles de agregación que deseamos toosee

## <a name="cube-options"></a>Opciones de Cube
Es posible toocreate un GROUP BY WITH CUBE con el enfoque de UNION ALL de Hola. problema de Hello es que el código de hello puede volverse rápidamente complejo y difícil de manejar. toomitigate esto ya puede utilizarla más avanzadas de enfoque.

Vamos a usar el ejemplo de Hola anterior.

Hola primer paso es toodefine hello 'cube' que define todos los niveles de Hola de agregación que deseamos toocreate. Es importante tootake nota de hello CROSS JOIN de las dos tablas derivadas de Hola. Esto genera todos los niveles de Hola para nosotros. resto de Hola de código de hello es realmente no existe para dar formato.

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

resultados de Hola de hello CTAS puede verse a continuación:

![][1]

Hola segundo paso es toospecify da como resultado una versión preliminar toostore la tabla de destino:

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

Hola tercer paso es tooloop sobre el cubo de columnas ejecutar Hola agregación. consulta de Hola se ejecuta una vez para cada fila de tabla temporal de hello #Cube y almacenar resultados de hello en la tabla temporal de hello #Results

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

Por último, podemos devolvemos resultados Hola simplemente leyendo de tabla temporal de hello #Results

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

Interrumpa el código de hello en secciones y generando un bucle Hola de construcción código pasa a ser más fáciles de administrar y mantener.

## <a name="next-steps"></a>Pasos siguientes
Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
