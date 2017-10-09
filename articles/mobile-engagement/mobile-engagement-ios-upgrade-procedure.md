---
title: "aaaAzure el procedimiento de actualización de SDK de Mobile Engagement iOS | Documentos de Microsoft"
description: "Actualizaciones y procedimientos más recientes para el SDK de iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="2cc5c-103">Procedimientos de actualización</span><span class="sxs-lookup"><span data-stu-id="2cc5c-103">Upgrade procedures</span></span>
<span data-ttu-id="2cc5c-104">Si ya ha integrado una versión anterior de interacción en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="2cc5c-105">Para cada nueva versión de hello SDK debe reemplazar primero (quitar y volver a importar en xcode) Hola carpetas EngagementSDK y EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-105">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="2cc5c-106">Desde 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="2cc5c-106">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="2cc5c-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="2cc5c-107">XCode 8</span></span>
<span data-ttu-id="2cc5c-108">XCode 8 es obligatorio a partir de la versión 4.0.0 de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-108">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="2cc5c-109">Si realmente dependen XCode 7, a continuación, puede usar hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="2cc5c-109">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="2cc5c-110">Hay un problema conocido en el módulo de reach Hola de esta versión anterior mientras se ejecuta en dispositivos iOS 10: las notificaciones del sistema no están activadas.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-110">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="2cc5c-111">toofix esto tendrá tooimplement hello en desuso API `application:didReceiveRemoteNotification:` en la aplicación el delegado como sigue:</span><span class="sxs-lookup"><span data-stu-id="2cc5c-111">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="2cc5c-112">**No se recomienda esta solución** ya que este comportamiento puede cambiar en la próxima actualización de la versión de iOS (por menor que sea) porque esta API de iOS está en desuso.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="2cc5c-113">Debería pasar tooXCode 8 tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-113">You should switch tooXCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="2cc5c-114">Marco de UserNotifications</span><span class="sxs-lookup"><span data-stu-id="2cc5c-114">UserNotifications framework</span></span>
<span data-ttu-id="2cc5c-115">Necesita tooadd hello `UserNotifications` framework en fases de compilación.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-115">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="2cc5c-116">en el Explorador de proyectos hello, abra el panel de proyecto y seleccione destino correcto Hola.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-116">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="2cc5c-117">A continuación, abra hello **"Fases de compilación"** ficha y Hola **"Binario con bibliotecas de vínculos"** menú, agregue framework `UserNotifications.framework` -establecer Hola vínculo como`Optional`</span><span class="sxs-lookup"><span data-stu-id="2cc5c-117">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="2cc5c-118">Funcionalidad de inserción de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2cc5c-118">Application push capability</span></span>
<span data-ttu-id="2cc5c-119">XCode 8 puede restablecer la aplicación capacidad de inserción, compruébela en hello `capability` ficha de su destino seleccionado.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-119">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="2cc5c-120">Agregar código de registro de hello nueva iOS notificación 10</span><span class="sxs-lookup"><span data-stu-id="2cc5c-120">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="2cc5c-121">Hola anteriores código fragmento tooregister aplicación hello toonotifications todavía funciona, pero está usando en desuso API mientras se ejecuta en iOS 10.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-121">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="2cc5c-122">Hola de importación `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="2cc5c-122">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="2cc5c-123">En el método de delegado de aplicación `application:didFinishLaunchingWithOptions` reemplace:</span><span class="sxs-lookup"><span data-stu-id="2cc5c-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="2cc5c-124">por:</span><span class="sxs-lookup"><span data-stu-id="2cc5c-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="2cc5c-125">Resolución de conflictos de delegado de UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="2cc5c-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="2cc5c-126">*Si ni la aplicación ni una de las bibliotecas de terceros implementa `UNUserNotificationCenterDelegate`, puede pasar por alto esta parte.*</span><span class="sxs-lookup"><span data-stu-id="2cc5c-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="2cc5c-127">Un `UNUserNotificationCenter` delegado es utilizado por el ciclo de vida de hello SDK toomonitor Hola de notificaciones de interacción en dispositivos que ejecutan en iOS 10 o superior.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-127">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="2cc5c-128">Hola SDK tiene su propia implementación de hello `UNUserNotificationCenterDelegate` de protocolo, pero puede haber solo un `UNUserNotificationCenter` delegar por aplicación.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-128">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="2cc5c-129">Cualquier otro delegado agrega toohello `UNUserNotificationCenter` objeto entrarán en conflicto con hello interacción uno.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-129">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="2cc5c-130">Si Hola SDK detecta a delegado su o cualquier otro de terceros no usará su propio toogive de implementación, una posibilidad tooresolve Hola conflictos.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-130">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="2cc5c-131">Tendrá tooadd Hola interacción lógica tooyour posee conflictos de hello tooresolve de delegado en orden.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-131">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="2cc5c-132">Hay dos tooachieve formas esto.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-132">There are two ways tooachieve this.</span></span>

<span data-ttu-id="2cc5c-133">Propuesta 1, enviando el delegado llama toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="2cc5c-133">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="2cc5c-134">O propuesta 2, heredando de hello `AEUserNotificationHandler` (clase)</span><span class="sxs-lookup"><span data-stu-id="2cc5c-134">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="2cc5c-135">Puede determinar si una notificación pueden proceder de contratación o no pasando su `userInfo` diccionario toohello agente `isEngagementPushPayload:` método de la clase.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="2cc5c-136">Asegúrese de que ese hello `UNUserNotificationCenter` delegado del objeto se establece el delegado tooyour dentro de cualquier hello `application:willFinishLaunchingWithOptions:` o hello `application:didFinishLaunchingWithOptions:` método de delegado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-136">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="2cc5c-137">Por ejemplo, si implementa Hola anteriormente propuesta 1:</span><span class="sxs-lookup"><span data-stu-id="2cc5c-137">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a><span data-ttu-id="2cc5c-138">Desde 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="2cc5c-138">From 2.0.0 too3.0.0</span></span>
<span data-ttu-id="2cc5c-139">Soporte de iOS 4.X eliminado.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="2cc5c-140">A partir de este destino de implementación de Hola de versión de la aplicación debe tener como mínimo iOS 6.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-140">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="2cc5c-141">Si está utilizando el alcance de la aplicación, debe agregar `remote-notification` toohello valor `UIBackgroundModes` matriz en el archivo Info.plist en las notificaciones de orden tooreceive remoto.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-141">If you are using Reach in your application, you must add `remote-notification` value toohello `UIBackgroundModes` array in your Info.plist file in order tooreceive remote notifications.</span></span>

<span data-ttu-id="2cc5c-142">Hola método `application:didReceiveRemoteNotification:` necesita toobe reemplazado por `application:didReceiveRemoteNotification:fetchCompletionHandler:` en el delegado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-142">hello method `application:didReceiveRemoteNotification:` needs toobe replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="2cc5c-143">"AEPushDelegate.h" está en desuso interfaz y necesita tooremove todas las referencias.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-143">"AEPushDelegate.h" is deprecated interface and you need tooremove all references.</span></span> <span data-ttu-id="2cc5c-144">Esto incluye la eliminación `[[EngagementAgent shared] setPushDelegate:self]` y Hola delegar métodos desde el delegado de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="2cc5c-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and hello delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a><span data-ttu-id="2cc5c-145">De 1.16.0 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="2cc5c-145">From 1.16.0 too2.0.0</span></span>
<span data-ttu-id="2cc5c-146">Hello siguiente describe cómo toomigrate una integración con el SDK de hello Capptain servicio ofrecido por Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-146">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="2cc5c-147">Si va a migrar desde una versión anterior, por favor, consulte hello Capptain sitio web toomigrate too1.16 en primer lugar, aplique Hola siguiendo el procedimiento.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-147">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.16 first then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cc5c-148">Capptain e interacción móvil no se Hola los mismos servicios y procedimiento Hola indicado a continuación sólo resalta cómo toomigrate Hola aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-148">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="2cc5c-149">Migrar Hola SDK en la aplicación hello no migrará los datos de hello Capptain toohello Mobile Engagement servidores</span><span class="sxs-lookup"><span data-stu-id="2cc5c-149">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="2cc5c-150">Agente</span><span class="sxs-lookup"><span data-stu-id="2cc5c-150">Agent</span></span>
<span data-ttu-id="2cc5c-151">Hola método `registerApp:` se ha reemplazado por el nuevo método de hello `init:`.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-151">hello method `registerApp:` has been replaced by hello new method `init:`.</span></span> <span data-ttu-id="2cc5c-152">El delegado de la aplicación deben actualizarse como corresponda y usar una cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="2cc5c-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="2cc5c-153">Seguimiento de SmartAd se ha quitado del SDK sólo tiene tooremove todas las instancias de `AETrackModule` (clase)</span><span class="sxs-lookup"><span data-stu-id="2cc5c-153">SmartAd tracking has been removed from SDK you just have tooremove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="2cc5c-154">Cambios del nombre de la clase</span><span class="sxs-lookup"><span data-stu-id="2cc5c-154">Class Name Changes</span></span>
<span data-ttu-id="2cc5c-155">Como parte de la reconfiguración de marca de hello, hay par clase/de nombres de archivo que necesitan toobe cambiado.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-155">As part of hello rebranding, there are couple of class/file names that need toobe changed.</span></span>

<span data-ttu-id="2cc5c-156">Todas las clases precedidas de "CP" cambian su nombre introduciendo el prefijo "AE".</span><span class="sxs-lookup"><span data-stu-id="2cc5c-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="2cc5c-157">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2cc5c-157">Example:</span></span>

* <span data-ttu-id="2cc5c-158">`CPModule.h`se cambia el nombre demasiado`AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-158">`CPModule.h` is renamed too`AEModule.h`.</span></span>

<span data-ttu-id="2cc5c-159">Todas las clases con el prefijo "Capptain" cambian su nombre para introducir el prefijo "Engagement".</span><span class="sxs-lookup"><span data-stu-id="2cc5c-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="2cc5c-160">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="2cc5c-160">Examples:</span></span>

* <span data-ttu-id="2cc5c-161">Hola clase `CapptainAgent` se cambia el nombre demasiado`EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-161">hello class `CapptainAgent` is renamed too`EngagementAgent`.</span></span>
* <span data-ttu-id="2cc5c-162">Hola clase `CapptainTableViewController` se cambia el nombre demasiado`EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-162">hello class `CapptainTableViewController` is renamed too`EngagementTableViewController`.</span></span>
* <span data-ttu-id="2cc5c-163">Hola clase `CapptainUtils` se cambia el nombre demasiado`EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-163">hello class `CapptainUtils` is renamed too`EngagementUtils`.</span></span>
* <span data-ttu-id="2cc5c-164">Hola clase `CapptainViewController` se cambia el nombre demasiado`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="2cc5c-164">hello class `CapptainViewController` is renamed too`EngagementViewController`.</span></span>

