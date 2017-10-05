---
title: "Procedimiento de actualización del SDK de iOS de Azure Mobile Engagement | Microsoft Docs"
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
ms.openlocfilehash: 37c7f133d079186f828d58cabce0d2a259efd085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="86e2b-103">Procedimientos de actualización</span><span class="sxs-lookup"><span data-stu-id="86e2b-103">Upgrade procedures</span></span>
<span data-ttu-id="86e2b-104">Si ya integró una versión anterior de Engagement en la aplicación, debería tener en cuenta los siguientes puntos a la hora de actualizar el SDK.</span><span class="sxs-lookup"><span data-stu-id="86e2b-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="86e2b-105">Para cada nueva versión del SDK debe reemplazar primero (quitar y volver a importar en xcode) las carpetas EngagementSDK y EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="86e2b-105">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="86e2b-106">De 3.0.0 a 4.0.0</span><span class="sxs-lookup"><span data-stu-id="86e2b-106">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="86e2b-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="86e2b-107">XCode 8</span></span>
<span data-ttu-id="86e2b-108">XCode 8 es obligatorio a partir de la versión 4.0.0 del SDK.</span><span class="sxs-lookup"><span data-stu-id="86e2b-108">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="86e2b-109">Si realmente depende de XCode 7, puede usar el [SDK v3.2.4 de Engagement para iOS](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="86e2b-109">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="86e2b-110">Existe un problema conocido en el módulo de cobertura de esta versión anterior cuando se ejecuta en dispositivos iOS 10: las notificaciones del sistema no se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="86e2b-110">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="86e2b-111">Para solucionarlo, tendrá que implementar la API `application:didReceiveRemoteNotification:` en desuso en su delegado de aplicación de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="86e2b-111">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="86e2b-112">**No se recomienda esta solución** ya que este comportamiento puede cambiar en la próxima actualización de la versión de iOS (por menor que sea) porque esta API de iOS está en desuso.</span><span class="sxs-lookup"><span data-stu-id="86e2b-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="86e2b-113">Debe cambiar a XCode 8 tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="86e2b-113">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="86e2b-114">Marco de UserNotifications</span><span class="sxs-lookup"><span data-stu-id="86e2b-114">UserNotifications framework</span></span>
<span data-ttu-id="86e2b-115">Debe agregar el marco `UserNotifications` en sus fases de compilación.</span><span class="sxs-lookup"><span data-stu-id="86e2b-115">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="86e2b-116">En el Explorador de proyectos, abra su panel de proyectos y seleccione el destino adecuado.</span><span class="sxs-lookup"><span data-stu-id="86e2b-116">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="86e2b-117">A continuación, abra la pestaña **"Build phases"** (Fases de compilación) y en el menú **"Link Binary With Libraries"** (Vincular binarios con bibliotecas), agregue el marco `UserNotifications.framework` y establezca el vínculo como `Optional`.</span><span class="sxs-lookup"><span data-stu-id="86e2b-117">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="86e2b-118">Funcionalidad de inserción de la aplicación</span><span class="sxs-lookup"><span data-stu-id="86e2b-118">Application push capability</span></span>
<span data-ttu-id="86e2b-119">XCode 8 puede restablecer la funcionalidad de inserción de su aplicación, solo tiene que marcarla dos veces en la pestaña `capability` del destino seleccionado.</span><span class="sxs-lookup"><span data-stu-id="86e2b-119">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="86e2b-120">Adición del nuevo código de registro de notificaciones de iOS 10</span><span class="sxs-lookup"><span data-stu-id="86e2b-120">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="86e2b-121">El fragmento de código anterior para registrar la aplicación para las notificaciones aún funciona, pero está utilizando API obsoletas mientras se ejecuta en iOS 10.</span><span class="sxs-lookup"><span data-stu-id="86e2b-121">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="86e2b-122">Importe la plataforma `User Notification` :</span><span class="sxs-lookup"><span data-stu-id="86e2b-122">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="86e2b-123">En el método de delegado de aplicación `application:didFinishLaunchingWithOptions` reemplace:</span><span class="sxs-lookup"><span data-stu-id="86e2b-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="86e2b-124">por:</span><span class="sxs-lookup"><span data-stu-id="86e2b-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="86e2b-125">Resolución de conflictos de delegado de UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="86e2b-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="86e2b-126">*Si ni la aplicación ni una de las bibliotecas de terceros implementa `UNUserNotificationCenterDelegate`, puede pasar por alto esta parte.*</span><span class="sxs-lookup"><span data-stu-id="86e2b-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="86e2b-127">El SDK usa un delegado de `UNUserNotificationCenter` para supervisar el ciclo de vida de las notificaciones de Engagement en dispositivos que se ejecutan en iOS 10 o superior.</span><span class="sxs-lookup"><span data-stu-id="86e2b-127">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="86e2b-128">El SDK tiene su propia implementación del protocolo `UNUserNotificationCenterDelegate`, pero solo puede haber un delegado de `UNUserNotificationCenter` por aplicación.</span><span class="sxs-lookup"><span data-stu-id="86e2b-128">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="86e2b-129">Cualquier otro delegado que se agrega al objeto `UNUserNotificationCenter` entrará en conflicto con Engagement.</span><span class="sxs-lookup"><span data-stu-id="86e2b-129">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="86e2b-130">Si el SDK detecta su delegado o cualquier otro de terceros, no usará su propia implementación para ofrecerle una oportunidad de resolver los conflictos.</span><span class="sxs-lookup"><span data-stu-id="86e2b-130">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="86e2b-131">Tendrá que agregar la lógica de Engagement a su propio delegado con el fin de resolver los conflictos.</span><span class="sxs-lookup"><span data-stu-id="86e2b-131">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="86e2b-132">Hay dos formas de hacerlo:</span><span class="sxs-lookup"><span data-stu-id="86e2b-132">There are two ways to achieve this.</span></span>

<span data-ttu-id="86e2b-133">Propuesta 1: reenviar las llamadas del delegado al SDK:</span><span class="sxs-lookup"><span data-stu-id="86e2b-133">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="86e2b-134">O propuesta 2: heredándola de la clase `AEUserNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="86e2b-134">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="86e2b-135">Puede determinar si una notificación proviene de Engagement o no pasando su diccionario `userInfo` al método de clase `isEngagementPushPayload:` del agente.</span><span class="sxs-lookup"><span data-stu-id="86e2b-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="86e2b-136">Asegúrese de que el delegado del objeto `UNUserNotificationCenter` se establece en su delegado en los métodos `application:willFinishLaunchingWithOptions:` o `application:didFinishLaunchingWithOptions:` del delegado de aplicación.</span><span class="sxs-lookup"><span data-stu-id="86e2b-136">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="86e2b-137">Por ejemplo, si implementa la propuesta anterior 1:</span><span class="sxs-lookup"><span data-stu-id="86e2b-137">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-to-300"></a><span data-ttu-id="86e2b-138">De 2.0.0 a 3.0.0</span><span class="sxs-lookup"><span data-stu-id="86e2b-138">From 2.0.0 to 3.0.0</span></span>
<span data-ttu-id="86e2b-139">Soporte de iOS 4.X eliminado.</span><span class="sxs-lookup"><span data-stu-id="86e2b-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="86e2b-140">A partir de esta versión, el destino de implementación de la aplicación debe ser como mínimo iOS 6.</span><span class="sxs-lookup"><span data-stu-id="86e2b-140">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="86e2b-141">Si usa Reach en la aplicación, debe agregar el valor `remote-notification` a la matriz `UIBackgroundModes` en el archivo Info.plist para recibir notificaciones remotas.</span><span class="sxs-lookup"><span data-stu-id="86e2b-141">If you are using Reach in your application, you must add `remote-notification` value to the `UIBackgroundModes` array in your Info.plist file in order to receive remote notifications.</span></span>

<span data-ttu-id="86e2b-142">El método `application:didReceiveRemoteNotification:` debe reemplazarse por `application:didReceiveRemoteNotification:fetchCompletionHandler:` en el delegado de aplicación.</span><span class="sxs-lookup"><span data-stu-id="86e2b-142">The method `application:didReceiveRemoteNotification:` needs to be replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="86e2b-143">"AEPushDelegate.h" es una interfaz desusada y debe quitar todas las referencias.</span><span class="sxs-lookup"><span data-stu-id="86e2b-143">"AEPushDelegate.h" is deprecated interface and you need to remove all references.</span></span> <span data-ttu-id="86e2b-144">Esto incluye eliminar `[[EngagementAgent shared] setPushDelegate:self]` y los métodos delegados del delegado de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="86e2b-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and the delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-to-200"></a><span data-ttu-id="86e2b-145">De 1.16.0 a 2.0.0</span><span class="sxs-lookup"><span data-stu-id="86e2b-145">From 1.16.0 to 2.0.0</span></span>
<span data-ttu-id="86e2b-146">A continuación se describe cómo migrar una integración del SDK desde el servicio Capptain que ofrece Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="86e2b-146">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="86e2b-147">Si va a migrar desde una versión anterior, consulte el sitio web de Capptain para migrar a 1.16 en primer lugar luego aplique el siguiente procedimiento.</span><span class="sxs-lookup"><span data-stu-id="86e2b-147">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.16 first then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86e2b-148">Capptain y Mobile Engagement no son los mismos servicios, y el procedimiento que se indica a continuación destaca únicamente cómo migrar la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="86e2b-148">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="86e2b-149">La migración del SDK en la aplicación NO migrará los datos desde los servidores Capptain a los servidores Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="86e2b-149">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="86e2b-150">Agente</span><span class="sxs-lookup"><span data-stu-id="86e2b-150">Agent</span></span>
<span data-ttu-id="86e2b-151">El método `registerApp:` se ha reemplazado por el nuevo método `init:`.</span><span class="sxs-lookup"><span data-stu-id="86e2b-151">The method `registerApp:` has been replaced by the new method `init:`.</span></span> <span data-ttu-id="86e2b-152">El delegado de la aplicación deben actualizarse como corresponda y usar una cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="86e2b-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="86e2b-153">Seguimiento de SmartAd se ha quitado del SDK y solo tiene que quitar todas las instancias de la clase `AETrackModule`</span><span class="sxs-lookup"><span data-stu-id="86e2b-153">SmartAd tracking has been removed from SDK you just have to remove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="86e2b-154">Cambios del nombre de la clase</span><span class="sxs-lookup"><span data-stu-id="86e2b-154">Class Name Changes</span></span>
<span data-ttu-id="86e2b-155">Como parte de la reconfiguración de marca, hay algunos nombres de clase/archivo que deben cambiarse.</span><span class="sxs-lookup"><span data-stu-id="86e2b-155">As part of the rebranding, there are couple of class/file names that need to be changed.</span></span>

<span data-ttu-id="86e2b-156">Todas las clases precedidas de "CP" cambian su nombre introduciendo el prefijo "AE".</span><span class="sxs-lookup"><span data-stu-id="86e2b-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="86e2b-157">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86e2b-157">Example:</span></span>

* <span data-ttu-id="86e2b-158">`CPModule.h` cambia su nombre a `AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="86e2b-158">`CPModule.h` is renamed to `AEModule.h`.</span></span>

<span data-ttu-id="86e2b-159">Todas las clases con el prefijo "Capptain" cambian su nombre para introducir el prefijo "Engagement".</span><span class="sxs-lookup"><span data-stu-id="86e2b-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="86e2b-160">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="86e2b-160">Examples:</span></span>

* <span data-ttu-id="86e2b-161">La clase `CapptainAgent` cambia su nombre a `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="86e2b-161">The class `CapptainAgent` is renamed to `EngagementAgent`.</span></span>
* <span data-ttu-id="86e2b-162">La clase `CapptainTableViewController` cambia su nombre a `EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="86e2b-162">The class `CapptainTableViewController` is renamed to `EngagementTableViewController`.</span></span>
* <span data-ttu-id="86e2b-163">La clase `CapptainUtils` cambia su nombre a `EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="86e2b-163">The class `CapptainUtils` is renamed to `EngagementUtils`.</span></span>
* <span data-ttu-id="86e2b-164">La clase `CapptainViewController` cambia su nombre a `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="86e2b-164">The class `CapptainViewController` is renamed to `EngagementViewController`.</span></span>

