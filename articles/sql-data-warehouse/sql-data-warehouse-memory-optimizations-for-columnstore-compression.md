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
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="b454a-103">Maximización de la calidad del grupo de filas del almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="b454a-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="b454a-104">Calidad de un grupo de filas se determina mediante el número de filas de un grupo de filas Hola.</span><span class="sxs-lookup"><span data-stu-id="b454a-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="b454a-105">Reduzca los requisitos de memoria o aumentar Hola memoria disponible toomaximize Hola número de filas de que un índice de almacén de columnas comprime en cada grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="b454a-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="b454a-106">Use las tasas de compresión de métodos tooimprove y rendimiento de las consultas para los índices de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="b454a-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="b454a-107">¿Por qué es importante el tamaño del grupo de filas de Hola</span><span class="sxs-lookup"><span data-stu-id="b454a-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="b454a-108">Puesto que un índice de almacén recorre una tabla mediante el análisis de segmentos de columna de grupos de filas individuales, maximizar el número de Hola de filas de cada grupo de filas mejora el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="b454a-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="b454a-109">Cuando los grupos de filas tienen un gran número de filas, la compresión de datos mejora lo que significa que hay menos tooread datos desde el disco.</span><span class="sxs-lookup"><span data-stu-id="b454a-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="b454a-110">Para obtener más información sobre los grupos de filas, consulte [Guía de índices de almacén de columnas](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="b454a-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="b454a-111">Tamaño objetivo de los grupos de filas</span><span class="sxs-lookup"><span data-stu-id="b454a-111">Target size for rowgroups</span></span>
<span data-ttu-id="b454a-112">Para obtener el mejor rendimiento de consulta, objetivo de hello es número de hello toomaximize de filas por grupo en un índice de almacén.</span><span class="sxs-lookup"><span data-stu-id="b454a-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="b454a-113">Un grupo de filas puede tener un máximo de 1.048.576 filas.</span><span class="sxs-lookup"><span data-stu-id="b454a-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="b454a-114">Su correcto toonot tiene número máximo de Hola de filas por grupo.</span><span class="sxs-lookup"><span data-stu-id="b454a-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="b454a-115">Los índices de almacén de columnas logran un buen rendimiento cuando los grupos de filas cuentan con al menos 100.000 filas.</span><span class="sxs-lookup"><span data-stu-id="b454a-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="b454a-116">Los grupos de filas pueden recortarse durante la compresión</span><span class="sxs-lookup"><span data-stu-id="b454a-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="b454a-117">Durante una regeneración de índice masiva carga o almacén de columnas, en ocasiones, no hay suficiente toocompress disponibles de memoria que todos Hola filas designados para cada grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="b454a-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="b454a-118">Cuando hay presión de memoria, índices de almacén de columnas recortan tamaños de grupo de filas de Hola para que compresión de almacén de columnas de Hola se realice correctamente.</span><span class="sxs-lookup"><span data-stu-id="b454a-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="b454a-119">Cuando hay filas de toocompress al menos 10 000 no hay memoria suficiente en cada grupo de filas, almacenamiento de datos de SQL genera un error.</span><span class="sxs-lookup"><span data-stu-id="b454a-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="b454a-120">Para obtener más información sobre la carga masiva, consulte [Carga de datos en un índice de almacén de columnas agrupado](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="b454a-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="b454a-121">La calidad de un grupo de filas toomonitor</span><span class="sxs-lookup"><span data-stu-id="b454a-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="b454a-122">Hay una DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) que expone información útil, como el número de filas de la razón de hello y grupos de filas de recorte si se recorta no existe.</span><span class="sxs-lookup"><span data-stu-id="b454a-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="b454a-123">Puede crear Hola después de la vista como una forma práctica tooquery esta información de tooget DMV de recorte de un grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="b454a-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

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

<span data-ttu-id="b454a-124">Hola trim_reason_desc indica si el grupo de filas de Hola se recorta (trim_reason_desc = NO_TRIM implica no hubo ningún recorte y grupo de filas es de calidad óptima).</span><span class="sxs-lookup"><span data-stu-id="b454a-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="b454a-125">Hello razones recorte siguientes indican prematura recorte del grupo de filas de hello:</span><span class="sxs-lookup"><span data-stu-id="b454a-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="b454a-126">Carga masiva: Ello recorte se utiliza al lote entrante de Hola de filas de carga de hello tenía menor que 1 millón de filas.</span><span class="sxs-lookup"><span data-stu-id="b454a-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="b454a-127">motor de Hello creará grupos de filas comprimido si hay más de 100.000 filas insertadas (como tooinserting lugar en el almacén delta de hello) pero conjuntos Hola tooBULKLOAD motivo recorte.</span><span class="sxs-lookup"><span data-stu-id="b454a-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="b454a-128">En este escenario, considere la posibilidad de aumentar su tooaccumulate de ventana de carga de lote más filas.</span><span class="sxs-lookup"><span data-stu-id="b454a-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="b454a-129">Además, vuelva a evaluar su tooensure de esquema de partición no es demasiado específico, como grupos de filas no pueden abarcar los límites de partición.</span><span class="sxs-lookup"><span data-stu-id="b454a-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="b454a-130">MEMORY_LIMITATION: motor de hello requiere toocreate grupos de filas con 1 millón de filas, una determinada cantidad de memoria de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b454a-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="b454a-131">Cuando la Hola cargar sesión de memoria disponible es menor que Hola necesaria de memoria de trabajo, prematuramente obtengan recuperan grupos de filas.</span><span class="sxs-lookup"><span data-stu-id="b454a-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="b454a-132">Hola las secciones siguientes explica cómo tooestimate memoria necesaria y asignar más memoria.</span><span class="sxs-lookup"><span data-stu-id="b454a-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="b454a-133">DICTIONARY_SIZE: este motivo de recorte indica que el recorte del grupo de filas se ha producido porque había al menos una columna de cadena con cadenas de cardinalidad anchas o altas.</span><span class="sxs-lookup"><span data-stu-id="b454a-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="b454a-134">el tamaño del diccionario Hello es limitado too16 MB de memoria y una vez que se alcanza este límite grupo de filas de Hola se comprime.</span><span class="sxs-lookup"><span data-stu-id="b454a-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="b454a-135">Si ejecuta esta situación, considere la posibilidad de aislar columna problemático hello en una tabla independiente.</span><span class="sxs-lookup"><span data-stu-id="b454a-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="b454a-136">¿Cómo tooestimate requisitos de memoria</span><span class="sxs-lookup"><span data-stu-id="b454a-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="b454a-137">Hola máximo memoria necesaria toocompress un grupo de filas es aproximadamente</span><span class="sxs-lookup"><span data-stu-id="b454a-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="b454a-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="b454a-138">72 MB +</span></span>
- <span data-ttu-id="b454a-139">\#filas \*\#columnas \* 8 bytes +</span><span class="sxs-lookup"><span data-stu-id="b454a-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="b454a-140">\#filas \*\#columnas de cadena corta \* 32 bytes +</span><span class="sxs-lookup"><span data-stu-id="b454a-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="b454a-141">\#columnas de cadena larga \* 16 MB para el diccionario de compresión</span><span class="sxs-lookup"><span data-stu-id="b454a-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="b454a-142">donde las columnas de cadena corta emplean tipos de datos de cadena de ≤32 bytes y las de cadena larga usan tipos de datos de cadena de >32 bytes.</span><span class="sxs-lookup"><span data-stu-id="b454a-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="b454a-143">Las cadenas largas que se comprimen con un método de compresión diseñado para comprimir texto.</span><span class="sxs-lookup"><span data-stu-id="b454a-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="b454a-144">Este método de compresión usa un *diccionario* toostore patrones de texto.</span><span class="sxs-lookup"><span data-stu-id="b454a-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="b454a-145">tamaño máximo de Hola de un diccionario es de 16 MB.</span><span class="sxs-lookup"><span data-stu-id="b454a-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="b454a-146">Hay solo un diccionario para cada columna de cadena larga en el grupo de filas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b454a-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="b454a-147">Para ver una discusión en profundidad sobre los requisitos de memoria del almacén de columnas, eche un vistazo al vídeo [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822) (Escalado de Azure SQL Data Warehouse: configuración y directrices).</span><span class="sxs-lookup"><span data-stu-id="b454a-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="b454a-148">Requisitos de memoria de formas tooreduce</span><span class="sxs-lookup"><span data-stu-id="b454a-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="b454a-149">Usar hello según los requisitos de memoria de técnicas tooreduce Hola para comprimir los grupos de filas en los índices de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="b454a-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="b454a-150">Utilizar menos columnas</span><span class="sxs-lookup"><span data-stu-id="b454a-150">Use fewer columns</span></span>
<span data-ttu-id="b454a-151">Si es posible, diseñar tabla Hola con menos columnas.</span><span class="sxs-lookup"><span data-stu-id="b454a-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="b454a-152">Cuando un grupo de filas se comprime en el almacén de columnas de hello, índice de almacén de columnas de hello comprime cada segmento de columna por separado.</span><span class="sxs-lookup"><span data-stu-id="b454a-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="b454a-153">Hola, por tanto, los requisitos de memoria aumentan a medida que Hola aumenta número de columnas toocompress un grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="b454a-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="b454a-154">Utilizar menos columnas de cadena</span><span class="sxs-lookup"><span data-stu-id="b454a-154">Use fewer string columns</span></span>
<span data-ttu-id="b454a-155">Las columnas de tipos de datos de cadena requieren más memoria que los tipos de datos numéricos y de fecha.</span><span class="sxs-lookup"><span data-stu-id="b454a-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="b454a-156">requisitos de memoria de tooreduce, considere la posibilidad de quitar las columnas de cadena de las tablas de hechos y colocarlos en las tablas de dimensión más pequeñas.</span><span class="sxs-lookup"><span data-stu-id="b454a-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="b454a-157">Requisitos de memoria adicionales para la compresión de cadenas:</span><span class="sxs-lookup"><span data-stu-id="b454a-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="b454a-158">Tipos de datos de cadena de caracteres de too32 pueden requerir 32 bytes adicionales por valor.</span><span class="sxs-lookup"><span data-stu-id="b454a-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="b454a-159">Los tipos de datos de cadena con más de 32 caracteres se comprimen con métodos de diccionario.</span><span class="sxs-lookup"><span data-stu-id="b454a-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="b454a-160">Cada columna de grupo de filas de hello puede requerir diccionario de tooan adicionales de 16 MB toobuild Hola.</span><span class="sxs-lookup"><span data-stu-id="b454a-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="b454a-161">Evitar un exceso de particiones</span><span class="sxs-lookup"><span data-stu-id="b454a-161">Avoid over-partitioning</span></span>

<span data-ttu-id="b454a-162">Los índices de almacén de columnas crean uno o varios grupos de filas por partición.</span><span class="sxs-lookup"><span data-stu-id="b454a-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="b454a-163">En el almacén de datos de SQL, número de Hola de particiones aumenta rápidamente porque Hola datos se distribuyen y se crean particiones de cada distribución.</span><span class="sxs-lookup"><span data-stu-id="b454a-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="b454a-164">Si tabla hello tiene demasiadas particiones, podría no ser suficiente grupos de filas de filas toofill Hola.</span><span class="sxs-lookup"><span data-stu-id="b454a-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="b454a-165">falta de Hola de filas no crea presión de memoria durante la compresión, pero lo hace toorowgroups que no se alcance el mejor rendimiento de consultas de almacén de columnas Hola.</span><span class="sxs-lookup"><span data-stu-id="b454a-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="b454a-166">Otro motivo tooavoid exceso particiones es que hay una sobrecarga de memoria para cargar las filas en un índice de almacén de columnas en una tabla con particiones.</span><span class="sxs-lookup"><span data-stu-id="b454a-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="b454a-167">Durante la carga de un número de particiones podría recibir filas entrantes hello, que se mantienen en la memoria hasta que cada partición tiene suficiente toobe de filas comprimido.</span><span class="sxs-lookup"><span data-stu-id="b454a-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="b454a-168">Si se cuenta con demasiadas particiones, se genera una presión de memoria adicional.</span><span class="sxs-lookup"><span data-stu-id="b454a-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="b454a-169">Simplificar la consulta de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="b454a-169">Simplify hello load query</span></span>

<span data-ttu-id="b454a-170">base de datos de Hello comparte Hola de concesión de memoria para una consulta entre todos los operadores de hello en consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="b454a-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="b454a-171">Cuando una consulta de carga tiene ordenaciones complejas y combinaciones, se reduce la memoria de hello disponible para la compresión.</span><span class="sxs-lookup"><span data-stu-id="b454a-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="b454a-172">Diseñar Hola carga consulta toofocus solo en cargar Hola consulta.</span><span class="sxs-lookup"><span data-stu-id="b454a-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="b454a-173">Si necesita toorun transformaciones en los datos de hello, ejecutarlos independiente de consulta de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="b454a-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="b454a-174">Por ejemplo, almacenar los datos en una tabla de montón, Hola ejecutar transformaciones de hello y, a continuación, cargar Hola tabla de ensayo en el índice de almacén de columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b454a-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="b454a-175">Puede cargar datos de hello en primer lugar y, a continuación, usar datos de saludo de hello MPP sistema tootransform.</span><span class="sxs-lookup"><span data-stu-id="b454a-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="b454a-176">Ajustar MAXDOP</span><span class="sxs-lookup"><span data-stu-id="b454a-176">Adjust MAXDOP</span></span>

<span data-ttu-id="b454a-177">Cada distribución comprime los grupos de filas en almacén de columnas de hello en paralelo cuando hay más de un núcleo de CPU disponible por la distribución.</span><span class="sxs-lookup"><span data-stu-id="b454a-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="b454a-178">paralelismo de Hello requiere recursos adicionales de memoria, lo que pueden provocar toomemory presión y recorte de un grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="b454a-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="b454a-179">tooreduce presión de memoria, puede usar Hola MAXDOP consulta sugerencia tooforce Hola carga operación toorun en modo serie dentro de cada distribución.</span><span class="sxs-lookup"><span data-stu-id="b454a-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="b454a-180">Formas tooallocate más memoria</span><span class="sxs-lookup"><span data-stu-id="b454a-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="b454a-181">Clase de recursos de usuario de hello y tamaño DWU combinación determinan la cantidad de memoria está disponible para una consulta de usuario.</span><span class="sxs-lookup"><span data-stu-id="b454a-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="b454a-182">tooincrease Hola de concesión de memoria para una consulta de carga, puede aumentar el número de Hola de a Dwu o aumentar la clase de recurso de hello.</span><span class="sxs-lookup"><span data-stu-id="b454a-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="b454a-183">¿Hola tooincrease a Dwu, vea [cómo escalar el rendimiento?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="b454a-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="b454a-184">clase de recurso de hello toochange para una consulta, vea [cambiar un ejemplo de clase del recurso de usuario](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="b454a-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="b454a-185">Por ejemplo, en 100 de DWU un usuario en la clase de recurso de hello smallrc puede usar 100 MB de memoria para cada distribución.</span><span class="sxs-lookup"><span data-stu-id="b454a-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="b454a-186">Para obtener detalles de hello, consulte [simultaneidad en el almacén de datos de SQL](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="b454a-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="b454a-187">Suponga que decide que necesita 700 MB de tamaños de memoria tooget grupo de filas de alta calidad.</span><span class="sxs-lookup"><span data-stu-id="b454a-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="b454a-188">Estos ejemplos muestran cómo se puede ejecutar la consulta de carga de hello con suficiente memoria.</span><span class="sxs-lookup"><span data-stu-id="b454a-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="b454a-189">Con 1000 DWU y mediumrc, la concesión de memoria es de 800 MB.</span><span class="sxs-lookup"><span data-stu-id="b454a-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="b454a-190">Con 600 DWU y largerc, la concesión de memoria es de 800 MB.</span><span class="sxs-lookup"><span data-stu-id="b454a-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b454a-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b454a-191">Next steps</span></span>

<span data-ttu-id="b454a-192">toofind más rendimiento tooimprove de formas en el almacén de datos de SQL, vea hello [información general sobre rendimiento](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="b454a-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
