---
title: "aaaAzure AD .NET web de introducción a la API | Documentos de Microsoft"
description: "Cómo toobuild una API de web .NET MVC que se integra con Azure AD para la autenticación y autorización."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="76e56-103">Ayuda para proteger una API web con tokens portadores de Azure AD</span><span class="sxs-lookup"><span data-stu-id="76e56-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="76e56-104">Si va a compilar una aplicación que proporciona acceso a recursos de tooprotected, necesita tooknow cómo tooprevent ilícita tener acceso a recursos de toothose.</span><span class="sxs-lookup"><span data-stu-id="76e56-104">If you’re building an application that provides access tooprotected resources, you need tooknow how tooprevent unwarranted access toothose resources.</span></span>
<span data-ttu-id="76e56-105">Azure Active Directory (Azure AD) simplifica el proceso y sencillo toohelp protege una API web mediante tokens de acceso de portador de OAuth 2.0 con solo unas pocas líneas de código.</span><span class="sxs-lookup"><span data-stu-id="76e56-105">Azure Active Directory (Azure AD) makes it simple and straightforward toohelp protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="76e56-106">En las aplicaciones web ASP.NET, puede realizar esta protección mediante el uso de la implementación de Microsoft de Hola de hello controlada por la Comunidad software intermedio OWIN incluido en .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="76e56-106">In ASP.NET web apps, you can accomplish this protection by using hello Microsoft implementation of hello community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="76e56-107">Aquí vamos a usar OWIN toobuild una API web de "tooDo lista" que:</span><span class="sxs-lookup"><span data-stu-id="76e56-107">Here we’ll use OWIN toobuild a "tooDo List" web API that:</span></span>

* <span data-ttu-id="76e56-108">Designar las API que están protegidas.</span><span class="sxs-lookup"><span data-stu-id="76e56-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="76e56-109">Valida que las llamadas de API web de hello contienen un token de acceso válido.</span><span class="sxs-lookup"><span data-stu-id="76e56-109">Validates that hello web API calls contain a valid access token.</span></span>

<span data-ttu-id="76e56-110">toobuild hello tooDo API de la lista, primero debe:</span><span class="sxs-lookup"><span data-stu-id="76e56-110">toobuild hello tooDo List API, you first need to:</span></span>

1. <span data-ttu-id="76e56-111">Registrar una aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76e56-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="76e56-112">Configurar la canalización de autenticación de hello aplicación toouse hello OWIN.</span><span class="sxs-lookup"><span data-stu-id="76e56-112">Set up hello app toouse hello OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="76e56-113">Configurar un cliente aplicación toocall Hola API web.</span><span class="sxs-lookup"><span data-stu-id="76e56-113">Configure a client application toocall hello web API.</span></span>

<span data-ttu-id="76e56-114">tooget iniciado, [descargar esqueleto de aplicación Hola](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="76e56-114">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="76e56-115">Cualquiera de los dos es una solución de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="76e56-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="76e56-116">También tenga a un inquilino de Azure AD en qué tooregister su aplicación.</span><span class="sxs-lookup"><span data-stu-id="76e56-116">You also need an Azure AD tenant in which tooregister your application.</span></span> <span data-ttu-id="76e56-117">Si aún no tiene uno, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="76e56-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="76e56-118">Paso 1: Registro de una aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="76e56-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="76e56-119">toohelp proteger la aplicación, primero necesita toocreate una aplicación en su inquilino y proporcionar algunos fragmentos de información clave a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76e56-119">toohelp secure your application, you first need toocreate an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="76e56-120">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="76e56-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="76e56-121">En la barra superior de hello, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="76e56-121">On hello top bar, click your account.</span></span> <span data-ttu-id="76e56-122">Hola **Directory** elija inquilino hello Azure AD en el que desea tooregister la aplicación.</span><span class="sxs-lookup"><span data-stu-id="76e56-122">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="76e56-123">Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="76e56-123">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="76e56-124">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="76e56-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="76e56-125">Siga las indicaciones de Hola y crear un nuevo **aplicación Web o API Web**.</span><span class="sxs-lookup"><span data-stu-id="76e56-125">Follow hello prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="76e56-126">**Nombre** describe su toousers de aplicación.</span><span class="sxs-lookup"><span data-stu-id="76e56-126">**Name** describes your application toousers.</span></span> <span data-ttu-id="76e56-127">Escriba **tooDo servicio de la lista**.</span><span class="sxs-lookup"><span data-stu-id="76e56-127">Enter **tooDo List Service**.</span></span>
  * <span data-ttu-id="76e56-128">**Uri de redireccionamiento** es una combinación de esquema y la cadena que Azure AD usa tooreturn cualquiera símbolos (token) que la aplicación ha solicitado.</span><span class="sxs-lookup"><span data-stu-id="76e56-128">**Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn any tokens that your app has requested.</span></span> <span data-ttu-id="76e56-129">Escriba `https://localhost:44321/` para este valor.</span><span class="sxs-lookup"><span data-stu-id="76e56-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="76e56-130">De hello **configuración** -> **propiedades** página de la aplicación, actualice Hola App ID URI.</span><span class="sxs-lookup"><span data-stu-id="76e56-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="76e56-131">Especifique un identificador específico del inquilino.</span><span class="sxs-lookup"><span data-stu-id="76e56-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="76e56-132">Por ejemplo, escriba: `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="76e56-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="76e56-133">Guardar configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="76e56-133">Save hello configuration.</span></span> <span data-ttu-id="76e56-134">Vulnerable portal hello, porque también necesitará tooregister la aplicación cliente en breve.</span><span class="sxs-lookup"><span data-stu-id="76e56-134">Leave hello portal open, because you'll also need tooregister your client application shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="76e56-135">Paso 2: Configurar la canalización de autenticación de hello aplicación toouse hello OWIN</span><span class="sxs-lookup"><span data-stu-id="76e56-135">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="76e56-136">las solicitudes entrantes de toovalidate y símbolos (tokens), deberá tooset seguridad su toocommunicate de aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76e56-136">toovalidate incoming requests and tokens, you need tooset up your application toocommunicate with Azure AD.</span></span>

1. <span data-ttu-id="76e56-137">toobegin, abra la solución de Hola y Agregar proyecto de toohello de paquetes de NuGet TodoListService de hello OWIN middleware mediante Hola Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="76e56-137">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="76e56-138">Agregue un proyecto TodoListService de inicio de OWIN clases toohello denominado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="76e56-138">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="76e56-139">Proyecto de Hola de menú contextual, seleccione **agregar** > **nuevo elemento**y, a continuación, busque **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="76e56-139">Right-click hello project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="76e56-140">middleware de OWIN Hola invocará hello `Configuration(…)` método cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="76e56-140">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="76e56-141">Cambie la declaración de clase de hello demasiado`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="76e56-141">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="76e56-142">Ya hemos implementado parte de esta clase en otro archivo.</span><span class="sxs-lookup"><span data-stu-id="76e56-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="76e56-143">Hola `Configuration(…)` método, realizar una llamada demasiado`ConfgureAuth(…)` tooset la autenticación para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="76e56-143">In hello `Configuration(…)` method, make a call too`ConfgureAuth(…)` tooset up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="76e56-144">Archivo abierto hello `App_Start\Startup.Auth.cs` e implementar hello `ConfigureAuth(…)` método.</span><span class="sxs-lookup"><span data-stu-id="76e56-144">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="76e56-145">Hola parámetros que se proporcionan en `WindowsAzureActiveDirectoryBearerAuthenticationOptions` servirá como coordenadas para su toocommunicate de aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76e56-145">hello parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. <span data-ttu-id="76e56-146">Ahora puede usar `[Authorize]` toohelp atributos proteger los controladores y acciones con la autenticación de portador de JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="76e56-146">Now you can use `[Authorize]` attributes toohelp protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="76e56-147">Decorar hello `Controllers\TodoListController.cs` clase con una etiqueta de autorizar.</span><span class="sxs-lookup"><span data-stu-id="76e56-147">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="76e56-148">Esto forzará Hola usuario toosign en antes de acceder a esa página.</span><span class="sxs-lookup"><span data-stu-id="76e56-148">This will force hello user toosign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="76e56-149">Cuando un llamador autorizado correctamente invoca uno de hello `TodoListController` API, acción de Hola podría necesita acceder a tooinformation sobre llamador Hola.</span><span class="sxs-lookup"><span data-stu-id="76e56-149">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span> <span data-ttu-id="76e56-150">OWIN proporciona acceso toohello notificaciones dentro de token de portador de hello mediante hello `ClaimsPrincpal` objeto.</span><span class="sxs-lookup"><span data-stu-id="76e56-150">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="76e56-151">Un requisito común de las API web es toovalidate Hola "ámbitos" está presentes en el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="76e56-151">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="76e56-152">Esto garantiza que el usuario Hola ha dado su consentimiento toohello permisos necesarios tooaccess hello tooDo servicio de la lista.</span><span class="sxs-lookup"><span data-stu-id="76e56-152">This ensures that hello user has consented toohello permissions required tooaccess hello tooDo List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="76e56-153">Abra hello `web.config` un archivo en la raíz de Hola de proyecto TodoListService de Hola y escriba los valores de configuración en hello `<appSettings>` sección.</span><span class="sxs-lookup"><span data-stu-id="76e56-153">Open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="76e56-154">`ida:Tenant`es el nombre de hello del inquilino de Azure AD: por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="76e56-154">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="76e56-155">`ida:Audience`se Hola App ID URI de aplicación Hola que escribió en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="76e56-155">`ida:Audience` is hello App ID URI of hello application that you entered in hello Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a><span data-ttu-id="76e56-156">Paso 3: Configurar una aplicación cliente y ejecutar el servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="76e56-156">Step 3: Configure a client application and run hello service</span></span>
<span data-ttu-id="76e56-157">Para poder ver hello tooDo servicio de la lista en acción, debe a cliente de la lista de tooconfigure hello tooDo para que pueda obtener tokens de Azure AD y realiza llamadas a un servicio toohello.</span><span class="sxs-lookup"><span data-stu-id="76e56-157">Before you can see hello tooDo List Service in action, you need tooconfigure hello tooDo List client so it can get tokens from Azure AD and make calls toohello service.</span></span>

1. <span data-ttu-id="76e56-158">Volver atrás toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="76e56-158">Go back toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="76e56-159">Crear una nueva aplicación en su inquilino de Azure AD y seleccione **aplicación cliente nativa** en el símbolo del sistema de hello resultante.</span><span class="sxs-lookup"><span data-stu-id="76e56-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in hello resulting prompt.</span></span>
  * <span data-ttu-id="76e56-160">**Nombre** describe su toousers de aplicación.</span><span class="sxs-lookup"><span data-stu-id="76e56-160">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="76e56-161">Escriba `http://TodoListClient/` para hello **Uri de redireccionamiento** valor.</span><span class="sxs-lookup"><span data-stu-id="76e56-161">Enter `http://TodoListClient/` for hello **Redirect Uri** value.</span></span>

3. <span data-ttu-id="76e56-162">Cuando termine de registro, Azure AD le asigna una aplicación de tooyour de Id. de aplicación exclusivo.</span><span class="sxs-lookup"><span data-stu-id="76e56-162">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="76e56-163">Necesitará este valor en pasos de hello, por lo tanto cópiela desde la página de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="76e56-163">You’ll need this value in hello next steps, so copy it from hello application page.</span></span>

4. <span data-ttu-id="76e56-164">De hello **configuración** página, seleccione **permisos necesarios**y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="76e56-164">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="76e56-165">Busque y seleccione hello tooDo servicio de la lista, agregue hello **acceso TodoListService** permiso en **permisos delegados**y, a continuación, haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="76e56-165">Locate and select hello tooDo List Service, add hello **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="76e56-166">En Visual Studio, abra `App.config` en Hola TodoListClient proyecto y, a continuación, escriba los valores de configuración en hello `<appSettings>` sección.</span><span class="sxs-lookup"><span data-stu-id="76e56-166">In Visual Studio, open `App.config` in hello TodoListClient project, and then enter your configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="76e56-167">`ida:Tenant`es el nombre de hello del inquilino de Azure AD: por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="76e56-167">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="76e56-168">`ida:ClientId`es el Id. de aplicación de Hola que copió de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="76e56-168">`ida:ClientId` is hello app ID that you copied from hello Azure portal.</span></span>
  * <span data-ttu-id="76e56-169">`todo:TodoListResourceId`es hello App ID URI de hello tooDo aplicación de servicio de la lista que escribió en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="76e56-169">`todo:TodoListResourceId` is hello App ID URI of hello tooDo List Service application that you entered in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76e56-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76e56-170">Next steps</span></span>
<span data-ttu-id="76e56-171">Por último, limpie, compile y ejecute cada proyecto.</span><span class="sxs-lookup"><span data-stu-id="76e56-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="76e56-172">Si no lo ha hecho ya, ahora es a Hola tiempo toocreate un nuevo usuario en el inquilino con un *. dominio onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="76e56-172">If you haven’t already, now is hello time toocreate a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="76e56-173">Inicie sesión en el cliente de la lista toohello tooDo a ese usuario y agregar la lista de tareas del usuario algunas tareas toohello.</span><span class="sxs-lookup"><span data-stu-id="76e56-173">Sign in toohello tooDo List client with that user, and add some tasks toohello user's to-do list.</span></span>

<span data-ttu-id="76e56-174">Como referencia, está disponible en el ejemplo de Hola finalizado (sin los valores de configuración) [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="76e56-174">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="76e56-175">Ahora puede mover en escenarios de identidad toomore.</span><span class="sxs-lookup"><span data-stu-id="76e56-175">You can now move on toomore identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
