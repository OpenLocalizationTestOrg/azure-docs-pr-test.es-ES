---
title: "aaaAzure los usuarios notificar a los centros de notificación para iOS con back-end de .NET"
description: "Obtenga información acerca de cómo toosend push toousers de notificaciones en Azure. Ejemplos de código escritos en Objective C y hello API de .NET para hello back-end."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a>Los Centros de notificaciones de Azure notifican a los usuarios para iOS con back-end de .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Información general
Compatibilidad de la notificación de inserción en Azure permite tooaccess una fácil de usar, multiplataforma y la infraestructura de inserción de escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa para dispositivos móviles plataformas. Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push usuario de aplicación específica de tooa de notificaciones en un dispositivo específico. Un back-end de ASP.NET WebAPI es tooauthenticate usa clientes y las notificaciones de toogenerate, como se muestra en el tema de la Guía de hello [registrar desde su aplicación de back-end](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).

> [!NOTE]
> Este tutorial asume que ha creado y configurado el centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md). Este tutorial también es toohello de requisitos previos de hello [seguros de inserción (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.
> Si desea toouse Mobile aplicaciones como el servicio back-end, vea hello [Mobile Apps empezar a trabajar con inserción](../app-service-mobile/app-service-mobile-ios-get-started-push.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a>Modificación de la aplicación iOS
1. Abra Hola única página ver la aplicación que creó en hello [Introducción a centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.
   
   > [!NOTE]
   > En esta sección asumimos que configuró el proyecto con un nombre de organización vacío. De lo contrario, deberá tooprepend los nombres de clase de tooall de nombre de organización.
   > 
   > 
2. En su Main.storyboard agregar componentes de Hola que se muestra en la captura de pantalla de hello debajo de la biblioteca de objetos de Hola.
   
    ![][1]
   
   * **Nombre de usuario**: UITextField de A con el texto de marcador de posición, *escriba el nombre de usuario*, inmediatamente debajo de hello enviar etiqueta results y restringida toohello dejados y los márgenes de la derecha y debajo de Hola enviar etiqueta de resultados.
   * **Contraseña**: UITextField de A con el texto de marcador de posición, *escribir la contraseña*, inmediatamente debajo Hola campo de texto Nombre de usuario y toohello restringida izquierda y a la derecha de los márgenes y por debajo del campo de texto Nombre de usuario de Hola. Comprobar hello **proteger la entrada de texto** opción Hola Inspector de atributo, en *devolver clave*.
   * **Inicie sesión**: UIButton A la etiqueta inmediatamente debajo del campo de texto de contraseña de Hola y desactive la opción hello **habilitado** opción Hola Inspector de atributos, en *contenido del Control*
   * **WNS**: etiqueta y el envío de conmutador tooenable Hola notificación del servicio de notificación de Windows si han pasado el programa de instalación en el concentrador de Hola. Vea hello [Introducción a Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.
   * **GCM**: etiqueta y el envío de conmutador tooenable Hola tooGoogle de notificación de mensajería en la nube si han pasado el programa de instalación en el concentrador de Hola. Consulte el tutorial [introductorio de Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .
   * **APN**: etiqueta y el envío de conmutador tooenable Hola notificación toohello servicio de notificación de plataforma de Apple.
   * **Recipent Username**: UITextField de A con el texto de marcador de posición, *etiqueta de nombre de usuario de destinatario*, inmediatamente debajo de hello GCM etiquetar y restringida toohello izquierdo y derecho márgenes y debajo de hello GCM etiquetar.

    Se agregaron algunos componentes en hello [Introducción a centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.

1. **CTRL** arrastre desde componentes de hello en hello vista tooViewController.h y agregue estas nuevas salidas.
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. En ViewController.h, agregue el siguiente hello `#define` justo debajo de las instrucciones de importación. Hola sustituto *< escriba el extremo de back-end\>*  marcador de posición con hello usa toodeploy el back-end de aplicación en la sección anterior de Hola de dirección URL de destino. Por ejemplo, *http://you_backend.azurewebsites.net*.
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. En el proyecto, cree un nuevo **cacao Touch clase** denominado **RegisterClient** toointerface con hello ASP.NET back-end que creó. Crear clase de Hola que hereda de `NSObject`. A continuación, agregue Hola después el código de hello RegisterClient.h.
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. Hola RegisterClient.m actualizar hello `@interface` sección:
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. Reemplace hello `@implementation` sección Hola RegisterClient.m con el siguiente código de hello.

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    código de Hello anterior implementa la lógica de hello explicado en el artículo de guía de hello [registrar desde su aplicación de back-end](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) con NSURLSession tooperform REST llama backend de la aplicación de tooyour y NSUserDefaults toolocally almacén Hola Identificador devuelto por el centro de notificaciones de Hola.

    Tenga en cuenta que esta clase requiere la propiedad **authorizationHeader** toobe establecida en orden toowork correctamente. Esta propiedad se establece por hello **ViewController** tras Hola del registro la clase.

1. En ViewController.h, agregue una instrucción `#import` a RegisterClient.h. A continuación, agregue una declaración para el token del dispositivo de Hola y hacer referencia a tooa `RegisterClient` instancia Hola `@interface` sección:
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. En ViewController.m, agregue una declaración de método privado en hello `@interface` sección:
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> Hello fragmento de código siguiente no es un esquema de autenticación segura, se debe sustituir implementación Hola de hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** con su mecanismo de autenticación concreto genera un toobe de token de autenticación utilizado por hello register clase de cliente, por ejemplo, OAuth, Active Directory.
> 
> 

1. A continuación, en hello `@implementation` sección de ViewController.m agregar Hola después el código que agrega la implementación de Hola para configuración Hola dispositivo símbolo (token) y autenticación de encabezado.
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    Tenga en cuenta cómo el token del dispositivo de configuración Hola permite Hola botón Iniciar sesión. Esto es porque como parte de la acción de inicio de sesión de hello, controlador de vista de hello registra las notificaciones de inserción con back-end de aplicación de Hola. Por lo tanto, no queremos que en el registro de acción toobe accesibles hasta que el token del dispositivo Hola se ha configurado correctamente. Puede desacoplar Hola sesión de registro de inserción de hello como primero Hola se realiza antes que este último Hola.
2. En ViewController.m, usar hello siguiendo el método de acción de fragmentos de código tooimplement Hola para su **inicio de sesión** botón y un método toosend Hola mensaje de notificación utilizando Hola back-end ASP.NET.
   
       - (IBAction) LogInAction: remitente (Id.) {/ / crear el encabezado de autenticación y establecerla en el registro cliente NSString * username = en sí mismo. UsernameField.text;   Contraseña de NSString = en sí mismo. PasswordField.text;
   
           [self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];
   
           __weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken etiquetas: nil andCompletion:^(NSError* error) {Si (! error) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered correctamente!"];});}}];}

        - (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];

            Pasar la etiqueta de pns y el nombre de usuario de hello como parámetros con la dirección URL de REST de hello toohello ASP.NET back-end NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];

            Solicitud de NSMutableURLRequest = [NSMutableURLRequest requestWithURL:requestURL];    [solicitud setHTTPMethod:@"POST"];

            Obtener Hola ficticia authenticationheader de cliente de registro de hello NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [solicitud setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            Agregue el cuerpo del mensaje de notificación de hello [solicitar setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [solicitar setHTTPBody: [mensaje dataUsingEncoding:NSUTF8StringEncoding]];

            Notificación de envío de hello API de REST se ejecuta en hello ASP.NET back-end NSURLSessionDataTask * dataTask = [sesión dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *Error) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) respuesta;        Si (error || httpResponse.statusCode! = 200) {NSString* estado = [NSString stringWithFormat:@"Error estado para % @: % d\nError: %@\n", pns, httpResponse.statusCode, aparece el error];            dispatch_async(dispatch_get_main_queue(), ^ {/ / anexar texto ya que todas las llamadas PNS 3 también pueden tener información tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            }];    [dataTask resume]; }


1. Actualizar la acción de Hola para hello **enviar notificación** botón toouse Hola ASP.NET back-end y enviar tooany PNS gracias a un conmutador.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. En la función **ViewDidLoad**, agregue Hola posterior tooinstantiate hello RegisterClient instancia y establece el delegado de Hola para los campos de texto.
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. Ahora, en **AppDelegate.m**, quitar todo el contenido del método hello hello **aplicación: didRegisterForPushNotificationWithDeviceToken:** y reemplazarlo con hello después toomake seguro que Hola vista controlador contiene hello más reciente dispositivo token recuperado de APNs:
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. Por último, en **AppDelegate.m**, asegúrese de que tienen Hola siguiente método:
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a>Hola aplicación de prueba
1. En XCode, ejecute la aplicación hello en un dispositivo de E/s físicas (inserción notificaciones no funcionará en el simulador de hello).
2. En la aplicación de iOS de hello interfaz de usuario, escriba un nombre de usuario y una contraseña. Pueden ser cualquier cadena, pero ambos deben ser Hola mismo valor de cadena. A continuación, haga clic en **Iniciar sesión**.
   
    ![][2]
3. Debería ver una ventana emergente que le informa del éxito de registro. Haga clic en **Aceptar**.
   
    ![][3]
4. Hola **etiqueta de nombre de usuario de destinatario* texto, escriba la etiqueta de nombre de usuario de hello utilizado con el registro de hello desde otro dispositivo.
5. Escriba un mensaje de notificación y haga clic en **Enviar notificación**.  Solo los dispositivos de Hola que tienen un registro con la etiqueta de nombre de usuario del destinatario de Hola reciban mensaje de notificación de Hola.  Sólo se envía a los usuarios de toothose.
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
