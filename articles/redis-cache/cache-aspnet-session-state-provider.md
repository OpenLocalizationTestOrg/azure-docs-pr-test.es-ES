---
title: "Proveedor de estado de sesión de ASP.NET aaaCache | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toostore con caché en Redis de Azure de estado de sesión ASP.NET"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Proveedor de estado de sesión de ASP.NET para Caché en Redis de Azure
Caché en Redis de Azure proporciona un proveedor de estado de sesión que puede usar toostore el estado de sesión en una memoria caché en lugar de en memoria o en un servidor SQL Server de base de datos. toouse Hola proveedor de estado de sesión de almacenamiento en caché, primero configure la caché y, a continuación, configure la aplicación de ASP.NET para la caché con el paquete de NuGet de estado de sesión de caché de Redis Hola.

A menudo no resulta práctico en un tooavoid de aplicación del mundo real en la nube almacenar algún tipo de estado para una sesión de usuario, pero algunos métodos afectan al rendimiento y la escalabilidad más que otros. Si tiene el estado de toostore, mejor solución de hello es tookeep Hola cantidad de pequeños de estado y almacenarlo en cookies. Si eso no es factible, siguiente mejor solución hello es toouse estado de sesión ASP.NET con un proveedor de caché distribuida en memoria. peor solución desde la perspectiva del rendimiento y la escalabilidad de Hello es toouse un proveedor de estado de sesión de copia de seguridad de base de datos. Este tema proporciona instrucciones sobre el uso de hello proveedor de estado de sesión de ASP.NET para caché en Redis de Azure. Para información sobre otras opciones de estado de sesión, consulte [Opciones de estado de sesión ASP.NET](#aspnet-session-state-options).

## <a name="store-aspnet-session-state-in-hello-cache"></a>Almacenar el estado de sesión ASP.NET en caché de Hola
tooconfigure una aplicación cliente en Visual Studio con paquete de NuGet de estado de sesión de caché de Redis hello, haga clic en **Administrador de paquetes de NuGet**, **Package Manager Console** de hello **herramientas** menú.

Ejecución hello después del comando de hello `Package Manager Console` ventana.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Si usas Hola característica de clústeres de nivel de hello premium, debe usar [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 o superior o una excepción se produce. Mover too2.0.1 o superior es un cambio brusco; Para obtener más información, consulte [v2.0.0 detalles de los cambios importantes](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details). En tiempo de presentación de este artículo se actualizó, versión actual de Hola de este paquete es 2.2.3.
> 
> 

paquete de NuGet de proveedor de estado de sesión de Redis Hello tiene una dependencia en el paquete StackExchange.Redis.StrongName de Hola. Si el paquete de hello StackExchange.Redis.StrongName no está presente en el proyecto, se instala.

>[!NOTE]
>En suma toohello seguro-paquete StackExchange.Redis.StrongName con nombre, también hay hello StackExchange.Redis no seguro-versión con nombre. Si el proyecto usa hello no-con nombre seguro StackExchange.Redis versión, debe desinstalarla, en caso contrario, conflictos de nomenclatura en el proyecto. Para obtener más información sobre estos paquetes, consulte [Configuración de los clientes de la caché de .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hola NuGet paquete descarga y agrega Hola requiere referencias de ensamblado y agrega la siguiente sección al archivo web.config de Hola. Esta sección contiene la configuración necesaria de Hola para su hello toouse de aplicación de ASP.NET proveedor de estado de sesión de caché de Redis.

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

Hola comentadas sección proporciona un ejemplo de Hola atributos y su configuración para cada atributo.

Configurar atributos de hello con valores de hello de la hoja de la caché en el portal de Microsoft Azure hello y configurar Hola otros valores según sea necesario. Para obtener instrucciones sobre cómo acceder a las propiedades de caché, consulte [Configuración de la caché en Redis](cache-configure.md#configure-redis-cache-settings).

* **host** : especifique el punto de conexión de la caché.
* **puerto** : usar el puerto no SSL o el puerto SSL, dependiendo de la configuración de ssl Hola.
* **accessKey** : usar cualquier clave primaria o secundaria de saludo de la memoria caché.
* **SSL** : true si desea toosecure caché-cliente con ssl; de lo contrario, false. Estar seguro de puerto correcto de toospecify Hola.
  * puerto no SSL de Hello está deshabilitado de forma predeterminada para las nuevas cachés. Especifique true para esta Hola de toouse configuración puerto SSL. Para obtener más información acerca de cómo habilitar el puerto no SSL de hello, vea hello [puertos de acceso](cache-configure.md#access-ports) sección Hola [configurar una memoria caché](cache-configure.md) tema.
* **throwOnError** : true si desea que un toobe de excepción que se produce si hay un error o false si desea toofail de operación de hello en modo silencioso. Puede comprobar si hay errores mediante la comprobación de propiedad Microsoft.Web.Redis.RedisSessionStateProvider.LastException estática de Hola. valor predeterminado de Hello es true.
* **retryTimeoutInMilliseconds** : durante este intervalo, especificado en milisegundos, se reintenta realizar las operaciones que generan errores. Hola primer reintento ocurre después de 20 milisegundos y, a continuación, los reintentos posteriores ocurren cada segundo hasta que expire el intervalo de saludo retryTimeoutInMilliseconds. Inmediatamente después de este intervalo, la operación de Hola se reintenta una última vez. Si Hola sigue fallando, Hola se devuelve excepción llamador toohello, dependiendo de la configuración de throwOnError Hola. valor predeterminado de Hello es 0, lo que no significa que no hay ningún reintento.
* **databaseId** : especifica qué toouse de base de datos de la memoria caché los datos de salida. Si no se especifica, se utiliza Hola valor predeterminado de 0.
* **applicationName`{<Application Name>_<Session ID>}_Data`: las claves se almacenan en Redis como** . Este esquema de nomenclatura permite que varias aplicaciones tooshare Hola la misma instancia de Redis. Este parámetro es opcional y, si no se especifica, se usa un valor predeterminado.
* **connectionTimeoutInMilliseconds** : esta configuración le permite toooverride Hola connectTimeout configuración de cliente de StackExchange.Redis Hola. Si no se especifica, se utiliza configuración de connectTimeout Hola predeterminado de 5000. Para obtener más información, consulte el [modelo de configuración de StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** : esta configuración le permite toooverride hello syncTimeout configuración de cliente de StackExchange.Redis Hola. Si no se especifica, se usa la configuración de syncTimeout de predeterminada de Hola de 1000. Para obtener más información, consulte el [modelo de configuración de StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Para obtener más información acerca de estas propiedades, consulte el anuncio de entrada de blog original de hello en [anuncio de proveedor de estado de sesión de ASP.NET para Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

No olvide toocomment Hola estándar InProc sesión estado proveedor sección al archivo Web.config.

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

Una vez realizados estos pasos, la aplicación es toouse configurado hello proveedor de estado de sesión de caché de Redis. Cuando se usa el estado de sesión en la aplicación, se almacena en una instancia de Azure Redis Cache.

> [!IMPORTANT]
> Datos almacenados en caché de Hola deben ser serializables, a diferencia de los datos de Hola que pueden almacenarse en hello predeterminados en la memoria de proveedor de estado de sesión de ASP.NET. Cuando se utiliza el proveedor de estado de sesión para Redis hello, asegúrese de que los tipos de datos de Hola que se almacenen en el estado de sesión sean serializables.
> 
> 

## <a name="aspnet-session-state-options"></a>Opciones de estado de sesión de ASP.NET
* En el proveedor de estado de sesión de memoria - este proveedor almacena estado de sesión de hello en la memoria. ventaja de Hola de usar este proveedor es que resulta sencillo y rápido. Sin embargo, con el proveedor en memoria no se pueden escalar las aplicaciones web, ya que no se distribuye.
* Proveedor de estado de sesión de SQL Server: este proveedor almacena el estado de sesión de hello en Sql Server. Utilice este proveedor si desea que el estado de sesión de toostore hello en el almacenamiento persistente. Puede escalar la aplicación web, pero el uso de SQL Server para la sesión afectará al rendimiento de dicha aplicación.
* Distribuido en memoria Session State Provider como Redis proveedor de estado de memoria caché de sesión - Esto deja de proveedor Hola mejor de ambos mundos. La aplicación web puede tener un proveedor de estado de sesión sencillo, rápido y escalable. Puesto que este Hola de almacenes de estado de sesión en una memoria caché, la aplicación de proveedor tiene tootake en consideración todas Hola características asociadas a comunicarse tooa distribuido en memoria caché, como errores de red transitorios. Para ver los procedimientos recomendados para el uso de la memoria caché, consulte [Instrucciones de almacenamiento en caché](../best-practices-caching.md) en las [Instrucciones de implementación y diseño de aplicaciones en la nube de Azure](https://github.com/mspnp/azure-guidance) de los modelos y prácticas de Microsoft.

Para obtener más información sobre el estado de sesión y otros procedimientos recomendados, consulte [Procedimientos recomendados de desarrollo web (compilación de aplicaciones en la nube reales con Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).

## <a name="next-steps"></a>Pasos siguientes
Extraer del repositorio hello [proveedor de caché de resultados de ASP.NET para caché en Redis de Azure](cache-aspnet-output-cache-provider.md).

