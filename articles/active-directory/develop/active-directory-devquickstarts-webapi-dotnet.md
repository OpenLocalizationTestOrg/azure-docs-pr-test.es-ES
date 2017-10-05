---
title: "Introducción a la API web de .NET de Azure AD | Microsoft Docs"
description: "Cómo crear una API web de .NET MVC que se integra con Azure AD para su autenticación y autorización."
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
ms.openlocfilehash: f44d75f45073a5d9aa9b1863ed227aba4efcf785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="c7890-103">Ayuda para proteger una API web con tokens portadores de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7890-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="c7890-104">Si va a crear una aplicación que proporciona acceso a recursos protegidos, debe saber cómo proteger dichos recursos frente a accesos injustificados.</span><span class="sxs-lookup"><span data-stu-id="c7890-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="c7890-105">Azure Active Directory (Azure AD) facilita la protección de una API web mediante tokens de acceso portadores de OAuth 2.0 con solo unas pocas líneas de código.</span><span class="sxs-lookup"><span data-stu-id="c7890-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="c7890-106">En las aplicaciones web ASP.NET, puede realizar esta protección con la implementación de Microsoft del middleware OWIN controlado por la comunidad incluido en .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="c7890-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="c7890-107">En este caso, usaremos OWIN para compilar una API web de "Lista de tareas pendientes" que lleve a cabo las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="c7890-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="c7890-108">Designar las API que están protegidas.</span><span class="sxs-lookup"><span data-stu-id="c7890-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="c7890-109">Validar que las llamadas de API web contengan un token de acceso válido.</span><span class="sxs-lookup"><span data-stu-id="c7890-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="c7890-110">Para compilar la API de lista de tareas pendientes, primero debe:</span><span class="sxs-lookup"><span data-stu-id="c7890-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="c7890-111">Registrar una aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7890-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="c7890-112">Configurar la aplicación para que use la canalización de autenticación OWIN.</span><span class="sxs-lookup"><span data-stu-id="c7890-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="c7890-113">Configurar una aplicación cliente para llamar a la API web.</span><span class="sxs-lookup"><span data-stu-id="c7890-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="c7890-114">Para empezar, [descargue el esquema de la aplicación](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) o [descargue el ejemplo finalizado](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="c7890-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="c7890-115">Cualquiera de los dos es una solución de Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c7890-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="c7890-116">También necesitará a un inquilino de Azure AD en el que registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7890-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="c7890-117">Si aún no tiene uno, [descubra cómo conseguirlo](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="c7890-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="c7890-118">Paso 1: Registro de una aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7890-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="c7890-119">Para proteger su aplicación, primero debe crear una aplicación en el inquilino y proporcionar a Azure AD algunos elementos de información clave.</span><span class="sxs-lookup"><span data-stu-id="c7890-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="c7890-120">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c7890-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c7890-121">En la barra superior, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="c7890-121">On the top bar, click your account.</span></span> <span data-ttu-id="c7890-122">En la lista **Directorio**, elija el inquilino de Azure AD donde desea registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7890-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="c7890-123">Haga clic en **Más servicios** en el panel izquierdo y seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7890-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="c7890-124">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c7890-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="c7890-125">Siga las indicaciones y cree una nueva **aplicación web y/o API web**.</span><span class="sxs-lookup"><span data-stu-id="c7890-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="c7890-126">**Nombre** describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c7890-126">**Name** describes your application to users.</span></span> <span data-ttu-id="c7890-127">Escriba **Servicio de lista de tareas pendientes**.</span><span class="sxs-lookup"><span data-stu-id="c7890-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="c7890-128">El **Uri de redirección** es una combinación de esquema y cadena que usa Azure AD para devolver los tokens solicitados por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7890-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="c7890-129">Escriba `https://localhost:44321/` para este valor.</span><span class="sxs-lookup"><span data-stu-id="c7890-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="c7890-130">En la página **Configuración** -> **Propiedades** de la aplicación, actualice el URI del identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7890-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="c7890-131">Especifique un identificador específico del inquilino.</span><span class="sxs-lookup"><span data-stu-id="c7890-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="c7890-132">Por ejemplo, escriba: `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="c7890-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="c7890-133">Guarde la configuración.</span><span class="sxs-lookup"><span data-stu-id="c7890-133">Save the configuration.</span></span> <span data-ttu-id="c7890-134">Deje abierto el portal, ya que también deberá registrar su aplicación cliente en breve.</span><span class="sxs-lookup"><span data-stu-id="c7890-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="c7890-135">Paso 2: Configuración de la aplicación para que use la canalización de autenticación OWIN</span><span class="sxs-lookup"><span data-stu-id="c7890-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="c7890-136">Para validar solicitudes y tokens entrantes, debe configurar la aplicación para que se comunique con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7890-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="c7890-137">Para comenzar, abra la solución y agregue los paquetes NuGet de middleware OWIN al proyecto TodoListService mediante la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c7890-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="c7890-138">Agregue una Clase de inicio OWIN al proyecto de ServicioListaTodo llamado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="c7890-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="c7890-139">Haga clic con el botón derecho en el proyecto, seleccione **Agregar** > **Nuevo elemento** y luego busque **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="c7890-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="c7890-140">El middleware OWIN invocará el método `Configuration(…)` al iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7890-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="c7890-141">Cambie la declaración de clase a `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="c7890-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="c7890-142">Ya hemos implementado parte de esta clase en otro archivo.</span><span class="sxs-lookup"><span data-stu-id="c7890-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="c7890-143">En el método `Configuration(…)`, realice una llamada a `ConfgureAuth(…)` para configurar la autenticación para su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c7890-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="c7890-144">Abra el archivo `App_Start\Startup.Auth.cs` e implemente el método `ConfigureAuth(…)`.</span><span class="sxs-lookup"><span data-stu-id="c7890-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="c7890-145">Los parámetros que proporciona en `WindowsAzureActiveDirectoryBearerAuthenticationOptions` servirán como coordenadas para que su aplicación se comunique con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7890-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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

5. <span data-ttu-id="c7890-146">Ahora puede usar atributos `[Authorize]` como ayuda para proteger los controladores y acciones con la autenticación de portador de JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="c7890-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="c7890-147">Decore la clase `Controllers\TodoListController.cs` con una etiqueta Autorizar.</span><span class="sxs-lookup"><span data-stu-id="c7890-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="c7890-148">Esto obligará al usuario a iniciar sesión antes de tener acceso a esa página.</span><span class="sxs-lookup"><span data-stu-id="c7890-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="c7890-149">Cuando un autor de llamada autorizado invoca correctamente una de las API `TodoListController` , es posible que la acción deba tener acceso a información sobre este.</span><span class="sxs-lookup"><span data-stu-id="c7890-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="c7890-150">OWIN proporciona acceso a las notificaciones dentro del token portador a través del objeto `ClaimsPrincpal` .</span><span class="sxs-lookup"><span data-stu-id="c7890-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="c7890-151">Un requisito común de las API web es validar los "ámbitos" presentes en el token.</span><span class="sxs-lookup"><span data-stu-id="c7890-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="c7890-152">De esta forma se garantiza que el usuario ha dado su consentimiento a los permisos necesarios para acceder al servicio de lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="c7890-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="c7890-153">Abra el archivo `web.config` en la raíz del proyecto TodoListService y escriba sus valores de configuración en la sección `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="c7890-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="c7890-154">`ida:Tenant` es el nombre del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="c7890-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="c7890-155">`ida:Audience` es el URI de id. de aplicación de la aplicación que escribió en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c7890-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="c7890-156">Paso 3: Configuración de una aplicación cliente y ejecución del servicio</span><span class="sxs-lookup"><span data-stu-id="c7890-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="c7890-157">Para poder ver el servicio de lista de tareas pendientes en acción, debe configurar el cliente de lista de tareas pendientes para que pueda obtener tokens de Azure AD y realizar llamadas al servicio.</span><span class="sxs-lookup"><span data-stu-id="c7890-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="c7890-158">Vuelva a [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c7890-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c7890-159">Cree una nueva aplicación en su inquilino de Azure AD y seleccione **Aplicación de cliente nativo** en la indicación resultante.</span><span class="sxs-lookup"><span data-stu-id="c7890-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="c7890-160">**Nombre** describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="c7890-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="c7890-161">Escriba `http://TodoListClient/` para el valor **Uri de redirección** .</span><span class="sxs-lookup"><span data-stu-id="c7890-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="c7890-162">Cuando termine el registro, Azure AD asignará un identificador de aplicación único a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7890-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="c7890-163">Necesitará este valor en las secciones siguientes, así que cópielo de la página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c7890-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="c7890-164">En la página **Configuración**, seleccione **Permisos necesarios** y **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c7890-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="c7890-165">Busque y seleccione el servicio de lista de tareas pendientes, agregue el permiso **Acceder a TodoListService** en **Permisos delegados** y luego haga clic en **Listo**.</span><span class="sxs-lookup"><span data-stu-id="c7890-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="c7890-166">En Visual Studio, abra `App.config` en el proyecto TodoListClient y escriba sus valores de configuración en la sección `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="c7890-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="c7890-167">`ida:Tenant` es el nombre del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="c7890-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="c7890-168">`ida:ClientId` es el id. de aplicación que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c7890-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="c7890-169">`todo:TodoListResourceId` es el URI de id. de aplicación de la aplicación del servicio de lista de tareas pendientes que escribió en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c7890-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7890-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c7890-170">Next steps</span></span>
<span data-ttu-id="c7890-171">Por último, limpie, compile y ejecute cada proyecto.</span><span class="sxs-lookup"><span data-stu-id="c7890-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="c7890-172">Si aún no lo ha hecho, ahora es el momento de crear un nuevo usuario en su inquilino con un dominio *.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="c7890-172">If you haven’t already, now is the time to create a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="c7890-173">Inicie sesión en el cliente de lista de tareas pendientes con ese usuario y agregue algunas tareas a la lista de tareas pendientes del usuario.</span><span class="sxs-lookup"><span data-stu-id="c7890-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="c7890-174">Como referencia, en [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip) está disponible el ejemplo finalizado (sin sus valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="c7890-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="c7890-175">Ahora puede continuar con más escenarios de identidad.</span><span class="sxs-lookup"><span data-stu-id="c7890-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
