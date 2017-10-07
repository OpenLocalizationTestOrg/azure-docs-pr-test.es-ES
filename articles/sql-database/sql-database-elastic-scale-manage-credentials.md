---
title: "credenciales de aaaManaging en la biblioteca de cliente de base de datos elástica Hola | Documentos de Microsoft"
description: "¿Cómo tooset Hola nivel adecuado de credenciales, administrador solo tooread, para las aplicaciones de base de datos elástica"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a><span data-ttu-id="c5538-103">Credenciales usan la biblioteca de cliente de base de datos elástica tooaccess Hola</span><span class="sxs-lookup"><span data-stu-id="c5538-103">Credentials used tooaccess hello Elastic Database client library</span></span>
<span data-ttu-id="c5538-104">Hola [biblioteca de cliente de base de datos elástica](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) usa tres tipos diferentes de hello de credenciales tooaccess [manager de mapa de particiones](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="c5538-104">hello [Elastic Database client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) uses three different kinds  of credentials tooaccess hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="c5538-105">Según la necesidad de hello, usar credenciales de Hola con un nivel más bajo de Hola de posibles de acceso.</span><span class="sxs-lookup"><span data-stu-id="c5538-105">Depending on hello need, use hello credential with  hello lowest level of access possible.</span></span>

* <span data-ttu-id="c5538-106">**Credenciales de administración**: se usan para crear o manipular un administrador de mapas de particiones.</span><span class="sxs-lookup"><span data-stu-id="c5538-106">**Management credentials**: for creating or manipulating a shard map manager.</span></span> <span data-ttu-id="c5538-107">(Vea hello [glosario](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="c5538-107">(See hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
* <span data-ttu-id="c5538-108">**Las credenciales de acceso**: administrador tooobtain información acerca de particiones asignan tooaccess una partición existente.</span><span class="sxs-lookup"><span data-stu-id="c5538-108">**Access credentials**: tooaccess an existing shard map manager tooobtain information about shards.</span></span>
* <span data-ttu-id="c5538-109">**Las credenciales de conexión**: tooconnect tooshards.</span><span class="sxs-lookup"><span data-stu-id="c5538-109">**Connection credentials**: tooconnect tooshards.</span></span> 

<span data-ttu-id="c5538-110">Consulte, asimismo, [Administrar bases de datos e inicios de sesión en la Base de datos SQL de Azure](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="c5538-110">See also [Managing databases and logins in Azure SQL Database](sql-database-manage-logins.md).</span></span> 

## <a name="about-management-credentials"></a><span data-ttu-id="c5538-111">Acerca de las credenciales de administración</span><span class="sxs-lookup"><span data-stu-id="c5538-111">About management credentials</span></span>
<span data-ttu-id="c5538-112">Las credenciales de administración son toocreate usado un [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) objeto para las aplicaciones que manipulan mapas de particiones.</span><span class="sxs-lookup"><span data-stu-id="c5538-112">Management credentials are used toocreate a [**ShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) object for applications that manipulate shard maps.</span></span> <span data-ttu-id="c5538-113">(Por ejemplo, vea [agregar una partición con herramientas de base de datos elástica](sql-database-elastic-scale-add-a-shard.md) y [enrutamiento dependiente de datos](sql-database-elastic-scale-data-dependent-routing.md)) usuario Hola Hola escala elástica de biblioteca de cliente crea inicios de sesión SQL y los usuarios SQL de Hola y garantiza que cada uno de ellos se concede permisos de lectura/escritura de hello en particiones global Hola asignan base de datos y todas las bases de datos de particiones también.</span><span class="sxs-lookup"><span data-stu-id="c5538-113">(For example, see [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md)) hello user of hello elastic scale client library creates hello SQL users and SQL logins and makes sure each is granted hello read/write permissions on hello global shard map database and all shard databases as well.</span></span> <span data-ttu-id="c5538-114">Estas credenciales son mapa de particiones global de Hola de toomaintain usado y mapas de particiones locales de hello cuando se realizan cambios mapa de particiones de toohello.</span><span class="sxs-lookup"><span data-stu-id="c5538-114">These credentials are used toomaintain hello global shard map and hello local shard maps when changes toohello shard map are performed.</span></span> <span data-ttu-id="c5538-115">Por ejemplo, usar Hola administración credenciales toocreate Hola particiones manager objeto map (mediante [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span><span class="sxs-lookup"><span data-stu-id="c5538-115">For instance, use hello management credentials toocreate hello shard map manager object (using [**GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx):</span></span> 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

<span data-ttu-id="c5538-116">variable de Hello **smmAdminConnectionString** es una cadena de conexión que contiene las credenciales de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5538-116">hello variable **smmAdminConnectionString** is a connection string that contains hello management credentials.</span></span> <span data-ttu-id="c5538-117">Hola Id. de usuario y la contraseña proporciona base de datos de la asignación de particiones de lectura/escritura access tooboth y las particiones individuales.</span><span class="sxs-lookup"><span data-stu-id="c5538-117">hello user ID and password provides read/write access tooboth shard map database and individual shards.</span></span> <span data-ttu-id="c5538-118">cadena de conexión de administración de Hello también incluye Hola servidor nombre y la base de datos nombre tooidentify Hola partición global mapa base de datos.</span><span class="sxs-lookup"><span data-stu-id="c5538-118">hello management connection string also includes hello server name and database name tooidentify hello global shard map database.</span></span> <span data-ttu-id="c5538-119">Esta es una cadena de conexión típica para ese fin:</span><span class="sxs-lookup"><span data-stu-id="c5538-119">Here is a typical connection string for that purpose:</span></span>

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

<span data-ttu-id="c5538-120">No utilice valores en forma de Hola de "username@server", en su lugar, simplemente utilice el valor de "username" de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5538-120">Do not use values in hello form of "username@server"—instead just use hello "username" value.</span></span>  <span data-ttu-id="c5538-121">Esto es porque las credenciales deben funcionar con la base de datos de administrador de mapa de particiones de Hola y particiones individuales, que pueden estar en diferentes servidores.</span><span class="sxs-lookup"><span data-stu-id="c5538-121">This is because credentials must work against both hello shard map manager database and individual shards, which may be on different servers.</span></span>

## <a name="access-credentials"></a><span data-ttu-id="c5538-122">Credenciales de acceso</span><span class="sxs-lookup"><span data-stu-id="c5538-122">Access credentials</span></span>
<span data-ttu-id="c5538-123">Al crear una partición en el Administrador de asignación en una aplicación que no administrar asignaciones de particiones, utilice las credenciales que tienen permisos de solo lectura en el mapa de particiones global de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5538-123">When creating a shard map manager in an application that does not administer shard maps, use credentials that have read-only permissions on hello global shard map.</span></span> <span data-ttu-id="c5538-124">Hello información recuperada de mapa de particiones global de hello en estas credenciales permiten [enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md) y partición de hello toopopulate asignar la memoria caché en el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5538-124">hello information retrieved from hello global shard map under these credentials are used for [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and toopopulate hello shard map cache on hello client.</span></span> <span data-ttu-id="c5538-125">Hello las credenciales son proporcionados a través de hello mismo call (modelo) demasiado**GetSqlShardMapManager** como se indicó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="c5538-125">hello credentials are provided through hello same call pattern too**GetSqlShardMapManager** as shown above:</span></span> 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

<span data-ttu-id="c5538-126">Tenga en cuenta Hola uso del programa Hola a **smmReadOnlyConnectionString** tooreflect uso de Hola de credenciales diferentes para este acceso en nombre de **sin derechos administrativos** a los usuarios: estas credenciales no deberían proporcionar escritura permisos en el mapa de particiones global de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5538-126">Note hello use of hello **smmReadOnlyConnectionString** tooreflect hello use of different credentials for this access on behalf of **non-admin** users: these credentials should not provide write permissions on hello global shard map.</span></span> 

## <a name="connection-credentials"></a><span data-ttu-id="c5538-127">Credenciales de conexión</span><span class="sxs-lookup"><span data-stu-id="c5538-127">Connection credentials</span></span>
<span data-ttu-id="c5538-128">Se necesitan credenciales adicionales cuando se usa hello [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) método tooaccess una partición asociada a una clave de particionamiento.</span><span class="sxs-lookup"><span data-stu-id="c5538-128">Additional credentials are needed when using hello [**OpenConnectionForKey**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) method tooaccess a shard associated with a sharding key.</span></span> <span data-ttu-id="c5538-129">Estas credenciales necesitan permisos de tooprovide para tablas de mapas de acceso de solo lectura toohello particiones locales que residen en la partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5538-129">These credentials need tooprovide permissions for read-only access toohello local shard map tables residing on hello shard.</span></span> <span data-ttu-id="c5538-130">Se trata de validación de la conexión de tooperform necesarios para el enrutamiento dependiente de los datos en particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5538-130">This is needed tooperform connection validation for data-dependent routing on hello shard.</span></span> <span data-ttu-id="c5538-131">Este fragmento de código permite el acceso de datos en el contexto de Hola de enrutamiento dependiente de datos:</span><span class="sxs-lookup"><span data-stu-id="c5538-131">This code snippet allows data access in hello context of data dependent routing:</span></span> 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

<span data-ttu-id="c5538-132">En este ejemplo, **smmUserConnectionString** contiene la cadena de conexión de Hola para hello las credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="c5538-132">In this example, **smmUserConnectionString** holds hello connection string for hello user credentials.</span></span> <span data-ttu-id="c5538-133">En el caso de Base de datos SQL de Azure, la siguiente es una cadena de conexión típica para las credenciales de usuario:</span><span class="sxs-lookup"><span data-stu-id="c5538-133">For Azure SQL DB, here is a typical connection string for user credentials:</span></span> 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

<span data-ttu-id="c5538-134">Al igual que con las credenciales de administrador de hello, no los valores en forma de Hola de "username@server".</span><span class="sxs-lookup"><span data-stu-id="c5538-134">As with hello admin credentials, do not values in hello form of "username@server".</span></span> <span data-ttu-id="c5538-135">En su lugar, use aquellos que tengan el formato "username".</span><span class="sxs-lookup"><span data-stu-id="c5538-135">Instead, just use "username".</span></span>  <span data-ttu-id="c5538-136">Tenga en cuenta también que la cadena de conexión de hello no contiene un nombre de servidor y nombre de base de datos.</span><span class="sxs-lookup"><span data-stu-id="c5538-136">Also note that hello connection string does not contain a server name and database name.</span></span> <span data-ttu-id="c5538-137">Esto es así porque hello **OpenConnectionForKey** llamada dirigirá automáticamente Hola conexión toohello correcta de partición basada en clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5538-137">That is because hello **OpenConnectionForKey** call will automatically direct hello connection toohello correct shard based on hello key.</span></span> <span data-ttu-id="c5538-138">Por lo tanto, no se proporcionan el nombre de la base de datos de Hola y el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="c5538-138">Hence, hello database name and server name are not provided.</span></span> 

## <a name="see-also"></a><span data-ttu-id="c5538-139">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="c5538-139">See also</span></span>
[<span data-ttu-id="c5538-140">Administrar bases de datos e inicios de sesión en Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="c5538-140">Managing databases and logins in Azure SQL Database</span></span>](sql-database-manage-logins.md)

[<span data-ttu-id="c5538-141">Protección de bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="c5538-141">Securing your SQL Database</span></span>](sql-database-security-overview.md)

[<span data-ttu-id="c5538-142">Introducción a Trabajos de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="c5538-142">Getting started with Elastic Database jobs</span></span>](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]
