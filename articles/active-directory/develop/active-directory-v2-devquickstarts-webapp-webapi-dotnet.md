---
title: "Introducción a la API de llamada de la aplicación web de .NET v2.0 de Azure AD | Microsoft Docs"
description: "Cómo crear una aplicación web de MVC de .NET que llame a los servicios web mediante cuentas personales de Microsoft y cuentas profesionales o educativas para iniciar sesión."
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
ms.openlocfilehash: dc3162ae8e6ce622139125c2e78fa45d2e90d534
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="a9ec2-103">Llamada a una API web desde una aplicación web .NET</span><span class="sxs-lookup"><span data-stu-id="a9ec2-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="a9ec2-104">Con el punto de conexión v2.0 puede agregar rápidamente la autenticación a sus aplicaciones web y API web compatibles tanto con las cuentas personales de Microsoft como con las cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="a9ec2-105">Aquí compilaremos una aplicación web MVC que inicia la sesión de los usuarios mediante OpenID Connect, con un poco de ayuda del middleware OWIN de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="a9ec2-106">La aplicación web obtendrá tokens de acceso de OAuth 2.0 para una API web protegida por OAuth 2.0 que permite las tareas de creación, lectura y eliminación en la "lista de tareas pendientes" de un usuario determinado.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="a9ec2-107">Este tutorial se centrará principalmente en el uso de MSAL para obtener y usar tokens de acceso en una aplicación web, lo que se describe [aquí](active-directory-v2-flows.md#web-apps) en su totalidad.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="a9ec2-108">Como requisitos previos, es aconsejable que aprenda primero cómo [agregar un inicio de sesión básico a una aplicación web](active-directory-v2-devquickstarts-dotnet-web.md) o cómo [proteger correctamente una API web](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="a9ec2-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a9ec2-109">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión v2.0.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="a9ec2-110">Para determinar si debe utilizar la versión 2.0 del punto de conexión, obtenga información sobre las [limitaciones de esta versión](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a9ec2-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="a9ec2-111">Descarga de código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a9ec2-111">Download sample code</span></span>
<span data-ttu-id="a9ec2-112">El código de este tutorial se conserva [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="a9ec2-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="a9ec2-113">Para continuar, puede [descargar el esqueleto de la aplicación como un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) o clonar el esqueleto:</span><span class="sxs-lookup"><span data-stu-id="a9ec2-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="a9ec2-114">Como alternativa, puede [descargar la aplicación completada como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) o clonar la aplicación completada:</span><span class="sxs-lookup"><span data-stu-id="a9ec2-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="a9ec2-115">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="a9ec2-115">Register an app</span></span>
<span data-ttu-id="a9ec2-116">Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a9ec2-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="a9ec2-117">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="a9ec2-117">Make sure to:</span></span>

* <span data-ttu-id="a9ec2-118">Anota el **Id. de aplicación** asignado a su aplicación; lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="a9ec2-119">Crea un **secreto de la aplicación** del tipo **contraseña** y copia su valor para más tarde</span><span class="sxs-lookup"><span data-stu-id="a9ec2-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="a9ec2-120">Agregar la plataforma **web** para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-120">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="a9ec2-121">Escribir el **URI de redireccionamiento**correcto.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-121">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="a9ec2-122">El uri de redirección indica a Azure AD a dónde se deben dirigir las respuestas de autenticación: el valor predeterminado para este tutorial es `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="a9ec2-123">Instalar OWIN</span><span class="sxs-lookup"><span data-stu-id="a9ec2-123">Install OWIN</span></span>
<span data-ttu-id="a9ec2-124">Agregue los paquetes NuGet del middleware OWIN al proyecto `TodoList-WebApp` mediante la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span></span>  <span data-ttu-id="a9ec2-125">Se usará el middleware OWIN para emitir solicitudes de inicio y cierre de sesión, administrar la sesión del usuario y obtener información sobre el usuario, entre otras cosas.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a><span data-ttu-id="a9ec2-126">Iniciar la sesión del usuario</span><span class="sxs-lookup"><span data-stu-id="a9ec2-126">Sign the user in</span></span>
<span data-ttu-id="a9ec2-127">Ahora configure el middleware OWIN para usar el [protocolo de autenticación OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="a9ec2-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="a9ec2-128">Abra el archivo `web.config` en la raíz del proyecto `TodoList-WebApp` y escriba los valores de configuración de su aplicación en la sección `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="a9ec2-129">El `ida:ClientId` es el **identificador de aplicación** asignado a su aplicación en el portal de registro.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="a9ec2-130">El `ida:ClientSecret` es el **secreto de aplicación** que creó en el portal de registro.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span></span>
  * <span data-ttu-id="a9ec2-131">El `ida:RedirectUri` es el **identificador URI de redireccionamiento** que escribió en el portal.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>
* <span data-ttu-id="a9ec2-132">Abra el archivo `web.config` en la raíz del proyecto `TodoList-Service` y reemplace `ida:Audience` por el mismo **Id. de aplicación** que se ha utilizado antes.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span></span>
* <span data-ttu-id="a9ec2-133">Abra el archivo `App_Start\Startup.Auth.cs` y agregue instrucciones `using` para las bibliotecas anteriores.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span></span>
* <span data-ttu-id="a9ec2-134">Implemente el método `ConfigureAuth(...)` en el mismo archivo.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-134">In the same file, implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="a9ec2-135">Los parámetros que proporciona en `OpenIDConnectAuthenticationOptions` servirán como coordenadas para que su aplicación se comunique con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // The `AuthorizationCodeReceived` notification is used to capture and redeem the authorization_code that the v2.0 endpoint returns to your app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-to-get-access-tokens"></a><span data-ttu-id="a9ec2-136">Uso de MSAL para obtener tokens de acceso</span><span class="sxs-lookup"><span data-stu-id="a9ec2-136">Use MSAL to get access tokens</span></span>
<span data-ttu-id="a9ec2-137">En la notificación `AuthorizationCodeReceived`, deseamos usar [OAuth 2.0 conjuntamente con OpenID Connect](active-directory-v2-protocols.md) para canjear authorization_code por un token de acceso en el servicio de lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span></span>  <span data-ttu-id="a9ec2-138">MSAL puede facilitarle este proceso:</span><span class="sxs-lookup"><span data-stu-id="a9ec2-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="a9ec2-139">En primer lugar, instale la versión preliminar de MSAL:</span><span class="sxs-lookup"><span data-stu-id="a9ec2-139">First, install the preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="a9ec2-140">Y agregue otra instrucción `using` al archivo `App_Start\Startup.Auth.cs` para MSAL.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="a9ec2-141">Ahora agregue un nuevo método, el controlador de eventos `OnAuthorizationCodeReceived`.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="a9ec2-142">Este controlador usará MSAL para obtener un token de acceso a la API de la lista de tareas pendientes y almacenará el token en la caché de tokens de MSAL para su uso posterior:</span><span class="sxs-lookup"><span data-stu-id="a9ec2-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="a9ec2-143">En las aplicaciones web, MSAL tiene una caché de tokens extensible que puede utilizarse para almacenar los tokens.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span></span>  <span data-ttu-id="a9ec2-144">Este ejemplo implementa el `NaiveSessionCache` que usa almacenamiento de sesión http para almacenar los token en el caché.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a><span data-ttu-id="a9ec2-145">Llamada a la API web</span><span class="sxs-lookup"><span data-stu-id="a9ec2-145">Call the Web API</span></span>
<span data-ttu-id="a9ec2-146">Ahora es el momento de usar el access_token que adquirió en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-146">Now it's time to actually use the access_token you acquired in step 3.</span></span>  <span data-ttu-id="a9ec2-147">Abra el archivo `Controllers\TodoListController.cs` de la aplicación web para hacer todas las solicitudes CRUD a la API de la lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span></span>

* <span data-ttu-id="a9ec2-148">Puede usar MSAL aquí de nuevo para capturar access_tokens de la memoria caché de MSAL.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span></span>  <span data-ttu-id="a9ec2-149">En primer lugar, agregue una instrucción `using` para MSAL a este archivo.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-149">First, add a `using` statement for MSAL to this file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="a9ec2-150">En la acción `Index`, use el método `AcquireTokenSilentAsync` de MSAL para obtener un access_token que pueda utilizarse para leer datos desde el servicio de lista de tareas pendientes:</span><span class="sxs-lookup"><span data-stu-id="a9ec2-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="a9ec2-151">Entonces, el ejemplo agrega el token resultante a la solicitud HTTP GET como el encabezado de `Authorization`, que usa el servicio de lista de tareas pendientes para autenticar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span></span>
* <span data-ttu-id="a9ec2-152">Si el servicio de lista de tareas pendientes devuelve una respuesta `401 Unauthorized`, el access_tokens en MSAL dejó de ser válido por algún motivo.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="a9ec2-153">En este caso, debe anular cualquier access_tokens de la memoria caché de MSAL y mostrar al usuario un mensaje de que necesita iniciar sesión de nuevo, lo que reiniciará el flujo de adquisición del token.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span></span>

```C#
// ...
// If the call failed with access denied, then drop the current access token from the cache,
// and show the user an error indicating they might need to sign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need to sign in again.");
}
// ...
```

* <span data-ttu-id="a9ec2-154">Del mismo modo, si MSAL no puede devolver un access_token por cualquier motivo, se recomienda indicar al usuario que vuelva a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span></span>  <span data-ttu-id="a9ec2-155">Esto es tan sencillo como detectar cualquier `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="a9ec2-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* <span data-ttu-id="a9ec2-156">Se implementa exactamente la misma llamada de `AcquireTokenSilentAsync` en las acciones `Create` y `Delete`.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span></span>  <span data-ttu-id="a9ec2-157">En las aplicaciones web, puede utilizar este método MSAL para obtener access_tokens siempre que los necesite en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="a9ec2-158">MSAL se encargará de adquirir, almacenar en caché y actualizar tokens por usted.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="a9ec2-159">Por último, compile y ejecute su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-159">Finally, build and run your app!</span></span>  <span data-ttu-id="a9ec2-160">Inicie sesión con una cuenta Microsoft o con una cuenta de Azure AD y observe cómo se refleja la identidad del usuario en la barra de navegación superior.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="a9ec2-161">Agregue y elimine algunos elementos de lista de tareas del usuario para ver las llamadas de API protegidas de OAuth 2.0 en acción.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="a9ec2-162">Ahora dispone de una aplicación web y de una API web, ambas protegidas mediante protocolos estándar del sector, que pueden autenticar a los usuarios tanto con sus cuentas personales como con sus cuentas profesionales/educativas.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="a9ec2-163">Como referencia, [aquí puede ver](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip)el ejemplo finalizado (sin sus valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="a9ec2-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a9ec2-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9ec2-164">Next Steps</span></span>
<span data-ttu-id="a9ec2-165">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="a9ec2-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="a9ec2-166">La guía del desarrollador de v2.0 >></span><span class="sxs-lookup"><span data-stu-id="a9ec2-166">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="a9ec2-167">Etiqueta "azure-active-directory" de StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="a9ec2-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="a9ec2-168">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="a9ec2-168">Get security updates for our products</span></span>
<span data-ttu-id="a9ec2-169">Le animamos a que obtenga notificaciones de los incidentes de seguridad que se produzcan; para ello, visite [esta página](https://technet.microsoft.com/security/dd252948) y suscríbase a las alertas de avisos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="a9ec2-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

