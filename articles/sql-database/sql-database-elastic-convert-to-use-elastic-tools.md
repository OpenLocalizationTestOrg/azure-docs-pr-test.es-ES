---
title: aaaMigrate existente bases de datos fuera de tooscale | Documentos de Microsoft
description: "Convertir herramientas de bases de datos particionadas toouse elástico de base de datos mediante la creación de un administrador de mapa de particiones"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a><span data-ttu-id="c25b3-103">Migrar tooscale-fuera de las bases de datos existente</span><span class="sxs-lookup"><span data-stu-id="c25b3-103">Migrate existing databases tooscale-out</span></span>
<span data-ttu-id="c25b3-104">Administrar fácilmente la capacidad de ampliación horizontal particionadas bases de datos existentes con herramientas de base de datos de base de datos de SQL Azure (por ejemplo, hello [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="c25b3-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as hello [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="c25b3-105">Primero debe convertir un conjunto existente de Hola de bases de datos toouse [manager de mapa de particiones](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="c25b3-105">You must first convert an existing set of databases toouse hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="c25b3-106">Información general</span><span class="sxs-lookup"><span data-stu-id="c25b3-106">Overview</span></span>
<span data-ttu-id="c25b3-107">toomigrate una base de datos particionada existente:</span><span class="sxs-lookup"><span data-stu-id="c25b3-107">toomigrate an existing sharded database:</span></span> 

1. <span data-ttu-id="c25b3-108">Preparar hello [base de datos de administrador de asignación de particiones](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="c25b3-108">Prepare hello [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="c25b3-109">Crear mapa de particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="c25b3-109">Create hello shard map.</span></span>
3. <span data-ttu-id="c25b3-110">Preparar las particiones individuales Hola.</span><span class="sxs-lookup"><span data-stu-id="c25b3-110">Prepare hello individual shards.</span></span>  
4. <span data-ttu-id="c25b3-111">Agregue el mapa de particiones de toohello de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="c25b3-111">Add mappings toohello shard map.</span></span>

<span data-ttu-id="c25b3-112">Estas técnicas se pueden implementar con cualquier hello [biblioteca de cliente de .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), o los scripts de PowerShell de Hola se encuentran en [base de datos de SQL de Azure: secuencias de comandos de herramientas de base de datos elástica](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="c25b3-112">These techniques can be implemented using either hello [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or hello PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="c25b3-113">ejemplos de Hello aquí usan scripts de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="c25b3-113">hello examples here use hello PowerShell scripts.</span></span>

<span data-ttu-id="c25b3-114">Para obtener más información acerca de hello ShardMapManager, consulte [administración de mapa de particiones](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="c25b3-114">For more information about hello ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="c25b3-115">Para obtener información general de herramientas de base de datos elástica hello, consulte [Introducción a características de base de datos elástica](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c25b3-115">For an overview of hello elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-hello-shard-map-manager-database"></a><span data-ttu-id="c25b3-116">Preparar base de datos de administrador de asignación de hello particiones</span><span class="sxs-lookup"><span data-stu-id="c25b3-116">Prepare hello shard map manager database</span></span>
<span data-ttu-id="c25b3-117">el Administrador de mapa de particiones de Hello es una base de datos especial que contiene las bases de datos de escala horizontal de hello datos toomanage.</span><span class="sxs-lookup"><span data-stu-id="c25b3-117">hello shard map manager is a special database that contains hello data toomanage scaled-out databases.</span></span> <span data-ttu-id="c25b3-118">Puede utilizar una base de datos existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="c25b3-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="c25b3-119">Tenga en cuenta que una base de datos que actúa como administrador de asignación de partición no debe ser Hola misma base de datos como una partición.</span><span class="sxs-lookup"><span data-stu-id="c25b3-119">Note that a database acting as shard map manager should not be hello same database as a shard.</span></span> <span data-ttu-id="c25b3-120">Tenga en cuenta también que script de PowerShell de hello no crear base de datos de Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="c25b3-120">Also note that hello PowerShell script does not create hello database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="c25b3-121">Paso 1: crear un administrador de mapas de particiones</span><span class="sxs-lookup"><span data-stu-id="c25b3-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a><span data-ttu-id="c25b3-122">Administrador de mapa de particiones de hello tooretrieve</span><span class="sxs-lookup"><span data-stu-id="c25b3-122">tooretrieve hello shard map manager</span></span>
<span data-ttu-id="c25b3-123">Después de la creación, puede recuperar el Administrador de mapa de particiones de hello con este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c25b3-123">After creation, you can retrieve hello shard map manager with this cmdlet.</span></span> <span data-ttu-id="c25b3-124">Este paso es necesario cada vez que se necesita toouse hello ShardMapManager objeto.</span><span class="sxs-lookup"><span data-stu-id="c25b3-124">This step is needed every time you need toouse hello ShardMapManager object.</span></span>

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a><span data-ttu-id="c25b3-125">Paso 2: crear el mapa de particiones de Hola</span><span class="sxs-lookup"><span data-stu-id="c25b3-125">Step 2: create hello shard map</span></span>
<span data-ttu-id="c25b3-126">Debe seleccionar tipo de Hola de toocreate de mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="c25b3-126">You must select hello type of shard map toocreate.</span></span> <span data-ttu-id="c25b3-127">elección de Hello depende de la arquitectura de base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="c25b3-127">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="c25b3-128">Un inquilino por base de datos (para obtener términos, vea hello [glosario](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="c25b3-128">Single tenant per database (For terms, see hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="c25b3-129">Varios inquilinos por base de datos (dos tipos):</span><span class="sxs-lookup"><span data-stu-id="c25b3-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="c25b3-130">Asignación de lista</span><span class="sxs-lookup"><span data-stu-id="c25b3-130">List mapping</span></span>
   2. <span data-ttu-id="c25b3-131">Asignación de intervalo</span><span class="sxs-lookup"><span data-stu-id="c25b3-131">Range mapping</span></span>

<span data-ttu-id="c25b3-132">Para un modelo de un solo inquilino, cree un mapa de particiones de **asignación de lista** .</span><span class="sxs-lookup"><span data-stu-id="c25b3-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="c25b3-133">modelo de Hello único inquilino asigna una base de datos por inquilino.</span><span class="sxs-lookup"><span data-stu-id="c25b3-133">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="c25b3-134">Se trata de un modelo eficaz para desarrolladores de SaaS, pues simplifica la administración.</span><span class="sxs-lookup"><span data-stu-id="c25b3-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Asignación de lista][1]

<span data-ttu-id="c25b3-136">modelo de varios inquilinos de Hello asigna a varios inquilinos tooa única base de datos (y grupos de inquilinos puede distribuir a través de varias bases de datos).</span><span class="sxs-lookup"><span data-stu-id="c25b3-136">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="c25b3-137">Use este modelo cuando espera que necesitan cada datos pequeños de toohave de inquilino.</span><span class="sxs-lookup"><span data-stu-id="c25b3-137">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="c25b3-138">En este modelo, se asigna un intervalo de los inquilinos tooa base de datos usando **asignación de intervalo**.</span><span class="sxs-lookup"><span data-stu-id="c25b3-138">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Asignación de intervalo][2]

<span data-ttu-id="c25b3-140">O puede implementar un modelo de base de datos de varios inquilinos mediante un *asignación de lista* tooassign varios inquilinos tooa única base de datos.</span><span class="sxs-lookup"><span data-stu-id="c25b3-140">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="c25b3-141">Por ejemplo, DB1 es toostore usa información acerca del Id. de inquilino 1 y 5, y DB2 almacena los datos de inquilino 10 e inquilino 7.</span><span class="sxs-lookup"><span data-stu-id="c25b3-141">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Varios inquilinos en una sola base de datos][3] 

<span data-ttu-id="c25b3-143">**En función de su elección, elija una de estas opciones:**</span><span class="sxs-lookup"><span data-stu-id="c25b3-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="c25b3-144">Opción 1: crear un mapa de particiones para una asignación de lista</span><span class="sxs-lookup"><span data-stu-id="c25b3-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="c25b3-145">Crear un mapa de particiones con objeto de ShardMapManager Hola.</span><span class="sxs-lookup"><span data-stu-id="c25b3-145">Create a shard map using hello ShardMapManager object.</span></span> 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="c25b3-146">Opción 2: crear un mapa de particiones para una asignación de intervalo</span><span class="sxs-lookup"><span data-stu-id="c25b3-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="c25b3-147">Tenga en cuenta que tooutilize este patrón de asignación, los valores de Id. de inquilino debe toobe continua intervalos y es espacio toohave aceptable en intervalos de hello simplemente omitiendo intervalo Hola al crear las bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c25b3-147">Note that tooutilize this mapping pattern, tenant id values needs toobe continuous ranges, and it is acceptable toohave gap in hello ranges by simply skipping hello range when creating hello databases.</span></span>

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="c25b3-148">Opción 3: asignaciones de lista en una base de datos única</span><span class="sxs-lookup"><span data-stu-id="c25b3-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="c25b3-149">La configuración de este patrón también requiere la creación de un mapa de lista, tal como se muestra en el paso 2, opción 1.</span><span class="sxs-lookup"><span data-stu-id="c25b3-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="c25b3-150">Paso 3: preparar particiones individuales</span><span class="sxs-lookup"><span data-stu-id="c25b3-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="c25b3-151">Agregue cada administrador de mapa de particiones (base de datos) toohello particiones.</span><span class="sxs-lookup"><span data-stu-id="c25b3-151">Add each shard (database) toohello shard map manager.</span></span> <span data-ttu-id="c25b3-152">Esto prepara las bases de datos individuales de Hola para almacenar información de asignación.</span><span class="sxs-lookup"><span data-stu-id="c25b3-152">This prepares hello individual databases for storing mapping information.</span></span> <span data-ttu-id="c25b3-153">Ejecute este método en cada partición.</span><span class="sxs-lookup"><span data-stu-id="c25b3-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="c25b3-154">Paso 4: agregar asignaciones</span><span class="sxs-lookup"><span data-stu-id="c25b3-154">Step 4: Add mappings</span></span>
<span data-ttu-id="c25b3-155">Adición de Hola de asignaciones depende de tipo hello de mapa de particiones que ha creado.</span><span class="sxs-lookup"><span data-stu-id="c25b3-155">hello addition of mappings depends on hello kind of shard map you created.</span></span> <span data-ttu-id="c25b3-156">Si ha creado un mapa de lista, agregue asignaciones de lista.</span><span class="sxs-lookup"><span data-stu-id="c25b3-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="c25b3-157">Si ha creado un mapa de intervalo, agregue asignaciones de intervalo.</span><span class="sxs-lookup"><span data-stu-id="c25b3-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-hello-data-for-a-list-mapping"></a><span data-ttu-id="c25b3-158">Opción 1: asignar datos de Hola para una asignación de lista</span><span class="sxs-lookup"><span data-stu-id="c25b3-158">Option 1: map hello data for a list mapping</span></span>
<span data-ttu-id="c25b3-159">Asignar datos de hello mediante la adición de una asignación de lista para cada inquilino.</span><span class="sxs-lookup"><span data-stu-id="c25b3-159">Map hello data by adding a list mapping for each tenant.</span></span>  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a><span data-ttu-id="c25b3-160">Opción 2: asignar datos de Hola para una asignación de intervalo</span><span class="sxs-lookup"><span data-stu-id="c25b3-160">Option 2: map hello data for a range mapping</span></span>
<span data-ttu-id="c25b3-161">Agregar asignaciones de intervalo de Hola para todos los Hola inquilino intervalo de Id. - las asociaciones de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="c25b3-161">Add hello range mappings for all hello tenant id range - database associations:</span></span>

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="c25b3-162">Paso 4 opción 3: asignar datos de Hola para varios inquilinos en una sola base de datos</span><span class="sxs-lookup"><span data-stu-id="c25b3-162">Step 4 option 3: map hello data for multiple tenants on a single database</span></span>
<span data-ttu-id="c25b3-163">Para cada inquilino, ejecute hello ListMapping agregar (opción 1, anteriormente).</span><span class="sxs-lookup"><span data-stu-id="c25b3-163">For each tenant, run hello Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-hello-mappings"></a><span data-ttu-id="c25b3-164">Comprobación de asignaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="c25b3-164">Checking hello mappings</span></span>
<span data-ttu-id="c25b3-165">Puede consultar información acerca de las particiones existentes hello y asignaciones de hello asociadas a ellos con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="c25b3-165">Information about hello existing shards and hello mappings associated with them can be queried using following commands:</span></span>  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="c25b3-166">Resumen</span><span class="sxs-lookup"><span data-stu-id="c25b3-166">Summary</span></span>
<span data-ttu-id="c25b3-167">Una vez haya completado el programa de instalación de hello, puede empezar a biblioteca de cliente de base de datos elástica toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="c25b3-167">Once you have completed hello setup, you can begin toouse hello Elastic Database client library.</span></span> <span data-ttu-id="c25b3-168">También puede usar las características de [enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md) y [consulta a través de particiones múltiples](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="c25b3-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c25b3-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c25b3-169">Next steps</span></span>
<span data-ttu-id="c25b3-170">Obtener scripts de PowerShell de Hola de [sripts de herramientas de base de datos de Azure SQL DB elásticas](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="c25b3-170">Get hello PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="c25b3-171">herramientas de Hello también están en GitHub: [Azure/elásticas-db-tools](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="c25b3-171">hello tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="c25b3-172">Utilice Hola herramienta Dividir-combinar toomove datos tooor de un modelo de un solo inquilino de tooa de modelo de varios inquilinos.</span><span class="sxs-lookup"><span data-stu-id="c25b3-172">Use hello split-merge tool toomove data tooor from a multi-tenant model tooa single tenant model.</span></span> <span data-ttu-id="c25b3-173">Consulte el artículo sobre la [herramienta de división y combinación](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c25b3-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c25b3-174">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c25b3-174">Additional resources</span></span>
<span data-ttu-id="c25b3-175">Para obtener información sobre los patrones comunes de la arquitectura de datos de aplicaciones de base de datos de software como servicio (SaaS) multiinquilino, consulte [Modelos de diseño para las aplicaciones SaaS multiinquilino con base de datos SQL de Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="c25b3-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="c25b3-176">Preguntas y solicitudes de características</span><span class="sxs-lookup"><span data-stu-id="c25b3-176">Questions and Feature Requests</span></span>
<span data-ttu-id="c25b3-177">Si tiene preguntas, póngase en contacto toous en hello [foro de base de datos SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) y para las solicitudes de características, agréguelos toohello [foro de comentarios de la base de datos SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="c25b3-177">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

