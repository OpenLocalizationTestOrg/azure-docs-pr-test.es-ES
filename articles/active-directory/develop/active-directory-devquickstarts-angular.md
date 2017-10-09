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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="dada4-103">Ayuda para proteger aplicaciones de una sola página AngularJS mediante Azure AD</span><span class="sxs-lookup"><span data-stu-id="dada4-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="dada4-104">Azure Active Directory (Azure AD) permite simple y sencillo para tooadd inicio de sesión, cierre de sesión, y llamadas de API de OAuth segura tooyour aplicaciones de la página.</span><span class="sxs-lookup"><span data-stu-id="dada4-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="dada4-105">Permite a los usuarios de aplicaciones tooauthenticate con sus cuentas de Windows Server Active Directory y consumir cualquier API que Azure AD le ayuda a proteger, como Hola API de Office 365 o hello Azure API web.</span><span class="sxs-lookup"><span data-stu-id="dada4-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="dada4-106">Para las aplicaciones de JavaScript que se ejecuta en un explorador, Azure AD proporciona Hola biblioteca de autenticación de Active Directory (ADAL) o adal.js.</span><span class="sxs-lookup"><span data-stu-id="dada4-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="dada4-107">Hola único propósito de adal.js es toomake más sencilla para los tokens de acceso de tooget de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="dada4-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="dada4-108">toodemonstrate lo fácil es, a continuación, crearemos una aplicación de la lista de AngularJS tooDo que:</span><span class="sxs-lookup"><span data-stu-id="dada4-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="dada4-109">Usuario de hello signos en toohello aplicación mediante Azure AD como proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="dada4-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="dada4-110">Muestra información acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="dada4-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="dada4-111">Forma segura llamadas Hola tooDo de la aplicación API de la lista mediante el uso de tokens de portador de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dada4-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="dada4-112">Signos de Hola usuario fuera de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dada4-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="dada4-113">aplicación toobuild Hola completa, trabajo, debe:</span><span class="sxs-lookup"><span data-stu-id="dada4-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="dada4-114">Registrar la aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dada4-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="dada4-115">Instalar AAL y configurar la aplicación de la página de hello.</span><span class="sxs-lookup"><span data-stu-id="dada4-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="dada4-116">Usar páginas seguras toohelp AAL en aplicación de la página de hello.</span><span class="sxs-lookup"><span data-stu-id="dada4-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="dada4-117">tooget iniciado, [descargar esqueleto de aplicación Hola](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) o [Descargar ejemplo Hola completado](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="dada4-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="dada4-118">También necesita a un inquilino de Azure AD en el que pueda crear usuarios y registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="dada4-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="dada4-119">Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="dada4-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="dada4-120">Paso 1: Registrar aplicación de DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="dada4-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="dada4-121">tooenable aplicación tooauthenticate usuarios y tokens de get, primero debe tooregister en Azure AD de los inquilinos:</span><span class="sxs-lookup"><span data-stu-id="dada4-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="dada4-122">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dada4-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dada4-123">Si ha iniciado sesión toomultiple directorios, debe tooensure que está viendo el directorio correcto de Hola.</span><span class="sxs-lookup"><span data-stu-id="dada4-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="dada4-124">toodo por lo tanto, en la barra superior de hello, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="dada4-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="dada4-125">En hello **Directory** elija inquilino hello Azure AD en el que desea tooregister la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dada4-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="dada4-126">Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dada4-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="dada4-127">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dada4-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="dada4-128">Siga las indicaciones de Hola y cree una nueva aplicación web o API web:</span><span class="sxs-lookup"><span data-stu-id="dada4-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="dada4-129">**Nombre** describe su toousers de aplicación.</span><span class="sxs-lookup"><span data-stu-id="dada4-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="dada4-130">**Uri de redireccionamiento** es toowhich de ubicación de hello Azure AD devolverá tokens.</span><span class="sxs-lookup"><span data-stu-id="dada4-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="dada4-131">ubicación predeterminada de Hola para este ejemplo es `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="dada4-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="dada4-132">Cuando termine de registro, Azure AD le asigna una aplicación de tooyour de Id. de aplicación exclusivo.</span><span class="sxs-lookup"><span data-stu-id="dada4-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="dada4-133">Necesitará este valor en las secciones siguientes de hello, por lo tanto cópiela desde la pestaña de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dada4-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="dada4-134">Adal.js usa hello OAuth flujo implícito toocommunicate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dada4-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="dada4-135">Debe habilitar el flujo implícito de hello para la aplicación:</span><span class="sxs-lookup"><span data-stu-id="dada4-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="dada4-136">Haga clic en la aplicación hello y seleccione **manifiesto** editor de manifiestos de tooopen hello en línea.</span><span class="sxs-lookup"><span data-stu-id="dada4-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="dada4-137">Busque hello `oauth2AllowImplicitFlow` propiedad.</span><span class="sxs-lookup"><span data-stu-id="dada4-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="dada4-138">Establezca su valor demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="dada4-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="dada4-139">Haga clic en **guardar** toosave manifiesto de Hola.</span><span class="sxs-lookup"><span data-stu-id="dada4-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="dada4-140">Conceda permisos para la aplicación en todo el inquilino.</span><span class="sxs-lookup"><span data-stu-id="dada4-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="dada4-141">Vaya demasiado**configuración** > **propiedades** > **permisos necesarios**y haga clic en hello **conceder permisos**botón de barra superior Hola.</span><span class="sxs-lookup"><span data-stu-id="dada4-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="dada4-142">Haga clic en **Sí** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="dada4-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="dada4-143">Paso 2: Instalar AAL y configurar la aplicación de la página de hello</span><span class="sxs-lookup"><span data-stu-id="dada4-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="dada4-144">Ahora que tiene una aplicación en Azure AD, puede instalar adal.js y escribir el código relacionado con la identidad.</span><span class="sxs-lookup"><span data-stu-id="dada4-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="dada4-145">Configurar el cliente de JavaScript de Hola</span><span class="sxs-lookup"><span data-stu-id="dada4-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="dada4-146">Comienza agregando adal.js toohello TodoSPA proyecto mediante el uso de la consola de administrador de paquetes de saludo:</span><span class="sxs-lookup"><span data-stu-id="dada4-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="dada4-147">Descargar [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) y agregue toohello `App/Scripts/` directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="dada4-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="dada4-148">Descargar [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) y agregue toohello `App/Scripts/` directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="dada4-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="dada4-149">Cargar cada script antes del fin de Hola Hola `</body>` en `index.html`:</span><span class="sxs-lookup"><span data-stu-id="dada4-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="dada4-150">Configurar servidor de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="dada4-150">Configure hello back end server</span></span>
<span data-ttu-id="dada4-151">Para los tokens de la aplicación hello página tooDo back-end lista API tooaccept desde el Explorador de hello, back-end de hello necesita información de configuración de registro de una aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="dada4-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="dada4-152">En hello TodoSPA proyecto, abra `web.config`.</span><span class="sxs-lookup"><span data-stu-id="dada4-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="dada4-153">Reemplace los valores de hello de elementos de Hola Hola `<appSettings>` Hola de valores de hello tooreflect una sección que usó en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dada4-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="dada4-154">El código hará referencia a estos valores siempre que use ADAL.</span><span class="sxs-lookup"><span data-stu-id="dada4-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="dada4-155">`ida:Tenant`es el dominio de hello del inquilino de Azure AD: por ejemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="dada4-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="dada4-156">`ida:Audience`es el Id. de cliente de saludo de la aplicación que ha copiado desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="dada4-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="dada4-157">Paso 3: Utilizan toohelp AAL seguras páginas de aplicación de la página de hello</span><span class="sxs-lookup"><span data-stu-id="dada4-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="dada4-158">Adal.js se integra con la ruta de AngularJS y los proveedores HTTP, por lo que puede ayudar a proteger vistas individuales en la aplicación de una sola página.</span><span class="sxs-lookup"><span data-stu-id="dada4-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="dada4-159">En `App/Scripts/app.js`, poner en el módulo de Hola adal.js:</span><span class="sxs-lookup"><span data-stu-id="dada4-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="dada4-160">Inicializar `adalProvider` mediante los valores de configuración de Hola de su registro de la aplicación, también en `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="dada4-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="dada4-161">Ayudar a Hola segura `TodoList` vista en la aplicación hello mediante el uso de una única línea de código: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="dada4-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="dada4-162">Resumen</span><span class="sxs-lookup"><span data-stu-id="dada4-162">Summary</span></span>
<span data-ttu-id="dada4-163">Ahora tiene una aplicación de página segura que se puede iniciar sesión en los usuarios y emitir solicitudes de token de portador protegido tooits back-end API.</span><span class="sxs-lookup"><span data-stu-id="dada4-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="dada4-164">Cuando un usuario hace clic en hello **TodoList** vínculo, adal.js le redirigirá automáticamente tooAzure AD para inicio de sesión si es necesario.</span><span class="sxs-lookup"><span data-stu-id="dada4-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="dada4-165">Además, adal.js se asociará automáticamente un acceso token tooany Ajax solicita que se envían back-end de la aplicación toohello.</span><span class="sxs-lookup"><span data-stu-id="dada4-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="dada4-166">Hello pasos anteriores están toobuild necesaria mínima una aplicación de la página de reconstrucción de hello mediante adal.js.</span><span class="sxs-lookup"><span data-stu-id="dada4-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="dada4-167">Pero algunas otras características son útiles en una aplicación de una sola página:</span><span class="sxs-lookup"><span data-stu-id="dada4-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="dada4-168">tooexplicitly emitir solicitudes de inicio de sesión y cierre de sesión, puede definir las funciones en los controladores que invocan adal.js.</span><span class="sxs-lookup"><span data-stu-id="dada4-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="dada4-169">En `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="dada4-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="dada4-170">Conviene toopresent información de usuario en la interfaz de usuario de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="dada4-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="dada4-171">Hola AAL servicio ya se ha agregado toohello `userDataCtrl` controlador, para que pueda acceder hello `userInfo` objeto Hola asociado a la vista, `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="dada4-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="dada4-172">Hay muchos escenarios en los que es conveniente tooknow si el usuario de hello ha iniciado sesión o no.</span><span class="sxs-lookup"><span data-stu-id="dada4-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="dada4-173">También puede usar hello `userInfo` objeto toogather esta información.</span><span class="sxs-lookup"><span data-stu-id="dada4-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="dada4-174">Por ejemplo, en `index.html`, puede mostrar cualquier hello **inicio de sesión** o **Logout** botón de acuerdo con el estado de autenticación:</span><span class="sxs-lookup"><span data-stu-id="dada4-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="dada4-175">La aplicación de página única integrada en AD Azure puede autenticar a los usuarios, con seguridad llame a su back-end mediante OAuth 2.0 y obtener información básica acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="dada4-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="dada4-176">Si no lo ha hecho ya, ahora es Hola tiempo toopopulate el inquilino con algunos usuarios.</span><span class="sxs-lookup"><span data-stu-id="dada4-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="dada4-177">Ejecutar la aplicación de una página de lista de tooDo y, inicie sesión con uno de esos usuarios.</span><span class="sxs-lookup"><span data-stu-id="dada4-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="dada4-178">Agregar la lista de tareas del usuario de las tareas toohello, cierre la sesión y volverla a iniciar.</span><span class="sxs-lookup"><span data-stu-id="dada4-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="dada4-179">Adal.js hace fácil tooincorporate características de identidad comunes en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dada4-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="dada4-180">Se encarga de todo el trabajo dirty Hola para usted: administración de la caché, compatibilidad con el protocolo OAuth, presentar usuario Hola con un inicio de sesión de interfaz de usuario, actualizar tokens caducados y mucho más.</span><span class="sxs-lookup"><span data-stu-id="dada4-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="dada4-181">Como referencia, está disponible en el ejemplo de Hola finalizado (sin los valores de configuración) [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="dada4-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dada4-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dada4-182">Next steps</span></span>
<span data-ttu-id="dada4-183">Ahora puede mover en escenarios de tooadditional.</span><span class="sxs-lookup"><span data-stu-id="dada4-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="dada4-184">Es recomendable tootry: [llamar a una API web CORS desde una aplicación de la página](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="dada4-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
