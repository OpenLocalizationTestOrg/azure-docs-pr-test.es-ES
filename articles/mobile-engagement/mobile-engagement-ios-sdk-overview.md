---
title: "Información general de SDK de iOS de Azure Mobile Engagement | Microsoft Docs"
description: "Actualizaciones y procedimientos más recientes para el SDK de iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 6acd343782a3ee07750e27ec3022ff81cedfadee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="ac7f5-103">SDK de iOS para Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ac7f5-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="ac7f5-104">Comience aquí a obtener todos los detalles sobre cómo integrar Azure Mobile Engagement en una aplicación de iOS.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-104">Start here to get all the details on how to integrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="ac7f5-105">Si primero quiere probarlo, asegúrese de seguir nuestro [tutorial de 15 minutos](mobile-engagement-ios-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="ac7f5-105">If you'd like to give it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="ac7f5-106">Haga clic para ver el [contenido del SDK](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="ac7f5-106">Click to see the [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="ac7f5-107">Procedimientos de integración</span><span class="sxs-lookup"><span data-stu-id="ac7f5-107">Integration procedures</span></span>
1. <span data-ttu-id="ac7f5-108">Comience aquí: [Cómo integrar Mobile Engagement en su aplicación de iOS](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="ac7f5-108">Start here: [How to integrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="ac7f5-109">Para las notificaciones: [Integración de cobertura (notificaciones) en su aplicación iOS](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="ac7f5-109">For Notifications: [How to integrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="ac7f5-110">Implementación del plan de etiquetas: [Uso de la API de etiquetado de Mobile Engagement avanzada en su aplicación iOS](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="ac7f5-110">Tag plan implementation: [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="ac7f5-111">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="ac7f5-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="ac7f5-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="ac7f5-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="ac7f5-113">Se han corregido las notificaciones borradas en el fondo.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="ac7f5-114">Se han corregido las advertencias de XCode 9 sobre las API a las que no se llamaba en cola principal.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="ac7f5-115">Se ha corregido una fuga de memoria en los sondeos de cobertura.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="ac7f5-116">Se ha eliminado el soporte técnico para iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="ac7f5-117">A partir de esta versión, el destino de implementación de la aplicación tiene que ser como mínimo iOS 7.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-117">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="ac7f5-118">Para la versión anterior, consulte las [notas de la versión completas](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="ac7f5-118">For earlier version please see the [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="ac7f5-119">Procedimientos de actualización</span><span class="sxs-lookup"><span data-stu-id="ac7f5-119">Upgrade procedures</span></span>
<span data-ttu-id="ac7f5-120">Si ya integró una versión anterior de Engagement en la aplicación, debería tener en cuenta los siguientes puntos a la hora de actualizar el SDK.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-120">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="ac7f5-121">Es posible que tenga que seguir varios procedimientos si se perdió varias versiones del SDK, consulte la sección completa [Procedimientos de actualización](mobile-engagement-ios-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="ac7f5-121">You may have to follow several procedures if you missed several versions of the SDK see the complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="ac7f5-122">Para cada nueva versión del SDK debe reemplazar primero (quitar y volver a importar en xcode) las carpetas EngagementSDK y EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-122">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-to-400"></a><span data-ttu-id="ac7f5-123">De 3.0.0 a 4.0.0</span><span class="sxs-lookup"><span data-stu-id="ac7f5-123">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="ac7f5-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="ac7f5-124">XCode 8</span></span>
<span data-ttu-id="ac7f5-125">XCode 8 es obligatorio a partir de la versión 4.0.0 del SDK.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-125">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="ac7f5-126">Si realmente depende de XCode 7, puede usar el [SDK v3.2.4 de Engagement para iOS](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="ac7f5-126">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="ac7f5-127">Existe un problema conocido en el módulo de cobertura de esta versión anterior cuando se ejecuta en dispositivos iOS 10: las notificaciones del sistema no se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-127">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="ac7f5-128">Para solucionarlo, tendrá que implementar la API `application:didReceiveRemoteNotification:` en desuso en su delegado de aplicación de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac7f5-128">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="ac7f5-129">**No se recomienda esta solución** ya que este comportamiento puede cambiar en la próxima actualización de la versión de iOS (por menor que sea) porque esta API de iOS está en desuso.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="ac7f5-130">Debe cambiar a XCode 8 tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-130">You should switch to XCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="ac7f5-131">Marco de UserNotifications</span><span class="sxs-lookup"><span data-stu-id="ac7f5-131">UserNotifications framework</span></span>
<span data-ttu-id="ac7f5-132">Debe agregar el marco `UserNotifications` en sus fases de compilación.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-132">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="ac7f5-133">En el Explorador de proyectos, abra su panel de proyectos y seleccione el destino adecuado.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-133">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="ac7f5-134">A continuación, abra la pestaña **"Build phases"** (Fases de compilación) y en el menú **"Link Binary With Libraries"** (Vincular binarios con bibliotecas), agregue el marco `UserNotifications.framework` y establezca el vínculo como `Optional`.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-134">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="ac7f5-135">Funcionalidad de inserción de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ac7f5-135">Application push capability</span></span>
<span data-ttu-id="ac7f5-136">XCode 8 puede restablecer la funcionalidad de inserción de su aplicación, solo tiene que marcarla dos veces en la pestaña `capability` del destino seleccionado.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-136">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

#### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="ac7f5-137">Adición del nuevo código de registro de notificaciones de iOS 10</span><span class="sxs-lookup"><span data-stu-id="ac7f5-137">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="ac7f5-138">El fragmento de código anterior para registrar la aplicación para las notificaciones aún funciona, pero está utilizando API obsoletas mientras se ejecuta en iOS 10.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-138">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="ac7f5-139">Importe la plataforma `User Notification` :</span><span class="sxs-lookup"><span data-stu-id="ac7f5-139">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="ac7f5-140">En el método de delegado de aplicación `application:didFinishLaunchingWithOptions` reemplace:</span><span class="sxs-lookup"><span data-stu-id="ac7f5-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="ac7f5-141">por:</span><span class="sxs-lookup"><span data-stu-id="ac7f5-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="ac7f5-142">Resolución de conflictos de delegado de UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="ac7f5-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="ac7f5-143">*Si ni la aplicación ni una de las bibliotecas de terceros implementa `UNUserNotificationCenterDelegate`, puede pasar por alto esta parte.*</span><span class="sxs-lookup"><span data-stu-id="ac7f5-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="ac7f5-144">El SDK usa un delegado de `UNUserNotificationCenter` para supervisar el ciclo de vida de las notificaciones de Engagement en dispositivos que se ejecutan en iOS 10 o superior.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-144">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="ac7f5-145">El SDK tiene su propia implementación del protocolo `UNUserNotificationCenterDelegate`, pero solo puede haber un delegado de `UNUserNotificationCenter` por aplicación.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-145">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="ac7f5-146">Cualquier otro delegado que se agrega al objeto `UNUserNotificationCenter` entrará en conflicto con Engagement.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-146">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="ac7f5-147">Si el SDK detecta su delegado o cualquier otro de terceros, no usará su propia implementación para ofrecerle una oportunidad de resolver los conflictos.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-147">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="ac7f5-148">Tendrá que agregar la lógica de Engagement a su propio delegado con el fin de resolver los conflictos.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-148">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="ac7f5-149">Hay dos formas de hacerlo:</span><span class="sxs-lookup"><span data-stu-id="ac7f5-149">There are two ways to achieve this.</span></span>

<span data-ttu-id="ac7f5-150">Propuesta 1: reenviar las llamadas del delegado al SDK:</span><span class="sxs-lookup"><span data-stu-id="ac7f5-150">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

<span data-ttu-id="ac7f5-151">O propuesta 2: heredándola de la clase `AEUserNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-151">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> <span data-ttu-id="ac7f5-152">Puede determinar si una notificación proviene de Engagement o no pasando su diccionario `userInfo` al método de clase `isEngagementPushPayload:` del agente.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="ac7f5-153">Asegúrese de que el delegado del objeto `UNUserNotificationCenter` se establece en su delegado en los métodos `application:willFinishLaunchingWithOptions:` o `application:didFinishLaunchingWithOptions:` del delegado de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ac7f5-153">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="ac7f5-154">Por ejemplo, si implementa la propuesta anterior 1:</span><span class="sxs-lookup"><span data-stu-id="ac7f5-154">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
