---
title: Enrutamiento dependiente de los datos con Azure SQL Database | Microsoft Docs
description: "Cómo usar la clase ShardMapManager en aplicaciones .NET para el enrutamiento dependiente de los datos, una característica de las bases de datos con particiones en Azure SQL Database"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 6b68bbb0133afd1493acdb58f79f3eeaf6a8d7cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="a6d6c-103">Enrutamiento dependiente de los datos</span><span class="sxs-lookup"><span data-stu-id="a6d6c-103">Data dependent routing</span></span>
<span data-ttu-id="a6d6c-104">**Enrutamiento dependiente de los datos** es la posibilidad de utilizar los datos de una consulta para enrutar la solicitud a una base de datos adecuada.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-104">**Data dependent routing** is the ability to use the data in a query to route the request to an appropriate database.</span></span> <span data-ttu-id="a6d6c-105">Se trata de un patrón fundamental cuando se trabaja con bases de datos particionadas.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="a6d6c-106">El contexto de solicitud también puede utilizarse para enrutar la solicitud, en especial si la clave de particionamiento no forma parte de la consulta.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-106">The request context may also be used to route the request, especially if the sharding key is not part of the query.</span></span> <span data-ttu-id="a6d6c-107">Cada consulta o transacción específica en una aplicación que usa enrutamiento dependiente de los datos tiene restringido el acceso a una base de datos única por solicitud.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-107">Each specific query or transaction in an application using data dependent routing is restricted to accessing a single database per request.</span></span> <span data-ttu-id="a6d6c-108">En las herramientas de base de datos elástica de Azure SQL Database, este enrutamiento se efectúa con la **[clase ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** en aplicaciones ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-108">For the Azure SQL Database Elastic tools, this routing is accomplished with the **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="a6d6c-109">La aplicación no necesita realizar el seguimiento de las distintas cadenas de conexión o ubicaciones de base de datos asociadas con diferentes segmentos de datos en el entorno particionado.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-109">The application does not need to track various connection strings or DB locations associated with different slices of data in the sharded environment.</span></span> <span data-ttu-id="a6d6c-110">Por el contrario, el [Administrador de mapas de particiones](sql-database-elastic-scale-shard-map-management.md) abre las conexiones a las bases de datos correctas cuando es necesario, en función de los datos del mapa de particiones y del valor de la clave de particionamiento que es el destino de la solicitud de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-110">Instead, the [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections to the correct databases when needed, based on the data in the shard map and the value of the sharding key that is the target of the application’s request.</span></span> <span data-ttu-id="a6d6c-111">(Esta clave normalmente es *customer_id*, *tenant_id*, *date_key* o algún otro identificador específico que es un parámetro fundamental de la solicitud de base de datos).</span><span class="sxs-lookup"><span data-stu-id="a6d6c-111">The key is typically the *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of the database request).</span></span> 

<span data-ttu-id="a6d6c-112">Para más información, consulte [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx)(Escalado horizontal de SQL Server con enrutamiento dependiente de los datos).</span><span class="sxs-lookup"><span data-stu-id="a6d6c-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-the-client-library"></a><span data-ttu-id="a6d6c-113">Descarga de la biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="a6d6c-113">Download the client library</span></span>
<span data-ttu-id="a6d6c-114">Para obtener la clase, instale la [biblioteca de cliente de Base de datos elástica](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="a6d6c-114">To get the class, install the [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="a6d6c-115">Usar un ShardMapManager en una aplicación de enrutamiento dependiente de datos</span><span class="sxs-lookup"><span data-stu-id="a6d6c-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="a6d6c-116">Las aplicaciones deben crear una instancia de **ShardMapManager** durante la inicialización, mediante la llamada de fábrica **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-116">Applications should instantiate the **ShardMapManager** during initialization, using the factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="a6d6c-117">En este ejemplo, se inicializan **ShardMapManager** y un elemento **ShardMap** específico que contiene.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="a6d6c-118">En este ejemplo se muestran los métodos GetSqlShardMapManager y [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a6d6c-118">This example shows the GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-the-shard-map"></a><span data-ttu-id="a6d6c-119">Uso de credenciales de menor privilegio posible para obtener el mapa de particiones</span><span class="sxs-lookup"><span data-stu-id="a6d6c-119">Use lowest privilege credentials possible for getting the shard map</span></span>
<span data-ttu-id="a6d6c-120">Si una aplicación no manipula el propio mapa de particiones, las credenciales utilizadas en el método de fábrica deben tener simplemente permisos de solo lectura en la base de datos del **mapa de particiones global** .</span><span class="sxs-lookup"><span data-stu-id="a6d6c-120">If an application is not manipulating the shard map itself, the credentials used in the factory method should have just read-only permissions on the **Global Shard Map** database.</span></span> <span data-ttu-id="a6d6c-121">Estas credenciales normalmente son distintas de las credenciales que se usan para abrir conexiones con el administrador de mapa de particiones.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-121">These credentials are typically different from credentials used to open connections to the shard map manager.</span></span> <span data-ttu-id="a6d6c-122">Consulte también [Credenciales usadas para acceder a la biblioteca de cliente de bases de datos elásticas](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="a6d6c-122">See also [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-the-openconnectionforkey-method"></a><span data-ttu-id="a6d6c-123">Llamada al método OpenConnectionForKey</span><span class="sxs-lookup"><span data-stu-id="a6d6c-123">Call the OpenConnectionForKey method</span></span>
<span data-ttu-id="a6d6c-124">El método **[ShardMap.OpenConnectionForKey](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** devuelve una conexión ADO.Net lista para emitir comandos a la base de datos adecuada según el valor del parámetro **key**.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-124">The **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands to the appropriate database based on the value of the **key** parameter.</span></span> <span data-ttu-id="a6d6c-125">La información de particionamiento la almacena **ShardMapManager** en la caché de la aplicación, de modo que las solicitudes no implican normalmente una búsqueda de base de datos contra la base de datos **Mapa de particiones global**.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-125">Shard information is cached in the application by the **ShardMapManager**, so these requests do not typically involve a database lookup against the **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="a6d6c-126">El parámetro **key** se usa como clave de búsqueda en el mapa de particiones para determinar la base de datos adecuada para la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-126">The **key** parameter is used as a lookup key into the shard map to determine the appropriate database for the request.</span></span> 
* <span data-ttu-id="a6d6c-127">El elemento **connectionString** se usa para pasar únicamente las credenciales de usuario para la conexión deseada.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-127">The **connectionString** is used to pass only the user credentials for the desired connection.</span></span> <span data-ttu-id="a6d6c-128">Ningún nombre de base de datos o de servidor se incluye en esta *connectionString* dado que el método determinará la base de datos y el servidor usando el **ShardMap**.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-128">No database name or server name are included in this *connectionString* since the method will determine the database and server using the **ShardMap**.</span></span> 
* <span data-ttu-id="a6d6c-129">El valor de **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** se debe establecer en **ConnectionOptions.Validate** si se trata de un entorno donde los mapas de particiones pueden cambiar y las filas pueden moverse a otras bases de datos como resultado de operaciones de división o combinación.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-129">The **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set to **ConnectionOptions.Validate** if an environment where shard maps may change and rows may move to other databases as a result of split or merge operations.</span></span> <span data-ttu-id="a6d6c-130">Esto implica una breve consulta al mapa de particiones local en la base de datos de destino (no al mapa de particiones global) antes de que se entregue la conexión a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-130">This involves a brief query to the local shard map on the target database (not to the global shard map) before the connection is delivered to the application.</span></span> 

<span data-ttu-id="a6d6c-131">Si falla la validación contra el mapa de particiones local (lo que indica que el caché es incorrecto), el Administrador de mapa de particiones consultará el mapa de particiones global para obtener el nuevo valor correcto de la consulta, actualizar la caché y obtener y devolver la conexión de base de datos adecuada.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-131">If the validation against the local shard map fails (indicating that the cache is incorrect), the Shard Map Manager will query the global shard map to obtain the new correct value for the lookup, update the cache, and obtain and return the appropriate database connection.</span></span> 

<span data-ttu-id="a6d6c-132">Utilice **ConnectionOptions.None** solo cuando no se esperen cambios de asignación de particiones mientras una aplicación está en línea.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="a6d6c-133">En ese caso, los valores en caché se pueden asumir como correctos siempre y la llamada de validación de ida y vuelta adicional a la base de datos de destino se puede omitir sin problemas.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-133">In that case, the cached values can be assumed to always be correct, and the extra round-trip validation call to the target database can be safely skipped.</span></span> <span data-ttu-id="a6d6c-134">Esto reduce el tráfico de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-134">That reduces database traffic.</span></span> <span data-ttu-id="a6d6c-135">**connectionOptions** también se puede definir a través de un valor en un archivo de configuración para indicar si se esperan o no cambios en el particionamiento durante un período.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-135">The **connectionOptions** may also be set via a value in a configuration file to indicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="a6d6c-136">En este ejemplo se utiliza el valor de una clave de entero **CustomerID**, mediante un objeto **ShardMap** denominado **customerShardMap**.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-136">This example uses the value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect to the shard for that customer ID. No need to call a SqlConnection 
    // constructor followed by the Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

<span data-ttu-id="a6d6c-137">El método **OpenConnectionForKey** devuelve una nueva conexión ya abierta a la base de datos correcta.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-137">The **OpenConnectionForKey** method returns a new already-open connection to the correct database.</span></span> <span data-ttu-id="a6d6c-138">Las conexiones utilizadas de esta manera seguirán aprovechando completamente las agrupaciones de conexiones de ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="a6d6c-139">Siempre y cuando las transacciones y las solicitudes puedan verse satisfecha por una partición a la vez, esta debiera ser la única modificación necesaria en una aplicación utilizando ya ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-139">As long as transactions and requests can be satisfied by one shard at a time, this should be the only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="a6d6c-140">El **[método OpenConnectionForKeyAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** también está disponible si su aplicación hace uso de programación asincrónica con ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-140">The **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="a6d6c-141">Su comportamiento es equivalente al enrutamiento dependiente de los datos del método **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** de ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-141">Its behavior is the data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="a6d6c-142">Integración con el control de errores transitorios</span><span class="sxs-lookup"><span data-stu-id="a6d6c-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="a6d6c-143">Un procedimiento recomendado para el desarrollo de aplicaciones de acceso a datos en la nube es tener la seguridad de que la aplicación es capaz de capturar los errores transitorios y que las operaciones se reintentan varias veces antes de presentarse un error.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-143">A best practice in developing data access applications in the cloud is to ensure that transient faults are caught by the app, and that the operations are retried several times before throwing an error.</span></span> <span data-ttu-id="a6d6c-144">El control de errores transitorios para aplicaciones en la nube se describe en [Control de errores transitorios](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span><span class="sxs-lookup"><span data-stu-id="a6d6c-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="a6d6c-145">El control de errores transitorios puede coexistir naturalmente con el patrón de Enrutamiento dependiente de los datos.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-145">Transient fault handling can coexist naturally with the Data Dependent Routing pattern.</span></span> <span data-ttu-id="a6d6c-146">El requisito clave es volver a intentar la solicitud de acceso a los datos completa, incluido el bloque **using** que obtuvo la conexión de enrutamiento dependiente de los datos.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-146">The key requirement is to retry the entire data access request including the **using** block that obtained the data-dependent routing connection.</span></span> <span data-ttu-id="a6d6c-147">El ejemplo anterior se podría reescribir de la siguiente manera (observe el cambio resaltado).</span><span class="sxs-lookup"><span data-stu-id="a6d6c-147">The example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="a6d6c-148">Ejemplo: enrutamiento dependiente de los datos con control de errores transitorios</span><span class="sxs-lookup"><span data-stu-id="a6d6c-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect to the shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


<span data-ttu-id="a6d6c-149">Los paquetes necesarios para implementar el control de errores transitorio se descargan automáticamente cuando crea la aplicación  de ejemplo de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-149">Packages necessary to implement transient fault handling are downloaded automatically when you build the elastic database sample application.</span></span> <span data-ttu-id="a6d6c-150">Los paquetes también están disponibles por separado en [Biblioteca de información empresarial: bloque de aplicación Control de errores transitorios](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span><span class="sxs-lookup"><span data-stu-id="a6d6c-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="a6d6c-151">Use la versión 6.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="a6d6c-152">Coherencia de las transacciones</span><span class="sxs-lookup"><span data-stu-id="a6d6c-152">Transactional consistency</span></span>
<span data-ttu-id="a6d6c-153">Las propiedades de las transacciones están garantizadas para todas las operaciones locales respecto a una partición.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-153">Transactional properties are guaranteed for all operations local to a shard.</span></span> <span data-ttu-id="a6d6c-154">Por ejemplo, las transacciones enviadas a través del enrutamiento dependiente de los datos se ejecutan dentro del ámbito de la partición de destino de la conexión.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-154">For example, transactions submitted through data-dependent routing execute within the scope of the target shard for the connection.</span></span> <span data-ttu-id="a6d6c-155">En este momento, no se proporcionan funcionalidades para alistar conexiones múltiples en una transacción y, por lo tanto, no hay garantías de transacciones para las operaciones realizadas a través de las particiones.</span><span class="sxs-lookup"><span data-stu-id="a6d6c-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6d6c-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a6d6c-156">Next steps</span></span>
<span data-ttu-id="a6d6c-157">Para desasociar una partición, o volver a adjuntar una partición, consulte [Uso de la clase RecoveryManager para solucionar problemas de mapas de particiones](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="a6d6c-157">To detach a shard, or to reattach a shard, see [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

