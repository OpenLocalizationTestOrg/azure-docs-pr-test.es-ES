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
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a><span data-ttu-id="9669b-103">Agregar aplicación de una página de inicio de sesión tooan AngularJS - .NET</span><span class="sxs-lookup"><span data-stu-id="9669b-103">Add sign-in tooan AngularJS single page app - .NET</span></span>
<span data-ttu-id="9669b-104">En este artículo, vamos a agregar inicie sesión con la aplicación de AngularJS tooan Microsoft con la tecnología de cuentas con el punto de conexión de hello Azure Active Directory v2.0.</span><span class="sxs-lookup"><span data-stu-id="9669b-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="9669b-105">el punto de conexión de Hello v2.0 permite tooperform una integración única de la aplicación y autenticar a los usuarios con cuentas personales y de trabajo o escuela.</span><span class="sxs-lookup"><span data-stu-id="9669b-105">hello v2.0 endpoint enables you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="9669b-106">Este ejemplo es una aplicación simple de una página lista de tareas que almacena las tareas en un back-end de API de REST, escrito con marco de MVC de .NET 4.5 de Hola y segura mediante el uso de tokens de portador de OAuth de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9669b-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using hello .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="9669b-107">Hello AngularJS aplicación usará nuestra biblioteca de autenticación de JavaScript de código abierto [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle Hola el proceso de inicio de sesión completo y adquirir tokens de Hola que realiza la llamada API de REST.</span><span class="sxs-lookup"><span data-stu-id="9669b-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="9669b-108">Hello mismo modelo puede ser aplicada tooauthenticate tooother API de REST, como hello [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9669b-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="9669b-109">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="9669b-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="9669b-110">toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="9669b-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="9669b-111">Descargar</span><span class="sxs-lookup"><span data-stu-id="9669b-111">Download</span></span>
<span data-ttu-id="9669b-112">tooget iniciado, será necesario toodownload & instalar Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9669b-112">tooget started, you'll need toodownload & install Visual Studio.</span></span>  <span data-ttu-id="9669b-113">Luego, puede clonar o [descargar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) una aplicación de esqueleto:</span><span class="sxs-lookup"><span data-stu-id="9669b-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="9669b-114">aplicación esqueleto de Hello incluye todo el código Hola reutilizable para una aplicación sencilla de AngularJS, pero le falta todas partes relacionadas con la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9669b-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="9669b-115">Si no desea toofollow a lo largo de, en su lugar, se pueden clonar o [descargar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) ejemplo hello completado.</span><span class="sxs-lookup"><span data-stu-id="9669b-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="9669b-116">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="9669b-116">Register an app</span></span>
<span data-ttu-id="9669b-117">En primer lugar, cree una aplicación Hola [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o siga estas [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="9669b-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="9669b-118">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="9669b-118">Make sure to:</span></span>

* <span data-ttu-id="9669b-119">Agregar hello **Web** plataforma para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9669b-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="9669b-120">Escriba Hola correcto **URI de redireccionamiento**.</span><span class="sxs-lookup"><span data-stu-id="9669b-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="9669b-121">valor predeterminado de Hola para este ejemplo es `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="9669b-121">hello default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="9669b-122">Deje hello **Permitir flujo implícito** casilla habilitada.</span><span class="sxs-lookup"><span data-stu-id="9669b-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="9669b-123">Copia hacia abajo hello **Id. de aplicación** aplicación tooyour asignado, ya que lo necesitará en breve.</span><span class="sxs-lookup"><span data-stu-id="9669b-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="9669b-124">Instalación de adal.js</span><span class="sxs-lookup"><span data-stu-id="9669b-124">Install adal.js</span></span>
<span data-ttu-id="9669b-125">toostart, navegue tooproject descargó e instalar adal.js.</span><span class="sxs-lookup"><span data-stu-id="9669b-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="9669b-126">Si tiene [bower](http://bower.io/) instalado, solo puede ejecutar este comando.</span><span class="sxs-lookup"><span data-stu-id="9669b-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="9669b-127">Para cualquier discrepancia de versión de dependencia, elija una versión superior Hola.</span><span class="sxs-lookup"><span data-stu-id="9669b-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="9669b-128">Como alternativa, puede descargar manualmente [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) y [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="9669b-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="9669b-129">Agregar ambos archivos toohello `app/lib/adal-angular-experimental/dist` directorio de hello `TodoSPA` proyecto.</span><span class="sxs-lookup"><span data-stu-id="9669b-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory of hello `TodoSPA` project.</span></span>

<span data-ttu-id="9669b-130">Ahora abra el proyecto de hello en Visual Studio y cargar adal.js final Hola del cuerpo de la página principal de hello:</span><span class="sxs-lookup"><span data-stu-id="9669b-130">Now open hello project in Visual Studio, and load adal.js at hello end of hello main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="9669b-131">Configurar Hola API de REST</span><span class="sxs-lookup"><span data-stu-id="9669b-131">Set up hello REST API</span></span>
<span data-ttu-id="9669b-132">Mientras estamos configurando cosas, supongamos que funcione de API de REST de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="9669b-132">While we're setting things up, let's get hello backend REST API working.</span></span>  <span data-ttu-id="9669b-133">En la raíz de hello del proyecto de hello, abra `web.config` y reemplazar hello `audience` valor.</span><span class="sxs-lookup"><span data-stu-id="9669b-133">In hello root of hello project, open `web.config` and replace hello `audience` value.</span></span>  <span data-ttu-id="9669b-134">API de REST de Hello utilizará este testigos de toovalidate de valor recibe de aplicación Angular hello en las solicitudes de AJAX.</span><span class="sxs-lookup"><span data-stu-id="9669b-134">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="9669b-135">Eso es todo tiempo Hola vamos toospend hablar sobre cómo funciona la API de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="9669b-135">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="9669b-136">Cree toopoke libre en el código de hello, pero si desea que toolearn más acerca de cómo proteger web API con Azure AD, consulte [este artículo](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="9669b-136">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="9669b-137">Inicio de sesión de los usuarios</span><span class="sxs-lookup"><span data-stu-id="9669b-137">Sign users in</span></span>
<span data-ttu-id="9669b-138">Tiempo toowrite algún código de identidad.</span><span class="sxs-lookup"><span data-stu-id="9669b-138">Time toowrite some identity code.</span></span>  <span data-ttu-id="9669b-139">Es posible que haya notado que adal.js contiene un proveedor de AngularJS, que se reproduce perfectamente con los mecanismos de enrutamiento de Angular.</span><span class="sxs-lookup"><span data-stu-id="9669b-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="9669b-140">Empiece por Agregar aplicación de hello módulo AAL toohello:</span><span class="sxs-lookup"><span data-stu-id="9669b-140">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="9669b-141">Ahora puede inicializar hello `adalProvider` con el identificador de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="9669b-141">You can now initialize hello `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="9669b-142">Muy bien, ahora adal.js tiene toda la información de hello debe toosecure los usuarios de aplicación e inicie sesión en.</span><span class="sxs-lookup"><span data-stu-id="9669b-142">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="9669b-143">tooforce inicio de sesión para una determinada ruta de la aplicación hello, todo lo necesario es una línea de código:</span><span class="sxs-lookup"><span data-stu-id="9669b-143">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="9669b-144">Ahora cuando un usuario hace clic en hello `TodoList` vínculo, adal.js le redirigirá automáticamente tooAzure AD para inicio de sesión si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9669b-144">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="9669b-145">También puede enviar explícitamente solicitudes de inicio y cierre de sesión mediante la invocación de adal.js en sus controladores:</span><span class="sxs-lookup"><span data-stu-id="9669b-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="9669b-146">Visualización de la información de usuario</span><span class="sxs-lookup"><span data-stu-id="9669b-146">Display user info</span></span>
<span data-ttu-id="9669b-147">Ahora que hello usuario ha iniciado sesión, probablemente necesitará datos de autenticación tooaccess Hola inició sesión del usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9669b-147">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="9669b-148">Adal.js expone esta información en hello `userInfo` objeto.</span><span class="sxs-lookup"><span data-stu-id="9669b-148">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="9669b-149">tooaccess este objeto en una vista, primero agregue adal.js toohello ámbito de raíz de controlador de hello correspondiente:</span><span class="sxs-lookup"><span data-stu-id="9669b-149">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="9669b-150">A continuación, se pueden resolver directamente hello `userInfo` objeto en la vista:</span><span class="sxs-lookup"><span data-stu-id="9669b-150">Then you can directly address hello `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="9669b-151">También puede usar hello `userInfo` toodetermine del objeto si el usuario de hello ha iniciado sesión o no.</span><span class="sxs-lookup"><span data-stu-id="9669b-151">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

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

## <a name="call-hello-rest-api"></a><span data-ttu-id="9669b-152">Hola llamada API de REST</span><span class="sxs-lookup"><span data-stu-id="9669b-152">Call hello REST API</span></span>
<span data-ttu-id="9669b-153">Por último, es hora tooget algunos símbolos (tokens) y la llamada Hola toocreate de API de REST, leerán, actualizarán y eliminar tareas.</span><span class="sxs-lookup"><span data-stu-id="9669b-153">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="9669b-154">Bien, ¿sabe qué?</span><span class="sxs-lookup"><span data-stu-id="9669b-154">Well guess what?</span></span>  <span data-ttu-id="9669b-155">No tienes toodo *algo*.</span><span class="sxs-lookup"><span data-stu-id="9669b-155">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="9669b-156">Adal.js se encarga automáticamente de obtener, almacenar en caché y actualizar los tokens.</span><span class="sxs-lookup"><span data-stu-id="9669b-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="9669b-157">También se encargará de asociar esos tokens que toooutgoing AJAX solicita que enviar toohello API de REST.</span><span class="sxs-lookup"><span data-stu-id="9669b-157">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="9669b-158">¿Cómo funciona esto exactamente?</span><span class="sxs-lookup"><span data-stu-id="9669b-158">How exactly does this work?</span></span> <span data-ttu-id="9669b-159">Es todo gracias toohello mágico de [interceptores de AngularJS](https://docs.angularjs.org/api/ng/service/$http), lo que permite adal.js tootransform mensajes http salientes y entrantes.</span><span class="sxs-lookup"><span data-stu-id="9669b-159">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="9669b-160">Además, adal.js se da por supuesto que las solicitudes de envío toohello mismo dominio como ventana hello debe usar tokens destinado a Hola mismo identificador de aplicación como aplicación de AngularJS de Hola.</span><span class="sxs-lookup"><span data-stu-id="9669b-160">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="9669b-161">Por lo tanto, hemos usado Hola mismo identificador de aplicación en ambas aplicaciones Angular Hola y Hola NodeJS API de REST.</span><span class="sxs-lookup"><span data-stu-id="9669b-161">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="9669b-162">Por supuesto, puede invalidar este comportamiento y saber adal.js tooget tokens para otras API de REST si es necesario - pero por este Hola escenario sencillo los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="9669b-162">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="9669b-163">Este es un fragmento de código que muestra lo fácil que es toosend solicitudes con tokens de portador de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9669b-163">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="9669b-164">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="9669b-164">Congratulations!</span></span>  <span data-ttu-id="9669b-165">La aplicación de una sola página integrada de Azure AD está terminada ahora.</span><span class="sxs-lookup"><span data-stu-id="9669b-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="9669b-166">!Ya puede salir a recibir el aplauso del público!</span><span class="sxs-lookup"><span data-stu-id="9669b-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="9669b-167">Puede autenticar a los usuarios, seguro llamar a su API de REST mediante OpenID Connect de back-end y obtener información básica acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9669b-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="9669b-168">Desde el principio de hello, admite cualquier usuario con una Account Microsoft personal o una cuenta de trabajo o escuela de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9669b-168">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="9669b-169">Ejecutar aplicación hello y en un explorador vaya demasiado`https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="9669b-169">Run hello app, and in a browser navigate too`https://localhost:44326/`.</span></span>  <span data-ttu-id="9669b-170">Inicie sesión con una cuenta de Microsoft personal, profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="9669b-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="9669b-171">Agregar la lista de tareas del usuario de las tareas toohello y cierre la sesión.  Intente iniciar sesión con Hola otro tipo de cuenta.</span><span class="sxs-lookup"><span data-stu-id="9669b-171">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="9669b-172">Si necesita un usuarios de trabajo o escuela toocreate del inquilino de Azure AD, [Obtenga información acerca de cómo tooget uno aquí](active-directory-howto-tenant.md) (no disponible).</span><span class="sxs-lookup"><span data-stu-id="9669b-172">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="9669b-173">toocontinue obtener información sobre el punto de conexión de hello v2.0, principal tooour Atrás [Guía del desarrollador v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9669b-173">toocontinue learning about hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="9669b-174">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="9669b-174">For additional resources, check out:</span></span>

* [<span data-ttu-id="9669b-175">Ejemplos de Azure en GitHub &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="9669b-175">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="9669b-176">Azure AD en Stack Overflow &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="9669b-176">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="9669b-177">Documentación de Azure AD en [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="9669b-177">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="9669b-178">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="9669b-178">Get security updates for our products</span></span>
<span data-ttu-id="9669b-179">Le recomendamos que las notificaciones de tooget de cuando se producen incidentes de seguridad visitando [esta página](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.</span><span class="sxs-lookup"><span data-stu-id="9669b-179">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

