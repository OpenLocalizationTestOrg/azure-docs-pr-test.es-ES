---
title: "Migración del esquema a SQL Data Warehouse | Microsoft Docs"
description: Sugerencias para migrar el esquema a Almacenamiento de datos SQL de Azure a fin de desarrollar soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 07ca2321852e276502187e768177e7e82bdfd080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-schemas-to-sql-data-warehouse"></a><span data-ttu-id="38970-103">Migración de esquemas a SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="38970-103">Migrate your schemas to SQL Data Warehouse</span></span>
<span data-ttu-id="38970-104">Guía para migrar esquemas SQL a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="38970-104">Guidance for migrating your SQL schemas to SQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="38970-105">Planeamiento de la migración del esquema</span><span class="sxs-lookup"><span data-stu-id="38970-105">Plan your schema migration</span></span>

<span data-ttu-id="38970-106">Cuando planee una migración, consulte la [información general de tablas][table overview] para familiarizarse con las consideraciones sobre el diseño de tabla, como las estadísticas, la distribución, la creación de particiones y la indexación.</span><span class="sxs-lookup"><span data-stu-id="38970-106">As you plan a migration, see the [table overview][table overview] to become familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="38970-107">También se incluyen algunas [características no admitidas de las tablas][unsupported table features] y las soluciones alternativas a tales carencias.</span><span class="sxs-lookup"><span data-stu-id="38970-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-to-consolidate-databases"></a><span data-ttu-id="38970-108">Uso de esquemas definidos por el usuario para consolidar bases de datos</span><span class="sxs-lookup"><span data-stu-id="38970-108">Use user-defined schemas to consolidate databases</span></span>

<span data-ttu-id="38970-109">Probablemente, su carga de trabajo existente tiene más de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="38970-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="38970-110">Por ejemplo, un almacenamiento de datos de SQL Server podría incluir una base de datos provisional, una de almacenamiento de datos y algunas de tipo data mart.</span><span class="sxs-lookup"><span data-stu-id="38970-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="38970-111">En esta topología, cada base de datos se ejecuta como una carga de trabajo independiente con directivas de seguridad distintas.</span><span class="sxs-lookup"><span data-stu-id="38970-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="38970-112">Por el contrario, el Almacenamiento de datos SQL ejecuta la carga de trabajo completa del almacenamiento de datos dentro de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="38970-112">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="38970-113">No se permiten las combinaciones entre bases de datos.</span><span class="sxs-lookup"><span data-stu-id="38970-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="38970-114">Por lo tanto, SQL Data Warehouse espera que todas las tablas utilizadas por el almacenamiento de datos se almacenen en una única base de datos.</span><span class="sxs-lookup"><span data-stu-id="38970-114">Therefore, SQL Data Warehouse expects all tables used by the data warehouse to be stored within the one database.</span></span>

<span data-ttu-id="38970-115">Se recomienda usar esquemas definidos por el usuario para consolidar la carga de trabajo existente en una sola base de datos.</span><span class="sxs-lookup"><span data-stu-id="38970-115">We recommend using user-defined schemas to consolidate your existing workload into one database.</span></span> <span data-ttu-id="38970-116">Para ver ejemplos, consulte [Esquemas definidos por el usuario](sql-data-warehouse-develop-user-defined-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="38970-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="38970-117">Uso de tipos de datos compatibles</span><span class="sxs-lookup"><span data-stu-id="38970-117">Use compatible data types</span></span>
<span data-ttu-id="38970-118">Modifique los tipos de datos para que sean compatibles con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="38970-118">Modify your data types to be compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="38970-119">Para ver una lista de tipos de datos admitidos y no admitidos, consulte el artículo sobre [tipos de datos][data types].</span><span class="sxs-lookup"><span data-stu-id="38970-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="38970-120">En ese tema, se proporcionan soluciones alternativas para los tipos no compatibles.</span><span class="sxs-lookup"><span data-stu-id="38970-120">That topic gives workarounds for the unsupported types.</span></span> <span data-ttu-id="38970-121">También se proporciona una consulta para identificar tipos existentes que no se admitan en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="38970-121">It also provides a query to identify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="38970-122">Minimización del tamaño de fila</span><span class="sxs-lookup"><span data-stu-id="38970-122">Minimize row size</span></span>
<span data-ttu-id="38970-123">Para lograr un rendimiento óptimo, minimice la longitud de fila de las tablas.</span><span class="sxs-lookup"><span data-stu-id="38970-123">For best performance, minimize the row length of your tables.</span></span> <span data-ttu-id="38970-124">Dado que las longitudes de fila más cortas conducen a un mejor rendimiento, use los tipos de datos más pequeños que funcionen para los datos.</span><span class="sxs-lookup"><span data-stu-id="38970-124">Since shorter row lengths lead to better performance, use the smallest data types that work for your data.</span></span> 

<span data-ttu-id="38970-125">Para el ancho de fila de tabla, PolyBase tiene un límite de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="38970-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="38970-126">Si tiene previsto cargar datos en SQL Data Warehouse con PolyBase, actualice las tablas para que el ancho máximo de la fila sea de menos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="38970-126">If you plan to load data into SQL Data Warehouse with PolyBase, update your tables to have maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but the largest possible size of the row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and the defined row width is less than one MB. When loading rows, PolyBase allocates the full length of the variable-length data. The full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-the-distribution-option"></a><span data-ttu-id="38970-127">Especificación de la opción de distribución</span><span class="sxs-lookup"><span data-stu-id="38970-127">Specify the distribution option</span></span>
<span data-ttu-id="38970-128">SQL Data Warehouse es un sistema de base de datos distribuida.</span><span class="sxs-lookup"><span data-stu-id="38970-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="38970-129">Cada tabla se distribuye o se replica en todos los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="38970-129">Each table is distributed or replicated across the Compute nodes.</span></span> <span data-ttu-id="38970-130">Hay una opción de tabla que le permite especificar cómo distribuir los datos.</span><span class="sxs-lookup"><span data-stu-id="38970-130">There's a table option that lets you specify how to distribute the data.</span></span> <span data-ttu-id="38970-131">Las opciones son round robin, replicada o distribuida por hash.</span><span class="sxs-lookup"><span data-stu-id="38970-131">The choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="38970-132">Cada una tiene ventajas y desventajas.</span><span class="sxs-lookup"><span data-stu-id="38970-132">Each has pros and cons.</span></span> <span data-ttu-id="38970-133">Si no se especifica la opción de distribución, SQL Data Warehouse usará round robin como valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="38970-133">If you don't specify the distribution option, SQL Data Warehouse will use round-robin as the default.</span></span>

- <span data-ttu-id="38970-134">Round robin es el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="38970-134">Round-robin is the default.</span></span> <span data-ttu-id="38970-135">Es la más sencilla de usar y carga los datos lo más rápido posible, pero las combinaciones requerirán que se muevan los datos, lo que reduce el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="38970-135">It is the simplest to use, and loads the data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="38970-136">Replicada almacena una copia de la tabla en cada nodo de proceso.</span><span class="sxs-lookup"><span data-stu-id="38970-136">Replicated stores a copy of the table on each Compute node.</span></span> <span data-ttu-id="38970-137">Las tablas replicadas tienen buen rendimiento porque no requieren que se muevan datos para las combinaciones y agregaciones.</span><span class="sxs-lookup"><span data-stu-id="38970-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="38970-138">Sí requieren almacenamiento adicional y, por lo tanto, funcionan mejor con tablas más pequeñas.</span><span class="sxs-lookup"><span data-stu-id="38970-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="38970-139">Distribuida por hash distribuye las filas en todos los nodos mediante una función hash.</span><span class="sxs-lookup"><span data-stu-id="38970-139">Hash distributed distributes the rows across all the nodes via a hash function.</span></span> <span data-ttu-id="38970-140">Las tablas distribuidas por hash son la esencia de SQL Data Warehouse, ya que están diseñadas para proporcionar un rendimiento elevado de consultas en tablas grandes.</span><span class="sxs-lookup"><span data-stu-id="38970-140">Hash distributed tables are the heart of SQL Data Warehouse since they are designed to provide high query performance on large tables.</span></span> <span data-ttu-id="38970-141">Esta opción requiere cierto planeamiento para seleccionar la mejor columna en la que distribuir los datos.</span><span class="sxs-lookup"><span data-stu-id="38970-141">This option requires some planning to select the best column on which to distribute the data.</span></span> <span data-ttu-id="38970-142">Sin embargo, si no elige la mejor columna la primera vez, se pueden volver a distribuir fácilmente los datos en una columna diferente.</span><span class="sxs-lookup"><span data-stu-id="38970-142">However, if you don't choose the best column the first time, you can easily re-distribute the data on a different column.</span></span> 

<span data-ttu-id="38970-143">Para elegir la mejor opción de distribución para cada tabla, consulte [Tablas distribuidas](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="38970-143">To choose the best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="38970-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="38970-144">Next steps</span></span>
<span data-ttu-id="38970-145">Una vez migrado correctamente el esquema de base de datos al Almacenamiento de datos SQL, continúe con uno de los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="38970-145">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span></span>

* <span data-ttu-id="38970-146">[Migración de los datos][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="38970-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="38970-147">[Migración del código][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="38970-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="38970-148">Para obtener más información sobre los procedimientos recomendados de SQL Data Warehouse, consulte el artículo sobre [procedimientos recomendados][best practices].</span><span class="sxs-lookup"><span data-stu-id="38970-148">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
