---
title: "aaaCache proveedor de caché de resultados de ASP.NET"
description: "Obtenga información acerca de cómo toocache con caché en Redis de Azure de resultados de página ASP.NET"
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
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="99c2c-103">Proveedor de caché de salida de ASP.NET para Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="99c2c-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="99c2c-104">Hola Redis proveedor de caché de resultados es un mecanismo de almacenamiento fuera de proceso para los datos de la caché de salida.</span><span class="sxs-lookup"><span data-stu-id="99c2c-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="99c2c-105">Estos datos resultan necesarios específicamente para respuestas HTTP completas (caché de resultados de la página).</span><span class="sxs-lookup"><span data-stu-id="99c2c-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="99c2c-106">Hola proveedor se conecta Hola nueva salida caché proveedor punto de extensibilidad que se introdujo en ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="99c2c-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="99c2c-107">Hola toouse proveedor de caché de salida Redis, primero configure la caché y, a continuación, configure la aplicación de ASP.NET mediante el paquete de NuGet de proveedor de caché de resultados en Redis de Hola.</span><span class="sxs-lookup"><span data-stu-id="99c2c-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="99c2c-108">Este tema proporciona instrucciones sobre cómo configurar su Hola de toouse aplicación Redis proveedor de caché de resultados.</span><span class="sxs-lookup"><span data-stu-id="99c2c-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="99c2c-109">Para obtener más información sobre cómo crear y configurar una instancia de Caché en Redis de Azure, consulte [Creación de una caché](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="99c2c-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="99c2c-110">Almacenar el resultado de la página ASP.NET en caché de Hola</span><span class="sxs-lookup"><span data-stu-id="99c2c-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="99c2c-111">tooconfigure una aplicación cliente en Visual Studio con paquete de NuGet de estado de sesión de caché de Redis hello, haga clic en **Administrador de paquetes de NuGet**, **Package Manager Console** de hello **herramientas** menú.</span><span class="sxs-lookup"><span data-stu-id="99c2c-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="99c2c-112">Ejecución hello después del comando de hello `Package Manager Console` ventana.</span><span class="sxs-lookup"><span data-stu-id="99c2c-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="99c2c-113">paquete de NuGet de proveedor de caché de resultados en Redis Hello tiene una dependencia en el paquete StackExchange.Redis.StrongName de Hola.</span><span class="sxs-lookup"><span data-stu-id="99c2c-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="99c2c-114">Si el paquete de hello StackExchange.Redis.StrongName no está presente en el proyecto, se instala.</span><span class="sxs-lookup"><span data-stu-id="99c2c-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="99c2c-115">Para obtener más información sobre el paquete de NuGet de proveedor de caché de resultados en Redis hello, vea hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) página de NuGet.</span><span class="sxs-lookup"><span data-stu-id="99c2c-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="99c2c-116">En suma toohello seguro-paquete StackExchange.Redis.StrongName con nombre, también hay hello StackExchange.Redis no seguro-versión con nombre.</span><span class="sxs-lookup"><span data-stu-id="99c2c-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="99c2c-117">Si el proyecto usa hello no-con nombre seguro StackExchange.Redis versión, debe desinstalarla, en caso contrario, conflictos de nomenclatura en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="99c2c-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="99c2c-118">Para obtener más información sobre estos paquetes, consulte [Configuración de los clientes de la caché de .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="99c2c-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="99c2c-119">Hola NuGet paquete descarga y agrega Hola requiere referencias de ensamblado y agrega la siguiente sección al archivo web.config de Hola.</span><span class="sxs-lookup"><span data-stu-id="99c2c-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="99c2c-120">Esta sección contiene la configuración necesaria de Hola para su hello toouse de aplicación de ASP.NET Redis proveedor de caché de resultados.</span><span class="sxs-lookup"><span data-stu-id="99c2c-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

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

<span data-ttu-id="99c2c-121">Hola comentadas sección proporciona un ejemplo de Hola atributos y su configuración para cada atributo.</span><span class="sxs-lookup"><span data-stu-id="99c2c-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="99c2c-122">Configurar atributos de hello con valores de hello de la hoja de la caché en el portal de Microsoft Azure hello y configurar Hola otros valores según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="99c2c-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="99c2c-123">Para obtener instrucciones sobre cómo acceder a las propiedades de caché, consulte [Configuración de la caché en Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="99c2c-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="99c2c-124">**host** : especifique el punto de conexión de la caché.</span><span class="sxs-lookup"><span data-stu-id="99c2c-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="99c2c-125">**puerto** : usar el puerto no SSL o el puerto SSL, dependiendo de la configuración de ssl Hola.</span><span class="sxs-lookup"><span data-stu-id="99c2c-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="99c2c-126">**accessKey** : usar cualquier clave primaria o secundaria de saludo de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="99c2c-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="99c2c-127">**SSL** : true si desea toosecure caché-cliente con ssl; de lo contrario, false.</span><span class="sxs-lookup"><span data-stu-id="99c2c-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="99c2c-128">Estar seguro de puerto correcto de toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="99c2c-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="99c2c-129">puerto no SSL de Hello está deshabilitado de forma predeterminada para las nuevas cachés.</span><span class="sxs-lookup"><span data-stu-id="99c2c-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="99c2c-130">Especifique true para esta Hola de toouse configuración puerto SSL.</span><span class="sxs-lookup"><span data-stu-id="99c2c-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="99c2c-131">Para obtener más información acerca de cómo habilitar el puerto no SSL de hello, vea hello [puertos de acceso](cache-configure.md#access-ports) sección Hola [configurar una memoria caché](cache-configure.md) tema.</span><span class="sxs-lookup"><span data-stu-id="99c2c-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="99c2c-132">**databaseId** : Specified qué toouse de base de datos de la memoria caché los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="99c2c-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="99c2c-133">Si no se especifica, se utiliza Hola valor predeterminado de 0.</span><span class="sxs-lookup"><span data-stu-id="99c2c-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="99c2c-134">**applicationName**: las claves se almacenan en Redis como `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="99c2c-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="99c2c-135">Este esquema de nomenclatura permite Hola de tooshare de varias aplicaciones misma clave.</span><span class="sxs-lookup"><span data-stu-id="99c2c-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="99c2c-136">Este parámetro es opcional y, si no se especifica, se usa un valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="99c2c-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="99c2c-137">**connectionTimeoutInMilliseconds** : esta configuración le permite toooverride Hola connectTimeout configuración de cliente de StackExchange.Redis Hola.</span><span class="sxs-lookup"><span data-stu-id="99c2c-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="99c2c-138">Si no se especifica, se utiliza configuración de connectTimeout Hola predeterminado de 5000.</span><span class="sxs-lookup"><span data-stu-id="99c2c-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="99c2c-139">Para obtener más información, consulte el [modelo de configuración de StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="99c2c-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="99c2c-140">**operationTimeoutInMilliseconds** : esta configuración le permite toooverride hello syncTimeout configuración de cliente de StackExchange.Redis Hola.</span><span class="sxs-lookup"><span data-stu-id="99c2c-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="99c2c-141">Si no se especifica, se usa la configuración de syncTimeout de predeterminada de Hola de 1000.</span><span class="sxs-lookup"><span data-stu-id="99c2c-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="99c2c-142">Para obtener más información, consulte el [modelo de configuración de StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="99c2c-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="99c2c-143">Agregue una página de tooeach directiva OutputCache para el que desea salida de hello toocache.</span><span class="sxs-lookup"><span data-stu-id="99c2c-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="99c2c-144">En el ejemplo anterior de hello, Hola almacenado en memoria caché de datos de página permanece en memoria caché de Hola durante 60 segundos y se almacena en caché una versión diferente de la página de Hola para cada combinación de parámetros.</span><span class="sxs-lookup"><span data-stu-id="99c2c-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="99c2c-145">Para obtener más información acerca de la directiva OutputCache hello, consulte [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="99c2c-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="99c2c-146">Una vez realizados estos pasos, la aplicación es toouse configurado hello Redis proveedor de caché de resultados.</span><span class="sxs-lookup"><span data-stu-id="99c2c-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99c2c-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99c2c-147">Next steps</span></span>
<span data-ttu-id="99c2c-148">Extraer del repositorio hello [proveedor de estado de sesión de ASP.NET para caché en Redis de Azure](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="99c2c-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

