---
title: "Configuración de SPA de JS en Azure AD v2: uso | Microsoft Docs"
description: "Cómo pueden llamar las aplicaciones SPA de JavaScript a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: f52157df298ddfc1c1b29a18dc9a54aae59b52a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-sign-in-the-user"></a><span data-ttu-id="29054-103">Use la biblioteca de autenticación de Microsoft (MSAL) para iniciar la sesión del usuario</span><span class="sxs-lookup"><span data-stu-id="29054-103">Use the Microsoft Authentication Library (MSAL) to sign-in the user</span></span>

1.  <span data-ttu-id="29054-104">Cree un archivo llamado `app.js`.</span><span class="sxs-lookup"><span data-stu-id="29054-104">Create a file named `app.js`.</span></span> <span data-ttu-id="29054-105">Si se usa Visual Studio, seleccione el proyecto (carpeta raíz del proyecto), haga clic con el botón derecho y seleccione: `Add` > `New Item` > `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="29054-105">If you are using Visual Studio, select the project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="29054-106">Agregue el siguiente código al archivo `app.js`:</span><span class="sxs-lookup"><span data-stu-id="29054-106">Add the following code to your `app.js` file:</span></span>

```javascript
// Graph API endpoint to show user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used to obtain the access token to read user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue to display user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call the Microsoft Graph API and display the results on the page. Sign the user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user to sign in via loginRedirect.
        // This will redirect user to the Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // The call to loginRedirect above frontloads the consent to query Graph API during the sign-in.
        // If you want to use dynamic consent, just remove the graphAPIScopes from loginRedirect call.
        // As such, user will be prompted to give consent when requested access to a resource that 
        // he/she hasn't consented before. In the case of this application - 
        // the first time the Graph API call to obtain user's profile is executed.
    } else {
        // If user is already signed in, display the user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API to show the user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order to call the Graph API, an access token needs to be acquired.
        // Try to acquire the token used to query Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After the access token is acquired, call the Web API, sending the acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If the acquireTokenSilent() method fails, then acquire the token interactively via acquireTokenRedirect().
                // In this case, the browser will redirect user back to the Azure Active Directory v2 Endpoint so the user 
                // can reenter the current username/ password and/ or give consent to new permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get the token silently, the Graph API call results will be made and results will be displayed in the page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() to show results.
 * @param {string} errorDesc - If error occur, the error message
 * @param {object} token - The token received from login
 * @param {object} error - The error string
 * @param {string} tokenType - the token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in the page
 * @param {string} endpoint - the endpoint used for the error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="29054-107">Más información</span><span class="sxs-lookup"><span data-stu-id="29054-107">More Information</span></span>

<span data-ttu-id="29054-108">Después de que un usuario hace clic en el botón *"Call Microsoft Graph API"* (Llamar a la API de Microsoft Graph) por primera vez, el método `callGraphApi` llama a `loginRedirect` para iniciar la sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="29054-108">After a user clicks the *‘Call Microsoft Graph API’* button for the first time, `callGraphApi` method calls `loginRedirect` to sign in the user.</span></span> <span data-ttu-id="29054-109">Este método hace que se redireccione al usuario al *punto de conexión de Microsoft Azure Active Directory v2* para pedir y validar las credenciales del usuario.</span><span class="sxs-lookup"><span data-stu-id="29054-109">This method results in redirecting the user to the *Microsoft Azure Active Directory v2 endpoint* to prompt and validate the user's credentials.</span></span> <span data-ttu-id="29054-110">Como resultado de un inicio de sesión correcto, se redirige al usuario a la página *index.html* original y se recibe un token, el que `msal.js` procesa, y se almacena en caché la información que contiene el token.</span><span class="sxs-lookup"><span data-stu-id="29054-110">As a result of a successful sign-in, the user is redirected back to the original *index.html* page, and a token is received, processed by `msal.js` and the information contained in the token is cached.</span></span> <span data-ttu-id="29054-111">Este token se conoce como el *token de identificador* y contiene información básica sobre el usuario, como su nombre.</span><span class="sxs-lookup"><span data-stu-id="29054-111">This token is known as the *ID token* and contains basic information about the user, such as the user display name.</span></span> <span data-ttu-id="29054-112">Si piensa utilizar los datos proporcionados por este token para algún propósito, debe asegurarse de que el servidor backend lo valide para garantizar que el token se emitió a un usuario válido para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29054-112">If you plan to use any data provided by this token for any purposes, you need to make sure this token is validated by your backend server to guarantee that the token was issued to a valid user for your application.</span></span>

<span data-ttu-id="29054-113">La instancia de SPA generada por esta guía no usa directamente el token de identificador: en su lugar, llama a `acquireTokenSilent` o a `acquireTokenRedirect` para adquirir un *token de acceso* que se usa para consultar la API de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="29054-113">The SPA generated by this guide does not make use directly of the ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` to acquire an *access token* used to query the Microsoft Graph API.</span></span> <span data-ttu-id="29054-114">Si necesita obtener un ejemplo que valide el token de identificador, eche un vistazo a [esta aplicación de ejemplo](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "ejemplo Github active-directory-javascript-singlepageapp-dotnet-webapi-v2") en GitHub (usa una ASP.NET WEB API para la validación del token).</span><span class="sxs-lookup"><span data-stu-id="29054-114">If you need a sample that validates the ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – the sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="29054-115">Obtención de un token de usuario interactivamente</span><span class="sxs-lookup"><span data-stu-id="29054-115">Getting a user token interactively</span></span>

<span data-ttu-id="29054-116">Después del inicio de sesión inicial, no desea pedirle a los usuarios que se reautentiquen cada vez que tengan que solicitar un token para acceder a un recurso, por lo que *acquireTokenSilent* se debería usar la mayor parte del tiempo para adquirir los tokens.</span><span class="sxs-lookup"><span data-stu-id="29054-116">After the initial sign-in, you do not want the ask users to reauthenticate every time they need to request a token to access a resource – so *acquireTokenSilent* should be used most of the time to acquire tokens.</span></span> <span data-ttu-id="29054-117">Sin embargo, hay situaciones en las que resulta necesario forzar a que los usuarios interactúen con el punto de conexión de Azure Active Directory v2. Algunos ejemplos de esto son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="29054-117">There are situations however that you need to force users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="29054-118">Es posible que los usuarios deban volver a escribir las credenciales porque la contraseña expiró</span><span class="sxs-lookup"><span data-stu-id="29054-118">Users may need to reenter their credentials because the password has expired</span></span>
-   <span data-ttu-id="29054-119">La aplicación solicita acceso a un recurso para el cual el usuario necesita consentimiento</span><span class="sxs-lookup"><span data-stu-id="29054-119">Your application is requesting access to a resource that the user needs to consent to</span></span>
-   <span data-ttu-id="29054-120">Se requiere la autenticación en dos fases</span><span class="sxs-lookup"><span data-stu-id="29054-120">Two factor authentication is required</span></span>

<span data-ttu-id="29054-121">Llamar a *acquireTokenRedirect(scope)* genera que se redirija a los usuarios al punto de conexión de Azure Active Directory v2 (o *acquireTokenPopup(scope)* genera una ventana emergente) donde los usuarios deben interactuar, ya sea confirmando las credenciales, dándole el consentimiento al recurso requerido o completando la autenticación en dos fases.</span><span class="sxs-lookup"><span data-stu-id="29054-121">Calling the *acquireTokenRedirect(scope)* result in redirecting users to the Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need to interact with by either confirming their credentials, giving the consent to the required resource, or completing the two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="29054-122">Obtención de un token de usuario en silencio</span><span class="sxs-lookup"><span data-stu-id="29054-122">Getting a user token silently</span></span>
<span data-ttu-id="29054-123">El método ` acquireTokenSilent` controla la renovación y las adquisiciones de tokens sin la interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="29054-123">The ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="29054-124">Después de ejecutar `loginRedirect` (o `loginPopup`) por primera vez, `acquireTokenSilent` es el método usado habitualmente para obtener los tokens empleados para acceder a recursos protegidos en las llamadas posteriores, ya que las llamadas para solicitar o renovar los tokens se realizan en modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="29054-124">After `loginRedirect` (or `loginPopup`) is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>
<span data-ttu-id="29054-125">`acquireTokenSilent` puede generar errores en algunos casos, por ejemplo, si la contraseña del usuario expiró.</span><span class="sxs-lookup"><span data-stu-id="29054-125">`acquireTokenSilent` may fail in some cases – for example, the user's password has expired.</span></span> <span data-ttu-id="29054-126">La aplicación puede abordar esta excepción de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="29054-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="29054-127">Realizar una llamada a `acquireTokenRedirect` inmediatamente, lo que ocasiona que el usuario tenga que iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="29054-127">Make a call to `acquireTokenRedirect` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="29054-128">Este patrón se da comúnmente en aplicaciones en línea en las que no hay ningún contenido no autenticado en la aplicación disponible para el usuario.</span><span class="sxs-lookup"><span data-stu-id="29054-128">This pattern is commonly used in online applications where there is no unauthenticated content in the application available to the user.</span></span> <span data-ttu-id="29054-129">El ejemplo generado por esta instalación guiada usa este patrón.</span><span class="sxs-lookup"><span data-stu-id="29054-129">The sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="29054-130">Las aplicaciones también pueden hacer una indicación visual al usuario de que se requiere un inicio de sesión interactivo, de manera que el usuario pueda seleccionar el momento adecuado para iniciar sesión, o la aplicación puede reintentar `acquireTokenSilent` en un momento posterior.</span><span class="sxs-lookup"><span data-stu-id="29054-130">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="29054-131">Esto se usa habitualmente cuando el usuario puede utilizar otras funciones de la aplicación sin que se le interrumpa: por ejemplo, hay contenido no autenticado disponible en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29054-131">This is commonly used when the user can use other functionality of the application without being disrupted - for example, there is unauthenticated content available in the application.</span></span> <span data-ttu-id="29054-132">En este caso, el usuario puede decidir cuando desea iniciar sesión para acceder al recurso protegido o para actualizar la información obsoleta.</span><span class="sxs-lookup"><span data-stu-id="29054-132">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="29054-133">Llamada a la API Graph de Microsoft con el token que acaba de obtener</span><span class="sxs-lookup"><span data-stu-id="29054-133">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="29054-134">Agregue el siguiente código al archivo `app.js`:</span><span class="sxs-lookup"><span data-stu-id="29054-134">Add the following code to your `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used to display the results
 * @param {object} showTokenElement = HTML element used to display the RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in the page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in the page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="29054-135">Más información acerca de cómo realizar una llamada de REST a una API protegida</span><span class="sxs-lookup"><span data-stu-id="29054-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="29054-136">En la aplicación de ejemplo creada en esta guía, el método `callWebApiWithToken()` se usa para realizar una solicitud HTTP `GET` a un recurso protegido que requiere un token y, a continuación, devolver el contenido al autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="29054-136">In the sample application created by this guide, the `callWebApiWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="29054-137">Este método agrega el token adquirido al *encabezado de autorización HTTP*.</span><span class="sxs-lookup"><span data-stu-id="29054-137">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="29054-138">En este ejemplo de aplicación creada en esta guía, el recurso es el punto de conexión *me* de Microsoft Graph API, que muestra información del perfil del usuario.</span><span class="sxs-lookup"><span data-stu-id="29054-138">For the sample application created by this guide, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-to-sign-out-the-user"></a><span data-ttu-id="29054-139">Adición de un método para cerrar la sesión del usuario</span><span class="sxs-lookup"><span data-stu-id="29054-139">Add a method to sign out the user</span></span>

<span data-ttu-id="29054-140">Agregue el siguiente código al archivo `app.js`:</span><span class="sxs-lookup"><span data-stu-id="29054-140">Add the following code to your `app.js` file:</span></span>

```javascript
/**
 * Sign-out the user
 */
function signOut() {
    userAgentApplication.logout();
}
```
