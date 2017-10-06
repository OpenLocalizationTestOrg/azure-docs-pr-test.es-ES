---
title: "aaaAdd inserción notificaciones tooyour Xamarin.Android aplicación | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse servicio de aplicaciones de Azure y los centros de notificaciones de Azure toosend push notificaciones tooyour Xamarin.Android aplicación"
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a>Agregar aplicación de Xamarin.Android de tooyour de notificaciones de inserción
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Información general
En este tutorial, agregará toohello de notificaciones de inserción [inicio rápido de Xamarin.Android](app-service-mobile-windows-store-dotnet-get-started.md) del proyecto para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.

Si no usa Hola descarga el proyecto de servidor de inicio rápido, se necesita Hola paquete de extensión de notificación de inserción. Vea [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial requiere siguiente de hello:

* Una cuenta de Google activa. Puede registrarse para obtener una cuenta de Google en [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).
* [Componente del cliente de Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/).

## <a name="configure-hub"></a>Configurar un Centro de notificaciones
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Habilitar la mensajería en la nube Firebase
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a>Configurar las solicitudes de inserción de Azure toosend
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a>Actualizar notificaciones de inserción de hello servidor proyecto toosend
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a>Configurar el proyecto de cliente de Hola para notificaciones de inserción
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>Agregar aplicación de tooyour de código de las notificaciones de inserción
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a>Prueba de las notificaciones push en su aplicación
Puede probar la aplicación hello mediante el uso de un dispositivo virtual en el emulador de Hola. Hay pasos de configuración adicionales necesarios cuando se ejecuta en un emulador.

1. Asegúrese de que se va a implementar tooor depuración en un dispositivo virtual que tiene Google APIs establecer como destino de hello, tal y como se muestra a continuación, en el Administrador de dispositivos virtuales Android (AVD) Hola.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. Agregar un dispositivo Android de Google cuenta toohello haciendo clic en **aplicaciones** > **configuración** > **Agregar cuenta**, siga las instrucciones de Hola.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. Ejecutar la aplicación de todolist hello como antes e insertar un nuevo elemento de lista de tareas. Esta vez, se muestra un icono de notificación en el área de notificación de Hola. Puede abrir Hola notificación cajón tooview Hola texto completo de la notificación de Hola.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
