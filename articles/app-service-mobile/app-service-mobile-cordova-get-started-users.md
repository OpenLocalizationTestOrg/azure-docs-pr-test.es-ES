---
title: "Adición de autenticación en Apache Cordova con Mobile Apps | Microsoft Docs"
description: "Obtenga información sobre cómo usar Aplicaciones móviles en el Servicio de aplicaciones de Azure para autenticar usuarios de su aplicación de Apache Cordova a través de una variedad de proveedores de identidades, incluidos Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: b7362b7f26859de541f792e714502851d74c98e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-apache-cordova-app"></a><span data-ttu-id="426b8-103">Agregar autenticación a su aplicación de Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="426b8-103">Add authentication to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="426b8-104">Resumen</span><span class="sxs-lookup"><span data-stu-id="426b8-104">Summary</span></span>
<span data-ttu-id="426b8-105">En este tutorial podrá agregar la autenticación al proyecto de inicio rápido todolist en Apache Cordova con un proveedor de identidades admitido.</span><span class="sxs-lookup"><span data-stu-id="426b8-105">In this tutorial, you add authentication to the todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="426b8-106">Este tutorial está basado en el tutorial [Introducción a Mobile Apps] , que debe completar primero.</span><span class="sxs-lookup"><span data-stu-id="426b8-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="426b8-107"><a name="register"></a>Registro de la aplicación para la autenticación y configuración del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="426b8-107"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="426b8-108">Visualización de un vídeo donde se muestren pasos similares</span><span class="sxs-lookup"><span data-stu-id="426b8-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="426b8-109"><a name="permissions"></a>Restricción de los permisos para los usuarios autenticados</span><span class="sxs-lookup"><span data-stu-id="426b8-109"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="426b8-110">Ahora, puede comprobar que se deshabilitó el acceso anónimo a su back-end.</span><span class="sxs-lookup"><span data-stu-id="426b8-110">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="426b8-111">En Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="426b8-111">In Visual Studio:</span></span>

* <span data-ttu-id="426b8-112">Abra el proyecto que ha creado al completar el tutorial [Introducción a Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="426b8-112">Open the project that you created when you completed the tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="426b8-113">Ejecute la aplicación en el **emulador de Google Android**.</span><span class="sxs-lookup"><span data-stu-id="426b8-113">Run your application in the **Google Android Emulator**.</span></span>
* <span data-ttu-id="426b8-114">Compruebe que se muestra un error de conexión inesperado después de iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="426b8-114">Verify that an Unexpected Connection Failure is shown after the app starts.</span></span>

<span data-ttu-id="426b8-115">A continuación, actualice la aplicación para autenticar usuarios antes de solicitar recursos del back-end de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="426b8-115">Next, update the app to authenticate users before requesting resources from the Mobile App backend.</span></span>

## <span data-ttu-id="426b8-116"><a name="add-authentication"></a>Incorporación de autenticación a la aplicación</span><span class="sxs-lookup"><span data-stu-id="426b8-116"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="426b8-117">Abra el proyecto en **Visual Studio** y, después, abra el archivo `www/index.html` para editarlo.</span><span class="sxs-lookup"><span data-stu-id="426b8-117">Open your project in **Visual Studio**, then open the `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="426b8-118">Busque la etiqueta META `Content-Security-Policy` en la sección de encabezado.</span><span class="sxs-lookup"><span data-stu-id="426b8-118">Locate the `Content-Security-Policy` meta tag in the head section.</span></span>  <span data-ttu-id="426b8-119">Agregue el host de OAuth a la lista de orígenes permitidos.</span><span class="sxs-lookup"><span data-stu-id="426b8-119">Add the OAuth host to the list of allowed sources.</span></span>

   | <span data-ttu-id="426b8-120">Proveedor</span><span class="sxs-lookup"><span data-stu-id="426b8-120">Provider</span></span> | <span data-ttu-id="426b8-121">Nombre del proveedor del SDK</span><span class="sxs-lookup"><span data-stu-id="426b8-121">SDK Provider Name</span></span> | <span data-ttu-id="426b8-122">Host de OAuth</span><span class="sxs-lookup"><span data-stu-id="426b8-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="426b8-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="426b8-123">Azure Active Directory</span></span> | <span data-ttu-id="426b8-124">aad</span><span class="sxs-lookup"><span data-stu-id="426b8-124">aad</span></span> | <span data-ttu-id="426b8-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="426b8-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="426b8-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="426b8-126">Facebook</span></span> | <span data-ttu-id="426b8-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="426b8-127">facebook</span></span> | <span data-ttu-id="426b8-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="426b8-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="426b8-129">Google</span><span class="sxs-lookup"><span data-stu-id="426b8-129">Google</span></span> | <span data-ttu-id="426b8-130">Google</span><span class="sxs-lookup"><span data-stu-id="426b8-130">google</span></span> | <span data-ttu-id="426b8-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="426b8-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="426b8-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="426b8-132">Microsoft</span></span> | <span data-ttu-id="426b8-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="426b8-133">microsoftaccount</span></span> | <span data-ttu-id="426b8-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="426b8-134">https://login.live.com</span></span> |
   | <span data-ttu-id="426b8-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="426b8-135">Twitter</span></span> | <span data-ttu-id="426b8-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="426b8-136">twitter</span></span> | <span data-ttu-id="426b8-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="426b8-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="426b8-138">A continuación se muestra un ejemplo de Content-Security-Policy (implementado para Azure Active Directory):</span><span class="sxs-lookup"><span data-stu-id="426b8-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="426b8-139">Reemplace `https://login.microsoftonline.com` por el host de OAuth de la tabla anterior.</span><span class="sxs-lookup"><span data-stu-id="426b8-139">Replace `https://login.microsoftonline.com` with the OAuth host from the preceding table.</span></span>  <span data-ttu-id="426b8-140">Para obtener más información sobre la etiqueta de metadatos de lContent-Security-Policy, consulte la [documentación de Content-Security-Policy].</span><span class="sxs-lookup"><span data-stu-id="426b8-140">For more information about the content-security-policy meta tag, see the [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="426b8-141">Algunos proveedores de autenticación no requieren cambios en Content-Security-Policy cuando se usa en dispositivos móviles adecuados.</span><span class="sxs-lookup"><span data-stu-id="426b8-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="426b8-142">Por ejemplo, no se requiere ningún cambio en Content-Security-Policy cuando se usa la autenticación de Google en un dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="426b8-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="426b8-143">Abra el archivo `www/js/index.js` para editarlo, busque el método `onDeviceReady()` y, en el código de creación del cliente, agregue el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="426b8-143">Open the `www/js/index.js` file for editing, locate the `onDeviceReady()` method, and under the client  creation code add the following code:</span></span>

        // Login to the service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="426b8-144">Este código reemplaza el código existente que crea la referencia de tabla y actualiza la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="426b8-144">This code replaces the existing code that creates the table reference and refreshes the UI.</span></span>

    <span data-ttu-id="426b8-145">El método login() inicia la autenticación con el proveedor.</span><span class="sxs-lookup"><span data-stu-id="426b8-145">The login() method starts authentication with the provider.</span></span> <span data-ttu-id="426b8-146">El método login() es una función asincrónica que devuelve una promesa de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="426b8-146">The login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="426b8-147">El resto de la inicialización se coloca dentro de la respuesta de la promesa para que no se ejecute hasta que se complete el método login().</span><span class="sxs-lookup"><span data-stu-id="426b8-147">The rest of the initialization is placed inside the promise response so that it is not executed until the login() method completes.</span></span>

4. <span data-ttu-id="426b8-148">En el código que acaba de agregar, reemplace `SDK_Provider_Name` por el nombre de su proveedor de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="426b8-148">In the code that you just added, replace `SDK_Provider_Name` with the name of your login provider.</span></span> <span data-ttu-id="426b8-149">Por ejemplo, para Azure Active Directory, use `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="426b8-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="426b8-150">Ejecute el proyecto.</span><span class="sxs-lookup"><span data-stu-id="426b8-150">Run your project.</span></span>  <span data-ttu-id="426b8-151">Cuando el proyecto acabe de inicializarse, la aplicación mostrará la página de inicio de sesión de OAuth del proveedor de autenticación seleccionado.</span><span class="sxs-lookup"><span data-stu-id="426b8-151">When the project has finished initializing, your application shows the OAuth login page for the chosen authentication provider.</span></span>

## <span data-ttu-id="426b8-152"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="426b8-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="426b8-153">Obtenga más información [sobre la autenticación] con el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="426b8-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="426b8-154">Prosiga el tutorial agregando [notificaciones push] a la aplicación de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="426b8-154">Continue the tutorial by adding [Push Notifications] to your Apache Cordova app.</span></span>

<span data-ttu-id="426b8-155">Obtenga información sobre cómo usar los SDK.</span><span class="sxs-lookup"><span data-stu-id="426b8-155">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="426b8-156">[SDK de Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="426b8-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="426b8-157">[SDK de servidor ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="426b8-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="426b8-158">[SDK de servidor Node.js]</span><span class="sxs-lookup"><span data-stu-id="426b8-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
<span data-ttu-id="426b8-159">[Introducción a Mobile Apps]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="426b8-159">[Get started with Mobile Apps]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="426b8-160">[documentación de Content-Security-Policy]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span><span class="sxs-lookup"><span data-stu-id="426b8-160">[Content-Security-Policy documentation]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span></span>
<span data-ttu-id="426b8-161">[notificaciones push]: app-service-mobile-cordova-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="426b8-161">[Push Notifications]: app-service-mobile-cordova-get-started-push.md</span></span>
<span data-ttu-id="426b8-162">[sobre la autenticación]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="426b8-162">[About Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="426b8-163">[SDK de Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="426b8-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="426b8-164">[SDK de servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="426b8-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="426b8-165">[SDK de servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="426b8-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>
