---
title: "aaaAzure AD v2.0 NodeJS AngularJS aplicación de una página Introducción | Documentos de Microsoft"
description: "Cómo la toobuild una aplicación de una página JS Angular que inicia sesión a los usuarios con Microsoft personal cuentas y de trabajo o escolares."
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 1ab450caf08ab05fba140b94b1b8de652e99cbc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a><span data-ttu-id="06273-103">Agregar aplicación de una página de inicio de sesión tooan AngularJS - NodeJS</span><span class="sxs-lookup"><span data-stu-id="06273-103">Add sign-in tooan AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="06273-104">En este artículo, vamos a agregar inicie sesión con la aplicación de AngularJS tooan Microsoft con la tecnología de cuentas con el punto de conexión de hello Azure Active Directory v2.0.</span><span class="sxs-lookup"><span data-stu-id="06273-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="06273-105">el punto de conexión de Hello v2.0 permiten tooperform una integración única de la aplicación y autenticar a los usuarios con cuentas personales y de trabajo o escuela.</span><span class="sxs-lookup"><span data-stu-id="06273-105">hello v2.0 endpoint enable you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="06273-106">Este ejemplo es una sencilla aplicación de lista de tareas de una sola página que almacena las tareas en una API de REST de back-end, escrita en NodeJS y protegida con tokens de portador OAuth de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06273-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="06273-107">Hello AngularJS aplicación usará nuestra biblioteca de autenticación de JavaScript de código abierto [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle Hola el proceso de inicio de sesión completo y adquirir tokens de Hola que realiza la llamada API de REST.</span><span class="sxs-lookup"><span data-stu-id="06273-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="06273-108">Hello mismo modelo puede ser aplicada tooauthenticate tooother API de REST, como hello [Microsoft Graph](https://graph.microsoft.com) o hello las API del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="06273-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com) or hello Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="06273-109">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="06273-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="06273-110">toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="06273-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="06273-111">Descargar</span><span class="sxs-lookup"><span data-stu-id="06273-111">Download</span></span>
<span data-ttu-id="06273-112">tooget iniciado, necesitará toodownload & instalar [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="06273-112">tooget started, you'll need toodownload & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="06273-113">Luego, puede clonar o [descargar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) una aplicación de esqueleto:</span><span class="sxs-lookup"><span data-stu-id="06273-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="06273-114">aplicación esqueleto de Hello incluye todo el código Hola reutilizable para una aplicación sencilla de AngularJS, pero le falta todas partes relacionadas con la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="06273-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="06273-115">Si no desea toofollow a lo largo de, en su lugar, se pueden clonar o [descargar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) ejemplo hello completado.</span><span class="sxs-lookup"><span data-stu-id="06273-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="06273-116">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="06273-116">Register an app</span></span>
<span data-ttu-id="06273-117">En primer lugar, cree una aplicación Hola [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o siga estas [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="06273-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="06273-118">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="06273-118">Make sure to:</span></span>

* <span data-ttu-id="06273-119">Agregar hello **Web** plataforma para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="06273-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="06273-120">Escriba Hola correcto **URI de redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="06273-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="06273-121">valor predeterminado de Hola para este ejemplo es `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="06273-121">hello default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="06273-122">Deje hello **Permitir flujo implícito** casilla habilitada.</span><span class="sxs-lookup"><span data-stu-id="06273-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="06273-123">Copia hacia abajo hello **Id. de aplicación** aplicación tooyour asignado, ya que lo necesitará en breve.</span><span class="sxs-lookup"><span data-stu-id="06273-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="06273-124">Instalación de adal.js</span><span class="sxs-lookup"><span data-stu-id="06273-124">Install adal.js</span></span>
<span data-ttu-id="06273-125">toostart, navegue tooproject descargó e instalar adal.js.</span><span class="sxs-lookup"><span data-stu-id="06273-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="06273-126">Si tiene [bower](http://bower.io/) instalado, solo puede ejecutar este comando.</span><span class="sxs-lookup"><span data-stu-id="06273-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="06273-127">Para cualquier discrepancia de versión de dependencia, elija una versión superior Hola.</span><span class="sxs-lookup"><span data-stu-id="06273-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="06273-128">Como alternativa, puede descargar manualmente [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) y [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="06273-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="06273-129">Agregar ambos toohello archivos `app/lib/adal-angular-experimental/dist` directory.</span><span class="sxs-lookup"><span data-stu-id="06273-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="06273-130">Ahora abra el proyecto de hello en el editor de texto que prefiera y cargar adal.js final Hola del cuerpo de la página de hello:</span><span class="sxs-lookup"><span data-stu-id="06273-130">Now open hello project in your favorite text editor, and load adal.js at hello end of hello page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="06273-131">Configurar Hola API de REST</span><span class="sxs-lookup"><span data-stu-id="06273-131">Set up hello REST API</span></span>
<span data-ttu-id="06273-132">Mientras estamos configurando cosas, permite trabajar de API de REST de get hello back-end.</span><span class="sxs-lookup"><span data-stu-id="06273-132">While we're setting things up, lets get hello backend REST API working.</span></span>  <span data-ttu-id="06273-133">En un símbolo del sistema, instale todos los paquetes necesarios Hola ejecutando (asegúrese de que se encuentra en el directorio de nivel superior de hello del proyecto de hello):</span><span class="sxs-lookup"><span data-stu-id="06273-133">In a command prompt, install all hello necessary packages by running (make sure you're in hello top-level directory of hello project):</span></span>

```
npm install
```

<span data-ttu-id="06273-134">Ahora, abra `config.js` y reemplazar hello `audience` valor:</span><span class="sxs-lookup"><span data-stu-id="06273-134">Now open `config.js` and replace hello `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="06273-135">API de REST de Hello utilizará este testigos de toovalidate de valor recibe de aplicación Angular hello en las solicitudes de AJAX.</span><span class="sxs-lookup"><span data-stu-id="06273-135">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>  <span data-ttu-id="06273-136">Tenga en cuenta que esta API de REST simple almacena datos en memoria: por lo que cada servidor de tiempo toostop hello, perderá todas las tareas creadas con anterioridad.</span><span class="sxs-lookup"><span data-stu-id="06273-136">Note that this simple REST API stores data in-memory - so each time toostop hello server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="06273-137">Eso es todo tiempo Hola vamos toospend hablar sobre cómo funciona la API de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="06273-137">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="06273-138">Cree toopoke libre en el código de hello, pero si desea que toolearn más acerca de cómo proteger web API con Azure AD, consulte [este artículo](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="06273-138">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="06273-139">Inicio de sesión de los usuarios</span><span class="sxs-lookup"><span data-stu-id="06273-139">Sign users in</span></span>
<span data-ttu-id="06273-140">Tiempo toowrite algún código de identidad.</span><span class="sxs-lookup"><span data-stu-id="06273-140">Time toowrite some identity code.</span></span>  <span data-ttu-id="06273-141">Es posible que haya notado que adal.js contiene un proveedor de AngularJS, que se reproduce perfectamente con los mecanismos de enrutamiento de Angular.</span><span class="sxs-lookup"><span data-stu-id="06273-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="06273-142">Empiece por Agregar aplicación de hello módulo AAL toohello:</span><span class="sxs-lookup"><span data-stu-id="06273-142">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="06273-143">Ahora puede inicializar hello `adalProvider` con el identificador de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="06273-143">You can now initialize hello `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="06273-144">Muy bien, ahora adal.js tiene toda la información de hello debe toosecure los usuarios de aplicación e inicie sesión en.</span><span class="sxs-lookup"><span data-stu-id="06273-144">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="06273-145">tooforce inicio de sesión para una determinada ruta de la aplicación hello, todo lo necesario es una línea de código:</span><span class="sxs-lookup"><span data-stu-id="06273-145">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="06273-146">Ahora cuando un usuario hace clic en hello `TodoList` vínculo, adal.js le redirigirá automáticamente tooAzure AD para inicio de sesión si es necesario.</span><span class="sxs-lookup"><span data-stu-id="06273-146">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="06273-147">También puede enviar explícitamente solicitudes de inicio y cierre de sesión mediante la invocación de adal.js en sus controladores:</span><span class="sxs-lookup"><span data-stu-id="06273-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="06273-148">Visualización de la información de usuario</span><span class="sxs-lookup"><span data-stu-id="06273-148">Display user info</span></span>
<span data-ttu-id="06273-149">Ahora que hello usuario ha iniciado sesión, probablemente necesitará datos de autenticación tooaccess Hola inició sesión del usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="06273-149">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="06273-150">Adal.js expone esta información en hello `userInfo` objeto.</span><span class="sxs-lookup"><span data-stu-id="06273-150">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="06273-151">tooaccess este objeto en una vista, primero agregue adal.js toohello ámbito de raíz de controlador de hello correspondiente:</span><span class="sxs-lookup"><span data-stu-id="06273-151">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="06273-152">A continuación, se pueden resolver directamente hello `userInfo` objeto en la vista:</span><span class="sxs-lookup"><span data-stu-id="06273-152">Then you can directly address hello `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="06273-153">También puede usar hello `userInfo` toodetermine del objeto si el usuario de hello ha iniciado sesión o no.</span><span class="sxs-lookup"><span data-stu-id="06273-153">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

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

## <a name="call-hello-rest-api"></a><span data-ttu-id="06273-154">Hola llamada API de REST</span><span class="sxs-lookup"><span data-stu-id="06273-154">Call hello REST API</span></span>
<span data-ttu-id="06273-155">Por último, es hora tooget algunos símbolos (tokens) y la llamada Hola toocreate de API de REST, leerán, actualizarán y eliminar tareas.</span><span class="sxs-lookup"><span data-stu-id="06273-155">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="06273-156">Bien, ¿sabe qué?</span><span class="sxs-lookup"><span data-stu-id="06273-156">Well guess what?</span></span>  <span data-ttu-id="06273-157">No tienes toodo *algo*.</span><span class="sxs-lookup"><span data-stu-id="06273-157">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="06273-158">Adal.js se encarga automáticamente de obtener, almacenar en caché y actualizar los tokens.</span><span class="sxs-lookup"><span data-stu-id="06273-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="06273-159">También se encargará de asociar esos tokens que toooutgoing AJAX solicita que enviar toohello API de REST.</span><span class="sxs-lookup"><span data-stu-id="06273-159">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="06273-160">¿Cómo funciona esto exactamente?</span><span class="sxs-lookup"><span data-stu-id="06273-160">How exactly does this work?</span></span> <span data-ttu-id="06273-161">Es todo gracias toohello mágico de [interceptores de AngularJS](https://docs.angularjs.org/api/ng/service/$http), lo que permite adal.js tootransform mensajes http salientes y entrantes.</span><span class="sxs-lookup"><span data-stu-id="06273-161">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="06273-162">Además, adal.js se da por supuesto que las solicitudes de envío toohello mismo dominio como ventana hello debe usar tokens destinado a Hola mismo identificador de aplicación como aplicación de AngularJS de Hola.</span><span class="sxs-lookup"><span data-stu-id="06273-162">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="06273-163">Por lo tanto, hemos usado Hola mismo identificador de aplicación en ambas aplicaciones Angular Hola y Hola NodeJS API de REST.</span><span class="sxs-lookup"><span data-stu-id="06273-163">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="06273-164">Por supuesto, puede invalidar este comportamiento y saber adal.js tooget tokens para otras API de REST si es necesario - pero por este Hola escenario sencillo los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="06273-164">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="06273-165">Este es un fragmento de código que muestra lo fácil que es toosend solicitudes con tokens de portador de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="06273-165">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="06273-166">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="06273-166">Congratulations!</span></span>  <span data-ttu-id="06273-167">La aplicación de una sola página integrada de Azure AD está terminada ahora.</span><span class="sxs-lookup"><span data-stu-id="06273-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="06273-168">!Ya puede salir a recibir el aplauso del público!</span><span class="sxs-lookup"><span data-stu-id="06273-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="06273-169">Puede autenticar a los usuarios, seguro llamar a su API de REST mediante OpenID Connect de back-end y obtener información básica acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="06273-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="06273-170">Desde el principio de hello, admite cualquier usuario con una Account Microsoft personal o una cuenta de trabajo o escuela de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06273-170">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="06273-171">Pruebe aplicación hello ejecutando:</span><span class="sxs-lookup"><span data-stu-id="06273-171">Give hello app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="06273-172">En un explorador vaya demasiado`http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="06273-172">In a browser navigate too`http://localhost:8080`.</span></span>  <span data-ttu-id="06273-173">Inicie sesión con una cuenta de Microsoft personal, profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="06273-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="06273-174">Agregar la lista de tareas del usuario de las tareas toohello y cierre la sesión.  Intente iniciar sesión con Hola otro tipo de cuenta.</span><span class="sxs-lookup"><span data-stu-id="06273-174">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="06273-175">Si necesita un usuarios de trabajo o escuela toocreate del inquilino de Azure AD, [Obtenga información acerca de cómo tooget uno aquí](active-directory-howto-tenant.md) (no disponible).</span><span class="sxs-lookup"><span data-stu-id="06273-175">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="06273-176">toocontinue conocer Hola Hola extremo v2.0, head atrás tooour [Guía del desarrollador v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="06273-176">toocontinue learning about hello hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="06273-177">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="06273-177">For additional resources, check out:</span></span>

* [<span data-ttu-id="06273-178">Ejemplos de Azure en GitHub &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="06273-178">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="06273-179">Azure AD en Stack Overflow &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="06273-179">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="06273-180">Documentación de Azure AD en [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="06273-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="06273-181">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="06273-181">Get security updates for our products</span></span>
<span data-ttu-id="06273-182">Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.</span><span class="sxs-lookup"><span data-stu-id="06273-182">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

