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
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="69bb4-103">Administración de estadísticas en tablas en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="69bb4-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="69bb4-104">[Información general][Overview]</span><span class="sxs-lookup"><span data-stu-id="69bb4-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="69bb4-105">[Tipos de datos][Data Types]</span><span class="sxs-lookup"><span data-stu-id="69bb4-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="69bb4-106">[Distribución][Distribute]</span><span class="sxs-lookup"><span data-stu-id="69bb4-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="69bb4-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="69bb4-107">[Index][Index]</span></span>
> * <span data-ttu-id="69bb4-108">[Partición][Partition]</span><span class="sxs-lookup"><span data-stu-id="69bb4-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="69bb4-109">[Estadísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="69bb4-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="69bb4-110">[Temporal][Temporary]</span><span class="sxs-lookup"><span data-stu-id="69bb4-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="69bb4-111">Hello almacenamiento de datos de SQL más sepa sobre los datos, hello más rápido puede ejecutar consultas en los datos.</span><span class="sxs-lookup"><span data-stu-id="69bb4-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="69bb4-112">forma de Hola que proporcione almacenamiento de datos de SQL sobre los datos consiste en recopilar las estadísticas sobre los datos.</span><span class="sxs-lookup"><span data-stu-id="69bb4-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="69bb4-113">Cuentan con estadísticas en los datos es uno de los aspectos más importantes de hello puede hacer toooptimize las consultas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="69bb4-114">Las estadísticas ayudan a almacenamiento de datos SQL crear Hola plan más óptimo para las consultas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="69bb4-115">Esto es porque el optimizador de basados en consultas de almacenamiento de datos SQL de hello optimizador lleva un costo.</span><span class="sxs-lookup"><span data-stu-id="69bb4-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="69bb4-116">Es decir, compara el costo de Hola de varios planes de consulta y, a continuación, elige Hola plan con el costo más bajo de hello, que debe ser también plan de Hola que va a ejecutar hello más rápido.</span><span class="sxs-lookup"><span data-stu-id="69bb4-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="69bb4-117">Se pueden crear estadísticas de una sola columna, de varias columnas o de un índice de una tabla.</span><span class="sxs-lookup"><span data-stu-id="69bb4-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="69bb4-118">Las estadísticas se almacenan en un histograma que captura el intervalo de Hola y selectividad de valores.</span><span class="sxs-lookup"><span data-stu-id="69bb4-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="69bb4-119">Esto resulta de especial interés cuando el optimizador de hello necesita tooevaluate combinaciones, GROUP BY, HAVING y las cláusulas WHERE en una consulta.</span><span class="sxs-lookup"><span data-stu-id="69bb4-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="69bb4-120">Por ejemplo, si el optimizador de hello calcula que fecha Hola se va a filtrar en la consulta devolverá 1 fila, puede elegir un muy diferentes planificar que si se estimaciones que fecha han seleccionado se devuelven 1 millón de filas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="69bb4-121">Mientras que la creación de estadísticas es muy importante, es igualmente importante que las estadísticas de *con precisión* reflejan Hola el estado actual de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="69bb4-122">Cuentan con estadísticas actualizadas se asegura de que está seleccionado un buen plan optimizador Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="69bb4-123">planes de Hello creados por el optimizador de hello solo son tan eficaces como las estadísticas de hello en los datos.</span><span class="sxs-lookup"><span data-stu-id="69bb4-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="69bb4-124">proceso de Hola de creación y actualización de estadísticas actualmente es un proceso manual, pero es muy sencillo toodo.</span><span class="sxs-lookup"><span data-stu-id="69bb4-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="69bb4-125">Esto es diferente de lo que sucede en SQL Server, que crea y actualiza automáticamente estadísticas de columnas únicas e índices.</span><span class="sxs-lookup"><span data-stu-id="69bb4-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="69bb4-126">Mediante el uso de información de Hola a continuación, en gran medida puede automatizar la administración de Hola de estadísticas de hello en los datos.</span><span class="sxs-lookup"><span data-stu-id="69bb4-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="69bb4-127">Introducción a las estadísticas</span><span class="sxs-lookup"><span data-stu-id="69bb4-127">Getting started with statistics</span></span>
 <span data-ttu-id="69bb4-128">Las estadísticas muestreadas en todas las columnas es una manera sencilla de tooget inició la creación con las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="69bb4-129">Puesto que es igualmente importante tookeep estadísticas actualizadas, un enfoque conservador puede ser las estadísticas de tooupdate diariamente o después de cada carga.</span><span class="sxs-lookup"><span data-stu-id="69bb4-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="69bb4-130">Siempre hay ventajas y desventajas de rendimiento y Hola costo toocreate y actualice las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="69bb4-131">Si encuentra está tardando demasiado toomaintain todas las estadísticas, puede que desee tootry toobe más selectivo con respecto a las columnas que tienen estadísticas o las columnas que necesita una actualización frecuente.</span><span class="sxs-lookup"><span data-stu-id="69bb4-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="69bb4-132">Por ejemplo, conviene columnas de fecha tooupdate todos los días, tal y como se pueden agregar nuevos valores en lugar de después de cada carga.</span><span class="sxs-lookup"><span data-stu-id="69bb4-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="69bb4-133">Una vez más, dispondrá de hello máximas ventajas por cuentan con estadísticas en las columnas que intervienen en las combinaciones, GROUP BY, HAVING y las cláusulas WHERE.</span><span class="sxs-lookup"><span data-stu-id="69bb4-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="69bb4-134">Si tiene una tabla con una gran cantidad de columnas que se utilizan únicamente en hello SELECT (cláusula), no pueden ayudar las estadísticas de estas columnas, y gastos un poco más tooidentify de esfuerzo solo las columnas de Hola que le ayudará las estadísticas, puede reducir Hola tiempo toomaintain las estadísticas .</span><span class="sxs-lookup"><span data-stu-id="69bb4-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="69bb4-135">Estadísticas de varias columnas</span><span class="sxs-lookup"><span data-stu-id="69bb4-135">Multi-column statistics</span></span>
<span data-ttu-id="69bb4-136">Además toocreating estadísticas en columnas únicas, es posible que las consultas se beneficiarán de las estadísticas de varias columnas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="69bb4-137">Las estadísticas de varias columnas son las estadísticas creadas en una lista de columnas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="69bb4-138">Incluyen las estadísticas de columna única en la primera columna de hello en lista de hello, además de cierta información de correlación entre las columnas denominado densidades.</span><span class="sxs-lookup"><span data-stu-id="69bb4-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="69bb4-139">Por ejemplo, si tiene una tabla que combina tooanother en dos columnas, es posible que almacenamiento de datos SQL puede optimizar mejor plan de hello aunque entienda relación Hola entre dos columnas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="69bb4-140">Las estadísticas de varias columnas pueden mejorar el rendimiento de las consultas en algunas operaciones, como las cláusulas compuestas JOINs y GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="69bb4-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="69bb4-141">Actualización de estadísticas</span><span class="sxs-lookup"><span data-stu-id="69bb4-141">Updating statistics</span></span>
<span data-ttu-id="69bb4-142">La actualización de estadísticas es una parte importante de la rutina de administración de base de datos.</span><span class="sxs-lookup"><span data-stu-id="69bb4-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="69bb4-143">Cuando se cambia la distribución de Hola de los datos en la base de datos de hello, las estadísticas deben toobe actualizado.</span><span class="sxs-lookup"><span data-stu-id="69bb4-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="69bb4-144">Las estadísticas obsoletas llevará rendimiento toosub óptimo de las consultas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="69bb4-145">Una práctica recomendada es tooupdate estadísticas en columnas de fecha cada día a medida que se agregan nuevas fechas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="69bb4-146">Cada fila nueva de tiempo se carga en el almacén de datos de Hola, se agregan nuevas fechas de carga o de transacción.</span><span class="sxs-lookup"><span data-stu-id="69bb4-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="69bb4-147">Estos cambian la distribución de datos de Hola y hacer que las estadísticas de Hola quede obsoleto.</span><span class="sxs-lookup"><span data-stu-id="69bb4-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="69bb4-148">Por el contrario, las estadísticas de una columna de país en una tabla de clientes nunca necesite toobe actualizado, como generalmente no cambia la distribución de Hola de valores.</span><span class="sxs-lookup"><span data-stu-id="69bb4-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="69bb4-149">Suponiendo que la distribución de hello es constante entre los clientes, agregar nueva variación de tabla toohello de filas no va distribución de datos de toochange Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="69bb4-150">Sin embargo, si el almacenamiento de datos solo contiene un país y aparezca los datos de un nuevo país, resultante en datos procedentes de varios países va a almacenar, a continuación, definitivamente necesita tooupdate estadísticas en la columna de país de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="69bb4-151">Uno de hello primera preguntas tooask cuando está en la solución de problemas de una consulta, "son las estadísticas de hello actualizada?"</span><span class="sxs-lookup"><span data-stu-id="69bb4-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="69bb4-152">Esta pregunta no es uno que se puede responder por antigüedad de Hola de los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="69bb4-153">Un objeto de estadísticas toodate arriba podría ser muy antiguo si no ha habido ningún toohello cambio material datos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="69bb4-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="69bb4-154">Número de Hola de filas ha cambiado considerablemente cuando o hay un cambio material en la distribución de Hola de valores para una columna determinada *, a continuación,* es estadísticas de tiempo de tooupdate.</span><span class="sxs-lookup"><span data-stu-id="69bb4-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="69bb4-155">Como referencia, **SQL Server** (no Almacenamiento de datos SQL) actualiza automáticamente las estadísticas para estas situaciones:</span><span class="sxs-lookup"><span data-stu-id="69bb4-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="69bb4-156">Si tiene cero filas de tabla de hello, cuando se agregan filas, obtendrá una actualización automática de estadísticas</span><span class="sxs-lookup"><span data-stu-id="69bb4-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="69bb4-157">Cuando se agrega la tabla de tooa más de 500 filas a partir de menos de 500 filas (por ejemplo, en el inicio tenga 499 y, a continuación, agregue 500 total de tooa de filas de 999 filas), obtendrá una actualización automática</span><span class="sxs-lookup"><span data-stu-id="69bb4-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="69bb4-158">Una vez que haya más de 500 filas tendrá tooadd 500 filas adicionales + 20% del tamaño de Hola de tabla Hola antes, verá una actualización automática de estadísticas de Hola</span><span class="sxs-lookup"><span data-stu-id="69bb4-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="69bb4-159">Puesto que no hay ningún toodetermine DMV si datos dentro de la tabla de hello ha cambiado desde que se actualizaron las estadísticas de tiempo de último hello, conocer la antigüedad de Hola de las estadísticas de puede proporcionar con parte de la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="69bb4-160">Puede usar Hola después toodetermine Hola última vez las estadísticas de consulta cuando se actualiza en cada tabla.</span><span class="sxs-lookup"><span data-stu-id="69bb4-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="69bb4-161">Recuerde que si hay un cambio material en la distribución de Hola de valores para una columna determinada, deberá actualizar las estadísticas con independencia de hello última vez que se actualicen.</span><span class="sxs-lookup"><span data-stu-id="69bb4-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
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

<span data-ttu-id="69bb4-162">Las columnas de fecha en un almacenamiento de datos, por ejemplo, normalmente necesitan frecuentes actualizaciones de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="69bb4-163">Cada fila nueva de tiempo se carga en el almacén de datos de Hola, se agregan nuevas fechas de carga o de transacción.</span><span class="sxs-lookup"><span data-stu-id="69bb4-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="69bb4-164">Estos cambian la distribución de datos de Hola y hacer que las estadísticas de Hola quede obsoleto.</span><span class="sxs-lookup"><span data-stu-id="69bb4-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="69bb4-165">Por el contrario, las estadísticas de una columna de sexo en una tabla de clientes nunca necesite toobe actualizado.</span><span class="sxs-lookup"><span data-stu-id="69bb4-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="69bb4-166">Suponiendo que la distribución de hello es constante entre los clientes, agregar nueva variación de tabla toohello de filas no va distribución de datos de toochange Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="69bb4-167">Sin embargo, si el almacenamiento de datos solo contiene un género y un nuevo requisito da como resultado varios géneros definitivamente deberá tooupdate estadísticas en la columna de género Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="69bb4-168">Para obtener más información, consulte [Estadísticas][Statistics] en MSDN.</span><span class="sxs-lookup"><span data-stu-id="69bb4-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="69bb4-169">Implementación de administración de estadísticas</span><span class="sxs-lookup"><span data-stu-id="69bb4-169">Implementing statistics management</span></span>
<span data-ttu-id="69bb4-170">A menudo resulta una buena idea tooextend los datos de carga tooensure de proceso que las estadísticas se actualizan en Hola final de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="69bb4-171">carga de datos de Hello es cuando las tablas con más frecuencia cambian su tamaño o su distribución de valores.</span><span class="sxs-lookup"><span data-stu-id="69bb4-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="69bb4-172">Por lo tanto, esto es un lugar lógico tooimplement algunos procesos de administración.</span><span class="sxs-lookup"><span data-stu-id="69bb4-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="69bb4-173">Algunos de los principios rectores se proporcionan a continuación para actualizar las estadísticas durante el proceso de carga de hello:</span><span class="sxs-lookup"><span data-stu-id="69bb4-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="69bb4-174">Asegúrese de que cada tabla cargada tiene al menos un objeto de estadísticas actualizado.</span><span class="sxs-lookup"><span data-stu-id="69bb4-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="69bb4-175">Este Hola actualizaciones tablas información de tamaño (recuento de filas y recuento de páginas) como parte de la actualización de estadísticas de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="69bb4-176">Céntrese en las columnas que participan en las cláusulas JOIN, GROUP BY, ORDER BY y DISTINCT.</span><span class="sxs-lookup"><span data-stu-id="69bb4-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="69bb4-177">Considere actualizar las fechas con más frecuencia como estos valores no se incluirán en el histograma de estadísticas de Hola "ascendente clave" columnas como transacción.</span><span class="sxs-lookup"><span data-stu-id="69bb4-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="69bb4-178">Considere la posibilidad de actualizar columnas de distribución estática con menor frecuencia.</span><span class="sxs-lookup"><span data-stu-id="69bb4-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="69bb4-179">Recuerde que cada objeto de estadística se actualiza en serie.</span><span class="sxs-lookup"><span data-stu-id="69bb4-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="69bb4-180">Implementar solo `UPDATE STATISTICS <TABLE_NAME>` puede no ser recomendable, especialmente para las tablas amplias con muchos objetos de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="69bb4-181">Para obtener más detalles sobre [ascendente clave], consulte notas de modelo de estimación de cardinalidad toohello SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="69bb4-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="69bb4-182">Para obtener más información, consulte [estimación de cardinalidad][Cardinality Estimation] en MSDN.</span><span class="sxs-lookup"><span data-stu-id="69bb4-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="69bb4-183">Ejemplos: crear estadísticas</span><span class="sxs-lookup"><span data-stu-id="69bb4-183">Examples: Create statistics</span></span>
<span data-ttu-id="69bb4-184">Estos ejemplos muestran cómo toouse distintas opciones de creación de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="69bb4-185">Opciones de Hola que usas para cada columna dependen de características de Hola de los datos y cómo se usará la columna de hello en las consultas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="69bb4-186">A.</span><span class="sxs-lookup"><span data-stu-id="69bb4-186">A.</span></span> <span data-ttu-id="69bb4-187">Crear estadísticas de columna única con las opciones predeterminadas</span><span class="sxs-lookup"><span data-stu-id="69bb4-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="69bb4-188">toocreate estadísticas en una columna, basta con proporcionar un nombre de objeto de estadísticas de Hola y Hola específicos de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="69bb4-189">Esta sintaxis utiliza todas las opciones predeterminadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="69bb4-190">De forma predeterminada, almacenamiento de datos SQL muestrea el 20 por ciento de la tabla de hello cuando crea estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="69bb4-191">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="69bb4-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="69bb4-192">B.</span><span class="sxs-lookup"><span data-stu-id="69bb4-192">B.</span></span> <span data-ttu-id="69bb4-193">Crear estadísticas de columna única mediante el examen de todas las filas</span><span class="sxs-lookup"><span data-stu-id="69bb4-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="69bb4-194">velocidad de muestreo predeterminada de Hello del 20 por ciento es suficiente para la mayoría de los casos.</span><span class="sxs-lookup"><span data-stu-id="69bb4-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="69bb4-195">Sin embargo, puede ajustar la frecuencia de muestreo de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="69bb4-196">Hola toosample completa de la tabla, use esta sintaxis:</span><span class="sxs-lookup"><span data-stu-id="69bb4-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="69bb4-197">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="69bb4-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="69bb4-198">C.</span><span class="sxs-lookup"><span data-stu-id="69bb4-198">C.</span></span> <span data-ttu-id="69bb4-199">Crear estadísticas de columna única mediante la especificación de tamaño de la muestra de Hola</span><span class="sxs-lookup"><span data-stu-id="69bb4-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="69bb4-200">Como alternativa, puede especificar el tamaño de la muestra de Hola como un porcentaje:</span><span class="sxs-lookup"><span data-stu-id="69bb4-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="69bb4-201">D.</span><span class="sxs-lookup"><span data-stu-id="69bb4-201">D.</span></span> <span data-ttu-id="69bb4-202">Crear estadísticas de columna única sólo en algunas filas de Hola</span><span class="sxs-lookup"><span data-stu-id="69bb4-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="69bb4-203">Otra opción, puede crear estadísticas en una parte de las filas de hello en la tabla.</span><span class="sxs-lookup"><span data-stu-id="69bb4-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="69bb4-204">A esto se le denomina una estadística filtrada.</span><span class="sxs-lookup"><span data-stu-id="69bb4-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="69bb4-205">Por ejemplo, podría utilizar las estadísticas filtradas cuando planee tooquery una partición específica de una tabla con particiones grande.</span><span class="sxs-lookup"><span data-stu-id="69bb4-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="69bb4-206">Mediante la creación de estadísticas en hello solo valores de la partición, precisión Hola de estadísticas de hello mejorará y, por lo tanto, mejorar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="69bb4-207">En este ejemplo se crean estadísticas sobre un intervalo de valores.</span><span class="sxs-lookup"><span data-stu-id="69bb4-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="69bb4-208">Hola valores podrían fácilmente ser define el intervalo de hello toomatch de valores en una partición.</span><span class="sxs-lookup"><span data-stu-id="69bb4-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="69bb4-209">Para tooconsider de optimizador de consultas de hello utilizando las estadísticas filtradas cuando elige el plan de consulta distribuida de hello, consulta Hola debe ajustarse en definición de Hola Hola de objeto de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="69bb4-210">Utilizando el ejemplo anterior hello, Hola la consulta donde cláusula necesita toospecify col1 valores entre 2000101 y 20001231.</span><span class="sxs-lookup"><span data-stu-id="69bb4-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="69bb4-211">E.</span><span class="sxs-lookup"><span data-stu-id="69bb4-211">E.</span></span> <span data-ttu-id="69bb4-212">Crear estadísticas de columna única con todas las opciones de Hola</span><span class="sxs-lookup"><span data-stu-id="69bb4-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="69bb4-213">Por supuesto, puede combinar opciones Hola juntos.</span><span class="sxs-lookup"><span data-stu-id="69bb4-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="69bb4-214">ejemplo de Hola siguiente crea un objeto de estadísticas filtradas con un tamaño de prueba personalizados:</span><span class="sxs-lookup"><span data-stu-id="69bb4-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="69bb4-215">Para hello referencia completa, consulte [CREATE STATISTICS] [ CREATE STATISTICS] en MSDN.</span><span class="sxs-lookup"><span data-stu-id="69bb4-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="69bb4-216">F.</span><span class="sxs-lookup"><span data-stu-id="69bb4-216">F.</span></span> <span data-ttu-id="69bb4-217">Crear estadísticas de varias columnas</span><span class="sxs-lookup"><span data-stu-id="69bb4-217">Create multi-column statistics</span></span>
<span data-ttu-id="69bb4-218">toocreate estadísticas de varias columnas, simplemente utilice los ejemplos anteriores de hello, pero especifique más columnas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="69bb4-219">histograma con Hello, que se usa solo está disponible para hello primera columna aparece en la definición del objeto de estadísticas de hello tooestimate número de filas en el resultado de la consulta Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="69bb4-220">En este ejemplo, se encuentra en el histograma de hello *producto\_categoría*.</span><span class="sxs-lookup"><span data-stu-id="69bb4-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="69bb4-221">Las estadísticas entre columnas se calculan en *product\_category* y *product\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="69bb4-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="69bb4-222">Dado que no hay una correlación entre *producto\_categoría* y *producto\_sub\_categoría*, un estado de varias columna puede ser útil si se tiene acceso a estas columnas en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="69bb4-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="69bb4-223">G.</span><span class="sxs-lookup"><span data-stu-id="69bb4-223">G.</span></span> <span data-ttu-id="69bb4-224">Crear estadísticas en todas las columnas de hello en una tabla</span><span class="sxs-lookup"><span data-stu-id="69bb4-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="69bb4-225">Las estadísticas de una manera de toocreate son tooissues comandos CREATE STATISTICS después de crear la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

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

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="69bb4-226">H.</span><span class="sxs-lookup"><span data-stu-id="69bb4-226">H.</span></span> <span data-ttu-id="69bb4-227">Usar una estadística de procedimiento almacenado toocreate en todas las columnas de una base de datos</span><span class="sxs-lookup"><span data-stu-id="69bb4-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="69bb4-228">Almacenamiento de datos SQL no tienen un equivalente de procedimiento almacenado de sistema también [] [sp_create_stats] en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="69bb4-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="69bb4-229">Este procedimiento almacenado crea un objeto de estadísticas de columna única en todas las columnas de base de datos de Hola que todavía no tiene estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="69bb4-230">Esto le ayudará a empezar a trabajar con el diseño de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="69bb4-230">This will help you get started with your database design.</span></span> <span data-ttu-id="69bb4-231">Sentirse tooadapt libre debe tooyour.</span><span class="sxs-lookup"><span data-stu-id="69bb4-231">Feel free tooadapt it tooyour needs.</span></span>

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

<span data-ttu-id="69bb4-232">estadísticas de toocreate en todas las columnas de tabla de hello con este procedimiento, basta con llamar a procedimiento Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="69bb4-233">Ejemplos: actualizar estadísticas</span><span class="sxs-lookup"><span data-stu-id="69bb4-233">Examples: update statistics</span></span>
<span data-ttu-id="69bb4-234">estadísticas de tooupdate, hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="69bb4-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="69bb4-235">Actualizar un objeto de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-235">Update one statistics object.</span></span> <span data-ttu-id="69bb4-236">Especifique el nombre de Hola de hello las estadísticas del objeto que se va tooupdate.</span><span class="sxs-lookup"><span data-stu-id="69bb4-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="69bb4-237">Actualizar todos los objetos de estadísticas de una tabla.</span><span class="sxs-lookup"><span data-stu-id="69bb4-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="69bb4-238">Especifique el nombre de Hola de tabla de hello en lugar de un objeto de estadísticas específicas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="69bb4-239">A.</span><span class="sxs-lookup"><span data-stu-id="69bb4-239">A.</span></span> <span data-ttu-id="69bb4-240">Actualizar un objeto de estadísticas específico</span><span class="sxs-lookup"><span data-stu-id="69bb4-240">Update one specific statistics object</span></span>
<span data-ttu-id="69bb4-241">Usar hello siguiendo la sintaxis tooupdate un objeto concreto de estadísticas:</span><span class="sxs-lookup"><span data-stu-id="69bb4-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="69bb4-242">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="69bb4-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="69bb4-243">Al actualizar los objetos de estadísticas específico, puede minimizar Hola tiempo y recursos necesarios toomanage las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="69bb4-244">Para ello, sin embargo, algunos considerar toochoose Hola mejor estadísticas objetos tooupdate.</span><span class="sxs-lookup"><span data-stu-id="69bb4-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="69bb4-245">B.</span><span class="sxs-lookup"><span data-stu-id="69bb4-245">B.</span></span> <span data-ttu-id="69bb4-246">Actualizar todas las estadísticas de una tabla</span><span class="sxs-lookup"><span data-stu-id="69bb4-246">Update all statistics on a table</span></span>
<span data-ttu-id="69bb4-247">Esto muestra un método sencillo para actualizar todos los objetos de estadísticas de hello en una tabla.</span><span class="sxs-lookup"><span data-stu-id="69bb4-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="69bb4-248">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="69bb4-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="69bb4-249">Esta instrucción resulta fácil toouse.</span><span class="sxs-lookup"><span data-stu-id="69bb4-249">This statement is easy toouse.</span></span> <span data-ttu-id="69bb4-250">Recuerde esto actualiza todas las estadísticas de la tabla de hello y, por lo tanto, puede realizar más trabajo que sean necesarios.</span><span class="sxs-lookup"><span data-stu-id="69bb4-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="69bb4-251">Si el rendimiento de hello no es un problema, definitivamente es manera más sencilla y más completa de hello tooguarantee estadísticas están actualizadas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="69bb4-252">Al actualizar todas las estadísticas de una tabla, almacenamiento de datos SQL realiza una tabla de hello toosample de examen para cada estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="69bb4-253">Si la tabla de hello es grande, tiene muchas columnas y muchas de las estadísticas, podría ser más eficaz tooupdate de estadísticas individuales según las necesidades del.</span><span class="sxs-lookup"><span data-stu-id="69bb4-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="69bb4-254">Para obtener una implementación de un `UPDATE STATISTICS` procedimiento vea hello [tablas temporales] [ Temporary] artículo.</span><span class="sxs-lookup"><span data-stu-id="69bb4-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="69bb4-255">método de implementación de Hello es ligeramente diferente toohello `CREATE STATISTICS` procedimiento anterior pero el resultado final de hello es Hola igual.</span><span class="sxs-lookup"><span data-stu-id="69bb4-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="69bb4-256">Para consultar la sintaxis completa hello, consulte [Update Statistics] [ Update Statistics] en MSDN.</span><span class="sxs-lookup"><span data-stu-id="69bb4-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="69bb4-257">Metadatos de las estadísticas</span><span class="sxs-lookup"><span data-stu-id="69bb4-257">Statistics metadata</span></span>
<span data-ttu-id="69bb4-258">Hay varias funciones que puede usar toofind información sobre las estadísticas y vista del sistema.</span><span class="sxs-lookup"><span data-stu-id="69bb4-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="69bb4-259">Por ejemplo, puede ver si un objeto de estadísticas podría estar obsoleto mediante Hola estadísticas fecha función toosee cuando última se crea o se actualizaron las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="69bb4-260">Vistas de catálogo para las estadísticas</span><span class="sxs-lookup"><span data-stu-id="69bb4-260">Catalog views for statistics</span></span>
<span data-ttu-id="69bb4-261">Estas vistas del sistema proporcionan información acerca de las estadísticas:</span><span class="sxs-lookup"><span data-stu-id="69bb4-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="69bb4-262">Datos del catálogo</span><span class="sxs-lookup"><span data-stu-id="69bb4-262">Catalog View</span></span> | <span data-ttu-id="69bb4-263">Descripción</span><span class="sxs-lookup"><span data-stu-id="69bb4-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="69bb4-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="69bb4-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="69bb4-265">Una fila por cada columna.</span><span class="sxs-lookup"><span data-stu-id="69bb4-265">One row for each column.</span></span> |
| <span data-ttu-id="69bb4-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="69bb4-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="69bb4-267">Una fila por cada objeto de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="69bb4-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="69bb4-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="69bb4-269">Una fila por cada esquema de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="69bb4-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="69bb4-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="69bb4-271">Una fila por cada objeto de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="69bb4-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="69bb4-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="69bb4-273">Una fila por cada columna de objeto de estadísticas de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="69bb4-274">Vínculos volver toosys.columns.</span><span class="sxs-lookup"><span data-stu-id="69bb4-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="69bb4-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="69bb4-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="69bb4-276">Una fila por cada tabla (incluye tablas externas).</span><span class="sxs-lookup"><span data-stu-id="69bb4-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="69bb4-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="69bb4-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="69bb4-278">Una fila por cada tipo de datos.</span><span class="sxs-lookup"><span data-stu-id="69bb4-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="69bb4-279">Funciones del sistema para las estadísticas</span><span class="sxs-lookup"><span data-stu-id="69bb4-279">System functions for statistics</span></span>
<span data-ttu-id="69bb4-280">Estas funciones del sistema son útiles para trabajar con las estadísticas:</span><span class="sxs-lookup"><span data-stu-id="69bb4-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="69bb4-281">Función del sistema</span><span class="sxs-lookup"><span data-stu-id="69bb4-281">System Function</span></span> | <span data-ttu-id="69bb4-282">Descripción</span><span class="sxs-lookup"><span data-stu-id="69bb4-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="69bb4-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="69bb4-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="69bb4-284">Date (objeto) estadísticas Hola se actualizó por última vez.</span><span class="sxs-lookup"><span data-stu-id="69bb4-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="69bb4-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="69bb4-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="69bb4-286">Proporciona información resumida de nivel y detallada acerca de la distribución de Hola de valores según lo entiende el objeto de estadísticas de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="69bb4-287">Combinar funciones y columnas de estadísticas en una vista</span><span class="sxs-lookup"><span data-stu-id="69bb4-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="69bb4-288">Esta vista muestra las columnas que están relacionadas con toostatistics y resultados de la función de hello [STATS_DATE()] [] juntos.</span><span class="sxs-lookup"><span data-stu-id="69bb4-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

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

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="69bb4-289">Ejemplos de DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="69bb4-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="69bb4-290">DBCC SHOW_STATISTICS() muestra datos Hola mantenidos dentro de un objeto de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="69bb4-291">Estos datos se presentan en tres partes.</span><span class="sxs-lookup"><span data-stu-id="69bb4-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="69bb4-292">Encabezado</span><span class="sxs-lookup"><span data-stu-id="69bb4-292">Header</span></span>
2. <span data-ttu-id="69bb4-293">Vector de densidad</span><span class="sxs-lookup"><span data-stu-id="69bb4-293">Density Vector</span></span>
3. <span data-ttu-id="69bb4-294">Histograma</span><span class="sxs-lookup"><span data-stu-id="69bb4-294">Histogram</span></span>

<span data-ttu-id="69bb4-295">Hola encabezado metadatos acerca de las estadísticas de Hola.</span><span class="sxs-lookup"><span data-stu-id="69bb4-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="69bb4-296">Histograma Hello muestra la distribución de Hola de valores en la primera columna de clave Hola Hola de objeto de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="69bb4-297">vector de densidad de Hello mide la correlación entre las columnas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="69bb4-298">SQLDW calcula las estimaciones de cardinalidad con cualquiera de los datos de Hola Hola objeto de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="69bb4-299">Mostrar el encabezado, la densidad y el histograma</span><span class="sxs-lookup"><span data-stu-id="69bb4-299">Show header, density, and histogram</span></span>
<span data-ttu-id="69bb4-300">Este ejemplo muestra las tres partes de un objeto de estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="69bb4-301">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="69bb4-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="69bb4-302">Mostrar una o varias partes de DBCC SHOW_STATISTICS();</span><span class="sxs-lookup"><span data-stu-id="69bb4-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="69bb4-303">Si solo está interesado en ver partes específicas, use hello `WITH` cláusula y especificar qué partes se desea toosee:</span><span class="sxs-lookup"><span data-stu-id="69bb4-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="69bb4-304">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="69bb4-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="69bb4-305">Diferencias de DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="69bb4-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="69bb4-306">DBCC SHOW_STATISTICS() más estrictamente se implementa en tooSQL en comparación de almacenamiento de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="69bb4-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="69bb4-307">No se admiten características no documentadas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="69bb4-308">No se puede usar Stats_stream.</span><span class="sxs-lookup"><span data-stu-id="69bb4-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="69bb4-309">No se pueden combinar resultados de subconjuntos específicos de datos de estadísticas, como por ejemplo (STAT_HEADER JOIN DENSITY_VECTOR).</span><span class="sxs-lookup"><span data-stu-id="69bb4-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="69bb4-310">No se puede establecer NO_INFOMSGS para la supresión de mensajes.</span><span class="sxs-lookup"><span data-stu-id="69bb4-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="69bb4-311">No se pueden usar corchetes alrededor de los nombres de las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="69bb4-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="69bb4-312">No se puede usar objetos de estadísticas de tooidentify de nombres de columna</span><span class="sxs-lookup"><span data-stu-id="69bb4-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="69bb4-313">No se admite el error personalizado 2767.</span><span class="sxs-lookup"><span data-stu-id="69bb4-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="69bb4-314">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69bb4-314">Next steps</span></span>
<span data-ttu-id="69bb4-315">Para obtener más información, consulte [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] en MSDN.</span><span class="sxs-lookup"><span data-stu-id="69bb4-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="69bb4-316">toolearn más información, vea los artículos de hello en [información general de la tabla][Overview], [tipos de datos de tabla][Data Types], [distribuir una tabla] [ Distribute], [Indiza una tabla][Index], [creación de particiones de una tabla] [ Partition] y [ Tablas temporales][Temporary].</span><span class="sxs-lookup"><span data-stu-id="69bb4-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="69bb4-317">Para obtener más información sobre los procedimientos recomendados, consulte [Procedimientos recomendados para SQL Data Warehouse de Azure][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="69bb4-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
