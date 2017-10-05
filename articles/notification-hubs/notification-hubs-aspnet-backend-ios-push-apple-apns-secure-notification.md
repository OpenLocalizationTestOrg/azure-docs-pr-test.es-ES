---
title: "Inserción segura de los Centros de notificaciones de Azure"
description: "Obtenga información acerca de cómo enviar notificaciones de inserción seguras a una aplicación iOS desde Azure. Ejemplos de código escritos en Objective-C y C#."
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
ms.openlocfilehash: e5f09fb3716303bb21fe7442aa6fa8832174838e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="f9b11-104">Inserción segura de los Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="f9b11-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9b11-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="f9b11-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="f9b11-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f9b11-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="f9b11-107">Android</span><span class="sxs-lookup"><span data-stu-id="f9b11-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="f9b11-108">Información general</span><span class="sxs-lookup"><span data-stu-id="f9b11-108">Overview</span></span>
<span data-ttu-id="f9b11-109">La compatibilidad con las notificaciones push en Microsoft Azure le permite tener acceso a una infraestructura multiplataforma y de escalamiento horizontal fácil de usar, que simplifica considerablemente la implementación de notificaciones push tanto en aplicaciones de consumidor como en aplicaciones empresariales para plataformas móviles.</span><span class="sxs-lookup"><span data-stu-id="f9b11-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="f9b11-110">Debido a restricciones reguladoras o de seguridad, algunas veces una aplicación podría querer incluir algo en la notificación que no se puede trasmitir a través de la infraestructura de las notificaciones de inserción estándar.</span><span class="sxs-lookup"><span data-stu-id="f9b11-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="f9b11-111">En este tutorial se describe cómo lograr la misma experiencia enviando información importante a través de una conexión segura y autenticada entre el dispositivo cliente y el back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9b11-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="f9b11-112">A un alto nivel, el flujo es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9b11-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="f9b11-113">El back-end de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="f9b11-113">The app back-end:</span></span>
   * <span data-ttu-id="f9b11-114">Almacena la carga segura en la base de datos back-end.</span><span class="sxs-lookup"><span data-stu-id="f9b11-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="f9b11-115">Envía el identificador de esta notificación al dispositivo (no se envía información segura).</span><span class="sxs-lookup"><span data-stu-id="f9b11-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="f9b11-116">La aplicación del dispositivo, cuando recibe la información:</span><span class="sxs-lookup"><span data-stu-id="f9b11-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="f9b11-117">El dispositivo entra en contacto con el back-end que solicita la carga segura.</span><span class="sxs-lookup"><span data-stu-id="f9b11-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="f9b11-118">La aplicación puede mostrar la carga como una notificación en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f9b11-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="f9b11-119">Es importante tener en cuenta que en el flujo anterior (y en este tutorial), asumimos que el dispositivo almacena un token de autenticación localmente y, después, el usuario inicia sesión.</span><span class="sxs-lookup"><span data-stu-id="f9b11-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="f9b11-120">Esto garantiza una experiencia sin ningún problema, ya que el dispositivo puede recuperar la carga segura de la notificación usando este token.</span><span class="sxs-lookup"><span data-stu-id="f9b11-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="f9b11-121">Si la aplicación no almacena tokens de autenticación en el dispositivo, o si estos tokens han expirado, la aplicación del dispositivo, al recibir la notificación, debe mostrar una notificación genérica pidiendo al usuario que inicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9b11-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="f9b11-122">Después, la aplicación autentica al usuario y muestra la carga de la notificación.</span><span class="sxs-lookup"><span data-stu-id="f9b11-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="f9b11-123">Este tutorial Inserción segura muestra cómo enviar una notificación de inserción de forma segura.</span><span class="sxs-lookup"><span data-stu-id="f9b11-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="f9b11-124">El tutorial se basa en el tutorial [Notificar a los usuarios](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) , por lo que debe completar los pasos de ese tutorial primero.</span><span class="sxs-lookup"><span data-stu-id="f9b11-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="f9b11-125">Este tutorial asume que ha creado y configurado el centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f9b11-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-ios-project"></a><span data-ttu-id="f9b11-126">Modificación del proyecto iOS</span><span class="sxs-lookup"><span data-stu-id="f9b11-126">Modify the iOS project</span></span>
<span data-ttu-id="f9b11-127">Una vez modificado el back-end de la aplicación para enviar solamente el *id* de una notificación, deberá modificar la aplicación iOS para que administre dicha notificación y devuelva la llamada a su back-end para recuperar el mensaje seguro que se debe mostrar.</span><span class="sxs-lookup"><span data-stu-id="f9b11-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>

<span data-ttu-id="f9b11-128">Para lograr este objetivo, tenemos que escribir la lógica para recuperar el contenido seguro del back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f9b11-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span></span>

1. <span data-ttu-id="f9b11-129">En **AppDelegate.m**, asegúrese de que la aplicación se registra para notificaciones silenciosas de manera a procesar el identificador de notificación enviado desde el back-end.</span><span class="sxs-lookup"><span data-stu-id="f9b11-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span></span> <span data-ttu-id="f9b11-130">Agregue la opción **UIRemoteNotificationTypeNewsstandContentAvailability** en didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="f9b11-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="f9b11-131">En su **AppDelegate.m** , agregue una sección de implementación en la parte superior con la siguiente declaración:</span><span class="sxs-lookup"><span data-stu-id="f9b11-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="f9b11-132">Después, en la sección de implementación, agregue el siguiente código, sustituyendo el marcador de posición `{back-end endpoint}` por el extremo para el back-end obtenido anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f9b11-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span></span>

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

    This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences.

1. <span data-ttu-id="f9b11-133">Ahora tenemos que administrar la notificación entrante y usar el método anterior para recuperar el contenido para mostrar.</span><span class="sxs-lookup"><span data-stu-id="f9b11-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span></span> <span data-ttu-id="f9b11-134">Primero, tenemos que habilitar la aplicación iOS para que se ejecute en segundo plano cuando reciba una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="f9b11-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span></span> <span data-ttu-id="f9b11-135">En **XCode**, seleccione el proyecto de aplicación en el panel izquierdo y, a continuación, haga clic en el destino de la aplicación principal en la sección **Targets** (Destinos) del panel central.</span><span class="sxs-lookup"><span data-stu-id="f9b11-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span></span>
2. <span data-ttu-id="f9b11-136">A continuación, haga clic en la pestaña **Capabilities** (Funcionalidades) situada en la parte superior del panel central y active la casilla **Remote Notifications** (Notificaciones remotas).</span><span class="sxs-lookup"><span data-stu-id="f9b11-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="f9b11-137">En **AppDelegate.m** , agregue el método siguiente para administrar las notificaciones de inserción:</span><span class="sxs-lookup"><span data-stu-id="f9b11-137">In **AppDelegate.m** add the following method to handle push notifications:</span></span>
   
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
   
    <span data-ttu-id="f9b11-138">Tenga en cuenta que es preferible administrar los casos de propiedad de encabezado de autenticación ausente o rechazo por el backend.</span><span class="sxs-lookup"><span data-stu-id="f9b11-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="f9b11-139">La administración específica de estos casos depende principalmente de la experiencia del usuario de destino.</span><span class="sxs-lookup"><span data-stu-id="f9b11-139">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="f9b11-140">Una opción es mostrar una notificación con un mensaje genérico para el usuario con el fin de que se autentique para recuperar la notificación real.</span><span class="sxs-lookup"><span data-stu-id="f9b11-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="f9b11-141">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f9b11-141">Run the Application</span></span>
<span data-ttu-id="f9b11-142">Para ejecutar la aplicación, realice las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="f9b11-142">To run the application, do the following:</span></span>

1. <span data-ttu-id="f9b11-143">En XCode, ejecute la aplicación en un dispositivo iOS físico (las notificaciones de inserción no funcionarán en el simulador).</span><span class="sxs-lookup"><span data-stu-id="f9b11-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="f9b11-144">En la interfaz de usuario de la aplicación iOS, escriba un nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="f9b11-144">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="f9b11-145">Esta información puede ser cualquier cadena, pero deben tener el mismo valor.</span><span class="sxs-lookup"><span data-stu-id="f9b11-145">These can be any string, but they must be the same value.</span></span>
3. <span data-ttu-id="f9b11-146">En la interfaz de usuario de la aplicación iOS, haga clic en **Log in**(Iniciar sesión).</span><span class="sxs-lookup"><span data-stu-id="f9b11-146">In the iOS app UI, click **Log in**.</span></span> <span data-ttu-id="f9b11-147">A continuación, haga clic en **Send push**(Enviar inserción).</span><span class="sxs-lookup"><span data-stu-id="f9b11-147">Then click **Send push**.</span></span> <span data-ttu-id="f9b11-148">Debe ver la notificación segura mostrada en el centro notificaciones.</span><span class="sxs-lookup"><span data-stu-id="f9b11-148">You should see the secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
