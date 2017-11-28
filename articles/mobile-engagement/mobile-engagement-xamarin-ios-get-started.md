---
title: aaaGet Started with Azure Mobile Engagement para Xamarin.iOS
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con las notificaciones de inserción para las aplicaciones de Xamarin.iOS y análisis."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="faa6e-103">Introducción a Azure Mobile Engagement para aplicaciones Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="faa6e-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="faa6e-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de aplicaciones y el envío de inserción a los usuarios de las notificaciones toosegmented en una aplicación de Xamarin.iOS.</span><span class="sxs-lookup"><span data-stu-id="faa6e-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="faa6e-105">En este tutorial, puede crear una aplicación Xamarin.iOS vacía que recopile datos básicos y reciba notificaciones push mediante el Sistema de notificaciones push de Apple (APNS).</span><span class="sxs-lookup"><span data-stu-id="faa6e-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="faa6e-106">servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible.</span><span class="sxs-lookup"><span data-stu-id="faa6e-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="faa6e-107">Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="faa6e-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="faa6e-108">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="faa6e-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="faa6e-109">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="faa6e-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="faa6e-110">También puede utilizar Visual Studio con Xamarin, pero en este tutorial se usa Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="faa6e-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="faa6e-111">Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx)para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="faa6e-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="faa6e-112">SDK de Mobile Engagement Xamarin</span><span class="sxs-lookup"><span data-stu-id="faa6e-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="faa6e-113">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="faa6e-113">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="faa6e-114">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="faa6e-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="faa6e-115">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="faa6e-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="faa6e-116"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="faa6e-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="faa6e-117"><a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="faa6e-117"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="faa6e-118">Este tutorial presenta una "integración básica de" hello mínimo establecido toocollect requiere datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="faa6e-118">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span>

<span data-ttu-id="faa6e-119">Se creará una aplicación básica con la integración de hello toodemonstrate de Xamarin:</span><span class="sxs-lookup"><span data-stu-id="faa6e-119">We will create a basic app with Xamarin toodemonstrate hello integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="faa6e-120">Creación de un nuevo proyecto de Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="faa6e-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="faa6e-121">Inicie Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="faa6e-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="faa6e-122">Vaya demasiado**archivo** -> **New** -> **solución**</span><span class="sxs-lookup"><span data-stu-id="faa6e-122">Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="faa6e-123">Seleccione **ver solo la aplicación**, asegúrese de que el idioma Hola seleccionado es **C#** y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="faa6e-123">Select **Single View App**, make sure hello selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="faa6e-124">Rellene hello **nombre de la aplicación** hello y **identificador de la organización** y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="faa6e-124">Fill in hello **App Name** and hello **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="faa6e-125">Asegúrese de que ese Hola finalmente use toodeploy que su aplicación iOS está usando un identificador de aplicación que coincida con exactamente con hello aquí tiene el identificador de paquete de perfil de publicación.</span><span class="sxs-lookup"><span data-stu-id="faa6e-125">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using an App ID which matches exactly with hello Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="faa6e-126">Hola de actualización **nombre del proyecto**, **nombre de la solución** y **ubicación** si es necesario y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="faa6e-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="faa6e-127">Xamarin Studio creará la aplicación de demostración de hello en el que se integrará Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="faa6e-127">Xamarin Studio will create hello demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="faa6e-128">Conectar el backend de interacción de tooMobile de aplicación</span><span class="sxs-lookup"><span data-stu-id="faa6e-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="faa6e-129">Haga clic en hello **paquetes** carpeta de windows de la solución de Hola y seleccione **agregar paquetes...**</span><span class="sxs-lookup"><span data-stu-id="faa6e-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="faa6e-130">Busque hello **Xamarin SDK de Microsoft Azure Mobile Engagement** y agregar soluciones tooyour.</span><span class="sxs-lookup"><span data-stu-id="faa6e-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="faa6e-131">Abra **AppDelegate.cs** y agregue Hola siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="faa6e-131">Open **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="faa6e-132">Hola **FinishedLaunching** método, agregue Hola después de la conexión de hello tooinitialize con Mobile Engagement back-end.</span><span class="sxs-lookup"><span data-stu-id="faa6e-132">In hello **FinishedLaunching** method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="faa6e-133">Asegúrese de que tooadd su **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="faa6e-133">Make sure tooadd your **ConnectionString**.</span></span> <span data-ttu-id="faa6e-134">Este código también usa un ficticia **NotificationIcon** que se agrega de forma Hola SDK de Mobile Engagement que puede que desee tooreplace.</span><span class="sxs-lookup"><span data-stu-id="faa6e-134">This code also uses a dummy **NotificationIcon** which is added by hello Mobile Engagement SDK which you may want tooreplace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="faa6e-135"><a id="monitor"></a>Habilitar supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="faa6e-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="faa6e-136">En orden toostart enviando los datos y asegurarse de que los usuarios de hello están activos, debe enviar al menos una pantalla toohello Mobile Engagement back-end.</span><span class="sxs-lookup"><span data-stu-id="faa6e-136">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="faa6e-137">Abra **ViewController.cs** y agregue Hola siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="faa6e-137">Open **ViewController.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="faa6e-138">Reemplace la clase hello desde el que `ViewController` hereda de `UIViewController` demasiado`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="faa6e-138">Replace hello class from which `ViewController` inherits from `UIViewController` too`EngagementViewController`.</span></span> 

## <span data-ttu-id="faa6e-139"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="faa6e-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="faa6e-140"><a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="faa6e-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="faa6e-141">Mobile Engagement le permite toointeract con los usuarios y alcance con notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas.</span><span class="sxs-lookup"><span data-stu-id="faa6e-141">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="faa6e-142">Este módulo se denomina alcance en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="faa6e-142">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="faa6e-143">Hello las secciones siguientes configure su aplicación tooreceive ellos.</span><span class="sxs-lookup"><span data-stu-id="faa6e-143">hello following sections set up your app tooreceive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="faa6e-144">Modifique su delegado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="faa6e-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="faa6e-145">Hola abierto **AppDelegate.cs** y agregue Hola siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="faa6e-145">Open hello **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="faa6e-146">Ahora dentro de hello `FinishedLaunching` método hello después tooregister para los mensajes de inserción después de agregar`EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="faa6e-146">Now inside hello `FinishedLaunching` method, add hello following tooregister for push messages after `EngagementAgent.init(...)`</span></span>
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. <span data-ttu-id="faa6e-147">Por último - actualizar o agregar Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="faa6e-147">Finally - update or add hello following methods:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="faa6e-148">En su **Info.plist** de archivos de solución de hello, confirme que hello **identificador de paquete** coincide con hello **Id. de aplicación** tiene en su perfil de aprovisionamiento en hello Dev de Apple Centro.</span><span class="sxs-lookup"><span data-stu-id="faa6e-148">In your **Info.plist** file in hello solution, confirm that hello **Bundle Identifier** matches with hello **App ID** you have in your provisioning profile in hello Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="faa6e-149">En Hola mismo **Info.plist** de archivos, asegúrese de que ha activado hello **habilitar modos en segundo plano** y **notificaciones remoto**.</span><span class="sxs-lookup"><span data-stu-id="faa6e-149">In hello same **Info.plist** file, make sure that you have checked hello **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="faa6e-150">Ejecutar la aplicación hello en dispositivo Hola que se ha asociado con este perfil de publicación.</span><span class="sxs-lookup"><span data-stu-id="faa6e-150">Run hello app on hello device you have associated with this publishing profile.</span></span> 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
