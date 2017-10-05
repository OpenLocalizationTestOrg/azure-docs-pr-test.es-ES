---
title: "Introducción a la aplicación web de .NET de Azure AD | Microsoft Docs"
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
ms.openlocfilehash: 7ac5d3e5cc28ead993e159d003244e6451acb0cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="e1c32-103">Inicio y cierre de sesión de la aplicación web de ASP.NET con Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1c32-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="e1c32-104">Azure Active Directory (Azure AD) facilita la externalización de la administración de identidad de las aplicaciones web al proporcionar un inicio y cierre de sesión únicos con unas cuantas líneas de código.</span><span class="sxs-lookup"><span data-stu-id="e1c32-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="e1c32-105">Puede iniciar y cerrar la sesión de los usuarios en las aplicaciones web de ASP.NET mediante la implementación de Microsoft del middleware Open Web Interface for .NET (OWIN).</span><span class="sxs-lookup"><span data-stu-id="e1c32-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="e1c32-106">El middleware OWIN controlado por la comunidad se incluye en .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e1c32-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="e1c32-107">En este artículo se muestra cómo usar OWIN para:</span><span class="sxs-lookup"><span data-stu-id="e1c32-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="e1c32-108">Iniciar la sesión de los usuarios en aplicaciones web mediante Azure AD como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="e1c32-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="e1c32-109">Mostrar información del usuario.</span><span class="sxs-lookup"><span data-stu-id="e1c32-109">Display some user information.</span></span>
* <span data-ttu-id="e1c32-110">Cerrar la sesión de los usuarios en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e1c32-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="e1c32-111">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="e1c32-111">Before you get started</span></span>
* <span data-ttu-id="e1c32-112">Descargue el [esqueleto de la aplicación](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o el [ejemplo completado](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e1c32-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="e1c32-113">También necesita a un inquilino de Azure AD en el que se va a registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1c32-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="e1c32-114">Si aún no tiene uno, [descubra cómo conseguirlo](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e1c32-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="e1c32-115">Cuando esté listo, siga los procedimientos descritos en las cuatro secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="e1c32-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="e1c32-116">Paso 1: Registro de la nueva aplicación en Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1c32-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="e1c32-117">Para configurar la aplicación para autenticar a los usuarios, primero regístrela mediante estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e1c32-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="e1c32-118">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1c32-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e1c32-119">En la barra superior, haga clic en el nombre de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="e1c32-119">On the top bar, click your account name.</span></span> <span data-ttu-id="e1c32-120">En la lista **Directorio** lista, seleccione el inquilino de Active Directory donde quiere registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1c32-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="e1c32-121">Haga clic en **Más servicios** en el panel izquierdo y seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e1c32-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e1c32-122">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e1c32-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="e1c32-123">Siga las indicaciones para crear una nueva **aplicación web o WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="e1c32-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="e1c32-124">**Nombre**: describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e1c32-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="e1c32-125">La **dirección URL de inicio de sesión** es la dirección URL base de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1c32-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="e1c32-126">La dirección URL predeterminada del esqueleto es https://localhost:44320/.</span><span class="sxs-lookup"><span data-stu-id="e1c32-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="e1c32-127">Después de haber completado el registro, Azure AD le asigna a la aplicación un id. de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="e1c32-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="e1c32-128">Copie el valor de la página de aplicación para usarlo en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="e1c32-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="e1c32-129">En la página **Configuración** -> **Propiedades** de la aplicación, actualice el URI del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1c32-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="e1c32-130">El **URI de identificador de aplicación** es un identificador único para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1c32-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="e1c32-131">La convención de nomenclatura es `https://<tenant-domain>/<app-name>` (por ejemplo, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="e1c32-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="e1c32-132">Paso 2: Configuración de la aplicación para que use la canalización de autenticación OWIN</span><span class="sxs-lookup"><span data-stu-id="e1c32-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="e1c32-133">En este paso, configuraremos el middleware OWIN para usar el protocolo de autenticación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="e1c32-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="e1c32-134">Usará OWIN para emitir solicitudes de inicio y cierre de sesión, administrar sesiones de usuario, obtener información del usuario, etc.</span><span class="sxs-lookup"><span data-stu-id="e1c32-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="e1c32-135">Para comenzar, agregue al proyecto los paquetes NuGet del middleware OWIN mediante la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="e1c32-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="e1c32-136">Para agregar una clase de inicio de OWIN al proyecto denominado `Startup.cs`, haga clic con el botón derecho en el proyecto, seleccione **Agregar**, **Nuevo elemento** y luego busque **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="e1c32-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="e1c32-137">El middleware de OWIN invoca el método **Configuration(...)** cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1c32-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="e1c32-138">Cambie la declaración de clase a `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="e1c32-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="e1c32-139">Ya hemos implementado parte de esta clase en otro archivo.</span><span class="sxs-lookup"><span data-stu-id="e1c32-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="e1c32-140">En el método **Configuration(...)**, realice una llamada a **ConfgureAuth(...)** para configurar la autenticación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1c32-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="e1c32-141">Abra el archivo App_Start\Startup.Auth.cs y luego implemente el método **ConfigureAuth(...)**.</span><span class="sxs-lookup"><span data-stu-id="e1c32-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="e1c32-142">Los parámetros que se proporcionan en *OpenIDConnectAuthenticationOptions* sirven de coordenadas de la aplicación para comunicarse con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1c32-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="e1c32-143">También debe configurar la autenticación con cookies, ya que el middleware OpenID Connect usa cookies en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="e1c32-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

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

5. <span data-ttu-id="e1c32-144">Abra el archivo web.config en la raíz del proyecto y luego especifique los valores de configuración en la sección `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="e1c32-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="e1c32-145">`ida:ClientId`: el GUID que copió de Azure Portal en "Paso 1: Registro de la nueva aplicación en Azure AD".</span><span class="sxs-lookup"><span data-stu-id="e1c32-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="e1c32-146">`ida:Tenant`: el dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="e1c32-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="e1c32-147">`ida:PostLogoutRedirectUri`: el indicador que señala a Azure AD dónde se debe redirigir a un usuario después de completarse correctamente una solicitud de cierre de sesión.</span><span class="sxs-lookup"><span data-stu-id="e1c32-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="e1c32-148">Paso 3: Uso de OWIN para emitir solicitudes de inicio y cierre de sesión a Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1c32-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="e1c32-149">Ahora la aplicación está correctamente configurada para comunicarse con Azure AD mediante el protocolo de autenticación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="e1c32-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="e1c32-150">OWIN se ha ocupado de todos los detalles de la creación de mensajes de autenticación, validación de tokens de Azure AD y mantenimiento de sesiones de usuario.</span><span class="sxs-lookup"><span data-stu-id="e1c32-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="e1c32-151">Lo único que queda consiste en ofrecer a sus usuarios una forma de iniciar y cerrar sesión.</span><span class="sxs-lookup"><span data-stu-id="e1c32-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="e1c32-152">Puede usar etiquetas de autorización en los controladores para exigir que los usuarios inicien sesión para poder acceder a determinadas páginas.</span><span class="sxs-lookup"><span data-stu-id="e1c32-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="e1c32-153">Para ello, abra Controllers\HomeController.cs y luego agregue la etiqueta `[Authorize]` al controlador About.</span><span class="sxs-lookup"><span data-stu-id="e1c32-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="e1c32-154">También puede usar OWIN para emitir directamente solicitudes de autenticación desde dentro de su código.</span><span class="sxs-lookup"><span data-stu-id="e1c32-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="e1c32-155">Para ello, abra Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="e1c32-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="e1c32-156">A continuación, en las acciones SignIn() y SignOut(), emita las solicitudes de desafío y cierre de sesión de OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="e1c32-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="e1c32-157">Abra Views\Shared\_LoginPartial.cshtml para mostrar al usuario los vínculos de inicio y cierre de sesión de la aplicación y para imprimir el nombre del usuario en una vista.</span><span class="sxs-lookup"><span data-stu-id="e1c32-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="e1c32-158">Paso 4: Visualización de la información del usuario</span><span class="sxs-lookup"><span data-stu-id="e1c32-158">Step 4: Display user information</span></span>
<span data-ttu-id="e1c32-159">Cuando los usuarios se autentican con OpenID Connect, Azure AD devuelve un id_token a la aplicación que contiene "notificaciones" o aserciones sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="e1c32-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="e1c32-160">Puede usar estas notificaciones para personalizar la aplicación de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="e1c32-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="e1c32-161">Abra el archivo Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="e1c32-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="e1c32-162">Puede tener acceso a las solicitudes del usuario en sus controladores a través del objeto principal de seguridad `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="e1c32-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="e1c32-163">Compile y ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e1c32-163">Build and run the app.</span></span> <span data-ttu-id="e1c32-164">Si aún no ha creado un nuevo usuario en el inquilino con un dominio onmicrosoft.com, ahora es el momento de hacerlo.</span><span class="sxs-lookup"><span data-stu-id="e1c32-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="e1c32-165">Este es el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="e1c32-165">Here's how:</span></span>

  <span data-ttu-id="e1c32-166">a.</span><span class="sxs-lookup"><span data-stu-id="e1c32-166">a.</span></span> <span data-ttu-id="e1c32-167">Inicie sesión con ese usuario y observe cómo se refleja la identidad del usuario en la barra superior.</span><span class="sxs-lookup"><span data-stu-id="e1c32-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="e1c32-168">b.</span><span class="sxs-lookup"><span data-stu-id="e1c32-168">b.</span></span> <span data-ttu-id="e1c32-169">Cierre la sesión y vuelva a iniciarla con otro usuario en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="e1c32-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="e1c32-170">c.</span><span class="sxs-lookup"><span data-stu-id="e1c32-170">c.</span></span> <span data-ttu-id="e1c32-171">Si se siente especialmente ambicioso, registre y ejecute otra instancia de esta aplicación (con su propio clientId) y vea el inicio de sesión único en acción.</span><span class="sxs-lookup"><span data-stu-id="e1c32-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1c32-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1c32-172">Next steps</span></span>
<span data-ttu-id="e1c32-173">Como referencia, consulte el [ejemplo completado](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (sin sus valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="e1c32-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="e1c32-174">Ahora puede pasar a temas más avanzados.</span><span class="sxs-lookup"><span data-stu-id="e1c32-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="e1c32-175">Por ejemplo, intente [proteger una API web con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e1c32-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
