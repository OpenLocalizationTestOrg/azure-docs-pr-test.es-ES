---
title: "Incorporación del inicio de sesión a una API web MVC de .NET mediante el punto de conexión de Azure AD v2.0 | Microsoft Docs"
description: "Cómo crear una API web MVC de .NET que acepta los token de las cuentas de Microsoft y de las cuentas profesionales o educativas."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: b2d7bbfcd9218698f71e9dfdb1ad5d9ff8740f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="52ad9-103">Protección de una API web MVC</span><span class="sxs-lookup"><span data-stu-id="52ad9-103">Secure an MVC web API</span></span>
<span data-ttu-id="52ad9-104">Con el punto de conexión v2.0 de Azure Active Directory, puede proteger una API web mediante tokens de acceso [OAuth 2.0](active-directory-v2-protocols.md) , lo que permite a los usuarios que tengan una cuenta Microsoft personal y cuentas profesionales o educativas el acceso seguro a su API web.</span><span class="sxs-lookup"><span data-stu-id="52ad9-104">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="52ad9-105">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión v2.0.</span><span class="sxs-lookup"><span data-stu-id="52ad9-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="52ad9-106">Para determinar si debe usar el punto de conexión v2.0, lea acerca de las [limitaciones de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="52ad9-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="52ad9-107">En las API web ASP.NET puede realizar esto con el OWIN middleware de Microsoft incluido en .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="52ad9-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="52ad9-108">Aquí vamos a usar OWIN para compilar una API web MVC "Lista de tareas pendientes" que permite a los clientes crear y leer tareas de la lista de tareas pendientes de un usuario.</span><span class="sxs-lookup"><span data-stu-id="52ad9-108">Here we’ll use OWIN to build a "To Do List" MVC Web API that allows clients to create and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="52ad9-109">La API web validará que las solicitudes entrantes contienen un token de acceso válido y rechazará todas las solicitudes que no superen la validación en una ruta protegida.</span><span class="sxs-lookup"><span data-stu-id="52ad9-109">The web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="52ad9-110">Este ejemplo se creó con Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="52ad9-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="52ad9-111">Descargar</span><span class="sxs-lookup"><span data-stu-id="52ad9-111">Download</span></span>
<span data-ttu-id="52ad9-112">El código de este tutorial se conserva [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="52ad9-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="52ad9-113">Para continuar, puede [descargar el esqueleto de la aplicación como un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o clonar el esqueleto:</span><span class="sxs-lookup"><span data-stu-id="52ad9-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="52ad9-114">La estructura de aplicación incluye todo el código reutilizable para una API sencilla, pero no tiene las partes relacionadas con la identidad.</span><span class="sxs-lookup"><span data-stu-id="52ad9-114">The skeleton app includes all the boilerplate code for a simple API, but is missing all of the identity-related pieces.</span></span> <span data-ttu-id="52ad9-115">Si no desea continuar por este camino, en su lugar puede clonar o [descargar el ejemplo finalizado](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="52ad9-115">If you don't want to follow along, you can instead clone or [download the completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="52ad9-116">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="52ad9-116">Register an app</span></span>
<span data-ttu-id="52ad9-117">Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="52ad9-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="52ad9-118">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="52ad9-118">Make sure to:</span></span>

* <span data-ttu-id="52ad9-119">Anotar el **Id. de aplicación** asignado a su aplicación; lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="52ad9-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>

<span data-ttu-id="52ad9-120">La solución de Visual Studio también contiene "TodoListClient", que es una sencilla aplicación WPF.</span><span class="sxs-lookup"><span data-stu-id="52ad9-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="52ad9-121">TodoListClient se utiliza para demostrar cómo el usuario inicia sesión y cómo el cliente puede enviar solicitudes a la API de web.</span><span class="sxs-lookup"><span data-stu-id="52ad9-121">The TodoListClient is used to demonstrate how a user signs-in and how a client can issue requests to your Web API.</span></span>  <span data-ttu-id="52ad9-122">En este caso, tanto TodoListClient como TodoListService se representan por la misma aplicación.</span><span class="sxs-lookup"><span data-stu-id="52ad9-122">In this case, both the TodoListClient and the TodoListService are represented by the same app.</span></span>  <span data-ttu-id="52ad9-123">Para configurar TodoListClient, también debe:</span><span class="sxs-lookup"><span data-stu-id="52ad9-123">To configure the TodoListClient, you should also:</span></span>

* <span data-ttu-id="52ad9-124">Agregar la plataforma **Móvil** a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52ad9-124">Add the **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="52ad9-125">Instalar OWIN</span><span class="sxs-lookup"><span data-stu-id="52ad9-125">Install OWIN</span></span>
<span data-ttu-id="52ad9-126">Ahora que ha registrado una aplicación, debe configurarla para comunicarse con el extremo v2.0 con objeto de validar las solicitudes y tokens entrantes.</span><span class="sxs-lookup"><span data-stu-id="52ad9-126">Now that you’ve registered an app, you need to set up your app to communicate with the v2.0 endpoint in order to validate incoming requests & tokens.</span></span>

* <span data-ttu-id="52ad9-127">Para comenzar, abra la solución y agregue los paquetes NuGet de middleware OWIN al proyecto de ServicioListaTodo mediante la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="52ad9-127">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="52ad9-128">Configurar la autenticación de OAuth</span><span class="sxs-lookup"><span data-stu-id="52ad9-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="52ad9-129">Agregue una Clase de inicio OWIN al proyecto de ServicioListaTodo llamado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="52ad9-129">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="52ad9-130">Haga clic con el botón derecho en el proyecto --> **Agregar** --> **Nuevo elemento** --> Busque "OWIN".</span><span class="sxs-lookup"><span data-stu-id="52ad9-130">Right click on the project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="52ad9-131">El middleware OWIN invocará el método `Configuration(…)` al iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52ad9-131">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="52ad9-132">Cambie la declaración de clase a `public partial class Startup` (ya hemos implementado parte de esta clase para usted en otro archivo).</span><span class="sxs-lookup"><span data-stu-id="52ad9-132">Change the class declaration to `public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="52ad9-133">En el método `Configuration(…)`, realice una llamada a ConfigureAuth(...) para configurar la autenticación para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="52ad9-133">In the `Configuration(…)` method, make a call to ConfgureAuth(…) to set up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="52ad9-134">Abra el archivo `App_Start\Startup.Auth.cs` e implemente el método `ConfigureAuth(…)`, que configurará la API web para aceptar tokens desde el punto de conexión v2.0.</span><span class="sxs-lookup"><span data-stu-id="52ad9-134">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method, which will set up the Web API to accept tokens from the v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, the TodoListClient and TodoListService
                // are represented using the same Application Id - we use
                // the Application Id to represent the audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that the user's organization (if applicable) has
                // signed up for the app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up the OWIN pipeline to use OAuth 2.0 Bearer authentication.
        // The options provided here tell the middleware about the type of tokens
        // that will be recieved, which are JWTs for the v2.0 endpoint.

        // NOTE: The usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by the v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used to fetch & use the OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="52ad9-135">Ahora puede utilizar atributos de `[Authorize]` para proteger sus controladores y acciones con la autenticación portadora de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="52ad9-135">Now you can use `[Authorize]` attributes to protect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="52ad9-136">Decore la clase `Controllers\TodoListController.cs` con una etiqueta Autorizar.</span><span class="sxs-lookup"><span data-stu-id="52ad9-136">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="52ad9-137">Esto obligará al usuario a iniciar sesión antes de tener acceso a esa página.</span><span class="sxs-lookup"><span data-stu-id="52ad9-137">This will force the user to sign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="52ad9-138">Cuando un autor de llamada autorizado invoca correctamente una de las API `TodoListController` , es posible que la acción deba tener acceso a información sobre este.</span><span class="sxs-lookup"><span data-stu-id="52ad9-138">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span>  <span data-ttu-id="52ad9-139">OWIN proporciona acceso a las notificaciones dentro del token portador a través del objeto `ClaimsPrincpal` .</span><span class="sxs-lookup"><span data-stu-id="52ad9-139">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use the ClaimsPrincipal to access information about the
    // user making the call.  In this case, we use the 'sub' or
    // NameIdentifier claim to serve as a key for the tasks in the data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="52ad9-140">Por último, abra el archivo `web.config` en la raíz del proyecto de ServicioListaTodo y escriba sus valores de configuración en la sección `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="52ad9-140">Finally, open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="52ad9-141">Su `ida:Audience` es el **Id. de aplicación** de la aplicación que escribió en el portal.</span><span class="sxs-lookup"><span data-stu-id="52ad9-141">Your `ida:Audience` is the **Application Id** of the app that you entered in the portal.</span></span>

## <a name="configure-the-client-app"></a><span data-ttu-id="52ad9-142">Configurar la aplicación cliente</span><span class="sxs-lookup"><span data-stu-id="52ad9-142">Configure the client app</span></span>
<span data-ttu-id="52ad9-143">Para poder ver el servicio de lista de tareas pendientes en acción, deberá configurar el cliente de lista de tareas pendientes para que pueda obtener token del extremo v2.0 y realizar llamadas al servicio.</span><span class="sxs-lookup"><span data-stu-id="52ad9-143">Before you can see the Todo List Service in action, you need to configure the Todo List Client so it can get tokens from the v2.0 endpoint and make calls to the service.</span></span>

* <span data-ttu-id="52ad9-144">El proyecto TodoListClient, abra `App.config` y escriba sus valores de configuración en la sección `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="52ad9-144">In the TodoListClient project, open `App.config` and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="52ad9-145">Su Id. de aplicación `ida:ClientId` que copió desde el portal.</span><span class="sxs-lookup"><span data-stu-id="52ad9-145">Your `ida:ClientId` Application Id you copied from the portal.</span></span>

<span data-ttu-id="52ad9-146">Por último, limpie, compile y ejecute cada proyecto.</span><span class="sxs-lookup"><span data-stu-id="52ad9-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="52ad9-147">Ahora dispone de una API web MVC de .NET que acepta los token de las cuentas de Microsoft y de las cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="52ad9-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="52ad9-148">Inicie sesión en TodoListClient y llame a la api web para agregar tareas a la lista de tareas del usuario.</span><span class="sxs-lookup"><span data-stu-id="52ad9-148">Sign into the TodoListClient, and call your web api to add tasks to the user's To-Do list.</span></span>

<span data-ttu-id="52ad9-149">Como referencia, el ejemplo finalizado (sin sus valores de configuración) [se proporciona en forma de archivo .zip aquí](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), aunque también puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="52ad9-149">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="52ad9-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52ad9-150">Next steps</span></span>
<span data-ttu-id="52ad9-151">Ahora puede pasar a otros temas adicionales.</span><span class="sxs-lookup"><span data-stu-id="52ad9-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="52ad9-152">También puede probar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="52ad9-152">You may want to try:</span></span>

[<span data-ttu-id="52ad9-153">Llamada a una API web desde una aplicación web >></span><span class="sxs-lookup"><span data-stu-id="52ad9-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="52ad9-154">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="52ad9-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="52ad9-155">La guía del desarrollador de v2.0 >></span><span class="sxs-lookup"><span data-stu-id="52ad9-155">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="52ad9-156">Etiqueta "azure-active-directory" de StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="52ad9-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="52ad9-157">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="52ad9-157">Get security updates for our products</span></span>
<span data-ttu-id="52ad9-158">Le animamos a que obtenga notificaciones de los incidentes de seguridad que se produzcan; para ello, visite [esta página](https://technet.microsoft.com/security/dd252948) y suscríbase a las alertas de avisos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="52ad9-158">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
