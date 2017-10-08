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
# <a name="add-sign-in-tooan-net-mvc-web-app"></a><span data-ttu-id="95175-103">Agregar la aplicación web de inicio de sesión tooan .NET MVC</span><span class="sxs-lookup"><span data-stu-id="95175-103">Add sign-in tooan .NET MVC web app</span></span>
<span data-ttu-id="95175-104">Con el punto de conexión de hello v2.0, puede agregar rápidamente autenticación tooyour las aplicaciones web con la compatibilidad para ambas cuentas de Microsoft personales y cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="95175-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="95175-105">En las aplicaciones web ASP.NET puede realizar esto con el OWIN middleware de Microsoft incluido en .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="95175-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="95175-106">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="95175-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="95175-107">toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="95175-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="95175-108">Aquí, crearemos una aplicación web que usa el usuario OWIN toosign hello en pantalla de cierta información sobre el usuario de Hola y usuario fuera de la aplicación hello de Hola de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="95175-108">Here we'll build an web app that uses OWIN toosign hello user in, display some information about hello user, and sign hello user out of hello app.</span></span>

## <a name="download"></a><span data-ttu-id="95175-109">Descargar</span><span class="sxs-lookup"><span data-stu-id="95175-109">Download</span></span>
<span data-ttu-id="95175-110">código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="95175-110">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="95175-111">toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o esqueleto de Hola de clon:</span><span class="sxs-lookup"><span data-stu-id="95175-111">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="95175-112">final de Hola de este tutorial también se incluye aplicación Hello completado.</span><span class="sxs-lookup"><span data-stu-id="95175-112">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="95175-113">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="95175-113">Register an app</span></span>
<span data-ttu-id="95175-114">Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="95175-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="95175-115">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="95175-115">Make sure to:</span></span>

* <span data-ttu-id="95175-116">Copia hacia abajo hello **Id. de aplicación** asignado tooyour aplicación, ya que lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="95175-116">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="95175-117">Agregar hello **Web** plataforma para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95175-117">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="95175-118">Escriba Hola correcto **URI de redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="95175-118">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="95175-119">uri de redireccionamiento Hello indica tooAzure AD donde se deben dirigir las respuestas de autenticación: Hola predeterminado para este tutorial es `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="95175-119">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="95175-120">Instalación y configuración de la autenticación OWIN</span><span class="sxs-lookup"><span data-stu-id="95175-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="95175-121">En este caso, vamos a configurar hello OWIN middleware toouse Hola OpenID Connect protocolo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="95175-121">Here, we'll configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="95175-122">OWIN ser tooissue usa las solicitudes de inicio de sesión y cierre de sesión, administrar la sesión del usuario de Hola y obtener información acerca del usuario de hello, entre otras cosas.</span><span class="sxs-lookup"><span data-stu-id="95175-122">OWIN will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

1. <span data-ttu-id="95175-123">toobegin, abra hello `web.config` un archivo en la raíz de hello del proyecto de Hola y escriba los valores de configuración de la aplicación Hola `<appSettings>` sección.</span><span class="sxs-lookup"><span data-stu-id="95175-123">toobegin, open hello `web.config` file in hello root of hello project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="95175-124">Hola `ida:ClientId` es hello **Id. de aplicación** asignado tooyour aplicación de portal de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="95175-124">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="95175-125">Hola `ida:RedirectUri` es hello **Uri de redireccionamiento** que especificó en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="95175-125">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>

2. <span data-ttu-id="95175-126">A continuación, agregue hello OWIN middleware NuGet paquetes toohello proyecto mediante la consola de administrador de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="95175-126">Next, add hello OWIN middleware NuGet packages toohello project using hello Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="95175-127">Agregar un proyecto de toohello "Clase de inicio de OWIN" llamado `Startup.cs` derecho, haga clic en proyecto de hello--> **agregar** --> **nuevo elemento** --> busque "OWIN".</span><span class="sxs-lookup"><span data-stu-id="95175-127">Add an "OWIN Startup Class" toohello project called `Startup.cs`  Right click on hello project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="95175-128">middleware de OWIN Hola invocará hello `Configuration(...)` método cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95175-128">hello OWIN middleware will invoke hello `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="95175-129">Cambie la declaración de clase de hello demasiado`public partial class Startup` -hemos implementado ya parte de esta clase para usted en otro archivo.</span><span class="sxs-lookup"><span data-stu-id="95175-129">Change hello class declaration too`public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="95175-130">Hola `Configuration(...)` método, realizar un tooset de tooConfigureAuth(...) de llamada de la autenticación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="95175-130">In hello `Configuration(...)` method, make a call tooConfigureAuth(...) tooset up authentication for your web app</span></span>  

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

5. <span data-ttu-id="95175-131">Archivo abierto hello `App_Start\Startup.Auth.cs` e implementar hello `ConfigureAuth(...)` método.</span><span class="sxs-lookup"><span data-stu-id="95175-131">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="95175-132">Hola parámetros que se proporciona en `OpenIdConnectAuthenticationOptions` servirá como coordenadas para su toocommunicate de aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95175-132">hello parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>  <span data-ttu-id="95175-133">También necesitará tooset la Cookie de autenticación: Hola OpenID Connect middleware utiliza cookies debajo Hola portadas.</span><span class="sxs-lookup"><span data-stu-id="95175-133">You'll also need tooset up Cookie Authentication - hello OpenID Connect middleware uses cookies underneath hello covers.</span></span>

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

## <a name="send-authentication-requests"></a><span data-ttu-id="95175-134">Envío de solicitudes de autenticación</span><span class="sxs-lookup"><span data-stu-id="95175-134">Send authentication requests</span></span>
<span data-ttu-id="95175-135">La aplicación ya está configurada correctamente toocommunicate con punto de conexión de hello v2.0 mediante Protocolo de autenticación de OpenID Connect de Hola.</span><span class="sxs-lookup"><span data-stu-id="95175-135">Your app is now properly configured toocommunicate with hello v2.0 endpoint using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="95175-136">OWIN se ocupa de todos hello desagradable detalles de transmitir mensajes de autenticación, validar los tokens de Azure AD y mantener la sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="95175-136">OWIN has taken care of all of hello ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="95175-137">Lo único que queda es toogive a los usuarios una manera toosign en y cierre de sesión.</span><span class="sxs-lookup"><span data-stu-id="95175-137">All that remains is toogive your users a way toosign in and sign out.</span></span>

- <span data-ttu-id="95175-138">Puede utilizar etiquetas de autorizar en su toorequire de controladores que el usuario inicia sesión antes de acceder a una página determinada.</span><span class="sxs-lookup"><span data-stu-id="95175-138">You can use authorize tags in your controllers toorequire that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="95175-139">Abra `Controllers\HomeController.cs`y agregue hello `[Authorize]` etiqueta toohello sobre el controlador.</span><span class="sxs-lookup"><span data-stu-id="95175-139">Open `Controllers\HomeController.cs`, and add hello `[Authorize]` tag toohello About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="95175-140">También puede usar solicitudes de autenticación OWIN toodirectly problema desde dentro del código.</span><span class="sxs-lookup"><span data-stu-id="95175-140">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span>  <span data-ttu-id="95175-141">Abra `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="95175-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="95175-142">En hello SignIn() y acciones de SignOut(), emitir el desafío OpenID Connect y solicitudes de cierre de sesión, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="95175-142">In hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

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

- <span data-ttu-id="95175-143">Ahora, abra `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="95175-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="95175-144">Esto es donde podrá mostrar vínculos de inicio de sesión y cierre de sesión de la aplicación de usuario de Hola y el nombre del usuario de hello en una vista de impresión.</span><span class="sxs-lookup"><span data-stu-id="95175-144">This is where you'll show hello user your app's sign-in and sign-out links, and print out hello user's name in a view.</span></span>

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

## <a name="display-user-information"></a><span data-ttu-id="95175-145">Mostrar información de usuario</span><span class="sxs-lookup"><span data-stu-id="95175-145">Display user information</span></span>
<span data-ttu-id="95175-146">Al autenticar a los usuarios con OpenID Connect, el punto de conexión de hello v2.0 devuelve una aplicación de toohello id_token que contenga notificaciones o aserciones de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="95175-146">When authenticating users with OpenID Connect, hello v2.0 endpoint returns an id_token toohello app that contains claims, or assertions about hello user.</span></span>  <span data-ttu-id="95175-147">Puede usar estas notificaciones toopersonalize su aplicación:</span><span class="sxs-lookup"><span data-stu-id="95175-147">You can use these claims toopersonalize your app:</span></span>

- <span data-ttu-id="95175-148">Abra hello `Controllers\HomeController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="95175-148">Open hello `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="95175-149">Puede tener acceso a solicitudes del usuario de hello en los controladores a través de hello `ClaimsPrincipal.Current` objeto de entidad de seguridad.</span><span class="sxs-lookup"><span data-stu-id="95175-149">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

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

## <a name="run"></a><span data-ttu-id="95175-150">Ejecute</span><span class="sxs-lookup"><span data-stu-id="95175-150">Run</span></span>
<span data-ttu-id="95175-151">Por último, compile y ejecute su aplicación.</span><span class="sxs-lookup"><span data-stu-id="95175-151">Finally, build and run your app!</span></span>   <span data-ttu-id="95175-152">Inicie sesión con una Account Microsoft personal o una cuenta profesional o educativa y observe cómo se refleja la identidad del usuario de hello en la barra de navegación superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="95175-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="95175-153">Ahora dispone de una aplicación web protegida mediante protocolos estándar del sector que pueden autenticar a los usuarios tanto con sus cuentas personales como con sus cuentas profesionales/educativas.</span><span class="sxs-lookup"><span data-stu-id="95175-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="95175-154">Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como .zip aquí](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), o se puede clonar desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="95175-154">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="95175-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95175-155">Next steps</span></span>
<span data-ttu-id="95175-156">Ahora puede pasar a temas más avanzados.</span><span class="sxs-lookup"><span data-stu-id="95175-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="95175-157">Puede que desee tootry:</span><span class="sxs-lookup"><span data-stu-id="95175-157">You may want tootry:</span></span>

[<span data-ttu-id="95175-158">Proteger una API Web con el punto de conexión de Hola Hola v2.0 >></span><span class="sxs-lookup"><span data-stu-id="95175-158">Secure a Web API with hello hello v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="95175-159">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="95175-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="95175-160">Guía del desarrollador de Hello v2.0 >></span><span class="sxs-lookup"><span data-stu-id="95175-160">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="95175-161">Etiqueta "azure-active-directory" de StackOverflow &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="95175-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="95175-162">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="95175-162">Get security updates for our products</span></span>
<span data-ttu-id="95175-163">Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.</span><span class="sxs-lookup"><span data-stu-id="95175-163">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
