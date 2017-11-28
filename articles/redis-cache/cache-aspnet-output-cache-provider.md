---
title: "Proveedor de la caché de salida de ASP.NET"
description: "Obtenga información sobre cómo almacenar en caché los resultados de página de ASP.NET con Caché en Redis de Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: 845f25637a0e48460fc76c1ee36060274b3cec38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="bfdfe-103">Proveedor de caché de salida de ASP.NET para Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="bfdfe-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="bfdfe-104">El proveedor de la caché de salida de Redis es un mecanismo de almacenamiento fuera de proceso para los datos de la caché de salida.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-104">The Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="bfdfe-105">Estos datos resultan necesarios específicamente para respuestas HTTP completas (caché de resultados de la página).</span><span class="sxs-lookup"><span data-stu-id="bfdfe-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="bfdfe-106">El proveedor se conecta al nuevo punto de extensibilidad del proveedor de caché de salida que se introdujo en ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-106">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="bfdfe-107">Para usar el proveedor de la caché de salida de Redis, configure primero la caché y luego configure la aplicación de ASP.NET mediante el paquete NuGet del proveedor de la caché de salida de Redis.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-107">To use the Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using the Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="bfdfe-108">En este tema se proporcionan instrucciones sobre cómo configurar la aplicación para usar el proveedor de la caché de salida de Redis.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-108">This topic provides guidance on configuring your application to use the Redis Output Cache Provider.</span></span> <span data-ttu-id="bfdfe-109">Para obtener más información sobre cómo crear y configurar una instancia de Caché en Redis de Azure, consulte [Creación de una caché](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="bfdfe-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-the-cache"></a><span data-ttu-id="bfdfe-110">Almacenamiento de los resultados de página de ASP.NET en la caché</span><span class="sxs-lookup"><span data-stu-id="bfdfe-110">Store ASP.NET page output in the cache</span></span>
<span data-ttu-id="bfdfe-111">Para configurar una aplicación cliente en Visual Studio usando el paquete NuGet de estado de sesiones de Redis Cache, haga clic en **Administrar paquetes NuGet**, **Consola del administrador de paquetes** en el menú **Herramientas**.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-111">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>

<span data-ttu-id="bfdfe-112">Ejecute el siguiente comando desde la ventana `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-112">Run the following command from the `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="bfdfe-113">El paquete NuGet del proveedor de la caché de salida de Redis tiene una dependencia del paquete StackExchange.Redis.StrongName.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-113">The Redis Output Cache Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="bfdfe-114">Si el paquete StackExchange.Redis.StrongName no existe en el proyecto, se instalará.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-114">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="bfdfe-115">Para obtener más información sobre el paquete de NuGet del proveedor de caché de salida de Redis, vea la página [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) de NuGet.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-115">For more information about the Redis Output Cache Provider NuGet package, see the [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="bfdfe-116">Tenga en cuenta que, además del paquete StackExchange.Redis.StrongName con nombre seguro, también está la versión con nombre no seguro de StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-116">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="bfdfe-117">Si su proyecto está utilizando la versión de StackExchange.Redis con nombre no seguro deberá desinstalarla, ya que de lo contrario se producirán conflictos de nomenclatura en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-117">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="bfdfe-118">Para obtener más información sobre estos paquetes, consulte [Configuración de los clientes de la caché de .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="bfdfe-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="bfdfe-119">El paquete NuGet descarga y agrega las referencias de ensamblado necesarias y agrega la siguiente sección al archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-119">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span></span> <span data-ttu-id="bfdfe-120">Esta sección contiene la configuración necesaria para que la aplicación ASP.NET use el proveedor de memoria caché de salida de Redis.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-120">This section contains the required configuration for your ASP.NET application to use the Redis Output Cache Provider.</span></span>

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

<span data-ttu-id="bfdfe-121">En la sección comentada se proporciona un ejemplo de los atributos y la configuración de ejemplo de cada uno.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-121">The commented section provides an example of the attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="bfdfe-122">Configure los atributos con los valores de la hoja de la caché en el Portal de Microsoft Azure y configure los demás valores según prefiera.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-122">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span></span> <span data-ttu-id="bfdfe-123">Para obtener instrucciones sobre cómo acceder a las propiedades de caché, consulte [Configuración de la caché en Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="bfdfe-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="bfdfe-124">**host** : especifique el punto de conexión de la caché.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="bfdfe-125">**puerto** : use el puerto no SSL o SSL, según la configuración de SSL.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-125">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span></span>
* <span data-ttu-id="bfdfe-126">**accessKey** : use la clave primaria o secundaria para la caché.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-126">**accessKey** – use either the primary or secondary key for your cache.</span></span>
* <span data-ttu-id="bfdfe-127">**ssl** : true si desea proteger las comunicaciones de la caché o el cliente con SLS; de lo contrario, false.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-127">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="bfdfe-128">Asegúrese de especificar el puerto correcto.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-128">Be sure to specify the correct port.</span></span>
  * <span data-ttu-id="bfdfe-129">El puerto no SSL está deshabilitado de forma predeterminada para las cachés nuevas.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-129">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="bfdfe-130">Especifique true en este valor para usar el puerto SSL.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-130">Specify true for this setting to use the SSL port.</span></span> <span data-ttu-id="bfdfe-131">Para más información sobre cómo habilitar el puerto no SSL, consulte la sección [Puertos de acceso](cache-configure.md#access-ports) del tema de [Configuración de caché](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bfdfe-131">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="bfdfe-132">**databaseId** : especifique qué base de datos se usará para los datos de salida de la caché.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-132">**databaseId** – Specified which database to use for cache output data.</span></span> <span data-ttu-id="bfdfe-133">Si no se especifica, se usa el valor predeterminado de 0.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-133">If not specified, the default value of 0 is used.</span></span>
* <span data-ttu-id="bfdfe-134">**applicationName**: las claves se almacenan en Redis como `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="bfdfe-135">Este esquema de nomenclatura permite que varias aplicaciones compartan la misma clave.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-135">This naming scheme enables multiple applications to share the same key.</span></span> <span data-ttu-id="bfdfe-136">Este parámetro es opcional y, si no se especifica, se usa un valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="bfdfe-137">**connectionTimeoutInMilliseconds** : esta opción le permite invalidar la configuración de connectTimeout en el cliente de StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-137">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="bfdfe-138">Si no se especifica, se usa el valor predeterminado de connectTimeout, que es 5000.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-138">If not specified, the default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="bfdfe-139">Para obtener más información, consulte el [modelo de configuración de StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="bfdfe-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="bfdfe-140">**operationTimeoutInMilliseconds** : esta opción le permite invalidar la configuración de syncTimeout en el cliente de StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-140">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="bfdfe-141">Si no se especifica, se usa el valor predeterminado de syncTimeout, que es 1000.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-141">If not specified, the default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="bfdfe-142">Para obtener más información, consulte el [modelo de configuración de StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="bfdfe-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="bfdfe-143">Incorpore una directiva OutputCache a cada página cuyos resultados desea almacenar en caché.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-143">Add an OutputCache directive to each page for which you wish to cache the output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="bfdfe-144">En el ejemplo anterior, los datos de la página almacenados en la memoria caché permanecerán ahí durante 60 segundos y se almacenará en la memoria caché una versión diferente de la página para cada combinación de parámetros.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-144">In the previous example, the cached page data remains in the cache for 60 seconds, and a different version of the page is cached for each parameter combination.</span></span> <span data-ttu-id="bfdfe-145">Para obtener más información sobre la directiva OutputCache, consulte [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="bfdfe-145">For more information about the OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="bfdfe-146">Después de realizar estos pasos, la aplicación está configurada para usar el proveedor de la caché de salida de Redis.</span><span class="sxs-lookup"><span data-stu-id="bfdfe-146">Once these steps are performed, your application is configured to use the Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfdfe-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfdfe-147">Next steps</span></span>
<span data-ttu-id="bfdfe-148">Consulte el [proveedor de estado de sesión de ASP.NET para Caché en Redis de Azure](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="bfdfe-148">Check out the [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

