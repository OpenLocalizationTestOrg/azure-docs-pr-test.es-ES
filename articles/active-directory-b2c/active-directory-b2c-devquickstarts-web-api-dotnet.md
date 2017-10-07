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
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a>Azure AD B2C: llamada a una API web de .NET desde una aplic. web de .NET

Mediante el uso de Azure AD B2C, puede agregar aplicaciones web de identidad eficaz administración características tooyour y las API web. Este artículo describe cómo toorequest tokens de acceso y realizar llamadas desde una "lista de tareas pendientes" de .NET tooa de aplicación web .NET web api.

En este artículo no cubre cómo tooimplement sesión, inicio de sesión y el perfil de administración con Azure AD B2C. Se centra en las API de web que realiza la llamada después de hello usuario ya está autenticado. Si todavía no lo ha hecho, debe hacer lo siguiente:

* Comenzar a trabajar con una [aplicación web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
* Comenzar a trabajar con una [API web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)

## <a name="prerequisite"></a>Requisito previo

toobuild una aplicación web que llama a una web api, necesita:

1. [Crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).
2. [Registrar una API web](active-directory-b2c-app-registration.md#register-a-web-api).
3. [Registrar una aplicación web](active-directory-b2c-app-registration.md#register-a-web-app).
4. [Configurar directivas](active-directory-b2c-reference-policies.md).
5. [GRANT Hola web app permisos toouse Hola web api](active-directory-b2c-access-tokens.md#publishing-permissions).

> [!IMPORTANT]
> aplicación de cliente de Hello y API web deben usar directorio de hello misma instancia de Azure AD B2C.
>

## <a name="download-hello-code"></a>Descargar código de hello

código de Hello para este tutorial se mantiene en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Puede clonar el ejemplo hello ejecutando:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Después de descargar el código de ejemplo de Hola, inició tooget de archivo .sln de hello abrir Visual Studio. archivo de solución de Hello contiene dos proyectos: `TaskWebApp` y `TaskService`. `TaskWebApp`es una aplicación web MVC que Hola usuario interactúa con. `TaskService`es la API de web back-end de la aplicación hello que almacena la lista de tareas pendientes de cada usuario. En este artículo no cubre creación hello `TaskWebApp` aplicación web o hello `TaskService` web api. toolearn cómo toobuild Hola .NET web aplicación con Azure AD B2C, consulte nuestro [tutorial de aplicación web de .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md). toolearn cómo toobuild Hola .NET web API protegida con Azure AD B2C, consulte nuestro [tutorial de API web de .NET](active-directory-b2c-devquickstarts-api-dotnet.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Actualizar configuración de hello Azure AD B2C

Nuestro ejemplo es toouse configurado Hola directivas e ID de cliente de nuestro inquilino de demostración. Si desea que toouse su propio inquilino:

1. Abra `web.config` en hello `TaskService` de proyectos y valores de hello para

    * `ida:Tenant` por el nombre del inquilino
    * `ida:ClientId` por el identificador de la aplicación de API web
    * `ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"

2. Abra `web.config` en hello `TaskWebApp` de proyectos y valores de hello para

    * `ida:Tenant` por el nombre del inquilino
    * `ida:ClientId` por el identificador de la aplicación de API web
    * `ida:ClientSecret` por la clave secreta de aplicación web
    * `ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"
    * `ida:EditProfilePolicyId` por el nombre de la directiva "Editar perfil"
    * `ida:ResetPasswordPolicyId` por el nombre de la directiva "Restablecer contraseña"



## <a name="requesting-and-saving-an-access-token"></a>Solicitud y guardado de un token de acceso

### <a name="specify-hello-permissions"></a>Especificar permisos de Hola

En orden toomake Hola llamada toohello API web, necesita tooauthenticate Hola usuario (mediante la directiva de inicio de sesión-up/inicio de sesión de) y [recibir un token de acceso](active-directory-b2c-access-tokens.md) de Azure AD B2C. En orden tooreceive un token de acceso, primero debe especificar permisos de hello le gustaría toogrant de token de acceso de Hola. los permisos de Hola se especifican en hello `scope` parámetro al realizar Hola solicitud toohello `/authorize` punto de conexión. Por ejemplo, tooacquire aplicación de recursos de toohello de permiso que tiene un token de acceso con hello "lectura" Hola App ID URI de `https://contoso.onmicrosoft.com/tasks`, ámbito Hola sería `https://contoso.onmicrosoft.com/tasks/read`.

ámbito de hello toospecify en nuestro archivo de ejemplo, abra hello `App_Start\Startup.Auth.cs` y definir hello `Scope` variable OpenIdConnectAuthenticationOptions.

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

### <a name="exchange-hello-authorization-code-for-an-access-token"></a>Código de autorización de Hola para un token de acceso de Exchange

Al finalizar un usuario de la experiencia de inicio de sesión o inicio de sesión de hello, la aplicación recibirá un código de autorización de Azure AD B2C. middleware de OWIN OpenID Connect de Hello almacenará el código de hello, pero no la intercambiar para un token de acceso. Puede usar hello [biblioteca MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake exchange de Hola. En nuestro ejemplo, configuramos una devolución de llamada de notificación en el middleware de OpenID Connect de hello siempre que se recibe un código de autorización. En la devolución de llamada de hello, se MSAL tooexchange Hola código se utiliza un token y guardar el token de hello en la memoria caché de Hola.

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

## <a name="calling-hello-web-api"></a>Llamar a API web de Hola

Esta sección describe cómo el token de hello toouse recibido durante la sesión-up/inicie sesión con Azure AD B2C en orden tooaccess Hola API web.

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a>Recuperar el token de hello guardado en los controladores de Hola

Hola `TasksController` es responsable de comunicarse con la API web de Hola y para el envío de HTTP solicitudes toohello API tooread, crear y eliminar tareas. Como Hola API está protegida por Azure AD B2C, deberá toofirst recuperar Hola símbolo (token) que guardó en hello por encima del paso.

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

### <a name="read-tasks-from-hello-web-api"></a>Leer tareas de API web de Hola

Cuando tenga un token, se puede adjuntar toohello HTTP `GET` solicitud Hola `Authorization` llamada toosecurely de encabezado `TaskService`:

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

### <a name="create-and-delete-tasks-on-hello-web-api"></a>Crear y eliminar las tareas en API web de Hola

Hola seguimiento mismo patrón al enviar `POST` y `DELETE` solicita toohello web API, utilizando el token de acceso MSAL tooretrieve Hola de caché de Hola.

## <a name="run-hello-sample-app"></a>Ejecutar la aplicación de ejemplo de Hola

Por último, compile y ejecute ambas aplicaciones Hola. Registrarse iniciar sesión y crear tareas para el usuario que inició sesión Hola. Cierre la sesión y iníciela con otro usuario diferente. Cree tareas para ese usuario. Observe cómo las tareas de hello almacenados por usuario en hello API, porque Hola API extrae la identidad del usuario de Hola de recibe el token de Hola. También intente reproducir con ámbitos Hola. Quitar el permiso de hello demasiado "escritura" y, a continuación, intente agregar una tarea. Siempre que se toosign seguro out cada vez que cambie el ámbito de Hola.

