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
## <a name="set-up-your-project"></a><span data-ttu-id="2160a-103">Configurar su proyecto</span><span class="sxs-lookup"><span data-stu-id="2160a-103">Set up your project</span></span>

<span data-ttu-id="2160a-104">Esta sección muestra hello pasos tooinstall y configurar la canalización de autenticación de Hola a través de middleware OWIN en un proyecto de ASP.NET con OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2160a-104">This section shows hello steps tooinstall and configure hello authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="2160a-105">¿Prefiere toodownload proyecto de Visual Studio de este ejemplo en su lugar?</span><span class="sxs-lookup"><span data-stu-id="2160a-105">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="2160a-106">[Descargar un proyecto](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) y omitir toohello [paso de configuración](#create-an-application-express) ejemplo de código de hello tooconfigure antes de ejecutar.</span><span class="sxs-lookup"><span data-stu-id="2160a-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a><span data-ttu-id="2160a-107">Creación del proyecto de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2160a-107">Create your ASP.NET project</span></span>

> 1. <span data-ttu-id="2160a-108">En Visual Studio: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="2160a-108">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
> 2. <span data-ttu-id="2160a-109">En *Visual C#\Web*, seleccione `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="2160a-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
> 3. <span data-ttu-id="2160a-110">Asigne un nombre a la aplicación y haga clic en *Aceptar*.</span><span class="sxs-lookup"><span data-stu-id="2160a-110">Name your application and click *OK*</span></span>
> 4. <span data-ttu-id="2160a-111">Seleccione `Empty` y seleccione Hola casilla tooadd `MVC` referencias</span><span class="sxs-lookup"><span data-stu-id="2160a-111">Select `Empty` and select hello checkbox tooadd `MVC` references</span></span>
<!--end-collapse-->

## <a name="add-authentication-components"></a><span data-ttu-id="2160a-112">Adición de componentes de autenticación</span><span class="sxs-lookup"><span data-stu-id="2160a-112">Add authentication components</span></span>

1. <span data-ttu-id="2160a-113">En Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="2160a-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="2160a-114">Agregar *paquetes de NuGet de middleware OWIN* escribiendo siguiente de hello en la ventana de la consola de administrador de paquetes de saludo:</span><span class="sxs-lookup"><span data-stu-id="2160a-114">Add *OWIN middleware NuGet packages* by typing hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="2160a-115">Acerca de estas bibliotecas</span><span class="sxs-lookup"><span data-stu-id="2160a-115">About these libraries</span></span>

><span data-ttu-id="2160a-116">bibliotecas de Hello anteriores habilitan inicio de sesión único (SSO) con OpenID Connect a través de la autenticación basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="2160a-116">hello libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="2160a-117">Después de que se completa la autenticación y símbolo (token) de Hola que representa el usuario de Hola se envía la aplicación tooyour, middleware de OWIN crea una cookie de sesión.</span><span class="sxs-lookup"><span data-stu-id="2160a-117">After authentication is completed and hello token representing hello user is sent tooyour application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="2160a-118">Explorador de Hola, a continuación, usa esta cookie en solicitudes posteriores para que usuario hello no necesita tooretype su contraseña, y ninguna comprobación adicional es necesario.</span><span class="sxs-lookup"><span data-stu-id="2160a-118">hello browser then uses this cookie on subsequent requests so hello user doesn't need tooretype their password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a><span data-ttu-id="2160a-119">Configurar la canalización de autenticación de Hola</span><span class="sxs-lookup"><span data-stu-id="2160a-119">Configure hello authentication pipeline</span></span>
<span data-ttu-id="2160a-120">Hola pasos son toocreate usa una clase de inicio tooconfigure OpenID Connect autenticación con middleware OWIN.</span><span class="sxs-lookup"><span data-stu-id="2160a-120">hello steps below are used toocreate an OWIN middleware Startup Class tooconfigure OpenID Connect authentication.</span></span> <span data-ttu-id="2160a-121">Esta clase se ejecutará automáticamente cuando se inicie el proceso de IIS.</span><span class="sxs-lookup"><span data-stu-id="2160a-121">This class will be executed automatically when your IIS process starts.</span></span>

> <span data-ttu-id="2160a-122">Si el proyecto no tiene un `Startup.cs` archivo en la carpeta raíz de hello:</span><span class="sxs-lookup"><span data-stu-id="2160a-122">If your project doesn't have a `Startup.cs` file in hello root folder:</span></span><br/>
> 1. <span data-ttu-id="2160a-123">Haga clic con el botón secundario en la carpeta raíz del proyecto de hello: >`Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="2160a-123">Right click on hello project's root folder: >  `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="2160a-124">Asígnele el nombre `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="2160a-124">Name it `Startup.cs`</span></span>

> <span data-ttu-id="2160a-125">Asegúrese de que la clase hello seleccionada es una clase de inicio de OWIN y no una estándar clase de C#.</span><span class="sxs-lookup"><span data-stu-id="2160a-125">Make sure hello class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="2160a-126">Confirmarlo, compruebe si ve `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` por encima del espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="2160a-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above hello namespace.</span></span>


1. <span data-ttu-id="2160a-127">Agregar *OWIN* y *Microsoft.IdentityModel* hace referencia a demasiado`Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="2160a-127">Add *OWIN* and *Microsoft.IdentityModel* references too`Startup.cs`:</span></span>

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
<span data-ttu-id="2160a-128">Reemplace la clase de inicio con código de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="2160a-128">Replace Startup class with hello code below:</span></span>
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
> ### <a name="more-information"></a><span data-ttu-id="2160a-129">Más información</span><span class="sxs-lookup"><span data-stu-id="2160a-129">More Information</span></span>

> <span data-ttu-id="2160a-130">Hola parámetros que se proporciona en *OpenIDConnectAuthenticationOptions* actuar como coordenadas de hello toocommunicate de aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2160a-130">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello application toocommunicate with Azure AD.</span></span> <span data-ttu-id="2160a-131">Porque Hola OpenID Connect middleware utiliza cookies en segundo plano de hello, también deberá tooset la autenticación de la cookie como código de hello anterior muestra.</span><span class="sxs-lookup"><span data-stu-id="2160a-131">Because hello OpenID Connect middleware uses cookies in hello background, you also need tooset up cookie authentication as hello code above shows.</span></span> <span data-ttu-id="2160a-132">Hola *ValidateIssuer* valor indica OpenIdConnect toonot restringir acceso específica de tooone la organización.</span><span class="sxs-lookup"><span data-stu-id="2160a-132">hello *ValidateIssuer* value tells OpenIdConnect toonot restrict access tooone specific organization.</span></span>
<!--end-collapse-->

