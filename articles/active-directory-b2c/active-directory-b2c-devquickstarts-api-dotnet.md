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
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C: Creación de una API web de .NET

Con Azure Active Directory (Azure AD) B2C, puede proteger una API web mediante el uso de tokens de acceso de OAuth 2.0. Estos tokens permiten que al cliente toohello de tooauthenticate de aplicaciones de la API. Este artículo muestra cómo toocreate una API de .NET MVC "lista de tareas pendientes" permite a los usuarios del cliente de las tareas de tooCRUD de aplicaciones. Hola web API se protege mediante Azure AD B2C y solo permite a los usuarios autenticados toomanage su lista de tareas pendientes.

## <a name="create-an-azure-ad-b2c-directory"></a>Creación de un directorio de Azure AD B2C

Para poder usar Azure AD B2C, debe crear un directorio o inquilino. Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc. Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar con esta guía.

> [!NOTE]
> aplicación de cliente de Hello y API web deben usar directorio de hello misma instancia de Azure AD B2C.
>

## <a name="create-a-web-api"></a>Creación de una API web

A continuación, debe toocreate una aplicación de API web en el directorio B2C. Esto proporciona información de Azure AD que necesita toosecurely comunicarse con la aplicación. toocreate una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md). Asegúrese de:

* Incluir un **aplicación web** o **web API** en aplicación hello.
* Hola de uso **URI de redireccionamiento** `https://localhost:44332/` para la aplicación web de Hola. Se trata de una ubicación predeterminada de Hola de cliente de la aplicación hello web para este ejemplo de código.
* Hola copia **Id. de aplicación** decir tooyour asignado aplicación. Lo necesitará más adelante.
* Escriba un identificador de la aplicación en **URI de id. de aplicación**.
* Agregar permisos a través de hello **publicado ámbitos** menú.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Crear sus directivas

En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md). Deberá toocreate un toocommunicate de directiva con Azure AD B2C. Se recomienda utilizando Hola combina sesión-up/inicio de sesión de directiva, como se describe en hello [artículo de referencia de directiva](active-directory-b2c-reference-policies.md). Al crear la directiva, tenga en cuenta lo siguiente:

* Seleccionar **Nombre para mostrar** y otros atributos de registro en la directiva.
* Elegir las notificaciones **Nombre para mostrar** e **Id. de objeto** como notificaciones de aplicación en todas las directivas. Puede elegir también otras notificaciones.
* Hola copia **nombre** de cada directiva después de haberlo creado. Necesitará el nombre de directiva de hello más tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Después de que ha creado correctamente la directiva de hello, está listo toobuild la aplicación.

## <a name="download-hello-code"></a>Descargar código de hello

código de Hello para este tutorial se mantiene en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Puede clonar el ejemplo hello ejecutando:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Después de descargar el código de ejemplo de Hola, inició tooget de archivo .sln de hello abrir Visual Studio. archivo de solución de Hello contiene dos proyectos: `TaskWebApp` y `TaskService`. `TaskWebApp`es una aplicación web MVC que Hola usuario interactúa con. `TaskService`es la API de web back-end de la aplicación hello que almacena la lista de tareas pendientes de cada usuario. Este artículo describe solo hello `TaskService` aplicación. toolearn cómo toobuild `TaskWebApp` con Azure AD B2C, consulte [nuestro tutorial de aplicación web de .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Actualizar configuración de hello Azure AD B2C

Nuestro ejemplo es toouse configurado Hola directivas e ID de cliente de nuestro inquilino de demostración. Si desea que toouse su propio inquilino, necesitará hello toodo siguientes:

1. Abra `web.config` en hello `TaskService` de proyectos y valores de hello para
    * `ida:Tenant` por el nombre del inquilino
    * `ida:ClientId` por el identificador de la aplicación de API web
    * `ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"

2. Abra `web.config` en hello `TaskWebApp` de proyectos y valores de hello para
    * `ida:Tenant` por el nombre del inquilino
    * `ida:ClientId` por el identificador de la aplicación de API web
    * `ida:ClientSecret` por la clave secreta de aplicación web
    * `ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"
    * `ida:EditProfilePolicyId` por el nombre de la directiva "Editar perfil"
    * `ida:ResetPasswordPolicyId` por el nombre de la directiva "Restablecer contraseña"


## <a name="secure-hello-api"></a>Proteger API Hola

Si tiene un cliente que llama a la API, puede proteger la API (por ejemplo `TaskService`) con tokens de portador de OAuth 2.0. Esto garantiza que cada API de tooyour solicitud solo serán válido si la solicitud de hello tiene un token de portador. La API puede aceptar y validar tokens de portador mediante la biblioteca de Open Web Interface for .NET (OWIN) de Microsoft.

### <a name="install-owin"></a>Instalar OWIN

Empiece instalando la canalización de autenticación de OAuth de OWIN de hello mediante el uso de hello consola de administrador de paquetes de Visual Studio.

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

Este modo se instalará Hola middleware OWIN que aceptará y validará los tokens de portador.

### <a name="add-an-owin-startup-class"></a>Agregar una clase de inicio de OWIN

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

### <a name="configure-oauth-20-authentication"></a>Configurar la autenticación de OAuth 2.0

Archivo abierto hello `App_Start\Startup.Auth.cs`e implementar hello `ConfigureAuth(...)` método. Por ejemplo, podría verse como Hola siguiente:

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

### <a name="secure-hello-task-controller"></a>Controlador de la tarea de Hola segura

Una vez aplicación hello autenticación toouse configurado OAuth 2.0, puede proteger su API web agregando un `[Authorize]` controlador de tareas de toohello de etiqueta. Se trata de controlador de Hola donde manipulación de lista de todas las tareas realiza, por lo que debería proteger el controlador todo de hello en el nivel de clase de Hola. También puede agregar hello `[Authorize]` etiqueta tooindividual acciones para un control más minucioso.

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>Obtener la información de usuario de hello token

`TasksController`almacena las tareas en una base de datos donde cada tarea tiene un usuario asociado a la tarea hello "propietario". propietario de Hola se identifica mediante del usuario de hello **Id. de objeto**. (Por lo tanto, necesita tooadd Hola el Id. de objeto como una aplicación de notificación en todas las directivas.)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>Validar los permisos de hello en el token de Hola

Un requisito común de las API web es toovalidate Hola "ámbitos" está presentes en el token de Hola. Esto garantiza que ese usuario Hola ha dado su consentimiento de servicio de lista de tareas pendientes de toohello permisos tooaccess necesario Hola.

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

## <a name="run-hello-sample-app"></a>Ejecutar la aplicación de ejemplo de Hola

Por último, compile y ejecute `TaskWebApp` y `TaskService`. Crear algunas tareas en la lista de tareas del usuario de hello y observe cómo se conservan en hello API incluso después de detener y reiniciar al cliente de Hola.

## <a name="edit-your-policies"></a>Editar sus directivas

Después de haber protegido una API mediante el uso de Azure AD B2C, puede experimentar con la directiva de inicio de sesión-en/sesión-up y efectos de Hola de vista (o ausencia de las mismas) en hello API. Puede manipular notificaciones de la aplicación hello en las directivas de Hola y cambiar información de usuario de Hola que está disponible en hello web API. Las notificaciones que se agregan estarán disponibles tooyour .NET MVC web API en hello `ClaimsPrincipal` de objeto, como se describe anteriormente en este artículo.
