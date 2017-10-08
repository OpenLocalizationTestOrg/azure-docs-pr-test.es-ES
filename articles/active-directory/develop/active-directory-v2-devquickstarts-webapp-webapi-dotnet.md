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
# <a name="calling-a-web-api-from-a-net-web-app"></a>Llamada a una API web desde una aplicación web .NET
Con punto de conexión de hello v2.0, puede agregar aplicaciones web de autenticación tooyour rápidamente y las API web con la compatibilidad para ambas cuentas de Microsoft personales y cuentas profesionales o educativas.  Aquí compilaremos una aplicación web MVC que inicia la sesión de los usuarios mediante OpenID Connect, con un poco de ayuda del middleware OWIN de Microsoft.  aplicación web de Hello obtener tokens de acceso de OAuth 2.0 para una web api protegida por OAuth 2.0 que permite crear, leer y eliminar en un determinado usuario "lista de tareas pendientes".

Este tutorial se centran principalmente en el uso MSAL tooacquire y usar tokens de acceso en una aplicación web, se describe en su totalidad [aquí](active-directory-v2-flows.md#web-apps).  Como los requisitos previos, puede que desee toofirst Obtenga información acerca de cómo demasiado[agregar la aplicación web de básicos tooa de inicio de sesión](active-directory-v2-devquickstarts-dotnet-web.md) o cómo demasiado[asegurar correctamente una API web](active-directory-v2-devquickstarts-dotnet-api.md).

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.  toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

## <a name="download-sample-code"></a>Descarga de código de ejemplo
código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).  toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) o esqueleto de Hola de clon:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

Como alternativa, puede [descargar la aplicación hello completado como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) o aplicación de hello completado de clon:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a>Registrar una aplicación
Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).  Asegúrese de que:

* Copia hacia abajo hello **Id. de aplicación** asignado tooyour aplicación, ya que lo necesitará pronto.
* Crear un **secreto de la aplicación** de hello **contraseña** tipo y copia hacia abajo de su valor para más tarde
* Agregar hello **Web** plataforma para la aplicación.
* Escriba Hola correcto **URI de redireccionamiento**. uri de redireccionamiento Hello indica tooAzure AD donde se deben dirigir las respuestas de autenticación: Hola predeterminado para este tutorial es `https://localhost:44326/`.

## <a name="install-owin"></a>Instalar OWIN
Agregar toohello de paquetes de NuGet de hello OWIN middleware `TodoList-WebApp` proyecto utilizando Hola Package Manager Console.  middleware de OWIN Hola ser tooissue usa las solicitudes de inicio de sesión y cierre de sesión, administrar la sesión del usuario de Hola y obtener información acerca del usuario de hello, entre otras cosas.

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a>Usuario de inicio de sesión hello en
Configurar ahora Hola Hola de toouse de middleware OWIN [protocolo de autenticación OpenID Connect](active-directory-v2-protocols.md).  

* Abra hello `web.config` archivo en la raíz de Hola de hello `TodoList-WebApp` del proyecto y escriba los valores de configuración de la aplicación Hola `<appSettings>` sección.
  * Hola `ida:ClientId` es hello **Id. de aplicación** asignado tooyour aplicación de portal de registro de hello.
  * Hola `ida:ClientSecret` es hello **secreto de la aplicación** que creó en el portal de registro de hello.
  * Hola `ida:RedirectUri` es hello **Uri de redireccionamiento** que especificó en el portal de Hola.
* Hola abierto `web.config` archivo en la raíz de Hola de hello `TodoList-Service` de proyectos y hello `ida:Audience` con Hola mismo **Id. de aplicación** como arriba.
* Archivo abierto hello `App_Start\Startup.Auth.cs` y agregue `using` instrucciones para las bibliotecas de Hola desde arriba.
* En Hola el mismo archivo, implemente hello `ConfigureAuth(...)` método.  Hola parámetros que se proporciona en `OpenIDConnectAuthenticationOptions` servirá como coordenadas para su toocommunicate de aplicación con Azure AD.

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

## <a name="use-msal-tooget-access-tokens"></a>Usar tokens de acceso MSAL tooget
Hola `AuthorizationCodeReceived` notificación, queremos toouse [OAuth 2.0, conjuntamente con OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code para un servicio de la lista de tareas pendientes de toohello token de acceso.  MSAL puede facilitarle este proceso:

* En primer lugar, instale la versión de vista previa de Hola de MSAL:

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* Y agregue otro `using` toohello instrucción `App_Start\Startup.Auth.cs` archivo para MSAL.
* Ahora agregue un nuevo método hello `OnAuthorizationCodeReceived` controlador de eventos.  Este controlador utilizará MSAL tooacquire un toohello de token de acceso a API de la lista de tareas pendientes y token de Hola se almacenará en caché de tokens de MSAL para más tarde:

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

* En las aplicaciones web, MSAL tiene una caché de tokens extensible que puede ser utilizados toostore símbolos (tokens).  Este ejemplo implementa hello `NaiveSessionCache` que usa tokens de toocache de almacenamiento de información de sesión de http.

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a>Hola llamada API de Web
Ahora es el momento tooactually usar access_token Hola adquiridos en el paso 3.  Abra hello web app `Controllers\TodoListController.cs` de archivos, lo que hace que todos los Hola CRUD solicita toohello API de la lista de tareas pendientes.

* Puede usar MSAL nuevo aquí toofetch access_tokens de Hola caché MSAL.  En primer lugar, agregue un `using` instrucción para MSAL toothis archivo.
  
    `using Microsoft.Identity.Client;`
* Hola `Index` , MSAL use la acción `AcquireTokenSilentAsync` método tooget un access_token que pueden ser datos de uso tooread de hello servicio de lista de tareas:

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

* Hello muestra, a continuación, agrega solicitud de HTTP GET resultante de token toohello hello como hello `Authorization` encabezado, qué servicio de lista de tareas pendientes de hello usa tooauthenticate solicitud de saludo.
* Si devuelve Hola servicio de lista de tareas pendientes de un `401 Unauthorized` respuesta, hello access_tokens en MSAL ya no eran válidas por algún motivo.  En este caso, debe quitar cualquier access_tokens de hello caché MSAL y mostrar un mensaje que es posible que necesiten toosign de nuevo, lo que reiniciará flujo de adquisición de tokens de Hola de usuario de Hola.

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

* De forma similar, si MSAL es no se puede tooreturn un access_token por cualquier motivo, debe indicar a hello toosign de usuario de nuevo.  Esto es tan sencillo como detectar cualquier `MSALException`:

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* Hola exactamente igual `AcquireTokenSilentAsync` llamada es implementd en hello `Create` y `Delete` acciones.  En las aplicaciones web, puede usar este access_tokens de tooget MSAL método cada vez que necesite en la aplicación.  MSAL se encargará de adquirir, almacenar en caché y actualizar tokens por usted.

Por último, compile y ejecute su aplicación.  Inicie sesión con una Account de Microsoft o una cuenta de Azure AD y observe cómo se refleja la identidad del usuario de hello en la barra de navegación superior de Hola.  Agregar y eliminar algunos elementos de lista de tareas del usuario de Hola Hola toosee que OAuth 2.0 había protegida API llama en acción.  Ahora dispone de una aplicación web y de una API web, ambas protegidas mediante protocolos estándar del sector, que pueden autenticar a los usuarios tanto con sus cuentas personales como con sus cuentas profesionales/educativas.

Como referencia, Hola completado ejemplo (sin los valores de configuración) [aquí se proporcione](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).  

## <a name="next-steps"></a>Pasos siguientes
Para obtener recursos adicionales, consulte:

* [Guía del desarrollador de Hello v2.0 >>](active-directory-appmodel-v2-overview.md)
* [Etiqueta "azure-active-directory" de StackOverflow &gt;&gt;](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Obtención de actualizaciones de seguridad para nuestros productos
Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.

