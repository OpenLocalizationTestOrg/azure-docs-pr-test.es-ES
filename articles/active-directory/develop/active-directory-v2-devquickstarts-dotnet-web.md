---
title: "aaaAzure AD v2.0 .NET web de inicio de sesión de introducción | Documentos de Microsoft"
description: "¿Cómo toobuild una aplicación Web de MVC de .NET firma los usuarios con ambos Account personal de Microsoft y cuentas profesionales o educativas."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a>Agregar la aplicación web de inicio de sesión tooan .NET MVC
Con el punto de conexión de hello v2.0, puede agregar rápidamente autenticación tooyour las aplicaciones web con la compatibilidad para ambas cuentas de Microsoft personales y cuentas profesionales o educativas.  En las aplicaciones web ASP.NET puede realizar esto con el OWIN middleware de Microsoft incluido en .NET Framework 4.5.

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.  toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
>
>

 Aquí, crearemos una aplicación web que usa el usuario OWIN toosign hello en pantalla de cierta información sobre el usuario de Hola y usuario fuera de la aplicación hello de Hola de inicio de sesión.

## <a name="download"></a>Descargar
código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).  toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o esqueleto de Hola de clon:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

final de Hola de este tutorial también se incluye aplicación Hello completado.

## <a name="register-an-app"></a>Registrar una aplicación
Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).  Asegúrese de que:

* Copia hacia abajo hello **Id. de aplicación** asignado tooyour aplicación, ya que lo necesitará pronto.
* Agregar hello **Web** plataforma para la aplicación.
* Escriba Hola correcto **URI de redireccionamiento**. uri de redireccionamiento Hello indica tooAzure AD donde se deben dirigir las respuestas de autenticación: Hola predeterminado para este tutorial es `https://localhost:44326/`.

## <a name="install--configure-owin-authentication"></a>Instalación y configuración de la autenticación OWIN
En este caso, vamos a configurar hello OWIN middleware toouse Hola OpenID Connect protocolo de autenticación.  OWIN ser tooissue usa las solicitudes de inicio de sesión y cierre de sesión, administrar la sesión del usuario de Hola y obtener información acerca del usuario de hello, entre otras cosas.

1. toobegin, abra hello `web.config` un archivo en la raíz de hello del proyecto de Hola y escriba los valores de configuración de la aplicación Hola `<appSettings>` sección.

  * Hola `ida:ClientId` es hello **Id. de aplicación** asignado tooyour aplicación de portal de registro de hello.
  * Hola `ida:RedirectUri` es hello **Uri de redireccionamiento** que especificó en el portal de Hola.

2. A continuación, agregue hello OWIN middleware NuGet paquetes toohello proyecto mediante la consola de administrador de paquetes de saludo.

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. Agregar un proyecto de toohello "Clase de inicio de OWIN" llamado `Startup.cs` derecho, haga clic en proyecto de hello--> **agregar** --> **nuevo elemento** --> busque "OWIN".  middleware de OWIN Hola invocará hello `Configuration(...)` método cuando se inicia la aplicación.
4. Cambie la declaración de clase de hello demasiado`public partial class Startup` -hemos implementado ya parte de esta clase para usted en otro archivo.  Hola `Configuration(...)` método, realizar un tooset de tooConfigureAuth(...) de llamada de la autenticación de la aplicación web  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. Archivo abierto hello `App_Start\Startup.Auth.cs` e implementar hello `ConfigureAuth(...)` método.  Hola parámetros que se proporciona en `OpenIdConnectAuthenticationOptions` servirá como coordenadas para su toocommunicate de aplicación con Azure AD.  También necesitará tooset la Cookie de autenticación: Hola OpenID Connect middleware utiliza cookies debajo Hola portadas.

        ```C#
        public void ConfigureAuth(IAppBuilder app)
                     {
                             app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
        
                             app.UseCookieAuthentication(new CookieAuthenticationOptions());
        
                             app.UseOpenIdConnectAuthentication(
                                     new OpenIdConnectAuthenticationOptions
                                     {
                                             // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                                             // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                                             // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.
        
                                             ClientId = clientId,
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a>Envío de solicitudes de autenticación
La aplicación ya está configurada correctamente toocommunicate con punto de conexión de hello v2.0 mediante Protocolo de autenticación de OpenID Connect de Hola.  OWIN se ocupa de todos hello desagradable detalles de transmitir mensajes de autenticación, validar los tokens de Azure AD y mantener la sesión de usuario.  Lo único que queda es toogive a los usuarios una manera toosign en y cierre de sesión.

- Puede utilizar etiquetas de autorizar en su toorequire de controladores que el usuario inicia sesión antes de acceder a una página determinada.  Abra `Controllers\HomeController.cs`y agregue hello `[Authorize]` etiqueta toohello sobre el controlador.
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- También puede usar solicitudes de autenticación OWIN toodirectly problema desde dentro del código.  Abra `Controllers\AccountController.cs`.  En hello SignIn() y acciones de SignOut(), emitir el desafío OpenID Connect y solicitudes de cierre de sesión, respectivamente.

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- Ahora, abra `Views\Shared\_LoginPartial.cshtml`.  Esto es donde podrá mostrar vínculos de inicio de sesión y cierre de sesión de la aplicación de usuario de Hola y el nombre del usuario de hello en una vista de impresión.

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
                    </li>
                    <li>
                        @Html.ActionLink("Sign out", "SignOut", "Account")
                    </li>
                </ul>
            </text>
        }
        else
        {
            <ul class="nav navbar-nav navbar-right">
                <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
            </ul>
        }
        ```

## <a name="display-user-information"></a>Mostrar información de usuario
Al autenticar a los usuarios con OpenID Connect, el punto de conexión de hello v2.0 devuelve una aplicación de toohello id_token que contenga notificaciones o aserciones de usuario de Hola.  Puede usar estas notificaciones toopersonalize su aplicación:

- Abra hello `Controllers\HomeController.cs` archivo.  Puede tener acceso a solicitudes del usuario de hello en los controladores a través de hello `ClaimsPrincipal.Current` objeto de entidad de seguridad.

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a>Ejecute
Por último, compile y ejecute su aplicación.   Inicie sesión con una Account Microsoft personal o una cuenta profesional o educativa y observe cómo se refleja la identidad del usuario de hello en la barra de navegación superior de Hola.  Ahora dispone de una aplicación web protegida mediante protocolos estándar del sector que pueden autenticar a los usuarios tanto con sus cuentas personales como con sus cuentas profesionales/educativas.

Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como .zip aquí](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), o se puede clonar desde GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a>Pasos siguientes
Ahora puede pasar a temas más avanzados.  Puede que desee tootry:

[Proteger una API Web con el punto de conexión de Hola Hola v2.0 >>](active-directory-devquickstarts-webapi-dotnet.md)

Para obtener recursos adicionales, consulte:

* [Guía del desarrollador de Hello v2.0 >>](active-directory-appmodel-v2-overview.md)
* [Etiqueta "azure-active-directory" de StackOverflow &gt;&gt;](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Obtención de actualizaciones de seguridad para nuestros productos
Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.
