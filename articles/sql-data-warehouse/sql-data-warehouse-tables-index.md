---
title: "tablas de aaaIndexing en el almacén de datos de SQL | Microsoft Azure"
description: "Introducción a la indexación de tablas en Almacenamiento de datos SQL de Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2016
ms.author: shigu;barbkess
ms.openlocfilehash: e614d63c8fb871f2ba388f14576cf9f282d4b818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-tables-in-sql-data-warehouse"></a>Indexación de tablas en Almacenamiento de datos SQL
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

Almacenamiento de datos SQL ofrece varias opciones de indexación, entre las que se incluyen [índices de almacén de columnas][clustered columnstore indexes] e [índices agrupados y no agrupados descritos][clustered indexes and nonclustered indexes].  Además, también no ofrece una opción sin índice, que también se conoce como [montón][heap].  En este artículo se trata las ventajas de Hola de cada tipo de índice, así como sugerencias toogetting Hola máximo rendimiento de los índices. Vea [tabla sintaxis de create] [ create table syntax] para obtener información más detallada acerca de cómo toocreate una tabla en el almacén de datos de SQL.

## <a name="clustered-columnstore-indexes"></a>Índices de almacén de columnas en clúster
De forma predeterminada, Almacenamiento de datos SQL crea un índice de almacén de columnas en clúster cuando se especifican opciones sin índice en una tabla. Las tablas de almacén de columnas agrupado ofrecen ambos nivel más alto de Hola de compresión de datos, así como mejor rendimiento de consulta general Hola.  Tablas de almacén de columnas agrupado por lo general superan las tablas agrupadas de índice o montón y normalmente son Hola mejor opción para las tablas grandes.  Por estas razones, almacén de columnas agrupado es Hola mejor lugar toostart cuando no está seguro de cómo tooindex la tabla.  

toocreate una tabla de almacén de columnas agrupado, simplemente especifique el índice agrupado de almacén de columnas en la cláusula WITH de Hola o deje desactivada la cláusula WITH de hello:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

Hay algunos escenarios en los que un almacén de columnas en clúster puede que no sea una buena opción:

* Las tablas de almacén de columnas no admiten varchar (max), nvarchar (max) y varbinary (max).  Considere la posibilidad de usar un índice agrupado o de montón en su lugar.
* Las tablas de almacén de columnas pueden que sean menos eficientes para datos transitorios.  Considere la posibilidad de usar tablas de montón, e incluso tablas temporales.
* Tablas pequeñas con menos de 100 millones de filas.  Considere la posibilidad de usar tablas de montón.

## <a name="heap-tables"></a>Tablas de montón
Cuando temporalmente aterrizaje datos en almacenamiento de datos de SQL, es posible que el uso de una tabla de montón hará que Hola proceso general con mayor rapidez.  Esto es porque tooheaps cargas son más rápidas que las tablas de tooindex y en algunos Hola casos posteriores de lectura pueden realizarse desde la memoria caché.  Si va a cargar datos toostage solo antes de ejecutar transformaciones más, cargar Hola tabla tooheap tabla será mucho más rápido que cargar Hola datos tooa en el clúster de tabla de almacén de columnas. Además, cargar datos tooa [tabla temporal] [ Temporary] también cargará mucho más rápido que cargar un almacenamiento de tabla toopermanent.  

Para tablas de búsqueda pequeñas, con menos de 100 millones de filas, a menudo tiene sentido usar tablas de montón.  Tablas de almacén de columnas clúster comienzan tooachieve óptimo compresión cuando hay más de 100 millones de filas.

toocreate una tabla de montón, simplemente especifique MONTÓN en la cláusula WITH de hello:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a>Índices clúster y no clúster
Índices agrupados pueden superan las tablas de almacén de columnas agrupado cuando una sola fila necesita toobe recuperar rápidamente.  Para las consultas donde una sola o muy pocos búsqueda fila es necesario tooperformance con una velocidad de extremo, considere la posibilidad de un índice clúster o no clúster índice secundario.  Hola desventaja toousing un índice clúster es que solo las consultas que utilizan un filtro muy selectivo en la columna de índice agrupado de Hola se beneficiarán.  filtro tooimprove en otras columnas de que un índice no clúster puede ser agrega columnas tooother.  Sin embargo, cada índice que se agrega la tabla tooa agregará espacio y tooloads de tiempo de procesamiento.

toocreate una tabla de índice agrupado, simplemente especifique el índice clúster en la cláusula WITH de hello:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

tooadd un índice no agrupado en una tabla, basta con usar hello según la sintaxis:

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>Optimización de índices de almacén de columnas en clúster
Las tablas de almacén de columnas en clúster organizan los datos en segmentos.  De gran calidad alta segmento es el rendimiento óptimo de las consultas de tooachieving críticos en una tabla de almacén de columnas.  Calidad de segmento se puede medir por número de Hola de filas de un grupo de filas comprimido.  Calidad de segmento es más adecuado que hay al menos 100K filas por fila comprimida agruparán y obtienen un rendimiento como número de Hola de filas por fila Agrupar enfoque 1.048.576 filas, que es Hola la mayoría de las filas que puede contener un grupo de filas.

Hola debajo de vista se pueden crear y usar en su Hola de toocompute sistema promedio filas por cada fila, agrupar e identificar los índices de almacén de columnas clúster deficiente.  última columna de Hello en esta vista generará como instrucción SQL que puede ser usado toorebuild los índices.

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

Ahora que ha creado la vista de hello, ejecute esta consulta tooidentify tablas con grupos de filas con menos de 100 KB filas.  Por supuesto, puede que desee tooincrease umbral de Hola de 100 KB si desea obtener más calidad óptima de segmento. 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

Tras ejecutar consulta de Hola puede empezar toolook datos hello y analizar los resultados. Esta tabla explica qué toolook para en el análisis de grupo de filas.

| Columna | ¿Cómo toouse estos datos |
| --- | --- |
| [table_partition_count] |Si Hola tabla tiene particiones, puede esperar a que toosee recuentos de grupo de filas abierto superior. En teoría, cada partición de distribución de hello podría tener un grupo de filas abierto asociado con él. Incluir esto en el análisis. Una tabla pequeña que se han particionado podría optimizarse mediante la eliminación de hello particiones completamente como esto podría mejorar la compresión. |
| [row_count_total] |Número total de filas de tabla de Hola. Por ejemplo, puede utilizar este porcentaje toocalculate del valor de filas en estado de hello comprimido. |
| [row_count_per_distribution_MAX] |Si todas las filas se distribuyen uniformemente este valor sería el número de destino de Hola de filas por la distribución. Compare este valor con compressed_rowgroup_count Hola. |
| [COMPRESSED_rowgroup_rows] |Número total de filas en formato de almacén de columnas para la tabla de Hola. |
| [COMPRESSED_rowgroup_rows_AVG] |Si promedio de Hola de filas es mucho # inferior hello máximo de filas para un grupo de filas, a continuación, considere el uso CTAS o ALTER INDEX REBUILD toorecompress Hola datos |
| [COMPRESSED_rowgroup_count] |Número de grupos de filas en formato de almacén de columnas. Si este número es muy alta en la tabla de relaciones toohello es un indicador que densidad de almacén de columnas de hello es baja. |
| [COMPRESSED_rowgroup_rows_DELETED] |Las filas se eliminan lógicamente en formato de almacén de columnas. Si el número de hello es alta tamaño tootable relativo, considere la posibilidad de volver a crear particiones de Hola o volver a generar índice hello, ya que esto quita físicamente. |
| [COMPRESSED_rowgroup_rows_MIN] |Úselo junto con hello promedio y máximo columnas toounderstand Hola intervalo de valores para los grupos de filas de hello en el almacén de columnas. Un número bajo por encima del umbral de carga de hello (102.400 por la distribución de particiones alineadas) sugiere que las optimizaciones están disponibles en la carga de datos de Hola |
| [COMPRESSED_rowgroup_rows_MAX] |Mismo caso anterior. |
| [OPEN_rowgroup_count] |Los grupos de filas abiertos son normales. Cabe esperar un grupo de filas OPEN por cada distribución de tabla (60). Cantidades excesivas sugieren carga de datos entre particiones. Hola doble comprobación estrategia toomake seguro es sonido de creación de particiones |
| [OPEN_rowgroup_rows] |Cada grupo de filas puede incluir un máximo de 1 048 576 filas. Utilice esta cantidad de espacio libre de toosee de valor están grupos de filas abierto de Hola |
| [OPEN_rowgroup_rows_MIN] |Abrir grupos indican que datos están que se va a generación cargado en la tabla de Hola o que Hola esparcido por las filas restantes en este grupo de filas de carga anterior. Hola use MIN, MAX, AVG columnas toosee es SAT. la cantidad de datos en grupos de filas abierto. ¡Para tablas pequeñas podría ser 100% de todos los datos de Hola! En cuyo caso ALTER INDEX REBUILD tooforce Hola toocolumnstore de datos. |
| [OPEN_rowgroup_rows_MAX] |Mismo caso anterior. |
| [OPEN_rowgroup_rows_AVG] |Mismo caso anterior. |
| [CLOSED_rowgroup_rows] |Mire Hola cerrado fila Agrupar filas como una comprobación de integridad. |
| [CLOSED_rowgroup_count] |Hola de grupos de filas cerrados debe ser bajo si alguno se ven en absoluto. Los grupos de filas cerrados pueden ser convertido toocompressed rowg rupos mediante Hola ALTER INDEX... REORGANISE. Pero esto no suele ser necesario. Cerrado son grupos de fila toocolumnstore convertido automáticamente por proceso "tupla motriz" en segundo plano Hola. |
| [CLOSED_rowgroup_rows_MIN] |Los grupos de filas cerrados deben tener una velocidad de relleno muy alta. Si la tasa de relleno de Hola para un grupo de filas cerrados es bajo, un análisis más profundo de almacén de columnas de hello es necesario. |
| [CLOSED_rowgroup_rows_MAX] |Mismo caso anterior. |
| [CLOSED_rowgroup_rows_AVG] |Mismo caso anterior. |
| [Rebuild_Index_SQL] |Índice de almacén de columnas toorebuild SQL para una tabla |

## <a name="causes-of-poor-columnstore-index-quality"></a>Causas de una calidad deficiente del índice de almacén de columnas
Si ha identificado las tablas con calidad de segmento deficiente, le interesará causa raíz de tooidentify Hola.  A continuación se muestran otras causas comunes de baja calidad de los segmentos:

1. Presión de la memoria cuando se generó el índice
2. Gran volumen de operaciones de DML
3. Operaciones de carga pequeña o lenta
4. Demasiadas particiones

Estos factores pueden provocar un toohave de índice de almacén de columnas, significativamente menor que Hola óptimo 1 millón de filas por grupo de filas.  También pueden hacer que grupo de filas de filas toogo toohello delta en lugar de un grupo de filas comprimido. 

### <a name="memory-pressure-when-index-was-built"></a>Presión de la memoria cuando se generó el índice
número de Hola de filas por grupo de filas comprimidos es toohello directamente relacionada con el ancho de fila de Hola y Hola cantidad de memoria disponibles tooprocess Hola grupo de filas.  Cuando las filas se escriben toocolumnstore tablas bajo presión de memoria, puede sufrir calidad de segmento de almacén de columnas.  Por lo tanto, se recomienda hello es sesión de hello toogive que está escribiendo tablas de índice de almacén de columnas tooyour acceso tooas cantidad de memoria como sea posible.  Puesto que hay un equilibrio entre la memoria y la simultaneidad, instrucciones de hello en hello derecho memoria asignación depende de los datos de hello en cada fila de la tabla, la cantidad de Hola de unidad asignó los tooyour sistema y cantidad de Hola de simultaneidad ranuras disponibles pueden dar toohello sesión que está escribiendo la tabla de datos tooyour.  Como práctica recomendada, se recomienda empezar con xlargerc si usas DW300 o menos, largerc si utilizas DW400 tooDW600 y mediumrc si usas DW1000 y versiones posteriores.

### <a name="high-volume-of-dml-operations"></a>Gran volumen de operaciones de DML
Un gran volumen de operaciones de DML que actualizar y eliminar filas puede introducir ineficacia en el almacén de columnas de Hola. Esto es especialmente cierto si se modifica la mayoría de Hola de filas de hello en un grupo de filas.

* Al eliminar una fila de un grupo de filas comprimido lógicamente solo marca la fila de hello como eliminadas. fila de Hello permanece en grupo de filas comprimidos de hello hasta que se vuelve a generar Hola partición o tabla.
* Insertar una fila agrega una tabla de almacén de filas interno Hola fila tootooan llamada a un grupo de filas delta. fila de Hello insertado no está convertido toocolumnstore hasta que el grupo de filas delta Hola está lleno y se marca como cerradas. Grupos de filas se cierran una vez que llegan a su capacidad máxima Hola de 1.048.576 filas. 
* La actualización de una fila en formato de almacén de columnas se procesa como eliminación lógica y luego como inserción. fila de Hello insertado puede almacenarse en el almacén delta de Hola.

Actualización por lotes y las operaciones que sobrepasan el umbral de forma masiva Hola de 102.400 filas por partición alineada distribución se escribirá directamente el formato de almacén de columnas toohello de inserción. Sin embargo, si consideramos que una distribución uniforme, necesitaría toobe modificar más de un 6.144 millones de filas en una sola operación para este toooccur. Si número Hola de filas de una partición determinada alineada distribución es menos de 102.400 filas Hola irán almacén delta de toohello y permanecerán allí hasta que se han insertado filas suficientes o se ha vuelto a generar índice de Hola o grupo de la fila del hello tooclose modificado.

### <a name="small-or-trickle-load-operations"></a>Operaciones de carga pequeña o lenta
Las cargas pequeñas que fluyen al Almacenamiento de datos SQL también se denominan cargas lentas. Suelen representa un flujo constante están cercano de los datos que se va a ingestión sistema Hola. Sin embargo, como esta secuencia está cerca de volumen de hello continua de filas no es especialmente grande. Más a menudo de no datos hello son significativamente inferior al umbral de hello necesario para un formato de toocolumnstore carga directa.

En estas situaciones, es a menudo mejores datos de hello tooland primero en el almacenamiento de blobs de Azure y dejar que se acumulan tooloading anterior. A menudo, esta técnica se conoce como *procesamiento por microlotes*.

### <a name="too-many-partitions"></a>Demasiadas particiones
Tooconsider de otra cosa es impacto Hola de creación de particiones en las tablas de almacén de columnas agrupado.  Antes de crear particiones, Almacenamiento de datos SQL ya divide los datos en 60 bases de datos.  La creación de particiones divide aún más los datos.  Si dividir los datos, le interesará tooconsider que **cada** partición requerirá al menos 1 millón de toohave toobenefit de filas de un índice de almacén de columnas agrupado.  Si dividir la tabla en 100 particiones, la tabla deberá toohave al menos 6 millones toobenefit de filas de un índice de almacén de columnas agrupado (60 distribuciones * 100 particiones * 1 millón de filas). Si la tabla de 100 particiones no tiene 6 millones de filas, reduzca el número de Hola de particiones o considere la posibilidad de usar una tabla de montón en su lugar.

Una vez que se han cargado las tablas con datos, siga hello debajo tooidentify de pasos y vuelva a crear tablas con índices de almacén de columnas clúster deficiente.

## <a name="rebuilding-indexes-tooimprove-segment-quality"></a>Calidad de segmento de recompilar índices tooimprove
### <a name="step-1-identify-or-create-user-which-uses-hello-right-resource-class"></a>Paso 1: Identifique o cree el usuario que utiliza la clase de recurso correcto de hello
Una forma rápida de tooimmediately mejorar la calidad del segmento es el índice de Hola de toorebuild.  Hola SQL devuelto por Hola por encima de la vista devolverá una instrucción ALTER INDEX REBUILD, que puede ser usado toorebuild los índices.  Al volver a generar los índices, asegúrese de asignar suficiente sesión toohello de memoria que se volverá a generar el índice.  toodo, clase de recurso de Hola de aumento de un usuario que tiene permisos toorebuild Hola un índice en esta tabla toohello requisitos mínimos.  no se puede cambiar la clase de recurso de Hello de usuario de propietario de base de datos de hello, por lo que si no ha creado un usuario en el sistema de hello, necesitará toodo por lo que primero.  mínimo de Hello que recomendamos es xlargerc si usas DW300 o menos, largerc si utilizas DW400 tooDW600 y mediumrc si usas DW1000 y versiones posteriores.

A continuación se muestra un ejemplo de cómo tooallocate más tooa de usuario de la memoria mediante el aumento de su clase de recurso.  Para obtener más información acerca de las clases de recursos y cómo toocreate un nuevo usuario puede encontrarse en hello [administración de simultaneidad y la carga de trabajo] [ Concurrency] artículo.

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>Paso 2: volver a generar índices de almacén de columnas en clúster con un usuario con una clase de recurso mayor
Inicie sesión como Hola usuario del paso 1 (por ejemplo, LoadUser), que ahora está utilizando una clase de recurso superior y ejecutar instrucciones ALTER INDEX de Hola.  Asegúrese de que este usuario tiene tablas de toohello de permisos ALTER donde se regenera el índice de Hola.  Estos ejemplos muestran cómo toorebuild Hola índice de almacén de columnas completo o cómo toorebuild una sola partición. En las tablas grandes, resulta más prácticos índices toorebuild una sola partición a la vez.

O bien, en lugar de volver a generar índice hello, podría copiar Hola tabla tooa nueva tabla mediante [CTAS][CTAS].  ¿De qué manera es mejor? En el caso de grandes volúmenes de datos, [CTAS][CTAS] suele ser más rápido que [ALTER INDEX][ALTER INDEX]. Para volúmenes menores de datos, [ALTER INDEX] [ ALTER INDEX] es toouse más fácil y no requiere tooswap tabla Hola.  Vea **volver a generar índices con CTAS y modificación de particiones** a continuación para obtener más detalles sobre cómo se indiza toorebuild con CTAS.

```sql
-- Rebuild hello entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

La regeneración de un índice en Almacenamiento de datos SQL es una operación que se realiza sin conexión.  Para obtener más información sobre la reconstrucción de índices, vea Hola sección ALTER INDEX REBUILD [desfragmentación de índices de almacén de columnas] [ Columnstore Indexes Defragmentation] y el tema de la sintaxis de hello [ALTER INDEX] [ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>Paso 3: comprobar que ha mejorado la calidad de los segmentos de almacén de columnas en clúster
Consulta de Hola de vuelva a ejecutar que identifica la tabla con mala calidad de segmento y comprobar que ha mejorado la calidad de segmento.  Si no mejora la calidad de segmento, podría deberse a que las filas de hello en la tabla son más amplia.  Considere el uso de una clase de recurso superior o de DWU al volver a generar los índices.

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>Regeneración de índices con CTAS y conmutación de particiones
Este ejemplo se utiliza [CTAS] [ CTAS] y modificación toorebuild una partición de tabla de particiones. 

```sql
-- Step 1: Select hello partition of data and write it out tooa new table using CTAS
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT hello data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 too [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN hello rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 too [dbo].[FactInternetSales] PARTITION 2;
```

Para obtener más información acerca de cómo volver a crear las particiones que usan `CTAS`, vea hello [partición] [ Partition] artículo.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información, vea los artículos de hello en [información general de la tabla][Overview], [tipos de datos de tabla][Data Types], [distribuir una tabla] [ Distribute], [Creación de particiones de una tabla][Partition], [mantener las estadísticas de tabla] [ Statistics] y [ Tablas temporales][Temporary].  toolearn más información acerca de los procedimientos recomendados, consulte [prácticas recomendadas de almacenamiento de datos de SQL][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[ALTER INDEX]: https://msdn.microsoft.com/library/ms188388.aspx
[heap]: https://msdn.microsoft.com/library/hh213609.aspx
[clustered indexes and nonclustered indexes]: https://msdn.microsoft.com/library/ms190457.aspx
[create table syntax]: https://msdn.microsoft.com/library/mt203953.aspx
[Columnstore Indexes Defragmentation]: https://msdn.microsoft.com/library/dn935013.aspx#Anchor_1
[clustered columnstore indexes]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
