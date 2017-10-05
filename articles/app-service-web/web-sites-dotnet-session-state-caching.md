---
title: "Estado de sesión con caché en Redis de Azure en el Servicio de aplicaciones de Azure"
description: "Obtenga información acerca de cómo usar el servicio de caché de Azure para admitir la caché de estado de sesión de ASP.NET."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: 64fa909daf92b2b1f0cf4c7b334edba807fe7228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="cab58-103">Estado de sesión con caché en Redis de Azure en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="cab58-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="cab58-104">En este tema se explica cómo utilizar el servicio Caché en Redis de Azure para el estado de sesión.</span><span class="sxs-lookup"><span data-stu-id="cab58-104">This topic explains how to use the Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="cab58-105">Si su aplicación de ASP.NET utiliza el estado de sesión, deberá configurar un proveedor externo del estado de sesión (bien un servicio Caché en Redis o un proveedor de estado de sesión del SQL Server).</span><span class="sxs-lookup"><span data-stu-id="cab58-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="cab58-106">Si utiliza el estado de sesión y no utiliza un proveedor externo, deberá limitar su aplicación web a una instancia.</span><span class="sxs-lookup"><span data-stu-id="cab58-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span></span> <span data-ttu-id="cab58-107">El servicio Caché en Redis es el más sencillo y rápido que se puede habilitar.</span><span class="sxs-lookup"><span data-stu-id="cab58-107">The Redis Cache Service is the fastest and simplest to enable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="cab58-108"><a id="createcache"></a>Creación de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="cab58-108"><a id="createcache"></a>Create the Cache</span></span>
<span data-ttu-id="cab58-109">Siga [estas instrucciones](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) para crear la caché.</span><span class="sxs-lookup"><span data-stu-id="cab58-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span></span>

## <span data-ttu-id="cab58-110"><a id="configureproject"></a>Incorporación del paquete NuGet RedisSessionStateProvider a su aplicación web</span><span class="sxs-lookup"><span data-stu-id="cab58-110"><a id="configureproject"></a>Add the RedisSessionStateProvider NuGet package to your web app</span></span>
<span data-ttu-id="cab58-111">Instale el paquete NuGet `RedisSessionStateProvider` .</span><span class="sxs-lookup"><span data-stu-id="cab58-111">Install the NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="cab58-112">Utilice el comando siguiente para realizar la instalación desde la consola del administrador de paquetes (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span><span class="sxs-lookup"><span data-stu-id="cab58-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="cab58-113">Para instalar desde **Herramientas** > **Administrador de paquetes de NuGet** > **Administrar paquetes de NuGet para solución**, busque `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="cab58-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="cab58-114">Para obtener más información, vea la página [NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) y [Configuración de los clientes de caché](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="cab58-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="cab58-115"><a id="configurewebconfig"></a>Modificación del archivo web.config</span><span class="sxs-lookup"><span data-stu-id="cab58-115"><a id="configurewebconfig"></a>Modify the Web.Config File</span></span>
<span data-ttu-id="cab58-116">Además de hacer referencias de ensamblado para la memoria caché, el paquete NuGet agrega entradas auxiliares en el archivo *web.config* .</span><span class="sxs-lookup"><span data-stu-id="cab58-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span></span> 

1. <span data-ttu-id="cab58-117">Abra el archivo *web.config* y busque el elemento **sessionState** .</span><span class="sxs-lookup"><span data-stu-id="cab58-117">Open the *web.config* and find the the **sessionState** element.</span></span>
2. <span data-ttu-id="cab58-118">Introduzca los valores de `host`, `accessKey`, `port` (el puerto de SSL debe ser el 6380) y establezca `SSL` en `true`.</span><span class="sxs-lookup"><span data-stu-id="cab58-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span></span> <span data-ttu-id="cab58-119">Estos valores se pueden obtener en el cuadro del portal de vista previa de la hoja [Portal Azure](http://go.microsoft.com/fwlink/?LinkId=529715) para su instancia de caché.</span><span class="sxs-lookup"><span data-stu-id="cab58-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="cab58-120">Para obtener más información, vea [Conexión con la memoria caché](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="cab58-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="cab58-121">Tenga en cuenta que el puerto no SSL está deshabilitado de forma predeterminada para las cachés nuevas.</span><span class="sxs-lookup"><span data-stu-id="cab58-121">Note that the non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="cab58-122">Para más información sobre cómo habilitar el puerto no SSL, consulte la sección [Puertos de acceso](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) del tema de [Configuración de caché en Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx).</span><span class="sxs-lookup"><span data-stu-id="cab58-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="cab58-123">El siguiente marcado muestra los cambios realizados en el *web.config* de archivos, en concreto los cambios realizados en *puerto*, *host*, accessKey * y *ssl* .</span><span class="sxs-lookup"><span data-stu-id="cab58-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey*, and *ssl*.</span></span>
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <span data-ttu-id="cab58-124"><a id="usesessionobject"></a> Uso del objeto Session en el código</span><span class="sxs-lookup"><span data-stu-id="cab58-124"><a id="usesessionobject"></a> Use the Session Object in Code</span></span>
<span data-ttu-id="cab58-125">El paso final es comenzar a utilizar el objeto Session en su código ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cab58-125">The final step is to begin using the Session object in your ASP.NET code.</span></span> <span data-ttu-id="cab58-126">Agregue objetos al estado de sesión con el método **Session.Add** .</span><span class="sxs-lookup"><span data-stu-id="cab58-126">You add objects to session state by using the **Session.Add** method.</span></span> <span data-ttu-id="cab58-127">Este método utiliza pares clave-valor para almacenar elementos en la caché de estado de sesión.</span><span class="sxs-lookup"><span data-stu-id="cab58-127">This method uses key-value pairs to store items in the session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="cab58-128">El siguiente código recupera este valor desde el estado de sesión.</span><span class="sxs-lookup"><span data-stu-id="cab58-128">The following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="cab58-129">También puede usar el servicio Caché en Redis para almacenar objetos en la memoria caché en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cab58-129">You can also use the Redis Cache to cache objects in your web app.</span></span> <span data-ttu-id="cab58-130">Para obtener más información, consulte [Aplicación de películas MVC con Caché en Redis de Azure en 15 minutos](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="cab58-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="cab58-131">Para más detalles acerca de cómo utilizar el estado de sesión de ASP.NET, consulte [Información general sobre el estado de sesión de ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="cab58-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="cab58-132">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de suscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cab58-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="cab58-133">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="cab58-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="cab58-134">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="cab58-134">What's changed</span></span>
* <span data-ttu-id="cab58-135">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="cab58-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="cab58-136">*Por [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="cab58-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed the latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

