---
title: "aaaManaging estadísticas de las tablas en el almacén de datos de SQL | Documentos de Microsoft"
description: "Introducción a las estadísticas de tablas en Almacenamiento de datos SQL de Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a>Administración de estadísticas en tablas en Almacenamiento de datos SQL
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

Hello almacenamiento de datos de SQL más sepa sobre los datos, hello más rápido puede ejecutar consultas en los datos.  forma de Hola que proporcione almacenamiento de datos de SQL sobre los datos consiste en recopilar las estadísticas sobre los datos.  Cuentan con estadísticas en los datos es uno de los aspectos más importantes de hello puede hacer toooptimize las consultas.  Las estadísticas ayudan a almacenamiento de datos SQL crear Hola plan más óptimo para las consultas.  Esto es porque el optimizador de basados en consultas de almacenamiento de datos SQL de hello optimizador lleva un costo.  Es decir, compara el costo de Hola de varios planes de consulta y, a continuación, elige Hola plan con el costo más bajo de hello, que debe ser también plan de Hola que va a ejecutar hello más rápido.

Se pueden crear estadísticas de una sola columna, de varias columnas o de un índice de una tabla.  Las estadísticas se almacenan en un histograma que captura el intervalo de Hola y selectividad de valores.  Esto resulta de especial interés cuando el optimizador de hello necesita tooevaluate combinaciones, GROUP BY, HAVING y las cláusulas WHERE en una consulta.  Por ejemplo, si el optimizador de hello calcula que fecha Hola se va a filtrar en la consulta devolverá 1 fila, puede elegir un muy diferentes planificar que si se estimaciones que fecha han seleccionado se devuelven 1 millón de filas.  Mientras que la creación de estadísticas es muy importante, es igualmente importante que las estadísticas de *con precisión* reflejan Hola el estado actual de la tabla de Hola.  Cuentan con estadísticas actualizadas se asegura de que está seleccionado un buen plan optimizador Hola.  planes de Hello creados por el optimizador de hello solo son tan eficaces como las estadísticas de hello en los datos.

proceso de Hola de creación y actualización de estadísticas actualmente es un proceso manual, pero es muy sencillo toodo.  Esto es diferente de lo que sucede en SQL Server, que crea y actualiza automáticamente estadísticas de columnas únicas e índices.  Mediante el uso de información de Hola a continuación, en gran medida puede automatizar la administración de Hola de estadísticas de hello en los datos. 

## <a name="getting-started-with-statistics"></a>Introducción a las estadísticas
 Las estadísticas muestreadas en todas las columnas es una manera sencilla de tooget inició la creación con las estadísticas.  Puesto que es igualmente importante tookeep estadísticas actualizadas, un enfoque conservador puede ser las estadísticas de tooupdate diariamente o después de cada carga. Siempre hay ventajas y desventajas de rendimiento y Hola costo toocreate y actualice las estadísticas.  Si encuentra está tardando demasiado toomaintain todas las estadísticas, puede que desee tootry toobe más selectivo con respecto a las columnas que tienen estadísticas o las columnas que necesita una actualización frecuente.  Por ejemplo, conviene columnas de fecha tooupdate todos los días, tal y como se pueden agregar nuevos valores en lugar de después de cada carga. Una vez más, dispondrá de hello máximas ventajas por cuentan con estadísticas en las columnas que intervienen en las combinaciones, GROUP BY, HAVING y las cláusulas WHERE.  Si tiene una tabla con una gran cantidad de columnas que se utilizan únicamente en hello SELECT (cláusula), no pueden ayudar las estadísticas de estas columnas, y gastos un poco más tooidentify de esfuerzo solo las columnas de Hola que le ayudará las estadísticas, puede reducir Hola tiempo toomaintain las estadísticas .

## <a name="multi-column-statistics"></a>Estadísticas de varias columnas
Además toocreating estadísticas en columnas únicas, es posible que las consultas se beneficiarán de las estadísticas de varias columnas.  Las estadísticas de varias columnas son las estadísticas creadas en una lista de columnas.  Incluyen las estadísticas de columna única en la primera columna de hello en lista de hello, además de cierta información de correlación entre las columnas denominado densidades.  Por ejemplo, si tiene una tabla que combina tooanother en dos columnas, es posible que almacenamiento de datos SQL puede optimizar mejor plan de hello aunque entienda relación Hola entre dos columnas.   Las estadísticas de varias columnas pueden mejorar el rendimiento de las consultas en algunas operaciones, como las cláusulas compuestas JOINs y GROUP BY.

## <a name="updating-statistics"></a>Actualización de estadísticas
La actualización de estadísticas es una parte importante de la rutina de administración de base de datos.  Cuando se cambia la distribución de Hola de los datos en la base de datos de hello, las estadísticas deben toobe actualizado.  Las estadísticas obsoletas llevará rendimiento toosub óptimo de las consultas.

Una práctica recomendada es tooupdate estadísticas en columnas de fecha cada día a medida que se agregan nuevas fechas.  Cada fila nueva de tiempo se carga en el almacén de datos de Hola, se agregan nuevas fechas de carga o de transacción. Estos cambian la distribución de datos de Hola y hacer que las estadísticas de Hola quede obsoleto. Por el contrario, las estadísticas de una columna de país en una tabla de clientes nunca necesite toobe actualizado, como generalmente no cambia la distribución de Hola de valores. Suponiendo que la distribución de hello es constante entre los clientes, agregar nueva variación de tabla toohello de filas no va distribución de datos de toochange Hola. Sin embargo, si el almacenamiento de datos solo contiene un país y aparezca los datos de un nuevo país, resultante en datos procedentes de varios países va a almacenar, a continuación, definitivamente necesita tooupdate estadísticas en la columna de país de Hola.

Uno de hello primera preguntas tooask cuando está en la solución de problemas de una consulta, "son las estadísticas de hello actualizada?"

Esta pregunta no es uno que se puede responder por antigüedad de Hola de los datos de Hola. Un objeto de estadísticas toodate arriba podría ser muy antiguo si no ha habido ningún toohello cambio material datos subyacentes. Número de Hola de filas ha cambiado considerablemente cuando o hay un cambio material en la distribución de Hola de valores para una columna determinada *, a continuación,* es estadísticas de tiempo de tooupdate.  

Como referencia, **SQL Server** (no Almacenamiento de datos SQL) actualiza automáticamente las estadísticas para estas situaciones:

* Si tiene cero filas de tabla de hello, cuando se agregan filas, obtendrá una actualización automática de estadísticas
* Cuando se agrega la tabla de tooa más de 500 filas a partir de menos de 500 filas (por ejemplo, en el inicio tenga 499 y, a continuación, agregue 500 total de tooa de filas de 999 filas), obtendrá una actualización automática 
* Una vez que haya más de 500 filas tendrá tooadd 500 filas adicionales + 20% del tamaño de Hola de tabla Hola antes, verá una actualización automática de estadísticas de Hola

Puesto que no hay ningún toodetermine DMV si datos dentro de la tabla de hello ha cambiado desde que se actualizaron las estadísticas de tiempo de último hello, conocer la antigüedad de Hola de las estadísticas de puede proporcionar con parte de la imagen de Hola.  Puede usar Hola después toodetermine Hola última vez las estadísticas de consulta cuando se actualiza en cada tabla.  

> [!NOTE]
> Recuerde que si hay un cambio material en la distribución de Hola de valores para una columna determinada, deberá actualizar las estadísticas con independencia de hello última vez que se actualicen.  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

Las columnas de fecha en un almacenamiento de datos, por ejemplo, normalmente necesitan frecuentes actualizaciones de estadísticas. Cada fila nueva de tiempo se carga en el almacén de datos de Hola, se agregan nuevas fechas de carga o de transacción. Estos cambian la distribución de datos de Hola y hacer que las estadísticas de Hola quede obsoleto.  Por el contrario, las estadísticas de una columna de sexo en una tabla de clientes nunca necesite toobe actualizado. Suponiendo que la distribución de hello es constante entre los clientes, agregar nueva variación de tabla toohello de filas no va distribución de datos de toochange Hola. Sin embargo, si el almacenamiento de datos solo contiene un género y un nuevo requisito da como resultado varios géneros definitivamente deberá tooupdate estadísticas en la columna de género Hola.

Para obtener más información, consulte [Estadísticas][Statistics] en MSDN.

## <a name="implementing-statistics-management"></a>Implementación de administración de estadísticas
A menudo resulta una buena idea tooextend los datos de carga tooensure de proceso que las estadísticas se actualizan en Hola final de carga de Hola. carga de datos de Hello es cuando las tablas con más frecuencia cambian su tamaño o su distribución de valores. Por lo tanto, esto es un lugar lógico tooimplement algunos procesos de administración.

Algunos de los principios rectores se proporcionan a continuación para actualizar las estadísticas durante el proceso de carga de hello:

* Asegúrese de que cada tabla cargada tiene al menos un objeto de estadísticas actualizado. Este Hola actualizaciones tablas información de tamaño (recuento de filas y recuento de páginas) como parte de la actualización de estadísticas de Hola.
* Céntrese en las columnas que participan en las cláusulas JOIN, GROUP BY, ORDER BY y DISTINCT.
* Considere actualizar las fechas con más frecuencia como estos valores no se incluirán en el histograma de estadísticas de Hola "ascendente clave" columnas como transacción.
* Considere la posibilidad de actualizar columnas de distribución estática con menor frecuencia.
* Recuerde que cada objeto de estadística se actualiza en serie. Implementar solo `UPDATE STATISTICS <TABLE_NAME>` puede no ser recomendable, especialmente para las tablas amplias con muchos objetos de estadísticas.

> [!NOTE]
> Para obtener más detalles sobre [ascendente clave], consulte notas de modelo de estimación de cardinalidad toohello SQL Server 2014.
> 
> 

Para obtener más información, consulte [estimación de cardinalidad][Cardinality Estimation] en MSDN.

## <a name="examples-create-statistics"></a>Ejemplos: crear estadísticas
Estos ejemplos muestran cómo toouse distintas opciones de creación de estadísticas. Opciones de Hola que usas para cada columna dependen de características de Hola de los datos y cómo se usará la columna de hello en las consultas.

### <a name="a-create-single-column-statistics-with-default-options"></a>A. Crear estadísticas de columna única con las opciones predeterminadas
toocreate estadísticas en una columna, basta con proporcionar un nombre de objeto de estadísticas de Hola y Hola específicos de columna de Hola.

Esta sintaxis utiliza todas las opciones predeterminadas de Hola. De forma predeterminada, almacenamiento de datos SQL muestrea el 20 por ciento de la tabla de hello cuando crea estadísticas.

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

Por ejemplo:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a>B. Crear estadísticas de columna única mediante el examen de todas las filas
velocidad de muestreo predeterminada de Hello del 20 por ciento es suficiente para la mayoría de los casos. Sin embargo, puede ajustar la frecuencia de muestreo de Hola.

Hola toosample completa de la tabla, use esta sintaxis:

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

Por ejemplo:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a>C. Crear estadísticas de columna única mediante la especificación de tamaño de la muestra de Hola
Como alternativa, puede especificar el tamaño de la muestra de Hola como un porcentaje:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a>D. Crear estadísticas de columna única sólo en algunas filas de Hola
Otra opción, puede crear estadísticas en una parte de las filas de hello en la tabla. A esto se le denomina una estadística filtrada.

Por ejemplo, podría utilizar las estadísticas filtradas cuando planee tooquery una partición específica de una tabla con particiones grande. Mediante la creación de estadísticas en hello solo valores de la partición, precisión Hola de estadísticas de hello mejorará y, por lo tanto, mejorar el rendimiento de las consultas.

En este ejemplo se crean estadísticas sobre un intervalo de valores. Hola valores podrían fácilmente ser define el intervalo de hello toomatch de valores en una partición.

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> Para tooconsider de optimizador de consultas de hello utilizando las estadísticas filtradas cuando elige el plan de consulta distribuida de hello, consulta Hola debe ajustarse en definición de Hola Hola de objeto de estadísticas. Utilizando el ejemplo anterior hello, Hola la consulta donde cláusula necesita toospecify col1 valores entre 2000101 y 20001231.
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a>E. Crear estadísticas de columna única con todas las opciones de Hola
Por supuesto, puede combinar opciones Hola juntos. ejemplo de Hola siguiente crea un objeto de estadísticas filtradas con un tamaño de prueba personalizados:

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

Para hello referencia completa, consulte [CREATE STATISTICS] [ CREATE STATISTICS] en MSDN.

### <a name="f-create-multi-column-statistics"></a>F. Crear estadísticas de varias columnas
toocreate estadísticas de varias columnas, simplemente utilice los ejemplos anteriores de hello, pero especifique más columnas.

> [!NOTE]
> histograma con Hello, que se usa solo está disponible para hello primera columna aparece en la definición del objeto de estadísticas de hello tooestimate número de filas en el resultado de la consulta Hola.
> 
> 

En este ejemplo, se encuentra en el histograma de hello *producto\_categoría*. Las estadísticas entre columnas se calculan en *product\_category* y *product\_sub_c\ategory*:

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

Dado que no hay una correlación entre *producto\_categoría* y *producto\_sub\_categoría*, un estado de varias columna puede ser útil si se tiene acceso a estas columnas en hello mismo tiempo.

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a>G. Crear estadísticas en todas las columnas de hello en una tabla
Las estadísticas de una manera de toocreate son tooissues comandos CREATE STATISTICS después de crear la tabla de Hola.

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a>H. Usar una estadística de procedimiento almacenado toocreate en todas las columnas de una base de datos
Almacenamiento de datos SQL no tienen un equivalente de procedimiento almacenado de sistema también [] [sp_create_stats] en SQL Server. Este procedimiento almacenado crea un objeto de estadísticas de columna única en todas las columnas de base de datos de Hola que todavía no tiene estadísticas.

Esto le ayudará a empezar a trabajar con el diseño de la base de datos. Sentirse tooadapt libre debe tooyour.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

estadísticas de toocreate en todas las columnas de tabla de hello con este procedimiento, basta con llamar a procedimiento Hola.

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a>Ejemplos: actualizar estadísticas
estadísticas de tooupdate, hacer lo siguiente:

1. Actualizar un objeto de estadísticas. Especifique el nombre de Hola de hello las estadísticas del objeto que se va tooupdate.
2. Actualizar todos los objetos de estadísticas de una tabla. Especifique el nombre de Hola de tabla de hello en lugar de un objeto de estadísticas específicas.

### <a name="a-update-one-specific-statistics-object"></a>A. Actualizar un objeto de estadísticas específico
Usar hello siguiendo la sintaxis tooupdate un objeto concreto de estadísticas:

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

Por ejemplo:

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

Al actualizar los objetos de estadísticas específico, puede minimizar Hola tiempo y recursos necesarios toomanage las estadísticas. Para ello, sin embargo, algunos considerar toochoose Hola mejor estadísticas objetos tooupdate.

### <a name="b-update-all-statistics-on-a-table"></a>B. Actualizar todas las estadísticas de una tabla
Esto muestra un método sencillo para actualizar todos los objetos de estadísticas de hello en una tabla.

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

Por ejemplo:

```sql
UPDATE STATISTICS dbo.table1;
```

Esta instrucción resulta fácil toouse. Recuerde esto actualiza todas las estadísticas de la tabla de hello y, por lo tanto, puede realizar más trabajo que sean necesarios. Si el rendimiento de hello no es un problema, definitivamente es manera más sencilla y más completa de hello tooguarantee estadísticas están actualizadas.

> [!NOTE]
> Al actualizar todas las estadísticas de una tabla, almacenamiento de datos SQL realiza una tabla de hello toosample de examen para cada estadísticas. Si la tabla de hello es grande, tiene muchas columnas y muchas de las estadísticas, podría ser más eficaz tooupdate de estadísticas individuales según las necesidades del.
> 
> 

Para obtener una implementación de un `UPDATE STATISTICS` procedimiento vea hello [tablas temporales] [ Temporary] artículo. método de implementación de Hello es ligeramente diferente toohello `CREATE STATISTICS` procedimiento anterior pero el resultado final de hello es Hola igual.

Para consultar la sintaxis completa hello, consulte [Update Statistics] [ Update Statistics] en MSDN.

## <a name="statistics-metadata"></a>Metadatos de las estadísticas
Hay varias funciones que puede usar toofind información sobre las estadísticas y vista del sistema. Por ejemplo, puede ver si un objeto de estadísticas podría estar obsoleto mediante Hola estadísticas fecha función toosee cuando última se crea o se actualizaron las estadísticas.

### <a name="catalog-views-for-statistics"></a>Vistas de catálogo para las estadísticas
Estas vistas del sistema proporcionan información acerca de las estadísticas:

| Datos del catálogo | Descripción |
|:--- |:--- |
| [sys.columns][sys.columns] |Una fila por cada columna. |
| [sys.objects][sys.objects] |Una fila por cada objeto de base de datos de Hola. |
| [sys.schemas][sys.schemas] |Una fila por cada esquema de base de datos de Hola. |
| [sys.stats][sys.stats] |Una fila por cada objeto de estadísticas. |
| [sys.stats_columns][sys.stats_columns] |Una fila por cada columna de objeto de estadísticas de Hola. Vínculos volver toosys.columns. |
| [sys.tables][sys.tables] |Una fila por cada tabla (incluye tablas externas). |
| [sys.table_types][sys.table_types] |Una fila por cada tipo de datos. |

### <a name="system-functions-for-statistics"></a>Funciones del sistema para las estadísticas
Estas funciones del sistema son útiles para trabajar con las estadísticas:

| Función del sistema | Descripción |
|:--- |:--- |
| [STATS_DATE][STATS_DATE] |Date (objeto) estadísticas Hola se actualizó por última vez. |
| [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] |Proporciona información resumida de nivel y detallada acerca de la distribución de Hola de valores según lo entiende el objeto de estadísticas de Hola. |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a>Combinar funciones y columnas de estadísticas en una vista
Esta vista muestra las columnas que están relacionadas con toostatistics y resultados de la función de hello [STATS_DATE()] [] juntos.

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a>Ejemplos de DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() muestra datos Hola mantenidos dentro de un objeto de estadísticas. Estos datos se presentan en tres partes.

1. Encabezado
2. Vector de densidad
3. Histograma

Hola encabezado metadatos acerca de las estadísticas de Hola. Histograma Hello muestra la distribución de Hola de valores en la primera columna de clave Hola Hola de objeto de estadísticas. vector de densidad de Hello mide la correlación entre las columnas. SQLDW calcula las estimaciones de cardinalidad con cualquiera de los datos de Hola Hola objeto de estadísticas.

### <a name="show-header-density-and-histogram"></a>Mostrar el encabezado, la densidad y el histograma
Este ejemplo muestra las tres partes de un objeto de estadísticas.

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

Por ejemplo:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a>Mostrar una o varias partes de DBCC SHOW_STATISTICS();
Si solo está interesado en ver partes específicas, use hello `WITH` cláusula y especificar qué partes se desea toosee:

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

Por ejemplo:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a>Diferencias de DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() más estrictamente se implementa en tooSQL en comparación de almacenamiento de datos de SQL Server.

1. No se admiten características no documentadas.
2. No se puede usar Stats_stream.
3. No se pueden combinar resultados de subconjuntos específicos de datos de estadísticas, como por ejemplo (STAT_HEADER JOIN DENSITY_VECTOR).
4. No se puede establecer NO_INFOMSGS para la supresión de mensajes.
5. No se pueden usar corchetes alrededor de los nombres de las estadísticas.
6. No se puede usar objetos de estadísticas de tooidentify de nombres de columna
7. No se admite el error personalizado 2767.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, consulte [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] en MSDN.  toolearn más información, vea los artículos de hello en [información general de la tabla][Overview], [tipos de datos de tabla][Data Types], [distribuir una tabla] [ Distribute], [Indiza una tabla][Index], [creación de particiones de una tabla] [ Partition] y [ Tablas temporales][Temporary].  Para obtener más información sobre los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse de Azure][SQL Data Warehouse Best Practices].  

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

<!--MSDN references-->  
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
