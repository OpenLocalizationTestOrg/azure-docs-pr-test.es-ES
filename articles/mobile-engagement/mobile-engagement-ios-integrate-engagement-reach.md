---
title: "aaaAzure integración con alcanzar el SDK de Mobile Engagement iOS | Documentos de Microsoft"
description: "Actualizaciones y procedimientos más recientes para el SDK de iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a><span data-ttu-id="37bb1-103">Cómo tooIntegrate interacción a en iOS</span><span class="sxs-lookup"><span data-stu-id="37bb1-103">How tooIntegrate Engagement Reach on iOS</span></span>
<span data-ttu-id="37bb1-104">Debe seguir el procedimiento de integración de hello descrito en hello [cómo tooIntegrate interacción en el documento de iOS](mobile-engagement-ios-integrate-engagement.md) antes de seguir esta guía.</span><span class="sxs-lookup"><span data-stu-id="37bb1-104">You must follow hello integration procedure described in hello [How tooIntegrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="37bb1-105">Esta documentación requiere XCode 8.</span><span class="sxs-lookup"><span data-stu-id="37bb1-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="37bb1-106">Si realmente dependen XCode 7, a continuación, puede usar hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="37bb1-106">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="37bb1-107">Existe un problema conocido en esta versión anterior cuando se ejecuta en dispositivos iOS 10: las notificaciones del sistema no se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="37bb1-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="37bb1-108">toofix esto tendrá tooimplement hello en desuso API `application:didReceiveRemoteNotification:` en la aplicación el delegado como sigue:</span><span class="sxs-lookup"><span data-stu-id="37bb1-108">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="37bb1-109">**No se recomienda esta solución** ya que este comportamiento puede cambiar en la próxima actualización de la versión de iOS (por menor que sea) porque esta API de iOS está en desuso.</span><span class="sxs-lookup"><span data-stu-id="37bb1-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="37bb1-110">Debería pasar tooXCode 8 tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="37bb1-110">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="37bb1-111">Habilitar la tooreceive aplicación silenciosa de las notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="37bb1-111">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="37bb1-112">Pasos de integración</span><span class="sxs-lookup"><span data-stu-id="37bb1-112">Integration steps</span></span>
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="37bb1-113">Incrustar Hola interacción Reach SDK en el proyecto de iOS</span><span class="sxs-lookup"><span data-stu-id="37bb1-113">Embed hello Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="37bb1-114">Agregar sdk de alcance de hello en el proyecto de Xcode.</span><span class="sxs-lookup"><span data-stu-id="37bb1-114">Add hello Reach sdk in your Xcode project.</span></span> <span data-ttu-id="37bb1-115">En Xcode, vaya demasiado**proyecto \> agregar tooproject** y elija hello `EngagementReach` carpeta.</span><span class="sxs-lookup"><span data-stu-id="37bb1-115">In Xcode, go too**Project \> Add tooproject** and choose hello `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="37bb1-116">Modifique su delegado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="37bb1-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="37bb1-117">Hola parte superior de su archivo de implementación, importe el módulo de llegar a la interacción de hello:</span><span class="sxs-lookup"><span data-stu-id="37bb1-117">At hello top of your implementation file, import hello Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="37bb1-118">Método `applicationDidFinishLaunching:` o `application:didFinishLaunchingWithOptions:`, cree un módulo de reach y páselo tooyour línea de inicialización de contratación existente:</span><span class="sxs-lookup"><span data-stu-id="37bb1-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it tooyour existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="37bb1-119">Modificar **'icon.png'** cadena con el nombre de la imagen de Hola que desee utilizar como icono de la notificación.</span><span class="sxs-lookup"><span data-stu-id="37bb1-119">Modify **'icon.png'** string with hello image name you want as your notification icon.</span></span>
* <span data-ttu-id="37bb1-120">Si desea que la opción de hello toouse *valor del distintivo actualización* en las campañas de cobertura o si desea que la inserción nativa toouse \<nativa y formato de SaaS/alcance API/campaña de inserción\> campañas, debe dejar que módulo de Reach Hola administre Hola distintivo propio icono (se borrará automáticamente distintivo de la aplicación de Hola y también restablece el valor de hello almacenado interacción cada vez aplicación hello se inició o foregrounded).</span><span class="sxs-lookup"><span data-stu-id="37bb1-120">If you want toouse hello option *Update badge value* in Reach campaigns or if you want toouse native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let hello Reach module manage hello badge icon itself (it will automatically clear hello application badge and also reset hello value stored by Engagement every time hello application is started or foregrounded).</span></span> <span data-ttu-id="37bb1-121">Esto se realiza mediante la adición de hello después de línea después de la inicialización del módulo de Reach:</span><span class="sxs-lookup"><span data-stu-id="37bb1-121">This is done by adding hello following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="37bb1-122">Si desea que la inserción de datos de cobertura de toohandle, debe permitir que el delegado de la aplicación se ajustan toohello `AEReachDataPushDelegate` protocolo.</span><span class="sxs-lookup"><span data-stu-id="37bb1-122">If you want toohandle Reach data push, you must let your Application delegate conform toohello `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="37bb1-123">Agregue Hola después de línea después de la inicialización del módulo de alcance:</span><span class="sxs-lookup"><span data-stu-id="37bb1-123">Add hello following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="37bb1-124">A continuación, puede implementar métodos de hello `onDataPushStringReceived:` y `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` en el delegado de aplicación:</span><span class="sxs-lookup"><span data-stu-id="37bb1-124">Then you can implement hello methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a><span data-ttu-id="37bb1-125">Categoría</span><span class="sxs-lookup"><span data-stu-id="37bb1-125">Category</span></span>
<span data-ttu-id="37bb1-126">parámetro de categoría de Hello es opcional cuando se crea una campaña de inserción de datos y permite que los datos de toofilter inserta.</span><span class="sxs-lookup"><span data-stu-id="37bb1-126">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="37bb1-127">Esto es útil si desea que toopush diferentes tipos de `Base64` tooidentify de datos y quiere que su tipo antes del análisis de ellos.</span><span class="sxs-lookup"><span data-stu-id="37bb1-127">This is useful if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

<span data-ttu-id="37bb1-128">**La aplicación es ahora la presentación y listo tooreceive alcanzar el contenido.**</span><span class="sxs-lookup"><span data-stu-id="37bb1-128">**Your application is now ready tooreceive and display reach contents!**</span></span>

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a><span data-ttu-id="37bb1-129">¿Cómo tooreceive sondeos en cualquier momento y anuncios</span><span class="sxs-lookup"><span data-stu-id="37bb1-129">How tooreceive announcements and polls at any time</span></span>
<span data-ttu-id="37bb1-130">Interacción puede enviar notificaciones de alcance a los usuarios finales de tooyour en cualquier momento mediante Hola servicio de notificaciones Push de Apple.</span><span class="sxs-lookup"><span data-stu-id="37bb1-130">Engagement can send Reach notifications tooyour end users at any time by using hello Apple Push Notification Service.</span></span>

<span data-ttu-id="37bb1-131">tooenable esta funcionalidad, deberá tener tooprepare la aplicación para notificaciones de inserción de Apple y modificar el delegado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="37bb1-131">tooenable this functionality, you'll have tooprepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="37bb1-132">Preparar la aplicación para notificaciones de inserción de Apple</span><span class="sxs-lookup"><span data-stu-id="37bb1-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="37bb1-133">Siga la Guía de hello: [cómo tooPrepare la aplicación para notificaciones Push de Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="37bb1-133">Please follow hello guide : [How tooPrepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-hello-necessary-client-code"></a><span data-ttu-id="37bb1-134">Agregar código de cliente necesario Hola</span><span class="sxs-lookup"><span data-stu-id="37bb1-134">Add hello necessary client code</span></span>
<span data-ttu-id="37bb1-135">*En este momento la aplicación debe tener un certificado de inserción de Apple registrado en el front-end de hello interacción.*</span><span class="sxs-lookup"><span data-stu-id="37bb1-135">*At this point your application should have a registered Apple push certificate in hello Engagement frontend.*</span></span>

<span data-ttu-id="37bb1-136">Si ya no es así, deberá tooregister las notificaciones de inserción de tooreceive de aplicación.</span><span class="sxs-lookup"><span data-stu-id="37bb1-136">If it's not done already, you need tooregister your application tooreceive push notifications.</span></span>

* <span data-ttu-id="37bb1-137">Hola de importación `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="37bb1-137">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="37bb1-138">Agregar Hola siguientes línea cuando se inicia la aplicación (normalmente, en `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="37bb1-138">Add hello following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="37bb1-139">A continuación, deberá token del dispositivo tooprovide tooEngagement Hola devuelta por servidores de Apple.</span><span class="sxs-lookup"><span data-stu-id="37bb1-139">Then, You need tooprovide tooEngagement hello device token returned by Apple servers.</span></span> <span data-ttu-id="37bb1-140">Esto se hace en el método hello denominado `application:didRegisterForRemoteNotificationsWithDeviceToken:` en el delegado de aplicación:</span><span class="sxs-lookup"><span data-stu-id="37bb1-140">This is done in hello method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="37bb1-141">Por último, tendrá tooinform Hola Engagement SDK cuando la aplicación recibe una notificación remota.</span><span class="sxs-lookup"><span data-stu-id="37bb1-141">Finally, you have tooinform hello Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="37bb1-142">Hola a toodo que llame al método `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` en el delegado de aplicación:</span><span class="sxs-lookup"><span data-stu-id="37bb1-142">toodo that, call hello method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="37bb1-143">De forma predeterminada, interacción alcanzar controla completionHandler Hola.</span><span class="sxs-lookup"><span data-stu-id="37bb1-143">By default, Engagement Reach controls hello completionHandler.</span></span> <span data-ttu-id="37bb1-144">Si desea que toomanually responden toohello `handler` un bloqueo en el código, puede pasar nulo para hello `handler` bloquear el argumento y el control de finalización de hello usted mismo.</span><span class="sxs-lookup"><span data-stu-id="37bb1-144">If you want toomanually respond toohello `handler` block in your code, you can pass nil for hello `handler` argument and control hello completion block yourself.</span></span> <span data-ttu-id="37bb1-145">Vea hello `UIBackgroundFetchResult` tipo para obtener una lista de valores posibles.</span><span class="sxs-lookup"><span data-stu-id="37bb1-145">See hello `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="37bb1-146">Ejemplo completo</span><span class="sxs-lookup"><span data-stu-id="37bb1-146">Full example</span></span>
<span data-ttu-id="37bb1-147">Este es un ejemplo completo de integración:</span><span class="sxs-lookup"><span data-stu-id="37bb1-147">Here is a full example of integration:</span></span>

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="37bb1-148">Resolución de conflictos de delegado de UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="37bb1-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="37bb1-149">*Si ni la aplicación ni una de las bibliotecas de terceros implementa `UNUserNotificationCenterDelegate`, puede pasar por alto esta parte.*</span><span class="sxs-lookup"><span data-stu-id="37bb1-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="37bb1-150">Un `UNUserNotificationCenter` delegado es utilizado por el ciclo de vida de hello SDK toomonitor Hola de notificaciones de interacción en dispositivos que ejecutan en iOS 10 o superior.</span><span class="sxs-lookup"><span data-stu-id="37bb1-150">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="37bb1-151">Hola SDK tiene su propia implementación de hello `UNUserNotificationCenterDelegate` de protocolo, pero puede haber solo un `UNUserNotificationCenter` delegar por aplicación.</span><span class="sxs-lookup"><span data-stu-id="37bb1-151">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="37bb1-152">Cualquier otro delegado agrega toohello `UNUserNotificationCenter` objeto entrarán en conflicto con hello interacción uno.</span><span class="sxs-lookup"><span data-stu-id="37bb1-152">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="37bb1-153">Si Hola SDK detecta a delegado su o cualquier otro de terceros no usará su propio toogive de implementación, una posibilidad tooresolve Hola conflictos.</span><span class="sxs-lookup"><span data-stu-id="37bb1-153">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="37bb1-154">Tendrá tooadd Hola interacción lógica tooyour posee conflictos de hello tooresolve de delegado en orden.</span><span class="sxs-lookup"><span data-stu-id="37bb1-154">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="37bb1-155">Hay dos tooachieve formas esto.</span><span class="sxs-lookup"><span data-stu-id="37bb1-155">There are two ways tooachieve this.</span></span>

<span data-ttu-id="37bb1-156">Propuesta 1, enviando el delegado llama toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="37bb1-156">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="37bb1-157">O propuesta 2, heredando de hello `AEUserNotificationHandler` (clase)</span><span class="sxs-lookup"><span data-stu-id="37bb1-157">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="37bb1-158">Puede determinar si una notificación pueden proceder de contratación o no pasando su `userInfo` diccionario toohello agente `isEngagementPushPayload:` método de la clase.</span><span class="sxs-lookup"><span data-stu-id="37bb1-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="37bb1-159">Asegúrese de que ese hello `UNUserNotificationCenter` delegado del objeto se establece el delegado tooyour dentro de cualquier hello `application:willFinishLaunchingWithOptions:` o hello `application:didFinishLaunchingWithOptions:` método de delegado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="37bb1-159">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="37bb1-160">Por ejemplo, si implementa Hola anteriormente propuesta 1:</span><span class="sxs-lookup"><span data-stu-id="37bb1-160">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="37bb1-161">Cómo las campañas de toocustomize</span><span class="sxs-lookup"><span data-stu-id="37bb1-161">How toocustomize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="37bb1-162">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="37bb1-162">Notifications</span></span>
<span data-ttu-id="37bb1-163">Hay dos tipos de notificaciones: las notificaciones del sistema y de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="37bb1-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="37bb1-164">Las notificaciones del sistema se controlan con iOS y no se pueden personalizar.</span><span class="sxs-lookup"><span data-stu-id="37bb1-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="37bb1-165">Se realizan en la aplicación notificaciones de una vista que se agrega dinámicamente toohello ventana actual de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="37bb1-165">In-app notifications are made of a view that is dynamically added toohello current application window.</span></span> <span data-ttu-id="37bb1-166">Esto se denomina superposición de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="37bb1-166">This is called a notification overlay.</span></span> <span data-ttu-id="37bb1-167">Superposiciones de notificación son excelentes para una integración rápida porque no requieren toomodify cualquier vista de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="37bb1-167">Notification overlays are great for a fast integration because they does not require you toomodify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="37bb1-168">Diseño</span><span class="sxs-lookup"><span data-stu-id="37bb1-168">Layout</span></span>
<span data-ttu-id="37bb1-169">visión de hello toomodify de las notificaciones de la aplicación, simplemente puede modificar archivo hello `AENotificationView.xib` tooyour necesita, como conservar los valores de etiqueta de Hola y tipos de subvistas existente Hola.</span><span class="sxs-lookup"><span data-stu-id="37bb1-169">toomodify hello look of your in-app notifications, you can simply modify hello file `AENotificationView.xib` tooyour needs, as long as you keep hello tag values and types of hello existing subviews.</span></span>

<span data-ttu-id="37bb1-170">De forma predeterminada, las notificaciones de la aplicación se muestran en la parte inferior de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="37bb1-170">By default, in-app notifications are presented at hello bottom of hello screen.</span></span> <span data-ttu-id="37bb1-171">Si prefiere toodisplay proporcionan estos en la parte superior de Hola de pantalla, editar hello `AENotificationView.xib` y cambiar hello `AutoSizing` propiedad de la vista principal de Hola por lo que se pueden guardar en parte superior de Hola de su supervista.</span><span class="sxs-lookup"><span data-stu-id="37bb1-171">If you prefer toodisplay them at hello top of screen, edit hello provided `AENotificationView.xib` and change hello `AutoSizing` property of hello main view so it can be kept at hello top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="37bb1-172">Categorías</span><span class="sxs-lookup"><span data-stu-id="37bb1-172">Categories</span></span>
<span data-ttu-id="37bb1-173">Cuando se modifica Hola proporcionada diseño, modificar aspecto de Hola de todas las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="37bb1-173">When you modify hello provided layout, you modify hello look of all your notifications.</span></span> <span data-ttu-id="37bb1-174">Las categorías permiten toodefine que distintos destino busca (posiblemente comportamientos) para las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="37bb1-174">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="37bb1-175">Las categorías pueden especificarse cuando se crea una campaña de cobertura.</span><span class="sxs-lookup"><span data-stu-id="37bb1-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="37bb1-176">Tenga en cuenta que las categorías también permiten personalizar anuncios y sondeos, aspectos que se describen más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="37bb1-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="37bb1-177">tooregister un controlador de categoría para las notificaciones, debe tooadd una llamada una vez Hola llegan módulo se inicializa.</span><span class="sxs-lookup"><span data-stu-id="37bb1-177">tooregister a category handler for your notifications, you need tooadd a call once hello reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="37bb1-178">`myNotifier`debe ser una instancia de un objeto que se ajusta toohello protocolo `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="37bb1-178">`myNotifier` must be an instance of an object that conforms toohello protocol `AENotifier`.</span></span>

<span data-ttu-id="37bb1-179">Puede implementar métodos de protocolo de Hola por usted mismo o puede elegir la clase existente de hello tooreimplement `AEDefaultNotifier` ya que realiza la mayor parte del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="37bb1-179">You can implement hello protocol methods by yourself or you can choose tooreimplement hello existing class `AEDefaultNotifier` which already performs most of hello work.</span></span>

<span data-ttu-id="37bb1-180">Por ejemplo, si desea vista de notificaciones de hello tooredefine para una categoría específica, puede seguir este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="37bb1-180">For example, if you want tooredefine hello notification view for a specific category, you can follow this example:</span></span>

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

<span data-ttu-id="37bb1-181">En este ejemplo simple de categoría, se supone que tiene un archivo denominado `MyNotificationView.xib` en el paquete de aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="37bb1-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="37bb1-182">Si el método hello no es capaz de toofind correspondiente `.xib`, no se mostrará la notificación de Hola y contratación dará como resultado un mensaje en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="37bb1-182">If hello method is not able toofind a corresponding `.xib`, hello notification will not be displayed and Engagement will output a message in hello console.</span></span>

<span data-ttu-id="37bb1-183">archivo nib de Hello proporcionado debe respetar Hola siguiendo las reglas:</span><span class="sxs-lookup"><span data-stu-id="37bb1-183">hello provided nib file should respect hello following rules:</span></span>

* <span data-ttu-id="37bb1-184">Solo debe contener una vista.</span><span class="sxs-lookup"><span data-stu-id="37bb1-184">It should only contain one view.</span></span>
* <span data-ttu-id="37bb1-185">Deben ser subvistas de hello mismo tipos como Hola aquellos dentro de hello proporciona nib archivo denominado`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="37bb1-185">Subviews should be of hello same types as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="37bb1-186">Subvistas deben tener Hola mismo etiquetas como Hola aquellos dentro de hello proporciona nib archivo denominado`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="37bb1-186">Subviews should have hello same tags as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="37bb1-187">Simplemente copie el archivo nib de hello proporcionado, denominado `AENotificationView.xib`y empezar a trabajar desde allí.</span><span class="sxs-lookup"><span data-stu-id="37bb1-187">Just copy hello provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="37bb1-188">Pero tenga cuidado, Hola vista toohello clase asociada, dentro de este archivo nib es `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="37bb1-188">But be careful, hello view inside this nib file is associated toohello class `AENotificationView`.</span></span> <span data-ttu-id="37bb1-189">Esta clase se volvió a definir método hello `layoutSubViews` toomove y cambiar el tamaño de sus subvistas según toocontext.</span><span class="sxs-lookup"><span data-stu-id="37bb1-189">This class redefined hello method `layoutSubViews` toomove and resize its subviews according toocontext.</span></span> <span data-ttu-id="37bb1-190">Puede que desee tooreplace con un `UIView` o una clase de vista personalizada.</span><span class="sxs-lookup"><span data-stu-id="37bb1-190">You may want tooreplace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="37bb1-191">Si necesita personalización más profunda de las notificaciones (si se desea para la instancia tooload la vista directamente desde el código de hello), se recomienda tootake un vistazo a Hola proporciona documentación de código y la clase de origen de `Protocol ReferencesDefaultNotifier` y `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="37bb1-191">If you need deeper customization of your notifications(if you want for instance tooload your view directly from hello code), it is recommended tootake a look at hello provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="37bb1-192">Tenga en cuenta que puede usar Hola notificador mismo para varias categorías.</span><span class="sxs-lookup"><span data-stu-id="37bb1-192">Note that you can use hello same notifier for multiple categories.</span></span>

<span data-ttu-id="37bb1-193">Puede notificador de hello también redefinido predeterminado similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="37bb1-193">You can also redefined hello default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="37bb1-194">Manejo de notificaciones</span><span class="sxs-lookup"><span data-stu-id="37bb1-194">Notification handling</span></span>
<span data-ttu-id="37bb1-195">Cuando se usa la categoría predeterminada de hello, se llaman a algunos métodos de ciclo de vida en hello `AEReachContent` tooreport estadísticas y actualización Hola campaña el estado del objeto:</span><span class="sxs-lookup"><span data-stu-id="37bb1-195">When using hello default category, some life cycle methods are called on hello `AEReachContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="37bb1-196">Cuando se muestra la notificación de hello en aplicaciones, Hola `displayNotification` se llama al método (que notifica estadísticas) por `AEReachModule` si `handleNotification:` devuelve `YES`.</span><span class="sxs-lookup"><span data-stu-id="37bb1-196">When hello notification is displayed in application, hello `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="37bb1-197">Si se descarta la notificación de hello, Hola `exitNotification` método se llama, se notifica la estadística y ahora se pueden procesar las campañas siguientes.</span><span class="sxs-lookup"><span data-stu-id="37bb1-197">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="37bb1-198">Si se hace clic en la notificación de hello, `actionNotification` es llama, se notifican estadísticas y se realiza la acción de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="37bb1-198">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated action is performed.</span></span>

<span data-ttu-id="37bb1-199">Si la implementación de `AENotifier` omisiones Hola comportamiento predeterminado, tendrá toocall estos métodos de ciclo de vida por usted mismo.</span><span class="sxs-lookup"><span data-stu-id="37bb1-199">If your implementation of `AENotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="37bb1-200">Hello en los ejemplos siguientes muestra algunos casos donde se omite el comportamiento predeterminado de hello:</span><span class="sxs-lookup"><span data-stu-id="37bb1-200">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="37bb1-201">No se extienden `AEDefaultNotifier`, por ejemplo, se implementa el control de categoría desde cero.</span><span class="sxs-lookup"><span data-stu-id="37bb1-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="37bb1-202">Reemplazó `prepareNotificationView:forContent:`, ser al menos seguro toomap `onNotificationActioned` o `onNotificationExited` tooone de los controles de I.U.</span><span class="sxs-lookup"><span data-stu-id="37bb1-202">You overrode `prepareNotificationView:forContent:`, be sure toomap at least `onNotificationActioned` or `onNotificationExited` tooone of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="37bb1-203">Si `handleNotification:` inicia una excepción, Hola contenido se elimina y `drop` es llama, se notifica en las estadísticas y ahora se pueden procesar las campañas siguientes.</span><span class="sxs-lookup"><span data-stu-id="37bb1-203">If `handleNotification:` throws an exception, hello content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="37bb1-204">Incluir notificaciones como parte de una vista existente</span><span class="sxs-lookup"><span data-stu-id="37bb1-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="37bb1-205">Las superposiciones son ideales para una integración rápida, pero a veces pueden no ser convenientes o pueden tener efectos secundarios no deseados.</span><span class="sxs-lookup"><span data-stu-id="37bb1-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="37bb1-206">Si no está satisfecho con el sistema de superposición de hello en algunas de las vistas, puede personalizarlo para estas vistas.</span><span class="sxs-lookup"><span data-stu-id="37bb1-206">If you're not satisfied with hello overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="37bb1-207">Puede decidir tooinclude nuestro diseño de notificación en las vistas existentes.</span><span class="sxs-lookup"><span data-stu-id="37bb1-207">You can decide tooinclude our notification layout in your existing views.</span></span> <span data-ttu-id="37bb1-208">toodo por lo tanto, hay dos estilos de implementación:</span><span class="sxs-lookup"><span data-stu-id="37bb1-208">toodo so, there is two implementation styles:</span></span>

1. <span data-ttu-id="37bb1-209">Agregar vista de notificaciones de hello mediante el generador de interfaz</span><span class="sxs-lookup"><span data-stu-id="37bb1-209">Add hello notification view using interface builder</span></span>

   * <span data-ttu-id="37bb1-210">Abrir el *generador de la interfaz*</span><span class="sxs-lookup"><span data-stu-id="37bb1-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="37bb1-211">Coloque un 320 x 60 (o 60 x 768 si se encuentra en iPad) `UIView` donde desea Hola notificación tooappear</span><span class="sxs-lookup"><span data-stu-id="37bb1-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want hello notification tooappear</span></span>
   * <span data-ttu-id="37bb1-212">Establezca el valor de etiqueta de Hola para esta vista demasiado: **36822491**</span><span class="sxs-lookup"><span data-stu-id="37bb1-212">Set hello Tag value for this view too: **36822491**</span></span>
2. <span data-ttu-id="37bb1-213">Agregar vista de notificaciones de hello mediante programación.</span><span class="sxs-lookup"><span data-stu-id="37bb1-213">Add hello notification view programmatically.</span></span> <span data-ttu-id="37bb1-214">Basta con agregar Hola después de código cuando se ha inicializado la vista:</span><span class="sxs-lookup"><span data-stu-id="37bb1-214">Just add hello following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="37bb1-215">La macro `NOTIFICATION_AREA_VIEW_TAG` puede encontrarse en `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="37bb1-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="37bb1-216">notificador de Hello predeterminado detecta automáticamente ese diseño de notificación de Hola se incluye en esta vista y no agregará una superposición para él.</span><span class="sxs-lookup"><span data-stu-id="37bb1-216">hello default notifier automatically detects that hello notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="37bb1-217">Anuncios y sondeos</span><span class="sxs-lookup"><span data-stu-id="37bb1-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="37bb1-218">Diseños</span><span class="sxs-lookup"><span data-stu-id="37bb1-218">Layouts</span></span>
<span data-ttu-id="37bb1-219">Puede modificar archivos de hello `AEDefaultAnnouncementView.xib` y `AEDefaultPollView.xib` como mantener valores de etiqueta de Hola y tipos de subvistas existente Hola.</span><span class="sxs-lookup"><span data-stu-id="37bb1-219">You can modify hello files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep hello tag values and types of hello existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="37bb1-220">Categorías</span><span class="sxs-lookup"><span data-stu-id="37bb1-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="37bb1-221">Diseños alternativos</span><span class="sxs-lookup"><span data-stu-id="37bb1-221">Alternate layouts</span></span>
<span data-ttu-id="37bb1-222">Al igual que las notificaciones, categoría de la campaña de hello puede ser toohave usado diseños alternativos para los sondeos y anuncios.</span><span class="sxs-lookup"><span data-stu-id="37bb1-222">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="37bb1-223">toocreate una categoría de un anuncio, debe extender **AEAnnouncementViewController** y registrarlo una vez que se ha inicializado el módulo de reach hello:</span><span class="sxs-lookup"><span data-stu-id="37bb1-223">toocreate a category for an announcement, you must extend **AEAnnouncementViewController** and register it once hello reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="37bb1-224">Cada vez que un usuario ha hecho clic en una notificación para un anuncio con la categoría de Hola "Mi\_categoría", el controlador de vista registrados (en ese caso `MyCustomAnnouncementViewController`) se inicializará mediante una llamada a método hello `initWithAnnouncement:` y ver Hola será ventana de la aplicación de actual de toohello agregada.</span><span class="sxs-lookup"><span data-stu-id="37bb1-224">Each time a user will click on a notification for an announcement with hello category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling hello method `initWithAnnouncement:` and hello view will be added toohello current application window.</span></span>
>
>

<span data-ttu-id="37bb1-225">En la implementación de hello `AEAnnouncementViewController` clase tendrá la propiedad de hello tooread `announcement` tooinitialize sus subvistas.</span><span class="sxs-lookup"><span data-stu-id="37bb1-225">In your implementation of hello `AEAnnouncementViewController` class you will have tooread hello property `announcement` tooinitialize your subviews.</span></span> <span data-ttu-id="37bb1-226">Considere la posibilidad de ejemplo de Hola siguiente, donde dos etiquetas se inicializan mediante `title` y `body` propiedades de hello `AEReachAnnouncement` clase:</span><span class="sxs-lookup"><span data-stu-id="37bb1-226">Consider hello example below, where two labels are initialized using `title` and `body` properties of hello `AEReachAnnouncement` class:</span></span>

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

<span data-ttu-id="37bb1-227">Si no desea tooload sus vistas por sí mismo, pero solo desea que el diseño de la vista de anuncio de manera predeterminada tooreuse hello, simplemente hacer que el controlador de vista personalizada extiende la clase hello proporciona `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="37bb1-227">If you don't want tooload your views by yourself but you just want tooreuse hello default announcement view layout, you can simply make your custom view controller extends hello provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="37bb1-228">En ese caso, duplicar archivo nib de hello `AEDefaultAnnouncementView.xib` y cambie su nombre por lo que se puede cargar el controlador de vista personalizada (para un controlador denominado `CustomAnnouncementViewController`, debe llamar a su archivo nib `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="37bb1-228">In that case, duplicate hello nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="37bb1-229">categoría de tooreplace Hola predeterminada de los anuncios, simplemente registrar el controlador de vista personalizada para la categoría de hello definida en `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="37bb1-229">tooreplace hello default category of announcements, simply register your custom view controller for hello category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="37bb1-230">Sondeos pueden ser personalizada hello igual:</span><span class="sxs-lookup"><span data-stu-id="37bb1-230">Polls can be customized hello same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="37bb1-231">Esta vez, Hola proporciona `MyCustomPollViewController` debe extender `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="37bb1-231">This time, hello provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="37bb1-232">O bien puede tooextend controlador predeterminado de hello: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="37bb1-232">Or you can choose tooextend from hello default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37bb1-233">No olvide toocall o `action` (`submitAnswers:` para controladores de la vista de sondeo personalizado) o `exit` método antes de que se cierra el controlador de vista de Hola.</span><span class="sxs-lookup"><span data-stu-id="37bb1-233">Don't forget toocall either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before hello view controller is dismissed.</span></span> <span data-ttu-id="37bb1-234">En caso contrario, no se envían las estadísticas (es decir, ningún análisis en campaña Hola) y más las campañas siguiente lo importante es que no se notificará hasta que se reinicie el proceso de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="37bb1-234">Otherwise, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly next campaigns will not be notified until hello application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="37bb1-235">Ejemplo de implementación</span><span class="sxs-lookup"><span data-stu-id="37bb1-235">Implementation example</span></span>
<span data-ttu-id="37bb1-236">En esta implementación vista de anuncio personalizado Hola se carga desde un archivo externo xib.</span><span class="sxs-lookup"><span data-stu-id="37bb1-236">In this implementation hello custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="37bb1-237">Al igual que para la personalización avanzada de notificación, se recomienda toolook en el código fuente de Hola de implementación estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="37bb1-237">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
