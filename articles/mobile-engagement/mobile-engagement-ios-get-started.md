---
title: "Introducción a Azure Mobile Engagement para iOS en Objective C | Microsoft Docs"
description: "Aprenda a usar Azure Mobile Engagement con los análisis y las notificaciones push en aplicaciones iOS."
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
ms.openlocfilehash: 1b87a2ebb35b31ee3d3139ecead6267e62eb1033
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="f49e2-103">Introducción a Azure Mobile Engagement para aplicaciones iOS en Objective C</span><span class="sxs-lookup"><span data-stu-id="f49e2-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="f49e2-104">En este tema se muestra cómo utilizar Azure Mobile Engagement para conocer el uso de las aplicaciones y enviar notificaciones push a usuarios segmentados en una aplicación de iOS.</span><span class="sxs-lookup"><span data-stu-id="f49e2-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="f49e2-105">En este tutorial, puede crear una aplicación iOS vacía que recopile datos básicos y reciba notificaciones push mediante el sistema de notificaciones push de Apple (APN).</span><span class="sxs-lookup"><span data-stu-id="f49e2-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="f49e2-106">Este tutorial requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f49e2-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="f49e2-107">XCode 8, que se puede instalar desde la tienda de aplicaciones para Mac</span><span class="sxs-lookup"><span data-stu-id="f49e2-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="f49e2-108">[SDK de iOS para Mobile Engagement]</span><span class="sxs-lookup"><span data-stu-id="f49e2-108">the [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="f49e2-109">Completar este tutorial es un requisito previo para todos los tutoriales de Mobile Engagement para aplicaciones iOS.</span><span class="sxs-lookup"><span data-stu-id="f49e2-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="f49e2-110">Para completar este tutorial, deberá tener una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="f49e2-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="f49e2-111">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="f49e2-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f49e2-112">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="f49e2-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="f49e2-113"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="f49e2-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="f49e2-114"><a id="connecting-app"></a>Conectar la aplicación al backend de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f49e2-114"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="f49e2-115">En este tutorial se presenta una "integración básica", que es el conjunto mínimo necesario para recopilar los datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="f49e2-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="f49e2-116">Toda la información sobre la integración se encuentra en la [Integración del SDK de Mobile Engagement para iOS](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f49e2-116">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="f49e2-117">Crearemos una aplicación básica con XCode para demostrar la integración:</span><span class="sxs-lookup"><span data-stu-id="f49e2-117">We will create a basic app with XCode to demonstrate the integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="f49e2-118">Creación de un nuevo proyecto iOS</span><span class="sxs-lookup"><span data-stu-id="f49e2-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="f49e2-119">Conectar la aplicación al backend de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f49e2-119">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="f49e2-120">Descargue el [SDK de iOS para Mobile Engagement].</span><span class="sxs-lookup"><span data-stu-id="f49e2-120">Download the [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="f49e2-121">Extraiga el archivo .tar.gz en una carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="f49e2-121">Extract the .tar.gz file to a folder in your computer.</span></span>
3. <span data-ttu-id="f49e2-122">Haga clic con el botón derecho en el proyecto y luego seleccione **Agregar archivos a**.</span><span class="sxs-lookup"><span data-stu-id="f49e2-122">Right-click the project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="f49e2-123">Navegue hasta la carpeta en la que extrajo el SDK, seleccione la carpeta `EngagementSDK`, haga clic en **Options** (Opciones) en la esquina inferior izquierda y asegúrese de que tanto la casilla **Copy items if needed** (Copiar elementos si fuera necesario) y la casilla del destino están activadas y presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f49e2-123">Navigate to the folder where you extracted the SDK, select the `EngagementSDK` folder, click **Options** on the bottom left corner and make sure that the checkbox **Copy items if needed** and the checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="f49e2-124">Abra la pestaña **Generar fases** y, en el menú **Vincular binario con bibliotecas**, agregue los marcos de trabajo como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="f49e2-124">Open the **Build Phases** tab, and in the **Link Binary With Libraries** menu, add the frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="f49e2-125">Vuelva al Portal de Azure en la página **Información de conexión** de la aplicación y copie la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="f49e2-125">Go back to the Azure portal in your app's **Connection Info** page and copy the connection string.</span></span>

    ![][4]
7. <span data-ttu-id="f49e2-126">Agregue la siguiente línea de código al archivo **AppDelegate.m** .</span><span class="sxs-lookup"><span data-stu-id="f49e2-126">Add the following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="f49e2-127">Pegue la cadena de conexión en el delegado `didFinishLaunchingWithOptions` .</span><span class="sxs-lookup"><span data-stu-id="f49e2-127">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="f49e2-128">`setTestLogEnabled` es una instrucción opcional que habilita los registros del SDK para identificar problemas.</span><span class="sxs-lookup"><span data-stu-id="f49e2-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you to identify issues.</span></span>

## <span data-ttu-id="f49e2-129"><a id="monitor"></a>Habilitación de la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="f49e2-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="f49e2-130">Para comenzar a enviar datos y asegurarse de que los usuarios estén activos, debe enviar al menos una pantalla (Actividad) al back-end de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f49e2-130">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="f49e2-131">Abra el archivo **ViewController.h** e importe **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="f49e2-131">Open the **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="f49e2-132">Reemplace ahora la superclase de la interfaz de **ViewController** por `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="f49e2-132">Now replace the super class of the **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="f49e2-133"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="f49e2-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="f49e2-134"><a id="integrate-push"></a>Habilitación de las notificaciones push y la mensajería en aplicación</span><span class="sxs-lookup"><span data-stu-id="f49e2-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="f49e2-135">Mobile Engagement permite interactuar y llegar mediante notificaciones push y mensajería en la aplicación en el contexto de las campañas.</span><span class="sxs-lookup"><span data-stu-id="f49e2-135">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="f49e2-136">Este módulo se denomina REACH en el portal de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f49e2-136">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="f49e2-137">En las secciones siguientes se instala la aplicación para recibirlos.</span><span class="sxs-lookup"><span data-stu-id="f49e2-137">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="f49e2-138">Habilitación de la aplicación para recibir notificaciones push silenciosas</span><span class="sxs-lookup"><span data-stu-id="f49e2-138">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="f49e2-139">Adición de la biblioteca de cobertura al proyecto</span><span class="sxs-lookup"><span data-stu-id="f49e2-139">Add the Reach library to your project</span></span>
1. <span data-ttu-id="f49e2-140">Haga clic con el botón derecho en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="f49e2-140">Right-click your project.</span></span>
2. <span data-ttu-id="f49e2-141">Seleccione **Agregar archivo a**.</span><span class="sxs-lookup"><span data-stu-id="f49e2-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="f49e2-142">Navegue hasta la carpeta donde extrajo el SDK.</span><span class="sxs-lookup"><span data-stu-id="f49e2-142">Navigate to the folder where you extracted the SDK.</span></span>
4. <span data-ttu-id="f49e2-143">Seleccione la carpeta `EngagementReach` .</span><span class="sxs-lookup"><span data-stu-id="f49e2-143">Select the `EngagementReach` folder.</span></span>
5. <span data-ttu-id="f49e2-144">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f49e2-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="f49e2-145">Modifique su delegado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f49e2-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="f49e2-146">En el archivo **AppDeletegate.m** , importe el módulo Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="f49e2-146">Back in **AppDeletegate.m** file, import the Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="f49e2-147">Dentro del método `application:didFinishLaunchingWithOptions` , cree un módulo de Reach y páselo a la línea de inicialización de Engagement existente:</span><span class="sxs-lookup"><span data-stu-id="f49e2-147">Inside the `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it to your existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="f49e2-148">Habilite su aplicación para recibir notificaciones push de APN.</span><span class="sxs-lookup"><span data-stu-id="f49e2-148">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="f49e2-149">Agregue la siguiente línea al método `application:didFinishLaunchingWithOptions`:</span><span class="sxs-lookup"><span data-stu-id="f49e2-149">Add the following line to the `application:didFinishLaunchingWithOptions` method:</span></span>

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
2. <span data-ttu-id="f49e2-150">Agregue el método `application:didRegisterForRemoteNotificationsWithDeviceToken` de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="f49e2-150">Add the `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="f49e2-151">Agregue el método `didFailToRegisterForRemoteNotificationsWithError` de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="f49e2-151">Add the `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed to get token, error: %@", error);
        }
4. <span data-ttu-id="f49e2-152">Agregue el método `didReceiveRemoteNotification:fetchCompletionHandler` de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="f49e2-152">Add the `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
<span data-ttu-id="f49e2-153">[SDK de iOS para Mobile Engagement]: http://aka.ms/qk2rnj</span><span class="sxs-lookup"><span data-stu-id="f49e2-153">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
