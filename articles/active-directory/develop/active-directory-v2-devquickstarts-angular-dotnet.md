---
title: "aaaAzure AD v2.0 .NET AngularJS aplicación de una página Introducción | Documentos de Microsoft"
description: "Cómo la toobuild una aplicación de una página JS Angular que inicia sesión a los usuarios con Microsoft personal cuentas y de trabajo o escolares."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 6a341781-278f-461b-92ca-7572a06e6852
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: bd3fc8dce91eb0bedcbfed47a9b3ef52c5568c6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a>Agregar aplicación de una página de inicio de sesión tooan AngularJS - .NET
En este artículo, vamos a agregar inicie sesión con la aplicación de AngularJS tooan Microsoft con la tecnología de cuentas con el punto de conexión de hello Azure Active Directory v2.0.  el punto de conexión de Hello v2.0 permite tooperform una integración única de la aplicación y autenticar a los usuarios con cuentas personales y de trabajo o escuela.

Este ejemplo es una aplicación simple de una página lista de tareas que almacena las tareas en un back-end de API de REST, escrito con marco de MVC de .NET 4.5 de Hola y segura mediante el uso de tokens de portador de OAuth de Azure AD.  Hello AngularJS aplicación usará nuestra biblioteca de autenticación de JavaScript de código abierto [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle Hola el proceso de inicio de sesión completo y adquirir tokens de Hola que realiza la llamada API de REST.  Hello mismo modelo puede ser aplicada tooauthenticate tooother API de REST, como hello [Microsoft Graph](https://graph.microsoft.com).

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.  toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

## <a name="download"></a>Descargar
tooget iniciado, será necesario toodownload & instalar Visual Studio.  Luego, puede clonar o [descargar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) una aplicación de esqueleto:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

aplicación esqueleto de Hello incluye todo el código Hola reutilizable para una aplicación sencilla de AngularJS, pero le falta todas partes relacionadas con la identidad de Hola.  Si no desea toofollow a lo largo de, en su lugar, se pueden clonar o [descargar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) ejemplo hello completado.

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a>Registrar una aplicación
En primer lugar, cree una aplicación Hola [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o siga estas [pasos detallados](active-directory-v2-app-registration.md).  Asegúrese de que:

* Agregar hello **Web** plataforma para la aplicación.
* Escriba Hola correcto **URI de redireccionamiento**. valor predeterminado de Hola para este ejemplo es `https://localhost:44326/`.
* Deje hello **Permitir flujo implícito** casilla habilitada. 

Copia hacia abajo hello **Id. de aplicación** aplicación tooyour asignado, ya que lo necesitará en breve. 

## <a name="install-adaljs"></a>Instalación de adal.js
toostart, navegue tooproject descargó e instalar adal.js.  Si tiene [bower](http://bower.io/) instalado, solo puede ejecutar este comando.  Para cualquier discrepancia de versión de dependencia, elija una versión superior Hola.

```
bower install adal-angular#experimental
```

Como alternativa, puede descargar manualmente [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) y [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).  Agregar ambos archivos toohello `app/lib/adal-angular-experimental/dist` directorio de hello `TodoSPA` proyecto.

Ahora abra el proyecto de hello en Visual Studio y cargar adal.js final Hola del cuerpo de la página principal de hello:

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a>Configurar Hola API de REST
Mientras estamos configurando cosas, supongamos que funcione de API de REST de back-end de Hola.  En la raíz de hello del proyecto de hello, abra `web.config` y reemplazar hello `audience` valor.  API de REST de Hello utilizará este testigos de toovalidate de valor recibe de aplicación Angular hello en las solicitudes de AJAX.

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

Eso es todo tiempo Hola vamos toospend hablar sobre cómo funciona la API de REST de Hola.  Cree toopoke libre en el código de hello, pero si desea que toolearn más acerca de cómo proteger web API con Azure AD, consulte [este artículo](active-directory-v2-devquickstarts-dotnet-api.md). 

## <a name="sign-users-in"></a>Inicio de sesión de los usuarios
Tiempo toowrite algún código de identidad.  Es posible que haya notado que adal.js contiene un proveedor de AngularJS, que se reproduce perfectamente con los mecanismos de enrutamiento de Angular.  Empiece por Agregar aplicación de hello módulo AAL toohello:

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

Ahora puede inicializar hello `adalProvider` con el identificador de la aplicación:

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for hello public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // hello 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from hello registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - hello default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

Muy bien, ahora adal.js tiene toda la información de hello debe toosecure los usuarios de aplicación e inicie sesión en.  tooforce inicio de sesión para una determinada ruta de la aplicación hello, todo lo necesario es una línea de código:

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that hello user must be logged in tooaccess hello route
})

...
```

Ahora cuando un usuario hace clic en hello `TodoList` vínculo, adal.js le redirigirá automáticamente tooAzure AD para inicio de sesión si es necesario.  También puede enviar explícitamente solicitudes de inicio y cierre de sesión mediante la invocación de adal.js en sus controladores:

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js hello same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect hello user toosign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect hello user toolog out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a>Visualización de la información de usuario
Ahora que hello usuario ha iniciado sesión, probablemente necesitará datos de autenticación tooaccess Hola inició sesión del usuario en la aplicación.  Adal.js expone esta información en hello `userInfo` objeto.  tooaccess este objeto en una vista, primero agregue adal.js toohello ámbito de raíz de controlador de hello correspondiente:

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

A continuación, se pueden resolver directamente hello `userInfo` objeto en la vista: 

```html
<!--app/views/UserData.html-->

...

    <!--Get hello user's profile information from hello ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

También puede usar hello `userInfo` toodetermine del objeto si el usuario de hello ha iniciado sesión o no.

```html
<!--index.html-->

...

    <!--Use hello ADAL userInfo object tooshow hello right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-hello-rest-api"></a>Hola llamada API de REST
Por último, es hora tooget algunos símbolos (tokens) y la llamada Hola toocreate de API de REST, leerán, actualizarán y eliminar tareas.  Bien, ¿sabe qué?  No tienes toodo *algo*.  Adal.js se encarga automáticamente de obtener, almacenar en caché y actualizar los tokens.  También se encargará de asociar esos tokens que toooutgoing AJAX solicita que enviar toohello API de REST.  

¿Cómo funciona esto exactamente? Es todo gracias toohello mágico de [interceptores de AngularJS](https://docs.angularjs.org/api/ng/service/$http), lo que permite adal.js tootransform mensajes http salientes y entrantes.  Además, adal.js se da por supuesto que las solicitudes de envío toohello mismo dominio como ventana hello debe usar tokens destinado a Hola mismo identificador de aplicación como aplicación de AngularJS de Hola.  Por lo tanto, hemos usado Hola mismo identificador de aplicación en ambas aplicaciones Angular Hola y Hola NodeJS API de REST.  Por supuesto, puede invalidar este comportamiento y saber adal.js tooget tokens para otras API de REST si es necesario - pero por este Hola escenario sencillo los valores predeterminados.

Este es un fragmento de código que muestra lo fácil que es toosend solicitudes con tokens de portador de Azure AD:

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

¡Enhorabuena!  La aplicación de una sola página integrada de Azure AD está terminada ahora.  !Ya puede salir a recibir el aplauso del público!  Puede autenticar a los usuarios, seguro llamar a su API de REST mediante OpenID Connect de back-end y obtener información básica acerca del usuario de Hola.  Desde el principio de hello, admite cualquier usuario con una Account Microsoft personal o una cuenta de trabajo o escuela de Azure AD.  Ejecutar aplicación hello y en un explorador vaya demasiado`https://localhost:44326/`.  Inicie sesión con una cuenta de Microsoft personal, profesional o educativa.  Agregar la lista de tareas del usuario de las tareas toohello y cierre la sesión.  Intente iniciar sesión con Hola otro tipo de cuenta. Si necesita un usuarios de trabajo o escuela toocreate del inquilino de Azure AD, [Obtenga información acerca de cómo tooget uno aquí](active-directory-howto-tenant.md) (no disponible).

toocontinue obtener información sobre el punto de conexión de hello v2.0, principal tooour Atrás [Guía del desarrollador v2.0](active-directory-appmodel-v2-overview.md).  Para obtener recursos adicionales, consulte:

* [Ejemplos de Azure en GitHub &gt;&gt;](https://github.com/Azure-Samples)
* [Azure AD en Stack Overflow &gt;&gt;](http://stackoverflow.com/questions/tagged/azure-active-directory)
* Documentación de Azure AD en [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)

## <a name="get-security-updates-for-our-products"></a>Obtención de actualizaciones de seguridad para nuestros productos
Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.

