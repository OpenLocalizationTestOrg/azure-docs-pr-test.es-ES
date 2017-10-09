---
title: "aaaAzure notificación concentradores Rich Push"
description: "Obtenga información acerca de cómo toosend enriquecido push aplicación de iOS de tooan de notificaciones de Azure. Ejemplos de código escritos en Objective-C y C#."
documentationcenter: ios
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: 590304df-c0a4-46c5-8ef5-6a6486bb3340
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5432d8bf47777371bea3521a0c0176ade75fbd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-rich-push"></a>Inserción enriquecida de los Centros de notificaciones de Azure
## <a name="overview"></a>Información general
En orden tooengage a los usuarios con contenido enriquecido instantánea, una aplicación podría querer toopush más allá de texto sin formato. Estas notificaciones promueven las interacciones de los usuarios y presentan contenido como direcciones URL, sonidos, imágenes o cupones y más. Este tutorial se basa en hello [informar a los usuarios](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tema y muestra cómo toosend insertar las notificaciones que incorporan cargas (por ejemplo, imagen).

Este tutorial es compatible con iOS 7 y 8.

  ![][IOS1]

En un alto nivel:

1. Hola aplicación back-end:
   * Almacenes de Hola carga enriquecida (en este caso, la imagen) en almacenamiento de base de datos o local de back-end de Hola
   * Envía el Id. de este dispositivo de notificación enriquecido toohello
2. Aplicación Hola dispositivo:
   * Contactos Hola solicitando la carga enriquecido Hola con el Id. de hello recibe de back-end
   * Envía notificaciones a los usuarios en el dispositivo de hello cuando se completa la recuperación de datos y muestra la carga de hello inmediatamente cuando los usuarios pulsan toolearn más

## <a name="webapi-project"></a>Proyecto WebAPI
1. En Visual Studio, abra hello **AppBackend** proyecto que creó en hello [informar a los usuarios](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.
2. Obtener una imagen que desee toonotify a los usuarios y colocarla en un **img** carpeta en el directorio del proyecto.
3. Haga clic en **mostrar todos los archivos** en hello en el Explorador de soluciones y haga clic en carpeta de hello demasiado**incluir en el proyecto**.
4. Con la imagen de hello seleccionada, cambiar su acción de compilación en la ventana Propiedades también**recurso incrustado**.
   
    ![][IOS2]
5. En **Notifications.cs**, agregue Hola siguiente instrucción using:
   
        using System.Reflection;
6. Hola de actualización completa **notificaciones** clase con el siguiente código de hello. Ser tooreplace seguro de los marcadores de posición de hello con sus credenciales de base de datos central de notificaciones y el nombre de archivo de imagen.
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message toodisplay toousers
            public string Message { get; set; }
            // Type of rich payload (developer-defined)
            public string RichType { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }
   
        public class Notifications {
            public static Notifications Instance = new Notifications();
   
            private List<Notification> notifications = new List<Notification>();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                // Placeholders: replace with hello connection string (with full access) for your notification hub and hello hub name from hello Azure Classics Portal
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",  "{hub name}");
            }
   
            public Notification CreateNotification(string message, string richType, string payload) {
                var notification = new Notification() {
                    Id = notifications.Count,
                    Message = message,
                    RichType = richType,
                    Payload = payload,
                    Read = false
                };
   
                notifications.Add(notification);
   
                return notification;
            }
   
            public Stream ReadImage(int id) {
                var assembly = Assembly.GetExecutingAssembly();
                // Placeholder: image file name (for example, logo.png).
                return assembly.GetManifestResourceStream("AppBackend.img.{logo.png}");
            }
        }
   
   > [!NOTE]
   > (opcional) Consulte demasiado[cómo tooembed y acceder a recursos con Visual C#](http://support.microsoft.com/kb/319292) para obtener más información acerca de cómo tooadd y obtener los recursos del proyecto.
   > 
   > 
7. En **NotificationsController.cs**, volver a definir **NotificationsController** con hello siguientes fragmentos de código. Esto envía un toodevice de Id. de la notificación inicial silenciosa enriquecida y permite la recuperación de cliente de imagen:
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) tooclient
        public async Task<HttpResponseMessage> Post() {
            // Replace hello placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification tooapns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. Ahora se implementará volver a este sitio Web de Azure de tooan de aplicación en orden toomake, accesible desde todos los dispositivos. Haga doble clic en hello **AppBackend** de proyecto y seleccione **publicar**.
9. Seleccione Sitio web Azure como destino de publicación. Inicie sesión con su cuenta de Azure y seleccione un sitio Web nuevo o existente y tome nota de hello **dirección URL de destino** propiedad Hola **conexión** ficha. Nos referiremos toothis URL según su *punto de conexión de back-end* más adelante en este tutorial. Haga clic en **Publicar**.

## <a name="modify-hello-ios-project"></a>Modificar el proyecto de iOS de Hola
Ahora que ha modificado su Hola solo de aplicación back-end toosend *identificador* de una notificación, se cambia su toohandle de aplicación de iOS ese identificador y recuperar mensajes enriquecido Hola desde el back-end.

1. Abra el proyecto de iOS y habilitar las notificaciones de remotas que va de destino principal de la aplicación tooyour en hello **destinos** sección.
2. Haga clic en **capacidades**, activar **modos en segundo plano**y compruebe hello **notificaciones remoto** casilla de verificación.
   
    ![][IOS3]
3. Vaya demasiado**Main.storyboard**y asegúrese de que tiene un controlador de vista (usan tooas inicio View-Controller en este tutorial) desde [notificar al usuario](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.
4. Agregar un **controlador navegación** tooyour de guión gráfico y arrastre control tooHome View Controller toomake lo Hola **raíz vista** de navegación. Asegúrese de hello seguro **es View-Controller inicial** en atributos inspector está seleccionado para hello controlador de navegación.
5. Agregar un **View Controller** toostoryboard y agregue un **imagen de vista**. Se trata de página Hola los usuarios verán cuando deciden toolearn más haciendo clic en notifiication Hola. El guión gráfico debe tener el aspecto siguiente:
   
    ![][IOS4]
6. Haga clic en hello **inicio View Controller** en el guión gráfico y asegúrese de que tiene **homeViewController** como su **clase personalizada** y **Id. de guión gráfico**en inspector de identidad de Hola.
7. Hola mismo controlador de vista de imagen como **imageViewController**.
8. A continuación, cree una nueva clase de controlador de vista denominada **imageViewController** toohandle Hola interfaz de usuario que acaba de crear.
9. En **imageViewController.h**, agregar Hola siguientes declaraciones de interfaz del controlador de toohello. Asegúrese de arrastrar toocontrol seguro desde Hola guión gráfico imagen Vista toothese propiedades toolink Hola dos:
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. En **imageViewController.m**, agregue siguiente Hola final Hola de **viewDidload**:
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. En **AppDelegate.m**, controlador de imagen de Hola de importación que creó:
    
        #import "imageViewController.h"
12. Agregue una sección de la interfaz con hello siguiente declaración:
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. En **AppDelegate**, asegúrese de que la aplicación registra notificaciones silenciosas en **application: didFinishLaunchingWithOptions**:
    
        // Software version
        self.iOS8 = [[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)] && [[UIApplication sharedApplication] respondsToSelector:@selector(registerForRemoteNotifications)];
    
        // Register for remote notifications for iOS8 and previous versions
        if (self.iOS8) {
            NSLog(@"This device is running with iOS8.");
    
            // Action
            UIMutableUserNotificationAction *richPushAction = [[UIMutableUserNotificationAction alloc] init];
            richPushAction.identifier = @"richPushMore";
            richPushAction.activationMode = UIUserNotificationActivationModeForeground;
            richPushAction.authenticationRequired = NO;
            richPushAction.title = @"More";
    
            // Notification category
            UIMutableUserNotificationCategory* richPushCategory = [[UIMutableUserNotificationCategory alloc] init];
            richPushCategory.identifier = @"richPush";
            [richPushCategory setActions:@[richPushAction] forContext:UIUserNotificationActionContextDefault];
    
            // Notification categories
            NSSet* richPushCategories = [NSSet setWithObjects:richPushCategory, nil];

            UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                    UIUserNotificationTypeAlert |
                                                    UIUserNotificationTypeBadge
                                                                                     categories:richPushCategories];

            [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
            [[UIApplication sharedApplication] registerForRemoteNotifications];

        }
        else {
            // Previous iOS versions
            NSLog(@"This device is running with iOS7 or earlier versions.");

            [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
        }

        return YES;

1. Sustituirlas Hola después de la implementación de **aplicación: didRegisterForRemoteNotificationsWithDeviceToken** guión gráfico de hello tootake cambia de interfaz de usuario en cuenta:
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. A continuación, agregue Hola siguiendo métodos demasiado**AppDelegate.m** tooretrieve Hola imagen desde el punto de conexión y enviar una notificación local una vez completada la recuperación. Asegúrese de marcador de posición de seguro toosubstitute hello `{backend endpoint}` con su punto de conexión de back-end:
   
       NSString *const GetNotificationEndpoint = @"{backend endpoint}/api/notifications";
   
       // Helper: retrieve notification content from backend with rich notification id
       - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion {
           UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
           homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
           NSString* authenticationHeader = hvc.registerClient.authenticationHeader;
           // Check if authenticated
           if (!authenticationHeader) return;
   
           NSURLSession* session = [NSURLSession
                                    sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                    delegate:nil
                                    delegateQueue:nil];
   
           NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, richId]];
           NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
           [request setHTTPMethod:@"GET"];
           NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
           [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
   
           NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
   
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
               if (!error && httpResponse.statusCode == 200) {
                   // From NSData tooUIImage
                   self.imagePayload = [UIImage imageWithData:data];
   
                   completion(nil);
               }
               else {
                   NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                   if (error)
                       completion(error);
                   else {
                       completion([NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                   }
               }
           }];
           [dataTask resume];
       }
   
       // Handle silent push notifications when id is sent from backend
       - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler {
           self.userInfo = userInfo;
           int richId = [[self.userInfo objectForKey:@"richId"] intValue];
           NSString* richType = [self.userInfo objectForKey:@"richType"];
   
           // Retrieve image data
           if ([richType isEqualToString:@"img"]) {  
               [self retrieveRichImageWithId:richId completion:^(NSError* error) {
                   if (!error){
                       // Send local notification
                       UILocalNotification* localNotification = [[UILocalNotification alloc] init];
   
                       // "5" is arbitrary here toogive you enough time tooquit out of hello app and receive push notifications
                       localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:5];
                       localNotification.userInfo = self.userInfo;
                       localNotification.alertBody = [self.userInfo objectForKey:@"richMessage"];
                       localNotification.timeZone = [NSTimeZone defaultTimeZone];
   
                       // iOS8 categories
                       if (self.iOS8) {
                           localNotification.category = @"richPush";
                       }
   
                       [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                       handler(UIBackgroundFetchResultNewData);
                   }
                   else{
                       handler(UIBackgroundFetchResultFailed);
                   }
               }];
           }
           // Add "else if" here toohandle more types of rich content such as url, sound files, etc.
       }
3. Controlar la notificación local de hello anteriormente abriendo el controlador de vista de imagen de hello en **AppDelegate.m** con hello siguientes métodos:
   
       // Helper: redirect users tooimage view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image tooimage view controller
           imgViewController.imagePayload = img;
   
           // Redirect
           [navigationController pushViewController:imgViewController animated:YES];
       }
   
       // Handle local notification sent above in didReceiveRemoteNotification
       - (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
           if (application.applicationState == UIApplicationStateActive) {
               // Show in-app alert with an extra "more" button
               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:notification.alertBody delegate:self cancelButtonTitle:@"OK" otherButtonTitles:@"More", nil];
   
               [alert show];
           }
           // App becomes active from user's tap on notification
           else {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
       }
   
       // Handle buttons in in-app alerts and redirect with data/image
       - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
           // Handle "more" button
           if (buttonIndex == 1)
           {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           // Add "else if" here toohandle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-hello-application"></a>Ejecutar aplicación Hola
1. En XCode, ejecute la aplicación hello en un dispositivo de E/s físicas (inserción notificaciones no funcionará en el simulador de hello).
2. En la aplicación de iOS de hello interfaz de usuario, escriba un nombre de usuario y una contraseña de hello mismo valor para la autenticación y haga clic en **inicio de sesión**.
3. Haga clic en **Enviar inserción** y deberá ver una alerta en la aplicación. Si hace clic en **más**, podrá imagen toohello poner eligió tooinclude en el back-end de aplicación.
4. También puede hacer clic en **enviar inserción** e inmediatamente presione el botón de inicio de hello del dispositivo. En unos momentos recibirá una notificación de inserción. Si puntear en él o haga clic en más, se encontrarán tooyour hello y aplicación de contenido de imagen enriquecido.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
