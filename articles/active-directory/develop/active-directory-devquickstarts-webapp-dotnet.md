---
title: "aplicación web de .NET de aaaAzure AD Introducción | Documentos de Microsoft"
description: "Creación de una aplicación web de .NET MVC que se integra con Azure AD para el inicio de sesión."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="595e4-103">Inicio y cierre de sesión de la aplicación web de ASP.NET con Azure AD</span><span class="sxs-lookup"><span data-stu-id="595e4-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="595e4-104">Al proporcionar un único inicio de sesión y cierre de sesión con unas pocas líneas de código, Azure Active Directory (Azure AD) simplifica toooutsource aplicación web administración de identidades.</span><span class="sxs-lookup"><span data-stu-id="595e4-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="595e4-105">Puede iniciar sesión a los usuarios dentro y fuera de las aplicaciones web ASP.NET mediante la implementación de Microsoft de Hola de interfaz Web abierta para el middleware de .NET (OWIN).</span><span class="sxs-lookup"><span data-stu-id="595e4-105">You can sign users in and out of ASP.NET web apps by using hello Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="595e4-106">El middleware OWIN controlado por la comunidad se incluye en .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="595e4-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="595e4-107">Este artículo se muestra cómo toouse OWIN para:</span><span class="sxs-lookup"><span data-stu-id="595e4-107">This article shows how toouse OWIN to:</span></span>

* <span data-ttu-id="595e4-108">Usuarios de inicio de sesión en tooweb aplicaciones con Azure AD como proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="595e4-108">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="595e4-109">Mostrar información del usuario.</span><span class="sxs-lookup"><span data-stu-id="595e4-109">Display some user information.</span></span>
* <span data-ttu-id="595e4-110">Usuarios de inicio de sesión de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="595e4-110">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="595e4-111">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="595e4-111">Before you get started</span></span>
* <span data-ttu-id="595e4-112">Descargar hello [esqueleto aplicación](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o descargar hello [ejemplo completo](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="595e4-112">Download hello [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download hello [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="595e4-113">También necesita a un inquilino de Azure AD en qué aplicación de hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="595e4-113">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="595e4-114">Si aún no tiene un inquilino de Azure AD, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="595e4-114">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="595e4-115">Cuando esté listo, siga los procedimientos de hello en Hola cuatro secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="595e4-115">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="595e4-116">Paso 1: Registrar Hola nueva aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="595e4-116">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="595e4-117">tooset configurar usuarios de tooauthenticate de aplicación Hola, registra por primera vez en el inquilino haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="595e4-117">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="595e4-118">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="595e4-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="595e4-119">En la barra superior de hello, haga clic en el nombre de cuenta.</span><span class="sxs-lookup"><span data-stu-id="595e4-119">On hello top bar, click your account name.</span></span> <span data-ttu-id="595e4-120">En hello **Directory** inquilinos de Active Directory de hello seleccione donde desea que la aplicación de hello tooregister, la lista.</span><span class="sxs-lookup"><span data-stu-id="595e4-120">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="595e4-121">Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="595e4-121">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="595e4-122">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="595e4-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="595e4-123">Siga Hola solicita toocreate un nuevo **aplicación Web o WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="595e4-123">Follow hello prompts toocreate a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="595e4-124">**Nombre** describe hello toousers de aplicación.</span><span class="sxs-lookup"><span data-stu-id="595e4-124">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="595e4-125">**Dirección URL de inicio de sesión** es Hola dirección URL base de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="595e4-125">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="595e4-126">dirección URL de predeterminada del esqueleto Hello es https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="595e4-126">hello skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="595e4-127">Después de haber completado el registro de hello, Azure AD le asigna aplicación hello un identificador de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="595e4-127">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="595e4-128">Copiar valor de Hola de hello toouse de página de aplicación en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="595e4-128">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="595e4-129">De hello **configuración** -> **propiedades** página de la aplicación, actualice Hola App ID URI.</span><span class="sxs-lookup"><span data-stu-id="595e4-129">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="595e4-130">Hola **App ID URI** es un identificador único para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="595e4-130">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="595e4-131">Hello convención de nomenclatura es `https://<tenant-domain>/<app-name>` (por ejemplo, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="595e4-131">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="595e4-132">Paso 2: Configurar la canalización de autenticación de hello aplicación toouse hello OWIN</span><span class="sxs-lookup"><span data-stu-id="595e4-132">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="595e4-133">En este paso, configurará hello OWIN middleware toouse Hola OpenID Connect protocolo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="595e4-133">In this step, you configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="595e4-134">Usar las solicitudes de inicio de sesión y cierre de sesión de tooissue OWIN, administrar sesiones de usuario, obtener información de usuario y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="595e4-134">You use OWIN tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="595e4-135">toobegin, Agregar proyecto toohello de paquetes de NuGet de middleware de hello OWIN mediante el uso de la consola de administrador de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="595e4-135">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="595e4-136">tooadd llama a un proyecto de inicio de OWIN clase toohello `Startup.cs`, haga clic en proyecto de hello, seleccione **agregar**, seleccione **nuevo elemento**y, a continuación, busque **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="595e4-136">tooadd an OWIN Startup class toohello project called `Startup.cs`, right-click hello project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="595e4-137">middleware de OWIN Hola invoca hello **Configuration(...)**  método cuando se inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="595e4-137">hello OWIN middleware invokes hello **Configuration(...)** method when hello app starts.</span></span>
3. <span data-ttu-id="595e4-138">Cambie la declaración de clase de hello demasiado`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="595e4-138">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="595e4-139">Ya hemos implementado parte de esta clase en otro archivo.</span><span class="sxs-lookup"><span data-stu-id="595e4-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="595e4-140">Hola **Configuration(...)**  método, realizar una llamada demasiado**ConfgureAuth(...)**  tooset la autenticación para aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="595e4-140">In hello **Configuration(...)** method, make a call too**ConfgureAuth(...)** tooset up authentication for hello app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="595e4-141">Abra el archivo de App_Start\Startup.Auth.cs hello y luego implementar hello **ConfigureAuth(...)**  (método).</span><span class="sxs-lookup"><span data-stu-id="595e4-141">Open hello App_Start\Startup.Auth.cs file, and then implement hello **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="595e4-142">Hola parámetros que se proporciona en *OpenIDConnectAuthenticationOptions* actuar como coordenadas de hello toocommunicate de aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="595e4-142">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello app toocommunicate with Azure AD.</span></span> <span data-ttu-id="595e4-143">También deberá tooset la autenticación con cookies, porque Hola OpenID Connect middleware utiliza cookies en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="595e4-143">You also need tooset up cookie authentication, because hello OpenID Connect middleware uses cookies in hello background.</span></span>

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. <span data-ttu-id="595e4-144">Abrir el archivo web.config de hello en raíz de hello del proyecto de hello y, a continuación, escriba los valores de configuración de Hola Hola `<appSettings>` sección.</span><span class="sxs-lookup"><span data-stu-id="595e4-144">Open hello web.config file in hello root of hello project, and then enter hello configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="595e4-145">`ida:ClientId`: Hola GUID que copió de hello portal de Azure en "paso 1: registrar Hola nueva aplicación con Azure AD."</span><span class="sxs-lookup"><span data-stu-id="595e4-145">`ida:ClientId`: hello GUID you copied from hello Azure portal in "Step 1: Register hello new app with Azure AD."</span></span>
  * <span data-ttu-id="595e4-146">`ida:Tenant`: nombre de hello del inquilino de Azure AD (por ejemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="595e4-146">`ida:Tenant`: hello name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="595e4-147">`ida:PostLogoutRedirectUri`: indicador de Hola que indica a Azure AD que se debe redirigir un usuario después de una solicitud de cierre de sesión se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="595e4-147">`ida:PostLogoutRedirectUri`: hello indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="595e4-148">Paso 3: Usar OWIN tooissue inicio de sesión y cierre de sesión solicita tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="595e4-148">Step 3: Use OWIN tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="595e4-149">aplicación Hello ahora es toocommunicate configurada correctamente con Azure AD mediante el protocolo de autenticación de OpenID Connect de Hola.</span><span class="sxs-lookup"><span data-stu-id="595e4-149">hello app is now properly configured toocommunicate with Azure AD by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="595e4-150">OWIN ha controlado todos los detalles de Hola de transmitir mensajes de autenticación, validar los tokens de Azure AD y mantener las sesiones de usuario.</span><span class="sxs-lookup"><span data-stu-id="595e4-150">OWIN has handled all of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="595e4-151">Lo único que queda es toogive a los usuarios una manera toosign en y cierre de sesión.</span><span class="sxs-lookup"><span data-stu-id="595e4-151">All that remains is toogive your users a way toosign in and sign out.</span></span>

1. <span data-ttu-id="595e4-152">Puede usar autorizar su toosign de usuarios toorequire de controladores en las etiquetas para acceder a determinadas páginas.</span><span class="sxs-lookup"><span data-stu-id="595e4-152">You can use authorize tags in your controllers toorequire users toosign in before they access certain pages.</span></span> <span data-ttu-id="595e4-153">toodo por lo tanto, abra controllers\homecontroller y, a continuación, agregue hello `[Authorize]` etiqueta toohello sobre el controlador.</span><span class="sxs-lookup"><span data-stu-id="595e4-153">toodo so, open Controllers\HomeController.cs, and then add hello `[Authorize]` tag toohello About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="595e4-154">También puede usar solicitudes de autenticación OWIN toodirectly problema desde dentro del código.</span><span class="sxs-lookup"><span data-stu-id="595e4-154">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span> <span data-ttu-id="595e4-155">toodo, abra Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="595e4-155">toodo so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="595e4-156">A continuación, en acciones de SignIn() y SignOut() de hello, emitir desafío OpenID Connect y solicitudes de cierre de sesión.</span><span class="sxs-lookup"><span data-stu-id="595e4-156">Then, in hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. <span data-ttu-id="595e4-157">Abra Views\Shared\_LoginPartial.cshtml tooshow Hola usuario Hola aplicación inicio de sesión y cierre de sesión vínculos y tooprint el nombre del usuario de hello en una vista.</span><span class="sxs-lookup"><span data-stu-id="595e4-157">Open Views\Shared\_LoginPartial.cshtml tooshow hello user hello app sign-in and sign-out links, and tooprint out hello user's name in a view.</span></span>

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a><span data-ttu-id="595e4-158">Paso 4: Visualización de la información del usuario</span><span class="sxs-lookup"><span data-stu-id="595e4-158">Step 4: Display user information</span></span>
<span data-ttu-id="595e4-159">Cuando autentica a los usuarios con OpenID Connect, Azure AD devuelve una aplicación de toohello id_token que contiene "notificaciones", o aserciones sobre usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="595e4-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token toohello app that contains "claims," or assertions about hello user.</span></span> <span data-ttu-id="595e4-160">Puede usar estas aplicaciones de notificaciones toopersonalize Hola haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="595e4-160">You can use these claims toopersonalize hello app by doing hello following:</span></span>

1. <span data-ttu-id="595e4-161">Abra el archivo controllers\homecontroller. cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="595e4-161">Open hello Controllers\HomeController.cs file.</span></span> <span data-ttu-id="595e4-162">Puede tener acceso a solicitudes del usuario de hello en los controladores a través de hello `ClaimsPrincipal.Current` objeto de entidad de seguridad.</span><span class="sxs-lookup"><span data-stu-id="595e4-162">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. <span data-ttu-id="595e4-163">Compile y ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="595e4-163">Build and run hello app.</span></span> <span data-ttu-id="595e4-164">Si aún no ha creado un nuevo usuario en el inquilino con un dominio de onmicrosoft.com, ahora es Hola tiempo toodo para.</span><span class="sxs-lookup"><span data-stu-id="595e4-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is hello time toodo so.</span></span> <span data-ttu-id="595e4-165">Este es el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="595e4-165">Here's how:</span></span>

  <span data-ttu-id="595e4-166">a.</span><span class="sxs-lookup"><span data-stu-id="595e4-166">a.</span></span> <span data-ttu-id="595e4-167">Inicie sesión con ese usuario y tenga en cuenta cómo se refleja la identidad del usuario de hello en la barra superior Hola.</span><span class="sxs-lookup"><span data-stu-id="595e4-167">Sign in with that user, and note how hello user's identity is reflected on hello top bar.</span></span>

  <span data-ttu-id="595e4-168">b.</span><span class="sxs-lookup"><span data-stu-id="595e4-168">b.</span></span> <span data-ttu-id="595e4-169">Cierre la sesión y vuelva a iniciarla con otro usuario en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="595e4-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="595e4-170">c.</span><span class="sxs-lookup"><span data-stu-id="595e4-170">c.</span></span> <span data-ttu-id="595e4-171">Si se siente especialmente ambicioso, registre y ejecute otra instancia de esta aplicación (con su propio clientId) y vea el inicio de sesión único en acción.</span><span class="sxs-lookup"><span data-stu-id="595e4-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="595e4-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="595e4-172">Next steps</span></span>
<span data-ttu-id="595e4-173">Como referencia, vea [ejemplo hello completado](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (sin los valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="595e4-173">For reference, see [hello completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="595e4-174">Ahora puede mover en toomore temas avanzados.</span><span class="sxs-lookup"><span data-stu-id="595e4-174">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="595e4-175">Por ejemplo, intente [proteger una API web con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="595e4-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
