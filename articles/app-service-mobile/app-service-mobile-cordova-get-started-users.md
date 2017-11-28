---
title: "autenticación de aaaAdd en Apache Cordova con aplicaciones móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse aplicaciones móviles en el servicio de aplicación de Azure tooauthenticate a los usuarios de aplicaciones de Apache Cordova a través de una serie de proveedores de identidades, como Google, Facebook, Twitter y Microsoft."
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
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a><span data-ttu-id="881a2-103">Agregar aplicación de Apache Cordova de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="881a2-103">Add authentication tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="881a2-104">Resumen</span><span class="sxs-lookup"><span data-stu-id="881a2-104">Summary</span></span>
<span data-ttu-id="881a2-105">En este tutorial, agregará un proyecto de inicio rápido de autenticación toohello todolist en Apache Cordova mediante un proveedor de identidades admitidos.</span><span class="sxs-lookup"><span data-stu-id="881a2-105">In this tutorial, you add authentication toohello todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="881a2-106">Este tutorial se basa en hello [empezar a trabajar con aplicaciones móviles] tutorial, que debe completar primero.</span><span class="sxs-lookup"><span data-stu-id="881a2-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="881a2-107"><a name="register"></a>Registrar la aplicación para la autenticación y configurar Hola servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="881a2-107"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="881a2-108">Visualización de un vídeo donde se muestren pasos similares</span><span class="sxs-lookup"><span data-stu-id="881a2-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="881a2-109"><a name="permissions"></a>Restringir a los usuarios de tooauthenticated de permisos</span><span class="sxs-lookup"><span data-stu-id="881a2-109"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="881a2-110">Ahora, puede comprobar que tooyour el acceso anónimo, back-end se ha deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="881a2-110">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="881a2-111">En Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="881a2-111">In Visual Studio:</span></span>

* <span data-ttu-id="881a2-112">Proyecto abierto Hola que creó al completar el tutorial de hello [empezar a trabajar con aplicaciones móviles].</span><span class="sxs-lookup"><span data-stu-id="881a2-112">Open hello project that you created when you completed hello tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="881a2-113">Ejecutar la aplicación en hello **emulador de Google Android**.</span><span class="sxs-lookup"><span data-stu-id="881a2-113">Run your application in hello **Google Android Emulator**.</span></span>
* <span data-ttu-id="881a2-114">Compruebe que se muestra un error inesperado de la conexión una vez iniciada la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="881a2-114">Verify that an Unexpected Connection Failure is shown after hello app starts.</span></span>

<span data-ttu-id="881a2-115">A continuación, actualizar los usuarios tooauthenticate de aplicación Hola antes de solicitar recursos de aplicación móvil de hello back-end.</span><span class="sxs-lookup"><span data-stu-id="881a2-115">Next, update hello app tooauthenticate users before requesting resources from hello Mobile App backend.</span></span>

## <span data-ttu-id="881a2-116"><a name="add-authentication"></a>Agregar aplicación de autenticación toohello</span><span class="sxs-lookup"><span data-stu-id="881a2-116"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="881a2-117">Abra el proyecto en **Visual Studio**, a continuación, abra hello `www/index.html` archivo para su edición.</span><span class="sxs-lookup"><span data-stu-id="881a2-117">Open your project in **Visual Studio**, then open hello `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="881a2-118">Busque hello `Content-Security-Policy` meta etiqueta en la sección principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="881a2-118">Locate hello `Content-Security-Policy` meta tag in hello head section.</span></span>  <span data-ttu-id="881a2-119">Agregue hello OAuth host toohello lista de orígenes permitidos.</span><span class="sxs-lookup"><span data-stu-id="881a2-119">Add hello OAuth host toohello list of allowed sources.</span></span>

   | <span data-ttu-id="881a2-120">Proveedor</span><span class="sxs-lookup"><span data-stu-id="881a2-120">Provider</span></span> | <span data-ttu-id="881a2-121">Nombre del proveedor del SDK</span><span class="sxs-lookup"><span data-stu-id="881a2-121">SDK Provider Name</span></span> | <span data-ttu-id="881a2-122">Host de OAuth</span><span class="sxs-lookup"><span data-stu-id="881a2-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="881a2-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="881a2-123">Azure Active Directory</span></span> | <span data-ttu-id="881a2-124">aad</span><span class="sxs-lookup"><span data-stu-id="881a2-124">aad</span></span> | <span data-ttu-id="881a2-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="881a2-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="881a2-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="881a2-126">Facebook</span></span> | <span data-ttu-id="881a2-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="881a2-127">facebook</span></span> | <span data-ttu-id="881a2-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="881a2-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="881a2-129">Google</span><span class="sxs-lookup"><span data-stu-id="881a2-129">Google</span></span> | <span data-ttu-id="881a2-130">Google</span><span class="sxs-lookup"><span data-stu-id="881a2-130">google</span></span> | <span data-ttu-id="881a2-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="881a2-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="881a2-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="881a2-132">Microsoft</span></span> | <span data-ttu-id="881a2-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="881a2-133">microsoftaccount</span></span> | <span data-ttu-id="881a2-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="881a2-134">https://login.live.com</span></span> |
   | <span data-ttu-id="881a2-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="881a2-135">Twitter</span></span> | <span data-ttu-id="881a2-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="881a2-136">twitter</span></span> | <span data-ttu-id="881a2-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="881a2-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="881a2-138">A continuación se muestra un ejemplo de Content-Security-Policy (implementado para Azure Active Directory):</span><span class="sxs-lookup"><span data-stu-id="881a2-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="881a2-139">Reemplace `https://login.microsoftonline.com` a host OAuth Hola Hola tabla anterior.</span><span class="sxs-lookup"><span data-stu-id="881a2-139">Replace `https://login.microsoftonline.com` with hello OAuth host from hello preceding table.</span></span>  <span data-ttu-id="881a2-140">Para obtener más información acerca de la etiqueta meta de directiva de seguridad de contenido de hello, vea hello [documentación de directiva de seguridad de contenido].</span><span class="sxs-lookup"><span data-stu-id="881a2-140">For more information about hello content-security-policy meta tag, see hello [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="881a2-141">Algunos proveedores de autenticación no requieren cambios en Content-Security-Policy cuando se usa en dispositivos móviles adecuados.</span><span class="sxs-lookup"><span data-stu-id="881a2-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="881a2-142">Por ejemplo, no se requiere ningún cambio en Content-Security-Policy cuando se usa la autenticación de Google en un dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="881a2-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="881a2-143">Abra hello `www/js/index.js` para su edición de archivos, busque hello `onDeviceReady()` método, y en la creación de cliente de hello código agregar Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="881a2-143">Open hello `www/js/index.js` file for editing, locate hello `onDeviceReady()` method, and under hello client  creation code add hello following code:</span></span>

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="881a2-144">Este código reemplaza el código de existente de Hola que crea la referencia de tabla de Hola y actualiza la interfaz de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="881a2-144">This code replaces hello existing code that creates hello table reference and refreshes hello UI.</span></span>

    <span data-ttu-id="881a2-145">método login() de Hello inicia la autenticación con el proveedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="881a2-145">hello login() method starts authentication with hello provider.</span></span> <span data-ttu-id="881a2-146">método de Hello login() es una función de async que devuelve una promesa de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="881a2-146">hello login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="881a2-147">resto de Hola de inicialización de Hola se coloca dentro de respuesta de compromiso de Hola para que no se ejecuta hasta que se complete el método de hello login().</span><span class="sxs-lookup"><span data-stu-id="881a2-147">hello rest of hello initialization is placed inside hello promise response so that it is not executed until hello login() method completes.</span></span>

4. <span data-ttu-id="881a2-148">En el código de hello que acaba de agregar, reemplazar `SDK_Provider_Name` con el nombre de Hola de su proveedor de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="881a2-148">In hello code that you just added, replace `SDK_Provider_Name` with hello name of your login provider.</span></span> <span data-ttu-id="881a2-149">Por ejemplo, para Azure Active Directory, use `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="881a2-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="881a2-150">Ejecute el proyecto.</span><span class="sxs-lookup"><span data-stu-id="881a2-150">Run your project.</span></span>  <span data-ttu-id="881a2-151">Al proyecto de hello ha terminado de inicializar, la aplicación muestra la página de inicio de sesión de OAuth de Hola para hello elegido el proveedor de autenticación.</span><span class="sxs-lookup"><span data-stu-id="881a2-151">When hello project has finished initializing, your application shows hello OAuth login page for hello chosen authentication provider.</span></span>

## <span data-ttu-id="881a2-152"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="881a2-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="881a2-153">Obtenga más información [sobre la autenticación] con el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="881a2-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="881a2-154">Continuar con tutorial Hola agregando [notificaciones Push] tooyour aplicaciones de Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="881a2-154">Continue hello tutorial by adding [Push Notifications] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="881a2-155">Obtenga información acerca de cómo toouse Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="881a2-155">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="881a2-156">[SDK de Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="881a2-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="881a2-157">[SDK de servidor ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="881a2-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="881a2-158">[SDK de servidor Node.js]</span><span class="sxs-lookup"><span data-stu-id="881a2-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
[Introducción a Aplicaciones móviles]: app-service-mobile-cordova-get-started.md
[documentación de Content-Security-Policy]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[notificaciones push]: app-service-mobile-cordova-get-started-push.md
[sobre la autenticación]: app-service-mobile-auth.md
[SDK de Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[SDK de servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[SDK de servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
