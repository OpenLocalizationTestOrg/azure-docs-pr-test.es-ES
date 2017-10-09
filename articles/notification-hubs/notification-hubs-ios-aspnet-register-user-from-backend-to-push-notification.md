---
title: "usuario actual de hello aaaRegister para las notificaciones de inserción a través de Web API | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorequest Insertar registro de notificaciones en una aplicación de iOS con centros de notificaciones de Azure cuando se realiza registro por la API Web de ASP.NET."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a>Registrar al usuario actual de hello las notificaciones de inserción mediante ASP.NET
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a>Información general
Este tema muestra cómo toorequest Insertar registro de notificaciones con centros de notificaciones de Azure cuando el registro se realiza por la API Web de ASP.NET. Este tema amplían tutorial Hola [notificar a los usuarios con centros de notificaciones]. Debe haber completado pasos Hola necesario en ese servicio móvil de toocreate tutorial Hola autenticado. Para obtener más información sobre Hola notificar al escenario de los usuarios, consulte [notificar a los usuarios con centros de notificaciones].

## <a name="update-your-app"></a>Actualización de la aplicación
1. En su MainStoryboard_iPhone.storyboard, agregue Hola de los componentes siguientes de la biblioteca de objetos de hello:
   
   * **Etiqueta**: "TooUser con centros de notificaciones de inserción"
   * **Etiqueta**: "InstallationId"
   * **Etiqueta**: "User"
   * **Campo de texto**: "User"
   * **Etiqueta**: "Password"
   * **Campo de texto**: "Password"
   * **Botón**: "Login"
     
     En este momento, el guión gráfico Hola siguiente aspecto:
     
      ![][0]
2. En el editor de Asistente de hello, crear las salidas de todos los controles de hello cambiado y llamarlos, conectar los campos de texto hello con hello View-Controller (delegado) y crear un **acción** para hello **inicio de sesión** botón.
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. Cree una clase denominada **DeviceInfo**, y Hola copia siguiendo el código en la sección de la interfaz de Hola de archivo hello DeviceInfo.h:
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. Copie Hola después el código de sección de implementación de Hola de archivo de hello DeviceInfo.m:
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store hello install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. En PushToUserAppDelegate.h, agregue Hola después singleton de propiedad:
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. Hola **didFinishLaunchingWithOptions** método PushToUserAppDelegate.m, agregar Hola siguiente código:
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    primera línea de Hello inicializa hello **DeviceInfo** singleton. Hola segunda línea inicia Hola registro para las notificaciones de inserción, que ya está presente es ya completados hello [empezar a trabajar con los centros de notificaciones] tutorial.
7. En PushToUserAppDelegate.m, implemente el método hello **didRegisterForRemoteNotificationsWithDeviceToken** en su AppDelegate y agregue el siguiente código de hello:
   
        self.deviceInfo.deviceToken = deviceToken;
   
    Esto establece el token del dispositivo Hola para solicitud de Hola.
   
   > [!NOTE]
   > En este punto, no debería haber ningún otro código en este método. Si ya tiene una llamada toohello **registerNativeWithDeviceToken** método que se agregó al completar hello [empezar a trabajar con los centros de notificaciones](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial debe Comente o quite que llamar a.
   > 
   > 
8. En archivo de PushToUserAppDelegate.m de hello, agregue Hola siguiendo el método de controlador:
   
   * información de usuario de aplicación (void):(UIApplication *) aplicación didReceiveRemoteNotification:(NSDictionary *) {NSLog (@"% @", información de usuario);   UIAlertView * alerta = [[UIAlertView alloc] initWithTitle:@"Notification" mensaje: [información de usuario objectForKey:@"inAppMessage]" delegado: nil cancelButtonTitle: @ otherButtonTitles:nil "Aceptar", nulo];   [Mostrar alerta]; }
   
   Este método muestra una alerta en la interfaz de usuario de hello cuando la aplicación recibe notificaciones mientras se está ejecutando.
9. Abrir archivo de PushToUserViewController.m hello y teclado Hola devuelto en hello después de la implementación:
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. Hola **viewDidLoad** método hello PushToUserViewController.m archivo, inicializar etiqueta installationId de hello como sigue:
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. Agregue Hola propiedades de interfaz en PushToUserViewController.m siguientes:
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. A continuación, agregue Hola después de la implementación:
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. Copia Hola siguiente de código en hello **inicio de sesión** método de controlador creado por XCode:
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    Este método obtiene un identificador de instalación y el canal de notificaciones de inserción y lo envía, junto con el tipo de dispositivo de hello, toohello autentica el método API de Web que crea un registro en los centros de notificaciones. Esta API web se definió en [notificar a los usuarios con centros de notificaciones].

Ahora que hello aplicación cliente se ha actualizado, devolver toohello [notificar a los usuarios con centros de notificaciones] y actualizar notificaciones de toosend de hello servicio móvil con centros de notificaciones.

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[notificar a los usuarios con centros de notificaciones]: /manage/services/notification-hubs/notify-users-aspnet

[empezar a trabajar con los centros de notificaciones]: /manage/services/notification-hubs/get-started-notification-hubs-ios
