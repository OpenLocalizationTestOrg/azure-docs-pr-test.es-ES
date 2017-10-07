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
# <a name="optimizing-transactions-for-sql-data-warehouse"></a>Optimización de transacciones para Almacenamiento de datos SQL
Este artículo explica cómo toooptimize Hola rendimiento del código transaccional al minimizar el riesgo de reversión largo.

## <a name="transactions-and-logging"></a>Transacciones y registro
Las transacciones son un componente importante de un motor de base de datos relacional. Almacenamiento de datos SQL usa transacciones durante la modificación de los datos. Estas transacciones pueden ser explícitas o implícitas. Las instrucciones `INSERT`, `UPDATE` y `DELETE` son ejemplos de transacciones implícitas. Las transacciones explícitas se escriben explícitamente por un desarrollador que utiliza `BEGIN TRAN`, `COMMIT TRAN` o `ROLLBACK TRAN` y se usan normalmente cuando varias instrucciones de modificación necesitan toobe unido entre sí en una unidad atómica única. 

Almacenamiento de datos de SQL Azure confirma la base de datos de cambios toohello mediante registros de transacciones. Cada distribución tiene su propio registro de transacciones. Las escrituras en el registro de transacciones son automáticas. No es necesario realizar ninguna configuración. Sin embargo, mientras que este proceso garantiza la escritura de hello agrega una sobrecarga en el sistema de Hola. Para minimizar este impacto, puede escribir código transaccionalmente eficiente. De forma amplia, un código transaccionalmente eficiente pertenece en dos categorías.

* Aproveche las construcciones con registro mínimo, siempre que sea posible.
* Procesamiento de datos con ámbito singular de lotes tooavoid transacciones de larga ejecución
* Adoptar un modelo para tooa grandes modificaciones dada la partición de conmutación de particiones

## <a name="minimal-vs-full-logging"></a>Registro mínimo frente a registro completo
A diferencia de las operaciones de registro completo, que usan Hola transacciones registro tookeep realizar un seguimiento de cada cambio en la fila, realizar un seguimiento de las operaciones registradas al mínimo las asignaciones de extensiones y solo los cambios de metadatos. Por lo tanto, el registro mínimo implica registrar únicamente la información de Hola que sea necesario toorollback Hola transacciones en caso de hello de un error o una solicitud explícita (`ROLLBACK TRAN`). Como mucho menos se realiza un seguimiento de información de registro de transacciones de hello, una operación registrada al mínimo se comporta mejor que una operación completamente registrada dimensiones similares. Además, dado que escribe menos dejan de registro de transacciones de hello, se genera una menor cantidad de datos de registro y por lo que es más i/OS eficaz.

límites de seguridad de transacciones de Hello solo aplican operaciones toofully iniciado.

> [!NOTE]
> Las operaciones con registro mínimo pueden participar en transacciones explícitas. Tal y como se realiza el seguimiento de todos los cambios en las estructuras de asignación, es posible tooroll back mínimamente las operaciones registradas. Es importante toounderstand que el cambio de hello es "mínimo" optimizado no se ha iniciado sin.
> 
> 

## <a name="minimally-logged-operations"></a>Operaciones con registro mínimo
Hello operaciones siguientes son capaces de que se va a registrar mínimamente:

* CREATE TABLE AS SELECT ([CTAS][CTAS])
* INSERT..SELECT
* CREATE INDEX
* ALTER INDEX REBUILD
* DROP INDEX
* TRUNCATE TABLE
* DROP TABLE
* ALTER TABLE SWITCH PARTITION

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> Las operaciones de movimiento de datos internos (como `BROADCAST` y `SHUFFLE`) no se ven afectadas por el límite de seguridad de transacciones de Hola.
> 
> 

## <a name="minimal-logging-with-bulk-load"></a>Registro mínimo con carga masiva
`CTAS` y `INSERT...SELECT` son operaciones de carga masiva. Sin embargo, ambas se ven afectadas por la definición de tabla de destino de Hola y dependen de escenario de carga de Hola. A continuación se muestra una tabla que explica si la operación masiva tendrá un registro completo o mínimo:  

| Índice principal | Escenario de carga | Modo de registro |
| --- | --- | --- |
| Montón |Cualquiera |**Mínimo** |
| Índice agrupado |Tabla de destino vacía |**Mínimo** |
| Índice agrupado |Las filas cargadas no se superponen a páginas existentes en el destino |**Mínimo** |
| Índice agrupado |Las filas cargadas se superponen a páginas existentes en el destino |Completo |
| Índice de almacén de columnas agrupado |Tamaño del lote > = 102.400 por cada distribución con particiones alineadas |**Mínimo** |
| Índice de almacén de columnas agrupado |Tamaño del lote < = 102.400 por cada distribución con particiones alineadas |Completo |

Merece la pena indicar que todas las escrituras tooupdate secundaria o no clúster índices siempre estará totalmente las operaciones registran.

> [!IMPORTANT]
> Almacenamiento de datos SQL tiene 60 distribuciones. Por lo tanto, suponiendo que todas las filas se distribuyen uniformemente y de inicio en una sola partición, el lote deberá toocontain 6,144,000 filas o toobe mayor mínimamente registrados al escribir tooa Clustered Columnstore Index. Si tiene particiones tabla hello y filas de Hola que se insertan abarcan límites de la partición, deberá 6,144,000 filas por límite de la partición suponiendo que incluso la distribución de datos. Cada partición de cada distribución independientemente debe sobrepasan el umbral de fila 102.400 de Hola para hello insert toobe mínimamente en distribución Hola.
> 
> 

A menudo, la carga de datos en una tabla no vacía con un índice agrupado puede contener una mezcla de filas con registro completo y filas con registro mínimo. Un índice agrupado es un árbol equilibrado (árbol B) de las páginas. Si se escribe página hello tooalready contiene filas de otra transacción, a continuación, estas escrituras totalmente registrarán. Sin embargo, si Hola página está vacía, a continuación, página de toothat de escritura de hello mínimamente registrará.

## <a name="optimizing-deletes"></a>Optimización de eliminaciones
`DELETE` es una operación con registro completo.  Si necesita toodelete una gran cantidad de datos en una tabla o una partición, resulta más conveniente demasiado`SELECT` datos Hola desea tookeep, que se puede ejecutar como una operación registrada al mínimo.  tooaccomplish esto, cree una nueva tabla con [CTAS][CTAS].  Una vez creado, use [cambiar el nombre de] [ RENAME] tooswap fuera de la tabla anterior con la tabla de hello recién creado.

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

## <a name="optimizing-updates"></a>Optimización de actualizaciones
`UPDATE` es una operación con registro completo.  Si necesita tooupdate un gran número de filas de una tabla o una partición suele ser mucho más eficaz toouse una operación registrada al mínimo como [CTAS] [ CTAS] toodo para.

Hola ejemplo a continuación de una actualización de tabla completa ha sido convertido tooa `CTAS` para que el registro mínimo es posible.

En este caso retrospectivamente estamos agregando una venta de toohello de importe de descuento en la tabla de hello:

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
> Volver a crear tablas de gran tamaño puede beneficiarse del uso de las características de administración de cargas de trabajo de Almacenamiento de datos SQL. Para obtener más detalles, consulte la sección de administración de cargas de trabajo de toohello en hello [simultaneidad] [ concurrency] artículo.
> 
> 

## <a name="optimizing-with-partition-switching"></a>Optimización con modificación de particiones
Cuando se enfrenta a modificaciones a gran escala dentro de una [partición de tabla][table partition], un patrón de modificación de particiones constituye un buen enfoque. Si hello modificación de datos es importante e intervalos logra varias particiones, a continuación, recorrer simplemente particiones Hola Hola mismo resultado.

Hola pasos tooperform un cambio de partición son los siguientes:

1. Crear una partición vacía de salida
2. Realizar actualización' hello' como un CTAS
3. Hola toohello existente de datos tabla de desactivación
4. Intercambiar datos nuevos de Hola
5. Limpiar los datos de Hola

Sin embargo, toohelp identificar Hola particiones tooswitch primero necesitamos toobuild un procedimiento auxiliar como Hola uno a continuación. 

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

Este procedimiento maximiza la reutilización de código y mantiene modificación más compacta del ejemplo de la partición de Hola.

código de Hello siguiente muestra cinco pasos de hello mencionadas anteriormente tooachieve una rutina de modificación de la partición completa.

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

## <a name="minimize-logging-with-small-batches"></a>Minimización del registro con lotes pequeños
Para las operaciones de modificación de datos de gran tamaño, puede tener sentido toodivide Hola el funcionamiento en unidad de hello tooscope fragmentos o lotes de trabajo.

A continuación, se proporciona un ejemplo de trabajo. se ha establecido el tamaño del lote de Hello tooa trivial técnica número toohighlight Hola. En realidad, el tamaño del lote de Hola sería mucho mayor. 

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

## <a name="pause-and-scaling-guidance"></a>Instrucciones de operaciones de pausa y escalado
Almacenamiento de datos SQL de Azure permite pausar, reanudar y escalar su almacenamiento de datos a petición. Al pausar o escalar el almacenamiento de datos de SQL es toounderstand importante que las transacciones en curso terminan inmediatamente; haciendo que las transacciones abiertas toobe revierte. Si la carga de trabajo había emitido una larga ejecución y la modificación de datos incompletos anterior toohello pausa u operación de escala, este trabajo será necesario toobe deshacer. Esto puede afectar a Hola tarda toopause o escalar la base de datos de almacenamiento de datos de SQL Azure. 

> [!IMPORTANT]
> `UPDATE` y `DELETE` son operaciones con registro completo y, por tanto, estas operaciones de deshacer y rehacer pueden tardar bastante más que las operaciones con registro mínimo equivalentes. 
> 
> 

escenario "mejor" Hello es toolet en vuelo datos modificación transacciones completa anterior toopausing o escala almacenamiento de datos de SQL. Sin embargo, esto no siempre es posible. riesgo de hello toomitigate de una reversión largo, considere la posibilidad de una de las siguientes opciones de hello:

* Vuelva a escribir las operaciones de ejecución prolongada con [CTAS][CTAS].
* Operación de Hola se dividen en fragmentos; operar en un subconjunto de filas de Hola

## <a name="next-steps"></a>Pasos siguientes
Vea [las transacciones en el almacén de datos de SQL] [ Transactions in SQL Data Warehouse] toolearn más información acerca de los niveles de aislamiento y límites transaccionales.  Para obtener información general de otros procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse Best Practices].

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

