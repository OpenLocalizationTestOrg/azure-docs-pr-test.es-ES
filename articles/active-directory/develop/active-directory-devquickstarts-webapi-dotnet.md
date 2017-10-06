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
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a>Ayuda para proteger una API web con tokens portadores de Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Si va a compilar una aplicación que proporciona acceso a recursos de tooprotected, necesita tooknow cómo tooprevent ilícita tener acceso a recursos de toothose.
Azure Active Directory (Azure AD) simplifica el proceso y sencillo toohelp protege una API web mediante tokens de acceso de portador de OAuth 2.0 con solo unas pocas líneas de código.

En las aplicaciones web ASP.NET, puede realizar esta protección mediante el uso de la implementación de Microsoft de Hola de hello controlada por la Comunidad software intermedio OWIN incluido en .NET Framework 4.5. Aquí vamos a usar OWIN toobuild una API web de "tooDo lista" que:

* Designar las API que están protegidas.
* Valida que las llamadas de API web de hello contienen un token de acceso válido.

toobuild hello tooDo API de la lista, primero debe:

1. Registrar una aplicación con Azure AD.
2. Configurar la canalización de autenticación de hello aplicación toouse hello OWIN.
3. Configurar un cliente aplicación toocall Hola API web.

tooget iniciado, [descargar esqueleto de aplicación Hola](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Cualquiera de los dos es una solución de Visual Studio 2013. También tenga a un inquilino de Azure AD en qué tooregister su aplicación. Si aún no tiene uno, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).

## <a name="step-1-register-an-application-with-azure-ad"></a>Paso 1: Registro de una aplicación con Azure AD
toohelp proteger la aplicación, primero necesita toocreate una aplicación en su inquilino y proporcionar algunos fragmentos de información clave a Azure AD.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. En la barra superior de hello, haga clic en su cuenta. Hola **Directory** elija inquilino hello Azure AD en el que desea tooregister la aplicación.

3. Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.

4. Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.

5. Siga las indicaciones de Hola y crear un nuevo **aplicación Web o API Web**.
  * **Nombre** describe su toousers de aplicación. Escriba **tooDo servicio de la lista**.
  * **Uri de redireccionamiento** es una combinación de esquema y la cadena que Azure AD usa tooreturn cualquiera símbolos (token) que la aplicación ha solicitado. Escriba `https://localhost:44321/` para este valor.

6. De hello **configuración** -> **propiedades** página de la aplicación, actualice Hola App ID URI. Especifique un identificador específico del inquilino. Por ejemplo, escriba: `https://contoso.onmicrosoft.com/TodoListService`.

7. Guardar configuración de Hola. Vulnerable portal hello, porque también necesitará tooregister la aplicación cliente en breve.

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Paso 2: Configurar la canalización de autenticación de hello aplicación toouse hello OWIN
las solicitudes entrantes de toovalidate y símbolos (tokens), deberá tooset seguridad su toocommunicate de aplicación con Azure AD.

1. toobegin, abra la solución de Hola y Agregar proyecto de toohello de paquetes de NuGet TodoListService de hello OWIN middleware mediante Hola Package Manager Console.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. Agregue un proyecto TodoListService de inicio de OWIN clases toohello denominado `Startup.cs`.  Proyecto de Hola de menú contextual, seleccione **agregar** > **nuevo elemento**y, a continuación, busque **OWIN**. middleware de OWIN Hola invocará hello `Configuration(…)` método cuando se inicia la aplicación.

3. Cambie la declaración de clase de hello demasiado`public partial class Startup`. Ya hemos implementado parte de esta clase en otro archivo. Hola `Configuration(…)` método, realizar una llamada demasiado`ConfgureAuth(…)` tooset la autenticación para la aplicación web.

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. Archivo abierto hello `App_Start\Startup.Auth.cs` e implementar hello `ConfigureAuth(…)` método. Hola parámetros que se proporcionan en `WindowsAzureActiveDirectoryBearerAuthenticationOptions` servirá como coordenadas para su toocommunicate de aplicación con Azure AD.

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

5. Ahora puede usar `[Authorize]` toohelp atributos proteger los controladores y acciones con la autenticación de portador de JSON Web Token (JWT). Decorar hello `Controllers\TodoListController.cs` clase con una etiqueta de autorizar. Esto forzará Hola usuario toosign en antes de acceder a esa página.

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    Cuando un llamador autorizado correctamente invoca uno de hello `TodoListController` API, acción de Hola podría necesita acceder a tooinformation sobre llamador Hola. OWIN proporciona acceso toohello notificaciones dentro de token de portador de hello mediante hello `ClaimsPrincpal` objeto.  

6. Un requisito común de las API web es toovalidate Hola "ámbitos" está presentes en el token de Hola. Esto garantiza que el usuario Hola ha dado su consentimiento toohello permisos necesarios tooaccess hello tooDo servicio de la lista.

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

7. Abra hello `web.config` un archivo en la raíz de Hola de proyecto TodoListService de Hola y escriba los valores de configuración en hello `<appSettings>` sección.
  * `ida:Tenant`es el nombre de hello del inquilino de Azure AD: por ejemplo, contoso.onmicrosoft.com.
  * `ida:Audience`se Hola App ID URI de aplicación Hola que escribió en hello portal de Azure.

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a>Paso 3: Configurar una aplicación cliente y ejecutar el servicio de Hola
Para poder ver hello tooDo servicio de la lista en acción, debe a cliente de la lista de tooconfigure hello tooDo para que pueda obtener tokens de Azure AD y realiza llamadas a un servicio toohello.

1. Volver atrás toohello [portal de Azure](https://portal.azure.com).

2. Crear una nueva aplicación en su inquilino de Azure AD y seleccione **aplicación cliente nativa** en el símbolo del sistema de hello resultante.
  * **Nombre** describe su toousers de aplicación.
  * Escriba `http://TodoListClient/` para hello **Uri de redireccionamiento** valor.

3. Cuando termine de registro, Azure AD le asigna una aplicación de tooyour de Id. de aplicación exclusivo. Necesitará este valor en pasos de hello, por lo tanto cópiela desde la página de aplicación Hola.

4. De hello **configuración** página, seleccione **permisos necesarios**y, a continuación, seleccione **agregar**. Busque y seleccione hello tooDo servicio de la lista, agregue hello **acceso TodoListService** permiso en **permisos delegados**y, a continuación, haga clic en **realiza**.

5. En Visual Studio, abra `App.config` en Hola TodoListClient proyecto y, a continuación, escriba los valores de configuración en hello `<appSettings>` sección.

  * `ida:Tenant`es el nombre de hello del inquilino de Azure AD: por ejemplo, contoso.onmicrosoft.com.
  * `ida:ClientId`es el Id. de aplicación de Hola que copió de hello portal de Azure.
  * `todo:TodoListResourceId`es hello App ID URI de hello tooDo aplicación de servicio de la lista que escribió en hello portal de Azure.

## <a name="next-steps"></a>Pasos siguientes
Por último, limpie, compile y ejecute cada proyecto. Si no lo ha hecho ya, ahora es a Hola tiempo toocreate un nuevo usuario en el inquilino con un *. dominio onmicrosoft.com. Inicie sesión en el cliente de la lista toohello tooDo a ese usuario y agregar la lista de tareas del usuario algunas tareas toohello.

Como referencia, está disponible en el ejemplo de Hola finalizado (sin los valores de configuración) [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Ahora puede mover en escenarios de identidad toomore.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
