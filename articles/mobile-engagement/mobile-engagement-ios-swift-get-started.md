---
title: "Introducción a Azure Mobile Engagement para iOS en Swift | Microsoft Docs"
description: "Aprenda a usar Azure Mobile Engagement con los análisis y las notificaciones de inserción para aplicaciones iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 1011b9823333e79a52cd2d187df4f8d063b1f799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="ad693-103">Introducción a Azure Mobile Engagement para aplicaciones iOS en Swift</span><span class="sxs-lookup"><span data-stu-id="ad693-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="ad693-104">En este tema se muestra cómo utilizar Azure Mobile Engagement para conocer el uso de las aplicaciones y enviar notificaciones push a usuarios segmentados en una aplicación de iOS.</span><span class="sxs-lookup"><span data-stu-id="ad693-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="ad693-105">En este tutorial, puede crear una aplicación iOS vacía que recopile datos básicos y reciba notificaciones push mediante el sistema de notificaciones push de Apple (APN).</span><span class="sxs-lookup"><span data-stu-id="ad693-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="ad693-106">Este tutorial requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ad693-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="ad693-107">XCode 8, que se puede instalar desde la tienda de aplicaciones para Mac</span><span class="sxs-lookup"><span data-stu-id="ad693-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="ad693-108">[SDK de Mobile Engagement iOS]</span><span class="sxs-lookup"><span data-stu-id="ad693-108">the [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="ad693-109">Certificado de notificaciones push (.p12), que puede obtener en el centro de desarrolladores de Apple.</span><span class="sxs-lookup"><span data-stu-id="ad693-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="ad693-110">En este tutorial se usa Swift, versión 3.0.</span><span class="sxs-lookup"><span data-stu-id="ad693-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="ad693-111">Completar este tutorial es un requisito previo para todos los tutoriales de Mobile Engagement para aplicaciones iOS.</span><span class="sxs-lookup"><span data-stu-id="ad693-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="ad693-112">Para completar este tutorial, deberá tener una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="ad693-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ad693-113">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="ad693-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ad693-114">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span><span class="sxs-lookup"><span data-stu-id="ad693-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="ad693-115"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="ad693-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="ad693-116"><a id="connecting-app"></a>Conectar la aplicación al backend de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ad693-116"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="ad693-117">En este tutorial se presenta una "integración básica", que es el conjunto mínimo necesario para recopilar los datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="ad693-117">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="ad693-118">Toda la información sobre la integración se encuentra en la [Integración del SDK de Mobile Engagement para iOS](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ad693-118">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="ad693-119">Crearemos una aplicación básica con XCode para demostrar la integración:</span><span class="sxs-lookup"><span data-stu-id="ad693-119">We will create a basic app with XCode to demonstrate the integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="ad693-120">Creación de un nuevo proyecto iOS</span><span class="sxs-lookup"><span data-stu-id="ad693-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="ad693-121">Conectar la aplicación al back-end de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ad693-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="ad693-122">Descargue el [SDK de Mobile Engagement iOS]</span><span class="sxs-lookup"><span data-stu-id="ad693-122">Download the [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="ad693-123">Extraiga el archivo .tar.gz archivo en una carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="ad693-123">Extract the .tar.gz file to a folder in your computer</span></span>
3. <span data-ttu-id="ad693-124">Haga clic con el botón derecho del mouse en el proyecto y elija "Agregar archivos a...".</span><span class="sxs-lookup"><span data-stu-id="ad693-124">Right click the project and select "Add files to ..."</span></span>
   
    ![][1]
4. <span data-ttu-id="ad693-125">Navegue hasta la carpeta donde extrajo el SDK y seleccione la carpeta `EngagementSDK` y, luego, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="ad693-125">Navigate to the folder where you extracted the SDK and select the `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="ad693-126">Abra la ficha `Build Phases` y en el menú `Link Binary With Libraries` agregue los marcos tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="ad693-126">Open the `Build Phases` tab and in the `Link Binary With Libraries` menu add the frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="ad693-127">Cree un encabezado puente para poder usar las API de Objective-C de SDK mediante la selección de Archivo > Nuevo > Archivo > iOS > Origen > Archivo de encabezado.</span><span class="sxs-lookup"><span data-stu-id="ad693-127">Create a Bridging header to be able to use the SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="ad693-128">Edite el archivo de encabezado puente para exponer el código Mobile Engagement Objective-C en el código Swift, agregue las importaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad693-128">Edit the bridging header file to expose Mobile Engagement Objective-C code to your Swift code, add the following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="ad693-129">En Configuración de compilación, asegúrese de que la compilación del encabezado puente Objective-C en Compilador de Swift - Generación de código tiene una ruta de acceso a este encabezado.</span><span class="sxs-lookup"><span data-stu-id="ad693-129">Under Build Settings, make sure the Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path to this header.</span></span> <span data-ttu-id="ad693-130">Este es un ejemplo de ruta de acceso: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (en función de la ruta de acceso)**</span><span class="sxs-lookup"><span data-stu-id="ad693-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on the path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="ad693-131">Vuelva al portal de Azure en la página *Información de conexión* de la aplicación y copie la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="ad693-131">Go back to the Azure portal in your app's *Connection Info* page and copy the Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="ad693-132">Pegue la cadena de conexión en el delegado `didFinishLaunchingWithOptions`</span><span class="sxs-lookup"><span data-stu-id="ad693-132">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="ad693-133"><a id="monitor"></a>Habilitar supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="ad693-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="ad693-134">Para comenzar a enviar datos y asegurarse de que los usuarios estén activos, debe enviar al menos una pantalla (Actividad) al back-end de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ad693-134">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="ad693-135">Abra el archivo **ViewController.swift** y reemplace la clase base de **ViewController** para que sea **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="ad693-135">Open the **ViewController.swift** file and replace the base class of **ViewController** to be **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="ad693-136"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="ad693-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="ad693-137"><a id="integrate-push"></a>Habilitación de las notificaciones de inserción y mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="ad693-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="ad693-138">Mobile Engagement permite interactuar y llegar a los usuarios mediante notificaciones de inserción y mensajería en la aplicación en el contexto de las campañas.</span><span class="sxs-lookup"><span data-stu-id="ad693-138">Mobile Engagement allows you to interact and REACH with your users with Push Notifications and In-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="ad693-139">Este módulo se denomina REACH en el portal de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ad693-139">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="ad693-140">En las secciones siguientes se instalará la aplicación para recibirlos.</span><span class="sxs-lookup"><span data-stu-id="ad693-140">The following sections will setup your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="ad693-141">Habilitación de la aplicación para recibir notificaciones push silenciosas</span><span class="sxs-lookup"><span data-stu-id="ad693-141">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="ad693-142">Adición de la biblioteca de cobertura al proyecto</span><span class="sxs-lookup"><span data-stu-id="ad693-142">Add the Reach library to your project</span></span>
1. <span data-ttu-id="ad693-143">Haga clic con el botón derecho del mouse en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ad693-143">Right click your project</span></span>
2. <span data-ttu-id="ad693-144">Seleccionar `Add file to ...`</span><span class="sxs-lookup"><span data-stu-id="ad693-144">Select `Add file to ...`</span></span>
3. <span data-ttu-id="ad693-145">Navegue hasta la carpeta donde extrajo el SDK.</span><span class="sxs-lookup"><span data-stu-id="ad693-145">Navigate to the folder where you extracted the SDK</span></span>
4. <span data-ttu-id="ad693-146">Seleccione la carpeta `EngagementReach`</span><span class="sxs-lookup"><span data-stu-id="ad693-146">Select the `EngagementReach` folder</span></span>
5. <span data-ttu-id="ad693-147">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="ad693-147">Click Add</span></span>
6. <span data-ttu-id="ad693-148">Edite el archivo de encabezado puente para exponer encabezados Mobile Engagement Objective-C Reach y agregue las importaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="ad693-148">Edit the bridging header file to expose Mobile Engagement Objective-C Reach headers and add the following imports :</span></span>
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a><span data-ttu-id="ad693-149">Modifique su delegado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ad693-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="ad693-150">En el método `didFinishLaunchingWithOptions`, cree un módulo de cobertura y páselo a la línea de inicialización existente de Engagement:</span><span class="sxs-lookup"><span data-stu-id="ad693-150">Inside  the `didFinishLaunchingWithOptions` -  create a reach module and pass it to your existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="ad693-151">Habilite su aplicación para recibir notificaciones push de APN.</span><span class="sxs-lookup"><span data-stu-id="ad693-151">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="ad693-152">Agregue la siguiente línea al método `didFinishLaunchingWithOptions`:</span><span class="sxs-lookup"><span data-stu-id="ad693-152">Add the following line to the `didFinishLaunchingWithOptions` method:</span></span>
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. <span data-ttu-id="ad693-153">Agregue el método `didRegisterForRemoteNotificationsWithDeviceToken` de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="ad693-153">Add the `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="ad693-154">Agregue el método `didReceiveRemoteNotification:fetchCompletionHandler:` de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="ad693-154">Add the `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
<span data-ttu-id="ad693-155">[SDK de Mobile Engagement iOS]: http://aka.ms/qk2rnj</span><span class="sxs-lookup"><span data-stu-id="ad693-155">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
