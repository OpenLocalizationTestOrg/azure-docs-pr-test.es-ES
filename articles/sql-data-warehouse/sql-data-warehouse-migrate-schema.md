---
title: aaaMigrate el almacenamiento de datos de esquema tooSQL | Documentos de Microsoft
description: Sugerencias para migrar el almacenamiento de datos SQL de esquema tooAzure para desarrollar soluciones.
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
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a><span data-ttu-id="e660a-103">Migrar el almacenamiento de datos de esquemas tooSQL</span><span class="sxs-lookup"><span data-stu-id="e660a-103">Migrate your schemas tooSQL Data Warehouse</span></span>
<span data-ttu-id="e660a-104">Orientación para migrar su tooSQL de esquemas almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e660a-104">Guidance for migrating your SQL schemas tooSQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="e660a-105">Planeamiento de la migración del esquema</span><span class="sxs-lookup"><span data-stu-id="e660a-105">Plan your schema migration</span></span>

<span data-ttu-id="e660a-106">Cuando planee una migración, vea hello [información general de la tabla] [ table overview] toobecome familiarizado con las consideraciones de diseño de tabla, como las estadísticas de distribución, particiones e índices.</span><span class="sxs-lookup"><span data-stu-id="e660a-106">As you plan a migration, see hello [table overview][table overview] toobecome familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="e660a-107">También se incluyen algunas [características no admitidas de las tablas][unsupported table features] y las soluciones alternativas a tales carencias.</span><span class="sxs-lookup"><span data-stu-id="e660a-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a><span data-ttu-id="e660a-108">Usar bases de datos de esquemas definidos por el usuario tooconsolidate</span><span class="sxs-lookup"><span data-stu-id="e660a-108">Use user-defined schemas tooconsolidate databases</span></span>

<span data-ttu-id="e660a-109">Probablemente, su carga de trabajo existente tiene más de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="e660a-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="e660a-110">Por ejemplo, un almacenamiento de datos de SQL Server podría incluir una base de datos provisional, una de almacenamiento de datos y algunas de tipo data mart.</span><span class="sxs-lookup"><span data-stu-id="e660a-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="e660a-111">En esta topología, cada base de datos se ejecuta como una carga de trabajo independiente con directivas de seguridad distintas.</span><span class="sxs-lookup"><span data-stu-id="e660a-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="e660a-112">Por el contrario, el almacenamiento de datos SQL se ejecuta como carga de trabajo del almacenamiento de datos todo de hello dentro de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="e660a-112">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="e660a-113">No se permiten las combinaciones entre bases de datos.</span><span class="sxs-lookup"><span data-stu-id="e660a-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="e660a-114">Por lo tanto, almacenamiento de datos de SQL espera que todas las tablas utilizadas por toobe de almacenamiento de datos de hello almacenado en una base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e660a-114">Therefore, SQL Data Warehouse expects all tables used by hello data warehouse toobe stored within hello one database.</span></span>

<span data-ttu-id="e660a-115">Se recomienda utilizar esquemas definidos por el usuario tooconsolidate la carga de trabajo existente en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="e660a-115">We recommend using user-defined schemas tooconsolidate your existing workload into one database.</span></span> <span data-ttu-id="e660a-116">Para ver ejemplos, consulte [Esquemas definidos por el usuario](sql-data-warehouse-develop-user-defined-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="e660a-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="e660a-117">Uso de tipos de datos compatibles</span><span class="sxs-lookup"><span data-stu-id="e660a-117">Use compatible data types</span></span>
<span data-ttu-id="e660a-118">Modifique la toobe de tipos de datos compatible con el almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="e660a-118">Modify your data types toobe compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="e660a-119">Para ver una lista de tipos de datos admitidos y no admitidos, consulte el artículo sobre [tipos de datos][data types].</span><span class="sxs-lookup"><span data-stu-id="e660a-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="e660a-120">Ese tema proporciona soluciones alternativas para los tipos de hello no admitido.</span><span class="sxs-lookup"><span data-stu-id="e660a-120">That topic gives workarounds for hello unsupported types.</span></span> <span data-ttu-id="e660a-121">También proporciona una consulta tooidentify tipos existentes que no se admiten en el almacén de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="e660a-121">It also provides a query tooidentify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="e660a-122">Minimización del tamaño de fila</span><span class="sxs-lookup"><span data-stu-id="e660a-122">Minimize row size</span></span>
<span data-ttu-id="e660a-123">Para obtener el mejor rendimiento, minimizar Hola fila con longitud de las tablas.</span><span class="sxs-lookup"><span data-stu-id="e660a-123">For best performance, minimize hello row length of your tables.</span></span> <span data-ttu-id="e660a-124">Puesto que longitudes de fila más cortos conducen toobetter rendimiento, usar los datos más pequeños Hola que funcionan para los datos.</span><span class="sxs-lookup"><span data-stu-id="e660a-124">Since shorter row lengths lead toobetter performance, use hello smallest data types that work for your data.</span></span> 

<span data-ttu-id="e660a-125">Para el ancho de fila de tabla, PolyBase tiene un límite de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e660a-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="e660a-126">Si tiene previsto datos tooload en almacenamiento de datos de SQL con PolyBase, actualice los anchos de máximo de filas de tablas toohave de menos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e660a-126">If you plan tooload data into SQL Data Warehouse with PolyBase, update your tables toohave maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a><span data-ttu-id="e660a-127">Especifique la opción de distribución de Hola</span><span class="sxs-lookup"><span data-stu-id="e660a-127">Specify hello distribution option</span></span>
<span data-ttu-id="e660a-128">SQL Data Warehouse es un sistema de base de datos distribuida.</span><span class="sxs-lookup"><span data-stu-id="e660a-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="e660a-129">Cada tabla se distribuyen o se replican a través de nodos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="e660a-129">Each table is distributed or replicated across hello Compute nodes.</span></span> <span data-ttu-id="e660a-130">Hay una opción de tabla que le permite especificar cómo toodistribute Hola datos.</span><span class="sxs-lookup"><span data-stu-id="e660a-130">There's a table option that lets you specify how toodistribute hello data.</span></span> <span data-ttu-id="e660a-131">Opciones de Hello tienen round-robin, replicación, o está distribuido hash.</span><span class="sxs-lookup"><span data-stu-id="e660a-131">hello choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="e660a-132">Cada una tiene ventajas y desventajas.</span><span class="sxs-lookup"><span data-stu-id="e660a-132">Each has pros and cons.</span></span> <span data-ttu-id="e660a-133">Si no especifica la opción de distribución de hello, almacenamiento de datos de SQL utilizará round robin como valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e660a-133">If you don't specify hello distribution option, SQL Data Warehouse will use round-robin as hello default.</span></span>

- <span data-ttu-id="e660a-134">Round-robin es predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e660a-134">Round-robin is hello default.</span></span> <span data-ttu-id="e660a-135">Se toouse más sencilla de Hola y carga los datos de hello lo más rápidos posible, pero las combinaciones requerirá el movimiento de datos que reduce el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="e660a-135">It is hello simplest toouse, and loads hello data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="e660a-136">Replicada almacena una copia de la tabla de hello en cada nodo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="e660a-136">Replicated stores a copy of hello table on each Compute node.</span></span> <span data-ttu-id="e660a-137">Las tablas replicadas tienen buen rendimiento porque no requieren que se muevan datos para las combinaciones y agregaciones.</span><span class="sxs-lookup"><span data-stu-id="e660a-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="e660a-138">Sí requieren almacenamiento adicional y, por lo tanto, funcionan mejor con tablas más pequeñas.</span><span class="sxs-lookup"><span data-stu-id="e660a-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="e660a-139">Hash distribuida distribuye filas de Hola a todos los nodos de Hola a través de una función hash.</span><span class="sxs-lookup"><span data-stu-id="e660a-139">Hash distributed distributes hello rows across all hello nodes via a hash function.</span></span> <span data-ttu-id="e660a-140">Las tablas hash distribuida son la esencia de Hola de almacenamiento de datos SQL ya que son tooprovide diseñada consulta alto rendimiento en tablas grandes.</span><span class="sxs-lookup"><span data-stu-id="e660a-140">Hash distributed tables are hello heart of SQL Data Warehouse since they are designed tooprovide high query performance on large tables.</span></span> <span data-ttu-id="e660a-141">Esta opción requiere algunos planificación tooselect Hola mejor columna acerca de qué datos de hello toodistribute.</span><span class="sxs-lookup"><span data-stu-id="e660a-141">This option requires some planning tooselect hello best column on which toodistribute hello data.</span></span> <span data-ttu-id="e660a-142">Sin embargo, si no elige Hola Hola de columna mejor primera vez, se pueden volver a distribuir fácilmente datos de hello en una columna diferente.</span><span class="sxs-lookup"><span data-stu-id="e660a-142">However, if you don't choose hello best column hello first time, you can easily re-distribute hello data on a different column.</span></span> 

<span data-ttu-id="e660a-143">opción toochoose Hola de distribución recomendado para cada tabla, vea [distribuidas tablas](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="e660a-143">toochoose hello best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e660a-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e660a-144">Next steps</span></span>
<span data-ttu-id="e660a-145">Una vez que haya migrado correctamente su tooSQL de esquema de base de datos almacén de datos, continúe tooone de hello siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="e660a-145">Once you have successfully migrated your database schema tooSQL Data Warehouse, proceed tooone of hello following articles:</span></span>

* <span data-ttu-id="e660a-146">[Migración de los datos][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="e660a-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="e660a-147">[Migración del código][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="e660a-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="e660a-148">Para obtener más información sobre los procedimientos recomendados de almacenamiento de datos SQL, vea hello [prácticas recomendadas] [ best practices] artículo.</span><span class="sxs-lookup"><span data-stu-id="e660a-148">For more about SQL Data Warehouse best practices, see hello [best practices][best practices] article.</span></span>

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
