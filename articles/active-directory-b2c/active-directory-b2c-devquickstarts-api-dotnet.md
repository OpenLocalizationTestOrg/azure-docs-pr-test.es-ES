---
title: Azure AD B2C | Microsoft Docs
description: "Creación de una API web de .NET con Azure Active Directory B2C, protegida con tokens de acceso de OAuth 2.0 para autenticación."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 48749bfa2ab54a0e766a4aad4f39073cc4e90818
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="71883-103">Azure Active Directory B2C: Creación de una API web de .NET</span><span class="sxs-lookup"><span data-stu-id="71883-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="71883-104">Con Azure Active Directory (Azure AD) B2C, puede proteger una API web mediante el uso de tokens de acceso de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="71883-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="71883-105">Estos tokens permiten a las aplicaciones cliente autenticarse en la API.</span><span class="sxs-lookup"><span data-stu-id="71883-105">These tokens allow your client apps to authenticate to the API.</span></span> <span data-ttu-id="71883-106">En este artículo se muestra cómo crear una API de "lista de tareas pendientes" de MVC de .NET que permite a los usuarios de la aplicación cliente realizar tareas de creación, lectura, actualización y eliminación.</span><span class="sxs-lookup"><span data-stu-id="71883-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span></span> <span data-ttu-id="71883-107">La API web se protege con Azure AD B2C y solo permite a los usuarios autenticados administrar sus listas de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="71883-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="71883-108">Creación de un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="71883-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="71883-109">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="71883-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="71883-110">Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="71883-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="71883-111">Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar con esta guía.</span><span class="sxs-lookup"><span data-stu-id="71883-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="71883-112">La API de web y la aplicación de cliente deben usar el mismo directorio de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="71883-112">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="71883-113">Creación de una API web</span><span class="sxs-lookup"><span data-stu-id="71883-113">Create a web API</span></span>

<span data-ttu-id="71883-114">Después, debe crear una aplicación de API web en su directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="71883-114">Next, you need to create a web API app in your B2C directory.</span></span> <span data-ttu-id="71883-115">Esto proporciona a Azure AD la información que necesita para comunicarse de forma segura con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71883-115">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="71883-116">Para crear una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="71883-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="71883-117">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="71883-117">Be sure to:</span></span>

* <span data-ttu-id="71883-118">Incluir una **aplicación web** o una **API web** en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71883-118">Include a **web app** or **web API** in the application.</span></span>
* <span data-ttu-id="71883-119">Use el **URI de redirección** `https://localhost:44332/` para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="71883-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span></span> <span data-ttu-id="71883-120">Se trata de la ubicación predeterminada del cliente de aplicación web de este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="71883-120">This is the default location of the web app client for this code sample.</span></span>
* <span data-ttu-id="71883-121">Copiar el **identificador de aplicación** asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71883-121">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="71883-122">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="71883-122">You'll need it later.</span></span>
* <span data-ttu-id="71883-123">Escriba un identificador de la aplicación en **URI de id. de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="71883-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="71883-124">Agregue los permisos mediante el menú **Ámbitos publicados**.</span><span class="sxs-lookup"><span data-stu-id="71883-124">Add permissions through the **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="71883-125">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="71883-125">Create your policies</span></span>

<span data-ttu-id="71883-126">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="71883-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="71883-127">Debe crear una directiva para comunicarse con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="71883-127">You will need to create a policy to communicate with Azure AD B2C.</span></span> <span data-ttu-id="71883-128">Se recomienda usar la directiva de registro y de inicio de sesión combinada, tal como se describe en el [artículo de referencia de la directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="71883-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="71883-129">Al crear la directiva, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="71883-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="71883-130">Seleccionar **Nombre para mostrar** y otros atributos de registro en la directiva.</span><span class="sxs-lookup"><span data-stu-id="71883-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="71883-131">Elegir las notificaciones **Nombre para mostrar** e **Id. de objeto** como notificaciones de aplicación en todas las directivas.</span><span class="sxs-lookup"><span data-stu-id="71883-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="71883-132">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="71883-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="71883-133">Copiar el **nombre** de cada directiva después de crearla.</span><span class="sxs-lookup"><span data-stu-id="71883-133">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="71883-134">Necesitará el nombre de la directiva más adelante.</span><span class="sxs-lookup"><span data-stu-id="71883-134">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="71883-135">Cuando haya creado correctamente la directiva, estará listo para crear su aplicación.</span><span class="sxs-lookup"><span data-stu-id="71883-135">After you have successfully created the policy, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="71883-136">Descargar el código</span><span class="sxs-lookup"><span data-stu-id="71883-136">Download the code</span></span>

<span data-ttu-id="71883-137">El código de este tutorial se conserva [en GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="71883-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="71883-138">Puede clonar el ejemplo al ejecutar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="71883-138">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="71883-139">Una vez descargado el código de ejemplo, abra el archivo .sln de Visual Studio para empezar.</span><span class="sxs-lookup"><span data-stu-id="71883-139">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="71883-140">El archivo de solución contiene dos proyectos: `TaskWebApp` y `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="71883-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="71883-141">`TaskWebApp` es una aplicación web MVC con la que el usuario interactúa.</span><span class="sxs-lookup"><span data-stu-id="71883-141">`TaskWebApp` is an MVC web application that the user interacts with.</span></span> <span data-ttu-id="71883-142">`TaskService` es la API web del back-end de la aplicación que almacena la lista de tareas pendientes de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="71883-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="71883-143">En este artículo se describe únicamente la aplicación `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="71883-143">This article will only discuss the `TaskService` application.</span></span> <span data-ttu-id="71883-144">Para más información sobre cómo crear `TaskWebApp` con Azure AD B2C, consulte [nuestro tutorial de aplicaciones web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="71883-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="71883-145">Actualización de la configuración de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="71883-145">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="71883-146">Nuestro ejemplo está configurado para usar las directivas y el identificador de cliente de nuestro inquilino de demostración.</span><span class="sxs-lookup"><span data-stu-id="71883-146">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="71883-147">Si desea usar su propio inquilino, debe hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="71883-147">If you would like to use your own tenant, you will need to do the following:</span></span>

1. <span data-ttu-id="71883-148">Abra `web.config` en el proyecto `TaskService` y reemplace los valores de</span><span class="sxs-lookup"><span data-stu-id="71883-148">Open `web.config` in the `TaskService` project and replace the values for</span></span>
    * <span data-ttu-id="71883-149">`ida:Tenant` por el nombre del inquilino</span><span class="sxs-lookup"><span data-stu-id="71883-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="71883-150">`ida:ClientId` por el identificador de la aplicación de API web</span><span class="sxs-lookup"><span data-stu-id="71883-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="71883-151">`ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"</span><span class="sxs-lookup"><span data-stu-id="71883-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="71883-152">Abra `web.config` en el proyecto `TaskWebApp` y reemplace los valores de</span><span class="sxs-lookup"><span data-stu-id="71883-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>
    * <span data-ttu-id="71883-153">`ida:Tenant` por el nombre del inquilino</span><span class="sxs-lookup"><span data-stu-id="71883-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="71883-154">`ida:ClientId` por el identificador de la aplicación de API web</span><span class="sxs-lookup"><span data-stu-id="71883-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="71883-155">`ida:ClientSecret` por la clave secreta de aplicación web</span><span class="sxs-lookup"><span data-stu-id="71883-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="71883-156">`ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"</span><span class="sxs-lookup"><span data-stu-id="71883-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="71883-157">`ida:EditProfilePolicyId` por el nombre de la directiva "Editar perfil"</span><span class="sxs-lookup"><span data-stu-id="71883-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="71883-158">`ida:ResetPasswordPolicyId` por el nombre de la directiva "Restablecer contraseña"</span><span class="sxs-lookup"><span data-stu-id="71883-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-the-api"></a><span data-ttu-id="71883-159">Proteger la API</span><span class="sxs-lookup"><span data-stu-id="71883-159">Secure the API</span></span>

<span data-ttu-id="71883-160">Si tiene un cliente que llama a la API, puede proteger la API (por ejemplo `TaskService`) con tokens de portador de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="71883-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="71883-161">Esto garantiza que cada solicitud a la API solo será válida si la solicitud tiene un token de portador.</span><span class="sxs-lookup"><span data-stu-id="71883-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span></span> <span data-ttu-id="71883-162">La API puede aceptar y validar tokens de portador mediante la biblioteca de Open Web Interface for .NET (OWIN) de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="71883-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="71883-163">Instalar OWIN</span><span class="sxs-lookup"><span data-stu-id="71883-163">Install OWIN</span></span>

<span data-ttu-id="71883-164">Empiece instalando la canalización de autenticación OAuth de OWIN mediante la consola del Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71883-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="71883-165">Este modo se instalará el middleware de OWIN que aceptará y validará los tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="71883-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="71883-166">Agregar una clase de inicio de OWIN</span><span class="sxs-lookup"><span data-stu-id="71883-166">Add an OWIN startup class</span></span>

<span data-ttu-id="71883-167">Agregue una clase de inicio OWIN a la API llamada `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="71883-167">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="71883-168">Haga clic con el botón derecho en el proyecto, seleccione **Agregar** y **Nuevo elemento**; después, busque OWIN.</span><span class="sxs-lookup"><span data-stu-id="71883-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="71883-169">El middleware OWIN invocará el método `Configuration(…)` al iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71883-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="71883-170">En nuestro ejemplo, hemos cambiado la declaración de clase a `public partial class Startup` y hemos implementado la otra parte de la clase en `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="71883-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="71883-171">En el método `Configuration`, se agrega una llamada a `ConfigureAuth`, que se define en `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="71883-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="71883-172">Después de las modificaciones, `Startup.cs` es similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="71883-172">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="71883-173">Configurar la autenticación de OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="71883-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="71883-174">Abra el archivo `App_Start\Startup.Auth.cs` e implemente el método `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="71883-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="71883-175">Por ejemplo, podría ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="71883-175">For example, it could look like the following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure the authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where the audience of the token is equal to the client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-the-task-controller"></a><span data-ttu-id="71883-176">Proteger el controlador de la tarea</span><span class="sxs-lookup"><span data-stu-id="71883-176">Secure the task controller</span></span>

<span data-ttu-id="71883-177">Cuando la aplicación esté configurada para usar la autenticación de OAuth 2.0, puede proteger su API web agregando una etiqueta `[Authorize]` al controlador de tareas.</span><span class="sxs-lookup"><span data-stu-id="71883-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span></span> <span data-ttu-id="71883-178">Este es el controlador donde tiene lugar cualquier manipulación de la lista de tareas pendientes, por lo que debe proteger todo el controlador en el nivel de clase.</span><span class="sxs-lookup"><span data-stu-id="71883-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span></span> <span data-ttu-id="71883-179">También puede agregar la etiqueta `[Authorize]` a determinadas acciones para un control específico.</span><span class="sxs-lookup"><span data-stu-id="71883-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a><span data-ttu-id="71883-180">Obtener la información del usuario del token</span><span class="sxs-lookup"><span data-stu-id="71883-180">Get user information from the token</span></span>

<span data-ttu-id="71883-181">`TasksController` almacena las tareas en una base de datos donde cada tarea tiene un usuario asociado que la "posee".</span><span class="sxs-lookup"><span data-stu-id="71883-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span></span> <span data-ttu-id="71883-182">El propietario se identifica por el **Id. de objeto** del usuario.</span><span class="sxs-lookup"><span data-stu-id="71883-182">The owner is identified by the user's **object ID**.</span></span> <span data-ttu-id="71883-183">(por eso necesita agregar el Id. de objeto como una notificación de aplicación en todas sus directivas).</span><span class="sxs-lookup"><span data-stu-id="71883-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-the-permissions-in-the-token"></a><span data-ttu-id="71883-184">Validación de los permisos en el token</span><span class="sxs-lookup"><span data-stu-id="71883-184">Validate the permissions in the token</span></span>

<span data-ttu-id="71883-185">Un requisito común de las API web es validar los "ámbitos" presentes en el token.</span><span class="sxs-lookup"><span data-stu-id="71883-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="71883-186">De esta forma se garantiza que el usuario ha dado su consentimiento a los permisos necesarios para acceder al servicio de lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="71883-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "The Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="71883-187">Ejecutar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="71883-187">Run the sample app</span></span>

<span data-ttu-id="71883-188">Por último, compile y ejecute `TaskWebApp` y `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="71883-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="71883-189">Cree algunas tareas en la lista de tareas del usuario y observe cómo se conservan en la API incluso después de detener y reiniciar el cliente.</span><span class="sxs-lookup"><span data-stu-id="71883-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="71883-190">Editar sus directivas</span><span class="sxs-lookup"><span data-stu-id="71883-190">Edit your policies</span></span>

<span data-ttu-id="71883-191">Una vez que haya protegido una API mediante el uso de Azure AD B2C, puede experimentar con la directiva de inicio de sesión y registro, y ver los efectos (o la ausencia de estos) en la API.</span><span class="sxs-lookup"><span data-stu-id="71883-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span></span> <span data-ttu-id="71883-192">Puede manipular las notificaciones de aplicación en las directivas y modificar la información de usuario que está disponible en la API web.</span><span class="sxs-lookup"><span data-stu-id="71883-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span></span> <span data-ttu-id="71883-193">Las notificaciones que agregue estarán disponibles para la API web de MVC de .NET en el objeto `ClaimsPrincipal` , como se describió antes en este artículo.</span><span class="sxs-lookup"><span data-stu-id="71883-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span></span>
