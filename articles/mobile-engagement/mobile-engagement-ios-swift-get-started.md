---
title: aaaGet Started with Azure Mobile Engagement para iOS en Swift | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con análisis y notificaciones de inserción para aplicaciones iOS."
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
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="48889-103">Introducción a Azure Mobile Engagement para aplicaciones iOS en Swift</span><span class="sxs-lookup"><span data-stu-id="48889-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="48889-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de aplicaciones y el envío de inserción tooan iOS aplicación de notificaciones toosegmented a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="48889-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="48889-105">En este tutorial, puede crear una aplicación iOS vacía que recopile datos básicos y reciba notificaciones push mediante el sistema de notificaciones push de Apple (APN).</span><span class="sxs-lookup"><span data-stu-id="48889-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="48889-106">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="48889-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="48889-107">XCode 8, que se puede instalar desde la tienda de aplicaciones para Mac</span><span class="sxs-lookup"><span data-stu-id="48889-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="48889-108">Hola [Mobile Engagement SDK para iOS]</span><span class="sxs-lookup"><span data-stu-id="48889-108">hello [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="48889-109">Certificado de notificaciones push (.p12), que puede obtener en el centro de desarrolladores de Apple.</span><span class="sxs-lookup"><span data-stu-id="48889-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="48889-110">En este tutorial se usa Swift, versión 3.0.</span><span class="sxs-lookup"><span data-stu-id="48889-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="48889-111">Completar este tutorial es un requisito previo para todos los tutoriales de Mobile Engagement para aplicaciones iOS.</span><span class="sxs-lookup"><span data-stu-id="48889-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="48889-112">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="48889-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="48889-113">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="48889-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="48889-114">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span><span class="sxs-lookup"><span data-stu-id="48889-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="48889-115"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="48889-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="48889-116"><a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="48889-116"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="48889-117">Este tutorial presenta una "la integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="48889-117">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="48889-118">Encontrará documentación de integración completa de Hola Hola [integración de SDK de Mobile Engagement iOS](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="48889-118">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="48889-119">Se creará una aplicación básica con la integración de hello toodemonstrate XCode:</span><span class="sxs-lookup"><span data-stu-id="48889-119">We will create a basic app with XCode toodemonstrate hello integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="48889-120">Creación de un nuevo proyecto iOS</span><span class="sxs-lookup"><span data-stu-id="48889-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="48889-121">Conectar el backend de interacción de tooMobile de aplicación</span><span class="sxs-lookup"><span data-stu-id="48889-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="48889-122">Descargar hello [Mobile Engagement SDK para iOS]</span><span class="sxs-lookup"><span data-stu-id="48889-122">Download hello [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="48889-123">Extraer Hola. tar.gz carpeta de tooa de archivo en el equipo</span><span class="sxs-lookup"><span data-stu-id="48889-123">Extract hello .tar.gz file tooa folder in your computer</span></span>
3. <span data-ttu-id="48889-124">Haga clic en proyecto de Hola y seleccione "Agregar archivos demasiado..."</span><span class="sxs-lookup"><span data-stu-id="48889-124">Right click hello project and select "Add files too..."</span></span>
   
    ![][1]
4. <span data-ttu-id="48889-125">Desplazarse por las carpetas de toohello en la que extrajo Hola SDK y seleccione Hola `EngagementSDK` carpeta, a continuación, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="48889-125">Navigate toohello folder where you extracted hello SDK and select hello `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="48889-126">Abra hello `Build Phases` ficha y Hola `Link Binary With Libraries` menú Agregar marcos Hola tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="48889-126">Open hello `Build Phases` tab and in hello `Link Binary With Libraries` menu add hello frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="48889-127">Para crear un protocolo de puente del encabezado toobe toouse capaz de hello del objetivo C API del SDK, seleccione Archivo > Nuevo > Archivo > iOS > origen > archivo de encabezado.</span><span class="sxs-lookup"><span data-stu-id="48889-127">Create a Bridging header toobe able toouse hello SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="48889-128">Editar archivo encabezado tooyour tooexpose Mobile Engagement Objective-C código Swift código de puente de hello, agregue Hola siguientes importaciones:</span><span class="sxs-lookup"><span data-stu-id="48889-128">Edit hello bridging header file tooexpose Mobile Engagement Objective-C code tooyour Swift code, add hello following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="48889-129">En la configuración de compilación, asegúrese de que el encabezado de protocolo de puente Objective-C de compilación en el compilador de Swift: generación de código de hello tiene un encabezado de toothis de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="48889-129">Under Build Settings, make sure hello Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path toothis header.</span></span> <span data-ttu-id="48889-130">Este es un ejemplo de ruta de acceso: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (dependiendo de la ruta de acceso de hello)**</span><span class="sxs-lookup"><span data-stu-id="48889-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on hello path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="48889-131">Volver atrás toohello portal de Azure en la aplicación *información de conexión* página y copiar Hola cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="48889-131">Go back toohello Azure portal in your app's *Connection Info* page and copy hello Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="48889-132">Ahora pega cadena de conexión de Hola Hola `didFinishLaunchingWithOptions` delegar</span><span class="sxs-lookup"><span data-stu-id="48889-132">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="48889-133"><a id="monitor"></a>Habilitar supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="48889-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="48889-134">En orden toostart enviando los datos y asegurarse de que los usuarios de hello activos, debe enviar al menos un backend de interacción móvil toohello de pantalla (actividad).</span><span class="sxs-lookup"><span data-stu-id="48889-134">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="48889-135">Abra hello **ViewController.swift** archivo y reemplace la clase base hello de **ViewController** toobe **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="48889-135">Open hello **ViewController.swift** file and replace hello base class of **ViewController** toobe **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="48889-136"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="48889-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="48889-137"><a id="integrate-push"></a>Habilitación de las notificaciones de inserción y mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="48889-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="48889-138">Mobile Engagement le permite toointeract y alcance con los usuarios con las notificaciones de inserción y mensajería en la aplicación en el contexto de Hola de campañas.</span><span class="sxs-lookup"><span data-stu-id="48889-138">Mobile Engagement allows you toointeract and REACH with your users with Push Notifications and In-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="48889-139">Este módulo se denomina alcance en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="48889-139">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="48889-140">Hello las secciones siguientes se configurará la aplicación tooreceive ellos.</span><span class="sxs-lookup"><span data-stu-id="48889-140">hello following sections will setup your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="48889-141">Habilitar la tooreceive aplicación silenciosa de las notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="48889-141">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="48889-142">Agregar proyecto de hello alcance de la biblioteca tooyour</span><span class="sxs-lookup"><span data-stu-id="48889-142">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="48889-143">Haga clic con el botón derecho del mouse en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="48889-143">Right click your project</span></span>
2. <span data-ttu-id="48889-144">Seleccionar `Add file too...`</span><span class="sxs-lookup"><span data-stu-id="48889-144">Select `Add file too...`</span></span>
3. <span data-ttu-id="48889-145">Desplazarse por las carpetas de toohello en la que extrajo Hola SDK</span><span class="sxs-lookup"><span data-stu-id="48889-145">Navigate toohello folder where you extracted hello SDK</span></span>
4. <span data-ttu-id="48889-146">Seleccione hello `EngagementReach` carpeta</span><span class="sxs-lookup"><span data-stu-id="48889-146">Select hello `EngagementReach` folder</span></span>
5. <span data-ttu-id="48889-147">Haga clic en Agregar</span><span class="sxs-lookup"><span data-stu-id="48889-147">Click Add</span></span>
6. <span data-ttu-id="48889-148">Editar hello tooexpose Mobile Engagement Objective-C alcanzar encabezados de archivo de encabezado de protocolo de puente y agregue Hola siguientes importaciones:</span><span class="sxs-lookup"><span data-stu-id="48889-148">Edit hello bridging header file tooexpose Mobile Engagement Objective-C Reach headers and add hello following imports :</span></span>
   
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

### <a name="modify-your-application-delegate"></a><span data-ttu-id="48889-149">Modifique su delegado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="48889-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="48889-150">Hola interior `didFinishLaunchingWithOptions` : crear un módulo de reach y pasar tooyour línea de inicialización de contratación existente:</span><span class="sxs-lookup"><span data-stu-id="48889-150">Inside  hello `didFinishLaunchingWithOptions` -  create a reach module and pass it tooyour existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="48889-151">Habilitar la tooreceive de la aplicación notificaciones de inserción de APNS</span><span class="sxs-lookup"><span data-stu-id="48889-151">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="48889-152">Agregar Hola después línea toohello `didFinishLaunchingWithOptions` método:</span><span class="sxs-lookup"><span data-stu-id="48889-152">Add hello following line toohello `didFinishLaunchingWithOptions` method:</span></span>
   
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
2. <span data-ttu-id="48889-153">Agregar hello `didRegisterForRemoteNotificationsWithDeviceToken` método tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="48889-153">Add hello `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="48889-154">Agregar hello `didReceiveRemoteNotification:fetchCompletionHandler:` método tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="48889-154">Add hello `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement SDK para iOS]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
