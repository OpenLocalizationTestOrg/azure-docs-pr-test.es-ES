---
title: "aaaAzure AD AngularJS Introducción | Documentos de Microsoft"
description: "Cómo toobuild una aplicación de página de AngularJS que se integra con Azure AD para inicio de sesión y llama a las API de protegido por AD Azure mediante el uso de OAuth."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>Ayuda para proteger aplicaciones de una sola página AngularJS mediante Azure AD

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD) permite simple y sencillo para tooadd inicio de sesión, cierre de sesión, y llamadas de API de OAuth segura tooyour aplicaciones de la página.  Permite a los usuarios de aplicaciones tooauthenticate con sus cuentas de Windows Server Active Directory y consumir cualquier API que Azure AD le ayuda a proteger, como Hola API de Office 365 o hello Azure API web.

Para las aplicaciones de JavaScript que se ejecuta en un explorador, Azure AD proporciona Hola biblioteca de autenticación de Active Directory (ADAL) o adal.js. Hola único propósito de adal.js es toomake más sencilla para los tokens de acceso de tooget de su aplicación. toodemonstrate lo fácil es, a continuación, crearemos una aplicación de la lista de AngularJS tooDo que:

* Usuario de hello signos en toohello aplicación mediante Azure AD como proveedor de identidades de Hola.

* Muestra información acerca del usuario de Hola.
* Forma segura llamadas Hola tooDo de la aplicación API de la lista mediante el uso de tokens de portador de Azure AD.
* Signos de Hola usuario fuera de la aplicación hello.

aplicación toobuild Hola completa, trabajo, debe:

1. Registrar la aplicación con Azure AD.
2. Instalar AAL y configurar la aplicación de la página de hello.
3. Usar páginas seguras toohelp AAL en aplicación de la página de hello.

tooget iniciado, [descargar esqueleto de aplicación Hola](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip). También necesita a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación. Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).

## <a name="step-1-register-hello-directorysearcher-application"></a>Paso 1: Registrar aplicación de DirectorySearcher hello
tooenable aplicación tooauthenticate usuarios y tokens de get, primero debe tooregister en Azure AD de los inquilinos:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Si ha iniciado sesión toomultiple directorios, debe tooensure que está viendo el directorio correcto de Hola. toodo por lo tanto, en la barra superior de hello, haga clic en su cuenta. En hello **Directory** elija inquilino hello Azure AD en el que desea tooregister la aplicación.
3. Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.
5. Siga las indicaciones de Hola y cree una nueva aplicación web o API web:
  * **Nombre** describe su toousers de aplicación.
  * **Uri de redireccionamiento** es toowhich de ubicación de hello Azure AD devolverá tokens. ubicación predeterminada de Hola para este ejemplo es `https://localhost:44326/`.
6. Cuando termine de registro, Azure AD le asigna una aplicación de tooyour de Id. de aplicación exclusivo.  Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la pestaña de la aplicación hello.
7. Adal.js usa hello OAuth flujo implícito toocommunicate con Azure AD. Debe habilitar el flujo implícito de hello para la aplicación:
  1. Haga clic en la aplicación hello y seleccione **manifiesto** editor de manifiestos de tooopen hello en línea.
  2. Busque hello `oauth2AllowImplicitFlow` propiedad. Establezca su valor demasiado`true`.
  3. Haga clic en **guardar** toosave manifiesto de Hola.
8. Conceda permisos para la aplicación en todo el inquilino. Vaya demasiado**configuración** > **propiedades** > **permisos necesarios**y haga clic en hello **conceder permisos**botón de barra superior Hola. Haga clic en **Sí** tooconfirm.

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>Paso 2: Instalar AAL y configurar la aplicación de la página de hello
Ahora que tiene una aplicación en Azure AD, puede instalar adal.js y escribir el código relacionado con la identidad.

### <a name="configure-hello-javascript-client"></a>Configurar el cliente de JavaScript de Hola
Comienza agregando adal.js toohello TodoSPA proyecto mediante el uso de la consola de administrador de paquetes de saludo:
  1. Descargar [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) y agregue toohello `App/Scripts/` directorio del proyecto.
  2. Descargar [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) y agregue toohello `App/Scripts/` directorio del proyecto.
  3. Cargar cada script antes del fin de Hola Hola `</body>` en `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Configurar servidor de back-end de Hola
Para los tokens de la aplicación hello página tooDo back-end lista API tooaccept desde el Explorador de hello, back-end de hello necesita información de configuración de registro de una aplicación Hola. En hello TodoSPA proyecto, abra `web.config`. Reemplace los valores de hello de elementos de Hola Hola `<appSettings>` Hola de valores de hello tooreflect una sección que usó en el portal de Azure. El código hará referencia a estos valores siempre que use ADAL.
  * `ida:Tenant`es el dominio de hello del inquilino de Azure AD: por ejemplo, contoso.onmicrosoft.com.
  * `ida:Audience`es el Id. de cliente de saludo de la aplicación que ha copiado desde el portal de Hola.

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>Paso 3: Utilizan toohelp AAL seguras páginas de aplicación de la página de hello
Adal.js se integra con la ruta de AngularJS y los proveedores HTTP, por lo que puede ayudar a proteger vistas individuales en la aplicación de una sola página.

1. En `App/Scripts/app.js`, poner en el módulo de Hola adal.js:

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. Inicializar `adalProvider` mediante los valores de configuración de Hola de su registro de la aplicación, también en `App/Scripts/app.js`:

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. Ayudar a Hola segura `TodoList` vista en la aplicación hello mediante el uso de una única línea de código: `requireADLogin`.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>Resumen
Ahora tiene una aplicación de página segura que se puede iniciar sesión en los usuarios y emitir solicitudes de token de portador protegido tooits back-end API. Cuando un usuario hace clic en hello **TodoList** vínculo, adal.js le redirigirá automáticamente tooAzure AD para inicio de sesión si es necesario. Además, adal.js se asociará automáticamente un acceso token tooany Ajax solicita que se envían back-end de la aplicación toohello.  

Hello pasos anteriores están toobuild necesaria mínima una aplicación de la página de reconstrucción de hello mediante adal.js. Pero algunas otras características son útiles en una aplicación de una sola página:

* tooexplicitly emitir solicitudes de inicio de sesión y cierre de sesión, puede definir las funciones en los controladores que invocan adal.js.  En `App/Scripts/homeCtrl.js`:

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* Conviene toopresent información de usuario en la interfaz de usuario de la aplicación hello. Hola AAL servicio ya se ha agregado toohello `userDataCtrl` controlador, para que pueda acceder hello `userInfo` objeto Hola asociado a la vista, `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* Hay muchos escenarios en los que es conveniente tooknow si el usuario de hello ha iniciado sesión o no. También puede usar hello `userInfo` objeto toogather esta información.  Por ejemplo, en `index.html`, puede mostrar cualquier hello **inicio de sesión** o **Logout** botón de acuerdo con el estado de autenticación:

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

La aplicación de página única integrada en AD Azure puede autenticar a los usuarios, con seguridad llame a su back-end mediante OAuth 2.0 y obtener información básica acerca del usuario de Hola. Si no lo ha hecho ya, ahora es Hola tiempo toopopulate el inquilino con algunos usuarios. Ejecutar la aplicación de una página de lista de tooDo y, inicie sesión con uno de esos usuarios. Agregar la lista de tareas del usuario de las tareas toohello, cierre la sesión y volverla a iniciar.

Adal.js hace fácil tooincorporate características de identidad comunes en la aplicación. Se encarga de todo el trabajo dirty Hola para usted: administración de la caché, compatibilidad con el protocolo OAuth, presentar usuario Hola con un inicio de sesión de interfaz de usuario, actualizar tokens caducados y mucho más.

Como referencia, está disponible en el ejemplo de Hola finalizado (sin los valores de configuración) [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).

## <a name="next-steps"></a>Pasos siguientes
Ahora puede mover en escenarios de tooadditional. Es recomendable tootry: [llamar a una API web CORS desde una aplicación de la página](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
