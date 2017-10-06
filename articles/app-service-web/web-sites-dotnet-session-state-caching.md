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
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a>Estado de sesión con caché en Redis de Azure en el Servicio de aplicaciones de Azure
Este tema explica cómo toouse Hola servicio de caché de Redis de Azure para el estado de sesión.

Si la aplicación web ASP.NET utiliza el estado de sesión, deberá tooconfigure un proveedor de estado de sesión externo (Hola servicio de caché de Redis o un proveedor de estado de sesión de SQL Server). Si utiliza el estado de sesión y no use un proveedor externo, es posible que tooone limitado de instancia de la aplicación web. Hola servicio de caché de Redis es tooenable de hello más rápido y sencillo.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="createcache"></a>Crear hello caché
Siga [estas instrucciones](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) caché de hello toocreate.

## <a id="configureproject"></a>Agregar hello RedisSessionStateProvider NuGet paquete tooyour web app
Instalar Hola NuGet `RedisSessionStateProvider` paquete.  Siguiente Hola de uso del comando tooinstall desde la consola del Administrador de paquetes de saludo (**herramientas** > **Administrador de paquetes de NuGet** > **Package Manager Console**):

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

tooinstall de **herramientas** > **Administrador de paquetes de NuGet** > **administrar paquetes de Consejo para solución**, busque `RedisSessionStateProvider`.

Para obtener más información, vea hello [página NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) y [configurar cliente de caché de hello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).

## <a id="configurewebconfig"></a>Modificar el archivo Web.Config de Hola
Además toomaking ensamblado hace referencia para la memoria caché, paquete de NuGet Hola agrega las entradas de código auxiliar en hello *web.config* archivo. 

1. Abra hello *web.config* y encontrar Hola Hola **sessionState** elemento.
2. Especifique los valores de hello de `host`, `accessKey`, `port` (Hola puerto SSL debe ser 6380) y establecer `SSL` demasiado`true`. Estos valores se pueden obtener de hello [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715) hoja para la instancia de caché. Para obtener más información, consulte [conectar toohello caché](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache). Observe que el puerto no SSL de hello está deshabilitado de forma predeterminada para las nuevas cachés. Para obtener más información acerca de cómo habilitar el puerto no SSL de hello, vea hello [puertos de acceso](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) sección Hola [configurar una memoria caché en Redis de Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) tema. Hello marcado siguiente muestra hello cambios toohello *web.config* de archivos, en concreto los cambios de hello demasiado*puerto*, *host*, accessKey * y *ssl*.
   
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

## <a id="usesessionobject"></a>Usar objeto Session de hello en el código
Hola último paso es toobegin con objeto de sesión de hello en el código ASP.NET. Agrega objetos toosession estado mediante el uso de hello **método Session.Add** método. Este método usa elementos toostore de pares clave-valor en memoria caché de estado de sesión de Hola.

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

Hola siguiente código recupera este valor de estado de sesión.

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

También puede utilizar objetos de toocache de caché en Redis de hello en la aplicación web. Para obtener más información, consulte [Aplicación de películas MVC con Caché en Redis de Azure en 15 minutos](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).
Para obtener más información acerca de cómo toouse estado de sesión ASP.NET, vea [información general sobre el estado de sesión de ASP.NET][ASP.NET Session State Overview].

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)
  
  *Por [Rick Anderson](https://twitter.com/RickAndMSFT)*

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

