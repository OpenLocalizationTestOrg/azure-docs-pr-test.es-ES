---
title: "Introducción a Azure AD AngularJS | Microsoft Docs"
description: "Creación de una aplicación de una sola página AngularJS que se integra con Azure AD para el inicio de sesión y llama a las API protegidas de Azure AD mediante OAuth."
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
ms.openlocfilehash: 4153910bc03f112f84c26cda6f9c78f11028b934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="e2619-103">Ayuda para proteger aplicaciones de una sola página AngularJS mediante Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2619-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="e2619-104">Con Azure Active Directory (Azure AD), es sencillo y directo agregar llamadas de inicio y cierre de sesión, así como llamadas seguras de API de OAuth a las aplicaciones de una sola página.</span><span class="sxs-lookup"><span data-stu-id="e2619-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span></span>  <span data-ttu-id="e2619-105">Permite que la aplicación autentique a los usuarios con sus cuentas de Active Directory de Windows Server, además de consumir cualquier web API que Azure AD ayuda a proteger, como las API de Office 365 o la API de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2619-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="e2619-106">Para las aplicaciones de JavaScript que se ejecutan en un explorador, Azure AD proporciona la biblioteca de autenticación de Active Directory (ADAL), o adal.js.</span><span class="sxs-lookup"><span data-stu-id="e2619-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="e2619-107">La única finalidad de adal.js es facilitar a su aplicación la obtención de tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="e2619-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="e2619-108">Para demostrar lo fácil que es, crearemos aquí una aplicación de lista de tareas pendientes (ToDo) de AngularJS que permita realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="e2619-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span></span>

* <span data-ttu-id="e2619-109">Iniciar sesión del usuario en la aplicación con Azure AD como proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="e2619-109">Signs the user in to the app by using Azure AD as the identity provider.</span></span>

* <span data-ttu-id="e2619-110">Mostrar información sobre el usuario</span><span class="sxs-lookup"><span data-stu-id="e2619-110">Displays some information about the user.</span></span>
* <span data-ttu-id="e2619-111">Realizar una llamada con seguridad a la API de la lista de tareas pendientes de la aplicación mediante tokens de portador de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2619-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="e2619-112">Cerrar la sesión del usuario en la aplicación</span><span class="sxs-lookup"><span data-stu-id="e2619-112">Signs the user out of the app.</span></span>

<span data-ttu-id="e2619-113">Para crear la aplicación de trabajo completa, debe realizar estas acciones:</span><span class="sxs-lookup"><span data-stu-id="e2619-113">To build the complete, working application, you need to:</span></span>

1. <span data-ttu-id="e2619-114">Registrar la aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2619-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="e2619-115">Instalar ADAL y configurar la aplicación de una sola página.</span><span class="sxs-lookup"><span data-stu-id="e2619-115">Install ADAL and configure the single-page app.</span></span>
3. <span data-ttu-id="e2619-116">Usar ADAL para ayudar a proteger las páginas en la aplicación de una sola página.</span><span class="sxs-lookup"><span data-stu-id="e2619-116">Use ADAL to help secure pages in the single-page app.</span></span>

<span data-ttu-id="e2619-117">Para empezar, [descargue el esquema de la aplicación](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) o [descargue el ejemplo finalizado](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e2619-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="e2619-118">También necesita a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2619-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="e2619-119">Si aún no tiene un inquilino, [descubra cómo conseguir uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e2619-119">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-the-directorysearcher-application"></a><span data-ttu-id="e2619-120">Paso 1: Registro de la aplicación DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="e2619-120">Step 1: Register the DirectorySearcher application</span></span>
<span data-ttu-id="e2619-121">Para habilitar la aplicación a fin de autenticar a los usuarios y obtener tokens, primero debe registrarla en el inquilino de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e2619-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="e2619-122">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e2619-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e2619-123">Si inició sesión en varios directorios, debe asegurarse de que está viendo el directorio correcto.</span><span class="sxs-lookup"><span data-stu-id="e2619-123">If you are signed in to multiple directories, you may need to ensure you are viewing the correct directory.</span></span> <span data-ttu-id="e2619-124">Para ello, en la barra superior, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="e2619-124">To do so, on the top bar, click your account.</span></span> <span data-ttu-id="e2619-125">En la lista **Directorio** lista, elija el inquilino de Azure AD donde desea registrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2619-125">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="e2619-126">Haga clic en **Más servicios** en el panel izquierdo y luego seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e2619-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e2619-127">Haga clic en **Registros de aplicaciones** y luego seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e2619-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="e2619-128">Siga las indicaciones y cree una nueva aplicación web y/o API web:</span><span class="sxs-lookup"><span data-stu-id="e2619-128">Follow the prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="e2619-129">**Nombre** describe la aplicación a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e2619-129">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="e2619-130">**URI de redirección** es la ubicación a la que Azure AD devolverá los tokens.</span><span class="sxs-lookup"><span data-stu-id="e2619-130">**Redirect Uri** is the location to which Azure AD will return tokens.</span></span> <span data-ttu-id="e2619-131">La ubicación predeterminada para este ejemplo es `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="e2619-131">The default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="e2619-132">Cuando termine el registro, Azure AD asignará un identificador de aplicación único a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2619-132">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span>  <span data-ttu-id="e2619-133">Necesitará este valor en las secciones siguientes, así que cópielo de la pestaña de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2619-133">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="e2619-134">Adal.js utiliza el flujo implícito de OAuth para comunicarse con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2619-134">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span></span> <span data-ttu-id="e2619-135">Debe habilitar el flujo implícito para la aplicación mediante estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e2619-135">You must enable the implicit flow for your application:</span></span>
  1. <span data-ttu-id="e2619-136">Haga clic en la aplicación y seleccione **Manifiesto** para abrir el editor de manifiestos en línea.</span><span class="sxs-lookup"><span data-stu-id="e2619-136">Click the application and select **Manifest** to open the inline manifest editor.</span></span>
  2. <span data-ttu-id="e2619-137">Busque la propiedad `oauth2AllowImplicitFlow`.</span><span class="sxs-lookup"><span data-stu-id="e2619-137">Locate the `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="e2619-138">Establezca su valor en `true`.</span><span class="sxs-lookup"><span data-stu-id="e2619-138">Set its value to `true`.</span></span>
  3. <span data-ttu-id="e2619-139">Haga clic en **Guardar** para guardar el manifiesto.</span><span class="sxs-lookup"><span data-stu-id="e2619-139">Click **Save** to save the manifest.</span></span>
8. <span data-ttu-id="e2619-140">Conceda permisos para la aplicación en todo el inquilino.</span><span class="sxs-lookup"><span data-stu-id="e2619-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="e2619-141">Vaya a **Configuración** > **Propiedades** > **Permisos necesarios** y haga clic en el botón **Conceder permisos** de la barra superior.</span><span class="sxs-lookup"><span data-stu-id="e2619-141">Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span></span> <span data-ttu-id="e2619-142">Haga clic en **Sí** para continuar.</span><span class="sxs-lookup"><span data-stu-id="e2619-142">Click **Yes** to confirm.</span></span>

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a><span data-ttu-id="e2619-143">Paso 2: Instalación de ADAL y configuración de aplicación de una sola página</span><span class="sxs-lookup"><span data-stu-id="e2619-143">Step 2: Install ADAL and configure the single-page app</span></span>
<span data-ttu-id="e2619-144">Ahora que tiene una aplicación en Azure AD, puede instalar adal.js y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="e2619-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-the-javascript-client"></a><span data-ttu-id="e2619-145">Configuración del cliente de JavaScript</span><span class="sxs-lookup"><span data-stu-id="e2619-145">Configure the JavaScript client</span></span>
<span data-ttu-id="e2619-146">Comience agregando adal.js al proyecto TodoSPA mediante la Consola del Administrador de paquetes:</span><span class="sxs-lookup"><span data-stu-id="e2619-146">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span></span>
  1. <span data-ttu-id="e2619-147">Descargue [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) y agréguelo al directorio del proyecto `App/Scripts/`.</span><span class="sxs-lookup"><span data-stu-id="e2619-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="e2619-148">Descargue [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) y agréguelo al directorio del proyecto `App/Scripts/`.</span><span class="sxs-lookup"><span data-stu-id="e2619-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="e2619-149">Cargue cada script antes del fin de `</body>` in `index.html`:</span><span class="sxs-lookup"><span data-stu-id="e2619-149">Load each script before the end of the `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-the-back-end-server"></a><span data-ttu-id="e2619-150">Configuración del servidor back-end</span><span class="sxs-lookup"><span data-stu-id="e2619-150">Configure the back end server</span></span>
<span data-ttu-id="e2619-151">Para que la API de tareas pendientes del back-end de la aplicación de una sola página acepte tokens del explorador, el back-end necesita información de configuración acerca del registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2619-151">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span></span> <span data-ttu-id="e2619-152">En el proyecto TodoSPA, abra `web.config`.</span><span class="sxs-lookup"><span data-stu-id="e2619-152">In the TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="e2619-153">Reemplace los valores de los elementos de la sección `<appSettings>` para que reflejen los valores usados en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e2619-153">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="e2619-154">El código hará referencia a estos valores siempre que use ADAL.</span><span class="sxs-lookup"><span data-stu-id="e2619-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="e2619-155">`ida:Tenant` es el dominio del inquilino de Azure AD, por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="e2619-155">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="e2619-156">`ida:Audience` es el identificador de cliente de la aplicación que copió del portal.</span><span class="sxs-lookup"><span data-stu-id="e2619-156">`ida:Audience` is the client ID of your application that you copied from the portal.</span></span>

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a><span data-ttu-id="e2619-157">Paso 3: Uso de ADAL para ayudar a proteger las páginas en la aplicación de una sola página</span><span class="sxs-lookup"><span data-stu-id="e2619-157">Step 3: Use ADAL to help secure pages in the single-page app</span></span>
<span data-ttu-id="e2619-158">Adal.js se integra con la ruta de AngularJS y los proveedores HTTP, por lo que puede ayudar a proteger vistas individuales en la aplicación de una sola página.</span><span class="sxs-lookup"><span data-stu-id="e2619-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="e2619-159">En `App/Scripts/app.js`, importe el módulo adal.js:</span><span class="sxs-lookup"><span data-stu-id="e2619-159">In `App/Scripts/app.js`, bring in the adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="e2619-160">Inicialice `adalProvider` con los valores de configuración del registro de su aplicación, también en `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="e2619-160">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="e2619-161">Ayude a proteger la vista `TodoList` en la aplicación utilizando solamente una línea de código: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="e2619-161">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="e2619-162">Resumen</span><span class="sxs-lookup"><span data-stu-id="e2619-162">Summary</span></span>
<span data-ttu-id="e2619-163">Ahora tiene una aplicación de una sola página segura con capacidad para iniciar la sesión de los usuarios y emitir solicitudes protegidas de token de portador a su API de back-end.</span><span class="sxs-lookup"><span data-stu-id="e2619-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span></span> <span data-ttu-id="e2619-164">Cuando un usuario hace clic en el vínculo **TodoList**, adal.js le redireccionará automáticamente a Azure AD para iniciar sesión si es necesario.</span><span class="sxs-lookup"><span data-stu-id="e2619-164">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span> <span data-ttu-id="e2619-165">Además, adal.js adjuntará automáticamente un token de acceso a cualquier solicitud de Ajax que se envíe al servidor back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2619-165">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span></span>  

<span data-ttu-id="e2619-166">Los pasos anteriores son los mínimos necesarios para compilar una aplicación de una sola página mediante adal.js.</span><span class="sxs-lookup"><span data-stu-id="e2619-166">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span></span> <span data-ttu-id="e2619-167">Pero algunas otras características son útiles en una aplicación de una sola página:</span><span class="sxs-lookup"><span data-stu-id="e2619-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="e2619-168">Para emitir explícitamente solicitudes de inicio y cierre de sesión, puede definir funciones en sus controladores que invocan adal.js.</span><span class="sxs-lookup"><span data-stu-id="e2619-168">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="e2619-169">En `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="e2619-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="e2619-170">Puede que desee presentar información de usuario en la interfaz de usuario de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2619-170">You might want to present user information in the app's UI.</span></span> <span data-ttu-id="e2619-171">El servicio ADAL ya se ha agregado al controlador `userDataCtrl`, por lo que puede tener acceso al objeto `userInfo` en la vista asociada, `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="e2619-171">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="e2619-172">Hay muchos casos en los que deseará saber si el usuario ha iniciado sesión o no.</span><span class="sxs-lookup"><span data-stu-id="e2619-172">There are many scenarios in which you'll want to know if the user is signed in or not.</span></span> <span data-ttu-id="e2619-173">También puede utilizar el objeto `userInfo` para recopilar esta información.</span><span class="sxs-lookup"><span data-stu-id="e2619-173">You can also use the `userInfo` object to gather this information.</span></span>  <span data-ttu-id="e2619-174">Por ejemplo, en `index.html` puede mostrar el botón **Iniciar sesión** o **Cerrar sesión** en función del estado de autenticación:</span><span class="sxs-lookup"><span data-stu-id="e2619-174">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="e2619-175">La aplicación de una sola página integrada con Azure AD puede autenticar a los usuarios, efectuar llamadas seguras a back-end mediante OAuth 2.0 y obtener información básica sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="e2619-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="e2619-176">Si todavía no lo ha hecho, ahora es el momento de completar el inquilino con algunos usuarios.</span><span class="sxs-lookup"><span data-stu-id="e2619-176">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="e2619-177">Ejecute la aplicación de una sola página de la lista de tareas pendientes e inicie sesión con uno de esos usuarios.</span><span class="sxs-lookup"><span data-stu-id="e2619-177">Run your To Do List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="e2619-178">Agregue tareas a la lista de tareas pendientes de los usuarios, cierre la sesión y vuelva a iniciarla.</span><span class="sxs-lookup"><span data-stu-id="e2619-178">Add tasks to the user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="e2619-179">Adal.js facilita la incorporación de características comunes de identidad en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2619-179">Adal.js makes it easy to incorporate common identity features into your application.</span></span> <span data-ttu-id="e2619-180">Se encarga de todo el trabajo duro: administración de la memoria caché, compatibilidad con el protocolo OAuth, presentación del usuario con una interfaz de usuario de inicio de sesión, actualización de los tokens caducados, etc.</span><span class="sxs-lookup"><span data-stu-id="e2619-180">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="e2619-181">Como referencia, en [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip) está disponible el ejemplo finalizado (sin sus valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="e2619-181">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2619-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2619-182">Next steps</span></span>
<span data-ttu-id="e2619-183">Ahora puede pasar a otros escenarios.</span><span class="sxs-lookup"><span data-stu-id="e2619-183">You can now move on to additional scenarios.</span></span> <span data-ttu-id="e2619-184">Puede intentar [llamar a una API web CORS desde una aplicación de una sola página](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="e2619-184">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
