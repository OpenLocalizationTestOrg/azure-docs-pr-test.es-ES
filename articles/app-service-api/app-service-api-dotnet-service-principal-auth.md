---
title: "Autenticación de entidad de servicio para API Apps en Azure App Service | Microsoft Docs"
description: "Aprenda a proteger una aplicación de API en el Servicio de aplicaciones de Azure para escenarios entre servicios."
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
ms.openlocfilehash: 95653287546bbe358111ed16af0c30a53caff2b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Autenticación de entidad de servicio para Aplicaciones de API en el Servicio de aplicaciones de Azure
## <a name="overview"></a>Información general
Este artículo explica cómo utilizar la autenticación del Servicio de aplicaciones para obtener acceso *interno* a aplicaciones de API. Un escenario interno se produce cuando tiene una aplicación de API que desea que solo sea consumible mediante su propio código de aplicación. La manera recomendada de implementar este escenario en el Servicio de aplicaciones es utilizar Azure AD para proteger la aplicación de API llamada. Se llama a la aplicación de API protegida con un token de portador que obtiene de Azure AD al proporcionar credenciales (entidad de servicio) de identidad de la aplicación. Para ver alternativas al uso de Azure AD, consulte la sección **Autenticación entre servicios** en [Autenticación y autorización en el Servicio de aplicaciones de Azure](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

En este artículo, aprenderá lo siguiente:

* Usar Azure Active Directory (Azure AD) para proteger una aplicación de API de accesos no autenticados.
* Consumir una aplicación de API protegida desde otra aplicación de API, una aplicación web o una aplicación móvil mediante credenciales de entidad de servicio (identidad de aplicación) de Azure AD. Para más información sobre cómo consumir desde una aplicación lógica, consulte [Uso de la API personalizada hospedada en Servicio de aplicaciones con aplicaciones lógicas](../logic-apps/logic-apps-custom-hosted-api.md).
* Asegurarse de que los usuarios que iniciaron sesión no pueda llaman a la aplicación de API protegida desde un explorador.
* Asegurarse de que solo una entidad de servicio de Azure AD pueda llamar a la aplicación de API protegida.

El artículo contiene dos secciones:

* La sección [Configuración de la autenticación de entidad de servicio en Azure App Service](#authconfig) explica en términos generales cómo configurar la autenticación para cualquier aplicación de API y cómo usar la aplicación de API protegida. Esta sección se aplica igualmente a todos los marcos admitidos por el Servicio de aplicaciones, como. NET, Node.js y Java.
* A partir de la sección [Continuación de la serie de tutoriales de aplicaciones de API de .NET](#tutorialstart) , el tutorial lo guiará a través de la configuración de un escenario de "acceso interno" para una aplicación de ejemplo de .NET en ejecución en el Servicio de aplicaciones. 

## <a id="authconfig"></a> Configuración de la autenticación de entidad de servicio en el Servicio de aplicaciones de Azure
Esta sección proporciona instrucciones generales que se aplican a cualquier aplicación de API. Para obtener los pasos específicos para la aplicación de ejemplo de .NET To Do List, vaya a [Continuación de la serie de tutoriales de aplicaciones de API de .NET](#tutorialstart).

1. En [Azure Portal](https://portal.azure.com/), vaya a la hoja **Configuración** de la aplicación de API que quiere proteger, busque la sección **Características** y haga clic en **Autenticación/autorización**.
   
    ![Autenticación/autorización en el Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. En la hoja **Autenticación/autorización**, haga clic en **Activado**.
3. En la lista desplegable **Acción por realizar cuando no se autentique la solicitud**, seleccione **Iniciar sesión con Azure Active Directory**.
4. En **Proveedores de autenticación,** seleccione **Azure Active Directory**.
   
    ![Hoja Autenticación/autorización del Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Configure la hoja **Configuración de Azure Active Directory** para crear una aplicación de Azure AD o use una aplicación de Azure AD existente si ya tiene alguna que quiera utilizar.
   
    En los escenarios internos normalmente hay una aplicación de API que llama a una aplicación de API. Puede usar aplicaciones de AD independientes para cada aplicación de API o una sola aplicación de Azure AD.
   
    Para ver instrucciones detalladas sobre esta hoja, consulte [Configuración de la aplicación del Servicio de aplicaciones para usar el inicio de sesión de Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Cuando termine con la hoja de configuración del proveedor de autenticación, haga clic en **Aceptar**.
7. En la hoja **Autenticación/autorización**, haga clic en **Guardar**.
   
    ![Haga clic en Guardar](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Una vez hecho esto, el Servicio de aplicaciones solo admitirá solicitudes de los llamadores en el inquilino de Azure AD configurado. No se requiere ningún código de autenticación ni autorización en la aplicación de API protegida. El token de portador se pasa a la aplicación de API junto con las notificaciones utilizadas normalmente en encabezados HTTP y puede leer esa información en el código para comprobar que las solicitudes proceden de un llamador concreto, como una entidad de servicio.

Esta funcionalidad de autenticación funciona de la misma manera para todos los lenguajes que el servicio de aplicaciones admite, como .NET, Node.js y Java. 

#### <a name="how-to-consume-the-protected-api-app"></a>Uso de la aplicación de API protegida
El llamador debe proporcionar un token de portador de Azure AD con llamadas a API. Para obtener un token de portador con las credenciales de entidad de servicio, el llamador usa la biblioteca de autenticación de Active Directory (ADAL para [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) o [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). Para obtener un token, el código que llama a ADAL proporciona a ADAL la siguiente información:

* El nombre de su inquilino de Azure AD.
* El identificador de cliente y el secreto del cliente (clave de aplicación) de la aplicación de Azure AD asociada al llamador.
* El identificador de cliente de la aplicación de Azure AD asociada con la aplicación de API protegida. (Si se usa una sola aplicación de Azure AD, es el mismo identificador de cliente que el llamador).

Estos valores están disponibles en las páginas de Azure AD del [Portal de Azure clásico](https://manage.windowsazure.com/).

Una vez adquirido el token, el llamador lo incluye con las solicitudes HTTP en el encabezado de autorización.  El Servicio de aplicaciones valida el token y permite que las solicitudes lleguen a la aplicación de API protegida.

#### <a name="how-to-protect-the-api-app-from-access-by-users-in-the-same-tenant"></a>Protección de la aplicación de API del acceso de usuarios en el mismo inquilino
Los tokens de portador para los usuarios en el mismo inquilino se consideran válidos para la aplicación de API protegida.  Si desea asegurarse de que solo una entidad de servicio pueda llamar a la aplicación de API protegida, agregue el código en la aplicación de API protegida para validar las siguientes notificaciones del token:

* `appid` debe ser el identificador de cliente de la aplicación de Azure AD que está asociada con el llamador. 
* `oid` (`objectidentifier`) debe ser el identificador de entidad de servicio del llamador. 

El Servicio de aplicaciones también proporciona la notificación `objectidentifier` en el encabezado X-MS-CLIENT-PRINCIPAL-ID.

### <a name="how-to-protect-the-api-app-from-browser-access"></a>Protección de la aplicación de API de accesos desde el explorador
Si no valida las notificaciones en el código en la aplicación de API protegida y si usa otra aplicación de Azure AD para la aplicación de API protegida, asegúrese de que la dirección URL de respuesta de la aplicación de Azure AD no sea igual que la dirección URL base de la aplicación de API. Si la dirección URL de respuesta apunta directamente a la aplicación de API protegida, un usuario en el mismo inquilino de Azure AD podría usar un explorador para llegar a la aplicación de API, iniciar sesión y llamar correctamente a la API.

## <a id="tutorialstart"></a> Continuación de la serie de tutoriales de aplicaciones de API de .NET
Si está siguiendo las series de tutoriales de Node.js o de Java para aplicaciones de API, vaya a la sección [Siguientes pasos](#next-steps) . 

El resto de este artículo continúa la serie de tutoriales para aplicaciones de API de .NET y da por hecho que ha completado el [tutorial de autenticación de usuario](app-service-api-dotnet-user-principal-auth.md) y que tiene la aplicación de ejemplo en ejecución en Azure con la autenticación de usuario habilitada.

## <a name="set-up-authentication-in-azure"></a>Configuración de la autenticación en Azure
En esta sección, configurará el Servicio de aplicaciones para que solo las solicitudes HTTP que tengan tokens de portador de Azure AD válidos tengan acceso a la aplicación de API de capa de datos. 

En la siguiente sección, configurará la aplicación de API de nivel intermedio para enviar las credenciales de la aplicación a Azure AD, obtener un token de portador y enviar el token de portador a la aplicación de API de capa de datos. Este proceso se ilustra en el diagrama.

![Diagrama de autenticación del servicio](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Si experimenta problemas al seguir las instrucciones del tutorial, consulte la sección [Solución de problemas](#troubleshooting) al final. 

1. En [Azure Portal](https://portal.azure.com/), vaya a la hoja **Configuración** de la aplicación de API que creó para ToDoListDataAPI (capa de datos) y haga clic en **Configuración**.
2. En la hoja **Configuración**, busque la sección **Características** y haga clic en **Autenticación/autorización**.
   
    ![Autenticación/autorización en el Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. En la hoja **Autenticación/autorización**, haga clic en **Activado**.
4. En la lista desplegable **Acción por realizar cuando no se autentique la solicitud**, seleccione **Iniciar sesión con Azure Active Directory**.
   
    Esta es la configuración que hace que el Servicio de aplicaciones se asegure de que solo las solicitudes autenticadas alcancen la aplicación de API. Para las solicitudes que tienen tokens de portador válidos, el Servicio de aplicaciones pasa los tokens a la aplicación de API y rellena los encabezados HTTP con las notificaciones usadas normalmente para que esa información esté más fácilmente disponible para el código.
5. En **Proveedores de autenticación**, haga clic en **Azure Active Directory**.
   
    ![Hoja Autenticación/autorización del Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. En la hoja **Configuración de Azure Active Directory**, haga clic en **Rápido**.
   
    Con la opción **Rápido**, Azure puede crear automáticamente una aplicación AAD en su [inquilino](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)de Azure AD. 
   
    No es preciso que cree un inquilino, porque todas las cuenta de Azure tienen uno automáticamente.
7. En **Modo de administración**, haga clic en **Crear nueva aplicación de AD** si aún no está seleccionado.
   
    El portal conecta el cuadro de entrada **Crear aplicación** con un valor predeterminado. De forma predeterminada, la aplicación de Azure AD recibe el mismo nombre que la aplicación de API. Si lo prefiere, escriba un nombre diferente.
   
    ![Configuración de Azure AD](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Nota**: Como alternativa, podría usar una sola aplicación de Azure AD tanto para la aplicación de API que realiza la llamada como para la aplicación de API protegida. Si eligió esa alternativa, no necesitaría la opción **Crear nueva aplicación de AD** aquí porque ya creó antes una aplicación de Azure AD en el tutorial de autenticación de usuarios. Para este tutorial, usará aplicaciones diferentes de Azure AD para la aplicación que realiza la llamada de API y la aplicación de API protegida.
8. Anote el valor del cuadro de entrada **Crear aplicación** ; buscará esta aplicación AAD más adelante en el Portal de Azure clásico.
9. Haga clic en **OK**.
10. En la hoja **Autenticación/autorización**, haga clic en **Guardar**.
    
    ![Haga clic en Guardar](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    App Service crea una aplicación de Azure Active Directory con **URL de inicio de sesión** y **URL de respuesta** establecidas automáticamente en la URL de la aplicación de API. El último valor permite a los usuarios del inquilino de AAD iniciar sesión y tener acceso a la aplicación de API.

### <a name="verify-that-the-api-app-is-protected"></a>Comprobación de la protección de la aplicación de API
1. En un explorador, vaya a la dirección URL de la aplicación de API: en la hoja **Aplicación de API** de Azure Portal, haga clic en el vínculo bajo **URL**. 
   
    Se le redirigirá a una pantalla de inicio de sesión porque no se permite que las solicitudes no autenticadas tengan acceso a la aplicación de API. 
   
    Si el explorador va a la interfaz de usuario de Swagger, es posible que el explorador ya iniciara sesión; en ese caso, abra una ventana de InPrivate o Incognito y vaya a la dirección URL de la interfaz de usuario de Swagger.
2. Inicie sesión con las credenciales de un usuario en su inquilino de AAD.
   
   Una vez iniciada la sesión, en el explorador aparece una página que indica que "se creó correctamente".

## <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a>Configuración del proyecto ToDoListAPI para adquirir y enviar el token de Azure AD
En esta sección realizará las siguientes tareas:

* Agregar el código en la aplicación de API de nivel intermedio que usa credenciales de la aplicación de Azure AD para adquirir un token y enviarlo con las solicitudes HTTP a la aplicación de API de capa de datos.
* Obtener las credenciales que necesita de Azure AD.
* Escribir las credenciales en la configuración del entorno en tiempo de ejecución de Servicio de aplicaciones de Azure en la aplicación de API de nivel intermedio. 

### <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a>Configuración del proyecto ToDoListAPI para adquirir y enviar el token de Azure AD
Realice los cambios siguientes en el proyecto ToDoListAPI en Visual Studio.

1. Quite las marcas de comentarios de todo el código en el archivo *ServicePrincipal.cs* .
   
    Este es el código que usa ADAL para .NET para adquirir el token de portador de Azure AD.  Usa varios valores de configuración que se establecerán más adelante en el entorno en tiempo de ejecución de Azure. Este es el código: 
   
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
   
    **Nota:** Este código requiere ADAL para el paquete NuGet de .NET (Microsoft.IdentityModel.Clients.ActiveDirectory), que ya está instalado en el proyecto. Si estuviese creando este proyecto desde cero, tendría que instalar este paquete. La plantilla de nuevo proyecto de aplicación de API no instala este paquete automáticamente.
2. En *Controllers/ToDoListController*, quite las marcas de comentarios del código en el método `NewDataAPIClient` que agrega el token a las solicitudes HTTP en el encabezado de autorización.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Implemente el proyecto ToDoListAPI. (Haga clic con el botón derecho en el proyecto y haga clic en **Publicar > Publicar**).
   
    Visual Studio implementa el proyecto y abre un explorador en la dirección URL base de la aplicación web. Esto mostrará una página de error 403, lo que es normal cuando se intenta ir a una dirección URL base de Web API desde un explorador.
4. Cierre el explorador.

### <a name="get-azure-ad-configuration-values"></a>Obtención de los valores de configuración de Azure AD
1. En el [Portal de Azure clásico](https://manage.windowsazure.com/), vaya a **Azure Active Directory**.
2. En la pestaña **Directorio** , haga clic en su inquilino de AAD.
3. Haga clic en **Aplicaciones > Aplicación propiedad de mi compañía** y, después, en la marca de verificación.
4. En la lista de aplicaciones, haga clic en el nombre de la que Azure creó automáticamente cuando habilitó la autenticación para la aplicación de API ToDoListDataAPI (capa de datos).
5. Haga clic en la pestaña **Configurar** .
6. Copie el valor de **Id. de cliente** y guárdelo en un lugar de donde pueda recuperarlo más adelante. 
7. En el Portal de Azure clásico, vuelva a la lista **Aplicaciones que tiene mi compañía**y haga clic en la aplicación AAD que creó para la aplicación de API ToDoListAPI de nivel intermedio (la que creó en el tutorial anterior, no la que ha creado en este tutorial).
8. Haga clic en la pestaña **Configurar** .
9. Copie el valor de **Id. de cliente** y guárdelo en un lugar de donde pueda recuperarlo más adelante.
10. En **Claves**, seleccione **1 año** en la lista desplegable **Seleccionar duración**.
11. Haga clic en **Guardar**.
    
     ![Generar clave de aplicación](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Copie el valor de clave y guárdelo en un lugar donde pueda recuperarlo más adelante.
    
     ![Copiar la nueva clave de aplicación](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-the-middle-tier-api-apps-runtime-environment"></a>Configuración de opciones de Azure AD en el entorno en tiempo de ejecución de la aplicación de API de nivel intermedio
1. Vaya al [Portal de Azure](https://portal.azure.com/)y, después, vaya a la hoja **Aplicación de API** de la aplicación de API que hospeda el proyecto TodoListAPI (nivel intermedio).
2. Haga clic en **Configuración > Configuración de la aplicación**.
3. En la sección **Configuración de la aplicación** , agregue las claves y los valores siguientes:
   
   | **Clave** | ida:Authority |
   | --- | --- |
   | **Valor** |https://login.microsoftonline.com/{su nombre de inquilino de Azure AD} |
   | **Ejemplo** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Clave** | ida:ClientId |
   | --- | --- |
   | **Valor** |Id. de cliente de la aplicación que realiza la llamada (nivel intermedio, ToDoListAPI) |
   | **Ejemplo** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **Clave** | ida:ClientSecret |
   | --- | --- |
   | **Valor** |Clave de aplicación de la aplicación que realiza la llamada (nivel intermedio, ToDoListAPI) |
   | **Ejemplo** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **Clave** | ida:Resource |
   | --- | --- |
   | **Valor** |Id. de cliente de la aplicación a la que se llama (capa de datos, ToDoListDataAPI) |
   | **Ejemplo** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **Nota**: Para `ida:Resource`, asegúrese de utilizar el **Id. de cliente** de la aplicación a la que se llama y no su **URI de id. de aplicación**.
   
    `ida:ClientId` e `ida:Resource` son diferentes valores en este tutorial porque está utilizando aplicaciones de Azure AD distintas para el nivel intermedio y la capa de datos. Si usara una sola aplicación de Azure AD para la aplicación de API que realiza la llamada y la aplicación de API protegida, utilizaría el mismo valor tanto en `ida:ClientId` como en `ida:Resource`.
   
    El código usa ConfigurationManager para obtener estos valores, por lo que podría almacenarse en el archivo Web.config del proyecto o en el entorno en tiempo de ejecución de Azure. Mientras se ejecuta una aplicación ASP.NET en el Servicio de aplicaciones de Azure, la configuración del entorno invalida automáticamente la configuración de Web.config. La configuración del entorno suele ser una [manera más segura de almacenar información confidencial en comparación con un archivo Web.config](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. Haga clic en **Guardar**.
   
    ![Haga clic en Guardar](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-the-application"></a>Prueba de la aplicación
1. En un explorador, vaya a la dirección URL HTTPS de la aplicación web de front-end AngularJS.
2. Haga clic en la pestaña **To Do List** (Lista de tareas pendientes) e inicie sesión con las credenciales de un usuario en el inquilino de Azure AD. 
3. Agregue elementos de tareas pendientes para comprobar que la aplicación funciona.
   
    ![Página de Lista de tareas pendientes](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Si la aplicación no funciona como se espera, vuelva a comprobar todos los valores que escribió en el Portal de Azure. Si toda la configuración parece ser correcta, consulte la sección [Solución de problemas](#troubleshooting) más adelante en este tutorial.

## <a name="protect-the-api-app-from-browser-access"></a>Protección de la aplicación de API contra el acceso desde el explorador
Para este tutorial, creó una aplicación de Azure AD independiente para la aplicación de API ToDoListDataAPI (capa de datos). Como hemos visto, cuando el Servicio de aplicaciones crea una aplicación AAD, la configura de manera que permite a un usuario ir a la dirección URL de la aplicación de API en un explorador e iniciar sesión. Esto significa no solo una entidad de servicio puede tener acceso a la API, también un usuario final de su inquilino de Azure AD. 

Si quiere impedir el acceso desde el explorador sin escribir ningún código en la aplicación de API protegida, puede cambiar la **URL de respuesta** en la aplicación AAD para que sea diferente de la dirección URL base de la aplicación de API. 

### <a name="disable-browser-access"></a>Deshabilitación del acceso desde el explorador
1. En la pestaña **Configurar** del portal clásico de la aplicación AAD que se creó para TodoListService, modifique el valor del campo **URL de respuesta** para que sea una dirección URL válida, pero no la URL de la aplicación de API.
2. Haga clic en **Guardar**.

### <a name="verify-browser-access-no-longer-works"></a>Comprobación de que el acceso desde el explorador ya no funciona
Antes comprobó que puede ir a la URL de la aplicación de API desde un explorador iniciando sesión con las credenciales de un usuario individual. En esta sección, comprobará que ya no es posible. 

1. En una nueva ventana del explorador, vaya de nuevo a la dirección URL de la aplicación de API.
2. Inicie la sesión cuando se le solicite.
3. El inicio de sesión se realiza correctamente, pero genera una página de error.
   
    Configuró la aplicación AAD para que los usuarios del inquilino de AAD no puedan iniciar sesión ni acceder a la API desde un explorador. Aún puede acceder a la aplicación de API con un token de entidad de servicio; para comprobarlo, vaya a la URL de la aplicación web y agregue más elementos de tareas pendientes.

## <a name="restrict-access-to-a-particular-service-principal"></a>Restricción del acceso a una entidad de servicio determinada
En este momento, cualquier llamador que pueda obtener un token para un usuario o entidad de servicio del inquilino de Azure AD puede llamar a la aplicación de API TodoListDataAPI (capa de datos). Puede que quiera asegurarse de que la aplicación de API de capa de datos solo acepta llamadas de la aplicación de API TodoListAPI (nivel intermedio) y solo de una entidad de servicio determinada. 

Para agregar estas restricciones, puede agregar código para validar las notificaciones de `appid` y `objectidentifier` en las llamadas entrantes.

Para este tutorial, coloque código que valida el identificador de la aplicación y el identificador de la entidad de servicio directamente en las acciones de controlador.  Las alternativas son utilizar un atributo `Authorize` personalizado o realizar esta validación en las secuencias de inicio (por ejemplo, middleware OWIN). Para ver un ejemplo de esto último, consulte [esta aplicación de ejemplo](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Realice los cambios siguientes en el proyecto TodoListDataAPI.

1. Abra el archivo *Controllers/TodoListController.cs* .
2. Quite las marcas de comentarios de las líneas que establecen `trustedCallerClientId` y `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Quite los comentarios del código en el método CheckCallerId. Este método se llama al principio de cada método de acción en el controlador. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "The appID or service principal ID is not the expected value." });
            }
        }
4. Vuelva a implementar el proyecto ToDoListDataAPI en el Servicio de aplicaciones de Azure.
5. En el explorador, vaya a la dirección URL HTTPS de la aplicación web front-end de AngularJS y, en la página principal, haga clic en la pestaña **To Do List** (Lista de tareas pendientes).
   
    La aplicación no funciona porque se producen errores en llamadas al back-end. El nuevo código está comprobando los valores reales de appid y objectidentifier pero todavía no tiene los valores correctos con los que compararlos. La consola de herramientas para desarrolladores del explorador informa de que el servidor devuelve un error HTTP 401.
   
    ![Error en la Consola de Developer Tools](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    En los pasos siguientes configurará los valores esperados.
6. Con Azure AD PowerShell, obtenga el valor de la entidad de servicio para la aplicación de Azure AD que creó para el proyecto TodoListWebApp.
   
    a. Para obtener instrucciones sobre cómo instalar Azure PowerShell y conectarse a su suscripción, consulte [Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).
   
    b. Para ver una lista de entidades de servicio, ejecute el comando `Login-AzureRmAccount` y luego el comando `Get-AzureRmADServicePrincipal`.
   
    c. Busque el valor de objectid para la entidad de servicio de la aplicación TodoListAPI y guárdelo en una ubicación que pueda copiar más adelante.
7. En el Portal de Azure, vaya a la hoja de la aplicación de API correspondiente a la aplicación de API en la que implementó el proyecto ToDoListDataAPI.
8. Haga clic en **Configuración > Configuración de la aplicación**.
9. En la sección **Configuración de la aplicación** , agregue las claves y los valores siguientes:
   
   | **Clave** | todo:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Valor** |Id. de entidad de servicio de la aplicación que realiza la llamada |
   | **Ejemplo** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Clave** | todo:TrustedCallerClientId |
   | --- | --- |
   | **Valor** |Id. de cliente de la aplicación que realiza la llamada: copiado de la aplicación TodoListAPI de Azure AD |
   | **Ejemplo** |960adec2-b74a-484a-960adec2-b74a-484a |
10. Haga clic en **Guardar**.
    
     ![Haga clic en Guardar](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. En el explorador, vuelva a la dirección URL de la aplicación web y, en la página principal, haga clic en la pestaña **To Do List** (Lista de tareas pendientes).
    
     Esta vez la aplicación funciona según lo esperado porque el identificador de la aplicación que realiza la llamada y el identificador de entidad de servicio son los valores esperados.
    
     ![Página de Lista de tareas pendientes](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-the-projects-from-scratch"></a>Creación de los proyectos desde cero
Los dos proyectos de Web API se crearon con la plantilla de proyecto **Aplicación de API de Azure** y reemplazando el controlador de los valores predeterminados por un controlador de ToDoList. Para adquirir los tokens de entidad de servicio de Azure AD en el proyecto ToDoListAPI, se instaló el paquete NuGet [Biblioteca de autenticación de Active Directory (ADAL) para .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) .

Para más información sobre cómo crear una aplicación de una sola página de AngularJS con un back-end de API web como ToDoListAngular, consulte [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)(Laboratorio práctico: Crear una aplicación de una sola página (SPA) con ASP.NET Web API y Angular.js). Para más información sobre cómo agregar código de autenticación de Azure AD, consulte [Seguridad de las aplicaciones de una sola página AngularJS con Azure AD](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Solución de problemas
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Asegúrese de no confundir ToDoListAPI (nivel intermedio) con ToDoListDataAPI (capa de datos). Por ejemplo, en este tutorial agregará autenticación a la aplicación de API de capa de datos, **pero la clave de aplicación debe proceder de la aplicación de Azure AD que creó para la aplicación de API de nivel intermedio**.

## <a name="next-steps"></a>Siguientes pasos
Este es el último tutorial de la serie de aplicaciones de API. 

Para más información acerca de Azure Active Directory, consulte los siguientes recursos.

* [Guía para desarrolladores de Azure AD](http://aka.ms/aaddev)
* [Escenarios de Azure AD](http://aka.ms/aadscenarios)
* [Ejemplos de Azure AD](http://aka.ms/aadsamples)
  
    El ejemplo [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) es similar al que se muestra en este tutorial, pero sin utilizar la autenticación del Servicio de aplicaciones.

Para más información sobre otras formas de implementar proyectos de Visual Studio en aplicaciones de API, ya sea con Visual Studio o mediante la [automatización de la implementación](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) desde un [sistema de control de código fuente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), consulte [Documentación de implementación de Azure App Service](../app-service-web/web-sites-deploy.md).

