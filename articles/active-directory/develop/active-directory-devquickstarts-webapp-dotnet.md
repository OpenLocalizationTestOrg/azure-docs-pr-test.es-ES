---
title: "aplicación web de .NET de aaaAzure AD Introducción | Documentos de Microsoft"
description: "Creación de una aplicación web de .NET MVC que se integra con Azure AD para el inicio de sesión."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a>Inicio y cierre de sesión de la aplicación web de ASP.NET con Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Al proporcionar un único inicio de sesión y cierre de sesión con unas pocas líneas de código, Azure Active Directory (Azure AD) simplifica toooutsource aplicación web administración de identidades. Puede iniciar sesión a los usuarios dentro y fuera de las aplicaciones web ASP.NET mediante la implementación de Microsoft de Hola de interfaz Web abierta para el middleware de .NET (OWIN). El middleware OWIN controlado por la comunidad se incluye en .NET Framework 4.5. Este artículo se muestra cómo toouse OWIN para:

* Usuarios de inicio de sesión en tooweb aplicaciones con Azure AD como proveedor de identidades de Hola.
* Mostrar información del usuario.
* Usuarios de inicio de sesión de aplicaciones de Hola.

## <a name="before-you-get-started"></a>Antes de comenzar
* Descargar hello [esqueleto aplicación](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) o descargar hello [ejemplo completo](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).
* También necesita a un inquilino de Azure AD en qué aplicación de hello tooregister. Si aún no tiene un inquilino de Azure AD, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).

Cuando esté listo, siga los procedimientos de hello en Hola cuatro secciones siguientes.

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>Paso 1: Registrar Hola nueva aplicación con Azure AD
tooset configurar usuarios de tooauthenticate de aplicación Hola, registra por primera vez en el inquilino haciendo Hola siguiente:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en el nombre de cuenta. En hello **Directory** inquilinos de Active Directory de hello seleccione donde desea que la aplicación de hello tooregister, la lista.
3. Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.
5. Siga Hola solicita toocreate un nuevo **aplicación Web o WebAPI**.
  * **Nombre** describe hello toousers de aplicación.
  * **Dirección URL de inicio de sesión** es Hola dirección URL base de la aplicación hello. dirección URL de predeterminada del esqueleto Hello es https://localhost:44320 /.
6. Después de haber completado el registro de hello, Azure AD le asigna aplicación hello un identificador de aplicación único. Copiar valor de Hola de hello toouse de página de aplicación en las secciones siguientes se Hola.
7. De hello **configuración** -> **propiedades** página de la aplicación, actualice Hola App ID URI. Hola **App ID URI** es un identificador único para la aplicación hello. Hello convención de nomenclatura es `https://<tenant-domain>/<app-name>` (por ejemplo, `https://contoso.onmicrosoft.com/my-first-aad-app`).

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Paso 2: Configurar la canalización de autenticación de hello aplicación toouse hello OWIN
En este paso, configurará hello OWIN middleware toouse Hola OpenID Connect protocolo de autenticación. Usar las solicitudes de inicio de sesión y cierre de sesión de tooissue OWIN, administrar sesiones de usuario, obtener información de usuario y así sucesivamente.

1. toobegin, Agregar proyecto toohello de paquetes de NuGet de middleware de hello OWIN mediante el uso de la consola de administrador de paquetes de saludo.

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. tooadd llama a un proyecto de inicio de OWIN clase toohello `Startup.cs`, haga clic en proyecto de hello, seleccione **agregar**, seleccione **nuevo elemento**y, a continuación, busque **OWIN**. middleware de OWIN Hola invoca hello **Configuration(...)**  método cuando se inicia la aplicación hello.
3. Cambie la declaración de clase de hello demasiado`public partial class Startup`. Ya hemos implementado parte de esta clase en otro archivo. Hola **Configuration(...)**  método, realizar una llamada demasiado**ConfgureAuth(...)**  tooset la autenticación para aplicación hello.  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. Abra el archivo de App_Start\Startup.Auth.cs hello y luego implementar hello **ConfigureAuth(...)**  (método). Hola parámetros que se proporciona en *OpenIDConnectAuthenticationOptions* actuar como coordenadas de hello toocommunicate de aplicación con Azure AD. También deberá tooset la autenticación con cookies, porque Hola OpenID Connect middleware utiliza cookies en segundo plano de Hola.

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. Abrir el archivo web.config de hello en raíz de hello del proyecto de hello y, a continuación, escriba los valores de configuración de Hola Hola `<appSettings>` sección.
  * `ida:ClientId`: Hola GUID que copió de hello portal de Azure en "paso 1: registrar Hola nueva aplicación con Azure AD."
  * `ida:Tenant`: nombre de hello del inquilino de Azure AD (por ejemplo, contoso.onmicrosoft.com).
  * `ida:PostLogoutRedirectUri`: indicador de Hola que indica a Azure AD que se debe redirigir un usuario después de una solicitud de cierre de sesión se ha completado correctamente.

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Paso 3: Usar OWIN tooissue inicio de sesión y cierre de sesión solicita tooAzure AD
aplicación Hello ahora es toocommunicate configurada correctamente con Azure AD mediante el protocolo de autenticación de OpenID Connect de Hola. OWIN ha controlado todos los detalles de Hola de transmitir mensajes de autenticación, validar los tokens de Azure AD y mantener las sesiones de usuario. Lo único que queda es toogive a los usuarios una manera toosign en y cierre de sesión.

1. Puede usar autorizar su toosign de usuarios toorequire de controladores en las etiquetas para acceder a determinadas páginas. toodo por lo tanto, abra controllers\homecontroller y, a continuación, agregue hello `[Authorize]` etiqueta toohello sobre el controlador.

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. También puede usar solicitudes de autenticación OWIN toodirectly problema desde dentro del código. toodo, abra Controllers\AccountController.cs. A continuación, en acciones de SignIn() y SignOut() de hello, emitir desafío OpenID Connect y solicitudes de cierre de sesión.

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. Abra Views\Shared\_LoginPartial.cshtml tooshow Hola usuario Hola aplicación inicio de sesión y cierre de sesión vínculos y tooprint el nombre del usuario de hello en una vista.

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
             </li>
             <li>
                 @Html.ActionLink("Sign out", "SignOut", "Account")
             </li>
         </ul>
     </text>
    }
    else
    {
     <ul class="nav navbar-nav navbar-right">
         <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
     </ul>
    }
    ```

## <a name="step-4-display-user-information"></a>Paso 4: Visualización de la información del usuario
Cuando autentica a los usuarios con OpenID Connect, Azure AD devuelve una aplicación de toohello id_token que contiene "notificaciones", o aserciones sobre usuario Hola. Puede usar estas aplicaciones de notificaciones toopersonalize Hola haciendo Hola siguiente:

1. Abra el archivo controllers\homecontroller. cs de Hola. Puede tener acceso a solicitudes del usuario de hello en los controladores a través de hello `ClaimsPrincipal.Current` objeto de entidad de seguridad.

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. Compile y ejecute la aplicación hello. Si aún no ha creado un nuevo usuario en el inquilino con un dominio de onmicrosoft.com, ahora es Hola tiempo toodo para. Este es el procedimiento:

  a. Inicie sesión con ese usuario y tenga en cuenta cómo se refleja la identidad del usuario de hello en la barra superior Hola.

  b. Cierre la sesión y vuelva a iniciarla con otro usuario en su inquilino.

  c. Si se siente especialmente ambicioso, registre y ejecute otra instancia de esta aplicación (con su propio clientId) y vea el inicio de sesión único en acción.

## <a name="next-steps"></a>Pasos siguientes
Como referencia, vea [ejemplo hello completado](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (sin los valores de configuración).

Ahora puede mover en toomore temas avanzados. Por ejemplo, intente [proteger una API web con Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
