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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>Use Hola biblioteca de autenticación de Microsoft (MSAL) hello toosign de usuario

1.  Cree un archivo llamado `app.js`. Si usas el proyecto de Visual Studio, seleccione hello (carpeta raíz del proyecto), haga clic en y seleccione: `Add`  >  `New Item`  >  `JavaScript File`:
2.  Agregar Hola después código tooyour `app.js` archivo:

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
### <a name="more-information"></a>Más información

Después de que un usuario hace clic en hello *'Llamar a las API de Graph de Microsoft'* botón para hello primera vez, `callGraphApi` llamadas al método `loginRedirect` toosign usuario Hola. Este método resulta en la redirección Hola usuario toohello *punto de conexión de Microsoft Azure Active Directory v2* tooprompt y validar las credenciales del usuario de Hola. Como resultado un correcta inicio de sesión de usuario de hello es redirigido toohello atrás original *index.html* página y un token recibido, procesa `msal.js` y se almacena en caché información de hello contenida en el token de Hola. Este token se conoce como hello *identificador de token* y contiene información básica sobre el usuario de hello, como nombre para mostrar hello usuario. Si tiene previsto toouse todos los datos proporcionados por este token para fines, necesita toomake seguro que este token se valida su tooguarantee de servidor back-end que Hola token fue emitidos tooa usuario válido para la aplicación.

Hola SPA generado por esta guía no hace que usar directamente del token de Id. de hello: en su lugar, llama a `acquireTokenSilent` o `acquireTokenRedirect` tooacquire una *token de acceso* utiliza tooquery Hola API Graph de Microsoft. Si necesita obtener un ejemplo que valida el token de Id. de Hola, eche un vistazo en [esto](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 ejemplo") usa de ejemplo hello de aplicación de ejemplo en GitHub: una API Web de ASP.NET para la validación del token.

#### <a name="getting-a-user-token-interactively"></a>Obtención de un token de usuario interactivamente

Después de hello inicial del inicio de sesión, no desea Hola pida tooreauthenticate usuarios cada vez necesitan toorequest un token tooaccess un recurso: por lo que *acquireTokenSilent* debe ser usan la mayor parte de tokens en hello tiempo tooacquire. Hay sin embargo situaciones en las que necesita tooforce los usuarios interactúan con el punto de conexión de Azure Active Directory v2: algunos ejemplos son:
-   Los usuarios pueden necesitar tooreenter sus credenciales porque Hola contraseña ha expirado
-   La aplicación solicita recursos tooa de acceso que Hola tooconsent de necesidades de usuario para
-   Se requiere la autenticación en dos fases

Hola de llamar a *acquireTokenRedirect(scope)* dar lugar a redirigir el punto de conexión de los usuarios toohello v2 de Azure Active Directory (o *acquireTokenPopup(scope)* resultado en una ventana emergente) que los usuarios necesitan toointeract con sus credenciales, confirmando cualquier dando Hola consentimiento toohello necesita recursos, o completando autenticación en dos fases Hola.

#### <a name="getting-a-user-token-silently"></a>Obtención de un token de usuario en silencio
Hola ` acquireTokenSilent` método controla renovación sin ninguna interacción del usuario y adquisiciones de símbolo (token). Después de `loginRedirect` (o `loginPopup`) se ejecuta para hello primera vez, `acquireTokenSilent` es Hola método usada tooobtain tokens utilizados tooaccess recursos para llamadas posteriores - protegidos como llamadas toorequest o renovar los tokens se realizan en modo silencioso.
`acquireTokenSilent`Puede producirá un error en algunos casos, por ejemplo, la contraseña del usuario de hello ha expirado. La aplicación puede abordar esta excepción de dos maneras:

1.  Realizar una llamada demasiado`acquireTokenRedirect` inmediatamente, lo que produce preguntar Hola toosign de usuario en. Este patrón es más frecuente en las aplicaciones en línea que no hay ningún contenido no autenticado en usuario de toohello disponible la aplicación hello. ejemplo de Hola generado por este programa de instalación interactiva utiliza este patrón.

2. Las aplicaciones también pueden realizar un usuario de toohello de indicación visual en un inicio de sesión interactivo se requiere para el usuario de hello puede seleccionar Hola momento toosign en, o puede volver a intentar la aplicación hello `acquireTokenSilent` en un momento posterior. Esto suele utilizarse cuando el usuario de hello puede utilizar otras funciones de aplicación hello sin que se va a interrumpir; por ejemplo, hay contenido no autenticada disponibles en la aplicación hello. En este caso, puede decidir usuario hello cuando quieran toosign en recursos de hello protegido tooaccess o toorefresh Hola información obsoleta.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Llamar a la API de Microsoft Graph hello mediante el símbolo (token) de hello que acabara de obtener

Agregar Hola después código tooyour `app.js` archivo:

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Más información acerca de cómo realizar una llamada de REST a una API protegida

En la aplicación de ejemplo de Hola creada por esta guía, Hola `callWebApiWithToken()` método es toomake usa HTTP `GET` solicitud para un recurso protegido que requiera un llamador de contenido toohello Hola símbolo (token) y, a continuación, vuelva. Este método agrega el token de hello adquirido en hello *encabezado de autorización HTTP*. Para la aplicación de ejemplo de Hola creada por esta guía, recursos de hello es hello Microsoft Graph API *me* endpoint – que muestra información de perfil del usuario de Hola.

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Agregar un toosign método usuario Hola

Agregar Hola después código tooyour `app.js` archivo:

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
