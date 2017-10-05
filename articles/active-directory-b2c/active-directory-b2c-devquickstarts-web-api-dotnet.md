---
title: Azure Active Directory B2C | Microsoft Docs
description: "Creación de una aplic. web de .NET y llamada a una API web con Azure Active Directory B2C y tokens de acceso de OAuth 2.0."
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
ms.openlocfilehash: 48452eb68f826d1c7aa61d5e5531f941ac1422b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="800bf-103">Azure AD B2C: llamada a una API web de .NET desde una aplic. web de .NET</span><span class="sxs-lookup"><span data-stu-id="800bf-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="800bf-104">Con Azure AD B2C, puede agregar características eficaces de administración de identidades a las aplicaciones web y las API web.</span><span class="sxs-lookup"><span data-stu-id="800bf-104">By using Azure AD B2C, you can add powerful identity management features to your web apps and web APIs.</span></span> <span data-ttu-id="800bf-105">En este artículo se describe cómo solicitar tokens de acceso y hacer llamadas desde una aplic. web de "tareas pendientes" .NET a una API web de .NET.</span><span class="sxs-lookup"><span data-stu-id="800bf-105">This article discusses how to request access tokens and make calls from a .NET "to-do list" web app to a .NET web api.</span></span>

<span data-ttu-id="800bf-106">Este artículo no trata de la implementación de la administración de registros, inicios de sesión y perfiles con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="800bf-106">This article does not cover how to implement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="800bf-107">Se centra en la llamada a las API web después de que el usuario ya está autenticado.</span><span class="sxs-lookup"><span data-stu-id="800bf-107">It focuses on calling web APIs after the user is already authenticated.</span></span> <span data-ttu-id="800bf-108">Si todavía no lo ha hecho, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="800bf-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="800bf-109">Comenzar a trabajar con una [aplicación web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="800bf-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="800bf-110">Comenzar a trabajar con una [API web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="800bf-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="800bf-111">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="800bf-111">Prerequisite</span></span>

<span data-ttu-id="800bf-112">Para crear una aplicación web que llama a una API web, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="800bf-112">To build a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="800bf-113">[Crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="800bf-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="800bf-114">[Registrar una API web](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="800bf-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="800bf-115">[Registrar una aplicación web](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="800bf-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="800bf-116">[Configurar directivas](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="800bf-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="800bf-117">[Conceder a la aplicación web permisos para usar la API web](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="800bf-117">[Grant the web app permissions to use the web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="800bf-118">La API de web y la aplicación de cliente deben usar el mismo directorio de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="800bf-118">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="download-the-code"></a><span data-ttu-id="800bf-119">Descargar el código</span><span class="sxs-lookup"><span data-stu-id="800bf-119">Download the code</span></span>

<span data-ttu-id="800bf-120">El código de este tutorial se conserva [en GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="800bf-120">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="800bf-121">Puede clonar el ejemplo al ejecutar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="800bf-121">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="800bf-122">Una vez descargado el código de ejemplo, abra el archivo .sln de Visual Studio para empezar.</span><span class="sxs-lookup"><span data-stu-id="800bf-122">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="800bf-123">El archivo de solución contiene dos proyectos: `TaskWebApp` y `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="800bf-123">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="800bf-124">`TaskWebApp` es una aplicación web MVC con la que el usuario interactúa.</span><span class="sxs-lookup"><span data-stu-id="800bf-124">`TaskWebApp` is a MVC web application that the user interacts with.</span></span> <span data-ttu-id="800bf-125">`TaskService` es la API web del back-end de la aplicación que almacena la lista de tareas pendientes de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="800bf-125">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="800bf-126">En este artículo no se incluye la creación de la aplicación web `TaskWebApp` ni de la API web `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="800bf-126">This article does not cover building the `TaskWebApp` web app or the `TaskService` web api.</span></span> <span data-ttu-id="800bf-127">Para información sobre cómo crear la aplicación web .NET con Azure AD B2C, consulte el [tutorial de aplicación web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="800bf-127">To learn how to build the .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="800bf-128">Para información sobre cómo crear la API web .NET protegida con Azure AD B2C, consulte el [tutorial de API web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="800bf-128">To learn how to build the .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="800bf-129">Actualización de la configuración de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="800bf-129">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="800bf-130">Nuestro ejemplo está configurado para usar las directivas y el identificador de cliente de nuestro inquilino de demostración.</span><span class="sxs-lookup"><span data-stu-id="800bf-130">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="800bf-131">Si desea usar su propio inquilino:</span><span class="sxs-lookup"><span data-stu-id="800bf-131">If you would like to use your own tenant:</span></span>

1. <span data-ttu-id="800bf-132">Abra `web.config` en el proyecto `TaskService` y reemplace los valores de</span><span class="sxs-lookup"><span data-stu-id="800bf-132">Open `web.config` in the `TaskService` project and replace the values for</span></span>

    * <span data-ttu-id="800bf-133">`ida:Tenant` por el nombre del inquilino</span><span class="sxs-lookup"><span data-stu-id="800bf-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="800bf-134">`ida:ClientId` por el identificador de la aplicación de API web</span><span class="sxs-lookup"><span data-stu-id="800bf-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="800bf-135">`ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"</span><span class="sxs-lookup"><span data-stu-id="800bf-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="800bf-136">Abra `web.config` en el proyecto `TaskWebApp` y reemplace los valores de</span><span class="sxs-lookup"><span data-stu-id="800bf-136">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>

    * <span data-ttu-id="800bf-137">`ida:Tenant` por el nombre del inquilino</span><span class="sxs-lookup"><span data-stu-id="800bf-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="800bf-138">`ida:ClientId` por el identificador de la aplicación de API web</span><span class="sxs-lookup"><span data-stu-id="800bf-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="800bf-139">`ida:ClientSecret` por la clave secreta de aplicación web</span><span class="sxs-lookup"><span data-stu-id="800bf-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="800bf-140">`ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"</span><span class="sxs-lookup"><span data-stu-id="800bf-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="800bf-141">`ida:EditProfilePolicyId` por el nombre de la directiva "Editar perfil"</span><span class="sxs-lookup"><span data-stu-id="800bf-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="800bf-142">`ida:ResetPasswordPolicyId` por el nombre de la directiva "Restablecer contraseña"</span><span class="sxs-lookup"><span data-stu-id="800bf-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="800bf-143">Solicitud y guardado de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="800bf-143">Requesting and saving an access token</span></span>

### <a name="specify-the-permissions"></a><span data-ttu-id="800bf-144">Especificación de los permisos</span><span class="sxs-lookup"><span data-stu-id="800bf-144">Specify the permissions</span></span>

<span data-ttu-id="800bf-145">Para realizar la llamada a la API web, deberá autenticar el usuario (con la directiva de registro o inicio de sesión) y [recibir un token de acceso](active-directory-b2c-access-tokens.md) de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="800bf-145">In order to make the call to the web API, you need to authenticate the user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="800bf-146">Para recibir un token de acceso, primero debe especificar los permisos que le gustaría que concediera el token de acceso.</span><span class="sxs-lookup"><span data-stu-id="800bf-146">In order to receive an access token, you first must specify the permissions you would like the access token to grant.</span></span> <span data-ttu-id="800bf-147">Los parámetros se especifican en el parámetro `scope` cuando hace la solicitud al punto de conexión `/authorize`.</span><span class="sxs-lookup"><span data-stu-id="800bf-147">The permissions are specified in the `scope` parameter when you make the request to the `/authorize` endpoint.</span></span> <span data-ttu-id="800bf-148">Por ejemplo, para adquirir un token de acceso con el permiso de "lectura" a la aplicación de recursos que tiene el URI de id. de aplicación de `https://contoso.onmicrosoft.com/tasks`, el ámbito sería `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="800bf-148">For example, to acquire an access token with the “read” permission to the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/tasks`, the scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="800bf-149">Para especificar el ámbito del ejemplo, abra el archivo `App_Start\Startup.Auth.cs` y defina la variable `Scope` en OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="800bf-149">To specify the scope in our sample, open the file `App_Start\Startup.Auth.cs` and define the `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-the-authorization-code-for-an-access-token"></a><span data-ttu-id="800bf-150">Intercambio del código de autorización por un token de acceso</span><span class="sxs-lookup"><span data-stu-id="800bf-150">Exchange the authorization code for an access token</span></span>

<span data-ttu-id="800bf-151">Después de que un usuario completa la experiencia de registro o inicio de sesión, la aplicación recibirá un código de autorización de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="800bf-151">After an user completes the sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="800bf-152">El middleware de OpenID Connect de OWIN almacenará el código, pero no lo intercambiará por un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="800bf-152">The OWIN OpenID Connect middleware will store the code, but will not exchange it for an access token.</span></span> <span data-ttu-id="800bf-153">Puede usar la [biblioteca de MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) para hacer el intercambio.</span><span class="sxs-lookup"><span data-stu-id="800bf-153">You can use the [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) to make the exchange.</span></span> <span data-ttu-id="800bf-154">En el ejemplo, configuramos una devolución de llamada de notificación en el middleware de OpenID Connect para cada vez que se reciba un código de autorización.</span><span class="sxs-lookup"><span data-stu-id="800bf-154">In our sample, we configured a notification callback into the OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="800bf-155">En la devolución de llamada, usamos MSAL para intercambiar el código por un token y guardar el token en la caché.</span><span class="sxs-lookup"><span data-stu-id="800bf-155">In the callback, we use MSAL to exchange the code for a token and save the token into the cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract the code from the response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange the code for a token. Make sure to specify the necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-the-web-api"></a><span data-ttu-id="800bf-156">Llamada a la API web</span><span class="sxs-lookup"><span data-stu-id="800bf-156">Calling the web API</span></span>

<span data-ttu-id="800bf-157">En esta sección se describe cómo usar el token recibido durante el registro o el inicio de sesión con Azure AD B2C para tener acceso a la API web.</span><span class="sxs-lookup"><span data-stu-id="800bf-157">This section discusses how to use the token received during sign-up/sign-in with Azure AD B2C in order to access the web API.</span></span>

### <a name="retrieve-the-saved-token-in-the-controllers"></a><span data-ttu-id="800bf-158">Recuperación del token guardado en los controladores</span><span class="sxs-lookup"><span data-stu-id="800bf-158">Retrieve the saved token in the controllers</span></span>

<span data-ttu-id="800bf-159">`TasksController` es responsable de comunicarse con la API web y de enviar solicitudes HTTP a la API para leer, crear y eliminar tareas.</span><span class="sxs-lookup"><span data-stu-id="800bf-159">The `TasksController` is responsible for communicating with the web API and for sending HTTP requests to the API to read, create, and delete tasks.</span></span> <span data-ttu-id="800bf-160">Debido a que la API está protegida por Azure AD B2C, debe recuperar primero el token que guardó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="800bf-160">Because the API is secured by Azure AD B2C, you need to first retrieve the token you saved in the above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL to retrieve the token from the cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve the token using the provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-the-web-api"></a><span data-ttu-id="800bf-161">Leer tareas de la API web</span><span class="sxs-lookup"><span data-stu-id="800bf-161">Read tasks from the web API</span></span>

<span data-ttu-id="800bf-162">Cuando tenga un token, puede adjuntarlo a la solicitud `GET` HTTP en el encabezado `Authorization` para llamar de forma segura a `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="800bf-162">When you have a token, you can attach it to the HTTP `GET` request in the `Authorization` header to securely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve the token with the specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token to the Authorization header and make the request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-the-web-api"></a><span data-ttu-id="800bf-163">Creación y eliminación de tareas de la API web</span><span class="sxs-lookup"><span data-stu-id="800bf-163">Create and delete tasks on the web API</span></span>

<span data-ttu-id="800bf-164">Siga el mismo patrón al enviar las solicitudes `POST` y `DELETE` a la API web, mediante el uso de MSAL para recuperar el token de acceso desde la caché.</span><span class="sxs-lookup"><span data-stu-id="800bf-164">Follow the same pattern when you send `POST` and `DELETE` requests to the web API, using MSAL to retrieve the access token from the cache.</span></span>

## <a name="run-the-sample-app"></a><span data-ttu-id="800bf-165">Ejecutar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="800bf-165">Run the sample app</span></span>

<span data-ttu-id="800bf-166">Por último, compile y ejecute ambas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="800bf-166">Finally, build and run both the apps.</span></span> <span data-ttu-id="800bf-167">Regístrese o inicie sesión en la aplicación y cree tareas para el usuario que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="800bf-167">Sign up and sign in, and create tasks for the signed-in user.</span></span> <span data-ttu-id="800bf-168">Cierre la sesión y iníciela con otro usuario diferente.</span><span class="sxs-lookup"><span data-stu-id="800bf-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="800bf-169">Cree tareas para ese usuario.</span><span class="sxs-lookup"><span data-stu-id="800bf-169">Create tasks for that user.</span></span> <span data-ttu-id="800bf-170">Observe cómo se almacenan las tareas por usuario en la API, puesto que la API extrae la identidad del usuario del token que recibe.</span><span class="sxs-lookup"><span data-stu-id="800bf-170">Notice how the tasks are stored per-user on the API, because the API extracts the user's identity from the token it receives.</span></span> <span data-ttu-id="800bf-171">Intente también jugar con los ámbitos.</span><span class="sxs-lookup"><span data-stu-id="800bf-171">Also try playing with the scopes.</span></span> <span data-ttu-id="800bf-172">Quite el permiso para "escribir" y, luego, intente agregar una tarea.</span><span class="sxs-lookup"><span data-stu-id="800bf-172">Remove the permission to "write" and then try adding a task.</span></span> <span data-ttu-id="800bf-173">Solo debe asegurarse de cerrar sesión cada vez que cambia el ámbito.</span><span class="sxs-lookup"><span data-stu-id="800bf-173">Just make sure to sign out each time you change the scope.</span></span>

