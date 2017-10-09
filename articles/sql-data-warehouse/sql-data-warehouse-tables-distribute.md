---
title: "tablas de aaaDistributing en el almacén de datos de SQL | Documentos de Microsoft"
description: "Introducción a la distribución de tablas en Almacenamiento de datos SQL de Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a>Distribución de tablas en Almacenamiento de datos SQL
> [!div class="op_single_selector"]
> * [Información general][Overview]
> * [Tipos de datos][Data Types]
> * [Distribución][Distribute]
> * [Índice][Index]
> * [Partición][Partition]
> * [Estadísticas][Statistics]
> * [Temporal][Temporary]
>
>

El Almacenamiento de datos SQL es un sistema de base de datos distribuidas de procesamiento masivo en paralelo (MPP).  Al dividir los datos y la funcionalidad de procesamiento entre varios nodos, Almacenamiento de datos SQL puede ofrecer una gran escalabilidad, mucha más que cualquier sistema individual.  Decidir cómo toodistribute sus datos en el almacenamiento de datos de SQL están uno de los más importantes de hello factores tooachieving un rendimiento óptimo.   rendimiento de Hello toooptimal clave es la minimización de movimiento de datos y a su vez el movimiento de datos de clave toominimizing hello es seleccionando estrategia de distribución adecuada de Hola.

## <a name="understanding-data-movement"></a>Descripción del movimiento de datos
En un sistema MPP, datos de saludo de cada tabla se dividen entre varias bases de datos subyacentes.  las consultas de Hello más optimizado en un sistema MPP simplemente se pueden pasar a través de tooexecute Hola individuales bases de datos distribuidas sin interacción entre Hola otras bases de datos.  Por ejemplo, supongamos que tiene una base de datos con datos de ventas que contiene dos tablas, ventas y clientes.  Si tiene una consulta que necesite toojoin la tabla de clientes de tooyour de tabla de ventas y divide tanto los sales y las tablas de cliente de por número de cliente, colocar a cada cliente en una base de datos independiente, las consultas que unir ventas y el cliente se pueden resolver dentro de cada uno base de datos con ningún conocimiento de Hola a otras bases de datos.  En cambio, si divide los datos de ventas por número de pedido y los datos de clientes por número de cliente, a continuación, una base de datos no tendrá datos correspondientes de Hola para cada cliente y, por tanto, si deseara toojoin los datos de clientes de tooyour de datos de ventas, necesitará tooget Hola datos para cada cliente de hello otras bases de datos.  En este segundo ejemplo, el movimiento de datos necesitaría toooccur toomove Hola cliente datos toohello datos de ventas, para que se pueden combinar Hola dos tablas.  

Movimiento de datos no es algo malo, a veces resulta necesario toosolve una consulta.  Pero si se puede evitar este paso adicional, evidentemente la consulta se ejecutará más rápido.  El movimiento de los datos surge normalmente cuando se unen tablas o se realizan agregaciones.  En muchos casos deberá toodo ambos, por lo que aunque es posible que pueda toooptimize para un escenario, como una combinación, que todavía necesita toohelp de movimiento de datos puede resolver para Hola otro escenario, como una agregación.  El truco de Hello es pensar en que es menos trabajo.  En la mayoría de los casos, distribuir grandes tablas de hechos en una columna frecuentemente combinada es Hola método más eficaz para reducir hello más movimiento de datos.  Distribución de los datos en columnas de combinación es un movimiento de datos de tooreduce método mucho más habitual de distribución de los datos en las columnas que intervienen en una agregación.

## <a name="select-distribution-method"></a>Selección del método de distribución
Entre bastidores de hello, almacenamiento de datos SQL divide los datos en bases de datos de 60.  Cada base de datos es que se hace referencia tooas una **distribución**.  Cuando se cargan datos en cada tabla, almacenamiento de datos de SQL tiene tooknow cómo toodivide los datos a través de las distribuciones de 60.  

método de distribución de Hello se define en el nivel de tabla de Hola y actualmente hay dos opciones:

1. **Round Robin** , que distribuye los datos de manera uniforme, pero aleatoria.
2. **Distribuido por hash** , que distribuye datos en función de los valores de hash de una sola columna

De forma predeterminada, si no se define un método de distribución de datos, la tabla se distribuirán mediante hello **round-robin** método de distribución.  Sin embargo, se vuelven más sofisticadas en su implementación, deberá usar tooconsider **hash distribuida** toominimize el movimiento de datos que a su vez optimizará el rendimiento de las consultas de tablas.

### <a name="round-robin-tables"></a>Tablas Round Robin
Uso de hello método Round Robin de distribución de datos es demasiado cómo suena.  Medida que se cargan los datos, cada fila se envía simplemente toohello siguiente distribución.  Este método de distribución de los datos de hello siempre distribuirá aleatoriamente datos Hola muy uniformemente entre todas las distribuciones de Hola.  No es decir, no existe ninguna ordenación done durante Hola round robin proceso que coloca los datos.  Una distribución round robin a veces se denomina hash aleatorio por este motivo.  Con una tabla distribuida round robin no hay ningún dato de hello toounderstand necesidad.  Por este motivo, las tablas Round Robin suelen ser buenos objetivos para la carga.

De forma predeterminada, si no se selecciona ningún método de distribución, hello método de distribución de round robin se usará.  Sin embargo, mientras que las tablas de operación por turnos son toouse fácil, porque se distribuyen al azar en sistema Hola significa que el sistema de hello no puede garantizar qué distribución cada fila tiene en.  Como consecuencia, sistema de Hola a veces es necesario tooinvoke una toobetter de operación de movimiento de datos organizar los datos antes de que puede resolver una consulta.  Este paso adicional puede ralentizar las consultas.

Considere el uso de distribución de operación por turnos para la tabla en hello los escenarios siguientes:

* Cuando se empieza como un punto de partida sencillo.
* Si no hay ninguna clave de combinación obvia.
* Si no hay columna buena candidata para distribuir tabla Hola de hash
* Si hello tabla no comparte una clave de combinación común con otras tablas
* Si la combinación de hello es tan importante como otras combinaciones de consulta de Hola
* Cuando la tabla de hello es una tabla de ensayo temporal

Ambos ejemplos crearán una tabla Round Robin:

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> Mientras round-robin es el tipo de tabla de hello predeterminado es explícito en el DDL se considera una práctica recomendada para que las intenciones de Hola de su diseño de la tabla estén tooothers desactive.
>
>

### <a name="hash-distributed-tables"></a>Tablas con distribución por hash
Con un **Hash distribuida** algoritmo toodistribute las tablas pueden mejorar el rendimiento de muchos escenarios reduciendo el movimiento de datos en tiempo de consulta.  Hash distribuidas tablas son tablas que se dividen entre Hola distribuye las bases de datos usando un algoritmo hash en una sola columna que seleccionó.  columna de distribución de Hello es lo que determina cómo datos Hola se dividen en las bases de datos distribuidas.  función de hash de Hello usa Hola distribución columna tooassign filas toodistributions.  Hola algoritmo hash y la distribución resultante es determinista.  Es decir Hola mismo valor con hello al mismo tipo de datos usarán tiene toohello misma distribución.    

En este ejemplo se creará una tabla distribuida en id.:

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a>Selección de la columna de distribución
Cuando eliges demasiado**distribuir hash** una tabla, deberá tooselect una columna de distribución individuales.  Al seleccionar una columna de distribución, hay tres tooconsider de los factores más importantes.  

Seleccione una sola columna que:

1. No se actualizará
2. Distribuirá los datos uniformemente, con lo que se evita la asimetría de datos
3. Reducirá el movimiento de datos

### <a name="select-distribution-column-which-will-not-be-updated"></a>Selección de una columna de distribución que no se actualizará
Las columnas de distribución no se pueden actualizar; por lo tanto, seleccione una columna con valores estáticos.  Si una columna tendrá toobe actualizado, por lo general no resulta un candidato bueno de distribución.  Si hay un caso donde debe actualizar una columna de distribución, puede hacerlo eliminando primero fila hello y, a continuación, insertar una fila nueva.

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a>Selección de una columna que distribuirá los datos de manera uniforme
Ya que un sistema distribuido realiza solo tan rápido como su distribución más lenta, es importante toodivide Hola trabajo uniformemente a través de las distribuciones de hello en orden tooachieve equilibrada ejecución todo sistema Hola.  forma de Hola Hola trabajo se divide en un sistema distribuido se basa en donde residen los datos de Hola para cada distribución.  Esto facilita columna de distribución adecuada de hello tooselect muy importante para distribuir los datos de Hola para que cada distribución tiene trabajo igual y se toman Hola mismo toocomplete tiempo su parte del trabajo de Hola.  Cuando también se divide el trabajo en todo el sistema de Hola, datos Hola se equilibra entre las distribuciones de Hola.  Cuando los datos no están equilibrados de manera uniforme, se conoce como **asimetría de datos**.  

datos toodivide uniformemente y evitar el sesgo de datos, considere la siguiente Hola al seleccionar la columna de distribución:

1. Seleccione una columna que contenga un importante número de valores distintos.
2. Evite la distribución de los datos en las columnas con unos pocos valores distintivos.
3. Evite la distribución de los datos en las columnas con una alta frecuencia de valores NULL.
4. Evite la distribución de datos en columnas de fecha.

Dado que cada valor es too1 con hash de 60 distribuciones, distribución uniforme tooachieve le interesará tooselect una columna que es muy único y contiene más de 60 valores únicos.  tooillustrate, considere un caso donde una columna solamente tiene 40 valores únicos.  Si se ha seleccionado esta columna como clave de distribución de hello, datos de Hola para esa tabla llegaría en 40 distribuciones a lo sumo, dejando 20 distribuciones con ningún dato y no toodo de procesamiento.  Por el contrario, hello otras 40 distribuciones tendría más toodo de trabajo que, si hello datos se distribuye uniformemente las distribuciones de más de 60.  Este escenario es un ejemplo de la asimetría de datos.

En el sistema MPP, cada paso de consulta espera toocomplete de todas las distribuciones su cuota de trabajo de Hola.  Si está realizando más trabajo que Hola otros distribución, Hola recursos de hello otras distribuciones que básicamente se pierde esperando en distribución ocupado Hola.  Si el trabajo no se distribuye de manera uniforme en todas las distribuciones, se denomina una **asimetría de procesamiento**.  Sesgo de procesamiento provocará toorun de las consultas más lenta que si carga de trabajo de hello puede se distribuyen uniformemente entre las distribuciones de Hola.  Sesgo de datos dará lugar tooprocessing sesgado.

Evitar la distribución en la columna admite valores NULL alta como valores null de hello todos llegará a Hola mismo distribución. Distribuir en una columna de fecha puede hacer procesamiento sesgo porque todos los datos de una fecha específica llegará a Hola mismo distribución. Si varios usuarios ejecutan filtradas todas las consultas en hello misma fecha, a continuación, solo 1 de 60 distribuciones de Hola a realizar todo el trabajo de hello como una fecha determinada sólo estará en una distribución. En este escenario, las consultas de hello es probable que se ejecutarán 60 veces más lentas que si datos Hola se distribuye equitativamente sobre todas las distribuciones de Hola.

Cuando no existe ninguna columna de buena candidata, considere la posibilidad de usar round robin como método de distribución de hello.

### <a name="select-distribution-column-which-will-minimize-data-movement"></a>Selección de una columna de distribución que minimizará el movimiento de datos
Minimizar el movimiento de datos mediante la selección de columna de distribución adecuada de Hola es una de las estrategias más importantes de Hola para optimizar el rendimiento de su almacén de datos de SQL.  El movimiento de los datos surge normalmente cuando se unen tablas o se realizan agregaciones.  Las columnas usadas en las cláusulas `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` y `HAVING` son todas **buenas** candidatas para la distribución por hash.

Hola en otra parte, las columnas de hello `WHERE` cláusula realice **no** realizar para los candidatos de la columna de hash correcto porque limitar que las distribuciones participan en la consulta de hello, que produce el procesamiento de sesgado.  Un buen ejemplo de una columna que podría ser tentador toodistribute en, pero a menudo puede causar este procesamiento sesgo es una columna de fecha.

Por lo general, si tiene dos tablas de hechos de gran tamaño suelen incluirse en una combinación, dispondrá de hello máximo rendimiento mediante la distribución de ambas tablas en una de las columnas de combinación de Hola.  Si tiene una tabla que nunca se tooanother Unidos a un tabla de hechos de gran tamaño, a continuación, busque toocolumns que son a menudo en hello `GROUP BY` cláusula.

Hay unos criterios clave que deben ser tooavoid cumpla el movimiento de datos durante una combinación:

1. Hello tablas involucradas en la combinación de hello deben ser hash distribuida en **una** de columnas de Hola que participan en la combinación de Hola.
2. tipos de datos de Hola Hola de columnas de combinación deben coincidir entre las dos tablas.
3. columnas de Hello deben combinarse con un operador es igual a.
4. Hello tipo de combinación no sea un `CROSS JOIN`.

## <a name="troubleshooting-data-skew"></a>Solución de problemas de asimetría de datos
Cuando los datos de la tabla se distribuyen mediante el método de distribución de hash de hello hay una posibilidad de que algunas distribuciones será sesgado toohave desproporcionadamente más datos que otras personas. Exceso sesgo de datos pueden afectar al rendimiento de consulta dado resultado final de Hola de una consulta distribuida debe esperar a que toofinish de distribución de ejecución más larga de Hola. Lo dependiendo de grado de Hola de datos de hello sesgo que tendrá que tooaddress.

### <a name="identifying-skew"></a>Identificación de la asimetría
Un tooidentify de forma sencilla una tabla como sesgado es toouse `DBCC PDW_SHOWSPACEUSED`.  Se trata de una forma muy rápida y sencilla toosee Hola número de filas de tabla que se almacenan en cada una de las distribuciones de hello 60 de la base de datos.  Recuerde que para obtener un rendimiento más equilibrada de hello, filas de hello en la tabla distribuida se deben distribuir uniformemente en todas las distribuciones de Hola.

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Sin embargo, si consulta las vistas de administración dinámica de almacenamiento de datos de SQL Azure hello (DMV) puede realizar un análisis más detallado.  toostart, crear vista de hello [dbo.vTableSizes] [ dbo.vTableSizes] ver con Hola SQL desde [información general de la tabla] [ Overview] artículo.  Una vez que se crea la vista de hello, ejecute este tooidentify consulta las tablas que tienen más de sesgo de datos de 10%.

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a>Resolución de la asimetría de datos
No todos los sesgado es suficiente toowarrant una corrección.  En algunos casos, rendimiento de Hola de una tabla en algunas consultas puede sobrepasar daños Hola de sesgo de datos.  toodecide si debe resolver los datos de sesgo en una tabla, debe comprender tanto como sea posible sobre los volúmenes de datos de Hola y consultas en la carga de trabajo.   Toolook unidireccional en el impacto de Hola de sesgo es toouse pasos Hola Hola [consulta supervisión] [ Query Monitoring] artículo impacto de hello toomonitor de sesgo en el rendimiento de las consultas y específicamente Hola consultas largas toohow de impacto Tome toocomplete distribuciones individuales Hola.

Distribución de los datos consiste en buscar el equilibrio adecuado de hello entre reducir al mínimo el sesgo de datos y minimizar el movimiento de datos. Estos pueden ser opuestas objetivos y a veces es conveniente tookeep datos sesgo en el movimiento de datos de tooreduce de orden. Por ejemplo, cuando Hola distribución columna es con frecuencia Hola compartida de combinaciones y agregaciones, se puede minimizar movimiento de datos. Hello ventaja de tener el movimiento de datos mínima Hola puede contrarrestar impacto de Hola de contar con datos de sesgo.

forma habitual de Hello sesgo de datos de tooresolve es toore-crear tabla de hello con una columna de distribución diferente. Dado que no hay ninguna manera de columna de distribución de hello toochange en otra distribución de tablas, Hola forma toochange Hola de una tabla se toorecreate con un [] [CTAS].  Estos son dos ejemplos de cómo resolver la asimetría de datos:

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a>Ejemplo 1: Volver a crear la tabla de hello con una nueva columna de distribución
Este ejemplo utiliza [CTAS] [] toore-crear una tabla con una columna de distribución de hash diferente.

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a>Ejemplo 2: Volver a crear la tabla Hola usando la distribución de operación por turnos
Este ejemplo utiliza [CTAS] [] toore-crear una tabla con operación por turnos en lugar de una distribución de hash. Este cambio producirá la distribución de datos incluso en el costo de Hola de movimiento de datos mayor.

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca del diseño de tabla, vea hello [distribuir][Distribute], [índice][Index], [partición] [ Partition], [Tipos de datos][Data Types], [estadísticas] [ Statistics] y [tablas temporales] [ Temporary] artículos.

Para acceder a información general sobre los procedimientos recomendados, vea [Procedimientos recomendados para SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
