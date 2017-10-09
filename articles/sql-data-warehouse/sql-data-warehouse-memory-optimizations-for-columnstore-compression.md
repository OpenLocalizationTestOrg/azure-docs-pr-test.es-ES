---
title: "rendimiento del índice de almacén de columnas aaaImprove en SQL Azure | Documentos de Microsoft"
description: "Reduzca los requisitos de memoria o aumentar Hola memoria disponible toomaximize Hola número de filas de que un índice de almacén de columnas comprime en cada grupo de filas."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>Maximización de la calidad del grupo de filas del almacén de columnas

Calidad de un grupo de filas se determina mediante el número de filas de un grupo de filas Hola. Reduzca los requisitos de memoria o aumentar Hola memoria disponible toomaximize Hola número de filas de que un índice de almacén de columnas comprime en cada grupo de filas.  Use las tasas de compresión de métodos tooimprove y rendimiento de las consultas para los índices de almacén de columnas.

## <a name="why-hello-rowgroup-size-matters"></a>¿Por qué es importante el tamaño del grupo de filas de Hola
Puesto que un índice de almacén recorre una tabla mediante el análisis de segmentos de columna de grupos de filas individuales, maximizar el número de Hola de filas de cada grupo de filas mejora el rendimiento de las consultas. Cuando los grupos de filas tienen un gran número de filas, la compresión de datos mejora lo que significa que hay menos tooread datos desde el disco.

Para obtener más información sobre los grupos de filas, consulte [Guía de índices de almacén de columnas](https://msdn.microsoft.com/library/gg492088.aspx).

## <a name="target-size-for-rowgroups"></a>Tamaño objetivo de los grupos de filas
Para obtener el mejor rendimiento de consulta, objetivo de hello es número de hello toomaximize de filas por grupo en un índice de almacén. Un grupo de filas puede tener un máximo de 1.048.576 filas. Su correcto toonot tiene número máximo de Hola de filas por grupo. Los índices de almacén de columnas logran un buen rendimiento cuando los grupos de filas cuentan con al menos 100.000 filas.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>Los grupos de filas pueden recortarse durante la compresión

Durante una regeneración de índice masiva carga o almacén de columnas, en ocasiones, no hay suficiente toocompress disponibles de memoria que todos Hola filas designados para cada grupo de filas. Cuando hay presión de memoria, índices de almacén de columnas recortan tamaños de grupo de filas de Hola para que compresión de almacén de columnas de Hola se realice correctamente. 

Cuando hay filas de toocompress al menos 10 000 no hay memoria suficiente en cada grupo de filas, almacenamiento de datos de SQL genera un error.

Para obtener más información sobre la carga masiva, consulte [Carga de datos en un índice de almacén de columnas agrupado](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).

## <a name="how-toomonitor-rowgroup-quality"></a>La calidad de un grupo de filas toomonitor

Hay una DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) que expone información útil, como el número de filas de la razón de hello y grupos de filas de recorte si se recorta no existe. Puede crear Hola después de la vista como una forma práctica tooquery esta información de tooget DMV de recorte de un grupo de filas.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

Hola trim_reason_desc indica si el grupo de filas de Hola se recorta (trim_reason_desc = NO_TRIM implica no hubo ningún recorte y grupo de filas es de calidad óptima). Hello razones recorte siguientes indican prematura recorte del grupo de filas de hello:
- Carga masiva: Ello recorte se utiliza al lote entrante de Hola de filas de carga de hello tenía menor que 1 millón de filas. motor de Hello creará grupos de filas comprimido si hay más de 100.000 filas insertadas (como tooinserting lugar en el almacén delta de hello) pero conjuntos Hola tooBULKLOAD motivo recorte. En este escenario, considere la posibilidad de aumentar su tooaccumulate de ventana de carga de lote más filas. Además, vuelva a evaluar su tooensure de esquema de partición no es demasiado específico, como grupos de filas no pueden abarcar los límites de partición.
- MEMORY_LIMITATION: motor de hello requiere toocreate grupos de filas con 1 millón de filas, una determinada cantidad de memoria de trabajo. Cuando la Hola cargar sesión de memoria disponible es menor que Hola necesaria de memoria de trabajo, prematuramente obtengan recuperan grupos de filas. Hola las secciones siguientes explica cómo tooestimate memoria necesaria y asignar más memoria.
- DICTIONARY_SIZE: este motivo de recorte indica que el recorte del grupo de filas se ha producido porque había al menos una columna de cadena con cadenas de cardinalidad anchas o altas. el tamaño del diccionario Hello es limitado too16 MB de memoria y una vez que se alcanza este límite grupo de filas de Hola se comprime. Si ejecuta esta situación, considere la posibilidad de aislar columna problemático hello en una tabla independiente.

## <a name="how-tooestimate-memory-requirements"></a>¿Cómo tooestimate requisitos de memoria

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

Hola máximo memoria necesaria toocompress un grupo de filas es aproximadamente

- 72 MB +
- \#filas \*\#columnas \* 8 bytes +
- \#filas \*\#columnas de cadena corta \* 32 bytes +
- \#columnas de cadena larga \* 16 MB para el diccionario de compresión

donde las columnas de cadena corta emplean tipos de datos de cadena de ≤32 bytes y las de cadena larga usan tipos de datos de cadena de >32 bytes.

Las cadenas largas que se comprimen con un método de compresión diseñado para comprimir texto. Este método de compresión usa un *diccionario* toostore patrones de texto. tamaño máximo de Hola de un diccionario es de 16 MB. Hay solo un diccionario para cada columna de cadena larga en el grupo de filas de Hola.

Para ver una discusión en profundidad sobre los requisitos de memoria del almacén de columnas, eche un vistazo al vídeo [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822) (Escalado de Azure SQL Data Warehouse: configuración y directrices).

## <a name="ways-tooreduce-memory-requirements"></a>Requisitos de memoria de formas tooreduce

Usar hello según los requisitos de memoria de técnicas tooreduce Hola para comprimir los grupos de filas en los índices de almacén de columnas.

### <a name="use-fewer-columns"></a>Utilizar menos columnas
Si es posible, diseñar tabla Hola con menos columnas. Cuando un grupo de filas se comprime en el almacén de columnas de hello, índice de almacén de columnas de hello comprime cada segmento de columna por separado. Hola, por tanto, los requisitos de memoria aumentan a medida que Hola aumenta número de columnas toocompress un grupo de filas.


### <a name="use-fewer-string-columns"></a>Utilizar menos columnas de cadena
Las columnas de tipos de datos de cadena requieren más memoria que los tipos de datos numéricos y de fecha. requisitos de memoria de tooreduce, considere la posibilidad de quitar las columnas de cadena de las tablas de hechos y colocarlos en las tablas de dimensión más pequeñas.

Requisitos de memoria adicionales para la compresión de cadenas:

- Tipos de datos de cadena de caracteres de too32 pueden requerir 32 bytes adicionales por valor.
- Los tipos de datos de cadena con más de 32 caracteres se comprimen con métodos de diccionario.  Cada columna de grupo de filas de hello puede requerir diccionario de tooan adicionales de 16 MB toobuild Hola.

### <a name="avoid-over-partitioning"></a>Evitar un exceso de particiones

Los índices de almacén de columnas crean uno o varios grupos de filas por partición. En el almacén de datos de SQL, número de Hola de particiones aumenta rápidamente porque Hola datos se distribuyen y se crean particiones de cada distribución. Si tabla hello tiene demasiadas particiones, podría no ser suficiente grupos de filas de filas toofill Hola. falta de Hola de filas no crea presión de memoria durante la compresión, pero lo hace toorowgroups que no se alcance el mejor rendimiento de consultas de almacén de columnas Hola.

Otro motivo tooavoid exceso particiones es que hay una sobrecarga de memoria para cargar las filas en un índice de almacén de columnas en una tabla con particiones. Durante la carga de un número de particiones podría recibir filas entrantes hello, que se mantienen en la memoria hasta que cada partición tiene suficiente toobe de filas comprimido. Si se cuenta con demasiadas particiones, se genera una presión de memoria adicional.

### <a name="simplify-hello-load-query"></a>Simplificar la consulta de carga de Hola

base de datos de Hello comparte Hola de concesión de memoria para una consulta entre todos los operadores de hello en consulta Hola. Cuando una consulta de carga tiene ordenaciones complejas y combinaciones, se reduce la memoria de hello disponible para la compresión.

Diseñar Hola carga consulta toofocus solo en cargar Hola consulta. Si necesita toorun transformaciones en los datos de hello, ejecutarlos independiente de consulta de carga de Hola. Por ejemplo, almacenar los datos en una tabla de montón, Hola ejecutar transformaciones de hello y, a continuación, cargar Hola tabla de ensayo en el índice de almacén de columnas de Hola. Puede cargar datos de hello en primer lugar y, a continuación, usar datos de saludo de hello MPP sistema tootransform.

### <a name="adjust-maxdop"></a>Ajustar MAXDOP

Cada distribución comprime los grupos de filas en almacén de columnas de hello en paralelo cuando hay más de un núcleo de CPU disponible por la distribución. paralelismo de Hello requiere recursos adicionales de memoria, lo que pueden provocar toomemory presión y recorte de un grupo de filas.

tooreduce presión de memoria, puede usar Hola MAXDOP consulta sugerencia tooforce Hola carga operación toorun en modo serie dentro de cada distribución.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>Formas tooallocate más memoria

Clase de recursos de usuario de hello y tamaño DWU combinación determinan la cantidad de memoria está disponible para una consulta de usuario. tooincrease Hola de concesión de memoria para una consulta de carga, puede aumentar el número de Hola de a Dwu o aumentar la clase de recurso de hello.

- ¿Hola tooincrease a Dwu, vea [cómo escalar el rendimiento?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- clase de recurso de hello toochange para una consulta, vea [cambiar un ejemplo de clase del recurso de usuario](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

Por ejemplo, en 100 de DWU un usuario en la clase de recurso de hello smallrc puede usar 100 MB de memoria para cada distribución. Para obtener detalles de hello, consulte [simultaneidad en el almacén de datos de SQL](sql-data-warehouse-develop-concurrency.md).

Suponga que decide que necesita 700 MB de tamaños de memoria tooget grupo de filas de alta calidad. Estos ejemplos muestran cómo se puede ejecutar la consulta de carga de hello con suficiente memoria.

- Con 1000 DWU y mediumrc, la concesión de memoria es de 800 MB.
- Con 600 DWU y largerc, la concesión de memoria es de 800 MB.


## <a name="next-steps"></a>Pasos siguientes

toofind más rendimiento tooimprove de formas en el almacén de datos de SQL, vea hello [información general sobre rendimiento](sql-data-warehouse-overview-manage-user-queries.md).

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
