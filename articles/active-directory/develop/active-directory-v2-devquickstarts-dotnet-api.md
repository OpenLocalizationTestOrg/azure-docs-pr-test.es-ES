---
title: "uso de inicio de sesión tooa API web .NET MVC aaaAdd Hola extremo v2.0 de Azure AD | Documentos de Microsoft"
description: "¿Cómo toobuild una Api Web MVC de .NET que acepta los tokens de ambos Account personal de Microsoft y cuentas profesionales o educativas."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a>Protección de una API web MVC
Con el punto de conexión de Azure Active Directory Hola v2.0, puede proteger una API de Web mediante [OAuth 2.0](active-directory-v2-protocols.md) tokens de acceso, lo que permite a los usuarios con ambos cuenta personal de Microsoft y cuentas profesionales o educativas toosecurely tener acceso a la API Web.

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.  toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
>
>

En las API web ASP.NET puede realizar esto con el OWIN middleware de Microsoft incluido en .NET Framework 4.5.  Aquí usamos la OWIN toobuild una API Web MVC de "tooDo lista" que permite a los clientes las tareas toocreate y lectura de la lista de tareas pendientes de un usuario.  API de web Hola validará que contienen un token de acceso válido y rechazan las solicitudes que no pasan la validación en una ruta protegida las solicitudes entrantes.  Este ejemplo se creó con Visual Studio 2015.

## <a name="download"></a>Descargar
código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).  toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o esqueleto de Hola de clon:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

aplicación esqueleto de Hello incluye todo el código de hello reutilizable para una API sencilla, pero le falta todas partes relacionadas con la identidad de Hola. Si no desea toofollow a lo largo de, en su lugar, se pueden clonar o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>Registrar una aplicación
Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).  Asegúrese de que:

* Copia hacia abajo hello **Id. de aplicación** asignado tooyour aplicación, ya que lo necesitará pronto.

La solución de Visual Studio también contiene "TodoListClient", que es una sencilla aplicación WPF.  Hola TodoListClient es usado toodemonstrate cómo un usuario inicia sesión y cómo puede emitir un cliente solicita tooyour API Web.  En este caso, se representan hello TodoListClient y hello TodoListService por hello misma aplicación.  tooconfigure Hola TodoListClient, también debe:

* Agregar hello **Mobile** plataforma para la aplicación.

## <a name="install-owin"></a>Instalar OWIN
Ahora que ha registrado una aplicación, necesita tooset seguridad su toocommunicate de aplicación con punto de conexión de hello v2.0 en orden toovalidate las solicitudes entrantes y símbolos (tokens).

* toobegin, abra la solución de Hola y agregue hello OWIN middleware NuGet paquetes toohello TodoListService proyecto mediante la consola de administrador de paquetes de saludo.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>Configurar la autenticación de OAuth
* Agregue un proyecto TodoListService de inicio de OWIN clases toohello denominado `Startup.cs`.  Haga clic en proyecto de hello--> **agregar** --> **nuevo elemento** --> busque "OWIN".  middleware de OWIN Hola invocará hello `Configuration(…)` método cuando se inicia la aplicación.
* Cambie la declaración de clase de hello demasiado`public partial class Startup` -hemos implementado ya parte de esta clase para usted en otro archivo.  Hola `Configuration(…)` método, realizar un tooset de tooConfgureAuth(...) de llamada de la autenticación de la aplicación web.

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* Archivo abierto hello `App_Start\Startup.Auth.cs` e implementar hello `ConfigureAuth(…)` método, que configurará tooaccept tokens de hello Web API desde el punto de conexión de hello v2.0.

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* Ahora puede usar `[Authorize]` atributos tooprotect los controladores y acciones con la autenticación de portador de OAuth 2.0.  Decorar hello `Controllers\TodoListController.cs` clase con una etiqueta de autorizar.  Esto forzará Hola usuario toosign en antes de acceder a esa página.

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* Cuando un llamador autorizado correctamente invoca uno de hello `TodoListController` API, acción de Hola podría necesita acceder a tooinformation sobre llamador Hola.  OWIN proporciona acceso toohello notificaciones dentro de token de portador de hello mediante hello `ClaimsPrincpal` objeto.  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* Por último, abra hello `web.config` un archivo en la raíz de Hola de proyecto TodoListService de Hola y escriba los valores de configuración en hello `<appSettings>` sección.
  * Su `ida:Audience` es hello **Id. de aplicación** de aplicación hello especificado en el portal de Hola.

## <a name="configure-hello-client-app"></a>Configurar la aplicación de cliente hello
Para poder ver Hola servicio de lista de tareas en acción, deberá tooconfigure Hola cliente lista de tareas para que pueda obtener tokens de punto de conexión de hello v2.0 y hacer llamadas toohello servicio.

* En hello TodoListClient proyecto, abra `App.config` y escriba los valores de configuración en hello `<appSettings>` sección.
  * Su `ida:ClientId` identificador de la aplicación copian desde el portal de Hola.

Por último, limpie, compile y ejecute cada proyecto.  Ahora dispone de una API web MVC de .NET que acepta los token de las cuentas de Microsoft y de las cuentas profesionales o educativas.  Inicie sesión en hello TodoListClient y llamar a la lista de tareas pendientes de web api tooadd tareas toohello de sus usuarios.

Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como .zip aquí](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), o se puede clonar desde GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>Pasos siguientes
Ahora puede pasar a otros temas adicionales.  Puede que desee tootry:

[Llamada a una API web desde una aplicación web &gt;&gt;](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

Para obtener recursos adicionales, consulte:

* [Guía del desarrollador de Hello v2.0 >>](active-directory-appmodel-v2-overview.md)
* [Etiqueta "azure-active-directory" de StackOverflow &gt;&gt;](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Obtención de actualizaciones de seguridad para nuestros productos
Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.
