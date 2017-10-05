---
title: "Adición de autenticación en Android con Mobile Apps | Microsoft Docs"
description: "Obtenga información sobre cómo usar la característica Mobile Apps de Azure App Service para autenticar usuarios de su aplicación Android a través de una variedad de proveedores de identidad, incluidos Google, Facebook, Twitter y Microsoft."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 81331142aa6110d4e29e6fb30a90ce6e3a853439
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-android-app"></a><span data-ttu-id="c654c-103">Agregar autenticación a su aplicación de Android</span><span class="sxs-lookup"><span data-stu-id="c654c-103">Add authentication to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="c654c-104">Resumen</span><span class="sxs-lookup"><span data-stu-id="c654c-104">Summary</span></span>
<span data-ttu-id="c654c-105">En este tutorial podrá agregar la autenticación al proyecto de inicio rápido todolist en Android con un proveedor de identidades admitido.</span><span class="sxs-lookup"><span data-stu-id="c654c-105">In this tutorial, you add authentication to the todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="c654c-106">Este tutorial está basado en el tutorial [Introducción a Mobile Apps] , que debe completar primero.</span><span class="sxs-lookup"><span data-stu-id="c654c-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="c654c-107"><a name="register"></a>Registro de la aplicación para la autenticación y configuración de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c654c-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="c654c-108"><a name="redirecturl"></a>Adición de la aplicación a las direcciones URL de redirección externa permitidas</span><span class="sxs-lookup"><span data-stu-id="c654c-108"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="c654c-109">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c654c-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="c654c-110">Esto permite que el sistema de autenticación se redirija a la aplicación una vez completado el proceso de autenticación.</span><span class="sxs-lookup"><span data-stu-id="c654c-110">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="c654c-111">En este tutorial, se usará el esquema de dirección URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="c654c-111">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="c654c-112">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="c654c-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="c654c-113">Debe ser único para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c654c-113">It should be unique to your mobile application.</span></span> <span data-ttu-id="c654c-114">Para habilitar la redirección en el lado de servidor:</span><span class="sxs-lookup"><span data-stu-id="c654c-114">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="c654c-115">En [Azure Portal], seleccione App Service.</span><span class="sxs-lookup"><span data-stu-id="c654c-115">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="c654c-116">Haga clic en la opción de menú **Autenticación/autorización**.</span><span class="sxs-lookup"><span data-stu-id="c654c-116">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="c654c-117">En **URL de redirección externas permitidas**, introduzca `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="c654c-117">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="c654c-118">El valor de _appname_ de esta cadena es el esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c654c-118">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="c654c-119">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="c654c-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="c654c-120">Debe tomar nota de la cadena que elija ya que necesitará ajustar el código de la aplicación móvil con el esquema de direcciones URL en varios sitios.</span><span class="sxs-lookup"><span data-stu-id="c654c-120">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="c654c-121">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c654c-121">Click **OK**.</span></span>

5. <span data-ttu-id="c654c-122">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="c654c-122">Click **Save**.</span></span>

## <span data-ttu-id="c654c-123"><a name="permissions"></a>Restricción de los permisos para los usuarios autenticados</span><span class="sxs-lookup"><span data-stu-id="c654c-123"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="c654c-124">En Android Studio, abra el proyecto que ha completado con el tutorial [Introducción a Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="c654c-124">In Android Studio, open the project you completed with the tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="c654c-125">En el menú **Run** (Ejecutar), haga clic en **Run app** (Ejecutar aplicación). A continuación, compruebe que se lleva a cabo una excepción no controlada con el código de estado 401 (No autorizado) después de que se inicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c654c-125">From the **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span>

     <span data-ttu-id="c654c-126">Esta excepción produce porque la aplicación intenta obtener acceso al back-end como usuario sin autenticar, pero la tabla *TodoItem* requiere ahora autenticación.</span><span class="sxs-lookup"><span data-stu-id="c654c-126">This exception happens because the app attempts to access the back end as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="c654c-127">A continuación, actualice la aplicación para autenticar usuarios antes de solicitar recursos del back-end de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="c654c-127">Next, you update the app to authenticate users before requesting resources from the Mobile Apps back end.</span></span> 

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="c654c-128">Incorporación de autenticación a la aplicación</span><span class="sxs-lookup"><span data-stu-id="c654c-128">Add authentication to the app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="c654c-129"><a name="cache-tokens"></a>Almacenamiento en caché de tokens de autenticación en el cliente</span><span class="sxs-lookup"><span data-stu-id="c654c-129"><a name="cache-tokens"></a>Cache authentication tokens on the client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="c654c-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c654c-130">Next steps</span></span>
<span data-ttu-id="c654c-131">Ahora que ha completado este tutorial de autenticación básica, considere la posibilidad de continuar con uno de los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="c654c-131">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="c654c-132">[Incorporación de notificaciones push a la aplicación de Android](app-service-mobile-android-get-started-push.md)</span><span class="sxs-lookup"><span data-stu-id="c654c-132">[Add push notifications to your Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="c654c-133">Aprenda a configurar su back-end de Mobile Apps para usar Azure Notification Hubs para enviar notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="c654c-133">Learn how to configure your Mobile Apps back end to use Azure notification hubs to send push notifications.</span></span>
* <span data-ttu-id="c654c-134">[Habilitación de la sincronización sin conexión para la aplicación móvil de Android](app-service-mobile-android-get-started-offline-data.md)</span><span class="sxs-lookup"><span data-stu-id="c654c-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="c654c-135">Aprenda a agregar compatibilidad sin conexión a una aplicación con un back-end de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="c654c-135">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="c654c-136">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;aun cuando no haya conexión de red.</span><span class="sxs-lookup"><span data-stu-id="c654c-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions to authenticated users]: #permissions
[Add authentication to the app]: #add-authentication
[Store authentication tokens on the client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
<span data-ttu-id="c654c-137">[Introducción a Mobile Apps]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c654c-137">[Get started with Mobile Apps]: app-service-mobile-android-get-started.md</span></span>
