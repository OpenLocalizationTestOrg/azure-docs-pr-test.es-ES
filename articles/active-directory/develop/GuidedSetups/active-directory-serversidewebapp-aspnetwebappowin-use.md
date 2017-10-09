---
title: "aaaAzure AD v2 ASP.NET Web Server Introducción: uso | Documentos de Microsoft"
description: "Implementación de inicio de sesión de Microsoft en una solución ASP.NET con una aplicación basada en un explorador web tradicional mediante el estándar OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a>Agregue un solicitudes de inicio de sesión y cierre de sesión de toohandle de controlador

Este paso se muestra cómo toocreate una tooexpose controlador nuevo inicio de sesión de y los métodos de cierre de sesión.

1.  Haga clic en hello `Controllers` carpeta y seleccione`Add` > `Controller`
2.  Seleccione `MVC (.NET version) Controller – Empty`.
3.  Haga clic en *Agregar*.
4.  Asígnele el nombre `HomeController` y haga clic en *Aceptar*.
5.  Agregar *OWIN* hace referencia a clase toohello:

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Agregue dos métodos de hello debajo toohandle inicio de sesión y cierre de sesión tooyour controlador mediante la realización de un desafío de autenticación a través de código:
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a>Crear toosign de página principal de la aplicación hello en los usuarios a través de un botón de inicio de sesión

En Visual Studio, un botón Crear nueva vista tooadd Hola inicio de sesión y mostrar información de usuario después de la autenticación:

1.  Haga clic en hello `Views\Home` carpeta y seleccione`Add View`
2.  Asígnele el nombre `Index`.
3.  Agregue Hola después de HTML, que incluye Hola inicio de sesión botón, archivo de toohello:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a>Más información
> Esta página agrega un botón de inicio de sesión en formato SVG con un fondo negro:<br/>![Iniciar sesión en Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)<br/> Para los botones de inicio de sesión más, consulte toohello [esta página](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "directrices de personalización de marca").
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a>Agregar notificaciones de usuario controlador toodisplay
Este controlador de muestra usa Hola de hello `[Authorize]` tooprotect un controlador de atributo. Este atributo restringe el controlador de acceso toohello solo tiene que permitir a los usuarios autenticados. Hola de código siguiente hace uso de notificaciones de usuario de toodisplay de atributo de Hola que se recuperaron como parte del inicio de sesión de Hola.

1.  Haga clic en hello `Controllers` carpeta:`Add` > `Controller`
2.  Seleccione `MVC {version} Controller – Empty`.
3.  Haga clic en *Agregar*.
4.  Asígnele el nombre `ClaimsController`.
5.  Reemplace el código de hello de la clase de controlador con el código de hello por debajo de - esto agrega hello `[Authorize]` toohello clase de atributos:

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Más información
> Debido a la utilice Hola de hello `[Authorize]` atributo, todos los métodos de este controlador sólo se puede ejecutar si se autentica el usuario de Hola. Si usuario hello no está autenticada y trata de controlador de hello tooaccess, OWIN iniciarán un desafío de autenticación y forzar hello tooauthenticate de usuario. colección de hello de notificaciones de código de Hello encima busca hello `ClaimsPrincipal.Current` instancia para los atributos de usuario específico incluido en el token del usuario de Hola. Estos atributos incluyen el nombre completo del usuario de Hola y nombre de usuario, así como sujeto de identificador de usuario global Hola. También contiene hello *Id. de inquilino*, que representa el Id. de hello para la organización del usuario de Hola. 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a>Crear una vista de notificaciones del usuario de toodisplay Hola

En Visual Studio, cree una nueva vista de notificaciones de usuario de toodisplay hello en una página web:

1.  Haga clic en hello `Views\Claims` carpeta y:`Add View`
2.  Asígnele el nombre `Index`.
3.  Agregue Hola HTML toohello archivo siguiente:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
