---
title: "aaaAzure notificación concentradores seguros Push"
description: "Obtenga información acerca de cómo toosend segura push aplicación de iOS de tooan de notificaciones de Azure. Ejemplos de código escritos en Objective-C y C#."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="8cd91-104">Inserción segura de los Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="8cd91-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8cd91-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="8cd91-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="8cd91-106">iOS</span><span class="sxs-lookup"><span data-stu-id="8cd91-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="8cd91-107">Android</span><span class="sxs-lookup"><span data-stu-id="8cd91-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="8cd91-108">Información general</span><span class="sxs-lookup"><span data-stu-id="8cd91-108">Overview</span></span>
<span data-ttu-id="8cd91-109">Compatibilidad con notificaciones de inserción de Microsoft Azure le permite tooaccess una infraestructura de inserción fácil de usar, varias plataformas y escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa para dispositivos móviles plataformas.</span><span class="sxs-lookup"><span data-stu-id="8cd91-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="8cd91-110">A veces debido a restricciones de seguridad o tooregulatory, una aplicación podría querer tooinclude algo en la notificación de Hola que no se transmiten a través de la infraestructura de notificaciones de inserción estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="8cd91-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="8cd91-111">Este tutorial describe cómo tooachieve Hola misma experiencia mediante el envío de información confidencial a través de una conexión segura autenticada entre el dispositivo de cliente de Hola y Hola backend de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8cd91-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="8cd91-112">En un nivel alto, flujo de hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="8cd91-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="8cd91-113">Hola aplicación back-end:</span><span class="sxs-lookup"><span data-stu-id="8cd91-113">hello app back-end:</span></span>
   * <span data-ttu-id="8cd91-114">Almacena la carga segura en la base de datos back-end.</span><span class="sxs-lookup"><span data-stu-id="8cd91-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="8cd91-115">Envía el Id. de Hola de este dispositivo de toohello de notificación (se envía ninguna información segura).</span><span class="sxs-lookup"><span data-stu-id="8cd91-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="8cd91-116">aplicación Hello en dispositivo hello, al recibir la notificación de hello:</span><span class="sxs-lookup"><span data-stu-id="8cd91-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="8cd91-117">dispositivo de Hello contacta con hello back-end que lo solicita Hola carga de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8cd91-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="8cd91-118">aplicación Hello puede mostrar carga hello como una notificación en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cd91-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="8cd91-119">Es importante toonote que Hola anterior flujo (y en este tutorial), se da por supuesto ese dispositivo Hola almacena un token de autenticación en el almacenamiento local, después de hello usuario inicia sesión en.</span><span class="sxs-lookup"><span data-stu-id="8cd91-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="8cd91-120">Esto garantiza una experiencia completamente sin problemas, como dispositivo de hello puede recuperar la carga de seguridad de la notificación de hello con este token.</span><span class="sxs-lookup"><span data-stu-id="8cd91-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="8cd91-121">Si la aplicación no almacena tokens de autenticación en el dispositivo de hello, o si pueden haber expirado estos tokens, hello del dispositivo, tras recibir la notificación de Hola debe mostrar una notificación genérica preguntar aplicación Hola de hello usuario toolaunch.</span><span class="sxs-lookup"><span data-stu-id="8cd91-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="8cd91-122">aplicación Hello, a continuación, autentica el usuario de Hola y muestra la carga de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cd91-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="8cd91-123">Este tutorial de inserción seguros se muestra cómo toosend una notificación de inserción de forma segura.</span><span class="sxs-lookup"><span data-stu-id="8cd91-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="8cd91-124">tutorial de Hola se basa en hello [informar a los usuarios](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, por lo que debe completar los pasos de hello en ese tutorial primero.</span><span class="sxs-lookup"><span data-stu-id="8cd91-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="8cd91-125">Este tutorial asume que ha creado y configurado el centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8cd91-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a><span data-ttu-id="8cd91-126">Modificar el proyecto de iOS de Hola</span><span class="sxs-lookup"><span data-stu-id="8cd91-126">Modify hello iOS project</span></span>
<span data-ttu-id="8cd91-127">Ahora que ha modificado su Hola solo de aplicación back-end toosend *identificador* de una notificación, deberá toochange su toohandle de aplicación de iOS que notificación y devolución de llamada su Hola de back-end tooretrieve seguros toobe de mensaje que se muestra.</span><span class="sxs-lookup"><span data-stu-id="8cd91-127">Now that you modified your app back-end toosend just hello *id* of a notification, you have toochange your iOS app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>

<span data-ttu-id="8cd91-128">tooachieve este objetivo, tenemos toowrite Hola lógica tooretrieve Hola contenido seguro de Hola back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8cd91-128">tooachieve this goal, we have toowrite hello logic tooretrieve hello secure content from hello app back-end.</span></span>

1. <span data-ttu-id="8cd91-129">En **AppDelegate.m**, asegúrese de registros de aplicación Hola seguro para las notificaciones de modo silenciosas por lo que procesa el identificador de notificación de hello enviado desde Hola back-end.</span><span class="sxs-lookup"><span data-stu-id="8cd91-129">In **AppDelegate.m**, make sure hello app registers for silent notifications so it processes hello notification id sent from hello backend.</span></span> <span data-ttu-id="8cd91-130">Agregar hello **UIRemoteNotificationTypeNewsstandContentAvailability** opción en didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="8cd91-130">Add hello **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="8cd91-131">En su **AppDelegate.m** agrega una sección de implementación en la parte superior de hello con hello siguiente declaración:</span><span class="sxs-lookup"><span data-stu-id="8cd91-131">In your **AppDelegate.m** add an implementation section at hello top with hello following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="8cd91-132">A continuación, agregue Hola Hola de sección implementación siguiente código, sustituyendo el marcador de posición de hello `{back-end endpoint}` con punto de conexión de hello para el back-end obtenido anteriormente:</span><span class="sxs-lookup"><span data-stu-id="8cd91-132">Then add in hello implementation section hello following code, substituting hello placeholder `{back-end endpoint}` with hello endpoint for your back-end obtained previously:</span></span>

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. <span data-ttu-id="8cd91-133">Ahora estamos tienen toohandle Hola entrantes notificación y utilizar método hello anteriormente tooretrieve Hola contenido toodisplay.</span><span class="sxs-lookup"><span data-stu-id="8cd91-133">Now we have toohandle hello incoming notification and use hello method above tooretrieve hello content toodisplay.</span></span> <span data-ttu-id="8cd91-134">En primer lugar, tenemos tooenable su toorun de aplicación de iOS en segundo plano de hello al recibir una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="8cd91-134">First, we have tooenable your iOS app toorun in hello background when receiving a push notification.</span></span> <span data-ttu-id="8cd91-135">En **XCode**, seleccione el proyecto de aplicación en el panel izquierdo de Hola y luego haga clic en el destino de la aplicación principal en hello **destinos** sección del panel central de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cd91-135">In **XCode**, select your app project on hello left panel, then click your main app target in hello **Targets** section from hello central pane.</span></span>
2. <span data-ttu-id="8cd91-136">A continuación, haga clic en su **capacidades** pestaña princip Hola de su panel central y compruebe hello **notificaciones remoto** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="8cd91-136">Then click your **Capabilities** tab at hello top of your central pane, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="8cd91-137">En **AppDelegate.m** agregar Hola siguiendo las notificaciones de inserción de toohandle de método:</span><span class="sxs-lookup"><span data-stu-id="8cd91-137">In **AppDelegate.m** add hello following method toohandle push notifications:</span></span>
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    <span data-ttu-id="8cd91-138">Tenga en cuenta que es preferible toohandle casos de Hola de propiedad de encabezado de autenticación que falta o el rechazo por hello back-end.</span><span class="sxs-lookup"><span data-stu-id="8cd91-138">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="8cd91-139">control específico de Hola de estos casos dependen principalmente de la experiencia del usuario de destino.</span><span class="sxs-lookup"><span data-stu-id="8cd91-139">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="8cd91-140">Una opción es toodisplay una notificación con un mensaje genérico para la notificación de real de hello usuario tooauthenticate tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="8cd91-140">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="8cd91-141">Ejecutar aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="8cd91-141">Run hello Application</span></span>
<span data-ttu-id="8cd91-142">toorun Hola aplicación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="8cd91-142">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="8cd91-143">En XCode, ejecute la aplicación hello en un dispositivo de E/s físicas (inserción notificaciones no funcionará en el simulador de hello).</span><span class="sxs-lookup"><span data-stu-id="8cd91-143">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="8cd91-144">En la aplicación de iOS de hello interfaz de usuario, escriba un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="8cd91-144">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="8cd91-145">Pueden ser cualquier cadena, pero deben ser Hola el mismo valor.</span><span class="sxs-lookup"><span data-stu-id="8cd91-145">These can be any string, but they must be hello same value.</span></span>
3. <span data-ttu-id="8cd91-146">En la aplicación de iOS de hello interfaz de usuario, haga clic en **sesión**.</span><span class="sxs-lookup"><span data-stu-id="8cd91-146">In hello iOS app UI, click **Log in**.</span></span> <span data-ttu-id="8cd91-147">A continuación, haga clic en **Enviar inserción**.</span><span class="sxs-lookup"><span data-stu-id="8cd91-147">Then click **Send push**.</span></span> <span data-ttu-id="8cd91-148">Debería ver notificaciones seguras Hola se muestra en el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="8cd91-148">You should see hello secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
