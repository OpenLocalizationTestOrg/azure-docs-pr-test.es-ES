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
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>Proveedor de caché de salida de ASP.NET para Caché en Redis de Azure
Hola Redis proveedor de caché de resultados es un mecanismo de almacenamiento fuera de proceso para los datos de la caché de salida. Estos datos resultan necesarios específicamente para respuestas HTTP completas (caché de resultados de la página). Hola proveedor se conecta Hola nueva salida caché proveedor punto de extensibilidad que se introdujo en ASP.NET 4.

Hola toouse proveedor de caché de salida Redis, primero configure la caché y, a continuación, configure la aplicación de ASP.NET mediante el paquete de NuGet de proveedor de caché de resultados en Redis de Hola. Este tema proporciona instrucciones sobre cómo configurar su Hola de toouse aplicación Redis proveedor de caché de resultados. Para obtener más información sobre cómo crear y configurar una instancia de Caché en Redis de Azure, consulte [Creación de una caché](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

## <a name="store-aspnet-page-output-in-hello-cache"></a>Almacenar el resultado de la página ASP.NET en caché de Hola
tooconfigure una aplicación cliente en Visual Studio con paquete de NuGet de estado de sesión de caché de Redis hello, haga clic en **Administrador de paquetes de NuGet**, **Package Manager Console** de hello **herramientas** menú.

Ejecución hello después del comando de hello `Package Manager Console` ventana.
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

paquete de NuGet de proveedor de caché de resultados en Redis Hello tiene una dependencia en el paquete StackExchange.Redis.StrongName de Hola. Si el paquete de hello StackExchange.Redis.StrongName no está presente en el proyecto, se instala. Para obtener más información sobre el paquete de NuGet de proveedor de caché de resultados en Redis hello, vea hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) página de NuGet.

>[!NOTE]
>En suma toohello seguro-paquete StackExchange.Redis.StrongName con nombre, también hay hello StackExchange.Redis no seguro-versión con nombre. Si el proyecto usa hello no-con nombre seguro StackExchange.Redis versión, debe desinstalarla, en caso contrario, conflictos de nomenclatura en el proyecto. Para obtener más información sobre estos paquetes, consulte [Configuración de los clientes de la caché de .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hola NuGet paquete descarga y agrega Hola requiere referencias de ensamblado y agrega la siguiente sección al archivo web.config de Hola. Esta sección contiene la configuración necesaria de Hola para su hello toouse de aplicación de ASP.NET Redis proveedor de caché de resultados.

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

Hola comentadas sección proporciona un ejemplo de Hola atributos y su configuración para cada atributo.

Configurar atributos de hello con valores de hello de la hoja de la caché en el portal de Microsoft Azure hello y configurar Hola otros valores según sea necesario. Para obtener instrucciones sobre cómo acceder a las propiedades de caché, consulte [Configuración de la caché en Redis](cache-configure.md#configure-redis-cache-settings).

* **host** : especifique el punto de conexión de la caché.
* **puerto** : usar el puerto no SSL o el puerto SSL, dependiendo de la configuración de ssl Hola.
* **accessKey** : usar cualquier clave primaria o secundaria de saludo de la memoria caché.
* **SSL** : true si desea toosecure caché-cliente con ssl; de lo contrario, false. Estar seguro de puerto correcto de toospecify Hola.
  * puerto no SSL de Hello está deshabilitado de forma predeterminada para las nuevas cachés. Especifique true para esta Hola de toouse configuración puerto SSL. Para obtener más información acerca de cómo habilitar el puerto no SSL de hello, vea hello [puertos de acceso](cache-configure.md#access-ports) sección Hola [configurar una memoria caché](cache-configure.md) tema.
* **databaseId** : Specified qué toouse de base de datos de la memoria caché los datos de salida. Si no se especifica, se utiliza Hola valor predeterminado de 0.
* **applicationName**: las claves se almacenan en Redis como `<AppName>_<SessionId>_Data`. Este esquema de nomenclatura permite Hola de tooshare de varias aplicaciones misma clave. Este parámetro es opcional y, si no se especifica, se usa un valor predeterminado.
* **connectionTimeoutInMilliseconds** : esta configuración le permite toooverride Hola connectTimeout configuración de cliente de StackExchange.Redis Hola. Si no se especifica, se utiliza configuración de connectTimeout Hola predeterminado de 5000. Para obtener más información, consulte el [modelo de configuración de StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** : esta configuración le permite toooverride hello syncTimeout configuración de cliente de StackExchange.Redis Hola. Si no se especifica, se usa la configuración de syncTimeout de predeterminada de Hola de 1000. Para obtener más información, consulte el [modelo de configuración de StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Agregue una página de tooeach directiva OutputCache para el que desea salida de hello toocache.

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

En el ejemplo anterior de hello, Hola almacenado en memoria caché de datos de página permanece en memoria caché de Hola durante 60 segundos y se almacena en caché una versión diferente de la página de Hola para cada combinación de parámetros. Para obtener más información acerca de la directiva OutputCache hello, consulte [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).

Una vez realizados estos pasos, la aplicación es toouse configurado hello Redis proveedor de caché de resultados.

## <a name="next-steps"></a>Pasos siguientes
Extraer del repositorio hello [proveedor de estado de sesión de ASP.NET para caché en Redis de Azure](cache-aspnet-session-state-provider.md).

