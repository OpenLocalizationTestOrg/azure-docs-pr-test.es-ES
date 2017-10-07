---
title: aaaNotification concentradores adaptado importantes Tutorial de noticias para iOS
description: "Obtenga información acerca de cómo toouse centros de notificaciones de Bus de servicio de Azure toosend había adaptado importantes de las notificaciones de noticias (iOS)."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a>Usar dispositivos de centros de notificaciones importantes toosend adaptado noticias tooiOS
> [!div class="op_single_selector"]
> * [C# para Tienda Windows](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Información general
Este tema muestra cómo hello toouse [plantillas](notification-hubs-templates-cross-platform-push-messages.md) característica de toobroadcast centros de notificaciones de Azure interrumpir las notificaciones de noticias que se han localizado según el idioma y el dispositivo. En este tutorial debe comenzar con la aplicación de iOS de hello creado en [toosend de centros de notificaciones utilice noticias de última hora]. Cuando haya terminado, que será capaz de tooregister para las categorías que le interesen, especifique un idioma en qué notificaciones de hello tooreceive y recibir sólo las notificaciones de inserción para las categorías de hello seleccionado en ese idioma.

Hay dos partes toothis escenario:

* aplicación de iOS permite a cliente dispositivos toospecify un lenguaje y toodifferent toosubscribe importantes nuevas categorías;
* back-end Hello emite notificaciones de hello, mediante hello **etiqueta** y **plantilla** características de los centros de notificaciones de Azure.

## <a name="prerequisites"></a>Requisitos previos
Debe haber completado hello [toosend de centros de notificaciones utilice noticias de última hora] tutorial y tenga código de hello disponible, ya que este tutorial se basa directamente en ese código.

Visual Studio 2012 o posterior es opcional.

## <a name="template-concepts"></a>Conceptos de plantilla
En [toosend de centros de notificaciones utilice noticias de última hora] ha creado una aplicación que utiliza **etiquetas** toosubscribe toonotifications para categorías de noticias diferentes.
Sin embargo, muchas aplicaciones están dirigidas a varios mercados y requieren localización. Esto significa que contenido Hola de hello las notificaciones tienen toobe localizado y entregado toohello corregir el conjunto de dispositivos.
En este tema le mostraremos cómo hello toouse **plantilla** característica centros de notificaciones tooeasily entregar adaptado notificaciones de noticias de separación.

Nota: una manera toosend adaptado notificaciones es toocreate varias versiones de cada etiqueta. Por ejemplo, toosupport inglés, francés y mandarín, se necesita tres etiquetas diferentes para noticias internacionales: "world_en", "world_fr" y "world_ch". A continuación, tendríamos a toosend una versión localizada de hello world noticias tooeach estas etiquetas. En este tema se utilizan proliferación de hello tooavoid de plantillas de etiquetas y el requisito de Hola de enviar varios mensajes.

En un nivel alto, las plantillas son una manera toospecify cómo un dispositivo específico debe recibir una notificación. plantilla de Hello especifica el formato de carga exacto de hello consultando tooproperties que forman parte del mensaje de saludo enviado por el back-end de la aplicación. En nuestro caso, enviaremos un mensaje independiente de la configuración regional que contiene todos los idiomas compatibles:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

A continuación, se garantizará que los dispositivos se registren con una plantilla que hace referencia la propiedad correcta toohello. Por ejemplo, una aplicación de iOS que quiere tooregister para francés noticias registrará siguiente hello:

    {
        aps:{
            alert: "$(News_French)"
        }
    }

Las plantillas son una característica muy eficaz de la que puede obtener más información en nuestro artículo [Plantillas](notification-hubs-templates-cross-platform-push-messages.md) .

## <a name="hello-app-user-interface"></a>interfaz de usuario de aplicación Hola
Ahora modificaremos aplicación de noticias de última hora de hello que creó en el tema de hello [toosend de centros de notificaciones utilice noticias de última hora] toosend adaptado mediante plantillas de noticias de última hora.

En su MainStoryboard_iPhone.storyboard, agregue un Control segmentados con lenguajes de hello tres que se admitirán: inglés, francés y mandarín.

![][13]

A continuación, realice tooadd seguro un IBOutlet en su ViewController.h tal y como se muestra a continuación:

![][14]

## <a name="building-hello-ios-app"></a>Aplicación de iOS de hello de creación
1. En su Notification.h agregue hello *retrieveLocale* método y modificar el almacén de Hola y suscribirse a métodos tal y como se muestra a continuación:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    En su Notification.m, modifique hello *storeCategoriesAndSubscribe* método agregando el parámetro de configuración regional de Hola y almacenándolo en hello valores predeterminados del usuario:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    A continuación, modificar hello *suscribirse* configuración regional de método tooinclude hello:
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    Tenga en cuenta cómo ahora estamos utilizando método hello *registerTemplateWithDeviceToken*, en lugar de *registerNativeWithDeviceToken*. Cuando se registra para una plantilla tenemos plantilla json de tooprovide hello y también el nombre de plantilla de Hola (como nuestra aplicación conviene tooregister diferentes plantillas). Asegúrese de tooregister seguro sus categorías como etiquetas, puesto que queremos toomake seguro tooreceive hello notifciations para las noticias.
   
    Agregar una configuración regional de método tooretrieve Hola de valores predeterminados del usuario hello:
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. Ahora que hemos modificado nuestra clase notificaciones, tenemos toomake seguro de que nuestros ViewController hace uso de hello UISegmentControl nuevo. Agregar Hola línea siguiente en hello *viewDidLoad* método toomake seguro tooshow Hola configuración regional que está seleccionado actualmente:
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    A continuación, en su *suscribirse* (método), cambiar su llamada toohello *storeCategoriesAndSubscribe* toohello siguiente:
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. Por último, tener hello tooupdate *didRegisterForRemoteNotificationsWithDeviceToken* método en su AppDelegate.m, por lo que puede actualizar correctamente el registro cuando se inicia la aplicación. Cambiar la llamada toohello *suscribirse* método de notificaciones con siguiente hello:
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a>(Opcional) Envíe notificaciones de plantillas localizadas desde la aplicación de consola .NET.
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a>(opcional) Enviar notificaciones de plantilla localizada desde dispositivo Hola
Si no dispone de acceso tooVisual Studio o desea enviar notificaciones de la plantilla de hello adaptado directamente desde la aplicación hello en dispositivo Hola de prueba de toojust.  También puede simple agregar toohello de parámetros de plantilla de hello adaptado `SendNotificationRESTAPI` método definido en el tutorial anterior Hola.

        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];

            NSString *json;

            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];

            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];

            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];

            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];

            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];

            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];

            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];

            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];

            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];

            [dataTask resume];
        }




## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre el uso de plantillas, consulte:

* [Notificación a los usuarios con los Centros de notificaciones de Azure: ASP.NET]
* [Notificación a los usuarios con los Centros de notificaciones de Azure: Servicios móviles]

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[toosend de centros de notificaciones utilice noticias de última hora]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notificación a los usuarios con los Centros de notificaciones de Azure: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notificación a los usuarios con los Centros de notificaciones de Azure: Servicios móviles]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
