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
# <a name="azure-notification-hubs-secure-push"></a>Inserción segura de los Centros de notificaciones de Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Información general
Compatibilidad con notificaciones de inserción de Microsoft Azure le permite tooaccess una infraestructura de inserción fácil de usar, varias plataformas y escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa para dispositivos móviles plataformas.

A veces debido a restricciones de seguridad o tooregulatory, una aplicación podría querer tooinclude algo en la notificación de Hola que no se transmiten a través de la infraestructura de notificaciones de inserción estándar Hola. Este tutorial describe cómo tooachieve Hola misma experiencia mediante el envío de información confidencial a través de una conexión segura autenticada entre el dispositivo de cliente de Hola y Hola backend de la aplicación.

En un nivel alto, flujo de hello es como sigue:

1. Hola aplicación back-end:
   * Almacena la carga segura en la base de datos back-end.
   * Envía el Id. de Hola de este dispositivo de toohello de notificación (se envía ninguna información segura).
2. aplicación Hello en dispositivo hello, al recibir la notificación de hello:
   * dispositivo de Hello contacta con hello back-end que lo solicita Hola carga de seguridad.
   * aplicación Hello puede mostrar carga hello como una notificación en el dispositivo de Hola.

Es importante toonote que Hola anterior flujo (y en este tutorial), se da por supuesto ese dispositivo Hola almacena un token de autenticación en el almacenamiento local, después de hello usuario inicia sesión en. Esto garantiza una experiencia completamente sin problemas, como dispositivo de hello puede recuperar la carga de seguridad de la notificación de hello con este token. Si la aplicación no almacena tokens de autenticación en el dispositivo de hello, o si pueden haber expirado estos tokens, hello del dispositivo, tras recibir la notificación de Hola debe mostrar una notificación genérica preguntar aplicación Hola de hello usuario toolaunch. aplicación Hello, a continuación, autentica el usuario de Hola y muestra la carga de notificaciones de Hola.

Este tutorial de inserción seguros se muestra cómo toosend una notificación de inserción de forma segura. tutorial de Hola se basa en hello [informar a los usuarios](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, por lo que debe completar los pasos de hello en ese tutorial primero.

> [!NOTE]
> Este tutorial asume que ha creado y configurado el centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a>Modificar el proyecto de iOS de Hola
Ahora que ha modificado su Hola solo de aplicación back-end toosend *identificador* de una notificación, deberá toochange su toohandle de aplicación de iOS que notificación y devolución de llamada su Hola de back-end tooretrieve seguros toobe de mensaje que se muestra.

tooachieve este objetivo, tenemos toowrite Hola lógica tooretrieve Hola contenido seguro de Hola back-end de la aplicación.

1. En **AppDelegate.m**, asegúrese de registros de aplicación Hola seguro para las notificaciones de modo silenciosas por lo que procesa el identificador de notificación de hello enviado desde Hola back-end. Agregar hello **UIRemoteNotificationTypeNewsstandContentAvailability** opción en didFinishLaunchingWithOptions:
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. En su **AppDelegate.m** agrega una sección de implementación en la parte superior de hello con hello siguiente declaración:
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. A continuación, agregue Hola Hola de sección implementación siguiente código, sustituyendo el marcador de posición de hello `{back-end endpoint}` con punto de conexión de hello para el back-end obtenido anteriormente:

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

1. Ahora estamos tienen toohandle Hola entrantes notificación y utilizar método hello anteriormente tooretrieve Hola contenido toodisplay. En primer lugar, tenemos tooenable su toorun de aplicación de iOS en segundo plano de hello al recibir una notificación de inserción. En **XCode**, seleccione el proyecto de aplicación en el panel izquierdo de Hola y luego haga clic en el destino de la aplicación principal en hello **destinos** sección del panel central de Hola.
2. A continuación, haga clic en su **capacidades** pestaña princip Hola de su panel central y compruebe hello **notificaciones remoto** casilla de verificación.
   
    ![][IOS1]
3. En **AppDelegate.m** agregar Hola siguiendo las notificaciones de inserción de toohandle de método:
   
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
   
    Tenga en cuenta que es preferible toohandle casos de Hola de propiedad de encabezado de autenticación que falta o el rechazo por hello back-end. control específico de Hola de estos casos dependen principalmente de la experiencia del usuario de destino. Una opción es toodisplay una notificación con un mensaje genérico para la notificación de real de hello usuario tooauthenticate tooretrieve Hola.

## <a name="run-hello-application"></a>Ejecutar aplicación Hola
toorun Hola aplicación, Hola siguientes:

1. En XCode, ejecute la aplicación hello en un dispositivo de E/s físicas (inserción notificaciones no funcionará en el simulador de hello).
2. En la aplicación de iOS de hello interfaz de usuario, escriba un nombre de usuario y una contraseña. Pueden ser cualquier cadena, pero deben ser Hola el mismo valor.
3. En la aplicación de iOS de hello interfaz de usuario, haga clic en **sesión**. A continuación, haga clic en **Enviar inserción**. Debería ver notificaciones seguras Hola se muestra en el centro de notificaciones.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
