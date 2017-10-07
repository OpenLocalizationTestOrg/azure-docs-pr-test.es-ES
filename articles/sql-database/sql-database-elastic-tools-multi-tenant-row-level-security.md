---
title: "aplicaciones de inquilinos de aaaMulti con las herramientas de bases de datos elásticas y seguridad de nivel de fila"
description: "Obtenga información acerca de cómo toouse herramientas de base de datos elástica junto con nivel de fila seguridad toobuild una aplicación con un nivel de datos altamente escalable en la base de datos de SQL de Azure que admite varios inquilinos particiones."
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="0fc5a-103">Aplicaciones de múltiples inquilinos con herramientas de bases de datos elásticas y seguridad de nivel de fila</span><span class="sxs-lookup"><span data-stu-id="0fc5a-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="0fc5a-104">[Herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md) y [(RLS) de seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131) ofrecen un conjunto eficaz de capacidades de manera flexible y eficaz escalar la capa de datos de Hola de una aplicación multiempresa con base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling hello data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="0fc5a-105">Consulte [Modelos de diseño para las aplicaciones SaaS multiinquilino con base de datos SQL de Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="0fc5a-106">Este artículo se explica cómo toouse estos toobuild de tecnologías conjuntamente una aplicación con un nivel de datos altamente escalable que es compatible con particiones de varios inquilinos, con **ADO.NET SqlClient** o **deEntityFramework**.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-106">This article illustrates how toouse these technologies together toobuild an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="0fc5a-107">**Herramientas de base de datos elástica** permite a los desarrolladores tooscale fuera de la capa de datos de Hola de una aplicación a través de procedimientos recomendados de particionamiento estándar del sector mediante un conjunto de plantillas de servicio de Azure y bibliotecas de. NET.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-107">**Elastic database tools** enables developers tooscale out hello data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="0fc5a-108">Administración de particiones con el uso de hello elástico biblioteca de cliente de base de datos le ayuda a automatizar y simplificar muchas de tareas los Hola normalmente asociadas con el particionamiento.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-108">Managing shards with using hello Elastic Database Client Library helps automate and streamline many of hello infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="0fc5a-109">**Seguridad de nivel de fila** permite que los desarrolladores toostore datos para varios inquilinos en la misma base de datos utilizando toofilter de directivas de seguridad las filas que no pertenecen a los inquilinos toohello ejecutar una consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-109">**Row-level security** enables developers toostore data for multiple tenants in hello same database using security policies toofilter out rows that do not belong toohello tenant executing a query.</span></span> <span data-ttu-id="0fc5a-110">Centralizar la lógica de acceso con RLS dentro de la base de datos de hello, en su lugar de en la aplicación hello, simplifica el mantenimiento y reduce el riesgo de Hola de error como una aplicación codebase aumenta de tamaño.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-110">Centralizing access logic with RLS inside hello database, rather than in hello application, simplifies maintenance and reduces hello risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="0fc5a-111">Uso de estas características juntas, una aplicación puede beneficiarse de las mejoras de ahorro y eficiencia de costo mediante el almacenamiento de datos para varios inquilinos en hello mismo base de datos de partición.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in hello same shard database.</span></span> <span data-ttu-id="0fc5a-112">Hola mismo tiempo, una aplicación todavía tiene Hola flexibilidad toooffer aislada, único inquilino particiones para los inquilinos de "premium" que se requieren garantías de rendimiento más estrictas, puesto que las particiones de varios inquilinos no garantizan la distribución de recursos igual entre los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-112">At hello same time, an application still has hello flexibility toooffer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="0fc5a-113">En resumen, Hola de la biblioteca de cliente de base de datos elástica [enrutamiento dependiente de datos](sql-database-elastic-scale-data-dependent-routing.md) API conectan automáticamente los inquilinos toohello partición correcta base de datos con su clave de particionamiento (generalmente un "TenantId").</span><span class="sxs-lookup"><span data-stu-id="0fc5a-113">In short, hello elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants toohello correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="0fc5a-114">Una vez conectado, una directiva de seguridad RLS dentro de la base de datos de hello garantiza que los inquilinos sólo pueden tener acceso a las filas que contienen su TenantId.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-114">Once connected, an RLS security policy within hello database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="0fc5a-115">Se supone que todas las tablas contienen un tooindicate de columna de TenantId qué filas pertenecen a tooeach inquilino.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-115">It is assumed that all tables contain a TenantId column tooindicate which rows belong tooeach tenant.</span></span> 

![Arquitectura de la aplicación de creación de blogs][1]

## <a name="download-hello-sample-project"></a><span data-ttu-id="0fc5a-117">Descargar el proyecto de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="0fc5a-117">Download hello sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="0fc5a-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0fc5a-118">Prerequisites</span></span>
* <span data-ttu-id="0fc5a-119">Uso de Visual Studio (2012 o posterior)</span><span class="sxs-lookup"><span data-stu-id="0fc5a-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="0fc5a-120">Creación de tres Bases de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0fc5a-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="0fc5a-121">Descargue el proyecto de ejemplo: [Herramientas de bases de datos elásticas para SQL de Azure - Particiones con varios inquilinos](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="0fc5a-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="0fc5a-122">Rellenar la información de Hola para las bases de datos al principio de Hola de **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="0fc5a-122">Fill in hello information for your databases at hello beginning of **Program.cs**</span></span> 

<span data-ttu-id="0fc5a-123">Este proyecto extiende Hola uno se describe en [elástico herramientas de base de datos de SQL Azure - integración de Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) agregando compatibilidad para las bases de datos de la partición de varios inquilinos.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-123">This project extends hello one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="0fc5a-124">Se crea una aplicación de consola sencilla para la creación de blogs y publicaciones, con cuatro de los inquilinos y dos bases de datos de partición de varios inquilinos como se muestra en hello diagrama anterior.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in hello above diagram.</span></span> 

<span data-ttu-id="0fc5a-125">Compile y ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-125">Build and run hello application.</span></span> <span data-ttu-id="0fc5a-126">Esto arranca herramientas Hola elástico de base de datos Administrador de mapa de particiones y ejecución Hola después de pruebas:</span><span class="sxs-lookup"><span data-stu-id="0fc5a-126">This will bootstrap hello elastic database tools’ shard map manager and run hello following tests:</span></span> 

1. <span data-ttu-id="0fc5a-127">Con Entity Framework y LINQ, cree un nuevo blog y muestre todos los blogs para cada inquilino.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="0fc5a-128">Con ADO.NET SqlClient, muestre todos los blogs para un inquilino.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="0fc5a-129">Intente tooinsert blog para hello inquilino incorrecto tooverify que se produce un error</span><span class="sxs-lookup"><span data-stu-id="0fc5a-129">Try tooinsert a blog for hello wrong tenant tooverify that an error is thrown</span></span>  

<span data-ttu-id="0fc5a-130">Observe que, porque todavía no se ha habilitado RLS en bases de datos de partición de Hola, cada una de estas pruebas revela un problema: los inquilinos están toosee capaz de blogs que no pertenecen toothem y aplicación hello no se les impide insertar un blog del inquilino incorrecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-130">Notice that because RLS has not yet been enabled in hello shard databases, each of these tests reveals a problem: tenants are able toosee blogs that do not belong toothem, and hello application is not prevented from inserting a blog for hello wrong tenant.</span></span> <span data-ttu-id="0fc5a-131">Hello que queda de este artículo describe cómo tooresolve estos problemas mediante la aplicación de inquilino aislamiento con RLS.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-131">hello remainder of this article describes how tooresolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="0fc5a-132">Hay dos pasos:</span><span class="sxs-lookup"><span data-stu-id="0fc5a-132">There are two steps:</span></span> 

1. <span data-ttu-id="0fc5a-133">**Capa de aplicación**: modificar el código de la aplicación hello tooalways conjunto Hola TenantId actual en hello SESSION_CONTEXT después de abrir una conexión.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-133">**Application tier**: Modify hello application code tooalways set hello current TenantId in hello SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="0fc5a-134">proyecto de ejemplo de Hola ya ha hecho.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-134">hello sample project has already done this.</span></span> 
2. <span data-ttu-id="0fc5a-135">**Capa de datos**: crear una directiva de seguridad RLS en cada toofilter de base de datos de partición filas basadas en hello TenantId almacenados en SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-135">**Data tier**: Create an RLS security policy in each shard database toofilter rows based on hello TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="0fc5a-136">Deberá toodo esto para cada una de las bases de datos de la partición; en caso contrario, no se filtrarán filas en particiones de varios inquilinos.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-136">You will need toodo this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a><span data-ttu-id="0fc5a-137">Capa de aplicación del paso 1): establezca TenantId en hello SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="0fc5a-137">Step 1) Application tier: Set TenantId in hello SESSION_CONTEXT</span></span>
<span data-ttu-id="0fc5a-138">Después de conectar tooa particiones base de datos con datos de la biblioteca de cliente de base de datos elástica Hola que todavía la API de enrutamientos dependientes, aplicación hello necesidades de base de datos de tootell Hola qué TenantId usa esa conexión para que una directiva de seguridad RLS puede filtrar las filas tooother, que pertenecen los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-138">After connecting tooa shard database using hello elastic database client library’s data dependent routing APIs, hello application still needs tootell hello database which TenantId is using that connection so that an RLS security policy can filter out rows belonging tooother tenants.</span></span> <span data-ttu-id="0fc5a-139">Hola toopass manera recomendada esta información es toostore Hola TenantId actual para esa conexión en hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fc5a-139">hello recommended way toopass this information is toostore hello current TenantId for that connection in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="0fc5a-140">(Nota: como alternativa, podría usar [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), pero SESSION_CONTEXT constituye una mejor opción porque es más fácil toouse, devuelve NULL de forma predeterminada y admite pares de clave y valor.)</span><span class="sxs-lookup"><span data-stu-id="0fc5a-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier toouse, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="0fc5a-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="0fc5a-141">Entity Framework</span></span>
<span data-ttu-id="0fc5a-142">Para las aplicaciones que usan Entity Framework, un enfoque más sencillo Hola es hello tooset SESSION_CONTEXT dentro de hello ElasticScaleContext invalidar se describe en [enrutamiento dependiente de datos mediante EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="0fc5a-142">For applications using Entity Framework, hello easiest approach is tooset hello SESSION_CONTEXT within hello ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="0fc5a-143">Antes de devolver la conexión de hello asíncrona a través de enrutamiento dependiente de datos, crear y ejecutar un objeto SqlCommand que establece 'TenantId' en hello SESSION_CONTEXT toohello shardingKey especificada para esa conexión.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-143">Before returning hello connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in hello SESSION_CONTEXT toohello shardingKey specified for that connection.</span></span> <span data-ttu-id="0fc5a-144">De este modo, solo necesita toowrite código una vez tooset Hola SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-144">This way, you only need toowrite code once tooset hello SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

<span data-ttu-id="0fc5a-145">Ahora hello SESSION_CONTEXT se establece automáticamente con hello especifica TenantId siempre que se invoca ElasticScaleContext:</span><span class="sxs-lookup"><span data-stu-id="0fc5a-145">Now hello SESSION_CONTEXT is automatically set with hello specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a><span data-ttu-id="0fc5a-146">SqlClient de ADO.NET</span><span class="sxs-lookup"><span data-stu-id="0fc5a-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="0fc5a-147">Para aplicaciones que utilizan ADO.NET SqlClient, hello recomienda consiste toocreate una función de contenedor alrededor de ShardMap.OpenConnectionForKey() que establece automáticamente 'TenantId' en hello SESSION_CONTEXT toohello corregir TenantId antes de devolver un conexión.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-147">For applications using ADO.NET SqlClient, hello recommended approach is toocreate a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in hello SESSION_CONTEXT toohello correct TenantId before returning a connection.</span></span> <span data-ttu-id="0fc5a-148">tooensure que SESSION_CONTEXT siempre se establece, solo se deben abrir las conexiones que utilizan esta función de contenedor.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-148">tooensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="0fc5a-149">Paso 2) Capa de datos: cree una directiva de seguridad de nivel de fila</span><span class="sxs-lookup"><span data-stu-id="0fc5a-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a><span data-ttu-id="0fc5a-150">Crear un hello toofilter de directiva de seguridad filas que pueden tener acceso todos los inquilinos</span><span class="sxs-lookup"><span data-stu-id="0fc5a-150">Create a security policy toofilter hello rows each tenant can access</span></span>
<span data-ttu-id="0fc5a-151">Ahora que la aplicación hello es establecer SESSION_CONTEXT con Hola TenantId actual antes de consultar, una directiva de seguridad RLS puede filtrar las consultas y excluir filas que tienen un valor de TenantId diferentes.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-151">Now that hello application is setting SESSION_CONTEXT with hello current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="0fc5a-152">RLS se implementa en código T-SQL: una función definida por el usuario define la lógica de acceso de hello y una directiva de seguridad enlaza este número de tooany de función de tablas.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-152">RLS is implemented in T-SQL: a user-defined function defines hello access logic, and a security policy binds this function tooany number of tables.</span></span> <span data-ttu-id="0fc5a-153">Para este proyecto, función hello simplemente comprobará que Hola aplicación (en lugar de algún otro usuario SQL) es la base de datos de toohello conectado, y ese hello 'TenantId' almacenado en hello SESSION_CONTEXT coincide con hello TenantId de una fila determinada.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-153">For this project, hello function will simply verify that hello application (rather than some other SQL user) is connected toohello database, and that hello 'TenantId' stored in hello SESSION_CONTEXT matches hello TenantId of a given row.</span></span> <span data-ttu-id="0fc5a-154">Un predicado de filtro le permitirá las filas que cumplen estas condiciones toopass a través del filtro de Hola para consultas SELECT, UPDATE y DELETE; y un predicado block que impedirá que las filas que infringen estas condiciones que insertados o actualizados.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-154">A filter predicate will allow rows that meet these conditions toopass through hello filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="0fc5a-155">Si no se ha establecido SESSION_CONTEXT, devolverá que null y no hay ninguna fila será toobe visible o puede insertar.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able toobe inserted.</span></span> 

<span data-ttu-id="0fc5a-156">tooenable RLS, ejecute hello siguiente T-SQL en todas las particiones con cualquier Visual Studio (SSDT), SSMS, u Hola script de PowerShell incluido en el proyecto de hello (o si está utilizando [elástico de base de datos de trabajos](sql-database-elastic-jobs-overview.md), se puede usar tooautomate ejecución de esta instrucción T-SQL en todas las particiones):</span><span class="sxs-lookup"><span data-stu-id="0fc5a-156">tooenable RLS, execute hello following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or hello PowerShell script included in hello project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it tooautomate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> <span data-ttu-id="0fc5a-157">Para los proyectos más complejos que necesitan tooadd predicado de hello en cientos de tablas, puede utilizar un procedimiento almacenado auxiliar que genera automáticamente una directiva de seguridad que se agrega un predicado en todas las tablas en un esquema.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-157">For more complex projects that need tooadd hello predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="0fc5a-158">Vea [tablas de aplicar la seguridad de nivel de fila tooall - script auxiliar (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span><span class="sxs-lookup"><span data-stu-id="0fc5a-158">See [Apply Row-Level Security tooall tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="0fc5a-159">Ahora si se ejecuta de nuevo la aplicación de ejemplo de Hola, los inquilinos le pueda toosee solo las filas que pertenecen a toothem.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-159">Now if you run hello sample application again, tenants will able toosee only rows that belong toothem.</span></span> <span data-ttu-id="0fc5a-160">Además, aplicación hello no pueden insertar filas que pertenecen tootenants que no sea de base de datos de hello toohello conectado actualmente una partición, y no puede actualizar filas visibles toohave un valor de TenantId diferentes.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-160">In addition, hello application cannot insert rows that belong tootenants other than hello one currently connected toohello shard database, and it cannot update visible rows toohave a different TenantId.</span></span> <span data-ttu-id="0fc5a-161">Si hay aplicación hello intentos toodo o bien, se generará una DbUpdateException.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-161">If hello application attempts toodo either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="0fc5a-162">Si agrega una nueva tabla más adelante, simplemente ALTER Hola directiva de seguridad y agregue los predicados de filtro y de bloqueo en la nueva tabla de Hola:</span><span class="sxs-lookup"><span data-stu-id="0fc5a-162">If you add a new table later on, simply ALTER hello security policy and add filter and block predicates on hello new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a><span data-ttu-id="0fc5a-163">Agregar de forma predeterminada restricciones tooautomatically rellenar TenantId para las inserciones</span><span class="sxs-lookup"><span data-stu-id="0fc5a-163">Add default constraints tooautomatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="0fc5a-164">Puede colocar un valor predeterminado restricción en cada tabla tooautomatically rellenar hello TenantId con hello valor almacenado actualmente en SESSION_CONTEXT al insertar filas.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-164">You can put a default constraint on each table tooautomatically populate hello TenantId with hello value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="0fc5a-165">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0fc5a-165">For example:</span></span> 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="0fc5a-166">Ahora aplicación hello no es necesario un valor de TenantId toospecify al insertar filas:</span><span class="sxs-lookup"><span data-stu-id="0fc5a-166">Now hello application does not need toospecify a TenantId when inserting rows:</span></span> 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> <span data-ttu-id="0fc5a-167">Si utiliza las restricciones predeterminadas de un proyecto de Entity Framework, se recomienda que no incluye columnas de TenantId de hello en el modelo de datos EF.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include hello TenantId column in your EF data model.</span></span> <span data-ttu-id="0fc5a-168">Esto es porque las consultas de Entity Framework proporcionan automáticamente los valores predeterminados que invalidarán Hola predeterminado las restricciones creadas en T-SQL que utilizan SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-168">This is because Entity Framework queries automatically supply default values which will override hello default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="0fc5a-169">proyecto de ejemplo de las restricciones predeterminadas de toouse en hello, por ejemplo, debes quitar TenantId DataClasses.cs (y Add-Migration ejecución en la consola de administrador de paquetes de saludo) y tooensure usar T-SQL que Hola campo solo se encuentra en tablas de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-169">toouse default constraints in hello sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in hello Package Manager Console) and use T-SQL tooensure that hello field only exists in hello database tables.</span></span> <span data-ttu-id="0fc5a-170">De este modo, EF no proporcionará automáticamente los valores predeterminados incorrectos al insertar datos.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a><span data-ttu-id="0fc5a-171">(Opcional) Habilitar todas las filas de una tooaccess de "superusuario"</span><span class="sxs-lookup"><span data-stu-id="0fc5a-171">(Optional) Enable a "superuser" tooaccess all rows</span></span>
<span data-ttu-id="0fc5a-172">Algunas aplicaciones pueden necesitar toocreate "superusuario" quién puede acceder a todas las filas, por ejemplo, en tooenable orden reporting a través de todos los inquilinos en todas las particiones o las operaciones de división/combinación tooperform en particiones que implican mover filas de inquilino entre bases de datos.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-172">Some applications may want toocreate a "superuser" who can access all rows, for instance, in order tooenable reporting across all tenants on all shards, or tooperform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="0fc5a-173">tooenable esto, debe crear un nuevo usuario SQL ("superusuario" en este ejemplo) en cada base de datos de la partición.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-173">tooenable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="0fc5a-174">A continuación, modifique la directiva de seguridad de hello con una nueva función de predicado que permite a este usuario tooaccess todas las filas:</span><span class="sxs-lookup"><span data-stu-id="0fc5a-174">Then alter hello security policy with a new predicate function that allows this user tooaccess all rows:</span></span>

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="0fc5a-175">Mantenimiento</span><span class="sxs-lookup"><span data-stu-id="0fc5a-175">Maintenance</span></span>
* <span data-ttu-id="0fc5a-176">**Agregar nuevas particiones**: debe ejecutar script de Hola T-SQL tooenable RLS en las nuevas particiones, en caso contrario, no se filtrarán las consultas en esas particiones.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-176">**Adding new shards**: You must execute hello T-SQL script tooenable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="0fc5a-177">**Adición de nuevas tablas**: debe agregar un filtro y bloquear la directiva de seguridad de predicado toohello en todas las particiones siempre que se crea una nueva tabla, en caso contrario, no se filtrarán las consultas en la nueva tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-177">**Adding new tables**: You must add a filter and block predicate toohello security policy on all shards whenever a new table is created, otherwise queries on hello new table will not be filtered.</span></span> <span data-ttu-id="0fc5a-178">Esto se puede automatizar mediante un desencadenador DDL, como se describe en [aplicar seguridad de nivel de fila toonewly crea automáticamente tablas (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fc5a-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically toonewly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="0fc5a-179">Resumen</span><span class="sxs-lookup"><span data-stu-id="0fc5a-179">Summary</span></span>
<span data-ttu-id="0fc5a-180">Herramientas de bases de datos elásticas y seguridad de nivel de fila pueden ser usado tooscale junto a la capa de datos de una aplicación con compatibilidad para varios inquilinos y único inquilino particiones.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-180">Elastic database tools and row-level security can be used together tooscale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="0fc5a-181">Particiones de varios inquilinos pueden ser utilizados toostore datos más eficazmente (especialmente en casos donde un gran número de los inquilinos tener solamente algunas filas de datos), al único inquilino particiones pueden ser los inquilinos de premium toosupport usados con más estrictos aislamiento y rendimiento requisitos.</span><span class="sxs-lookup"><span data-stu-id="0fc5a-181">Multi-tenant shards can be used toostore data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used toosupport premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="0fc5a-182">Para obtener más información, consulte la [referencia sobre la seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="0fc5a-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0fc5a-183">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0fc5a-183">Additional resources</span></span>
* [<span data-ttu-id="0fc5a-184">¿Qué es un grupo elástico de Azure?</span><span class="sxs-lookup"><span data-stu-id="0fc5a-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="0fc5a-185">Escalado horizontal con Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0fc5a-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="0fc5a-186">Modelos de diseño para las aplicaciones SaaS multiinquilino con base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0fc5a-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="0fc5a-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="0fc5a-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="0fc5a-188">Aplicación Tailspin Surveys</span><span class="sxs-lookup"><span data-stu-id="0fc5a-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="0fc5a-189">Preguntas y solicitudes de características</span><span class="sxs-lookup"><span data-stu-id="0fc5a-189">Questions and Feature Requests</span></span>
<span data-ttu-id="0fc5a-190">Si tiene preguntas, póngase en contacto toous en hello [foro de base de datos SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) y para las solicitudes de características, agréguelos toohello [foro de comentarios de la base de datos SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="0fc5a-190">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


