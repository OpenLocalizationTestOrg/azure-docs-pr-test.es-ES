---
title: "Introducción a la aplicación de página única de AngularJS de NodeJS v2.0 de Azure AD | Microsoft Docs"
description: "Cómo crear una aplicación de una página Angular JS que inicia la sesión de los usuarios tanto con cuentas de Microsoft personales como educativas o profesionales."
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
ms.openlocfilehash: 0e90171afd9c4c782fbb18375ab2d147497ef442
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---nodejs"></a><span data-ttu-id="3bdba-103">Agregar inicio de sesión a una aplicación de una página AngularJS (NodeJS)</span><span class="sxs-lookup"><span data-stu-id="3bdba-103">Add sign-in to an AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="3bdba-104">En este artículo vamos a agregar inicio de sesión con cuentas con tecnología de Microsoft a una aplicación AngularJS mediante el punto de conexión de Azure Active Directory v2.0.</span><span class="sxs-lookup"><span data-stu-id="3bdba-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="3bdba-105">El punto de conexión v2.0 permite realizar una sola integración en la aplicación y autenticar a los usuarios tanto con cuentas personales como profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="3bdba-105">the v2.0 endpoint enable you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="3bdba-106">Este ejemplo es una sencilla aplicación de lista de tareas de una sola página que almacena las tareas en una API de REST de back-end, escrita en NodeJS y protegida con tokens de portador OAuth de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bdba-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="3bdba-107">La aplicación AngularJS usará nuestra biblioteca de autenticación JavaScript de código abierto [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) para gestionar el proceso completo de inicio de sesión y adquirir tokens para llamar a la API de REST.</span><span class="sxs-lookup"><span data-stu-id="3bdba-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="3bdba-108">Se puede aplicar el mismo patrón para autenticarse en otras API de REST, como las API de [Microsoft Graph](https://graph.microsoft.com) o del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3bdba-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com) or the Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="3bdba-109">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión v2.0.</span><span class="sxs-lookup"><span data-stu-id="3bdba-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="3bdba-110">Para determinar si debe usar el punto de conexión v2.0, lea acerca de las [limitaciones de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3bdba-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="3bdba-111">Descargar</span><span class="sxs-lookup"><span data-stu-id="3bdba-111">Download</span></span>
<span data-ttu-id="3bdba-112">Para comenzar, necesitará descargar e instalar [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="3bdba-112">To get started, you'll need to download & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="3bdba-113">Luego, puede clonar o [descargar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) una aplicación de esqueleto:</span><span class="sxs-lookup"><span data-stu-id="3bdba-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="3bdba-114">La aplicación de esqueleto incluye todo el código reutilizable para una aplicación sencilla de AngularJS, pero faltan todas las partes relacionadas con la identidad.</span><span class="sxs-lookup"><span data-stu-id="3bdba-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="3bdba-115">Si no desea continuar por este camino, en su lugar puede clonar o [descargar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) el ejemplo finalizado.</span><span class="sxs-lookup"><span data-stu-id="3bdba-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="3bdba-116">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="3bdba-116">Register an app</span></span>
<span data-ttu-id="3bdba-117">En primer lugar, cree una aplicación en el [Portal de registro de aplicaciones](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga estos [pasos detallados](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3bdba-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="3bdba-118">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="3bdba-118">Make sure to:</span></span>

* <span data-ttu-id="3bdba-119">Agrega la plataforma **web** para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="3bdba-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="3bdba-120">Escribe el **URI de redireccionamiento**correcto.</span><span class="sxs-lookup"><span data-stu-id="3bdba-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="3bdba-121">El valor predeterminado en este ejemplo es `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="3bdba-121">The default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="3bdba-122">Deja la casilla **Permitir flujo implícito** habilitada.</span><span class="sxs-lookup"><span data-stu-id="3bdba-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="3bdba-123">Anota el valor de **Id. de aplicación** asignado a su aplicación; lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="3bdba-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="3bdba-124">Instalación de adal.js</span><span class="sxs-lookup"><span data-stu-id="3bdba-124">Install adal.js</span></span>
<span data-ttu-id="3bdba-125">Para comenzar, vaya al proyecto que ha descargado e instale adal.js.</span><span class="sxs-lookup"><span data-stu-id="3bdba-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="3bdba-126">Si tiene [bower](http://bower.io/) instalado, solo puede ejecutar este comando.</span><span class="sxs-lookup"><span data-stu-id="3bdba-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="3bdba-127">Si aparecen errores de coincidencia en relación con la versión de dependencia, elija la versión superior.</span><span class="sxs-lookup"><span data-stu-id="3bdba-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="3bdba-128">Como alternativa, puede descargar manualmente [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) y [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="3bdba-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="3bdba-129">Agregue ambos archivos al directorio `app/lib/adal-angular-experimental/dist` .</span><span class="sxs-lookup"><span data-stu-id="3bdba-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="3bdba-130">Ahora abra el proyecto en el editor de texto que prefiera y cargue adal.js al final del cuerpo de la página:</span><span class="sxs-lookup"><span data-stu-id="3bdba-130">Now open the project in your favorite text editor, and load adal.js at the end of the page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="3bdba-131">Configuración de la API de REST</span><span class="sxs-lookup"><span data-stu-id="3bdba-131">Set up the REST API</span></span>
<span data-ttu-id="3bdba-132">Mientras realizamos todas estas configuraciones, vamos a poner en funcionamiento la API de REST de back-end.</span><span class="sxs-lookup"><span data-stu-id="3bdba-132">While we're setting things up, lets get the backend REST API working.</span></span>  <span data-ttu-id="3bdba-133">En un símbolo del sistema, instale todos los paquetes necesarios, para ello, ejecute (asegúrese de que se encuentra en el directorio de nivel superior del proyecto):</span><span class="sxs-lookup"><span data-stu-id="3bdba-133">In a command prompt, install all the necessary packages by running (make sure you're in the top-level directory of the project):</span></span>

```
npm install
```

<span data-ttu-id="3bdba-134">Ahora abra `config.js` y reemplace el valor de `audience`:</span><span class="sxs-lookup"><span data-stu-id="3bdba-134">Now open `config.js` and replace the `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with the Application ID from the registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="3bdba-135">La API de REST usará este valor para validar los tokens que recibe de la aplicación Angular en las solicitudes AJAX.</span><span class="sxs-lookup"><span data-stu-id="3bdba-135">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>  <span data-ttu-id="3bdba-136">Tenga en cuenta que esta sencilla API de REST almacena datos en memoria, así que cada vez que se detenga el servidor, se perderán todas las tareas creadas con anterioridad.</span><span class="sxs-lookup"><span data-stu-id="3bdba-136">Note that this simple REST API stores data in-memory - so each time to stop the server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="3bdba-137">Ese es todo el tiempo que vamos a dedicar a hablar de cómo funciona la API de REST.</span><span class="sxs-lookup"><span data-stu-id="3bdba-137">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="3bdba-138">No dude en echar un vistazo al código, pero si desea aprender más sobre cómo proteger las API web con Azure AD, consulte [este artículo](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="3bdba-138">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="3bdba-139">Inicio de sesión de los usuarios</span><span class="sxs-lookup"><span data-stu-id="3bdba-139">Sign users in</span></span>
<span data-ttu-id="3bdba-140">Es hora de escribir algún código de identidad.</span><span class="sxs-lookup"><span data-stu-id="3bdba-140">Time to write some identity code.</span></span>  <span data-ttu-id="3bdba-141">Es posible que haya notado que adal.js contiene un proveedor de AngularJS, que se reproduce perfectamente con los mecanismos de enrutamiento de Angular.</span><span class="sxs-lookup"><span data-stu-id="3bdba-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="3bdba-142">Empiece por agregar el módulo adal a la aplicación:</span><span class="sxs-lookup"><span data-stu-id="3bdba-142">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="3bdba-143">Ahora puede inicializar la instancia de `adalProvider` con su id. de aplicación:</span><span class="sxs-lookup"><span data-stu-id="3bdba-143">You can now initialize the `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for the public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // The 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from the registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - the default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="3bdba-144">Muy bien, ahora adal.js tiene toda la información que necesita para proteger su aplicación e iniciar la sesión de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="3bdba-144">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="3bdba-145">Para forzar el inicio de sesión en una determinada ruta de la aplicación, basta con una línea de código:</span><span class="sxs-lookup"><span data-stu-id="3bdba-145">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that the user must be logged in to access the route
})

...
```

<span data-ttu-id="3bdba-146">Ahora, cuando un usuario hace clic en el vínculo `TodoList` , adal.js le redireccionará automáticamente a Azure AD para iniciar sesión si es necesario.</span><span class="sxs-lookup"><span data-stu-id="3bdba-146">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="3bdba-147">También puede enviar explícitamente solicitudes de inicio y cierre de sesión mediante la invocación de adal.js en sus controladores:</span><span class="sxs-lookup"><span data-stu-id="3bdba-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js the same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect the user to sign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect the user to log out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="3bdba-148">Visualización de la información de usuario</span><span class="sxs-lookup"><span data-stu-id="3bdba-148">Display user info</span></span>
<span data-ttu-id="3bdba-149">Ahora que el usuario ha iniciado sesión, probablemente necesitará tener acceso a los datos de autenticación de dicho usuario en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3bdba-149">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="3bdba-150">Adal.js expone esta información en el objeto `userInfo` .</span><span class="sxs-lookup"><span data-stu-id="3bdba-150">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="3bdba-151">Para tener acceso a este objeto en una vista, primero agregue adal.js al ámbito raíz del controlador correspondiente:</span><span class="sxs-lookup"><span data-stu-id="3bdba-151">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="3bdba-152">A continuación, puede dirigir directamente el objeto `userInfo` en la vista:</span><span class="sxs-lookup"><span data-stu-id="3bdba-152">Then you can directly address the `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get the user's profile information from the ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="3bdba-153">También puede usar el objeto `userInfo` para determinar si el usuario ha iniciado sesión o no.</span><span class="sxs-lookup"><span data-stu-id="3bdba-153">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use the ADAL userInfo object to show the right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-the-rest-api"></a><span data-ttu-id="3bdba-154">Llamada a la API de REST</span><span class="sxs-lookup"><span data-stu-id="3bdba-154">Call the REST API</span></span>
<span data-ttu-id="3bdba-155">Por último, es momento de obtener algunos tokens y llamar a la API de REST para crear, leer, actualizar y eliminar tareas.</span><span class="sxs-lookup"><span data-stu-id="3bdba-155">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="3bdba-156">Bien, ¿sabe qué?</span><span class="sxs-lookup"><span data-stu-id="3bdba-156">Well guess what?</span></span>  <span data-ttu-id="3bdba-157">No tiene que hacer *nada*.</span><span class="sxs-lookup"><span data-stu-id="3bdba-157">You don't have to do *a thing*.</span></span>  <span data-ttu-id="3bdba-158">Adal.js se encarga automáticamente de obtener, almacenar en caché y actualizar los tokens.</span><span class="sxs-lookup"><span data-stu-id="3bdba-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="3bdba-159">También se encarga de adjuntar esos tokens a las solicitudes AJAX salientes que se envían a la API de REST.</span><span class="sxs-lookup"><span data-stu-id="3bdba-159">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="3bdba-160">¿Cómo funciona esto exactamente?</span><span class="sxs-lookup"><span data-stu-id="3bdba-160">How exactly does this work?</span></span> <span data-ttu-id="3bdba-161">Es todo gracias a la magia de los [interceptores de AngularJS](https://docs.angularjs.org/api/ng/service/$http), que permiten a adal.js transformar los mensajes http entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="3bdba-161">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="3bdba-162">Además, adal.js presupone que cualquier solicitud enviada al mismo dominio que la ventana debe usar los tokens previstos para el mismo id. de aplicación que la aplicación AngularJS.</span><span class="sxs-lookup"><span data-stu-id="3bdba-162">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="3bdba-163">Por eso hemos usado el mismo id. de aplicación tanto en la aplicación Angular como en la API de REST de NodeJS.</span><span class="sxs-lookup"><span data-stu-id="3bdba-163">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="3bdba-164">Por supuesto, puede invalidar este comportamiento y decir a adal.js que obtenga tokens para otras API de REST si es necesario, pero en este sencillo escenario estos son los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="3bdba-164">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="3bdba-165">Este es un fragmento de código que muestra lo fácil que es enviar solicitudes con tokens de portador de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="3bdba-165">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="3bdba-166">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="3bdba-166">Congratulations!</span></span>  <span data-ttu-id="3bdba-167">La aplicación de una sola página integrada de Azure AD está terminada ahora.</span><span class="sxs-lookup"><span data-stu-id="3bdba-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="3bdba-168">!Ya puede salir a recibir el aplauso del público!</span><span class="sxs-lookup"><span data-stu-id="3bdba-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="3bdba-169">Con ella puede autenticar usuarios, llamar de forma segura a su API de REST de back-end mediante OpenID Connect y obtener información básica sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="3bdba-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="3bdba-170">De forma predeterminada, es compatible con cualquier usuario con una cuenta de Microsoft personal, profesional o educativa desde Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bdba-170">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="3bdba-171">Pruebe la aplicación ejecutando:</span><span class="sxs-lookup"><span data-stu-id="3bdba-171">Give the app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="3bdba-172">Abra un explorador y vaya a `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="3bdba-172">In a browser navigate to `http://localhost:8080`.</span></span>  <span data-ttu-id="3bdba-173">Inicie sesión con una cuenta de Microsoft personal, profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="3bdba-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="3bdba-174">Agregue tareas a la lista de tareas del usuario y cierre la sesión.</span><span class="sxs-lookup"><span data-stu-id="3bdba-174">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="3bdba-175">Intente iniciar sesión con el otro tipo de cuenta.</span><span class="sxs-lookup"><span data-stu-id="3bdba-175">Try signing in with the other type of account.</span></span> <span data-ttu-id="3bdba-176">Si necesita un inquilino de Azure AD para crear usuarios de cuentas profesionales o educativas, [obtenga información sobre cómo conseguir uno aquí](active-directory-howto-tenant.md) (es gratuito).</span><span class="sxs-lookup"><span data-stu-id="3bdba-176">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="3bdba-177">Para obtener más información sobre el punto de conexión v2.0, regrese a nuestra [guía para desarrolladores de v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3bdba-177">To continue learning about the the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="3bdba-178">Para obtener recursos adicionales, consulte:</span><span class="sxs-lookup"><span data-stu-id="3bdba-178">For additional resources, check out:</span></span>

* [<span data-ttu-id="3bdba-179">Ejemplos de Azure en GitHub >></span><span class="sxs-lookup"><span data-stu-id="3bdba-179">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="3bdba-180">Azure AD en Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="3bdba-180">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="3bdba-181">Documentación de Azure AD en [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="3bdba-181">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="3bdba-182">Obtención de actualizaciones de seguridad para nuestros productos</span><span class="sxs-lookup"><span data-stu-id="3bdba-182">Get security updates for our products</span></span>
<span data-ttu-id="3bdba-183">Le animamos a que obtenga notificaciones de los incidentes de seguridad que se produzcan; para ello, visite [esta página](https://technet.microsoft.com/security/dd252948) y suscríbase a las alertas de avisos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3bdba-183">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

