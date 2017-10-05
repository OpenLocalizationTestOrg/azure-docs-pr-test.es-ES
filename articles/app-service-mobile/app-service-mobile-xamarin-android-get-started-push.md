---
title: "Incorporación de notificaciones push a una aplicación Xamarin Android | Microsoft Docs"
description: "Más información sobre cómo usar Servicios de aplicaciones de Azure y Centros de notificaciones de Azure para enviar notificaciones push a la aplicación de Xamarin Android"
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
ms.openlocfilehash: c3757d56fb1792092710740dc5ffbd64f18730cf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a><span data-ttu-id="96d56-103">Agregar notificaciones push a la aplicación de Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="96d56-103">Add push notifications to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="96d56-104">Información general</span><span class="sxs-lookup"><span data-stu-id="96d56-104">Overview</span></span>
<span data-ttu-id="96d56-105">En este tutorial, agregará notificaciones de inserción al proyecto de [inicio rápido de Xamarin.Android](app-service-mobile-windows-store-dotnet-get-started.md) para que cada vez que se envíe una notificación de inserción al dispositivo, se inserte un registro.</span><span class="sxs-lookup"><span data-stu-id="96d56-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="96d56-106">Si no usa el proyecto de servidor de inicio rápido descargado, necesitará el paquete de extensión de la notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="96d56-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="96d56-107">Vea [Trabajar con el SDK de servidor de back-end de .NET para Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="96d56-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96d56-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="96d56-108">Prerequisites</span></span>
<span data-ttu-id="96d56-109">Este tutorial requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="96d56-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="96d56-110">Una cuenta de Google activa.</span><span class="sxs-lookup"><span data-stu-id="96d56-110">An active Google account.</span></span> <span data-ttu-id="96d56-111">Puede registrarse para obtener una cuenta de Google en [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="96d56-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="96d56-112">[Componente del cliente de Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="96d56-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="96d56-113"><a name="configure-hub"></a>Configurar un Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="96d56-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="96d56-114"><a id="register"></a>Habilitar la mensajería en la nube Firebase</span><span class="sxs-lookup"><span data-stu-id="96d56-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a><span data-ttu-id="96d56-115">Configuración de Azure para enviar notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="96d56-115">Configure Azure to send push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="96d56-116"><a id="update-server"></a>Actualizar el proyecto de servidor para que envíe notificaciones push</span><span class="sxs-lookup"><span data-stu-id="96d56-116"><a id="update-server"></a>Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="96d56-117"><a id="configure-app"></a>Configurar el proyecto cliente para las notificaciones push</span><span class="sxs-lookup"><span data-stu-id="96d56-117"><a id="configure-app"></a>Configure the client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="96d56-118"><a id="add-push"></a>Incorporación de código de notificaciones de inserción a la aplicación</span><span class="sxs-lookup"><span data-stu-id="96d56-118"><a id="add-push"></a>Add push notifications code to your app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="96d56-119"><a name="test"></a>Prueba de las notificaciones push en su aplicación</span><span class="sxs-lookup"><span data-stu-id="96d56-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="96d56-120">Puede probar la aplicación con un dispositivo virtual en el emulador.</span><span class="sxs-lookup"><span data-stu-id="96d56-120">You can test the app by using a virtual device in the emulator.</span></span> <span data-ttu-id="96d56-121">Hay pasos de configuración adicionales necesarios cuando se ejecuta en un emulador.</span><span class="sxs-lookup"><span data-stu-id="96d56-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="96d56-122">Asegúrese de que va a implementar o depurar en un dispositivo virtual que tenga las API de Google como destino, como se muestra a continuación en el administrador de dispositivo virtual Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="96d56-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="96d56-123">Agregue una cuenta de Google al dispositivo Android haciendo clic en **Aplicaciones** > **Configuración** > **Agregar cuenta** y luego siga las indicaciones.</span><span class="sxs-lookup"><span data-stu-id="96d56-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="96d56-124">Ejecute la aplicación todolist como antes e inserte un nuevo elemento todo.</span><span class="sxs-lookup"><span data-stu-id="96d56-124">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="96d56-125">Esta vez, se muestra un icono de notificación en el área de notificación.</span><span class="sxs-lookup"><span data-stu-id="96d56-125">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="96d56-126">Puede abrir el cajón de notificaciones para ver el texto completo de la notificación.</span><span class="sxs-lookup"><span data-stu-id="96d56-126">You can open the notification drawer to view the full text of the notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
