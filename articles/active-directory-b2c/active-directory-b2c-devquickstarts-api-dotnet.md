---
title: aaaAzure AD B2C | Documentos de Microsoft
description: "¿Cómo toobuild una API Web de .NET mediante el uso de Azure Active B2C de directorio, proteger mediante tokens de acceso de OAuth 2.0 para la autenticación."
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
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="e4fec-103">Azure Active Directory B2C: Creación de una API web de .NET</span><span class="sxs-lookup"><span data-stu-id="e4fec-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="e4fec-104">Con Azure Active Directory (Azure AD) B2C, puede proteger una API web mediante el uso de tokens de acceso de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="e4fec-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="e4fec-105">Estos tokens permiten que al cliente toohello de tooauthenticate de aplicaciones de la API.</span><span class="sxs-lookup"><span data-stu-id="e4fec-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="e4fec-106">Este artículo muestra cómo toocreate una API de .NET MVC "lista de tareas pendientes" permite a los usuarios del cliente de las tareas de tooCRUD de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e4fec-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="e4fec-107">Hola web API se protege mediante Azure AD B2C y solo permite a los usuarios autenticados toomanage su lista de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="e4fec-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="e4fec-108">Creación de un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e4fec-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="e4fec-109">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="e4fec-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="e4fec-110">Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="e4fec-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="e4fec-111">Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar con esta guía.</span><span class="sxs-lookup"><span data-stu-id="e4fec-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="e4fec-112">aplicación de cliente de Hello y API web deben usar directorio de hello misma instancia de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e4fec-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="e4fec-113">Creación de una API web</span><span class="sxs-lookup"><span data-stu-id="e4fec-113">Create a web API</span></span>

<span data-ttu-id="e4fec-114">A continuación, debe toocreate una aplicación de API web en el directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="e4fec-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="e4fec-115">Esto proporciona información de Azure AD que necesita toosecurely comunicarse con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4fec-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="e4fec-116">toocreate una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="e4fec-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="e4fec-117">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="e4fec-117">Be sure to:</span></span>

* <span data-ttu-id="e4fec-118">Incluir un **aplicación web** o **web API** en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e4fec-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="e4fec-119">Hola de uso **URI de redireccionamiento** `https://localhost:44332/` para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4fec-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="e4fec-120">Se trata de una ubicación predeterminada de Hola de cliente de la aplicación hello web para este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="e4fec-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="e4fec-121">Hola copia **Id. de aplicación** decir tooyour asignado aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4fec-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="e4fec-122">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="e4fec-122">You'll need it later.</span></span>
* <span data-ttu-id="e4fec-123">Escriba un identificador de la aplicación en **URI de id. de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="e4fec-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="e4fec-124">Agregar permisos a través de hello **publicado ámbitos** menú.</span><span class="sxs-lookup"><span data-stu-id="e4fec-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="e4fec-125">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="e4fec-125">Create your policies</span></span>

<span data-ttu-id="e4fec-126">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e4fec-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="e4fec-127">Deberá toocreate un toocommunicate de directiva con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e4fec-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="e4fec-128">Se recomienda utilizando Hola combina sesión-up/inicio de sesión de directiva, como se describe en hello [artículo de referencia de directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e4fec-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="e4fec-129">Al crear la directiva, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e4fec-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="e4fec-130">Seleccionar **Nombre para mostrar** y otros atributos de registro en la directiva.</span><span class="sxs-lookup"><span data-stu-id="e4fec-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="e4fec-131">Elegir las notificaciones **Nombre para mostrar** e **Id. de objeto** como notificaciones de aplicación en todas las directivas.</span><span class="sxs-lookup"><span data-stu-id="e4fec-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="e4fec-132">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="e4fec-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="e4fec-133">Hola copia **nombre** de cada directiva después de haberlo creado.</span><span class="sxs-lookup"><span data-stu-id="e4fec-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="e4fec-134">Necesitará el nombre de directiva de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="e4fec-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="e4fec-135">Después de que ha creado correctamente la directiva de hello, está listo toobuild la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4fec-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="e4fec-136">Descargar código de hello</span><span class="sxs-lookup"><span data-stu-id="e4fec-136">Download hello code</span></span>

<span data-ttu-id="e4fec-137">código de Hello para este tutorial se mantiene en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="e4fec-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="e4fec-138">Puede clonar el ejemplo hello ejecutando:</span><span class="sxs-lookup"><span data-stu-id="e4fec-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="e4fec-139">Después de descargar el código de ejemplo de Hola, inició tooget de archivo .sln de hello abrir Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4fec-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="e4fec-140">archivo de solución de Hello contiene dos proyectos: `TaskWebApp` y `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="e4fec-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="e4fec-141">`TaskWebApp`es una aplicación web MVC que Hola usuario interactúa con.</span><span class="sxs-lookup"><span data-stu-id="e4fec-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="e4fec-142">`TaskService`es la API de web back-end de la aplicación hello que almacena la lista de tareas pendientes de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="e4fec-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="e4fec-143">Este artículo describe solo hello `TaskService` aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4fec-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="e4fec-144">toolearn cómo toobuild `TaskWebApp` con Azure AD B2C, consulte [nuestro tutorial de aplicación web de .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="e4fec-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="e4fec-145">Actualizar configuración de hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e4fec-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="e4fec-146">Nuestro ejemplo es toouse configurado Hola directivas e ID de cliente de nuestro inquilino de demostración.</span><span class="sxs-lookup"><span data-stu-id="e4fec-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="e4fec-147">Si desea que toouse su propio inquilino, necesitará hello toodo siguientes:</span><span class="sxs-lookup"><span data-stu-id="e4fec-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="e4fec-148">Abra `web.config` en hello `TaskService` de proyectos y valores de hello para</span><span class="sxs-lookup"><span data-stu-id="e4fec-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="e4fec-149">`ida:Tenant` por el nombre del inquilino</span><span class="sxs-lookup"><span data-stu-id="e4fec-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="e4fec-150">`ida:ClientId` por el identificador de la aplicación de API web</span><span class="sxs-lookup"><span data-stu-id="e4fec-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="e4fec-151">`ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"</span><span class="sxs-lookup"><span data-stu-id="e4fec-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="e4fec-152">Abra `web.config` en hello `TaskWebApp` de proyectos y valores de hello para</span><span class="sxs-lookup"><span data-stu-id="e4fec-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="e4fec-153">`ida:Tenant` por el nombre del inquilino</span><span class="sxs-lookup"><span data-stu-id="e4fec-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="e4fec-154">`ida:ClientId` por el identificador de la aplicación de API web</span><span class="sxs-lookup"><span data-stu-id="e4fec-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="e4fec-155">`ida:ClientSecret` por la clave secreta de aplicación web</span><span class="sxs-lookup"><span data-stu-id="e4fec-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="e4fec-156">`ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"</span><span class="sxs-lookup"><span data-stu-id="e4fec-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="e4fec-157">`ida:EditProfilePolicyId` por el nombre de la directiva "Editar perfil"</span><span class="sxs-lookup"><span data-stu-id="e4fec-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="e4fec-158">`ida:ResetPasswordPolicyId` por el nombre de la directiva "Restablecer contraseña"</span><span class="sxs-lookup"><span data-stu-id="e4fec-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="e4fec-159">Proteger API Hola</span><span class="sxs-lookup"><span data-stu-id="e4fec-159">Secure hello API</span></span>

<span data-ttu-id="e4fec-160">Si tiene un cliente que llama a la API, puede proteger la API (por ejemplo `TaskService`) con tokens de portador de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="e4fec-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="e4fec-161">Esto garantiza que cada API de tooyour solicitud solo serán válido si la solicitud de hello tiene un token de portador.</span><span class="sxs-lookup"><span data-stu-id="e4fec-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="e4fec-162">La API puede aceptar y validar tokens de portador mediante la biblioteca de Open Web Interface for .NET (OWIN) de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e4fec-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="e4fec-163">Instalar OWIN</span><span class="sxs-lookup"><span data-stu-id="e4fec-163">Install OWIN</span></span>

<span data-ttu-id="e4fec-164">Empiece instalando la canalización de autenticación de OAuth de OWIN de hello mediante el uso de hello consola de administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4fec-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="e4fec-165">Este modo se instalará Hola middleware OWIN que aceptará y validará los tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="e4fec-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="e4fec-166">Agregar una clase de inicio de OWIN</span><span class="sxs-lookup"><span data-stu-id="e4fec-166">Add an OWIN startup class</span></span>

<span data-ttu-id="e4fec-167">Agrega una clase de inicio OWIN toohello API denominado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="e4fec-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="e4fec-168">Haga doble clic en el proyecto de hello, seleccione **agregar** y **nuevo elemento**y, a continuación, busque OWIN.</span><span class="sxs-lookup"><span data-stu-id="e4fec-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="e4fec-169">middleware de OWIN Hola invocará hello `Configuration(…)` método cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4fec-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="e4fec-170">En nuestro ejemplo, hemos cambiado declaración de clase de hello demasiado`public partial class Startup` e implementado Hola otra parte de la clase hello en `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="e4fec-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="e4fec-171">Hola interior `Configuration` método, agregamos una llamada demasiado`ConfigureAuth`, que se define en `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="e4fec-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="e4fec-172">Después de las modificaciones de hello, `Startup.cs` Hola siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="e4fec-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

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

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="e4fec-173">Configurar la autenticación de OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="e4fec-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="e4fec-174">Archivo abierto hello `App_Start\Startup.Auth.cs`e implementar hello `ConfigureAuth(...)` método.</span><span class="sxs-lookup"><span data-stu-id="e4fec-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="e4fec-175">Por ejemplo, podría verse como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e4fec-175">For example, it could look like hello following:</span></span>

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
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a><span data-ttu-id="e4fec-176">Controlador de la tarea de Hola segura</span><span class="sxs-lookup"><span data-stu-id="e4fec-176">Secure hello task controller</span></span>

<span data-ttu-id="e4fec-177">Una vez aplicación hello autenticación toouse configurado OAuth 2.0, puede proteger su API web agregando un `[Authorize]` controlador de tareas de toohello de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="e4fec-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="e4fec-178">Se trata de controlador de Hola donde manipulación de lista de todas las tareas realiza, por lo que debería proteger el controlador todo de hello en el nivel de clase de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4fec-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="e4fec-179">También puede agregar hello `[Authorize]` etiqueta tooindividual acciones para un control más minucioso.</span><span class="sxs-lookup"><span data-stu-id="e4fec-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="e4fec-180">Obtener la información de usuario de hello token</span><span class="sxs-lookup"><span data-stu-id="e4fec-180">Get user information from hello token</span></span>

<span data-ttu-id="e4fec-181">`TasksController`almacena las tareas en una base de datos donde cada tarea tiene un usuario asociado a la tarea hello "propietario".</span><span class="sxs-lookup"><span data-stu-id="e4fec-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="e4fec-182">propietario de Hola se identifica mediante del usuario de hello **Id. de objeto**.</span><span class="sxs-lookup"><span data-stu-id="e4fec-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="e4fec-183">(Por lo tanto, necesita tooadd Hola el Id. de objeto como una aplicación de notificación en todas las directivas.)</span><span class="sxs-lookup"><span data-stu-id="e4fec-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="e4fec-184">Validar los permisos de hello en el token de Hola</span><span class="sxs-lookup"><span data-stu-id="e4fec-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="e4fec-185">Un requisito común de las API web es toovalidate Hola "ámbitos" está presentes en el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4fec-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="e4fec-186">Esto garantiza que ese usuario Hola ha dado su consentimiento de servicio de lista de tareas pendientes de toohello permisos tooaccess necesario Hola.</span><span class="sxs-lookup"><span data-stu-id="e4fec-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="e4fec-187">Ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="e4fec-187">Run hello sample app</span></span>

<span data-ttu-id="e4fec-188">Por último, compile y ejecute `TaskWebApp` y `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="e4fec-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="e4fec-189">Crear algunas tareas en la lista de tareas del usuario de hello y observe cómo se conservan en hello API incluso después de detener y reiniciar al cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4fec-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="e4fec-190">Editar sus directivas</span><span class="sxs-lookup"><span data-stu-id="e4fec-190">Edit your policies</span></span>

<span data-ttu-id="e4fec-191">Después de haber protegido una API mediante el uso de Azure AD B2C, puede experimentar con la directiva de inicio de sesión-en/sesión-up y efectos de Hola de vista (o ausencia de las mismas) en hello API.</span><span class="sxs-lookup"><span data-stu-id="e4fec-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="e4fec-192">Puede manipular notificaciones de la aplicación hello en las directivas de Hola y cambiar información de usuario de Hola que está disponible en hello web API.</span><span class="sxs-lookup"><span data-stu-id="e4fec-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="e4fec-193">Las notificaciones que se agregan estarán disponibles tooyour .NET MVC web API en hello `ClaimsPrincipal` de objeto, como se describe anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="e4fec-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
