---
title: aaaNotification Tutorial importantes de noticias de concentradores - iOS
description: "Obtenga información acerca de cómo toouse centros de notificaciones de Bus de servicio de Azure toosend principales de dispositivos de tooiOS de notificaciones de noticias."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Usar toosend centros de notificaciones noticias de última hora
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Información general
Este tema muestra cómo toouse centros de notificaciones de Azure toobroadcast importantes noticias notificaciones tooan aplicación de iOS. Cuando haya finalizado, se puede tooregister puede romper la categorías de noticias que le interesen y recibir notificaciones de inserción solo para esas categorías. Este escenario es un patrón común para muchas aplicaciones donde las notificaciones tienen toogroups toobe enviado de los usuarios que previamente se han declarado el interés en ellos, por ejemplo, aplicaciones de ventiladores de música, etcetera, lector RSS.

Escenarios de difusión se habilitan mediante la inclusión de uno o varios *etiquetas* al crear un registro en el centro de notificaciones de Hola. Cuando se envían las notificaciones tooa etiqueta, todos los dispositivos que se han registrado para la etiqueta de hello recibirá notificación de Hola. Dado que las etiquetas son simplemente cadenas, no tiene toobe aprovisionado de antemano. Para obtener más información acerca de las etiquetas, consulte demasiado[notificación centros de enrutamiento y expresiones de etiqueta](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Requisitos previos
En este tema se basa en la aplicación hello que creó en [empezar a trabajar con los centros de notificaciones][get-started]. Antes de comenzar este tutorial, debe haber completado la [Introducción a Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Agregar categoría selección toohello aplicación
Hola primer paso es tooadd Hola UI elementos tooyour guión gráfico existente que permiten Hola usuario tooselect categorías tooregister. categorías de Hello seleccionadas por el usuario se almacenan en el dispositivo de Hola. Cuando se inicia la aplicación hello, se crea un registro de dispositivos en el centro de notificaciones con las categorías de hello seleccionado como etiquetas.

1. En su MainStoryboard_iPhone.storyboard agregue Hola de los componentes siguientes de la biblioteca de objetos de hello:
   
   * Una etiqueta con el texto "Breaking News",
   * Etiquetas con los textos de categoría "World", "Politics", "Business", "Technology", "Science", "Sports",
   * Seis modificadores, uno por cada categoría, establezca cada conmutador **estado** toobe **desactivar** de forma predeterminada.
   * Un botón etiquetado con "Subscribe"
     
     El guión gráfico debe tener el aspecto siguiente:
     
     ![][3]
2. En el editor de Asistente de hello, cree las salidas de todos los conmutadores de Hola y llamarlos "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"
3. Cree una Acción para el botón con nombre "subscribe". El ViewController.h debe contener grupos Hola siguientes:
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. Cree una nueva **clase Cocoa Touch** denominada `Notifications`. Copie Hola después el código de sección de la interfaz de Hola de archivo hello Notifications.h:
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. Agregue Hola después tooNotifications.m la directiva de importación:
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. Copie Hola después el código en la sección de implementación de Hola de archivo hello Notifications.m.
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    Esta clase usa almacenamiento local toostore y recuperar las categorías de Hola de noticias que van a recibir este dispositivo. Además, contiene un tooregister de método para estas categorías mediante un [plantilla](notification-hubs-templates-cross-platform-push-messages.md) registro.

1. En el archivo de AppDelegate.h hello, agregue una instrucción import para Notifications.h y agregar una propiedad de una instancia de clase de las notificaciones de hello:
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. Hola **didFinishLaunchingWithOptions** método AppDelegate.m, agregar Hola código tooinitialize Hola notificaciones instancia a partir del método hello Hola.  
   
    `HUBNAME`y `HUBLISTENACCESS` (definido en hubinfo.h) ya debe disponer de hello `<hub name>` y `<connection string with listen access>` marcadores de posición se reemplazan con la notificación concentrador hello y nombre de cadena de conexión para *DefaultListenSharedAccessSignature*que ha obtenido antes
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > Dado que las credenciales que se distribuyen con una aplicación cliente no son generalmente seguras, debe distribuir solo clave hello para el acceso de escucha con la aplicación cliente. Escuchar habilita el acceso que no se puede modificar su tooregister de aplicación para notificaciones, pero los registros existentes y no se enviarán las notificaciones. clave de acceso completa de Hola se usa en un servicio seguro back-end para enviar notificaciones y cambiar los registros existentes.
   > 
   > 
3. Hola **didRegisterForRemoteNotificationsWithDeviceToken** método en AppDelegate.m, reemplace el código de hello en método hello con hello después de la clase de código toopass hello dispositivo toohello token las notificaciones. clase de notificaciones de Hello llevará a cabo Hola registrarse para recibir notificaciones con las categorías de Hola. Si el usuario de hello cambia las selecciones de categorías, llamamos a hello `subscribeWithCategories` método en respuesta toohello **suscribirse** tooupdate botón ellos.
   
   > [!NOTE]
   > Dado que puede cambiar símbolo (token) de dispositivo de hello asignado por el servicio de notificación de inserción de Apple (APNS) de Hola en cualquier momento, se deben registrar para notificaciones con frecuencia tooavoid errores de notificación. En este ejemplo se registra para la notificación cada vez que inicia la aplicación hello. Para las aplicaciones que se ejecutan con frecuencia, más de una vez al día, puede probablemente Omitir ancho de banda de registro toopreserve si ha pasado menos de un día desde el registro de hello anterior.
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    Tenga en cuenta que en este momento no debería haber ningún otro código en hello **didRegisterForRemoteNotificationsWithDeviceToken** método.

1. Hello métodos siguientes deben estar ya presentes en AppDelegate.m complete hello [empezar a trabajar con los centros de notificaciones] [ get-started] tutorial.  De lo contrario, agréguelos.
   
    -(void) MessageBox:(NSString *) título mensaje:(NSString *) messageText {}
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * aplicación (void):(UIApplication *) aplicación didReceiveRemoteNotification: (NSDictionary *) información de usuario {NSLog (@"% @", información de usuario);   [mensaje self MessageBox:@"Notification": [valueForKey:@"alert [información de usuario objectForKey:@"aps"]"]]; }
   
   Este método controla las notificaciones que recibe cuando se está ejecutando, mostrando una sencilla aplicación hello **UIAlert**.
2. En ViewController.m, agregue una instrucción de importación para hello AppDelegate.h y copiar después el código en hello genera XCode **suscribirse** método. Este código actualizará Hola notificación registro toouse Hola nuevas etiquetas de categoría Hola usuario ha elegido en la interfaz de usuario de Hola.
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   Este método crea un **NSMutableArray** de categorías y se utiliza hello **notificaciones** lista de clases toostore Hola Hola local almacenamiento registros Hola correspondiente etiquetas y con el centro de notificaciones. Cuando se cambian las categorías, se vuelve a crear el registro de hello con nuevas categorías de Hola.
3. En ViewController.m, agregue Hola después el código de hello **viewDidLoad** interfaz de usuario de método tooset Hola basadas en categorías de hello guardado previamente.

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



aplicación Hello ahora puede almacenar un conjunto de categorías en hello dispositivo almacenamiento local usa tooregister con el centro de notificaciones de hello cada vez que inicia la aplicación hello.  usuario de Hello puede cambiar la selección de Hola de categorías en tiempo de ejecución y haga clic en hello **suscribirse** registro de hello tooupdate de método para dispositivo Hola. A continuación, actualizará Hola Hola de toosend aplicación importantes notificaciones de noticias directamente en la propia aplicación Hola.

## <a name="optional-sending-tagged-notifications"></a>(Opcional) Envío de notificaciones con etiquetas
Si no tienes acceso tooVisual Studio, puede omitir la sección siguiente toohello y enviar notificaciones desde la propia aplicación Hola. También puede enviar notificación de plantilla adecuados de Hola de hello [Portal clásico de Azure] usando pestaña de depuración de hello en el centro de notificaciones. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a>(opcional) Enviar notificaciones de dispositivo de Hola
Normalmente se enviaría notificaciones por un servicio back-end, pero puede enviar notificaciones de noticias de separación directamente desde la aplicación hello. toodo esto actualizaremos hello `SendNotificationRESTAPI` método que hemos definido en hello [empezar a trabajar con los centros de notificaciones] [ get-started] tutorial.

1. Hola de actualización de ViewController.m `SendNotificationRESTAPI` método como sigue para que acepta un parámetro para la etiqueta de categoría de Hola y las envía Hola apropiado [plantilla](notification-hubs-templates-cross-platform-push-messages.md) notificación.
   
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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
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
2. Hola de actualización de ViewController.m **enviar notificación** acción tal como se muestra en el código de hello que sigue. Para que envíe notificaciones de hello utilizando cada etiqueta de forma individual y enviar toomultiple plataformas.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. Recompile el proyecto y asegúrese de que no haya errores de compilación.

## <a name="run-hello-app-and-generate-notifications"></a>Ejecutar aplicación hello y generar notificaciones
1. Presione Hola ejecutar botón toobuild Hola proyecto y de iniciar la aplicación hello. Seleccione algunos tooand de toosubscribe de opciones de separación de noticias, a continuación, presione hello **suscribir** botón. Debería ver un cuadro de diálogo que indica hello las notificaciones se han suscrito.
   
    ![][1]
   
    Cuando eliges **suscribir**, Hola Hola seleccionado categorías de aplicación se convierte en etiquetas y solicita un nuevo registro de dispositivo para etiquetas de hello seleccionada del centro de notificaciones de Hola.
2. Escriba un toobe de mensaje enviado como noticias de última hora, a continuación, presione hello **enviar notificación** botón. También puede ejecutar las notificaciones toogenerate de aplicación de hello .NET consola.
   
    ![][2]
3. Cada noticias de toobreaking dispositivo suscrito recibirá notificaciones de noticias de separación de hello que acabamos de enviar.

## <a name="next-steps"></a>Pasos siguientes
En este tutorial hemos visto cómo toobroadcast noticias de última hora por categoría. Considere la posibilidad de completar uno de hello tutoriales que indican errores de otros escenarios avanzados de centros de notificaciones:

* **[Utilice noticias de última hora de toobroadcast localizado de los centros de notificaciones]**
  
    Obtenga información acerca de cómo hello tooexpand interrumpir el envío de noticias aplicación tooenable localizar las notificaciones.

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Utilice noticias de última hora de toobroadcast localizado de los centros de notificaciones]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[Portal clásico de Azure]: https://manage.windowsazure.com
