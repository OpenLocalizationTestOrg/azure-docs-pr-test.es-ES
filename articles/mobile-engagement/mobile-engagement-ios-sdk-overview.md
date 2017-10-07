---
title: "información general del SDK de Mobile Engagement iOS aaaAzure | Documentos de Microsoft"
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
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="0cf3e-103">SDK de iOS para Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="0cf3e-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="0cf3e-104">Iniciar todos los detalles de Hola de aquí tooget acerca de cómo toointegrate Azure Mobile Engagement en una aplicación de iOS.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-104">Start here tooget all hello details on how toointegrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="0cf3e-105">Si desea que toogive que un bloque try en primer lugar, asegúrese de que no nuestro [tutorial de 15 minutos](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0cf3e-105">If you'd like toogive it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="0cf3e-106">Haga clic en hello toosee [contenido de SDK](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="0cf3e-106">Click toosee hello [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="0cf3e-107">Procedimientos de integración</span><span class="sxs-lookup"><span data-stu-id="0cf3e-107">Integration procedures</span></span>
1. <span data-ttu-id="0cf3e-108">Empiece aquí: [cómo toointegrate Mobile Engagement en la aplicación de iOS](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="0cf3e-108">Start here: [How toointegrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="0cf3e-109">Para las notificaciones: [cómo toointegrate alcance (notificaciones) en la aplicación de iOS](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="0cf3e-109">For Notifications: [How toointegrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="0cf3e-110">Implementación del plan de etiqueta: [cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación iOS](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="0cf3e-110">Tag plan implementation: [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="0cf3e-111">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="0cf3e-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="0cf3e-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="0cf3e-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="0cf3e-113">Se han corregido las notificaciones borradas en el fondo.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="0cf3e-114">Se han corregido las advertencias de XCode 9 sobre las API a las que no se llamaba en cola principal.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="0cf3e-115">Se ha corregido una fuga de memoria en los sondeos de cobertura.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="0cf3e-116">Se ha eliminado el soporte técnico para iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="0cf3e-117">A partir de este destino de implementación de Hola de versión de la aplicación debe tener como mínimo iOS 7.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-117">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="0cf3e-118">Para la versión anterior, consulte hello [completar notas de la versión](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="0cf3e-118">For earlier version please see hello [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="0cf3e-119">Procedimientos de actualización</span><span class="sxs-lookup"><span data-stu-id="0cf3e-119">Upgrade procedures</span></span>
<span data-ttu-id="0cf3e-120">Si ya ha integrado una versión anterior de interacción en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-120">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="0cf3e-121">Puede tener a toofollow varios procedimientos si ejecutado varias versiones de hello SDK vea Hola completa [procedimientos de actualización de](mobile-engagement-ios-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="0cf3e-121">You may have toofollow several procedures if you missed several versions of hello SDK see hello complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="0cf3e-122">Para cada nueva versión de hello SDK debe reemplazar primero (quitar y volver a importar en xcode) Hola carpetas EngagementSDK y EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-122">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-too400"></a><span data-ttu-id="0cf3e-123">Desde 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="0cf3e-123">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="0cf3e-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="0cf3e-124">XCode 8</span></span>
<span data-ttu-id="0cf3e-125">XCode 8 es obligatorio a partir de la versión 4.0.0 de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-125">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="0cf3e-126">Si realmente dependen XCode 7, a continuación, puede usar hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="0cf3e-126">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="0cf3e-127">Hay un problema conocido en el módulo de reach Hola de esta versión anterior mientras se ejecuta en dispositivos iOS 10: las notificaciones del sistema no están activadas.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-127">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="0cf3e-128">toofix esto tendrá tooimplement hello en desuso API `application:didReceiveRemoteNotification:` en la aplicación el delegado como sigue:</span><span class="sxs-lookup"><span data-stu-id="0cf3e-128">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="0cf3e-129">**No se recomienda esta solución** ya que este comportamiento puede cambiar en la próxima actualización de la versión de iOS (por menor que sea) porque esta API de iOS está en desuso.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="0cf3e-130">Debería pasar tooXCode 8 tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-130">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="0cf3e-131">Marco de UserNotifications</span><span class="sxs-lookup"><span data-stu-id="0cf3e-131">UserNotifications framework</span></span>
<span data-ttu-id="0cf3e-132">Necesita tooadd hello `UserNotifications` framework en fases de compilación.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-132">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="0cf3e-133">en el Explorador de proyectos hello, abra el panel de proyecto y seleccione destino correcto Hola.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-133">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="0cf3e-134">A continuación, abra hello **"Fases de compilación"** ficha y Hola **"Binario con bibliotecas de vínculos"** menú, agregue framework `UserNotifications.framework` -establecer Hola vínculo como`Optional`</span><span class="sxs-lookup"><span data-stu-id="0cf3e-134">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="0cf3e-135">Funcionalidad de inserción de la aplicación</span><span class="sxs-lookup"><span data-stu-id="0cf3e-135">Application push capability</span></span>
<span data-ttu-id="0cf3e-136">XCode 8 puede restablecer la aplicación capacidad de inserción, compruébela en hello `capability` ficha de su destino seleccionado.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-136">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

#### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="0cf3e-137">Agregar código de registro de hello nueva iOS notificación 10</span><span class="sxs-lookup"><span data-stu-id="0cf3e-137">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="0cf3e-138">Hola anteriores código fragmento tooregister aplicación hello toonotifications todavía funciona, pero está usando en desuso API mientras se ejecuta en iOS 10.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-138">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="0cf3e-139">Hola de importación `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="0cf3e-139">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="0cf3e-140">En el método de delegado de aplicación `application:didFinishLaunchingWithOptions` reemplace:</span><span class="sxs-lookup"><span data-stu-id="0cf3e-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="0cf3e-141">por:</span><span class="sxs-lookup"><span data-stu-id="0cf3e-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="0cf3e-142">Resolución de conflictos de delegado de UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="0cf3e-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="0cf3e-143">*Si ni la aplicación ni una de las bibliotecas de terceros implementa `UNUserNotificationCenterDelegate`, puede pasar por alto esta parte.*</span><span class="sxs-lookup"><span data-stu-id="0cf3e-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="0cf3e-144">Un `UNUserNotificationCenter` delegado es utilizado por el ciclo de vida de hello SDK toomonitor Hola de notificaciones de interacción en dispositivos que ejecutan en iOS 10 o superior.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-144">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="0cf3e-145">Hola SDK tiene su propia implementación de hello `UNUserNotificationCenterDelegate` de protocolo, pero puede haber solo un `UNUserNotificationCenter` delegar por aplicación.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-145">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="0cf3e-146">Cualquier otro delegado agrega toohello `UNUserNotificationCenter` objeto entrarán en conflicto con hello interacción uno.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-146">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="0cf3e-147">Si Hola SDK detecta a delegado su o cualquier otro de terceros no usará su propio toogive de implementación, una posibilidad tooresolve Hola conflictos.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-147">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="0cf3e-148">Tendrá tooadd Hola interacción lógica tooyour posee conflictos de hello tooresolve de delegado en orden.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-148">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="0cf3e-149">Hay dos tooachieve formas esto.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-149">There are two ways tooachieve this.</span></span>

<span data-ttu-id="0cf3e-150">Propuesta 1, enviando el delegado llama toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="0cf3e-150">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="0cf3e-151">O propuesta 2, heredando de hello `AEUserNotificationHandler` (clase)</span><span class="sxs-lookup"><span data-stu-id="0cf3e-151">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="0cf3e-152">Puede determinar si una notificación pueden proceder de contratación o no pasando su `userInfo` diccionario toohello agente `isEngagementPushPayload:` método de la clase.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="0cf3e-153">Asegúrese de que ese hello `UNUserNotificationCenter` delegado del objeto se establece el delegado tooyour dentro de cualquier hello `application:willFinishLaunchingWithOptions:` o hello `application:didFinishLaunchingWithOptions:` método de delegado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0cf3e-153">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="0cf3e-154">Por ejemplo, si implementa Hola anteriormente propuesta 1:</span><span class="sxs-lookup"><span data-stu-id="0cf3e-154">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
