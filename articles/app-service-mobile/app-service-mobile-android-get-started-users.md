---
title: "autenticación de aaaAdd en Android con aplicaciones móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola característica de aplicaciones móviles de usuarios de tooauthenticate de servicio de aplicaciones de Azure de su aplicación Android a través de una serie de proveedores de identidades, como Google, Facebook, Twitter y Microsoft."
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
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a><span data-ttu-id="f9ce2-103">Agregar aplicación Android de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="f9ce2-103">Add authentication tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="f9ce2-104">Resumen</span><span class="sxs-lookup"><span data-stu-id="f9ce2-104">Summary</span></span>
<span data-ttu-id="f9ce2-105">En este tutorial, Agregar proyecto de inicio rápido de autenticación toohello todolist en Android mediante un proveedor de identidades admitidos.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-105">In this tutorial, you add authentication toohello todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="f9ce2-106">Este tutorial se basa en hello [empezar a trabajar con aplicaciones móviles] tutorial, que debe completar primero.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="f9ce2-107"><a name="register"></a>Registro de la aplicación para la autenticación y configuración de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f9ce2-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="f9ce2-108"><a name="redirecturl"></a>Agregue las direcciones URL de redirección externa permitido de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="f9ce2-108"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="f9ce2-109">La autenticación segura requiere que se defina un nuevo esquema de dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="f9ce2-110">Esto permite tooredirect tooyour back-aplicación de hello autenticación sistema cuando se complete el proceso de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-110">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="f9ce2-111">En este tutorial, se utiliza el esquema de dirección URL de hello _appname_ a lo largo.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-111">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="f9ce2-112">Sin embargo, puede utilizar cualquier otro esquema de dirección URL que elija.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="f9ce2-113">Debe ser único tooyour aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-113">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="f9ce2-114">redirección de hello tooenable en servidor hello:</span><span class="sxs-lookup"><span data-stu-id="f9ce2-114">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="f9ce2-115">Hola [portal de Azure], seleccione su servicio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-115">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="f9ce2-116">Haga clic en hello **autenticación / autorización** opción de menú.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-116">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="f9ce2-117">Hola **permite redirigir direcciones URL externas de**, escriba `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-117">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="f9ce2-118">Hola _appname_ de esta cadena es hello esquema de dirección URL para la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-118">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="f9ce2-119">Debe seguir la especificación normal de las direcciones URL para un protocolo (usar únicamente letras y números, y comenzar por una letra).</span><span class="sxs-lookup"><span data-stu-id="f9ce2-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="f9ce2-120">Debe realizar una nota de cadena de Hola que elija, ya que será necesario tooadjust el código de aplicaciones móviles con hello esquema de dirección URL en varios lugares.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-120">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="f9ce2-121">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-121">Click **OK**.</span></span>

5. <span data-ttu-id="f9ce2-122">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-122">Click **Save**.</span></span>

## <span data-ttu-id="f9ce2-123"><a name="permissions"></a>Restringir a los usuarios de tooauthenticated de permisos</span><span class="sxs-lookup"><span data-stu-id="f9ce2-123"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="f9ce2-124">En Android Studio, abra el proyecto de Hola que completado con el tutorial de hello [empezar a trabajar con aplicaciones móviles].</span><span class="sxs-lookup"><span data-stu-id="f9ce2-124">In Android Studio, open hello project you completed with hello tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="f9ce2-125">De hello **ejecutar** menú, haga clic en **ejecutar aplicación**y compruebe que se produce una excepción no controlada con un código de estado de 401 (no autorizado) cuando se inicie la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-125">From hello **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span>

     <span data-ttu-id="f9ce2-126">Esta excepción ocurre porque los intentos de aplicación Hola tooaccess Hola volver end que un usuario no autenticado, pero Hola *TodoItem* tabla ahora requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-126">This exception happens because hello app attempts tooaccess hello back end as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="f9ce2-127">A continuación, actualizar los usuarios tooauthenticate de aplicación Hola antes de solicitar recursos de hello que terminar de aplicaciones móviles de nuevo.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-127">Next, you update hello app tooauthenticate users before requesting resources from hello Mobile Apps back end.</span></span> 

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="f9ce2-128">Agregar aplicación de autenticación toohello</span><span class="sxs-lookup"><span data-stu-id="f9ce2-128">Add authentication toohello app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="f9ce2-129"><a name="cache-tokens"></a>Almacenar en caché los tokens de autenticación de cliente hello</span><span class="sxs-lookup"><span data-stu-id="f9ce2-129"><a name="cache-tokens"></a>Cache authentication tokens on hello client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="f9ce2-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9ce2-130">Next steps</span></span>
<span data-ttu-id="f9ce2-131">Completado este tutorial de la autenticación básica, considere la posibilidad de continuar en tooone de hello tutoriales:</span><span class="sxs-lookup"><span data-stu-id="f9ce2-131">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="f9ce2-132">[Agregar aplicación de Android de tooyour de notificaciones de inserción](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="f9ce2-132">[Add push notifications tooyour Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="f9ce2-133">Obtenga información acerca de cómo tooconfigure realizar copias de las aplicaciones móviles finalizar notificaciones de inserción de toosend de bases de datos centrales de notificación de Azure de toouse.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-133">Learn how tooconfigure your Mobile Apps back end toouse Azure notification hubs toosend push notifications.</span></span>
* <span data-ttu-id="f9ce2-134">[Habilitación de la sincronización sin conexión para la aplicación móvil de Android](app-service-mobile-android-get-started-offline-data.md)</span><span class="sxs-lookup"><span data-stu-id="f9ce2-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="f9ce2-135">Obtenga información acerca de cómo tooadd sin conexión son compatibles con tooyour aplicación mediante el uso de un back-end de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-135">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="f9ce2-136">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;aun cuando no haya conexión de red.</span><span class="sxs-lookup"><span data-stu-id="f9ce2-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[empezar a trabajar con aplicaciones móviles]: app-service-mobile-android-get-started.md
