---
title: "Mejora del rendimiento del índice de almacén de columnas en Azure SQL | Microsoft Docs"
description: "Reduzca los requisitos de memoria o aumente la memoria disponible para maximizar el número de filas que un índice de almacén de columnas comprime en cada grupo de filas."
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
ms.openlocfilehash: f0e0b839b4a0c216eee2eb5134d43b91d8f83289
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="dfc43-103">Maximización de la calidad del grupo de filas del almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="dfc43-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="dfc43-104">El número de filas de un grupo de filas determina la calidad del grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-104">Rowgroup quality is determined by the number of rows in a rowgroup.</span></span> <span data-ttu-id="dfc43-105">Reduzca los requisitos de memoria o aumente la memoria disponible para maximizar el número de filas que un índice de almacén de columnas comprime en cada grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-105">Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="dfc43-106">Emplee estos métodos para mejorar las tasas de compresión y el rendimiento de las consultas de los índices de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-106">Use these methods to improve compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-the-rowgroup-size-matters"></a><span data-ttu-id="dfc43-107">Por qué importa el tamaño del grupo de filas</span><span class="sxs-lookup"><span data-stu-id="dfc43-107">Why the rowgroup size matters</span></span>
<span data-ttu-id="dfc43-108">Como los índices de almacén de columnas examinan una tabla mediante el examen de segmentos de columna de grupos de filas individuales, al maximizar el número de filas de cada grupo de estas, se mejora el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="dfc43-109">Cuando los grupos de filas presentan un gran número de filas, la compresión de datos mejora; es decir, hay menos datos que se deben leer en el disco.</span><span class="sxs-lookup"><span data-stu-id="dfc43-109">When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.</span></span>

<span data-ttu-id="dfc43-110">Para obtener más información sobre los grupos de filas, consulte [Guía de índices de almacén de columnas](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfc43-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="dfc43-111">Tamaño objetivo de los grupos de filas</span><span class="sxs-lookup"><span data-stu-id="dfc43-111">Target size for rowgroups</span></span>
<span data-ttu-id="dfc43-112">Para obtener el mejor rendimiento de consultas, el objetivo consiste en maximizar el número de filas por grupo de un índice de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-112">For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="dfc43-113">Un grupo de filas puede tener un máximo de 1.048.576 filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="dfc43-114">No pasa nada si no se tiene el máximo número de filas por grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-114">It's okay to not have the maximum number of rows per rowgroup.</span></span> <span data-ttu-id="dfc43-115">Los índices de almacén de columnas logran un buen rendimiento cuando los grupos de filas cuentan con al menos 100.000 filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="dfc43-116">Los grupos de filas pueden recortarse durante la compresión</span><span class="sxs-lookup"><span data-stu-id="dfc43-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="dfc43-117">Durante una carga masiva o regeneración de índice de almacén columnas, a veces no queda suficiente memoria disponible para comprimir todas las filas designadas para cada grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup.</span></span> <span data-ttu-id="dfc43-118">Cuando existe una presión de memoria, los índices de almacén de columnas recortan el tamaño de los grupos de filas para que se pueda realizar la compresión en el almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-118">When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.</span></span> 

<span data-ttu-id="dfc43-119">Cuando no hay memoria suficiente para comprimir al menos 10.000 filas en cada grupo de filas, SQL Data Warehouse genera un error.</span><span class="sxs-lookup"><span data-stu-id="dfc43-119">When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="dfc43-120">Para obtener más información sobre la carga masiva, consulte [Carga de datos en un índice de almacén de columnas agrupado](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="dfc43-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-to-monitor-rowgroup-quality"></a><span data-ttu-id="dfc43-121">Cómo supervisar la calidad del grupo de filas</span><span class="sxs-lookup"><span data-stu-id="dfc43-121">How to monitor rowgroup quality</span></span>

<span data-ttu-id="dfc43-122">Hay una DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) que expone información útil como el número de filas de los grupos de filas y el motivo para recortar si ha habido recorte.</span><span class="sxs-lookup"><span data-stu-id="dfc43-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and the reason for trimming if there was trimming.</span></span> <span data-ttu-id="dfc43-123">Puede crear la siguiente vista como una forma práctica para consultar esta DMV a fin de obtener información sobre el recorte del grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-123">You can create the following view as a handy way to query this DMV to get information on rowgroup trimming.</span></span>

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

<span data-ttu-id="dfc43-124">trim_reason_desc indica si el grupo de filas se ha recortado (trim_reason_desc = NO_TRIM implica que no ha habido ningún recorte y que el grupo de filas es de calidad óptima).</span><span class="sxs-lookup"><span data-stu-id="dfc43-124">The trim_reason_desc tells whether the rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="dfc43-125">Los siguientes motivos de recorte indican el recorte prematuro del grupo de filas:</span><span class="sxs-lookup"><span data-stu-id="dfc43-125">The following trim reasons indicate premature trimming of the rowgroup:</span></span>
- <span data-ttu-id="dfc43-126">BULKLOAD: este motivo de recorte se usa cuando el lote entrante de filas de la carga tenía menos de 1 millón de filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-126">BULKLOAD: This trim reason is used when the incoming batch of rows for the load had less than 1 million rows.</span></span> <span data-ttu-id="dfc43-127">El motor creará grupos de filas comprimidos si hay más de 100.000 filas que se van a insertar (en lugar de insertar en el almacén delta), pero establece el motivo de recorte en BULKLOAD.</span><span class="sxs-lookup"><span data-stu-id="dfc43-127">The engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed to inserting into the delta store) but sets the trim reason to BULKLOAD.</span></span> <span data-ttu-id="dfc43-128">En este escenario, considere la posibilidad de aumentar la ventana de carga por lotes para acumular más filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-128">In this scenario, consider increasing your batch load window to accumulate more rows.</span></span> <span data-ttu-id="dfc43-129">Además, vuelva a evaluar el esquema de partición para asegurarse de que no es demasiado granular si los grupos de filas no pueden abarcar los límites de partición.</span><span class="sxs-lookup"><span data-stu-id="dfc43-129">Also, reevaluate your partitioning scheme to ensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="dfc43-130">MEMORY_LIMITATION: para crear grupos de filas con 1 millón de filas, el motor necesita una determinada cantidad de memoria de trabajo.</span><span class="sxs-lookup"><span data-stu-id="dfc43-130">MEMORY_LIMITATION: To create row groups with 1 million rows, a certain amount of working memory is required by the engine.</span></span> <span data-ttu-id="dfc43-131">Cuando la memoria disponible de la sesión de carga es inferior a la memoria de trabajo necesaria, los grupos de filas se recortan prematuramente.</span><span class="sxs-lookup"><span data-stu-id="dfc43-131">When available memory of the loading session is less than the required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="dfc43-132">En las siguientes secciones se explica cómo estimar la memoria necesaria y asignar más.</span><span class="sxs-lookup"><span data-stu-id="dfc43-132">The following sections explain how to estimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="dfc43-133">DICTIONARY_SIZE: este motivo de recorte indica que el recorte del grupo de filas se ha producido porque había al menos una columna de cadena con cadenas de cardinalidad anchas o altas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="dfc43-134">El tamaño del diccionario está limitado a 16 MB de memoria y, cuando se alcanza este límite, se comprime el grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-134">The dictionary size is limited to 16 MB in memory and once this limit is reached the row group is compressed.</span></span> <span data-ttu-id="dfc43-135">Si ejecuta en esta situación, considere la posibilidad de aislar la columna problemática en una tabla independiente.</span><span class="sxs-lookup"><span data-stu-id="dfc43-135">If you do run into this situation, consider isolating the problematic column into a separate table.</span></span>

## <a name="how-to-estimate-memory-requirements"></a><span data-ttu-id="dfc43-136">Cómo calcular los requisitos de memoria</span><span class="sxs-lookup"><span data-stu-id="dfc43-136">How to estimate memory requirements</span></span>

<!--
To view an estimate of the memory requirements to compress a rowgroup of maximum size into a columnstore index, download and run the view [dbo.vCS_mon_mem_grant](). This view shows the size of the memory grant that a rowgroup requires for compression in to the columnstore.
-->

<span data-ttu-id="dfc43-137">La memoria máxima requerida para comprimir un grupo de filas es aproximadamente:</span><span class="sxs-lookup"><span data-stu-id="dfc43-137">The maximum required memory to compress one rowgroup is approximately</span></span>

- <span data-ttu-id="dfc43-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="dfc43-138">72 MB +</span></span>
- <span data-ttu-id="dfc43-139">\#filas \* \#columnas \* 8 bytes +</span><span class="sxs-lookup"><span data-stu-id="dfc43-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="dfc43-140">\#filas \* \#columnas de cadena corta \* 32 bytes +</span><span class="sxs-lookup"><span data-stu-id="dfc43-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="dfc43-141">\#columnas de cadena larga \* 16 MB para el diccionario de compresión</span><span class="sxs-lookup"><span data-stu-id="dfc43-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="dfc43-142">donde las columnas de cadena corta emplean tipos de datos de cadena de ≤32 bytes y las de cadena larga usan tipos de datos de cadena de >32 bytes.</span><span class="sxs-lookup"><span data-stu-id="dfc43-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="dfc43-143">Las cadenas largas que se comprimen con un método de compresión diseñado para comprimir texto.</span><span class="sxs-lookup"><span data-stu-id="dfc43-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="dfc43-144">Este método de compresión utiliza un *diccionario* para almacenar patrones de texto.</span><span class="sxs-lookup"><span data-stu-id="dfc43-144">This compression method uses a *dictionary* to store text patterns.</span></span> <span data-ttu-id="dfc43-145">El tamaño máximo de un diccionario es de 16 MB.</span><span class="sxs-lookup"><span data-stu-id="dfc43-145">The maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="dfc43-146">Hay solo un diccionario para cada columna de cadena larga del grupo de filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-146">There is only one dictionary for each long string column in the rowgroup.</span></span>

<span data-ttu-id="dfc43-147">Para ver una discusión en profundidad sobre los requisitos de memoria del almacén de columnas, eche un vistazo al vídeo [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822) (Escalado de Azure SQL Data Warehouse: configuración y directrices).</span><span class="sxs-lookup"><span data-stu-id="dfc43-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-to-reduce-memory-requirements"></a><span data-ttu-id="dfc43-148">Formas de reducir los requisitos de memoria</span><span class="sxs-lookup"><span data-stu-id="dfc43-148">Ways to reduce memory requirements</span></span>

<span data-ttu-id="dfc43-149">Ponga en práctica las siguientes técnicas a fin de reducir los requisitos de memoria para comprimir los grupos de filas en índices de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-149">Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="dfc43-150">Utilizar menos columnas</span><span class="sxs-lookup"><span data-stu-id="dfc43-150">Use fewer columns</span></span>
<span data-ttu-id="dfc43-151">Si es posible, diseñe la tabla con menos columnas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-151">If possible, design the table with fewer columns.</span></span> <span data-ttu-id="dfc43-152">Cuando se comprime un grupo de filas en el almacén de columnas, el índice de este comprime cada segmento de columna por separado.</span><span class="sxs-lookup"><span data-stu-id="dfc43-152">When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="dfc43-153">Por lo tanto, los requisitos de memoria para comprimir un grupo de filas aumentan a la par que el número de columnas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-153">Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="dfc43-154">Utilizar menos columnas de cadena</span><span class="sxs-lookup"><span data-stu-id="dfc43-154">Use fewer string columns</span></span>
<span data-ttu-id="dfc43-155">Las columnas de tipos de datos de cadena requieren más memoria que los tipos de datos numéricos y de fecha.</span><span class="sxs-lookup"><span data-stu-id="dfc43-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="dfc43-156">Para reducir los requisitos de memoria, plantéese la posibilidad de quitar las columnas de cadena de las tablas de hechos y colocarlos en las tablas de dimensiones más pequeñas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-156">To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="dfc43-157">Requisitos de memoria adicionales para la compresión de cadenas:</span><span class="sxs-lookup"><span data-stu-id="dfc43-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="dfc43-158">Los tipos de datos de cadena de hasta 32 caracteres pueden requerir 32 bytes adicionales por valor.</span><span class="sxs-lookup"><span data-stu-id="dfc43-158">String data types up to 32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="dfc43-159">Los tipos de datos de cadena con más de 32 caracteres se comprimen con métodos de diccionario.</span><span class="sxs-lookup"><span data-stu-id="dfc43-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="dfc43-160">Cada columna del grupo de filas puede requerir hasta 16 MB adicionales para crear el diccionario.</span><span class="sxs-lookup"><span data-stu-id="dfc43-160">Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="dfc43-161">Evitar un exceso de particiones</span><span class="sxs-lookup"><span data-stu-id="dfc43-161">Avoid over-partitioning</span></span>

<span data-ttu-id="dfc43-162">Los índices de almacén de columnas crean uno o varios grupos de filas por partición.</span><span class="sxs-lookup"><span data-stu-id="dfc43-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="dfc43-163">En SQL Data Warehouse, el número de particiones aumenta rápidamente porque los datos se distribuyen y cada distribución se particiona.</span><span class="sxs-lookup"><span data-stu-id="dfc43-163">In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="dfc43-164">Si la tabla presenta demasiadas particiones, es posible que no haya un número de filas suficiente para llenar los grupos de filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-164">If the table has too many partitions, there might not be enough rows to fill the rowgroups.</span></span> <span data-ttu-id="dfc43-165">La falta de filas no genera presión de memoria durante la compresión, pero da lugar a grupos de filas que no logran el mejor rendimiento de consultas de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-165">The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.</span></span>

<span data-ttu-id="dfc43-166">Otro motivo para evitar el exceso de particiones es que cargar filas en un índice de columnas en una tabla particionada conlleva una sobrecarga para la memoria.</span><span class="sxs-lookup"><span data-stu-id="dfc43-166">Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="dfc43-167">Durante la carga, muchas particiones podrían recibir las filas entrantes, que se guardan en la memoria hasta que cada partición alcance el número de filas suficiente para llevar a cabo la compresión.</span><span class="sxs-lookup"><span data-stu-id="dfc43-167">During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed.</span></span> <span data-ttu-id="dfc43-168">Si se cuenta con demasiadas particiones, se genera una presión de memoria adicional.</span><span class="sxs-lookup"><span data-stu-id="dfc43-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-the-load-query"></a><span data-ttu-id="dfc43-169">Simplificar la consulta de carga</span><span class="sxs-lookup"><span data-stu-id="dfc43-169">Simplify the load query</span></span>

<span data-ttu-id="dfc43-170">La base de datos comparte la concesión de memoria para una consulta con todos los operadores de esta.</span><span class="sxs-lookup"><span data-stu-id="dfc43-170">The database shares the memory grant for a query among all the operators in the query.</span></span> <span data-ttu-id="dfc43-171">Cuando una consulta de carga presenta ordenaciones y uniones complejas, se reduce la memoria disponible para la compresión.</span><span class="sxs-lookup"><span data-stu-id="dfc43-171">When a load query has complex sorts and joins, the memory available for compression is reduced.</span></span>

<span data-ttu-id="dfc43-172">Diseñe la consulta de carga para que se centre únicamente en cargar la consulta.</span><span class="sxs-lookup"><span data-stu-id="dfc43-172">Design the load query to focus only on loading the query.</span></span> <span data-ttu-id="dfc43-173">Si tiene que ejecutar transformaciones en los datos, ejecútelas de forma independiente de la consulta de carga.</span><span class="sxs-lookup"><span data-stu-id="dfc43-173">If you need to run transformations on the data, run them separate from the load query.</span></span> <span data-ttu-id="dfc43-174">Por ejemplo, almacene provisionalmente los datos en una tabla de montón, ejecute las transformaciones y, después, cargue la tabla de almacenamiento provisional en el índice de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-174">For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index.</span></span> <span data-ttu-id="dfc43-175">Puede cargar los datos primero y, después, usar el sistema MPP para transformar los datos.</span><span class="sxs-lookup"><span data-stu-id="dfc43-175">You can also load the data first and then use the MPP system to transform the data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="dfc43-176">Ajustar MAXDOP</span><span class="sxs-lookup"><span data-stu-id="dfc43-176">Adjust MAXDOP</span></span>

<span data-ttu-id="dfc43-177">Cada distribución comprime los grupos de filas en el almacén de columnas en paralelo cuando hay más de un núcleo de CPU disponible por distribución.</span><span class="sxs-lookup"><span data-stu-id="dfc43-177">Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="dfc43-178">El paralelismo requiere recursos de memoria adicionales, lo que puede generar presión de memoria y recorte de los grupos de filas.</span><span class="sxs-lookup"><span data-stu-id="dfc43-178">The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="dfc43-179">Para reducir la presión de memoria, puede usar la sugerencia de consulta MAXDOP a fin de forzar la operación de carga con el objetivo de que se ejecute en modo serie dentro de cada distribución.</span><span class="sxs-lookup"><span data-stu-id="dfc43-179">To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-to-allocate-more-memory"></a><span data-ttu-id="dfc43-180">Formas de asignar más memoria</span><span class="sxs-lookup"><span data-stu-id="dfc43-180">Ways to allocate more memory</span></span>

<span data-ttu-id="dfc43-181">Juntos, el tamaño de DWU y la clase de recursos de usuario, determinan cuánta memoria hay disponible para la consulta de un usuario.</span><span class="sxs-lookup"><span data-stu-id="dfc43-181">DWU size and the user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="dfc43-182">A fin de incrementar la concesión de memoria para una consulta de carga, puede aumentar el número de DWU o la clase de recursos.</span><span class="sxs-lookup"><span data-stu-id="dfc43-182">To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.</span></span>

- <span data-ttu-id="dfc43-183">Para aumentar las DWU, consulte [¿Cómo se realiza el escalado del rendimiento?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="dfc43-183">To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="dfc43-184">Para cambiar la clase de recursos de una consulta, consulte [Cambio de ejemplo de clase de recursos de usuario](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="dfc43-184">To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="dfc43-185">Por ejemplo, con 100 DWU, un usuario de la clase de recursos smallrc puede usar 100 MB de memoria para cada distribución.</span><span class="sxs-lookup"><span data-stu-id="dfc43-185">For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="dfc43-186">Para obtener información más detallada, consulte el artículo sobre [simultaneidad en SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="dfc43-186">For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="dfc43-187">Supongamos que decide que necesita 700 MB de memoria para obtener tamaños de grupo de filas de alta calidad.</span><span class="sxs-lookup"><span data-stu-id="dfc43-187">Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes.</span></span> <span data-ttu-id="dfc43-188">Estos ejemplos muestran cómo se puede ejecutar la consulta de carga con suficiente memoria.</span><span class="sxs-lookup"><span data-stu-id="dfc43-188">These examples show how you can run the load query with enough memory.</span></span>

- <span data-ttu-id="dfc43-189">Con 1000 DWU y mediumrc, la concesión de memoria es de 800 MB.</span><span class="sxs-lookup"><span data-stu-id="dfc43-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="dfc43-190">Con 600 DWU y largerc, la concesión de memoria es de 800 MB.</span><span class="sxs-lookup"><span data-stu-id="dfc43-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dfc43-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dfc43-191">Next steps</span></span>

<span data-ttu-id="dfc43-192">Para descubrir más formas de mejorar el rendimiento en SQL Data Warehouse, consulte el tema de [información general sobre rendimiento](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="dfc43-192">To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
