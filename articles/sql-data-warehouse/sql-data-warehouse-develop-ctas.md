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
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>Create Table As Select (CTAS) en Almacenamiento de datos SQL
Crear tabla como select o `CTAS` es uno de hello más importantes características de T-SQL disponibles. Es una operación de ejecución en paralelo totalmente que crea una nueva tabla en función de la salida de hello de una instrucción SELECT. `CTAS`es una copia de una tabla de hello toocreate de forma más sencilla y rápida. Este documento incluye ejemplos y procedimientos recomendados para `CTAS`.

## <a name="selectinto-vs-ctas"></a>SELECT..INTO frente a CTAS
Puede considerar `CTAS` como una versión muy cargada de `SELECT..INTO`.

Aquí tiene un ejemplo de una instrucción `SELECT..INTO` sencilla:

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

En el ejemplo de Hola anterior `[dbo].[FactInternetSales_new]` se crearán como tabla distribuida de ROUND_ROBIN con un índice de almacén de columnas en clúster en el se trata de valores predeterminados de la tabla de hello en el almacén de datos de SQL Azure.

`SELECT..INTO`Sin embargo no podrá toochange cualquier índice hello, distribución, método o hello escribe como parte de la operación de Hola. Aquí es donde `CTAS` entra en juego.

tooconvert Hola anteriormente demasiado`CTAS` es bastante sencilla:

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

Con `CTAS` es capaz de toochange ambos Hola distribución de datos de la tabla de hello, así como el tipo de tabla Hola. 

> [!NOTE]
> Si solo está tratando de índice de hello toochange en su `CTAS` hello y operación de tabla de origen es hash distribuida la `CTAS` llevará a cabo operación mejor si mantiene Hola el mismo tipo de columna y los datos de distribución. Esto evitará cross movimiento de datos de distribución durante la operación de Hola que es más eficaz.
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>Usar CTAS toocopy una tabla
Quizás uno de hello más comunes usos del `CTAS` es crear una copia de una tabla para que pueda cambiar Hola DDL. Si por ejemplo creó originalmente la tabla como `ROUND_ROBIN` y ahora desea cambiarla tooa tabla distribuida en una columna, `CTAS` es ¿cómo cambiaría la columna de distribución de Hola. `CTAS`También puede ser usado toochange tipos de particiones, la indización o la columna.

Supongamos que creó esta tabla utilizando el tipo de distribución de hello predeterminado de `ROUND_ROBIN` distribuidas porque se especificó ninguna columna de distribución en hello `CREATE TABLE`.

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

Ahora desea toocreate una nueva copia de esta tabla con un índice de almacén de columnas agrupado por lo que puede aprovechar las ventajas de rendimiento de Hola de tablas de almacén de columnas clúster. También puede toodistribute esta tabla en ProductKey desde que se anticipan combinaciones en esta columna y desea que el movimiento de datos tooavoid durante las combinaciones en ProductKey. Por último también es conveniente tooadd creación de particiones en OrderDateKey para que pueda eliminar rápidamente los datos antiguos colocando particiones antiguas. Aquí es instrucción CTAS de Hola que copiaría la tabla anterior en una nueva tabla.

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

Por último, puede cambiar el nombre de su tooswap de tablas en la nueva tabla y, a continuación, elimine la tabla anterior.

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas.  En orden tooget Hola un mejor rendimiento de las consultas, es importante que las estadísticas se crean en todas las columnas de todas las tablas después de la primera carga de Hola o se producen cambios sustanciales en datos Hola.  Para obtener una explicación detallada de las estadísticas, vea hello [estadísticas] [ Statistics] tema en el grupo de desarrollo de Hola de temas.
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>Usar toowork CTAS según las características no admitidas
`CTAS`También se puede ser usado toowork alrededor de un número de características no admitida de Hola enumeradas a continuación. Esto puede a menudo demostrar toobe una situación favorece como no solo el código serán compatible, pero a menudo se ejecutará más rápido en almacenamiento de datos de SQL. El motivo es su diseño completamente en paralelo. Algunas situaciones que se pueden solucionar con CTAS incluyen:

* ANSI JOINS en UPDATE
* ANSI JOINS en DELETE
* Instrucción MERGE

> [!NOTE]
> Intente toothink "CTAS primera". Si cree que puede resolver un problema mediante `CTAS` , a continuación, que suele ser tooapproach de manera mejor de hello, incluso si se escribe como resultado más datos.
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>Sustitución de una combinación ANSI en instrucciones update
Es posible que tener una actualización compleja que combina más de dos tablas juntos mediante unión hello tooperform de sintaxis de ANSI UPDATE o DELETE.

Imagine que había tooupdate esta tabla:

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

consulta de Hello original podría han consultado algo parecido a esto:

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

Puesto que el almacenamiento de datos SQL no es compatible con ANSI combinaciones en hello `FROM` cláusula de una `UPDATE` (instrucción), no se puede copiar este código a través sin cambiar ligeramente.

Puede usar una combinación de un `CTAS` y un modo implícito unir tooreplace este código:

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

## <a name="ansi-join-replacement-for-delete-statements"></a>Sustitución de una combinación ANSI en instrucciones delete
A veces mejor método para eliminar datos de hello es toouse `CTAS`. En lugar de eliminar datos de hello basta con seleccionar datos de Hola que desee tookeep. Este especialmente cierto para `DELETE` las instrucciones que utilizan ansi unir sintaxis puesto que el almacenamiento de datos SQL no admite combinaciones ANSI en hello `FROM` cláusula de una `DELETE` instrucción.

A continuación se muestra un ejemplo de una instrucción DELETE convertida:

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

## <a name="replace-merge-statements"></a>Sustitución de instrucciones MERGE
Las instrucciones merge se pueden sustituir, al menos en parte, mediante el uso de `CTAS`. Es posible consolidar hello `INSERT` hello y `UPDATE` en una única instrucción. Los registros eliminados necesitaría toobe cerrado en una segunda instrucción.

Un ejemplo de un `UPSERT` está disponible a continuación:

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

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>Recomendación de CTAS: establezca explícitamente el tipo de datos y la nulabilidad de salida
Al migrar código, podría encontrarse ejecutando este tipo modelo de codificación:

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

Instintivamente que piense debería migrar este tooa código CTAS y se correcto. Sin embargo, hay un problema oculto aquí.

Hello siguiente código no produce Hola el mismo resultado:

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

Tenga en cuenta que Hola columna "resultado" traslada los valores de tipo y la nulabilidad de datos Hola de expresión de Hola. Esto puede provocar toosubtle varianzas en valores si no tiene cuidado.

Intente Hola siguiente como ejemplo:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

valor de Hello almacenado para el resultado es diferente. Dado que el valor almacenado en la columna de resultados de Hola Hola se utiliza una en otro error Hola de expresiones se convierte en incluso más significativo.

![][1]

Esto es especialmente importante para las migraciones de datos. Aunque la segunda consulta de hello es sin duda más precisa, hay un problema. datos de Hello sería toohello en comparación con otro sistema de origen y conduce tooquestions de integridad en migración Hola. Este es uno de los pocos casos donde la respuesta "incorrecto" hello es realmente Hola derecha.

Hello motivo vemos esta disparidad entre los resultados de hello dos está inactivo tooimplicit conversión de tipos. Hola primera tabla de ejemplo Hola define la definición de columna de Hola. Cuando se inserta la fila de Hola se realiza una conversión de tipos implícita. En el segundo ejemplo de Hola no hay ninguna conversión de tipos implícita como expresión de hello define el tipo de datos de columna de Hola. Tenga en cuenta que también esa columna hello en el segundo ejemplo de Hola se ha definido como una columna que acepta valores NULL, mientras que en el primer ejemplo de Hola no tiene. Cuando se crea la tabla de hello en hello primer ejemplo nulabilidad en las columnas se define explícitamente. En el segundo ejemplo de Hola simplemente quedó toohello expresión y de forma predeterminada, esto se creará en una definición de NULL.  

tooresolve estos aspectos que debe establecer explícitamente la conversión de tipos de Hola y la nulabilidad en hello `SELECT` parte de hello `CTAS` instrucción. No se puede establecer estas propiedades en hello crear elemento de tabla.

ejemplo de Hola siguiente muestra cómo toofix Hola código:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Tenga en cuenta los siguiente hello:

* Se podría haber usado CAST o CONVERT.
* ISNULL es tooforce usado nulabilidad no COALESCE
* ISNULL es la función más externo Hola
* Hola segunda parte del programa Hola ISNULL es una constante, es decir, 0

> [!NOTE]
> Para hello nulabilidad toobe establece correctamente es vital toouse `ISNULL` y no `COALESCE`. `COALESCE`no es una función determinista y así Hola será resultado de expresión Hola siempre acepta valores NULL. `ISNULL` es diferente. Es determinista. Por lo tanto, cuando Hola segunda parte del programa Hola `ISNULL` función es una constante o un literal, a continuación, el valor resultante hello no NULL.
> 
> 

Esta sugerencia no es sólo es útil para garantizar la integridad de Hola de los cálculos. También es importante para la modificación de particiones de tabla. Imagine que tiene esta tabla definida como hecho:

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

Sin embargo, el campo de valor de Hola es una expresión calculada no es parte de los datos de origen de Hola.

toocreate el conjunto de datos con particiones puede toodo esto:

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

consulta de Hello llevarían a cabo perfectamente correcto. problema de Hello aparece cuando intenta tooperform cambio de partición de Hola. las definiciones de tabla de Hello no coinciden. definiciones de tabla toomake Hola encontrar Hola que ctas necesita toobe modificado.

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

Por lo tanto, puede ver que la coherencia de los tipos y el mantenimiento de las propiedades de nulabilidad en CTAS es una buena práctica de ingeniería. Le ayuda a toomaintain de integridad en los cálculos y también garantiza que la modificación de particiones es posible.

Consulte tooMSDN para obtener más información sobre el uso de [CTAS][CTAS]. Es una de las instrucciones de más importantes de hello en el almacén de datos de SQL Azure. Asegúrese de que la comprende perfectamente.

## <a name="next-steps"></a>Pasos siguientes
Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
