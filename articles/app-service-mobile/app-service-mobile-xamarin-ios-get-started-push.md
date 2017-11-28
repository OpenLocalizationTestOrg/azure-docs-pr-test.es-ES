---
title: "aplicación Xamarin.iOS tooyour de notificaciones de inserción de aaaAdd con el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo toosend de servicio de aplicaciones de Azure toouse push notificaciones tooyour Xamarin.iOS aplicación"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a><span data-ttu-id="a3cf9-103">Agregar tooyour de notificaciones de inserción Xamarin.iOS App</span><span class="sxs-lookup"><span data-stu-id="a3cf9-103">Add push notifications tooyour Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="a3cf9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a3cf9-104">Overview</span></span>
<span data-ttu-id="a3cf9-105">En este tutorial, agregará toohello de notificaciones de inserción [inicio rápido de Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) del proyecto para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-105">In this tutorial, you add push notifications toohello [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="a3cf9-106">Si no usa Hola descarga el proyecto de servidor de inicio rápido, se necesita Hola paquete de extensión de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="a3cf9-107">Vea [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3cf9-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a3cf9-108">Prerequisites</span></span>
* <span data-ttu-id="a3cf9-109">Hola completa [inicio rápido de Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-109">Complete hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="a3cf9-110">Un dispositivo iOS físico.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-110">A physical iOS device.</span></span> <span data-ttu-id="a3cf9-111">Notificaciones de inserción no son compatibles con el simulador de iOS de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-111">Push notifications are not supported by hello iOS simulator.</span></span>

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="a3cf9-112">Registrar la aplicación hello las notificaciones de inserción en el portal para desarrolladores de Apple</span><span class="sxs-lookup"><span data-stu-id="a3cf9-112">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a><span data-ttu-id="a3cf9-113">Configurar las notificaciones de inserción de toosend de aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="a3cf9-113">Configure your Mobile App toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="a3cf9-114">Actualizar notificaciones de inserción de hello servidor proyecto toosend</span><span class="sxs-lookup"><span data-stu-id="a3cf9-114">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="a3cf9-115">Configuración del proyecto de Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="a3cf9-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="a3cf9-116">Agregar aplicación de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="a3cf9-116">Add push notifications tooyour app</span></span>
1. <span data-ttu-id="a3cf9-117">En **QSTodoService**, agregar Hola después de propiedad para que **AppDelegate** puede adquirir el cliente móvil hello:</span><span class="sxs-lookup"><span data-stu-id="a3cf9-117">In **QSTodoService**, add hello following property so that **AppDelegate** can acquire hello mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="a3cf9-118">Agregue Hola siguiente `using` arriba toohello de instrucción de hello **AppDelegate.cs** archivo.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-118">Add hello following `using` statement toohello top of hello **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="a3cf9-119">En **AppDelegate**, invalidar hello **FinishedLaunching** eventos:</span><span class="sxs-lookup"><span data-stu-id="a3cf9-119">In **AppDelegate**, override hello **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="a3cf9-120">En Hola el mismo archivo, invalide hello **RegisteredForRemoteNotifications** eventos.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-120">In hello same file, override hello **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="a3cf9-121">En este código está registrando para una notificación de plantilla simple que se enviarán a través de todas las plataformas admitidas por el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by hello server.</span></span>
   
    <span data-ttu-id="a3cf9-122">Para más información sobre las plantillas con centros de notificaciones, vea [Plantillas](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="a3cf9-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="a3cf9-123">A continuación, invalidar hello **DidReceivedRemoteNotification** eventos:</span><span class="sxs-lookup"><span data-stu-id="a3cf9-123">Then, override hello **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="a3cf9-124">La aplicación ya está actualizado toosupport notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-124">Your app is now updated toosupport push notifications.</span></span>

## <span data-ttu-id="a3cf9-125"><a name="test"></a>Prueba de las notificaciones push en su aplicación</span><span class="sxs-lookup"><span data-stu-id="a3cf9-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="a3cf9-126">Hola presione **ejecutar** toobuild proyecto de Hola e Iniciar aplicación hello en un dispositivo compatible con iOS, a continuación, haga clic en **Aceptar** tooaccept notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-126">Press hello **Run** button toobuild hello project and start hello app in an iOS capable device, then click **OK** tooaccept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a3cf9-127">Debe aceptar de forma explícita las notificaciones push desde su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="a3cf9-128">Esta solicitud sólo produce a Hola primera vez que Hola se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-128">This request only occurs hello first time that hello app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="a3cf9-129">En la aplicación hello, escriba una tarea y, a continuación, haga clic en hello signo más (**+**) icono.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-129">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
3. <span data-ttu-id="a3cf9-130">Compruebe que se recibe una notificación, y haga clic en **Aceptar** toodismiss Hola notificación.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-130">Verify that a notification is received, then click **OK** toodismiss hello notification.</span></span>
4. <span data-ttu-id="a3cf9-131">Repita el paso 2 y cierre inmediatamente Hola aplicación, a continuación, compruebe que aparece una notificación.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-131">Repeat step 2 and immediately close hello app, then verify that a notification is shown.</span></span>

<span data-ttu-id="a3cf9-132">Ha completado correctamente este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



