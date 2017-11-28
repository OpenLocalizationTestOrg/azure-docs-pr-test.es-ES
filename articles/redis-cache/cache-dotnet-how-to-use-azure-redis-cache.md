---
title: "aaaHow tooUse caché en Redis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooimprove Hola rendimiento de las aplicaciones de Azure con caché en Redis de Azure"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="adaba-103">Cómo tooUse Redis de Azure almacenan en caché</span><span class="sxs-lookup"><span data-stu-id="adaba-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="adaba-104">.NET</span><span class="sxs-lookup"><span data-stu-id="adaba-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="adaba-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="adaba-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="adaba-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="adaba-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="adaba-107">Java</span><span class="sxs-lookup"><span data-stu-id="adaba-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="adaba-108">Python</span><span class="sxs-lookup"><span data-stu-id="adaba-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="adaba-109">Esta guía le mostrará cómo tooget a usar **Azure Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="adaba-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="adaba-110">Caché en Redis de Microsoft Azure se basa en código abierto populares de hello caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="adaba-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="adaba-111">Proporciona acceso a tooa dedicado Redis caché segura, administrada por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="adaba-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="adaba-112">Una caché creada con Azure Redis Cache es accesible desde cualquier aplicación dentro de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="adaba-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="adaba-113">Caché en Redis de Microsoft Azure está disponible en hello siguientes niveles:</span><span class="sxs-lookup"><span data-stu-id="adaba-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="adaba-114">**Básico** – Nodo único.</span><span class="sxs-lookup"><span data-stu-id="adaba-114">**Basic** – Single node.</span></span> <span data-ttu-id="adaba-115">Varios tamaños de too53 GB.</span><span class="sxs-lookup"><span data-stu-id="adaba-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="adaba-116">**Estándar**: principal/réplica de dos nodos.</span><span class="sxs-lookup"><span data-stu-id="adaba-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="adaba-117">Varios tamaños de too53 GB.</span><span class="sxs-lookup"><span data-stu-id="adaba-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="adaba-118">Contrato de nivel de servicio del 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="adaba-118">99.9% SLA.</span></span>
* <span data-ttu-id="adaba-119">**Premium** : dos nodos principal/réplica con too10 particiones.</span><span class="sxs-lookup"><span data-stu-id="adaba-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="adaba-120">Varios tamaños de 6 GB too530 GB.</span><span class="sxs-lookup"><span data-stu-id="adaba-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="adaba-121">Todas las características del nivel Estándar y algunas otras características son compatibles con los [clústeres de Redis](cache-how-to-premium-clustering.md), la [persistencia de Redis](cache-how-to-premium-persistence.md) y [Azure Virtual Network](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="adaba-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="adaba-122">Contrato de nivel de servicio del 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="adaba-122">99.9% SLA.</span></span>

<span data-ttu-id="adaba-123">Estos niveles difieren en las características y el precio.</span><span class="sxs-lookup"><span data-stu-id="adaba-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="adaba-124">Para más información sobre los precios, consulte los [precios de caché][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="adaba-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="adaba-125">Esta guía le mostrará cómo hello toouse [StackExchange.Redis] [ StackExchange.Redis] cliente mediante C\# código.</span><span class="sxs-lookup"><span data-stu-id="adaba-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="adaba-126">Hello escenarios descritos se incluyen **crear y configurar una memoria caché**, **configurar clientes de caché**, y **agregando y quitando objetos de caché de hello**.</span><span class="sxs-lookup"><span data-stu-id="adaba-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="adaba-127">Para más información sobre el uso de Azure Redis Cache, consulte [Pasos siguientes][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="adaba-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="adaba-128">Para obtener un tutorial paso a paso de la creación una ASP.NET MVC de aplicación web con caché en Redis, vea [cómo toocreate una aplicación Web con caché en Redis](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="adaba-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="adaba-129">Introducción a Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="adaba-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="adaba-130">Empezar a trabajar con Azure Redis Cache es fácil.</span><span class="sxs-lookup"><span data-stu-id="adaba-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="adaba-131">tooget iniciado, hacer provisioning y configurar una memoria caché.</span><span class="sxs-lookup"><span data-stu-id="adaba-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="adaba-132">A continuación, configure los clientes de caché de Hola por lo que puede tener acceso a la memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="adaba-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="adaba-133">Después de configuran los clientes de caché de hello, puede empezar a trabajar con ellos.</span><span class="sxs-lookup"><span data-stu-id="adaba-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="adaba-134">[Crear la memoria caché de Hola][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="adaba-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="adaba-135">[Configurar a clientes de caché de Hola][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="adaba-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="adaba-136">Creación de una caché</span><span class="sxs-lookup"><span data-stu-id="adaba-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="adaba-137">tooaccess se crea en la memoria caché después de él</span><span class="sxs-lookup"><span data-stu-id="adaba-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="adaba-138">Para obtener más información acerca de cómo configurar la memoria caché, vea [cómo tooconfigure Azure Redis Cache](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="adaba-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="adaba-139">Configurar a clientes de caché de Hola</span><span class="sxs-lookup"><span data-stu-id="adaba-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="adaba-140">Una vez que el proyecto de cliente está configurado para almacenar en caché, puede usar técnicas de hello descritas en las siguientes secciones para trabajar con la memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="adaba-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="adaba-141">Trabajo con cachés</span><span class="sxs-lookup"><span data-stu-id="adaba-141">Working with Caches</span></span>
<span data-ttu-id="adaba-142">pasos de Hello en esta sección describe cómo las tareas comunes de tooperform con memoria caché.</span><span class="sxs-lookup"><span data-stu-id="adaba-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="adaba-143">[Conectar toohello caché][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="adaba-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="adaba-144">[Agregar y recuperar objetos de caché de Hola][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="adaba-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="adaba-145">Trabajar con objetos de .NET en memoria caché de Hola</span><span class="sxs-lookup"><span data-stu-id="adaba-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="adaba-146">Conectar toohello caché</span><span class="sxs-lookup"><span data-stu-id="adaba-146">Connect toohello cache</span></span>
<span data-ttu-id="adaba-147">trabajo de tooprogrammatically con una memoria caché, tiene una memoria caché toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="adaba-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="adaba-148">Agregar Hola después de la parte superior de toohello de cualquier archivo desde el que desea toouse hello StackExchange.Redis cliente tooaccess una caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="adaba-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="adaba-149">cliente de Hello StackExchange.Redis requiere .NET Framework 4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="adaba-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="adaba-150">Hola toohello conexión caché en Redis de Azure está administrado por hello `ConnectionMultiplexer` clase.</span><span class="sxs-lookup"><span data-stu-id="adaba-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="adaba-151">Esta clase se debe compartir y reutiliza a lo largo de la aplicación cliente y no es necesario toobe creado en cada operación.</span><span class="sxs-lookup"><span data-stu-id="adaba-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="adaba-152">tooconnect tooan caché en Redis de Azure y devolver una instancia de un `ConnectionMultiplexer`, llamada Hola estático `Connect` método y pase Hola caché extremo y la clave.</span><span class="sxs-lookup"><span data-stu-id="adaba-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="adaba-153">Usar clave Hola generado a partir de portal de Azure como parámetro de contraseña de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="adaba-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="adaba-154">Advertencia: nunca almacene credenciales en el código fuente.</span><span class="sxs-lookup"><span data-stu-id="adaba-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="adaba-155">tookeep este sencillo ejemplo, estoy mostrarlos en código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="adaba-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="adaba-156">Vea [cómo las cadenas de la aplicación y el trabajo de las cadenas de conexión] [ How Application Strings and Connection Strings Work] para obtener información acerca de cómo toostore credenciales.</span><span class="sxs-lookup"><span data-stu-id="adaba-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="adaba-157">Si no desea toouse SSL, establezca `ssl=false` u omitir hello `ssl` parámetro.</span><span class="sxs-lookup"><span data-stu-id="adaba-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="adaba-158">puerto no SSL de Hello está deshabilitado de forma predeterminada para las nuevas cachés.</span><span class="sxs-lookup"><span data-stu-id="adaba-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="adaba-159">Para obtener instrucciones acerca de cómo habilitar el puerto no SSL de hello, consulte [puertos de acceso](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="adaba-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="adaba-160">Un enfoque toosharing una `ConnectionMultiplexer` las instancias de la aplicación es toohave una propiedad estática que devuelve una instancia conectada, similar toohello siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="adaba-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="adaba-161">Este enfoque proporciona una manera segura para subprocesos tooinitialize sólo un único conectado `ConnectionMultiplexer` instancia.</span><span class="sxs-lookup"><span data-stu-id="adaba-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="adaba-162">En estos ejemplos `abortConnect` es toofalse de conjunto, lo que significa que la llamada de hello es correcta incluso si no se establece un toohello conexión caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="adaba-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="adaba-163">Una característica clave de `ConnectionMultiplexer` es que restaurará automáticamente caché de conectividad toohello una vez que el problema de red de Hola o por otros motivos se resuelven.</span><span class="sxs-lookup"><span data-stu-id="adaba-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

<span data-ttu-id="adaba-164">Para más información sobre las opciones de configuración de conexión avanzadas, consulte el artículo sobre el [modelo de configuración de StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="adaba-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="adaba-165">Una vez establecida la conexión de hello, devolver una base de datos de caché de referencia toohello redis Hola llamada `ConnectionMultiplexer.GetDatabase` método.</span><span class="sxs-lookup"><span data-stu-id="adaba-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="adaba-166">Devuelve el objeto de Hola de hello `GetDatabase` método es un objeto ligero de acceso directo y no es necesario toobe almacenado.</span><span class="sxs-lookup"><span data-stu-id="adaba-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="adaba-167">Las memorias caché de Redis de Azure tienen un número configurable de bases de datos (valor predeterminado de 16) que pueden ser datos de hello independiente toologically utilizados dentro de una caché de Redis.</span><span class="sxs-lookup"><span data-stu-id="adaba-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="adaba-168">Para más información, consulte [What are Redis databases?](cache-faq.md#what-are-redis-databases) (¿Qué son las bases de datos de Redis?) y [Configuración predeterminada del servidor Redis](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="adaba-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="adaba-169">Ahora que sabe cómo caché de base de datos de instancia de caché en Redis de Azure de tooconnect tooan y devuelven una referencia toohello, echemos un vistazo a trabajar con la memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="adaba-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="adaba-170">Agregar y recuperar objetos de caché de Hola</span><span class="sxs-lookup"><span data-stu-id="adaba-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="adaba-171">Los elementos se pueden almacenar en y recupera desde una memoria caché con hello `StringSet` y `StringGet` métodos.</span><span class="sxs-lookup"><span data-stu-id="adaba-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="adaba-172">Redis almacenes de mayoría de los datos como cadenas de Redis, sino que estas cadenas puede contener muchos tipos de datos, incluidos los datos binarios serializados, que se pueden usar al almacenar .NET objetos en memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="adaba-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="adaba-173">Al llamar a `StringGet`, si existe un objeto hello, se devuelve, y si no es así, `null` se devuelve.</span><span class="sxs-lookup"><span data-stu-id="adaba-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="adaba-174">Si `null` se devuelve, puede recuperar el valor de Hola Hola deseado origen de datos y almacenar en memoria caché de Hola para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="adaba-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="adaba-175">Este patrón de uso se conoce como modelo de cache-aside Hola.</span><span class="sxs-lookup"><span data-stu-id="adaba-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="adaba-176">También puede usar `RedisValue`, tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="adaba-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="adaba-177">`RedisValue` tiene operadores implícitos para trabajar con tipos de datos enteros y puede ser útil si `null` es un valor esperado para un elemento almacenado en caché.</span><span class="sxs-lookup"><span data-stu-id="adaba-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="adaba-178">expiración de hello toospecify de un elemento en caché de hello, use hello `TimeSpan` parámetro de `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="adaba-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="adaba-179">Trabajar con objetos de .NET en memoria caché de Hola</span><span class="sxs-lookup"><span data-stu-id="adaba-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="adaba-180">Azure Redis Cache puede almacenar en caché objetos .NET así como tipos de datos primitivos, pero antes de poder almacenar en caché un objeto .NET, se debe serializar.</span><span class="sxs-lookup"><span data-stu-id="adaba-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="adaba-181">Esta serialización de objetos .NET es responsabilidad de hello del desarrollador de la aplicación hello y le ofrece flexibilidad de desarrollador de hello en la elección de Hola de serializador de Hola.</span><span class="sxs-lookup"><span data-stu-id="adaba-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="adaba-182">Objetos de tooserialize de una manera sencilla es hello toouse `JsonConvert` métodos de serialización en [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) y serializar tooand de JSON.</span><span class="sxs-lookup"><span data-stu-id="adaba-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="adaba-183">Hello en el ejemplo siguiente se muestra un get y set utilizando un `Employee` instancia del objeto.</span><span class="sxs-lookup"><span data-stu-id="adaba-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="adaba-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="adaba-184">Next Steps</span></span>
<span data-ttu-id="adaba-185">Ahora que conoce los fundamentos de hello, siga estas toolearn de vínculos más información acerca de la caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="adaba-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="adaba-186">Desproteger Hola proveedores ASP.NET para caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="adaba-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="adaba-187">Proveedor de estado de sesión de Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="adaba-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="adaba-188">Proveedor de caché de resultados de ASP.NET de caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="adaba-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="adaba-189">[Habilitar los diagnósticos de caché](cache-how-to-monitor.md#enable-cache-diagnostics) para que pueda [monitor](cache-how-to-monitor.md) Hola estado de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="adaba-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="adaba-190">Puede ver hello las métricas de hello portal de Azure y también pueden [descargar y revisar](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) mediante herramientas de Hola de su elección.</span><span class="sxs-lookup"><span data-stu-id="adaba-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="adaba-191">Extraer del repositorio hello [documentación del cliente de caché de StackExchange.Redis][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="adaba-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="adaba-192">Se puede obtener acceso a Azure Redis Cache desde numerosos clientes de Redis y lenguajes de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="adaba-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="adaba-193">Para más información, consulte [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="adaba-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="adaba-194">Azure Redis Cache puede utilizarse también con herramientas como Redsmin y Redis Desktop Manager y servicios de terceros.</span><span class="sxs-lookup"><span data-stu-id="adaba-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="adaba-195">Para obtener más información sobre Redsmin, consulte [cómo tooretrieve una conexión a Redis de Azure, de cadena y usarlo con Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="adaba-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="adaba-196">Acceda e inspeccione los datos en Azure Redis Cache con una GUI mediante [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="adaba-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="adaba-197">Vea hello [redis] [ redis] documentación y obtener información acerca de [tipos de datos de redis] [ redis data types] y [una introducción de quince minutos tipos de datos de tooRedis][a fifteen minute introduction tooRedis data types].</span><span class="sxs-lookup"><span data-stu-id="adaba-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


