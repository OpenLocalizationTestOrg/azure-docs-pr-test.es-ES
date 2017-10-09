---
title: aaaGet Started with Azure Mobile Engagement para iOS en Objective C | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement a las notificaciones de inserción y de análisis para aplicaciones de iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="52698-103">Introducción a Azure Mobile Engagement para aplicaciones iOS en Objective C</span><span class="sxs-lookup"><span data-stu-id="52698-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="52698-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de aplicaciones y el envío de inserción tooan iOS aplicación de notificaciones toosegmented a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="52698-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="52698-105">En este tutorial, puede crear una aplicación iOS vacía que recopile datos básicos y reciba notificaciones push mediante el sistema de notificaciones push de Apple (APN).</span><span class="sxs-lookup"><span data-stu-id="52698-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="52698-106">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="52698-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="52698-107">XCode 8, que se puede instalar desde la tienda de aplicaciones para Mac</span><span class="sxs-lookup"><span data-stu-id="52698-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="52698-108">Hola [Mobile Engagement SDK para iOS]</span><span class="sxs-lookup"><span data-stu-id="52698-108">hello [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="52698-109">Completar este tutorial es un requisito previo para todos los tutoriales de Mobile Engagement para aplicaciones iOS.</span><span class="sxs-lookup"><span data-stu-id="52698-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="52698-110">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="52698-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="52698-111">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="52698-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="52698-112">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="52698-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="52698-113"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="52698-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="52698-114"><a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="52698-114"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="52698-115">Este tutorial presenta una "la integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="52698-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="52698-116">Encontrará documentación de integración completa de Hola Hola [integración de SDK de Mobile Engagement iOS](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="52698-116">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="52698-117">Se creará una aplicación básica con la integración de XCode toodemonstrate Hola.</span><span class="sxs-lookup"><span data-stu-id="52698-117">We will create a basic app with XCode toodemonstrate hello integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="52698-118">Creación de un nuevo proyecto iOS</span><span class="sxs-lookup"><span data-stu-id="52698-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="52698-119">Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="52698-119">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="52698-120">Descargar hello [Mobile Engagement SDK para iOS].</span><span class="sxs-lookup"><span data-stu-id="52698-120">Download hello [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="52698-121">Extraer Hola. tar.gz carpeta de tooa de archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="52698-121">Extract hello .tar.gz file tooa folder in your computer.</span></span>
3. <span data-ttu-id="52698-122">Haga clic en proyecto de hello y, a continuación, seleccione **agrega archivos a**.</span><span class="sxs-lookup"><span data-stu-id="52698-122">Right-click hello project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="52698-123">Desplazarse por las carpetas de toohello en la que extrajo Hola SDK, seleccione hello `EngagementSDK` carpeta, haga clic en **opciones** Hola esquina inferior izquierda y asegúrese de que esa casilla hello **copiar elementos si es necesario** hello y casilla de verificación para el destino se comprueban a continuación, presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="52698-123">Navigate toohello folder where you extracted hello SDK, select hello `EngagementSDK` folder, click **Options** on hello bottom left corner and make sure that hello checkbox **Copy items if needed** and hello checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="52698-124">Hola abierto **fases de compilación** ficha y en hello **binario con las bibliotecas de vínculos** menú, agregue marcos de hello tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="52698-124">Open hello **Build Phases** tab, and in hello **Link Binary With Libraries** menu, add hello frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="52698-125">Volver atrás toohello portal de Azure en la aplicación **información de conexión** página y copiar la cadena de conexión Hola.</span><span class="sxs-lookup"><span data-stu-id="52698-125">Go back toohello Azure portal in your app's **Connection Info** page and copy hello connection string.</span></span>

    ![][4]
7. <span data-ttu-id="52698-126">Agregar Hola después de la línea de código en su **AppDelegate.m** archivo.</span><span class="sxs-lookup"><span data-stu-id="52698-126">Add hello following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="52698-127">Ahora pega cadena de conexión de Hola Hola `didFinishLaunchingWithOptions` delegar.</span><span class="sxs-lookup"><span data-stu-id="52698-127">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="52698-128">`setTestLogEnabled`es una instrucción opcional que permite los registros SDK que tooidentify problemas.</span><span class="sxs-lookup"><span data-stu-id="52698-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you tooidentify issues.</span></span>

## <span data-ttu-id="52698-129"><a id="monitor"></a>Habilitación de la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="52698-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="52698-130">En orden toostart enviando los datos y asegurarse de que los usuarios de hello activos, debe enviar al menos un backend de interacción móvil toohello de pantalla (actividad).</span><span class="sxs-lookup"><span data-stu-id="52698-130">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="52698-131">Abra hello **ViewController.h** archivo e importar **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="52698-131">Open hello **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="52698-132">Ahora reemplace superclase Hola de hello **ViewController** interfaz por `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="52698-132">Now replace hello super class of hello **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="52698-133"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="52698-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="52698-134"><a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="52698-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="52698-135">Mobile Engagement le permite toointeract con los usuarios y alcance con notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas.</span><span class="sxs-lookup"><span data-stu-id="52698-135">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="52698-136">Este módulo se denomina alcance en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="52698-136">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="52698-137">Hello las secciones siguientes configure su aplicación tooreceive ellos.</span><span class="sxs-lookup"><span data-stu-id="52698-137">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="52698-138">Habilitar la tooreceive aplicación silenciosa de las notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="52698-138">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="52698-139">Agregar proyecto de hello alcance de la biblioteca tooyour</span><span class="sxs-lookup"><span data-stu-id="52698-139">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="52698-140">Haga clic con el botón derecho en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="52698-140">Right-click your project.</span></span>
2. <span data-ttu-id="52698-141">Seleccione **Agregar archivo a**.</span><span class="sxs-lookup"><span data-stu-id="52698-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="52698-142">Desplazarse por las carpetas de toohello en la que extrajo Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="52698-142">Navigate toohello folder where you extracted hello SDK.</span></span>
4. <span data-ttu-id="52698-143">Seleccione hello `EngagementReach` carpeta.</span><span class="sxs-lookup"><span data-stu-id="52698-143">Select hello `EngagementReach` folder.</span></span>
5. <span data-ttu-id="52698-144">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="52698-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="52698-145">Modifique su delegado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="52698-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="52698-146">En **AppDeletegate.m** de archivos, importe el módulo de llegar a la interacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="52698-146">Back in **AppDeletegate.m** file, import hello Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="52698-147">Hola interior `application:didFinishLaunchingWithOptions` método, cree un módulo de Reach y páselo tooyour línea de inicialización de contratación existente:</span><span class="sxs-lookup"><span data-stu-id="52698-147">Inside hello `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it tooyour existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="52698-148">Habilitar la tooreceive de la aplicación notificaciones de inserción de APNS</span><span class="sxs-lookup"><span data-stu-id="52698-148">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="52698-149">Agregar Hola después línea toohello `application:didFinishLaunchingWithOptions` método:</span><span class="sxs-lookup"><span data-stu-id="52698-149">Add hello following line toohello `application:didFinishLaunchingWithOptions` method:</span></span>

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. <span data-ttu-id="52698-150">Agregar hello `application:didRegisterForRemoteNotificationsWithDeviceToken` método tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="52698-150">Add hello `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="52698-151">Agregar hello `didFailToRegisterForRemoteNotificationsWithError` método tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="52698-151">Add hello `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. <span data-ttu-id="52698-152">Agregar hello `didReceiveRemoteNotification:fetchCompletionHandler` método tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="52698-152">Add hello `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement SDK para iOS]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
