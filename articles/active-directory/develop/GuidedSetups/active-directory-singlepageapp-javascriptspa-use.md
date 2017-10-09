---
title: "aaaAzure AD v2 JS SPA configuración paso a paso: Use | Documentos de Microsoft"
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
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="a3abc-103">Use Hola biblioteca de autenticación de Microsoft (MSAL) hello toosign de usuario</span><span class="sxs-lookup"><span data-stu-id="a3abc-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="a3abc-104">Cree un archivo llamado `app.js`.</span><span class="sxs-lookup"><span data-stu-id="a3abc-104">Create a file named `app.js`.</span></span> <span data-ttu-id="a3abc-105">Si usas el proyecto de Visual Studio, seleccione hello (carpeta raíz del proyecto), haga clic en y seleccione: `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="a3abc-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="a3abc-106">Agregar Hola después código tooyour `app.js` archivo:</span><span class="sxs-lookup"><span data-stu-id="a3abc-106">Add hello following code tooyour `app.js` file:</span></span>

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
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
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
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
### <a name="more-information"></a><span data-ttu-id="a3abc-107">Más información</span><span class="sxs-lookup"><span data-stu-id="a3abc-107">More Information</span></span>

<span data-ttu-id="a3abc-108">Después de que un usuario hace clic en hello *'Llamar a las API de Graph de Microsoft'* botón para hello primera vez, `callGraphApi` llamadas al método `loginRedirect` toosign usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="a3abc-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="a3abc-109">Este método resulta en la redirección Hola usuario toohello *punto de conexión de Microsoft Azure Active Directory v2* tooprompt y validar las credenciales del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3abc-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="a3abc-110">Como resultado un correcta inicio de sesión de usuario de hello es redirigido toohello atrás original *index.html* página y un token recibido, procesa `msal.js` y se almacena en caché información de hello contenida en el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3abc-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="a3abc-111">Este token se conoce como hello *identificador de token* y contiene información básica sobre el usuario de hello, como nombre para mostrar hello usuario.</span><span class="sxs-lookup"><span data-stu-id="a3abc-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="a3abc-112">Si tiene previsto toouse todos los datos proporcionados por este token para fines, necesita toomake seguro que este token se valida su tooguarantee de servidor back-end que Hola token fue emitidos tooa usuario válido para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3abc-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="a3abc-113">Hola SPA generado por esta guía no hace que usar directamente del token de Id. de hello: en su lugar, llama a `acquireTokenSilent` o `acquireTokenRedirect` tooacquire una *token de acceso* utiliza tooquery Hola API Graph de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a3abc-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="a3abc-114">Si necesita obtener un ejemplo que valida el token de Id. de Hola, eche un vistazo en [esto](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 ejemplo") usa de ejemplo hello de aplicación de ejemplo en GitHub: una API Web de ASP.NET para la validación del token.</span><span class="sxs-lookup"><span data-stu-id="a3abc-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="a3abc-115">Obtención de un token de usuario interactivamente</span><span class="sxs-lookup"><span data-stu-id="a3abc-115">Getting a user token interactively</span></span>

<span data-ttu-id="a3abc-116">Después de hello inicial del inicio de sesión, no desea Hola pida tooreauthenticate usuarios cada vez necesitan toorequest un token tooaccess un recurso: por lo que *acquireTokenSilent* debe ser usan la mayor parte de tokens en hello tiempo tooacquire.</span><span class="sxs-lookup"><span data-stu-id="a3abc-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="a3abc-117">Hay sin embargo situaciones en las que necesita tooforce los usuarios interactúan con el punto de conexión de Azure Active Directory v2: algunos ejemplos son:</span><span class="sxs-lookup"><span data-stu-id="a3abc-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="a3abc-118">Los usuarios pueden necesitar tooreenter sus credenciales porque Hola contraseña ha expirado</span><span class="sxs-lookup"><span data-stu-id="a3abc-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="a3abc-119">La aplicación solicita recursos tooa de acceso que Hola tooconsent de necesidades de usuario para</span><span class="sxs-lookup"><span data-stu-id="a3abc-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="a3abc-120">Se requiere la autenticación en dos fases</span><span class="sxs-lookup"><span data-stu-id="a3abc-120">Two factor authentication is required</span></span>

<span data-ttu-id="a3abc-121">Hola de llamar a *acquireTokenRedirect(scope)* dar lugar a redirigir el punto de conexión de los usuarios toohello v2 de Azure Active Directory (o *acquireTokenPopup(scope)* resultado en una ventana emergente) que los usuarios necesitan toointeract con sus credenciales, confirmando cualquier dando Hola consentimiento toohello necesita recursos, o completando autenticación en dos fases Hola.</span><span class="sxs-lookup"><span data-stu-id="a3abc-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="a3abc-122">Obtención de un token de usuario en silencio</span><span class="sxs-lookup"><span data-stu-id="a3abc-122">Getting a user token silently</span></span>
<span data-ttu-id="a3abc-123">Hola ` acquireTokenSilent` método controla renovación sin ninguna interacción del usuario y adquisiciones de símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="a3abc-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="a3abc-124">Después de `loginRedirect` (o `loginPopup`) se ejecuta para hello primera vez, `acquireTokenSilent` es Hola método usada tooobtain tokens utilizados tooaccess recursos para llamadas posteriores - protegidos como llamadas toorequest o renovar los tokens se realizan en modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="a3abc-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="a3abc-125">`acquireTokenSilent`Puede producirá un error en algunos casos, por ejemplo, la contraseña del usuario de hello ha expirado.</span><span class="sxs-lookup"><span data-stu-id="a3abc-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="a3abc-126">La aplicación puede abordar esta excepción de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="a3abc-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="a3abc-127">Realizar una llamada demasiado`acquireTokenRedirect` inmediatamente, lo que produce preguntar Hola toosign de usuario en.</span><span class="sxs-lookup"><span data-stu-id="a3abc-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="a3abc-128">Este patrón es más frecuente en las aplicaciones en línea que no hay ningún contenido no autenticado en usuario de toohello disponible la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a3abc-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="a3abc-129">ejemplo de Hola generado por este programa de instalación interactiva utiliza este patrón.</span><span class="sxs-lookup"><span data-stu-id="a3abc-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="a3abc-130">Las aplicaciones también pueden realizar un usuario de toohello de indicación visual en un inicio de sesión interactivo se requiere para el usuario de hello puede seleccionar Hola momento toosign en, o puede volver a intentar la aplicación hello `acquireTokenSilent` en un momento posterior.</span><span class="sxs-lookup"><span data-stu-id="a3abc-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="a3abc-131">Esto suele utilizarse cuando el usuario de hello puede utilizar otras funciones de aplicación hello sin que se va a interrumpir; por ejemplo, hay contenido no autenticada disponibles en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a3abc-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="a3abc-132">En este caso, puede decidir usuario hello cuando quieran toosign en recursos de hello protegido tooaccess o toorefresh Hola información obsoleta.</span><span class="sxs-lookup"><span data-stu-id="a3abc-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="a3abc-133">Llamar a la API de Microsoft Graph hello mediante el símbolo (token) de hello que acabara de obtener</span><span class="sxs-lookup"><span data-stu-id="a3abc-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="a3abc-134">Agregar Hola después código tooyour `app.js` archivo:</span><span class="sxs-lookup"><span data-stu-id="a3abc-134">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
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
                        // Display response in hello page
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
                        // Display response as error in hello page
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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="a3abc-135">Más información acerca de cómo realizar una llamada de REST a una API protegida</span><span class="sxs-lookup"><span data-stu-id="a3abc-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="a3abc-136">En la aplicación de ejemplo de Hola creada por esta guía, Hola `callWebApiWithToken()` método es toomake usa HTTP `GET` solicitud para un recurso protegido que requiera un llamador de contenido toohello Hola símbolo (token) y, a continuación, vuelva.</span><span class="sxs-lookup"><span data-stu-id="a3abc-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="a3abc-137">Este método agrega el token de hello adquirido en hello *encabezado de autorización HTTP*.</span><span class="sxs-lookup"><span data-stu-id="a3abc-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="a3abc-138">Para la aplicación de ejemplo de Hola creada por esta guía, recursos de hello es hello Microsoft Graph API *me* endpoint – que muestra información de perfil del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3abc-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="a3abc-139">Agregar un toosign método usuario Hola</span><span class="sxs-lookup"><span data-stu-id="a3abc-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="a3abc-140">Agregar Hola después código tooyour `app.js` archivo:</span><span class="sxs-lookup"><span data-stu-id="a3abc-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
