---
title: "aaaService autenticación principal para las aplicaciones de API de servicio de aplicaciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de la aplicación de tooprotect una API de servicio de aplicaciones de Azure para escenarios de servicio al servicio."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Autenticación de entidad de servicio para Aplicaciones de API en el Servicio de aplicaciones de Azure
## <a name="overview"></a>Información general
Este artículo se explica cómo toouse autenticación de servicio de aplicaciones para *interno* acceder a las aplicaciones de tooAPI. Un escenario interno es donde haya una aplicación de API que desea toobe pueden utilizar su propio código de aplicación. Hola recomienda forma tooimplement este escenario en el servicio de aplicaciones se toouse Azure AD tooprotect Hola llama aplicación de API. Se llama a la aplicación de API de hello protegido con un token de portador que obtendrá de Azure AD proporcionando las credenciales (entidad de servicio) de identidad de la aplicación. Para alternativas toousing Azure AD, vea hello **autenticación del servicio a servicio** sección de hello [información general de la autenticación de servicio de aplicaciones de Azure](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

En este artículo, aprenderá lo siguiente:

* La aplicación de tooprotect una API de Azure Active Directory (Azure AD) toouse de acceso no autenticado.
* La aplicación de tooconsume API protegida desde una aplicación de API, aplicación web o aplicación móvil mediante el uso de credenciales de la entidad de seguridad (identidad de aplicación) de servicio de Azure AD. Para obtener información acerca de cómo tooconsume desde una aplicación de lógica, consulte [mediante la API personalizada hospedada en el servicio de aplicaciones a las aplicaciones lógicas](../logic-apps/logic-apps-custom-hosted-api.md).
* Cómo toomake seguro de que Hola protegido aplicación de API no se puede llamar desde un explorador, para iniciar sesión a los usuarios.
* Cómo toomake seguro de que Hola protegido aplicación de API solo puede llamarse mediante un determinado entidad de servicio de Azure AD.

artículo de Hello contiene dos secciones:

* Hola [cómo tooconfigure service autenticación principal en el servicio de aplicación de Azure](#authconfig) sección se explica cómo general tooconfigure autenticación para cualquier aplicación de API y cómo hello tooconsume protección de aplicación de API. En esta sección se aplica por igual marcos tooall compatibles con el servicio de aplicación, incluido. NET, Node.js y Java.
* A partir de hello [continuar tutoriales de introducción a .NET de hello](#tutorialstart) sección tutorial Hola le guía a través de configuración de un escenario de "acceso interno" para una aplicación de ejemplo de .NET en ejecución en el servicio de aplicación. 

## <a id="authconfig"></a>Cómo tooconfigure service autenticación principal en el servicio de aplicación de Azure
Esta sección proporciona instrucciones generales que se aplican a la aplicación de API de tooany. Para pasos específicos toohello tooDo aplicación de ejemplo de .NET de la lista, vaya demasiado[continuar serie de tutoriales de aplicaciones de API de .NET de hello](#tutorialstart).

1. Hola [portal de Azure](https://portal.azure.com/), navegue toohello **configuración** hoja de aplicación de hello API que desee tooprotect y, a continuación, busque hello **características** sección y haga clic en **Autenticación / autorización**.
   
    ![Autenticación/autorización en el Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Hola **autenticación / autorización** hoja, haga clic en **en**.
3. Hola **tootake de acción cuando no se autentica la solicitud** lista desplegable, seleccione **iniciar sesión con Azure Active Directory** .
4. En **Proveedores de autenticación,** seleccione **Azure Active Directory**.
   
    ![Hoja Autenticación/autorización del Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Configurar hello **configuración de Azure Active Directory** hoja toocreate un Azure nueva aplicación de AD, o utilizar una aplicación de Azure AD existente si ya tiene una que desea toouse.
   
    En los escenarios internos normalmente hay una aplicación de API que llama a una aplicación de API. Puede usar aplicaciones de AD independientes para cada aplicación de API o una sola aplicación de Azure AD.
   
    Para obtener instrucciones detalladas sobre esta hoja, vea [cómo tooconfigure su inicio de sesión de Azure Active Directory de servicio de aplicaciones aplicación toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Cuando haya terminado con la hoja de configuración de proveedor de autenticación de hello, haga clic en **Aceptar**.
7. Hola **autenticación / autorización** hoja, haga clic en **guardar**.
   
    ![Haga clic en Guardar](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Cuando esto sucede, servicio de aplicaciones solo permite las solicitudes de los llamadores de inquilino de Azure AD Hola configurado. No se requiere ningún código de autenticación o autorización de aplicación de API de hello protegido. Hello token de portador se pasa toohello API aplicación junto con notificaciones de uso frecuente en encabezados HTTP, y puede leer esa información en código toovalidate que las solicitudes proceden de un determinado autor de llamada, como una entidad de servicio.

Esta funcionalidad de autenticación funciona Hola admite ese servicio de aplicaciones de igual en todos los idiomas, incluido. NET, Node.js y Java. 

#### <a name="how-tooconsume-hello-protected-api-app"></a>Cómo tooconsume Hola protección de aplicación de API
llamador de Hello debe proporcionar un token de portador de Azure AD con llamadas a API. tooget un token de portador con credenciales de servicio principal, el llamador de hello usa biblioteca de autenticación de Active Directory (ADAL para [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), o [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). tooget un token, código de hello que llama a AAL proporciona hello tooADAL siguiente información:

* nombre de Hello del inquilino de Azure AD.
* Hola cliente y el identificador de secreto del cliente (clave de aplicación) de aplicación hello Azure AD asociado con un llamador de Hola.
* Hola Id. de cliente de aplicación de Azure AD asociada Hola Hola protegido aplicación de API. (Si se usa una sola aplicación de Azure AD, esto es Hola mismo identificador de cliente como uno para el llamador de Hola Hola.)

Estos valores están disponibles en las páginas de hello Azure AD de hello [portal de Azure clásico](https://manage.windowsazure.com/).

Una vez que se ha adquirido el token de hello, llamador Hola incluye con las solicitudes HTTP en el encabezado de autorización de Hola.  Servicio de aplicación valida el token de Hola y permite Hola Hola de tooreach solicitudes protegido aplicación de API.

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a>¿Cómo tooprotect Hola API aplicación del acceso de los usuarios de hello mismo inquilino
Tokens de portador para los usuarios de hello mismo inquilino se consideran válidos para hello protegen aplicación de API.  Si desea que tooensure que puede llamar un servicio principal Hola aplicación API protegida, agregar código de hello protegido Hola de toovalidate de aplicación de API después de las notificaciones de token de hello:

* `appid`debe ser el identificador de cliente de Hola de aplicación de Azure AD de Hola que está asociado con el autor de llamada de Hola. 
* `oid`(`objectidentifier`) debe ser el identificador de entidad de seguridad de servicio de Hola del autor de llamada de Hola. 

Servicio de aplicaciones también proporciona hello `objectidentifier` notificación en el encabezado X-MS-CLIENT-entidad de seguridad-ID de Hola.

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a>¿Cómo tooprotect Hola aplicación de API de acceso de explorador
Si no valida las notificaciones en el código de aplicación de API de hello protegido, y si usa un independiente aplicación de Azure AD para hello protegido aplicación de API, asegúrese de que ese hello es la dirección URL de respuesta de la aplicación de Azure AD no Hola igual que la dirección URL base de la aplicación de API de Hola. Si Hola dirección URL de respuesta apunta directamente aplicación de API de toohello protegido, un usuario inquilino Hola mismo AD de Azure podría examinar la aplicación de API de toohello, inicie sesión y llamar correctamente a la API de Hola.

## <a id="tutorialstart"></a>Continuar la serie de tutoriales de aplicaciones de API de .NET de Hola
Si está siguiendo hello Node.js o Java serie de tutoriales para aplicaciones de API, omitir toohello [pasos siguientes](#next-steps) sección. 

resto de Hola de este artículo continúa la serie de tutoriales de aplicaciones de API de .NET de Hola y se da por supuesto que se completaron hello [tutorial de autenticación de usuario](app-service-api-dotnet-user-principal-auth.md) y se ejecuta en Azure con autenticación de usuarios de aplicación de ejemplo de Hola habilitado.

## <a name="set-up-authentication-in-azure"></a>Configuración de la autenticación en Azure
En esta sección Configurar servicio de aplicaciones por lo que ese Hola solicitudes de HTTP solo permite la aplicación de API de nivel de datos de tooreach Hola Hola las que tienen Azure válida tokens de portador de AD. 

Hola la siguiente sección, configurar la aplicación de nivel intermedio API hello toosend aplicación credenciales tooAzure AD, regresar un token de portador y enviar a portador Hola aplicación de API de nivel de datos de token toohello. Este proceso se muestra en el diagrama de Hola.

![Diagrama de autenticación del servicio](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Si experimenta problemas al siguiente instrucciones de tutorial de hello, vea hello [solución de problemas](#troubleshooting) sección al final de hello del tutorial Hola. 

1. Hola [portal de Azure](https://portal.azure.com/), navegue toohello **configuración** hoja de aplicación Hola API que creó para la aplicación de API de hello ToDoListDataAPI (capa de datos) y, a continuación, haga clic en **configuración**.
2. Hola **configuración** hoja, buscar hello **características** sección y, a continuación, haga clic en **autenticación / autorización**.
   
    ![Autenticación/autorización en el Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. Hola **autenticación / autorización** hoja, haga clic en **en**.
4. Hola **tootake de acción cuando no se autentica la solicitud** lista desplegable, seleccione **iniciar sesión con Azure Active Directory**.
   
    Esta es la configuración de Hola que provoca tooensure de servicio de aplicaciones que solo autenticados aplicación de API de Hola de alcance de las solicitudes. Para las solicitudes que tienen los tokens de portador válido, servicio de aplicaciones pasa tokens de Hola a lo largo de la aplicación toohello API y rellena los encabezados HTTP con notificaciones utilizadas toomake esa información código tooyour disponibles con más facilidad.
5. En **Proveedores de autenticación**, haga clic en **Azure Active Directory**.
   
    ![Hoja Autenticación/autorización del Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. Hola **configuración de Azure Active Directory** hoja, haga clic en **Express**.
   
    Con hello **Express** opción Azure puede crear automáticamente una aplicación AAD de Azure AD [inquilino](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    No tienes toocreate un inquilino, porque cada cuenta de Azure automáticamente tiene uno.
7. En **Modo de administración**, haga clic en **Crear nueva aplicación de AD** si aún no está seleccionado.
   
    Hola conecta el portal de Hello **crear aplicación** cuadro de entrada con un valor predeterminado. De forma predeterminada, se denomina aplicación de Azure AD Hola Hola igual como aplicación hello API. Si lo prefiere, escriba un nombre diferente.
   
    ![Configuración de Azure AD](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Tenga en cuenta**: como alternativa, puede usar un único anuncio Azure aplicación para ambos Hola aplicación que realiza la llamada de API y Hola protegido aplicación de API. Si opta por esa alternativa, no necesitará hello **crear nueva aplicación de AD** opción aquí porque se ha creado una aplicación de Azure AD anteriormente en el tutorial de autenticación de usuario de Hola. Para este tutorial, usará separe las aplicaciones de Azure AD para hello llamada aplicación de API y Hola protegido aplicación de API.
8. Tome nota del valor de Hola Hola **crear aplicación** cuadro de entrada; podrá buscar esta aplicación AAD Hola portal de Azure clásico más adelante.
9. Haga clic en **Aceptar**.
10. Hola **autenticación / autorización** hoja, haga clic en **guardar**.
    
    ![Haga clic en Guardar](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    Servicio de aplicaciones crea una aplicación de Azure Active Directory con **dirección URL de inicio de sesión** y **dirección URL de respuesta** establece automáticamente la dirección URL de toohello de la aplicación de API. último valor de Hola permite a los usuarios en su toolog del inquilino AAD en y aplicación de API de acceso hello.

### <a name="verify-that-hello-api-app-is-protected"></a>Comprobar que la aplicación hello API está protegida
1. En un explorador, vaya toohello URL de aplicación hello API: Hola **aplicación de API** hoja Hola portal de Azure, haga clic en vínculo hello en **URL**. 
   
    Son redirigidos tooa pantalla de inicio de sesión dado que las solicitudes no autenticadas no se permiten la aplicación de API de hello tooreach. 
   
    Si el explorador vaya toohello Swagger de interfaz de usuario, el explorador ya podría haber iniciado sesión, en ese caso, abra una ventana de InPrivate o de incógnito y vaya toohello Swagger dirección URL de interfaz de usuario.
2. Inicie sesión con las credenciales de un usuario en su inquilino de AAD.
   
   Cuando ha iniciado sesión, Hola "se creó correctamente" página aparece en el Explorador de Hola.

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Configurar hello ToDoListAPI proyecto tooacquire y enviar el token de Azure AD Hola
En esta sección hello las siguientes tareas:

* Agregue el código de aplicación de API de nivel intermedio de Hola que usa Azure AD aplicación credenciales tooacquire un token y enviar con HTTP solicitudes de aplicación de API de nivel de datos de toohello.
* Obtener las credenciales de Hola que necesita de Azure AD.
* Escriba las credenciales de hello en configuración del entorno de servicio de aplicaciones de Azure en tiempo de ejecución en el nivel intermedio de hello aplicación de API. 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Configurar hello ToDoListAPI proyecto tooacquire y enviar el token de Azure AD Hola
Asegúrese de hello después cambios en hello ToDoListAPI proyecto en Visual Studio.

1. Quite todo código de hello en hello *ServicePrincipal.cs* archivo.
   
    Se trata de código de hello que usa ADAL para el token de portador de .NET tooacquire hello Azure AD.  Utiliza varios valores de configuración que se configuran en el entorno de Azure en tiempo de ejecución de hello más tarde. Este es el código de hello. 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    **Nota:** este código requiere Hola AAL para el paquete NuGet de .NET (Microsoft.IdentityModel.Clients.ActiveDirectory), que ya está instalado en el proyecto de Hola. Si estuviera creando este proyecto desde el principio, tendrás que tooinstall este paquete. Este paquete no se instala automáticamente con la plantilla de proyecto nuevo de aplicación de API de Hola.
2. En *controladores/ToDoListController*, quite el comentario de código de hello en hello `NewDataAPIClient` método que agrega las solicitudes de token tooHTTP Hola Hola encabezado de autorización.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Implementar proyecto de ToDoListAPI Hola. (Haga clic en proyecto de hello, a continuación, haga clic en **publicar > Publicar**.)
   
    Visual Studio implementa Hola proyecto y abre la dirección URL base de la aplicación web de toohello de explorador. Esto mostrará una página de 403 error, que es normal que un intento de toogo tooa API Web dirección URL base desde un explorador.
4. Explorador de hello cerrar.

### <a name="get-azure-ad-configuration-values"></a>Obtención de los valores de configuración de Azure AD
1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), vaya demasiado**Azure Active Directory**.
2. En hello **directorio** , haga clic en su inquilino de AAD.
3. Haga clic en **aplicaciones > las aplicaciones que tiene mi compañía**y, a continuación, haga clic en la casilla de verificación Hola.
4. En la lista Hola de aplicaciones, haga clic en Hola Hola uno que Azure crea automáticamente cuando se ha habilitado la autenticación para aplicación de API de hello ToDoListDataAPI (capa de datos).
5. Haga clic en hello **configurar** ficha.
6. Hola copia **Id. de cliente** valor y guardar un lugar puede obtener desde más tarde. 
7. En el portal de Azure clásico Hola volver atrás lista toohello de **aplicaciones tiene mi compañía**y haga clic en la aplicación de AAD de Hola que creó para la aplicación de API ToDoListAPI de nivel intermedio de hello (Hola creada en el tutorial anterior de hello, no Hola que creó en este tutorial).
8. Haga clic en hello **configurar** ficha.
9. Hola copia **Id. de cliente** valor y guardar un lugar puede obtener desde más tarde.
10. En **claves**, seleccione **1 año** de hello **seleccione duración** lista desplegable.
11. Haga clic en **Guardar**.
    
     ![Generar clave de aplicación](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Copie el valor de clave de Hola y lo guarda un lugar que puede obtener desde más tarde.
    
     ![Copiar la nueva clave de aplicación](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a>Configurar opciones de Azure AD en el entorno de tiempo de ejecución de la aplicación de API de nivel intermedio de Hola
1. Vaya toohello [portal de Azure](https://portal.azure.com/)y, a continuación, navegue toohello **API App** hoja para la aplicación hello API que hospeda el proyecto de hello TodoListAPI (nivel intermedio).
2. Haga clic en **Configuración > Configuración de la aplicación**.
3. Hola **configuración de la aplicación** sección, agregue Hola siguiendo las claves y valores:
   
   | **Clave** | ida:Authority |
   | --- | --- |
   | **Valor** |https://login.microsoftonline.com/{su nombre de inquilino de Azure AD} |
   | **Ejemplo** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Clave** | ida:ClientId |
   | --- | --- |
   | **Valor** |Id. de cliente del programa Hola a llamar a la aplicación (nivel intermedio - ToDoListAPI) |
   | **Ejemplo** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **Clave** | ida:ClientSecret |
   | --- | --- |
   | **Valor** |Clave de aplicación del programa Hola a llamar a la aplicación (nivel intermedio - ToDoListAPI) |
   | **Ejemplo** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **Clave** | ida:Resource |
   | --- | --- |
   | **Valor** |Identificador de cliente de Hola se denomina aplicación (capa de datos - ToDoListDataAPI) |
   | **Ejemplo** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **Tenga en cuenta**: para `ida:Resource`, asegúrese de usar Hola llama a la aplicación **Id. de cliente** y no su **App ID URI**.
   
    `ida:ClientId`y `ida:Resource` son diferentes valores para este tutorial porque lo está utilizando separan applicaations de Azure AD para el nivel intermedio de Hola y de capa de datos. Si usaba una única aplicación de Azure AD para llamar a hello y aplicación de API de hello protegido aplicación de API, usaría Hola mismo valor en ambos `ida:ClientId` y `ida:Resource`.
   
    código de Hello usa ConfigurationManager tooget estos valores, por lo que se puede almacenar en el archivo Web.config del proyecto de Hola o en el entorno de Azure en tiempo de ejecución de Hola. Mientras se ejecuta una aplicación ASP.NET en el Servicio de aplicaciones de Azure, la configuración del entorno invalida automáticamente la configuración de Web.config. Configuración del entorno es generalmente una [más segura información confidencial de manera toostore en comparación con el archivo Web.config de tooa](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. Haga clic en **Guardar**.
   
    ![Haga clic en Guardar](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a>Probar la aplicación hello
1. En un explorador vaya toohello dirección URL HTTPS de aplicación de hello AngularJS front-end web.
2. Haga clic en hello **tooDo lista** ficha e inicie sesión con credenciales de un usuario en su inquilino de Azure AD. 
3. Agregar tooverify de elementos de tarea que la aplicación hello funciona.
   
    ![página de lista tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Si la aplicación hello no funciona según lo previsto, compruebe todos los valores de hello que escribió en hello portal de Azure. Si todos los valores de hello aparecen toobe correcta, vea hello [solución de problemas](#troubleshooting) sección más adelante en este tutorial.

## <a name="protect-hello-api-app-from-browser-access"></a>Proteger la aplicación de API de hello contra el acceso de explorador
En este tutorial ha creado una independiente aplicación de Azure AD para la aplicación hello API ToDoListDataAPI (capa de datos). Tal y como se ha visto, cuando el servicio de aplicaciones crea una aplicación de AAD, configura la aplicación AAD de hello de forma que permite a un usuario toogo toohello API URL de la aplicación en un explorador e inicie sesión en. Eso significa es posible que un usuario final en el inquilino de Azure AD, no solo una entidad de servicio, tooaccess Hola API. 

Si desea que el acceso de explorador tooprevent sin escribir ningún código de hello protegidos aplicación de API, puede cambiar hello **dirección URL de respuesta** Hola aplicación AAD para que sea diferente de la aplicación hello API dirección URL base. 

### <a name="disable-browser-access"></a>Deshabilitación del acceso desde el explorador
1. En del portal clásico de hello **configurar** pestaña aplicación AAD de Hola que se creó para hello TodoListService, cambie el valor de Hola Hola **dirección URL de respuesta** campo para que sea una dirección URL válida, pero no Hola API de la aplicación DIRECCIÓN URL.
2. Haga clic en **Guardar**.

### <a name="verify-browser-access-no-longer-works"></a>Comprobación de que el acceso desde el explorador ya no funciona
Anteriormente, ha comprobado que puede ir toohello URL de la aplicación de API desde un explorador, inicie sesión con credenciales de un usuario concreto. En esta sección, comprobará que ya no es posible. 

1. En una nueva ventana del explorador, vaya toohello URL de aplicación de API de Hola de nuevo.
2. Inicio de sesión cuando se le pida toodo así.
3. Inicio de sesión se realiza correctamente pero conduce tooan página de error.
   
    Ha configurado la aplicación AAD de hello para que los usuarios de inquilino de AAD de hello no se pueden iniciar sesión y tener acceso a Hola API desde un explorador. Todavía puede tener acceso a la aplicación de API de hello mediante el uso de un token de entidad de seguridad de servicio, que puede comprobar desde la dirección URL de la aplicación web toohello y agregar más elementos de tareas pendientes.

## <a name="restrict-access-tooa-particular-service-principal"></a>Restringir la entidad de servicio determinado de tooa de acceso
En este momento, cualquier llamador que puede obtener un token para un usuario o entidad de servicio en su inquilino de Azure AD puede llamar a la aplicación hello API TodoListDataAPI (capa de datos). Puede ser conveniente toomake seguro de que esa aplicación de API de nivel de datos de hello solo acepta llamadas de aplicación de API de hello TodoListAPI (nivel intermedio) y solo de una entidad de servicio determinado. 

Puede agregar estas restricciones mediante la adición de Hola de código toovalidate `appid` y `objectidentifier` notificaciones en las llamadas entrantes.

Para este tutorial colocan el código de hello que valida el identificador de la aplicación y el Id. de entidad de seguridad de servicio directamente en las acciones de controlador.  Alternativas son toouse personalizado `Authorize` atributo o toodo esta validación en las secuencias de inicio (por ejemplo, el middleware de OWIN). Para obtener un ejemplo de Hola esta última, vea [esta aplicación de ejemplo](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Asegúrese de hello después de proyecto de TodoListDataAPI toohello de cambios.

1. Abra hello *Controllers/TodoListController.cs* archivo.
2. Quite el comentario de las líneas de Hola que establecen `trustedCallerClientId` y `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Quite el comentario de código de hello en hello CheckCallerId método. Este método se llama al inicio de Hola de cada método de acción de controlador de Hola. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. Volver a implementar hello ToDoListDataAPI proyecto tooAzure servicio de aplicaciones.
5. En el explorador, vaya la dirección URL de HTTPS de la aplicación de toohello AngularJS front-end web y en la página de inicio de hello, haga clic en hello **tooDo lista** ficha.
   
    aplicación Hello no funciona porque se producen errores en llamadas finalizar toohello atrás. nuevo código de Hello está comprobando appid real y objectidentifier pero todavía no tiene Hola valores correctos toocheck usarlas con. Hola explorador la consola de herramientas para desarrolladores informa de que ese servidor hello está devolviendo un error HTTP 401.
   
    ![Error en la Consola de Developer Tools](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    Hola pasos configurar valores esperados de Hola.
6. Con PowerShell de Azure AD, obtener valor de hello del servicio de hello principal para la aplicación de Azure AD que haya creado para el proyecto de TodoListWebApp Hola Hola.
   
    a. Para obtener instrucciones sobre cómo tooinstall PowerShell de Azure y conectar tooyour suscripción, vea [con Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md).
   
    b. tooget una lista de entidades de servicio, ejecute hello `Login-AzureRmAccount` comando y, a continuación, Hola `Get-AzureRmADServicePrincipal` comando.
   
    c. Busque objectid Hola Hola entidad de servicio de aplicación de hello TodoListAPI y guárdelo en una ubicación que se puede copiar desde más adelante.
7. Hola portal de Azure, navegue toohello hoja de aplicaciones de API para la aplicación de API de Hola que implementó hello ToDoListDataAPI proyecto a.
8. Haga clic en **Configuración > Configuración de la aplicación**.
9. Hola **configuración de la aplicación** sección, agregue Hola siguiendo las claves y valores:
   
   | **Clave** | todo:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Valor** |Id. de entidad de servicio de la aplicación que realiza la llamada |
   | **Ejemplo** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Clave** | todo:TrustedCallerClientId |
   | --- | --- |
   | **Valor** |Id. de cliente de la llamada a la aplicación - copiado desde la aplicación de Azure AD TodoListAPI hello |
   | **Ejemplo** |960adec2-b74a-484a-960adec2-b74a-484a |
10. Haga clic en **Guardar**.
    
     ![Haga clic en Guardar](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. En el explorador, la dirección URL de la aplicación web toohello de retorno y en la página de inicio de hello, haga clic en hello **tooDo lista** ficha.
    
     Esta aplicación en tiempo de hello funciona como se espera porque la aplicación del llamador de confianza de hello identificador y el identificador de entidad de seguridad de servicio son los valores esperados Hola.
    
     ![página de lista tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a>Compilar proyectos de Hola desde el principio
proyectos de Hello dos API Web se crearon con hello **aplicación de API de Azure** de proyectos de plantilla y reemplazando Hola valores de controlador predeterminado con un controlador ToDoList. Para adquirir tokens de entidad de seguridad de servicio de Azure AD en proyecto de hello ToDoListAPI, Hola [Active Directory Authentication Library (ADAL) para .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) se instaló el paquete NuGet.

Para obtener información acerca de cómo crear demasiado una aplicación de página de AngularJS con un back-end Web API como ToDoListAngular, consulte [manos en laboratorio: compilar una aplicación de página única (SPA) con ASP.NET Web API y Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Para obtener información acerca de cómo tooadd código de autenticación de Azure AD, consulte [proteger AngularJS única página aplicaciones con Azure AD](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Solución de problemas
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Asegúrese de no confundir ToDoListAPI (nivel intermedio) con ToDoListDataAPI (capa de datos). Por ejemplo, en este tutorial agrega aplicación de API de nivel de datos de autenticación toohello, **pero clave de aplicación Hola debe proceder de hello aplicación de Azure AD que haya creado para la aplicación de API de nivel intermedio de hello**.

## <a name="next-steps"></a>Pasos siguientes
Se trata de último tutorial de Hola Hola serie de aplicaciones de API. 

Para obtener más información acerca de Active Directory de Azure, vea Hola recursos siguientes.

* [Guía para desarrolladores de Azure AD](http://aka.ms/aaddev)
* [Escenarios de Azure AD](http://aka.ms/aadscenarios)
* [Ejemplos de Azure AD](http://aka.ms/aadsamples)
  
    Hola [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) ejemplo es similar toowhat se muestra en este tutorial, pero sin usar la autenticación de servicio de aplicaciones.

Para obtener información sobre otras maneras de toodeploy Visual Studio proyectos tooAPI aplicaciones, mediante Visual Studio o [automatizar la implementación](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) desde una [sistema de control de código fuente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), vea [cómo toodeploy un Aplicación de servicio de aplicaciones de Azure](../app-service-web/web-sites-deploy.md).

