---
title: aaaAzure B2C de Active Directory | Documentos de Microsoft
description: "Cómo generar perfiles toobuild una aplicación web que tiene sesión-up/inicio de sesión de, editar y restableció la contraseña mediante Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a>Creación de una aplicación web de ASP.NET con procesos de registro e inicio de sesión, edición de perfil y restablecimiento de contraseña de Azure Active Directory B2C

En este tutorial se muestra cómo realizar las siguientes acciones:

> [!div class="checklist"]
> * Agregar la aplicación web de Azure AD B2C identidad características tooyour
> * Registrar la aplicación web en el directorio de Azure AD B2C
> * Crear una directiva de registro e inicio de sesión de usuario, edición de perfil y restablecimiento de contraseña para la aplicación web

## <a name="prerequisites"></a>Requisitos previos

- Debe conectarse la tooan B2C inquilino cuenta de Azure. Puede crear una cuenta de Azure gratuita [aquí](https://azure.microsoft.com/en-us/).
- Necesita [Microsoft Visual Studio](https://www.visualstudio.com/) o un programa tooview y modificar el código de ejemplo de Hola similar.

## <a name="create-an-azure-ad-b2c-directory"></a>Creación de un directorio de Azure AD B2C

Para poder usar Azure AD B2C, debe crear un directorio o inquilino. Un directorio es un contenedor de todos los usuarios, aplicaciones, grupos, etc. Si aún no tiene uno, cree un directorio B2C antes de continuar con esta guía.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> Necesita tooconnect Hola B2C inquilino tooyour suscripción de Azure. Después de seleccionar **crear**, seleccione hello **toomy vínculo un B2C existente de AD de Azure inquilino suscripción de Azure** opción y, a continuación, en hello **inquilino de Azure AD B2C** de lista desplegable, seleccione inquilino de Hello desea tooassociate.

## <a name="create-and-register-an-application"></a>Creación y registro de una aplicación

A continuación, es necesario toocreate y registrar la aplicación hello en el directorio B2C. Esto proporciona información que Azure AD B2C necesita toosecurely comunicarse con la aplicación. 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

Cuando haya terminado, tendrá una API y una aplicación nativa en la configuración de la aplicación.

## <a name="create-policies-on-your-b2c-tenant"></a>Creación de directivas en el inquilino B2C

En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md). Este ejemplo de código contiene tres experiencias de identidad: **registro e inicio de sesión**, **edición de perfil** y **restablecimiento de contraseña**.  Deberá toocreate una directiva de cada tipo, tal y como se describe en hello [artículo de referencia de directiva](active-directory-b2c-reference-policies.md). Para cada directiva, ser seguro de atributo de nombre de visualización de tooselect Hola o notificación y toocopy hacia abajo el nombre de saludo de la directiva para su uso posterior.

### <a name="add-your-identity-providers"></a>Incorporación de sus proveedores de identidades

En la configuración, seleccione **Proveedores de identidades** y elija Registro de nombre de usuario o Registro por correo electrónico.

### <a name="create-a-sign-up-and-sign-in-policy"></a>Creación de una directiva de registro o de inicio de sesión

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a>Creación de una directiva de edición de perfil

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a>Crear una directiva de restablecimiento de contraseña

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

Después de crear las directivas, está listo toobuild la aplicación.

## <a name="download-hello-sample-code"></a>Descargar código de muestra de Hola

código de Hello para este tutorial se mantiene en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Puede clonar el ejemplo hello ejecutando:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Después de descargar el código de ejemplo de Hola, inició tooget de archivo .sln de hello abrir Visual Studio. archivo de solución de Hello contiene dos proyectos: `TaskWebApp` y `TaskService`. `TaskWebApp`es Hola aplicación web MVC que Hola usuario interactúa con. `TaskService`es la API de web back-end de la aplicación hello que almacena la lista de tareas pendientes de cada usuario. Este artículo describe solo hello `TaskWebApp` aplicación. toolearn cómo toobuild `TaskService` con Azure AD B2C, consulte [nuestro tutorial de api web de .NET](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="update-code-toouse-your-tenant-and-policies"></a>Actualizar código toouse las directivas y su inquilino

Nuestro ejemplo es toouse configurado Hola directivas e ID de cliente de nuestro inquilino de demostración. tooconnect se tooyour propio inquilino, necesita tooopen `web.config` en hello `TaskWebApp` de proyectos y Hola siguientes valores:

* `ida:Tenant` por el nombre del inquilino
* `ida:ClientId` por el identificador de la aplicación de API web
* `ida:ClientSecret` por la clave secreta de aplicación web
* `ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"
* `ida:EditProfilePolicyId` por el nombre de la directiva "Editar perfil"
* `ida:ResetPasswordPolicyId` por el nombre de la directiva "Restablecer contraseña"

## <a name="launch-hello-app"></a>Inicie la aplicación hello
Desde dentro de Visual Studio, iniciar aplicación hello. Navegar por pestaña de la lista de tareas pendientes de toohello y Hola tenga en cuenta que es la dirección URl: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...

Registrarse para la aplicación hello utilizando su nombre de usuario o la dirección de correo electrónico. Cerrar sesión, a continuación, inicie sesión de nuevo y editar el perfil de Hola o restablecer la contraseña de Hola. Cierre la sesión y iníciela con otro usuario diferente. 

## <a name="add-social-idps"></a>Agregar IDP sociales

Actualmente, la aplicación hello admite solo los usuarios registrarse e iniciar sesión mediante el uso de **cuentas locales**; cuentas almacenadas en el directorio B2C que usan un nombre de usuario y una contraseña. Con Azure AD B2C, puede agregar compatibilidad con otros **proveedores de identidades** (IDP) sin cambiar el código.

tooadd sociales IDPs tooyour aplicación, para comenzar, siga Hola detallada instrucciones que aparecen en estos artículos. Para cada IDP desea toosupport, necesita tooregister una aplicación en ese sistema y obtener un identificador de cliente.

* [Configurar Facebook como una IDP](active-directory-b2c-setup-fb-app.md)
* [Configurar Google como una IDP](active-directory-b2c-setup-goog-app.md)
* [Configurar Amazon como una IDP](active-directory-b2c-setup-amzn-app.md)
* [Configurar LinkedIn como una IDP](active-directory-b2c-setup-li-app.md)

Después de agregar tooyour de proveedores de identidad de hello directory B2C, edición de los tres directivas tooinclude Hola IDPs nueva, como se describe en hello [artículo de referencia de directiva](active-directory-b2c-reference-policies.md). Después de guardar las directivas, vuelva a ejecutar la aplicación hello.  Debería ver Hola que IDPS nueva se agregan como opciones de inicio de sesión y suscripción en cada una de sus experiencias de identidad.

Puede experimentar con las directivas y observar el efecto de hello en la aplicación de ejemplo. Agregue o quite proveedores de identidades, manipule notificaciones de aplicación o cambie atributos de registro. Experimente para ver cómo se combinan las directivas, las solicitudes de autenticación y OWIN.

## <a name="sample-code-walkthrough"></a>Tutorial de código de ejemplo
Hola las secciones siguientes muestra cómo se configura el código de aplicación de ejemplo de Hola. Puede usar dicho tutorial como guía en su futuro desarrollo de aplicaciones.

### <a name="add-authentication-support"></a>Incorporación de compatibilidad con la autenticación

Ahora puede configurar su toouse aplicación Azure AD B2C. La aplicación se comunica con Azure AD B2C mediante el envío de solicitudes de autenticación OpenID Connect. las solicitudes de Hello dictan la experiencia del usuario Hola tooexecute desea que la aplicación especificando la directiva Hola. Puede usar toosend de biblioteca de Microsoft OWIN estas solicitudes, ejecutar las directivas, administrar sesiones de usuario y mucho más.

#### <a name="install-owin"></a>Instalar OWIN

toobegin, Agregar proyecto toohello de paquetes de NuGet de middleware de hello OWIN mediante Hola consola de administrador de paquetes de Visual Studio.

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a>Agregar una clase de inicio de OWIN

Agrega una clase de inicio OWIN toohello API denominado `Startup.cs`.  Haga doble clic en el proyecto de hello, seleccione **agregar** y **nuevo elemento**y, a continuación, busque OWIN. middleware de OWIN Hola invocará hello `Configuration(…)` método cuando se inicia la aplicación.

En nuestro ejemplo, hemos cambiado declaración de clase de hello demasiado`public partial class Startup` e implementado Hola otra parte de la clase hello en `App_Start\Startup.Auth.cs`. Hola interior `Configuration` método, agregamos una llamada demasiado`ConfigureAuth`, que se define en `Startup.Auth.cs`. Después de las modificaciones de hello, `Startup.cs` Hola siguiente aspecto:

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a>Configurar el middleware de autenticación Hola

Archivo abierto hello `App_Start\Startup.Auth.cs` e implementar hello `ConfigureAuth(...)` método. Hola parámetros que se proporciona en `OpenIdConnectAuthenticationOptions` actuar como coordenadas para su toocommunicate de aplicación con Azure AD B2C. Si no especifica ciertos parámetros, usará el valor de predeterminada de Hola. Por ejemplo, no especificamos hello `ResponseType` en el ejemplo de Hola, Hola por lo que el valor predeterminado `code id_token` se utilizarán en cada tooAzure de solicitud saliente AD B2C.

También deberá tooset la autenticación de la cookie. Hola OpenID Connect middleware que usa las sesiones de usuario del toomaintain de cookies, entre otras cosas.

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

En `OpenIdConnectAuthenticationOptions` los casos anteriores, definimos un conjunto de funciones de devolución de llamada para notificaciones específicas que son recibidas por el middleware de OpenID Connect Hola. Estos comportamientos se definen mediante un `OpenIdConnectAuthenticationNotifications` objeto y almacenan en hello `Notifications` variable. En nuestro ejemplo, se definen tres devoluciones de llamada diferentes según el evento de Hola.

### <a name="using-different-policies"></a>Uso de distintas directivas

Hola `RedirectToIdentityProvider` notificación se desencadena cuando se realiza una solicitud tooAzure AD B2C. En función de devolución de llamada de hello `OnRedirectToIdentityProvider`, comprobamos Hola llamada de salida si lo deseamos toouse una directiva diferente. En orden toodo restablecer o editar un perfil de una contraseña, necesita directiva correspondiente de hello toouse como directiva en lugar de directiva de "Inicio de sesión o inicio de sesión" predeterminada Hola de restablecimiento de contraseña de Hola.

En nuestro ejemplo, cuando un usuario desea tooreset contraseña de Hola o editar el perfil de hello, agregamos directiva Hola se prefiere toouse en contexto OWIN de Hola. Esto puede realizarse mediante acciones Hola siguientes:

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

Se puede implementar la función de devolución de llamada de hello `OnRedirectToIdentityProvider` haciendo Hola siguiente:

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a>Control de códigos de autorización

Hola `AuthorizationCodeReceived` notificación se desencadena cuando se recibe un código de autorización. middleware de OpenID Connect de Hello no admite códigos de intercambio para los tokens de acceso. Puede intercambiar manualmente código de hello para el token de hello en una función de devolución de llamada. Para obtener más información, vea hello [documentación](active-directory-b2c-devquickstarts-web-api-dotnet.md) que explica cómo.

### <a name="handling-errors"></a>Control de errores

Hola `AuthenticationFailed` notificación se desencadena cuando se produce un error de autenticación. En su método de devolución de llamada, puede controlar los errores de hello como desee. Sin embargo, debe agregar una comprobación para el código de error de hello `AADB2C90118`. Durante la ejecución de Hola de directiva "Inicio de sesión o inicio de sesión" Hola, usuario de hello tiene Hola oportunidad tooselect una **¿olvidó su contraseña?** vínculo. En este caso, Azure AD B2C envía la aplicación ese código de error que indica que la aplicación realice una solicitud mediante la directiva de restablecimiento de contraseña de hello en su lugar.

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a>Enviar solicitudes de autenticación tooAzure AD

La aplicación ya está configurada correctamente toocommunicate con Azure AD B2C con el protocolo de autenticación de OpenID Connect de Hola. OWIN administra los detalles de Hola de transmitir mensajes de autenticación, validar los tokens de Azure AD B2C y mantener la sesión de usuario. Lo único que queda es tooinitiate flujo de cada usuario.

Cuando un usuario selecciona **arriba/inicio de sesión del inicio de sesión**, **Editar perfil**, o **de restablecimiento de contraseña** en la aplicación web de hello, se invoca la acción de hello asociado en `Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

También puede usar OWIN toosign usuario Hola desde la aplicación hello. En `Controllers\AccountController.cs`, tenemos:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

En suma tooexplicitly invocar una directiva, puede usar un `[Authorize]` etiqueta en los controladores que se ejecuta una directiva si el usuario de hello no ha iniciado sesión. Abra `Controllers\HomeController.cs` y agregue hello `[Authorize]` controlador de notificaciones de etiqueta toohello.  OWIN selecciona Hola última directiva que se configuró cuando hello `[Authorize]` se alcanza la etiqueta.

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a>Mostrar información de usuario

Cuando los usuarios se autentican mediante el uso de OpenID Connect, Azure AD B2C devuelve una aplicación de toohello token de identificador que contiene **notificaciones**. Estos son aserciones sobre usuario Hola. Puede usar toopersonalize de notificaciones de la aplicación.

Abra hello `Controllers\HomeController.cs` archivo. Puede tener acceso a notificaciones de usuario en los controladores a través de hello `ClaimsPrincipal.Current` objeto de entidad de seguridad.

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

Puede tener acceso a cualquier notificación que recibe la aplicación Hola igual manera.  Una lista de todas las notificaciones de hello recibe de la aplicación hello está disponible para usted en hello **notificaciones** página.
