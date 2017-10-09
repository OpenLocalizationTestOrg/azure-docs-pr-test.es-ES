---
title: aaaScale una base de datos SQL de Azure | Documentos de Microsoft
description: "¿Cómo toouse Hola ShardMapManager, biblioteca de cliente de base de datos elástica"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a><span data-ttu-id="24d29-103">Escalar horizontalmente bases de datos con el Administrador de mapa de particiones de Hola</span><span class="sxs-lookup"><span data-stu-id="24d29-103">Scale out databases with hello shard map manager</span></span>
<span data-ttu-id="24d29-104">tooeasily escalada bases de datos de SQL Azure, utilice un administrador de mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-104">tooeasily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="24d29-105">el Administrador de mapa de particiones de Hello es una base de datos especial que mantiene la información de asignación global acerca de todas las particiones (bases de datos) en un conjunto de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-105">hello shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="24d29-106">Hola de metadatos permite a una aplicación tooconnect toohello base de datos correcta en función de valor de Hola de hello **clave de particionamiento**.</span><span class="sxs-lookup"><span data-stu-id="24d29-106">hello metadata allows an application tooconnect toohello correct database based upon hello value of hello **sharding key**.</span></span> <span data-ttu-id="24d29-107">Además, cada partición en conjunto hello contiene asignaciones que realizan el seguimiento de datos de la partición local de hello (conocido como **shardlets**).</span><span class="sxs-lookup"><span data-stu-id="24d29-107">In addition, every shard in hello set contains maps that track hello local shard data (known as **shardlets**).</span></span> 

![Administración de mapas de particiones.](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="24d29-109">Descripción de cómo se construyen estas asignaciones es esencial tooshard de administración de mapa.</span><span class="sxs-lookup"><span data-stu-id="24d29-109">Understanding how these maps are constructed is essential tooshard map management.</span></span> <span data-ttu-id="24d29-110">Esto se realiza mediante hello [ShardMapManager clase](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), que se encuentra en hello [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md) toomanage partición se asigna.</span><span class="sxs-lookup"><span data-stu-id="24d29-110">This is done using hello [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in hello [Elastic Database client library](sql-database-elastic-database-client-library.md) toomanage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="24d29-111">Mapas de particiones y asignaciones de particiones</span><span class="sxs-lookup"><span data-stu-id="24d29-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="24d29-112">Para cada partición, debe seleccionar tipo de Hola de toocreate de mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-112">For each shard, you must select hello type of shard map toocreate.</span></span> <span data-ttu-id="24d29-113">elección de Hello depende de la arquitectura de base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="24d29-113">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="24d29-114">Un solo inquilino por base de datos</span><span class="sxs-lookup"><span data-stu-id="24d29-114">Single tenant per database</span></span>  
2. <span data-ttu-id="24d29-115">Varios inquilinos por base de datos (dos tipos):</span><span class="sxs-lookup"><span data-stu-id="24d29-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="24d29-116">Asignación de lista</span><span class="sxs-lookup"><span data-stu-id="24d29-116">List mapping</span></span>
   2. <span data-ttu-id="24d29-117">Asignación de intervalo</span><span class="sxs-lookup"><span data-stu-id="24d29-117">Range mapping</span></span>

<span data-ttu-id="24d29-118">Para un modelo de un solo inquilino, cree un mapa de particiones de **asignación de lista** .</span><span class="sxs-lookup"><span data-stu-id="24d29-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="24d29-119">modelo de Hello único inquilino asigna una base de datos por inquilino.</span><span class="sxs-lookup"><span data-stu-id="24d29-119">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="24d29-120">Se trata de un modelo eficaz para desarrolladores de SaaS, pues simplifica la administración.</span><span class="sxs-lookup"><span data-stu-id="24d29-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Asignación de lista][1]

<span data-ttu-id="24d29-122">modelo de varios inquilinos de Hello asigna a varios inquilinos tooa única base de datos (y grupos de inquilinos puede distribuir a través de varias bases de datos).</span><span class="sxs-lookup"><span data-stu-id="24d29-122">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="24d29-123">Use este modelo cuando espera que necesitan cada datos pequeños de toohave de inquilino.</span><span class="sxs-lookup"><span data-stu-id="24d29-123">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="24d29-124">En este modelo, se asigna un intervalo de los inquilinos tooa base de datos usando **asignación de intervalo**.</span><span class="sxs-lookup"><span data-stu-id="24d29-124">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Asignación de intervalo][2]

<span data-ttu-id="24d29-126">O puede implementar un modelo de base de datos de varios inquilinos mediante un *asignación de lista* tooassign varios inquilinos tooa única base de datos.</span><span class="sxs-lookup"><span data-stu-id="24d29-126">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="24d29-127">Por ejemplo, DB1 es toostore usa información acerca del Id. de inquilino 1 y 5, y DB2 almacena los datos de inquilino 10 e inquilino 7.</span><span class="sxs-lookup"><span data-stu-id="24d29-127">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Varios inquilinos en una sola base de datos][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="24d29-129">Tipos .NET admitidos para claves de particionamiento</span><span class="sxs-lookup"><span data-stu-id="24d29-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="24d29-130">Hola de soporte técnico de escala elástica después de .net Framework los tipos como claves de particionamiento:</span><span class="sxs-lookup"><span data-stu-id="24d29-130">Elastic Scale support hello following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="24d29-131">integer</span><span class="sxs-lookup"><span data-stu-id="24d29-131">integer</span></span>
* <span data-ttu-id="24d29-132">long</span><span class="sxs-lookup"><span data-stu-id="24d29-132">long</span></span>
* <span data-ttu-id="24d29-133">guid</span><span class="sxs-lookup"><span data-stu-id="24d29-133">guid</span></span>
* <span data-ttu-id="24d29-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="24d29-134">byte[]</span></span>  
* <span data-ttu-id="24d29-135">datetime</span><span class="sxs-lookup"><span data-stu-id="24d29-135">datetime</span></span>
* <span data-ttu-id="24d29-136">timespan</span><span class="sxs-lookup"><span data-stu-id="24d29-136">timespan</span></span>
* <span data-ttu-id="24d29-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="24d29-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="24d29-138">Mapas de particiones de lista y de intervalo</span><span class="sxs-lookup"><span data-stu-id="24d29-138">List and range shard maps</span></span>
<span data-ttu-id="24d29-139">Los mapas de particiones se pueden construir mediante **listas de valores individuales de clave de particionamiento**, o por medio de **intervalos de valores de clave de particionamiento**.</span><span class="sxs-lookup"><span data-stu-id="24d29-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="24d29-140">Mapas de particiones de lista</span><span class="sxs-lookup"><span data-stu-id="24d29-140">List shard maps</span></span>
<span data-ttu-id="24d29-141">**Particiones** contienen **shardlets** y asignación de Hola de shardlets tooshards se mantiene un mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-141">**Shards** contain **shardlets** and hello mapping of shardlets tooshards is maintained by a shard map.</span></span> <span data-ttu-id="24d29-142">A **mapa de particiones de lista** es una asociación entre los valores clave individuales Hola que identifican hello shardlets y bases de datos de Hola que actúan como particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-142">A **list shard map** is an association between hello individual key values that identify hello shardlets and hello databases that serve as shards.</span></span>  <span data-ttu-id="24d29-143">**Enumerar asignaciones** explícitas y distintos valores de clave pueden ser asignado toohello misma base de datos.</span><span class="sxs-lookup"><span data-stu-id="24d29-143">**List mappings** are explicit and different key values can be mapped toohello same database.</span></span> <span data-ttu-id="24d29-144">Por ejemplo, la clave 1 asigna tooDatabase A y B. de base de datos hacen referencia a valores de clave 3 y 6</span><span class="sxs-lookup"><span data-stu-id="24d29-144">For example, key 1 maps tooDatabase A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="24d29-145">Clave</span><span class="sxs-lookup"><span data-stu-id="24d29-145">Key</span></span> | <span data-ttu-id="24d29-146">Ubicación de la partición</span><span class="sxs-lookup"><span data-stu-id="24d29-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="24d29-147">1</span><span class="sxs-lookup"><span data-stu-id="24d29-147">1</span></span> |<span data-ttu-id="24d29-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="24d29-148">Database_A</span></span> |
| <span data-ttu-id="24d29-149">3</span><span class="sxs-lookup"><span data-stu-id="24d29-149">3</span></span> |<span data-ttu-id="24d29-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="24d29-150">Database_B</span></span> |
| <span data-ttu-id="24d29-151">4</span><span class="sxs-lookup"><span data-stu-id="24d29-151">4</span></span> |<span data-ttu-id="24d29-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="24d29-152">Database_C</span></span> |
| <span data-ttu-id="24d29-153">6</span><span class="sxs-lookup"><span data-stu-id="24d29-153">6</span></span> |<span data-ttu-id="24d29-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="24d29-154">Database_B</span></span> |
| <span data-ttu-id="24d29-155">...</span><span class="sxs-lookup"><span data-stu-id="24d29-155">...</span></span> |<span data-ttu-id="24d29-156">...</span><span class="sxs-lookup"><span data-stu-id="24d29-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="24d29-157">Mapas de particiones de intervalo</span><span class="sxs-lookup"><span data-stu-id="24d29-157">Range shard maps</span></span>
<span data-ttu-id="24d29-158">En un **mapa de particiones de intervalo**, intervalo de claves de Hola se describe mediante un par **[valor bajo, alto valor)** donde Hola *bajo valor* es clave mínimo de hello en el intervalo de Hola y Hola *Valor alto* es Hola primer valor mayor que el intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="24d29-158">In a **range shard map**, hello key range is described by a pair **[Low Value, High Value)** where hello *Low Value* is hello minimum key in hello range, and hello *High Value* is hello first value higher than hello range.</span></span> 

<span data-ttu-id="24d29-159">Por ejemplo **[0, 100)** incluye todos los números enteros que son mayores o iguales que 0 y menores que 100.</span><span class="sxs-lookup"><span data-stu-id="24d29-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="24d29-160">Tenga en cuenta que se admiten varios intervalos can punto toohello misma base de datos y discontinuas intervalos (por ejemplo, [100,200) y [400,600) ambos tooDatabase punto C en el siguiente ejemplo de Hola.)</span><span class="sxs-lookup"><span data-stu-id="24d29-160">Note that multiple ranges can point toohello same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point tooDatabase C in hello example below.)</span></span>

| <span data-ttu-id="24d29-161">Clave</span><span class="sxs-lookup"><span data-stu-id="24d29-161">Key</span></span> | <span data-ttu-id="24d29-162">Ubicación de la partición</span><span class="sxs-lookup"><span data-stu-id="24d29-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="24d29-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="24d29-163">[1,50)</span></span> |<span data-ttu-id="24d29-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="24d29-164">Database_A</span></span> |
| <span data-ttu-id="24d29-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="24d29-165">[50,100)</span></span> |<span data-ttu-id="24d29-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="24d29-166">Database_B</span></span> |
| <span data-ttu-id="24d29-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="24d29-167">[100,200)</span></span> |<span data-ttu-id="24d29-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="24d29-168">Database_C</span></span> |
| <span data-ttu-id="24d29-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="24d29-169">[400,600)</span></span> |<span data-ttu-id="24d29-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="24d29-170">Database_C</span></span> |
| <span data-ttu-id="24d29-171">...</span><span class="sxs-lookup"><span data-stu-id="24d29-171">...</span></span> |<span data-ttu-id="24d29-172">...</span><span class="sxs-lookup"><span data-stu-id="24d29-172">...</span></span> |

<span data-ttu-id="24d29-173">Cada una de las tablas de hello mostradas anteriormente es un ejemplo conceptual de un **ShardMap** objeto.</span><span class="sxs-lookup"><span data-stu-id="24d29-173">Each of hello tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="24d29-174">Cada fila es un ejemplo simplificado de una persona **PointMapping** (para el mapa de particiones de la lista de hello) o **RangeMapping** (para el mapa de particiones de intervalo de hello) objetos.</span><span class="sxs-lookup"><span data-stu-id="24d29-174">Each row is a simplified example of an individual **PointMapping** (for hello list shard map) or **RangeMapping** (for hello range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="24d29-175">Administrador de mapas de particiones</span><span class="sxs-lookup"><span data-stu-id="24d29-175">Shard map manager</span></span>
<span data-ttu-id="24d29-176">En la biblioteca de cliente de Hola, Administrador de mapa de particiones de hello es una colección de asignaciones de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-176">In hello client library, hello shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="24d29-177">Hola datos administrados por un **ShardMapManager** instancia se mantiene en tres lugares:</span><span class="sxs-lookup"><span data-stu-id="24d29-177">hello data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="24d29-178">**Mapa de particiones global (GSM)**: especificar un tooserve de base de datos como repositorio de Hola para todos sus asignaciones de particiones y asignaciones.</span><span class="sxs-lookup"><span data-stu-id="24d29-178">**Global Shard Map (GSM)**: You specify a database tooserve as hello repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="24d29-179">Tablas especiales y los procedimientos almacenados se crean automáticamente información de hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="24d29-179">Special tables and stored procedures are automatically created toomanage hello information.</span></span> <span data-ttu-id="24d29-180">Esto suele ser una pequeña base de datos y con menos acceso, y no debe usarse para otras necesidades de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="24d29-180">This is typically a small database and lightly accessed, and it should not be used for other needs of hello application.</span></span> <span data-ttu-id="24d29-181">Hello tablas están en un esquema especial llamado **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="24d29-181">hello tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="24d29-182">**Mapa de particiones locales (LSM)**: cada base de datos que especifique toobe una partición es modifica toocontain varias tablas pequeñas y los procedimientos almacenados especiales que contienen y administración particiones de toothat específico de información de mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-182">**Local Shard Map (LSM)**: Every database that you specify toobe a shard is modified toocontain several small tables and special stored procedures that contain and manage shard map information specific toothat shard.</span></span> <span data-ttu-id="24d29-183">Esta información es redundante con información de Hola Hola GSM y permite información de la asignación de particiones de hello aplicación toovalidate almacenado en memoria caché sin incluir ninguna carga en hello GSM; aplicación Hello usa Hola LSM toodetermine si una asignación almacenada en caché sigue siendo válida.</span><span class="sxs-lookup"><span data-stu-id="24d29-183">This information is redundant with hello information in hello GSM, and it allows hello application toovalidate cached shard map information without placing any load on hello GSM; hello application uses hello LSM toodetermine if a cached mapping is still valid.</span></span> <span data-ttu-id="24d29-184">Hola tablas correspondiente toohello LSM en cada partición también están en el esquema de hello **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="24d29-184">hello tables corresponding toohello LSM on each shard are also in hello schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="24d29-185">**Caché de aplicación**: cada instancia de la aplicación que accede a un objeto **ShardMapManager** mantiene una caché en memoria local de sus asignaciones.</span><span class="sxs-lookup"><span data-stu-id="24d29-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="24d29-186">Almacena información de enrutamiento que recientemente se ha recuperado.</span><span class="sxs-lookup"><span data-stu-id="24d29-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="24d29-187">Construcción de un ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="24d29-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="24d29-188">Un objeto **ShardMapManager** se construye mediante un patrón de [fábrica](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) .</span><span class="sxs-lookup"><span data-stu-id="24d29-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="24d29-189">Hola  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  método toma las credenciales (incluido el nombre del servidor de Hola y el nombre de base de datos que contiene Hola GSM) en forma de Hola de un  **ConnectionString** y devuelve una instancia de un **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="24d29-189">hello **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including hello server name and database name holding hello GSM) in hello form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="24d29-190">**Tenga en cuenta:** hello **ShardMapManager** deberían crear instancias de una sola vez por cada dominio de aplicación, en el código de inicialización de Hola para una aplicación.</span><span class="sxs-lookup"><span data-stu-id="24d29-190">**Please Note:** hello **ShardMapManager** should be instantiated only once per app domain, within hello initialization code for an application.</span></span> <span data-ttu-id="24d29-191">Creación de instancias adicionales de ShardMapManager Hola mismo appdomain, dará como resultado una mayor memoria y uso de CPU de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="24d29-191">Creation of additional instances of ShardMapManager in hello same appdomain, will result in increased memory and CPU utilization of hello application.</span></span> <span data-ttu-id="24d29-192">Un objeto **ShardMapManager** puede contener cualquier número de mapas de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="24d29-193">Aunque un solo mapa de particiones puede ser suficiente para muchas aplicaciones, hay veces en que se usan diferentes conjuntos de bases de datos para un esquema diferente o con fines únicos y, en esos casos, puede que sea preferible usar varios mapas de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="24d29-194">En este código, una aplicación intente tooopen existente **ShardMapManager** con hello [TryGetSqlShardMapManager método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="24d29-194">In this code, an application tries tooopen an existing **ShardMapManager** with hello [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="24d29-195">Si los objetos que representan un Global **ShardMapManager** (GSM) todavía no existe dentro de la base de datos de hello, biblioteca de cliente de hello crea existe con hello [CreateSqlShardMapManager método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="24d29-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside hello database, hello client library creates them there using hello [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

<span data-ttu-id="24d29-196">Como alternativa, puede usar Powershell toocreate un nuevo administrador de mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-196">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="24d29-197">Hay un ejemplo disponible [aquí](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="24d29-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="24d29-198">Obtención de las clases RangeShardMap o ListShardMap</span><span class="sxs-lookup"><span data-stu-id="24d29-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="24d29-199">Después de crear una partición en el Administrador de mapa, puede obtener hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) o [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) con hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), o hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="24d29-199">After creating a shard map manager, you can get hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="24d29-200">Credenciales de administración de mapas de particiones</span><span class="sxs-lookup"><span data-stu-id="24d29-200">Shard map administration credentials</span></span>
<span data-ttu-id="24d29-201">Las aplicaciones que administración y manipulan los mapas de particiones son diferentes de los que usan conexiones de tooroute de mapas de particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d29-201">Applications that administer and manipulate shard maps are different from those that use hello shard maps tooroute connections.</span></span> 

<span data-ttu-id="24d29-202">partición tooadminister se asigna (Agregar o cambiar particiones, mapas de particiones, las asignaciones de particiones, etc.) debe crear instancias de hello **ShardMapManager** con **las credenciales que tienen privilegios en ambas bases de datos GSM hello y en cada una de lectura/escritura base de datos que actúa como una partición**.</span><span class="sxs-lookup"><span data-stu-id="24d29-202">tooadminister shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate hello **ShardMapManager** using **credentials that have read/write privileges on both hello GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="24d29-203">las credenciales de Hello deben permitir para operaciones de escritura en tablas de hello en ambos Hola GSM y LSM como información de la asignación de particiones se especifica o se cambia, así como para crear tablas LSM en nuevas particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-203">hello credentials must allow for writes against hello tables in both hello GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="24d29-204">Vea [credenciales usan la biblioteca de cliente de base de datos elástica tooaccess hello](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="24d29-204">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="24d29-205">Solo los metadatos afectados</span><span class="sxs-lookup"><span data-stu-id="24d29-205">Only metadata affected</span></span>
<span data-ttu-id="24d29-206">Métodos que se utilizan para rellenar o cambiar hello **ShardMapManager** datos no alteran los datos de usuario de hello almacenados en particiones de Hola por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="24d29-206">Methods used for populating or changing hello **ShardMapManager** data do not alter hello user data stored in hello shards themselves.</span></span> <span data-ttu-id="24d29-207">Por ejemplo, los métodos como **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. afectan a los metadatos de mapa de particiones de hello solo.</span><span class="sxs-lookup"><span data-stu-id="24d29-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect hello shard map metadata only.</span></span> <span data-ttu-id="24d29-208">No, quitar, agregar o modificar los datos de usuario contenidos en particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d29-208">They do not remove, add, or alter user data contained in hello shards.</span></span> <span data-ttu-id="24d29-209">En su lugar, estos métodos son toobe diseñada usa junto con operaciones independientes para realiza toocreate o quitar bases de datos reales, o que mueva las filas de una partición tooanother toorebalance un entorno particionado.</span><span class="sxs-lookup"><span data-stu-id="24d29-209">Instead, these methods are designed toobe used in conjunction with separate operations you perform toocreate or remove actual databases, or that move rows from one shard tooanother toorebalance a sharded environment.</span></span>  <span data-ttu-id="24d29-210">(hello **dividir-combinar** herramienta que se incluye con las herramientas de base de datos elástica hace que el uso de estas API junto con la coordinación de movimiento de datos real entre las particiones.) Vea [escalado mediante la herramienta Hola bases de datos elásticas dividir-combinar](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="24d29-210">(hello **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="24d29-211">Ejemplo de cómo rellenar un mapa de particiones</span><span class="sxs-lookup"><span data-stu-id="24d29-211">Populating a shard map example</span></span>
<span data-ttu-id="24d29-212">A continuación se muestra un ejemplo de secuencia de operaciones toopopulate un mapa de particiones específicos.</span><span class="sxs-lookup"><span data-stu-id="24d29-212">An example sequence of operations toopopulate a specific shard map is shown below.</span></span> <span data-ttu-id="24d29-213">código de Hello realiza estos pasos:</span><span class="sxs-lookup"><span data-stu-id="24d29-213">hello code performs these steps:</span></span> 

1. <span data-ttu-id="24d29-214">Se crea un mapa de particiones en un administrador de mapas de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="24d29-215">se agregan metadatos de Hola para dos particiones diferentes toohello mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-215">hello metadata for two different shards is added toohello shard map.</span></span> 
3. <span data-ttu-id="24d29-216">Se agregan una variedad de asignaciones de intervalo de claves y hello contenido global del mapa de particiones de Hola se muestra.</span><span class="sxs-lookup"><span data-stu-id="24d29-216">A variety of key range mappings are added, and hello overall contents of hello shard map are displayed.</span></span> 

<span data-ttu-id="24d29-217">Hola código está escrito para que el método hello se puede volver a ejecutar si se produce un error.</span><span class="sxs-lookup"><span data-stu-id="24d29-217">hello code is written so that hello method can be rerun if an error occurs.</span></span> <span data-ttu-id="24d29-218">Cada solicitud de prueba si una partición o la asignación ya existe antes de intentar toocreate lo.</span><span class="sxs-lookup"><span data-stu-id="24d29-218">Each request tests whether a shard or mapping already exists, before attempting toocreate it.</span></span> <span data-ttu-id="24d29-219">Hello código supone que las bases de datos denominan **sample_shard_0**, **sample_shard_1** y **sample_shard_2** ya se han creado en el servidor hello encontrada por cadena **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="24d29-219">hello code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in hello server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="24d29-220">Como alternativa puede usar PowerShell scripts hello tooachieve el mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="24d29-220">As an alternative you can use PowerShell scripts tooachieve hello same result.</span></span> <span data-ttu-id="24d29-221">Algunos ejemplos de PowerShell de ejemplo de Hola están disponibles [aquí](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="24d29-221">Some of hello sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="24d29-222">Una vez que se han rellenado los mapas de particiones, aplicaciones de acceso a datos se pueden crear o adaptación toowork con mapas de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d29-222">Once shard maps have been populated, data access applications can be created or adapted toowork with hello maps.</span></span> <span data-ttu-id="24d29-223">Rellenar o manipular Hola mapas no necesita producirse nuevo hasta que **diseño mapa** necesita toochange.</span><span class="sxs-lookup"><span data-stu-id="24d29-223">Populating or manipulating hello maps need not occur again until **map layout** needs toochange.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="24d29-224">Enrutamiento dependiente de los datos</span><span class="sxs-lookup"><span data-stu-id="24d29-224">Data dependent routing</span></span>
<span data-ttu-id="24d29-225">Administrador de mapa de particiones de Hola se usará más en las aplicaciones que requieren operaciones de datos específicos de la aplicación de base de datos conexiones tooperform Hola.</span><span class="sxs-lookup"><span data-stu-id="24d29-225">hello shard map manager will be most used in applications that require database connections tooperform hello app-specific data operations.</span></span> <span data-ttu-id="24d29-226">Estas conexiones deben asociarse con la base de datos correcta Hola.</span><span class="sxs-lookup"><span data-stu-id="24d29-226">Those connections must be associated with hello correct database.</span></span> <span data-ttu-id="24d29-227">Esto se conoce como **Enrutamiento dependiente de los datos**.</span><span class="sxs-lookup"><span data-stu-id="24d29-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="24d29-228">Para estas aplicaciones, instancias de un objeto de administrador de asignación de particiones de generador de hello mediante las credenciales que tienen acceso de solo lectura en la base de datos de hello GSM.</span><span class="sxs-lookup"><span data-stu-id="24d29-228">For these applications, instantiate a shard map manager object from hello factory using credentials that have read-only access on hello GSM database.</span></span> <span data-ttu-id="24d29-229">Las solicitudes individuales para las conexiones posteriores proporcionan las credenciales necesarias para la conexión de base de datos de toohello particiones adecuado.</span><span class="sxs-lookup"><span data-stu-id="24d29-229">Individual requests for later connections supply credentials necessary for connecting toohello appropriate shard database.</span></span>

<span data-ttu-id="24d29-230">Tenga en cuenta que estas aplicaciones (mediante **ShardMapManager** abierto con las credenciales de solo lectura) no se puede realizar cambios toohello asignaciones o asignaciones.</span><span class="sxs-lookup"><span data-stu-id="24d29-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes toohello maps or mappings.</span></span> <span data-ttu-id="24d29-231">Para cubrir esas necesidades, cree aplicaciones específicas de administración o scripts de PowerShell que proporcionen credenciales con más privilegios, como se explicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="24d29-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="24d29-232">Vea [credenciales usan la biblioteca de cliente de base de datos elástica tooaccess hello](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="24d29-232">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="24d29-233">Para obtener más detalles, consulte [Enrutamiento dependiente de datos](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="24d29-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="24d29-234">Modificación de un mapa de particiones</span><span class="sxs-lookup"><span data-stu-id="24d29-234">Modifying a shard map</span></span>
<span data-ttu-id="24d29-235">Un mapa de particiones puede cambiarse de distintas maneras.</span><span class="sxs-lookup"><span data-stu-id="24d29-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="24d29-236">Todos de los siguientes métodos de Hola modifican los metadatos de Hola que describe las particiones de Hola y sus asignaciones, pero físicamente no modifican datos en particiones de hello, ni crear ni se eliminar bases de datos reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d29-236">All of hello following methods modify hello metadata describing hello shards and their mappings, but they do not physically modify data within hello shards, nor do they create or delete hello actual databases.</span></span>  <span data-ttu-id="24d29-237">Algunos de las operaciones de hello en mapa de particiones de Hola que se describe a continuación pueden necesitar toobe coordinada con acciones administrativas que mover físicamente los datos o que agregar y quitar bases de datos que actúa como particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-237">Some of hello operations on hello shard map described below may need toobe coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="24d29-238">Estos métodos funcionan en conjunto como bloques de creación de hello disponibles para modificar Hola distribución global de los datos en su entorno de base de datos particionada.</span><span class="sxs-lookup"><span data-stu-id="24d29-238">These methods work together as hello building blocks available for modifying hello overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="24d29-239">tooadd o quitar particiones: usar  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  y  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  de hello [Shardmap clase](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="24d29-239">tooadd or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of hello [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="24d29-240">Hello servidor y base de datos que representa la partición de destino de hello ya deben existir para estas operaciones tooexecute.</span><span class="sxs-lookup"><span data-stu-id="24d29-240">hello server and database representing hello target shard must already exist for these operations tooexecute.</span></span> <span data-ttu-id="24d29-241">Estos métodos no tiene ningún efecto en hello bases de datos, solo de metadatos en el mapa de particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d29-241">These methods do not have any impact on hello databases themselves, only on metadata in hello shard map.</span></span>
* <span data-ttu-id="24d29-242">toocreate o quitar puntos o intervalos que se asignan toohello particiones: usar  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  de hello [RangeShardMapping clase](https://msdn.microsoft.com/library/azure/dn807318.aspx), y  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  de hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="24d29-242">toocreate or remove points or ranges that are mapped toohello shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of hello [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="24d29-243">Muchos diferentes momentos o intervalos pueden ser asignada toohello misma partición.</span><span class="sxs-lookup"><span data-stu-id="24d29-243">Many different points or ranges can be mapped toohello same shard.</span></span> <span data-ttu-id="24d29-244">Estos métodos solo afectan a los metadatos, no a los datos que puedan existir ya en particiones.</span><span class="sxs-lookup"><span data-stu-id="24d29-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="24d29-245">Si los datos tienen toobe quitado de la base de datos de hello en orden toobe coherente con **DeleteMapping** operaciones, deberá tooperform esas operaciones por separado pero junto con el uso de estos métodos.</span><span class="sxs-lookup"><span data-stu-id="24d29-245">If data needs toobe removed from hello database in order toobe consistent with **DeleteMapping** operations, you will need tooperform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="24d29-246">toosplit rangos existente en dos o mezcla intervalos adyacentes en una sola: usar  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  y  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="24d29-246">toosplit existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="24d29-247">Tenga en cuenta que divide y combinar las operaciones **no cambie la clave de toowhich de hello partición se asignan valores**.</span><span class="sxs-lookup"><span data-stu-id="24d29-247">Note that split and merge operations **do not change hello shard toowhich key values are mapped**.</span></span> <span data-ttu-id="24d29-248">Una división divide un rango existente en dos partes, pero la deja como asignado toohello misma partición.</span><span class="sxs-lookup"><span data-stu-id="24d29-248">A split breaks an existing range into two parts, but leaves both as mapped toohello same shard.</span></span> <span data-ttu-id="24d29-249">Una combinación funciona en los dos intervalos adyacentes que ya están asignada toohello misma partición, fusión de ellas en un solo intervalo.</span><span class="sxs-lookup"><span data-stu-id="24d29-249">A merge operates on two adjacent ranges that are already mapped toohello same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="24d29-250">movimiento de puntos o intervalos de ellos mismos entre las particiones Hello necesita coordinan mediante el uso de toobe **UpdateMapping** junto con el movimiento de datos reales.</span><span class="sxs-lookup"><span data-stu-id="24d29-250">hello movement of points or ranges themselves between shards needs toobe coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="24d29-251">Puede usar hello **dividir y combinar** herramientas del servicio que forma parte de la base de datos elástica cambios en la asignación toocoordinate particiones con el movimiento de datos, cuando se necesita el movimiento.</span><span class="sxs-lookup"><span data-stu-id="24d29-251">You can use hello **Split/Merge** service that is part of elastic database tools toocoordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="24d29-252">mapa de toore (o mover) puntos o intervalos toodifferent particiones individuales: usar  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="24d29-252">toore-map (or move) individual points or ranges toodifferent shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="24d29-253">Puesto que los datos que necesite toobe movido de una partición tooanother en toobe orden coherente con **UpdateMapping** operations, necesitará tooperform este movimiento por separado pero junto con el uso de estos métodos.</span><span class="sxs-lookup"><span data-stu-id="24d29-253">Since data may need toobe moved from one shard tooanother in order toobe consistent with **UpdateMapping** operations, you will need tooperform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="24d29-254">asignaciones de tootake en línea y sin conexión: usar  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  y  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol Hola estado en línea de un asignación.</span><span class="sxs-lookup"><span data-stu-id="24d29-254">tootake mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** toocontrol hello online state of a mapping.</span></span> 
  
    <span data-ttu-id="24d29-255">Solo se permite realizar determinadas operaciones en las asignaciones de particiones cuando una asignación se encuentra en un estado "sin conexión", incluidas **UpdateMapping** y **DeleteMapping**.</span><span class="sxs-lookup"><span data-stu-id="24d29-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="24d29-256">Cuando una asignación está sin conexión, una solicitud dependiente de datos basada en una clave incluida en esa asignación devolverá un error.</span><span class="sxs-lookup"><span data-stu-id="24d29-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="24d29-257">Además, cuando un intervalo en primer lugar se queda sin conexión, todas las particiones de toohello afectada las conexiones se eliminan automáticamente de ordenar tooprevent los resultados incoherentes o incompletos para las consultas dirigidas con intervalos que se va a cambiar.</span><span class="sxs-lookup"><span data-stu-id="24d29-257">In addition, when a range is first taken offline, all connections toohello affected shard are automatically killed in order tooprevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="24d29-258">Las asignaciones son objetos inmutables en .NET</span><span class="sxs-lookup"><span data-stu-id="24d29-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="24d29-259">Todos los métodos de hello anteriores que cambiar las asignaciones de invalidarán también cualquier toothem de referencias en el código.</span><span class="sxs-lookup"><span data-stu-id="24d29-259">All of hello methods above that change mappings also invalidate any references toothem in your code.</span></span> <span data-ttu-id="24d29-260">toomake TI sea más fácil tooperform las secuencias de operaciones que cambian el estado de una asignación, todos los métodos de Hola que cambie una asignación de devuelven una nueva asignación de referencia, por lo que las operaciones se pueden encadenar.</span><span class="sxs-lookup"><span data-stu-id="24d29-260">toomake it easier tooperform sequences of operations that change a mapping’s state, all of hello methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="24d29-261">Por ejemplo, toodelete una asignación de sm shardmap que contiene la clave de hello 25 existente, puede ejecutar Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="24d29-261">For example, toodelete an existing mapping in shardmap sm that contains hello key 25, you can execute hello following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="24d29-262">Incorporación de una partición</span><span class="sxs-lookup"><span data-stu-id="24d29-262">Adding a shard</span></span>
<span data-ttu-id="24d29-263">Las aplicaciones a menudo necesita toosimply agregar nuevos datos de toohandle de particiones que cabe esperar de nuevas claves o intervalos de claves de un mapa de particiones que ya existe.</span><span class="sxs-lookup"><span data-stu-id="24d29-263">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="24d29-264">Por ejemplo, una aplicación particionada por Id. de inquilino puede necesitar tooprovision una nueva partición para un nuevo inquilino o mensual de particiones de datos que necesite una nueva partición aprovisionada antes del inicio de Hola de nuevo cada mes.</span><span class="sxs-lookup"><span data-stu-id="24d29-264">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="24d29-265">Si el nuevo intervalo de valores de clave de hello ya no es parte de una asignación existente y ningún movimiento de datos es necesario, es nueva partición de tooadd muy sencillo Hola y asociar la nueva clave de Hola o particiones de intervalo toothat.</span><span class="sxs-lookup"><span data-stu-id="24d29-265">If hello new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> <span data-ttu-id="24d29-266">Para obtener más información sobre cómo agregar nuevas particiones, consulte [Incorporación de una nueva partición](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="24d29-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="24d29-267">Sin embargo, para escenarios que requieren el movimiento de datos, herramienta Dividir-combinar de hello es necesario tooorchestrate Hola el movimiento de datos entre las particiones en combinación con las actualizaciones de mapas de particiones necesarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="24d29-267">For scenarios that require data movement, however, hello split-merge tool is needed tooorchestrate hello data movement between shards in combination with hello necessary shard map updates.</span></span> <span data-ttu-id="24d29-268">Para obtener más información sobre el uso de hello dividir-combinar yool, consulte [información general de la combinación de división](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="24d29-268">For details on using hello split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
