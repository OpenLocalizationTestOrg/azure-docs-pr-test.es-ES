---
title: "aaaAzure AD v2.0 .NET web API de aplicación que realiza la llamada Introducción | Documentos de Microsoft"
description: "Cómo toobuild una aplicación Web de MVC de .NET que llama a web services con Microsoft personal cuentas y cuentas profesionales o educativas para inicio de sesión."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="f479b-103">Llamada a una API web desde una aplicación web .NET</span><span class="sxs-lookup"><span data-stu-id="f479b-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="f479b-104">Con punto de conexión de hello v2.0, puede agregar aplicaciones web de autenticación tooyour rápidamente y las API web con la compatibilidad para ambas cuentas de Microsoft personales y cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="f479b-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="f479b-105">Aquí compilaremos una aplicación web MVC que inicia la sesión de los usuarios mediante OpenID Connect, con un poco de ayuda del middleware OWIN de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f479b-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="f479b-106">aplicación web de Hello obtener tokens de acceso de OAuth 2.0 para una web api protegida por OAuth 2.0 que permite crear, leer y eliminar en un determinado usuario "lista de tareas pendientes".</span><span class="sxs-lookup"><span data-stu-id="f479b-106">hello web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="f479b-107">Este tutorial se centran principalmente en el uso MSAL tooacquire y usar tokens de acceso en una aplicación web, se describe en su totalidad [aquí](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="f479b-107">This tutorial will focus primarily on using MSAL tooacquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="f479b-108">Como los requisitos previos, puede que desee toofirst Obtenga información acerca de cómo demasiado[agregar la aplicación web de básicos tooa de inicio de sesión](active-directory-v2-devquickstarts-dotnet-web.md) o cómo demasiado[asegurar correctamente una API web](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="f479b-108">As prerequisites, you may want toofirst learn how too[add basic sign-in tooa web app](active-directory-v2-devquickstarts-dotnet-web.md) or how too[properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f479b-109">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="f479b-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="f479b-110">toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="f479b-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="f479b-111">Descarga de código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f479b-111">Download sample code</span></span>
<span data-ttu-id="f479b-112">código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="f479b-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="f479b-113">toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) o esqueleto de Hola de clon:</span><span class="sxs-lookup"><span data-stu-id="f479b-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="f479b-114">Como alternativa, puede [descargar la aplicación hello completado como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) o aplicación de hello completado de clon:</span><span class="sxs-lookup"><span data-stu-id="f479b-114">Alternatively, you can [download hello completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone hello completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="f479b-115">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="f479b-115">Register an app</span></span>
<span data-ttu-id="f479b-116">Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f479b-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="f479b-117">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="f479b-117">Make sure to:</span></span>

* <span data-ttu-id="f479b-118">Copia hacia abajo hello **Id. de aplicación** asignado tooyour aplicación, ya que lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="f479b-118">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="f479b-119">Crear un **secreto de la aplicación** de hello **contraseña** tipo y copia hacia abajo de su valor para más tarde</span><span class="sxs-lookup"><span data-stu-id="f479b-119">Create an **App Secret** of hello **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="f479b-120">Agregar hello **Web** plataforma para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f479b-120">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="f479b-121">Escriba Hola correcto **URI de redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="f479b-121">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="f479b-122">uri de redireccionamiento Hello indica tooAzure AD donde se deben dirigir las respuestas de autenticación: Hola predeterminado para este tutorial es `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="f479b-122">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="f479b-123">Instalar OWIN</span><span class="sxs-lookup"><span data-stu-id="f479b-123">Install OWIN</span></span>
<span data-ttu-id="f479b-124">Agregar toohello de paquetes de NuGet de hello OWIN middleware `TodoList-WebApp` proyecto utilizando Hola Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="f479b-124">Add hello OWIN middleware NuGet packages toohello `TodoList-WebApp` project using hello Package Manager Console.</span></span>  <span data-ttu-id="f479b-125">middleware de OWIN Hola ser tooissue usa las solicitudes de inicio de sesión y cierre de sesión, administrar la sesión del usuario de Hola y obtener información acerca del usuario de hello, entre otras cosas.</span><span class="sxs-lookup"><span data-stu-id="f479b-125">hello OWIN middleware will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a><span data-ttu-id="f479b-126">Usuario de inicio de sesión hello en</span><span class="sxs-lookup"><span data-stu-id="f479b-126">Sign hello user in</span></span>
<span data-ttu-id="f479b-127">Configurar ahora Hola Hola de toouse de middleware OWIN [protocolo de autenticación OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="f479b-127">Now configure hello OWIN middleware toouse hello [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="f479b-128">Abra hello `web.config` archivo en la raíz de Hola de hello `TodoList-WebApp` del proyecto y escriba los valores de configuración de la aplicación Hola `<appSettings>` sección.</span><span class="sxs-lookup"><span data-stu-id="f479b-128">Open hello `web.config` file in hello root of hello `TodoList-WebApp` project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="f479b-129">Hola `ida:ClientId` es hello **Id. de aplicación** asignado tooyour aplicación de portal de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="f479b-129">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="f479b-130">Hola `ida:ClientSecret` es hello **secreto de la aplicación** que creó en el portal de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="f479b-130">hello `ida:ClientSecret` is hello **App Secret** you created in hello registration portal.</span></span>
  * <span data-ttu-id="f479b-131">Hola `ida:RedirectUri` es hello **Uri de redireccionamiento** que especificó en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f479b-131">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>
* <span data-ttu-id="f479b-132">Hola abierto `web.config` archivo en la raíz de Hola de hello `TodoList-Service` de proyectos y hello `ida:Audience` con Hola mismo **Id. de aplicación** como arriba.</span><span class="sxs-lookup"><span data-stu-id="f479b-132">Open hello `web.config` file in hello root of hello `TodoList-Service` project, and replace hello `ida:Audience` with hello same **Application Id** as above.</span></span>
* <span data-ttu-id="f479b-133">Archivo abierto hello `App_Start\Startup.Auth.cs` y agregue `using` instrucciones para las bibliotecas de Hola desde arriba.</span><span class="sxs-lookup"><span data-stu-id="f479b-133">Open hello file `App_Start\Startup.Auth.cs` and add `using` statements for hello libraries from above.</span></span>
* <span data-ttu-id="f479b-134">En Hola el mismo archivo, implemente hello `ConfigureAuth(...)` método.</span><span class="sxs-lookup"><span data-stu-id="f479b-134">In hello same file, implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="f479b-135">Hola parámetros que se proporciona en `OpenIDConnectAuthenticationOptions` servirá como coordenadas para su toocommunicate de aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f479b-135">hello parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a><span data-ttu-id="f479b-136">Usar tokens de acceso MSAL tooget</span><span class="sxs-lookup"><span data-stu-id="f479b-136">Use MSAL tooget access tokens</span></span>
<span data-ttu-id="f479b-137">Hola `AuthorizationCodeReceived` notificación, queremos toouse [OAuth 2.0, conjuntamente con OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code para un servicio de la lista de tareas pendientes de toohello token de acceso.</span><span class="sxs-lookup"><span data-stu-id="f479b-137">In hello `AuthorizationCodeReceived` notification, we want toouse [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code for an access token toohello To-Do List Service.</span></span>  <span data-ttu-id="f479b-138">MSAL puede facilitarle este proceso:</span><span class="sxs-lookup"><span data-stu-id="f479b-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="f479b-139">En primer lugar, instale la versión de vista previa de Hola de MSAL:</span><span class="sxs-lookup"><span data-stu-id="f479b-139">First, install hello preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="f479b-140">Y agregue otro `using` toohello instrucción `App_Start\Startup.Auth.cs` archivo para MSAL.</span><span class="sxs-lookup"><span data-stu-id="f479b-140">And add another `using` statement toohello `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="f479b-141">Ahora agregue un nuevo método hello `OnAuthorizationCodeReceived` controlador de eventos.</span><span class="sxs-lookup"><span data-stu-id="f479b-141">Now add a new method, hello `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="f479b-142">Este controlador utilizará MSAL tooacquire un toohello de token de acceso a API de la lista de tareas pendientes y token de Hola se almacenará en caché de tokens de MSAL para más tarde:</span><span class="sxs-lookup"><span data-stu-id="f479b-142">This handler will use MSAL tooacquire an access token toohello To-Do List API, and will store hello token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="f479b-143">En las aplicaciones web, MSAL tiene una caché de tokens extensible que puede ser utilizados toostore símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="f479b-143">In web apps, MSAL has an extensible token cache that can be used toostore tokens.</span></span>  <span data-ttu-id="f479b-144">Este ejemplo implementa hello `NaiveSessionCache` que usa tokens de toocache de almacenamiento de información de sesión de http.</span><span class="sxs-lookup"><span data-stu-id="f479b-144">This sample implements hello `NaiveSessionCache` which uses http session storage toocache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a><span data-ttu-id="f479b-145">Hola llamada API de Web</span><span class="sxs-lookup"><span data-stu-id="f479b-145">Call hello Web API</span></span>
<span data-ttu-id="f479b-146">Ahora es el momento tooactually usar access_token Hola adquiridos en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="f479b-146">Now it's time tooactually use hello access_token you acquired in step 3.</span></span>  <span data-ttu-id="f479b-147">Abra hello web app `Controllers\TodoListController.cs` de archivos, lo que hace que todos los Hola CRUD solicita toohello API de la lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="f479b-147">Open hello web app's `Controllers\TodoListController.cs` file, which makes all hello CRUD requests toohello To-Do List API.</span></span>

* <span data-ttu-id="f479b-148">Puede usar MSAL nuevo aquí toofetch access_tokens de Hola caché MSAL.</span><span class="sxs-lookup"><span data-stu-id="f479b-148">You can use MSAL again here toofetch access_tokens from hello MSAL cache.</span></span>  <span data-ttu-id="f479b-149">En primer lugar, agregue un `using` instrucción para MSAL toothis archivo.</span><span class="sxs-lookup"><span data-stu-id="f479b-149">First, add a `using` statement for MSAL toothis file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="f479b-150">Hola `Index` , MSAL use la acción `AcquireTokenSilentAsync` método tooget un access_token que pueden ser datos de uso tooread de hello servicio de lista de tareas:</span><span class="sxs-lookup"><span data-stu-id="f479b-150">In hello `Index` action, use MSAL's `AcquireTokenSilentAsync` method tooget an access_token that can be used tooread data from hello To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="f479b-151">Hello muestra, a continuación, agrega solicitud de HTTP GET resultante de token toohello hello como hello `Authorization` encabezado, qué servicio de lista de tareas pendientes de hello usa tooauthenticate solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="f479b-151">hello sample then adds hello resulting token toohello HTTP GET request as hello `Authorization` header, which hello To-Do List service uses tooauthenticate hello request.</span></span>
* <span data-ttu-id="f479b-152">Si devuelve Hola servicio de lista de tareas pendientes de un `401 Unauthorized` respuesta, hello access_tokens en MSAL ya no eran válidas por algún motivo.</span><span class="sxs-lookup"><span data-stu-id="f479b-152">If hello To-Do List service returns a `401 Unauthorized` response, hello access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="f479b-153">En este caso, debe quitar cualquier access_tokens de hello caché MSAL y mostrar un mensaje que es posible que necesiten toosign de nuevo, lo que reiniciará flujo de adquisición de tokens de Hola de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="f479b-153">In this case, you should drop any access_tokens from hello MSAL cache and show hello user a message that they may need toosign in again, which will restart hello token acquisition flow.</span></span>

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* <span data-ttu-id="f479b-154">De forma similar, si MSAL es no se puede tooreturn un access_token por cualquier motivo, debe indicar a hello toosign de usuario de nuevo.</span><span class="sxs-lookup"><span data-stu-id="f479b-154">Similarly, if MSAL is unable tooreturn an access_token for any reason, you should instruct hello user toosign in again.</span></span>  <span data-ttu-id="f479b-155">Esto es tan sencillo como detectar cualquier `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="f479b-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* <span data-ttu-id="f479b-156">Hola exactamente igual `AcquireTokenSilentAsync` llamada es implementd en hello `Create` y `Delete` acciones.</span><span class="sxs-lookup"><span data-stu-id="f479b-156">hello exact same `AcquireTokenSilentAsync` call is implementd in hello `Create` and `Delete` actions.</span></span>  <span data-ttu-id="f479b-157">En las aplicaciones web, puede usar este access_tokens de tooget MSAL método cada vez que necesite en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f479b-157">In web apps, you can use this MSAL method tooget access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="f479b-158">MSAL se encargará de adquirir, almacenar en caché y actualizar tokens por usted.</span><span class="sxs-lookup"><span data-stu-id="f479b-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="f479b-159">Por último, compile y ejecute su aplicación.</span><span class="sxs-lookup"><span data-stu-id="f479b-159">Finally, build and run your app!</span></span>  <span data-ttu-id="f479b-160">Inicie sesión con una Account de Microsoft o una cuenta de Azure AD y observe cómo se refleja la identidad del usuario de hello en la barra de navegación superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f479b-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="f479b-161">Agregar y eliminar algunos elementos de lista de tareas del usuario de Hola Hola toosee que OAuth 2.0 había protegida API llama en acción.</span><span class="sxs-lookup"><span data-stu-id="f479b-161">Add and delete some items from hello user's To-Do List toosee hello OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="f479b-162">Ahora dispone de una aplicación web y de una API web, ambas protegidas mediante protocolos estándar del sector, que pueden autenticar a los usuarios tanto con sus cuentas personales como con sus cuentas profesionales/educativas.</span><span class="sxs-lookup"><span data-stu-id="f479b-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="f479b-163">Como referencia, Hola completado ejemplo (sin los valores de configuración) [aquí se proporcione](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f479b-163">For reference, hello completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f479b-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f479b-164">Next Steps</span></span>
<span data-ttu-id="f479b-165">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="f479b-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="f479b-166">Guía del desarrollador de Hello v2.0 >></span><span class="sxs-lookup"><span data-stu-id="f479b-166">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="f479b-167">Etiqueta "azure-active-directory" de StackOverflow &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="f479b-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="f479b-168">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="f479b-168">Get security updates for our products</span></span>
<span data-ttu-id="f479b-169">Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.</span><span class="sxs-lookup"><span data-stu-id="f479b-169">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

