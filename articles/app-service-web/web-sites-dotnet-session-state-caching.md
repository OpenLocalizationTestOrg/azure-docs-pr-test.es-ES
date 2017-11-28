---
title: "estado de aaaSession con caché en Redis de Azure en el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo toouse Hola caché de estado de sesión de servicio de caché de Azure toosupport ASP.NET."
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
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="c27b9-103">Estado de sesión con caché en Redis de Azure en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c27b9-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="c27b9-104">Este tema explica cómo toouse Hola servicio de caché de Redis de Azure para el estado de sesión.</span><span class="sxs-lookup"><span data-stu-id="c27b9-104">This topic explains how toouse hello Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="c27b9-105">Si la aplicación web ASP.NET utiliza el estado de sesión, deberá tooconfigure un proveedor de estado de sesión externo (Hola servicio de caché de Redis o un proveedor de estado de sesión de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="c27b9-105">If your ASP.NET web app uses session state, you will need tooconfigure an external session state provider (either hello Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="c27b9-106">Si utiliza el estado de sesión y no use un proveedor externo, es posible que tooone limitado de instancia de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c27b9-106">If you use session state, and don't use an external provider, you will be limited tooone instance of your web app.</span></span> <span data-ttu-id="c27b9-107">Hola servicio de caché de Redis es tooenable de hello más rápido y sencillo.</span><span class="sxs-lookup"><span data-stu-id="c27b9-107">hello Redis Cache Service is hello fastest and simplest tooenable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="c27b9-108"><a id="createcache"></a>Crear hello caché</span><span class="sxs-lookup"><span data-stu-id="c27b9-108"><a id="createcache"></a>Create hello Cache</span></span>
<span data-ttu-id="c27b9-109">Siga [estas instrucciones](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) caché de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="c27b9-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello cache.</span></span>

## <span data-ttu-id="c27b9-110"><a id="configureproject"></a>Agregar hello RedisSessionStateProvider NuGet paquete tooyour web app</span><span class="sxs-lookup"><span data-stu-id="c27b9-110"><a id="configureproject"></a>Add hello RedisSessionStateProvider NuGet package tooyour web app</span></span>
<span data-ttu-id="c27b9-111">Instalar Hola NuGet `RedisSessionStateProvider` paquete.</span><span class="sxs-lookup"><span data-stu-id="c27b9-111">Install hello NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="c27b9-112">Siguiente Hola de uso del comando tooinstall desde la consola del Administrador de paquetes de saludo (**herramientas** > **Administrador de paquetes de NuGet** > **Package Manager Console**):</span><span class="sxs-lookup"><span data-stu-id="c27b9-112">Use hello following command tooinstall from hello package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="c27b9-113">tooinstall de **herramientas** > **Administrador de paquetes de NuGet** > **administrar paquetes de Consejo para solución**, busque `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="c27b9-113">tooinstall from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="c27b9-114">Para obtener más información, vea hello [página NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) y [configurar cliente de caché de hello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="c27b9-114">For more information see hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure hello cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="c27b9-115"><a id="configurewebconfig"></a>Modificar el archivo Web.Config de Hola</span><span class="sxs-lookup"><span data-stu-id="c27b9-115"><a id="configurewebconfig"></a>Modify hello Web.Config File</span></span>
<span data-ttu-id="c27b9-116">Además toomaking ensamblado hace referencia para la memoria caché, paquete de NuGet Hola agrega las entradas de código auxiliar en hello *web.config* archivo.</span><span class="sxs-lookup"><span data-stu-id="c27b9-116">In addition toomaking assembly references for Cache, hello NuGet package adds stub entries in hello *web.config* file.</span></span> 

1. <span data-ttu-id="c27b9-117">Abra hello *web.config* y encontrar Hola Hola **sessionState** elemento.</span><span class="sxs-lookup"><span data-stu-id="c27b9-117">Open hello *web.config* and find hello hello **sessionState** element.</span></span>
2. <span data-ttu-id="c27b9-118">Especifique los valores de hello de `host`, `accessKey`, `port` (Hola puerto SSL debe ser 6380) y establecer `SSL` demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="c27b9-118">Enter hello values for `host`, `accessKey`, `port` (hello SSL port should be 6380), and set `SSL` too`true`.</span></span> <span data-ttu-id="c27b9-119">Estos valores se pueden obtener de hello [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715) hoja para la instancia de caché.</span><span class="sxs-lookup"><span data-stu-id="c27b9-119">These values can be obtained from hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="c27b9-120">Para obtener más información, consulte [conectar toohello caché](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="c27b9-120">For more information, see [Connect toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="c27b9-121">Observe que el puerto no SSL de hello está deshabilitado de forma predeterminada para las nuevas cachés.</span><span class="sxs-lookup"><span data-stu-id="c27b9-121">Note that hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="c27b9-122">Para obtener más información acerca de cómo habilitar el puerto no SSL de hello, vea hello [puertos de acceso](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) sección Hola [configurar una memoria caché en Redis de Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="c27b9-122">For more information about enabling hello non-SSL port, see hello [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in hello [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="c27b9-123">Hello marcado siguiente muestra hello cambios toohello *web.config* de archivos, en concreto los cambios de hello demasiado*puerto*, *host*, accessKey * y *ssl*.</span><span class="sxs-lookup"><span data-stu-id="c27b9-123">hello following markup shows hello changes toohello *web.config* file, specifically hello changes too*port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="c27b9-124"><a id="usesessionobject"></a>Usar objeto Session de hello en el código</span><span class="sxs-lookup"><span data-stu-id="c27b9-124"><a id="usesessionobject"></a> Use hello Session Object in Code</span></span>
<span data-ttu-id="c27b9-125">Hola último paso es toobegin con objeto de sesión de hello en el código ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c27b9-125">hello final step is toobegin using hello Session object in your ASP.NET code.</span></span> <span data-ttu-id="c27b9-126">Agrega objetos toosession estado mediante el uso de hello **método Session.Add** método.</span><span class="sxs-lookup"><span data-stu-id="c27b9-126">You add objects toosession state by using hello **Session.Add** method.</span></span> <span data-ttu-id="c27b9-127">Este método usa elementos toostore de pares clave-valor en memoria caché de estado de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="c27b9-127">This method uses key-value pairs toostore items in hello session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="c27b9-128">Hola siguiente código recupera este valor de estado de sesión.</span><span class="sxs-lookup"><span data-stu-id="c27b9-128">hello following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="c27b9-129">También puede utilizar objetos de toocache de caché en Redis de hello en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c27b9-129">You can also use hello Redis Cache toocache objects in your web app.</span></span> <span data-ttu-id="c27b9-130">Para obtener más información, consulte [Aplicación de películas MVC con Caché en Redis de Azure en 15 minutos](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="c27b9-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="c27b9-131">Para obtener más información acerca de cómo toouse estado de sesión ASP.NET, vea [información general sobre el estado de sesión de ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="c27b9-131">For more details about how toouse ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="c27b9-132">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c27b9-132">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c27b9-133">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="c27b9-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="c27b9-134">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="c27b9-134">What's changed</span></span>
* <span data-ttu-id="c27b9-135">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c27b9-135">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="c27b9-136">*Por [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="c27b9-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

