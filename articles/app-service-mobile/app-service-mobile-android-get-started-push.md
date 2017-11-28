---
title: "aaaAdd inserción notificaciones tooyour aplicación Android con aplicaciones móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse aplicaciones móviles toosend push aplicación Android tooyour de notificaciones."
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a><span data-ttu-id="63352-103">Agregar aplicación de Android de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="63352-103">Add push notifications tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="63352-104">Información general</span><span class="sxs-lookup"><span data-stu-id="63352-104">Overview</span></span>
<span data-ttu-id="63352-105">En este tutorial, agregará toohello de notificaciones de inserción [inicio rápido Android] del proyecto para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.</span><span class="sxs-lookup"><span data-stu-id="63352-105">In this tutorial, you add push notifications toohello [Android quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="63352-106">Si no usa Hola descarga el proyecto de servidor de inicio rápido, necesita Hola paquete de extensión de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="63352-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="63352-107">Para obtener más información, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="63352-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63352-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="63352-108">Prerequisites</span></span>
<span data-ttu-id="63352-109">Necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="63352-109">You need hello following:</span></span>

* <span data-ttu-id="63352-110">Un IDE que depende del back-end del proyecto:</span><span class="sxs-lookup"><span data-stu-id="63352-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="63352-111">[Android Studio](https://developer.android.com/sdk/index.html) si esta aplicación tiene un back-end de Node.js.</span><span class="sxs-lookup"><span data-stu-id="63352-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="63352-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) o posterior si esta aplicación tiene un back-end. NET.</span><span class="sxs-lookup"><span data-stu-id="63352-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="63352-113">Android 2.3 o posterior y revisión de Google Repository 27 o superior, Google Play Services 9.0.2 o superior para Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="63352-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="63352-114">Hola completa [inicio rápido Android].</span><span class="sxs-lookup"><span data-stu-id="63352-114">Complete hello [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="63352-115">Creación de un proyecto que admita Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="63352-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="63352-116">Configuración de un Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="63352-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="63352-117">Configurar notificaciones de inserción de Azure toosend</span><span class="sxs-lookup"><span data-stu-id="63352-117">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a><span data-ttu-id="63352-118">Habilitar las notificaciones de inserción de proyecto del servidor hello</span><span class="sxs-lookup"><span data-stu-id="63352-118">Enable push notifications for hello server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="63352-119">Agregar aplicación de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="63352-119">Add push notifications tooyour app</span></span>
<span data-ttu-id="63352-120">En esta sección, actualice las notificaciones de inserción de cliente aplicación Android toohandle.</span><span class="sxs-lookup"><span data-stu-id="63352-120">In this section, you update your client Android app toohandle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="63352-121">Comprobación de la versión del SDK de Android</span><span class="sxs-lookup"><span data-stu-id="63352-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="63352-122">El siguiente paso es tooinstall servicios de Google Play.</span><span class="sxs-lookup"><span data-stu-id="63352-122">Your next step is tooinstall Google Play services.</span></span> <span data-ttu-id="63352-123">Google Cloud Messaging tiene ciertos requisitos mínimos de nivel de API para desarrollo y pruebas, qué hello **minSdkVersion** propiedad en el manifiesto de hello debe cumplir.</span><span class="sxs-lookup"><span data-stu-id="63352-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which hello **minSdkVersion** property in hello manifest must conform to.</span></span>

<span data-ttu-id="63352-124">Si va a probar con un dispositivo anterior, consulte [establecer seguridad de Google Play SDK de servicios] toodetermine lo bajo que puede establecer este valor y configurarlo de forma adecuada.</span><span class="sxs-lookup"><span data-stu-id="63352-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] toodetermine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="63352-125">Agregar proyecto de Google Play services toohello</span><span class="sxs-lookup"><span data-stu-id="63352-125">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="63352-126">Incorporación de código</span><span class="sxs-lookup"><span data-stu-id="63352-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a><span data-ttu-id="63352-127">Aplicación de prueba hello contra Hola publicado servicio móvil</span><span class="sxs-lookup"><span data-stu-id="63352-127">Test hello app against hello published mobile service</span></span>
<span data-ttu-id="63352-128">Puede probar la aplicación hello adjuntando un teléfono Android con un cable USB directamente o mediante un dispositivo virtual en el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="63352-128">You can test hello app by directly attaching an Android phone with a USB cable, or by using a virtual device in hello emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63352-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="63352-129">Next steps</span></span>
<span data-ttu-id="63352-130">Completado este tutorial, considere la posibilidad de continuar en tooone de hello tutoriales:</span><span class="sxs-lookup"><span data-stu-id="63352-130">Now that you completed this tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="63352-131">[Agregar aplicación de Android authentication tooyour](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="63352-131">[Add authentication tooyour Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="63352-132">Obtenga información acerca de cómo tooadd autenticación toohello todolist quickstart proyectar en Android mediante un proveedor de identidades admitidos.</span><span class="sxs-lookup"><span data-stu-id="63352-132">Learn how tooadd authentication toohello todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="63352-133">[Habilitación de la sincronización sin conexión para la aplicación móvil de Android](app-service-mobile-android-get-started-offline-data.md)</span><span class="sxs-lookup"><span data-stu-id="63352-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="63352-134">Obtenga información acerca de cómo tooadd sin conexión son compatibles con tooyour aplicación mediante el uso de un back-end de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="63352-134">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="63352-135">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;aun cuando no haya conexión de red.</span><span class="sxs-lookup"><span data-stu-id="63352-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[inicio rápido Android]: app-service-mobile-android-get-started.md

[establecer seguridad de Google Play SDK de servicios]:https://developers.google.com/android/guides/setup
