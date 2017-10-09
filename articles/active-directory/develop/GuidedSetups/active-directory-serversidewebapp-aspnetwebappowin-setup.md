---
title: "aaaAzure AD v2 ASP.NET Web Server introducción - el programa de instalación | Documentos de Microsoft"
description: "Implementación de inicio de sesión de Microsoft en una solución ASP.NET con una aplicación basada en un explorador web tradicional mediante el estándar OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configurar su proyecto

Esta sección muestra hello pasos tooinstall y configurar la canalización de autenticación de Hola a través de middleware OWIN en un proyecto de ASP.NET con OpenID Connect. 

> ¿Prefiere toodownload proyecto de Visual Studio de este ejemplo en su lugar? [Descargar un proyecto](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) y omitir toohello [paso de configuración](#create-an-application-express) ejemplo de código de hello tooconfigure antes de ejecutar.

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>Creación del proyecto de ASP.NET

> 1. En Visual Studio: `File` > `New` > `Project`<br/>
> 2. En *Visual C#\Web*, seleccione `ASP.NET Web Application (.NET Framework)`.
> 3. Asigne un nombre a la aplicación y haga clic en *Aceptar*.
> 4. Seleccione `Empty` y seleccione Hola casilla tooadd `MVC` referencias
<!--end-collapse-->

## <a name="add-authentication-components"></a>Adición de componentes de autenticación

1. En Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Agregar *paquetes de NuGet de middleware OWIN* escribiendo siguiente de hello en la ventana de la consola de administrador de paquetes de saludo:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>Acerca de estas bibliotecas

>bibliotecas de Hello anteriores habilitan inicio de sesión único (SSO) con OpenID Connect a través de la autenticación basada en cookies. Después de que se completa la autenticación y símbolo (token) de Hola que representa el usuario de Hola se envía la aplicación tooyour, middleware de OWIN crea una cookie de sesión. Explorador de Hola, a continuación, usa esta cookie en solicitudes posteriores para que usuario hello no necesita tooretype su contraseña, y ninguna comprobación adicional es necesario.
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a>Configurar la canalización de autenticación de Hola
Hola pasos son toocreate usa una clase de inicio tooconfigure OpenID Connect autenticación con middleware OWIN. Esta clase se ejecutará automáticamente cuando se inicie el proceso de IIS.

> Si el proyecto no tiene un `Startup.cs` archivo en la carpeta raíz de hello:<br/>
> 1. Haga clic con el botón secundario en la carpeta raíz del proyecto de hello: >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Asígnele el nombre `Startup.cs`.

> Asegúrese de que la clase hello seleccionada es una clase de inicio de OWIN y no una estándar clase de C#. Confirmarlo, compruebe si ve `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` por encima del espacio de nombres de Hola.


1. Agregar *OWIN* y *Microsoft.IdentityModel* hace referencia a demasiado`Startup.cs`:

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Reemplace la clase de inicio con código de hello siguiente:
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a>Más información

> Hola parámetros que se proporciona en *OpenIDConnectAuthenticationOptions* actuar como coordenadas de hello toocommunicate de aplicación con Azure AD. Porque Hola OpenID Connect middleware utiliza cookies en segundo plano de hello, también deberá tooset la autenticación de la cookie como código de hello anterior muestra. Hola *ValidateIssuer* valor indica OpenIdConnect toonot restringir acceso específica de tooone la organización.
<!--end-collapse-->

