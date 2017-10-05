---
title: "Introducción al inicio de sesión de la aplicación web de .NET v2.0 de Azure AD | Microsoft Docs"
description: "Cómo crear una aplicación web de .NET MVC con la que los usuarios pueden iniciar sesión utilizando tanto la cuenta personal de Microsoft como sus cuentas profesionales o educativas."
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
ms.openlocfilehash: ba5bdf7daba6086b70aec54ebe25d4445fa708c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-net-mvc-web-app"></a><span data-ttu-id="f30dc-103">Agregar inicio de sesión a una aplicación web .NET MVC</span><span class="sxs-lookup"><span data-stu-id="f30dc-103">Add sign-in to an .NET MVC web app</span></span>
<span data-ttu-id="f30dc-104">Con el punto de conexión v2.0 puede agregar rápidamente la autenticación a sus aplicaciones web compatibles tanto con las cuentas personales de Microsoft como con las cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="f30dc-104">With the v2.0 endpoint, you can quickly add authentication to your web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="f30dc-105">En las aplicaciones web ASP.NET puede realizar esto con el OWIN middleware de Microsoft incluido en .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f30dc-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="f30dc-106">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión v2.0.</span><span class="sxs-lookup"><span data-stu-id="f30dc-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="f30dc-107">Para determinar si debe utilizar la versión 2.0 del punto de conexión, obtenga información sobre las [limitaciones de esta versión](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="f30dc-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="f30dc-108">Aquí vamos a compilar una aplicación web que usa OWIN para iniciar la sesión del usuario, mostrar información sobre el usuario y cerrar la sesión del usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f30dc-108">Here we'll build an web app that uses OWIN to sign the user in, display some information about the user, and sign the user out of the app.</span></span>

## <a name="download"></a><span data-ttu-id="f30dc-109">Descargar</span><span class="sxs-lookup"><span data-stu-id="f30dc-109">Download</span></span>
<span data-ttu-id="f30dc-110">El código de este tutorial se conserva [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="f30dc-110">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="f30dc-111">Para continuar, puede [descargar el esqueleto de la aplicación como un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o clonar el esqueleto:</span><span class="sxs-lookup"><span data-stu-id="f30dc-111">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="f30dc-112">La aplicación completa se ofrece también al final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f30dc-112">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="f30dc-113">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="f30dc-113">Register an app</span></span>
<span data-ttu-id="f30dc-114">Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f30dc-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="f30dc-115">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="f30dc-115">Make sure to:</span></span>

* <span data-ttu-id="f30dc-116">Anotar el **Id. de aplicación** asignado a su aplicación; lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="f30dc-116">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="f30dc-117">Agregar la plataforma **web** para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="f30dc-117">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="f30dc-118">Escribir el **URI de redireccionamiento**correcto.</span><span class="sxs-lookup"><span data-stu-id="f30dc-118">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="f30dc-119">El uri de redirección indica a Azure AD a dónde se deben dirigir las respuestas de autenticación: el valor predeterminado para este tutorial es `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="f30dc-119">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="f30dc-120">Instalación y configuración de la autenticación OWIN</span><span class="sxs-lookup"><span data-stu-id="f30dc-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="f30dc-121">Aquí configuraremos el middleware OWIN para usar el protocolo de autenticación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f30dc-121">Here, we'll configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="f30dc-122">OWIN se usará para emitir solicitudes de inicio y cierre de sesión, administrar la sesión del usuario y obtener información sobre el usuario, entre otras cosas.</span><span class="sxs-lookup"><span data-stu-id="f30dc-122">OWIN will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

1. <span data-ttu-id="f30dc-123">Para comenzar, abra el archivo `web.config` en la raíz del proyecto y escriba los valores de configuración de la aplicación en la sección `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="f30dc-123">To begin, open the `web.config` file in the root of the project, and enter your app's configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="f30dc-124">El `ida:ClientId` es el **identificador de aplicación** asignado a su aplicación en el portal de registro.</span><span class="sxs-lookup"><span data-stu-id="f30dc-124">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="f30dc-125">El `ida:RedirectUri` es el **identificador URI de redireccionamiento** que escribió en el portal.</span><span class="sxs-lookup"><span data-stu-id="f30dc-125">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>

2. <span data-ttu-id="f30dc-126">A continuación, agregue los paquetes NuGet de middleware al proyecto usando la Consola de Administración de paquetes.</span><span class="sxs-lookup"><span data-stu-id="f30dc-126">Next, add the OWIN middleware NuGet packages to the project using the Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="f30dc-127">Agregue una Clase de inicio OWIN al proyecto denominado `Startup.cs`. Haga clic con el botón derecho en el proyecto **Agregar** --> **Nuevo elemento** --> Busque "OWIN".</span><span class="sxs-lookup"><span data-stu-id="f30dc-127">Add an "OWIN Startup Class" to the project called `Startup.cs`  Right click on the project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="f30dc-128">El middleware OWIN invocará el método `Configuration(...)` al iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f30dc-128">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="f30dc-129">Cambie la declaración de clase a `public partial class Startup` (ya hemos implementado parte de esta clase para usted en otro archivo).</span><span class="sxs-lookup"><span data-stu-id="f30dc-129">Change the class declaration to `public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="f30dc-130">En el método `Configuration(...)` , realice una llamada a ConfigureAuth(...) para configurar la autenticación para su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f30dc-130">In the `Configuration(...)` method, make a call to ConfigureAuth(...) to set up authentication for your web app</span></span>  

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

5. <span data-ttu-id="f30dc-131">Abra el archivo `App_Start\Startup.Auth.cs` e implemente el método `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="f30dc-131">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="f30dc-132">Los parámetros que proporciona en `OpenIdConnectAuthenticationOptions` servirán como coordenadas para que su aplicación se comunique con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f30dc-132">The parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>  <span data-ttu-id="f30dc-133">También tendrá que configurar la autenticación con cookies (el middleware OpenID Connect usa cookies debajo de las portadas).</span><span class="sxs-lookup"><span data-stu-id="f30dc-133">You'll also need to set up Cookie Authentication - the OpenID Connect middleware uses cookies underneath the covers.</span></span>

        ```C#
        public void ConfigureAuth(IAppBuilder app)
                     {
                             app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
        
                             app.UseCookieAuthentication(new CookieAuthenticationOptions());
        
                             app.UseOpenIdConnectAuthentication(
                                     new OpenIdConnectAuthenticationOptions
                                     {
                                             // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                                             // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                                             // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.
        
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

## <a name="send-authentication-requests"></a><span data-ttu-id="f30dc-134">Envío de solicitudes de autenticación</span><span class="sxs-lookup"><span data-stu-id="f30dc-134">Send authentication requests</span></span>
<span data-ttu-id="f30dc-135">Ahora la aplicación está correctamente configurada para comunicarse con el extremo v2.0 mediante el protocolo de autenticación de OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f30dc-135">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="f30dc-136">OWIN se ha ocupado de todos los detalles feos de la creación de mensajes de autenticación, validación de tokens de Azure AD y mantenimiento de la sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="f30dc-136">OWIN has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="f30dc-137">Lo único que queda consiste en ofrecer a sus usuarios una forma de iniciar y cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="f30dc-137">All that remains is to give your users a way to sign in and sign out.</span></span>

- <span data-ttu-id="f30dc-138">Puede usar etiquetas Autorizar en sus controladores para solicitar que el usuario inicie sesión antes de tener acceso a una página determinada.</span><span class="sxs-lookup"><span data-stu-id="f30dc-138">You can use authorize tags in your controllers to require that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="f30dc-139">Abra `Controllers\HomeController.cs` y agregue la etiqueta `[Authorize]` al controlador Acerca de.</span><span class="sxs-lookup"><span data-stu-id="f30dc-139">Open `Controllers\HomeController.cs`, and add the `[Authorize]` tag to the About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="f30dc-140">También puede usar OWIN para emitir directamente solicitudes de autenticación desde dentro de su código.</span><span class="sxs-lookup"><span data-stu-id="f30dc-140">You can also use OWIN to directly issue authentication requests from within your code.</span></span>  <span data-ttu-id="f30dc-141">Abra `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="f30dc-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="f30dc-142">En las acciones SignIn() y SignOut(), emita un concurso de OpenID Connect y solicitudes de cierre de sesión, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="f30dc-142">In the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with the v2.0 endpoint is not yet supported.  Here, we just end the session with the web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="f30dc-143">Ahora, abra `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f30dc-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="f30dc-144">Aquí mostrará al usuario los vínculos de inicio y cierre de sesión de su aplicación e imprimirá el nombre del usuario en una vista.</span><span class="sxs-lookup"><span data-stu-id="f30dc-144">This is where you'll show the user your app's sign-in and sign-out links, and print out the user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves.*@
        
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

## <a name="display-user-information"></a><span data-ttu-id="f30dc-145">Mostrar información de usuario</span><span class="sxs-lookup"><span data-stu-id="f30dc-145">Display user information</span></span>
<span data-ttu-id="f30dc-146">Al autenticar usuarios con OpenID Connect, el punto de conexión v2.0 devuelve un id_token a la aplicación que contiene notificaciones o aserciones sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="f30dc-146">When authenticating users with OpenID Connect, the v2.0 endpoint returns an id_token to the app that contains claims, or assertions about the user.</span></span>  <span data-ttu-id="f30dc-147">Puede usar estas notificaciones para personalizar su aplicación:</span><span class="sxs-lookup"><span data-stu-id="f30dc-147">You can use these claims to personalize your app:</span></span>

- <span data-ttu-id="f30dc-148">Abra el archivo `Controllers\HomeController.cs` .</span><span class="sxs-lookup"><span data-stu-id="f30dc-148">Open the `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="f30dc-149">Puede tener acceso a las solicitudes del usuario en sus controladores a través del objeto principal de seguridad `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="f30dc-149">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // The object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // The subject or nameidentifier claim can be used to uniquely identify the user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="f30dc-150">Ejecute</span><span class="sxs-lookup"><span data-stu-id="f30dc-150">Run</span></span>
<span data-ttu-id="f30dc-151">Por último, compile y ejecute su aplicación.</span><span class="sxs-lookup"><span data-stu-id="f30dc-151">Finally, build and run your app!</span></span>   <span data-ttu-id="f30dc-152">Inicie sesión con una cuenta personal de Microsoft o con una cuenta profesional o educativa y observe cómo se refleja la identidad del usuario en la barra de navegación superior.</span><span class="sxs-lookup"><span data-stu-id="f30dc-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="f30dc-153">Ahora dispone de una aplicación web protegida mediante protocolos estándar del sector que pueden autenticar a los usuarios tanto con sus cuentas personales como con sus cuentas profesionales/educativas.</span><span class="sxs-lookup"><span data-stu-id="f30dc-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="f30dc-154">Como referencia, el ejemplo finalizado (sin sus valores de configuración) [se proporciona en forma de archivo .zip aquí](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), aunque también puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="f30dc-154">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="f30dc-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f30dc-155">Next steps</span></span>
<span data-ttu-id="f30dc-156">Ahora puede pasar a temas más avanzados.</span><span class="sxs-lookup"><span data-stu-id="f30dc-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="f30dc-157">También puede probar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f30dc-157">You may want to try:</span></span>

[<span data-ttu-id="f30dc-158">Proteger una API web con el punto de conexión v2.0 >></span><span class="sxs-lookup"><span data-stu-id="f30dc-158">Secure a Web API with the the v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="f30dc-159">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="f30dc-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="f30dc-160">La guía del desarrollador de v2.0 >></span><span class="sxs-lookup"><span data-stu-id="f30dc-160">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="f30dc-161">Etiqueta "azure-active-directory" de StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="f30dc-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="f30dc-162">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="f30dc-162">Get security updates for our products</span></span>
<span data-ttu-id="f30dc-163">Le animamos a que obtenga notificaciones de los incidentes de seguridad que se produzcan; para ello, visite [esta página](https://technet.microsoft.com/security/dd252948) y suscríbase a las alertas de avisos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f30dc-163">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
