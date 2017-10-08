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
# <a name="add-push-notifications-tooyour-android-app"></a>Agregar aplicación de Android de tooyour de notificaciones de inserción
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Información general
En este tutorial, agregará toohello de notificaciones de inserción [inicio rápido Android] del proyecto para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.

Si no usa Hola descarga el proyecto de servidor de inicio rápido, necesita Hola paquete de extensión de notificación de inserción. Para obtener más información, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Requisitos previos
Necesita Hola siguiente:

* Un IDE que depende del back-end del proyecto:

  * [Android Studio](https://developer.android.com/sdk/index.html) si esta aplicación tiene un back-end de Node.js.
  * [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) o posterior si esta aplicación tiene un back-end. NET.
* Android 2.3 o posterior y revisión de Google Repository 27 o superior, Google Play Services 9.0.2 o superior para Firebase Cloud Messaging
* Hola completa [inicio rápido Android].

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Creación de un proyecto que admita Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>Configuración de un Centro de notificaciones
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Configurar notificaciones de inserción de Azure toosend
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a>Habilitar las notificaciones de inserción de proyecto del servidor hello
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a>Agregar aplicación de tooyour de notificaciones de inserción
En esta sección, actualice las notificaciones de inserción de cliente aplicación Android toohandle.

### <a name="verify-android-sdk-version"></a>Comprobación de la versión del SDK de Android
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

El siguiente paso es tooinstall servicios de Google Play. Google Cloud Messaging tiene ciertos requisitos mínimos de nivel de API para desarrollo y pruebas, qué hello **minSdkVersion** propiedad en el manifiesto de hello debe cumplir.

Si va a probar con un dispositivo anterior, consulte [establecer seguridad de Google Play SDK de servicios] toodetermine lo bajo que puede establecer este valor y configurarlo de forma adecuada.

### <a name="add-google-play-services-toohello-project"></a>Agregar proyecto de Google Play services toohello
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a>Incorporación de código
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a>Aplicación de prueba hello contra Hola publicado servicio móvil
Puede probar la aplicación hello adjuntando un teléfono Android con un cable USB directamente o mediante un dispositivo virtual en el emulador de Hola.

## <a name="next-steps"></a>Pasos siguientes
Completado este tutorial, considere la posibilidad de continuar en tooone de hello tutoriales:

* [Agregar aplicación de Android authentication tooyour](app-service-mobile-android-get-started-users.md).
  Obtenga información acerca de cómo tooadd autenticación toohello todolist quickstart proyectar en Android mediante un proveedor de identidades admitidos.
* [Habilitación de la sincronización sin conexión para la aplicación móvil de Android](app-service-mobile-android-get-started-offline-data.md)
  Obtenga información acerca de cómo tooadd sin conexión son compatibles con tooyour aplicación mediante el uso de un back-end de aplicaciones móviles. La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;aun cuando no haya conexión de red.

<!-- URLs -->
[inicio rápido Android]: app-service-mobile-android-get-started.md

[establecer seguridad de Google Play SDK de servicios]:https://developers.google.com/android/guides/setup
