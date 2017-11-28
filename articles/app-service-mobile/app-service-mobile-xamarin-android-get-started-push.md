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
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a><span data-ttu-id="e5aa0-103">Agregar aplicación de Xamarin.Android de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="e5aa0-103">Add push notifications tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="e5aa0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e5aa0-104">Overview</span></span>
<span data-ttu-id="e5aa0-105">En este tutorial, agregará toohello de notificaciones de inserción [inicio rápido de Xamarin.Android](app-service-mobile-windows-store-dotnet-get-started.md) del proyecto para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-105">In this tutorial, you add push notifications toohello [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="e5aa0-106">Si no usa Hola descarga el proyecto de servidor de inicio rápido, se necesita Hola paquete de extensión de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="e5aa0-107">Vea [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5aa0-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e5aa0-108">Prerequisites</span></span>
<span data-ttu-id="e5aa0-109">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="e5aa0-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="e5aa0-110">Una cuenta de Google activa.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-110">An active Google account.</span></span> <span data-ttu-id="e5aa0-111">Puede registrarse para obtener una cuenta de Google en [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="e5aa0-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="e5aa0-112">[Componente del cliente de Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="e5aa0-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="e5aa0-113"><a name="configure-hub"></a>Configurar un Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="e5aa0-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="e5aa0-114"><a id="register"></a>Habilitar la mensajería en la nube Firebase</span><span class="sxs-lookup"><span data-stu-id="e5aa0-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a><span data-ttu-id="e5aa0-115">Configurar las solicitudes de inserción de Azure toosend</span><span class="sxs-lookup"><span data-stu-id="e5aa0-115">Configure Azure toosend push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="e5aa0-116"><a id="update-server"></a>Actualizar notificaciones de inserción de hello servidor proyecto toosend</span><span class="sxs-lookup"><span data-stu-id="e5aa0-116"><a id="update-server"></a>Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="e5aa0-117"><a id="configure-app"></a>Configurar el proyecto de cliente de Hola para notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="e5aa0-117"><a id="configure-app"></a>Configure hello client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="e5aa0-118"><a id="add-push"></a>Agregar aplicación de tooyour de código de las notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="e5aa0-118"><a id="add-push"></a>Add push notifications code tooyour app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="e5aa0-119"><a name="test"></a>Prueba de las notificaciones push en su aplicación</span><span class="sxs-lookup"><span data-stu-id="e5aa0-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="e5aa0-120">Puede probar la aplicación hello mediante el uso de un dispositivo virtual en el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-120">You can test hello app by using a virtual device in hello emulator.</span></span> <span data-ttu-id="e5aa0-121">Hay pasos de configuración adicionales necesarios cuando se ejecuta en un emulador.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="e5aa0-122">Asegúrese de que se va a implementar tooor depuración en un dispositivo virtual que tiene Google APIs establecer como destino de hello, tal y como se muestra a continuación, en el Administrador de dispositivos virtuales Android (AVD) Hola.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-122">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="e5aa0-123">Agregar un dispositivo Android de Google cuenta toohello haciendo clic en **aplicaciones** > **configuración** > **Agregar cuenta**, siga las instrucciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-123">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="e5aa0-124">Ejecutar la aplicación de todolist hello como antes e insertar un nuevo elemento de lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-124">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="e5aa0-125">Esta vez, se muestra un icono de notificación en el área de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-125">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="e5aa0-126">Puede abrir Hola notificación cajón tooview Hola texto completo de la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5aa0-126">You can open hello notification drawer tooview hello full text of hello notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
