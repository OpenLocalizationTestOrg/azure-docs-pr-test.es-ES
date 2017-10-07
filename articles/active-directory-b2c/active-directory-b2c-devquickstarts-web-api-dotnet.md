---
title: aaaAzure B2C de Active Directory | Documentos de Microsoft
description: "¿Cómo toobuild una aplicación Web de .NET y llamar a una web api con tokens de acceso de Azure Active Directory B2C y OAuth 2.0."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="09352-103">Azure AD B2C: llamada a una API web de .NET desde una aplic. web de .NET</span><span class="sxs-lookup"><span data-stu-id="09352-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="09352-104">Mediante el uso de Azure AD B2C, puede agregar aplicaciones web de identidad eficaz administración características tooyour y las API web.</span><span class="sxs-lookup"><span data-stu-id="09352-104">By using Azure AD B2C, you can add powerful identity management features tooyour web apps and web APIs.</span></span> <span data-ttu-id="09352-105">Este artículo describe cómo toorequest tokens de acceso y realizar llamadas desde una "lista de tareas pendientes" de .NET tooa de aplicación web .NET web api.</span><span class="sxs-lookup"><span data-stu-id="09352-105">This article discusses how toorequest access tokens and make calls from a .NET "to-do list" web app tooa .NET web api.</span></span>

<span data-ttu-id="09352-106">En este artículo no cubre cómo tooimplement sesión, inicio de sesión y el perfil de administración con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="09352-106">This article does not cover how tooimplement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="09352-107">Se centra en las API de web que realiza la llamada después de hello usuario ya está autenticado.</span><span class="sxs-lookup"><span data-stu-id="09352-107">It focuses on calling web APIs after hello user is already authenticated.</span></span> <span data-ttu-id="09352-108">Si todavía no lo ha hecho, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="09352-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="09352-109">Comenzar a trabajar con una [aplicación web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="09352-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="09352-110">Comenzar a trabajar con una [API web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="09352-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="09352-111">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="09352-111">Prerequisite</span></span>

<span data-ttu-id="09352-112">toobuild una aplicación web que llama a una web api, necesita:</span><span class="sxs-lookup"><span data-stu-id="09352-112">toobuild a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="09352-113">[Crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="09352-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="09352-114">[Registrar una API web](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="09352-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="09352-115">[Registrar una aplicación web](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="09352-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="09352-116">[Configurar directivas](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="09352-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="09352-117">[GRANT Hola web app permisos toouse Hola web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="09352-117">[Grant hello web app permissions toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09352-118">aplicación de cliente de Hello y API web deben usar directorio de hello misma instancia de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="09352-118">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="download-hello-code"></a><span data-ttu-id="09352-119">Descargar código de hello</span><span class="sxs-lookup"><span data-stu-id="09352-119">Download hello code</span></span>

<span data-ttu-id="09352-120">código de Hello para este tutorial se mantiene en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="09352-120">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="09352-121">Puede clonar el ejemplo hello ejecutando:</span><span class="sxs-lookup"><span data-stu-id="09352-121">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="09352-122">Después de descargar el código de ejemplo de Hola, inició tooget de archivo .sln de hello abrir Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09352-122">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="09352-123">archivo de solución de Hello contiene dos proyectos: `TaskWebApp` y `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="09352-123">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="09352-124">`TaskWebApp`es una aplicación web MVC que Hola usuario interactúa con.</span><span class="sxs-lookup"><span data-stu-id="09352-124">`TaskWebApp` is a MVC web application that hello user interacts with.</span></span> <span data-ttu-id="09352-125">`TaskService`es la API de web back-end de la aplicación hello que almacena la lista de tareas pendientes de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="09352-125">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="09352-126">En este artículo no cubre creación hello `TaskWebApp` aplicación web o hello `TaskService` web api.</span><span class="sxs-lookup"><span data-stu-id="09352-126">This article does not cover building hello `TaskWebApp` web app or hello `TaskService` web api.</span></span> <span data-ttu-id="09352-127">toolearn cómo toobuild Hola .NET web aplicación con Azure AD B2C, consulte nuestro [tutorial de aplicación web de .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="09352-127">toolearn how toobuild hello .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="09352-128">toolearn cómo toobuild Hola .NET web API protegida con Azure AD B2C, consulte nuestro [tutorial de API web de .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="09352-128">toolearn how toobuild hello .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="09352-129">Actualizar configuración de hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="09352-129">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="09352-130">Nuestro ejemplo es toouse configurado Hola directivas e ID de cliente de nuestro inquilino de demostración.</span><span class="sxs-lookup"><span data-stu-id="09352-130">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="09352-131">Si desea que toouse su propio inquilino:</span><span class="sxs-lookup"><span data-stu-id="09352-131">If you would like toouse your own tenant:</span></span>

1. <span data-ttu-id="09352-132">Abra `web.config` en hello `TaskService` de proyectos y valores de hello para</span><span class="sxs-lookup"><span data-stu-id="09352-132">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>

    * <span data-ttu-id="09352-133">`ida:Tenant` por el nombre del inquilino</span><span class="sxs-lookup"><span data-stu-id="09352-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="09352-134">`ida:ClientId` por el identificador de la aplicación de API web</span><span class="sxs-lookup"><span data-stu-id="09352-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="09352-135">`ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"</span><span class="sxs-lookup"><span data-stu-id="09352-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="09352-136">Abra `web.config` en hello `TaskWebApp` de proyectos y valores de hello para</span><span class="sxs-lookup"><span data-stu-id="09352-136">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>

    * <span data-ttu-id="09352-137">`ida:Tenant` por el nombre del inquilino</span><span class="sxs-lookup"><span data-stu-id="09352-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="09352-138">`ida:ClientId` por el identificador de la aplicación de API web</span><span class="sxs-lookup"><span data-stu-id="09352-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="09352-139">`ida:ClientSecret` por la clave secreta de aplicación web</span><span class="sxs-lookup"><span data-stu-id="09352-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="09352-140">`ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"</span><span class="sxs-lookup"><span data-stu-id="09352-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="09352-141">`ida:EditProfilePolicyId` por el nombre de la directiva "Editar perfil"</span><span class="sxs-lookup"><span data-stu-id="09352-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="09352-142">`ida:ResetPasswordPolicyId` por el nombre de la directiva "Restablecer contraseña"</span><span class="sxs-lookup"><span data-stu-id="09352-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="09352-143">Solicitud y guardado de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="09352-143">Requesting and saving an access token</span></span>

### <a name="specify-hello-permissions"></a><span data-ttu-id="09352-144">Especificar permisos de Hola</span><span class="sxs-lookup"><span data-stu-id="09352-144">Specify hello permissions</span></span>

<span data-ttu-id="09352-145">En orden toomake Hola llamada toohello API web, necesita tooauthenticate Hola usuario (mediante la directiva de inicio de sesión-up/inicio de sesión de) y [recibir un token de acceso](active-directory-b2c-access-tokens.md) de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="09352-145">In order toomake hello call toohello web API, you need tooauthenticate hello user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="09352-146">En orden tooreceive un token de acceso, primero debe especificar permisos de hello le gustaría toogrant de token de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="09352-146">In order tooreceive an access token, you first must specify hello permissions you would like hello access token toogrant.</span></span> <span data-ttu-id="09352-147">los permisos de Hola se especifican en hello `scope` parámetro al realizar Hola solicitud toohello `/authorize` punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="09352-147">hello permissions are specified in hello `scope` parameter when you make hello request toohello `/authorize` endpoint.</span></span> <span data-ttu-id="09352-148">Por ejemplo, tooacquire aplicación de recursos de toohello de permiso que tiene un token de acceso con hello "lectura" Hola App ID URI de `https://contoso.onmicrosoft.com/tasks`, ámbito Hola sería `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="09352-148">For example, tooacquire an access token with hello “read” permission toohello resource application that has hello App ID URI of `https://contoso.onmicrosoft.com/tasks`, hello scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="09352-149">ámbito de hello toospecify en nuestro archivo de ejemplo, abra hello `App_Start\Startup.Auth.cs` y definir hello `Scope` variable OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="09352-149">toospecify hello scope in our sample, open hello file `App_Start\Startup.Auth.cs` and define hello `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a><span data-ttu-id="09352-150">Código de autorización de Hola para un token de acceso de Exchange</span><span class="sxs-lookup"><span data-stu-id="09352-150">Exchange hello authorization code for an access token</span></span>

<span data-ttu-id="09352-151">Al finalizar un usuario de la experiencia de inicio de sesión o inicio de sesión de hello, la aplicación recibirá un código de autorización de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="09352-151">After an user completes hello sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="09352-152">middleware de OWIN OpenID Connect de Hello almacenará el código de hello, pero no la intercambiar para un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="09352-152">hello OWIN OpenID Connect middleware will store hello code, but will not exchange it for an access token.</span></span> <span data-ttu-id="09352-153">Puede usar hello [biblioteca MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake exchange de Hola.</span><span class="sxs-lookup"><span data-stu-id="09352-153">You can use hello [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span></span> <span data-ttu-id="09352-154">En nuestro ejemplo, configuramos una devolución de llamada de notificación en el middleware de OpenID Connect de hello siempre que se recibe un código de autorización.</span><span class="sxs-lookup"><span data-stu-id="09352-154">In our sample, we configured a notification callback into hello OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="09352-155">En la devolución de llamada de hello, se MSAL tooexchange Hola código se utiliza un token y guardar el token de hello en la memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="09352-155">In hello callback, we use MSAL tooexchange hello code for a token and save hello token into hello cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a><span data-ttu-id="09352-156">Llamar a API web de Hola</span><span class="sxs-lookup"><span data-stu-id="09352-156">Calling hello web API</span></span>

<span data-ttu-id="09352-157">Esta sección describe cómo el token de hello toouse recibido durante la sesión-up/inicie sesión con Azure AD B2C en orden tooaccess Hola API web.</span><span class="sxs-lookup"><span data-stu-id="09352-157">This section discusses how toouse hello token received during sign-up/sign-in with Azure AD B2C in order tooaccess hello web API.</span></span>

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a><span data-ttu-id="09352-158">Recuperar el token de hello guardado en los controladores de Hola</span><span class="sxs-lookup"><span data-stu-id="09352-158">Retrieve hello saved token in hello controllers</span></span>

<span data-ttu-id="09352-159">Hola `TasksController` es responsable de comunicarse con la API web de Hola y para el envío de HTTP solicitudes toohello API tooread, crear y eliminar tareas.</span><span class="sxs-lookup"><span data-stu-id="09352-159">hello `TasksController` is responsible for communicating with hello web API and for sending HTTP requests toohello API tooread, create, and delete tasks.</span></span> <span data-ttu-id="09352-160">Como Hola API está protegida por Azure AD B2C, deberá toofirst recuperar Hola símbolo (token) que guardó en hello por encima del paso.</span><span class="sxs-lookup"><span data-stu-id="09352-160">Because hello API is secured by Azure AD B2C, you need toofirst retrieve hello token you saved in hello above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a><span data-ttu-id="09352-161">Leer tareas de API web de Hola</span><span class="sxs-lookup"><span data-stu-id="09352-161">Read tasks from hello web API</span></span>

<span data-ttu-id="09352-162">Cuando tenga un token, se puede adjuntar toohello HTTP `GET` solicitud Hola `Authorization` llamada toosecurely de encabezado `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="09352-162">When you have a token, you can attach it toohello HTTP `GET` request in hello `Authorization` header toosecurely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a><span data-ttu-id="09352-163">Crear y eliminar las tareas en API web de Hola</span><span class="sxs-lookup"><span data-stu-id="09352-163">Create and delete tasks on hello web API</span></span>

<span data-ttu-id="09352-164">Hola seguimiento mismo patrón al enviar `POST` y `DELETE` solicita toohello web API, utilizando el token de acceso MSAL tooretrieve Hola de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="09352-164">Follow hello same pattern when you send `POST` and `DELETE` requests toohello web API, using MSAL tooretrieve hello access token from hello cache.</span></span>

## <a name="run-hello-sample-app"></a><span data-ttu-id="09352-165">Ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="09352-165">Run hello sample app</span></span>

<span data-ttu-id="09352-166">Por último, compile y ejecute ambas aplicaciones Hola.</span><span class="sxs-lookup"><span data-stu-id="09352-166">Finally, build and run both hello apps.</span></span> <span data-ttu-id="09352-167">Registrarse iniciar sesión y crear tareas para el usuario que inició sesión Hola.</span><span class="sxs-lookup"><span data-stu-id="09352-167">Sign up and sign in, and create tasks for hello signed-in user.</span></span> <span data-ttu-id="09352-168">Cierre la sesión y iníciela con otro usuario diferente.</span><span class="sxs-lookup"><span data-stu-id="09352-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="09352-169">Cree tareas para ese usuario.</span><span class="sxs-lookup"><span data-stu-id="09352-169">Create tasks for that user.</span></span> <span data-ttu-id="09352-170">Observe cómo las tareas de hello almacenados por usuario en hello API, porque Hola API extrae la identidad del usuario de Hola de recibe el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="09352-170">Notice how hello tasks are stored per-user on hello API, because hello API extracts hello user's identity from hello token it receives.</span></span> <span data-ttu-id="09352-171">También intente reproducir con ámbitos Hola.</span><span class="sxs-lookup"><span data-stu-id="09352-171">Also try playing with hello scopes.</span></span> <span data-ttu-id="09352-172">Quitar el permiso de hello demasiado "escritura" y, a continuación, intente agregar una tarea.</span><span class="sxs-lookup"><span data-stu-id="09352-172">Remove hello permission too"write" and then try adding a task.</span></span> <span data-ttu-id="09352-173">Siempre que se toosign seguro out cada vez que cambie el ámbito de Hola.</span><span class="sxs-lookup"><span data-stu-id="09352-173">Just make sure toosign out each time you change hello scope.</span></span>

