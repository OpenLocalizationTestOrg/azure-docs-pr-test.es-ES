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
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a><span data-ttu-id="f4423-103">Agregue un solicitudes de inicio de sesión y cierre de sesión de toohandle de controlador</span><span class="sxs-lookup"><span data-stu-id="f4423-103">Add a controller toohandle sign-in and sign-out requests</span></span>

<span data-ttu-id="f4423-104">Este paso se muestra cómo toocreate una tooexpose controlador nuevo inicio de sesión de y los métodos de cierre de sesión.</span><span class="sxs-lookup"><span data-stu-id="f4423-104">This step shows how toocreate a new controller tooexpose sign-in and sign-out methods.</span></span>

1.  <span data-ttu-id="f4423-105">Haga clic en hello `Controllers` carpeta y seleccione`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="f4423-105">Right click hello `Controllers` folder and select `Add` > `Controller`</span></span>
2.  <span data-ttu-id="f4423-106">Seleccione `MVC (.NET version) Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="f4423-106">Select `MVC (.NET version) Controller – Empty`.</span></span>
3.  <span data-ttu-id="f4423-107">Haga clic en *Agregar*.</span><span class="sxs-lookup"><span data-stu-id="f4423-107">Click *Add*</span></span>
4.  <span data-ttu-id="f4423-108">Asígnele el nombre `HomeController` y haga clic en *Aceptar*.</span><span class="sxs-lookup"><span data-stu-id="f4423-108">Name it `HomeController` and click *Add*</span></span>
5.  <span data-ttu-id="f4423-109">Agregar *OWIN* hace referencia a clase toohello:</span><span class="sxs-lookup"><span data-stu-id="f4423-109">Add *OWIN* references toohello class:</span></span>

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="f4423-110">Agregue dos métodos de hello debajo toohandle inicio de sesión y cierre de sesión tooyour controlador mediante la realización de un desafío de autenticación a través de código:</span><span class="sxs-lookup"><span data-stu-id="f4423-110">Add hello two methods below toohandle sign-in and sign-out tooyour controller by initiating an authentication challenge via code:</span></span>
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

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a><span data-ttu-id="f4423-111">Crear toosign de página principal de la aplicación hello en los usuarios a través de un botón de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="f4423-111">Create hello app's home page toosign in users via a sign-in button</span></span>

<span data-ttu-id="f4423-112">En Visual Studio, un botón Crear nueva vista tooadd Hola inicio de sesión y mostrar información de usuario después de la autenticación:</span><span class="sxs-lookup"><span data-stu-id="f4423-112">In Visual Studio, create a new view tooadd hello sign-in button and display user information after authentication:</span></span>

1.  <span data-ttu-id="f4423-113">Haga clic en hello `Views\Home` carpeta y seleccione`Add View`</span><span class="sxs-lookup"><span data-stu-id="f4423-113">Right click hello `Views\Home` folder and select `Add View`</span></span>
2.  <span data-ttu-id="f4423-114">Asígnele el nombre `Index`.</span><span class="sxs-lookup"><span data-stu-id="f4423-114">Name it `Index`.</span></span>
3.  <span data-ttu-id="f4423-115">Agregue Hola después de HTML, que incluye Hola inicio de sesión botón, archivo de toohello:</span><span class="sxs-lookup"><span data-stu-id="f4423-115">Add hello following HTML, which includes hello sign-in button, toohello file:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="f4423-116">Más información</span><span class="sxs-lookup"><span data-stu-id="f4423-116">More Information</span></span>
> <span data-ttu-id="f4423-117">Esta página agrega un botón de inicio de sesión en formato SVG con un fondo negro:</span><span class="sxs-lookup"><span data-stu-id="f4423-117">This page adds a sign-in button in SVG format with a black background:</span></span><br/><span data-ttu-id="f4423-118">![Iniciar sesión en Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span><span class="sxs-lookup"><span data-stu-id="f4423-118">![Sign-in with Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span></span><br/> <span data-ttu-id="f4423-119">Para los botones de inicio de sesión más, consulte toohello [esta página](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "directrices de personalización de marca").</span><span class="sxs-lookup"><span data-stu-id="f4423-119">For more sign-in buttons, please go toohello [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span></span>
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a><span data-ttu-id="f4423-120">Agregar notificaciones de usuario controlador toodisplay</span><span class="sxs-lookup"><span data-stu-id="f4423-120">Add a controller toodisplay user's claims</span></span>
<span data-ttu-id="f4423-121">Este controlador de muestra usa Hola de hello `[Authorize]` tooprotect un controlador de atributo.</span><span class="sxs-lookup"><span data-stu-id="f4423-121">This controller demonstrates hello uses of hello `[Authorize]` attribute tooprotect a controller.</span></span> <span data-ttu-id="f4423-122">Este atributo restringe el controlador de acceso toohello solo tiene que permitir a los usuarios autenticados.</span><span class="sxs-lookup"><span data-stu-id="f4423-122">This attribute restricts access toohello controller by only allowing authenticated users.</span></span> <span data-ttu-id="f4423-123">Hola de código siguiente hace uso de notificaciones de usuario de toodisplay de atributo de Hola que se recuperaron como parte del inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4423-123">hello code below makes use of hello attribute toodisplay user claims that were retrieved as part of hello sign-in.</span></span>

1.  <span data-ttu-id="f4423-124">Haga clic en hello `Controllers` carpeta:`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="f4423-124">Right click hello `Controllers` folder: `Add` > `Controller`</span></span>
2.  <span data-ttu-id="f4423-125">Seleccione `MVC {version} Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="f4423-125">Select `MVC {version} Controller – Empty`.</span></span>
3.  <span data-ttu-id="f4423-126">Haga clic en *Agregar*.</span><span class="sxs-lookup"><span data-stu-id="f4423-126">Click *Add*</span></span>
4.  <span data-ttu-id="f4423-127">Asígnele el nombre `ClaimsController`.</span><span class="sxs-lookup"><span data-stu-id="f4423-127">Name it `ClaimsController`</span></span>
5.  <span data-ttu-id="f4423-128">Reemplace el código de hello de la clase de controlador con el código de hello por debajo de - esto agrega hello `[Authorize]` toohello clase de atributos:</span><span class="sxs-lookup"><span data-stu-id="f4423-128">Replace hello code of your controller class with hello code below - this adds hello `[Authorize]` attribute toohello class:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="f4423-129">Más información</span><span class="sxs-lookup"><span data-stu-id="f4423-129">More Information</span></span>
> <span data-ttu-id="f4423-130">Debido a la utilice Hola de hello `[Authorize]` atributo, todos los métodos de este controlador sólo se puede ejecutar si se autentica el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4423-130">Because of hello use of hello `[Authorize]` attribute, all methods of this controller can only be executed if hello user is authenticated.</span></span> <span data-ttu-id="f4423-131">Si usuario hello no está autenticada y trata de controlador de hello tooaccess, OWIN iniciarán un desafío de autenticación y forzar hello tooauthenticate de usuario.</span><span class="sxs-lookup"><span data-stu-id="f4423-131">If hello user is not authenticated and tries tooaccess hello controller, OWIN will initiate an authentication challenge and force hello user tooauthenticate.</span></span> <span data-ttu-id="f4423-132">colección de hello de notificaciones de código de Hello encima busca hello `ClaimsPrincipal.Current` instancia para los atributos de usuario específico incluido en el token del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4423-132">hello code above looks at hello claims collection of hello `ClaimsPrincipal.Current` instance for specific user attributes included in hello user’s token.</span></span> <span data-ttu-id="f4423-133">Estos atributos incluyen el nombre completo del usuario de Hola y nombre de usuario, así como sujeto de identificador de usuario global Hola.</span><span class="sxs-lookup"><span data-stu-id="f4423-133">These attributes include hello user’s full name and username, as well as hello global user identifier subject.</span></span> <span data-ttu-id="f4423-134">También contiene hello *Id. de inquilino*, que representa el Id. de hello para la organización del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4423-134">It also contains hello *Tenant ID*, which represents hello ID for hello user’s organization.</span></span> 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a><span data-ttu-id="f4423-135">Crear una vista de notificaciones del usuario de toodisplay Hola</span><span class="sxs-lookup"><span data-stu-id="f4423-135">Create a view toodisplay hello user's claims</span></span>

<span data-ttu-id="f4423-136">En Visual Studio, cree una nueva vista de notificaciones de usuario de toodisplay hello en una página web:</span><span class="sxs-lookup"><span data-stu-id="f4423-136">In Visual Studio, create a new view toodisplay hello user's claims in a web page:</span></span>

1.  <span data-ttu-id="f4423-137">Haga clic en hello `Views\Claims` carpeta y:`Add View`</span><span class="sxs-lookup"><span data-stu-id="f4423-137">Right click hello `Views\Claims` folder and: `Add View`</span></span>
2.  <span data-ttu-id="f4423-138">Asígnele el nombre `Index`.</span><span class="sxs-lookup"><span data-stu-id="f4423-138">Name it `Index`.</span></span>
3.  <span data-ttu-id="f4423-139">Agregue Hola HTML toohello archivo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f4423-139">Add hello following HTML toohello file:</span></span>

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
