---
title: "uso de inicio de sesión tooa API web .NET MVC aaaAdd Hola extremo v2.0 de Azure AD | Documentos de Microsoft"
description: "¿Cómo toobuild una Api Web MVC de .NET que acepta los tokens de ambos Account personal de Microsoft y cuentas profesionales o educativas."
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
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="9f51c-103">Protección de una API web MVC</span><span class="sxs-lookup"><span data-stu-id="9f51c-103">Secure an MVC web API</span></span>
<span data-ttu-id="9f51c-104">Con el punto de conexión de Azure Active Directory Hola v2.0, puede proteger una API de Web mediante [OAuth 2.0](active-directory-v2-protocols.md) tokens de acceso, lo que permite a los usuarios con ambos cuenta personal de Microsoft y cuentas profesionales o educativas toosecurely tener acceso a la API Web.</span><span class="sxs-lookup"><span data-stu-id="9f51c-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="9f51c-105">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="9f51c-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="9f51c-106">toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="9f51c-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="9f51c-107">En las API web ASP.NET puede realizar esto con el OWIN middleware de Microsoft incluido en .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="9f51c-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="9f51c-108">Aquí usamos la OWIN toobuild una API Web MVC de "tooDo lista" que permite a los clientes las tareas toocreate y lectura de la lista de tareas pendientes de un usuario.</span><span class="sxs-lookup"><span data-stu-id="9f51c-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="9f51c-109">API de web Hola validará que contienen un token de acceso válido y rechazan las solicitudes que no pasan la validación en una ruta protegida las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="9f51c-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="9f51c-110">Este ejemplo se creó con Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9f51c-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="9f51c-111">Descargar</span><span class="sxs-lookup"><span data-stu-id="9f51c-111">Download</span></span>
<span data-ttu-id="9f51c-112">código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="9f51c-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="9f51c-113">toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) o esqueleto de Hola de clon:</span><span class="sxs-lookup"><span data-stu-id="9f51c-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="9f51c-114">aplicación esqueleto de Hello incluye todo el código de hello reutilizable para una API sencilla, pero le falta todas partes relacionadas con la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f51c-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="9f51c-115">Si no desea toofollow a lo largo de, en su lugar, se pueden clonar o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="9f51c-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="9f51c-116">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="9f51c-116">Register an app</span></span>
<span data-ttu-id="9f51c-117">Cree una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="9f51c-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="9f51c-118">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="9f51c-118">Make sure to:</span></span>

* <span data-ttu-id="9f51c-119">Copia hacia abajo hello **Id. de aplicación** asignado tooyour aplicación, ya que lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="9f51c-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="9f51c-120">La solución de Visual Studio también contiene "TodoListClient", que es una sencilla aplicación WPF.</span><span class="sxs-lookup"><span data-stu-id="9f51c-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="9f51c-121">Hola TodoListClient es usado toodemonstrate cómo un usuario inicia sesión y cómo puede emitir un cliente solicita tooyour API Web.</span><span class="sxs-lookup"><span data-stu-id="9f51c-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="9f51c-122">En este caso, se representan hello TodoListClient y hello TodoListService por hello misma aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f51c-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="9f51c-123">tooconfigure Hola TodoListClient, también debe:</span><span class="sxs-lookup"><span data-stu-id="9f51c-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="9f51c-124">Agregar hello **Mobile** plataforma para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f51c-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="9f51c-125">Instalar OWIN</span><span class="sxs-lookup"><span data-stu-id="9f51c-125">Install OWIN</span></span>
<span data-ttu-id="9f51c-126">Ahora que ha registrado una aplicación, necesita tooset seguridad su toocommunicate de aplicación con punto de conexión de hello v2.0 en orden toovalidate las solicitudes entrantes y símbolos (tokens).</span><span class="sxs-lookup"><span data-stu-id="9f51c-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="9f51c-127">toobegin, abra la solución de Hola y agregue hello OWIN middleware NuGet paquetes toohello TodoListService proyecto mediante la consola de administrador de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="9f51c-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="9f51c-128">Configurar la autenticación de OAuth</span><span class="sxs-lookup"><span data-stu-id="9f51c-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="9f51c-129">Agregue un proyecto TodoListService de inicio de OWIN clases toohello denominado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="9f51c-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="9f51c-130">Haga clic en proyecto de hello--> **agregar** --> **nuevo elemento** --> busque "OWIN".</span><span class="sxs-lookup"><span data-stu-id="9f51c-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="9f51c-131">middleware de OWIN Hola invocará hello `Configuration(…)` método cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9f51c-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="9f51c-132">Cambie la declaración de clase de hello demasiado`public partial class Startup` -hemos implementado ya parte de esta clase para usted en otro archivo.</span><span class="sxs-lookup"><span data-stu-id="9f51c-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="9f51c-133">Hola `Configuration(…)` método, realizar un tooset de tooConfgureAuth(...) de llamada de la autenticación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="9f51c-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="9f51c-134">Archivo abierto hello `App_Start\Startup.Auth.cs` e implementar hello `ConfigureAuth(…)` método, que configurará tooaccept tokens de hello Web API desde el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="9f51c-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="9f51c-135">Ahora puede usar `[Authorize]` atributos tooprotect los controladores y acciones con la autenticación de portador de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="9f51c-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="9f51c-136">Decorar hello `Controllers\TodoListController.cs` clase con una etiqueta de autorizar.</span><span class="sxs-lookup"><span data-stu-id="9f51c-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="9f51c-137">Esto forzará Hola usuario toosign en antes de acceder a esa página.</span><span class="sxs-lookup"><span data-stu-id="9f51c-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="9f51c-138">Cuando un llamador autorizado correctamente invoca uno de hello `TodoListController` API, acción de Hola podría necesita acceder a tooinformation sobre llamador Hola.</span><span class="sxs-lookup"><span data-stu-id="9f51c-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="9f51c-139">OWIN proporciona acceso toohello notificaciones dentro de token de portador de hello mediante hello `ClaimsPrincpal` objeto.</span><span class="sxs-lookup"><span data-stu-id="9f51c-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="9f51c-140">Por último, abra hello `web.config` un archivo en la raíz de Hola de proyecto TodoListService de Hola y escriba los valores de configuración en hello `<appSettings>` sección.</span><span class="sxs-lookup"><span data-stu-id="9f51c-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="9f51c-141">Su `ida:Audience` es hello **Id. de aplicación** de aplicación hello especificado en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f51c-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="9f51c-142">Configurar la aplicación de cliente hello</span><span class="sxs-lookup"><span data-stu-id="9f51c-142">Configure hello client app</span></span>
<span data-ttu-id="9f51c-143">Para poder ver Hola servicio de lista de tareas en acción, deberá tooconfigure Hola cliente lista de tareas para que pueda obtener tokens de punto de conexión de hello v2.0 y hacer llamadas toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="9f51c-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="9f51c-144">En hello TodoListClient proyecto, abra `App.config` y escriba los valores de configuración en hello `<appSettings>` sección.</span><span class="sxs-lookup"><span data-stu-id="9f51c-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="9f51c-145">Su `ida:ClientId` identificador de la aplicación copian desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f51c-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="9f51c-146">Por último, limpie, compile y ejecute cada proyecto.</span><span class="sxs-lookup"><span data-stu-id="9f51c-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="9f51c-147">Ahora dispone de una API web MVC de .NET que acepta los token de las cuentas de Microsoft y de las cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="9f51c-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="9f51c-148">Inicie sesión en hello TodoListClient y llamar a la lista de tareas pendientes de web api tooadd tareas toohello de sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="9f51c-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="9f51c-149">Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como .zip aquí](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), o se puede clonar desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="9f51c-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="9f51c-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f51c-150">Next steps</span></span>
<span data-ttu-id="9f51c-151">Ahora puede pasar a otros temas adicionales.</span><span class="sxs-lookup"><span data-stu-id="9f51c-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="9f51c-152">Puede que desee tootry:</span><span class="sxs-lookup"><span data-stu-id="9f51c-152">You may want tootry:</span></span>

[<span data-ttu-id="9f51c-153">Llamada a una API web desde una aplicación web &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="9f51c-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="9f51c-154">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="9f51c-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="9f51c-155">Guía del desarrollador de Hello v2.0 >></span><span class="sxs-lookup"><span data-stu-id="9f51c-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="9f51c-156">Etiqueta "azure-active-directory" de StackOverflow &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="9f51c-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="9f51c-157">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="9f51c-157">Get security updates for our products</span></span>
<span data-ttu-id="9f51c-158">Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.</span><span class="sxs-lookup"><span data-stu-id="9f51c-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
