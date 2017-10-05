---
title: Los Centros de notificaciones de Azure notifican a los usuarios para iOS con back-end de .NET
description: "Aprenda a enviar notificaciones push a los usuarios en Azure. Ejemplos de código escritos en Objective-C con la API de .NET."
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
ms.openlocfilehash: 0fa7a886e1ecb0a90b6aebc1dbf9ef0c6ce1acf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="7efa5-104">Los Centros de notificaciones de Azure notifican a los usuarios para iOS con back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="7efa5-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="7efa5-105">Información general</span><span class="sxs-lookup"><span data-stu-id="7efa5-105">Overview</span></span>
<span data-ttu-id="7efa5-106">La compatibilidad con las notificaciones de inserción en Azure le permite tener acceso a una infraestructura multiplataforma y de escalamiento horizontal fácil de usar, que simplifica considerablemente la implementación de notificaciones de inserción tanto en aplicaciones de consumidor, como en aplicaciones empresariales para plataformas móviles.</span><span class="sxs-lookup"><span data-stu-id="7efa5-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="7efa5-107">Este tutorial muestra cómo puede utilizar los Centros de notificaciones de Azure para enviar notificaciones de inserción a un usuario de aplicaciones determinado en un dispositivo concreto.</span><span class="sxs-lookup"><span data-stu-id="7efa5-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="7efa5-108">Un back-end de ASP.NET WebAPI se usa para autenticar clientes y generar notificaciones, tal como se muestra en el tema de referencia [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) (Registro desde el back-end de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="7efa5-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="7efa5-109">Este tutorial asume que ha creado y configurado el centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7efa5-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="7efa5-110">Este tutorial también es el requisito previo para el tutorial [Inserción segura (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="7efa5-110">This tutorial is also the prerequisite to the [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="7efa5-111">Si quiere utilizar Aplicaciones móviles como su servicio back-end, consulte [Incorporación de notificaciones push a la aplicación iOS](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="7efa5-111">If you want to use Mobile Apps as your backend service, see the [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="7efa5-112">Modificación de la aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="7efa5-112">Modify your iOS app</span></span>
1. <span data-ttu-id="7efa5-113">Abra la aplicación de vista de una página que creó en el tutorial [Introducción a los Centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="7efa5-113">Open the Single Page view app you created in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7efa5-114">En esta sección asumimos que configuró el proyecto con un nombre de organización vacío.</span><span class="sxs-lookup"><span data-stu-id="7efa5-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="7efa5-115">Si no es así, debe anteponer el nombre de la organización a todos los nombres de clase.</span><span class="sxs-lookup"><span data-stu-id="7efa5-115">If not, you will need to prepend your organization name to all class names.</span></span>
   > 
   > 
2. <span data-ttu-id="7efa5-116">En Main.storyboard, agregue los componentes mostrados en la captura de pantalla siguiente desde la biblioteca de objetos.</span><span class="sxs-lookup"><span data-stu-id="7efa5-116">In your Main.storyboard add the components shown in the screenshot below from the object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="7efa5-117">**Nombre de usuario**: Campo de texto de la interfaz de usuario con texto de marcador de posición, *Escriba el nombre de usuario*, inmediatamente debajo de la etiqueta de resultados de envío y limitado a los márgenes izquierdo y derecho y por debajo de la etiqueta de envío de resultados.</span><span class="sxs-lookup"><span data-stu-id="7efa5-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath the send results label and constrained to the left and right margins and beneath the send results label.</span></span>
   * <span data-ttu-id="7efa5-118">**Contraseña**: Campo de texto de la interfaz de usuario con texto de marcador de posición, *Escriba la contraseña*, inmediatamente debajo del campo de texto de no nombre de usuario y limitado a los márgenes izquierdo y derecho y por debajo del campo de texto del nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="7efa5-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath the username text field and constrained to the left and right margins and beneath the username text field.</span></span> <span data-ttu-id="7efa5-119">Active la opción **Entrada de texto seguro** en el Inspector de atributos, en *Devolver clave*.</span><span class="sxs-lookup"><span data-stu-id="7efa5-119">Check the **Secure Text Entry** option in the Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="7efa5-120">**Iniciar sesión**: botón de la interfaz de usuario inmediatamente debajo del campo de texto de contraseña y la opción **Habilitado** del Inspector de atributos, debajo de *Control-Content*.</span><span class="sxs-lookup"><span data-stu-id="7efa5-120">**Log in**: A UIButton labeled immediately beneath the password text field and uncheck the **Enabled** option in the Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="7efa5-121">**WNS**: etiqueta y modificador para habilitar el envío de la notificación del Servicio de notificaciones de Windows si se ha instalado en el concentrador.</span><span class="sxs-lookup"><span data-stu-id="7efa5-121">**WNS**: Label and switch to enable sending the notification Windows Notification Service if it has been setup on the hub.</span></span> <span data-ttu-id="7efa5-122">Consulte el tutorial [introductorio de Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="7efa5-122">See the [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="7efa5-123">**GCM**: etiqueta y modificador para habilitar el envío de la notificación a Google Cloud Messaging si se ha instalado en el concentrador.</span><span class="sxs-lookup"><span data-stu-id="7efa5-123">**GCM**: Label and switch to enable sending the notification to Google Cloud Messaging if it has been setup on the hub.</span></span> <span data-ttu-id="7efa5-124">Consulte el tutorial [introductorio de Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="7efa5-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="7efa5-125">**APNS**: etiqueta y modificador para habilitar el envío de la notificación al Servicio de notificaciones de la plataforma Apple.</span><span class="sxs-lookup"><span data-stu-id="7efa5-125">**APNS**: Label and switch to enable sending the notification to the Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="7efa5-126">**Nombre de usuario destinatario**: campo de texto de la interfaz de usuario con texto de marcador de posición, *Etiqueta de nombre de usuario destinatario*, inmediatamente debajo de la etiqueta GCM y limitado a los márgenes izquierdo y derecho y por debajo de la etiqueta GCM.</span><span class="sxs-lookup"><span data-stu-id="7efa5-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath the GCM label and constrained to the left and right margins and beneath the GCM label.</span></span>

    <span data-ttu-id="7efa5-127">Algunos componentes se agregaron al tutorial [Introducción a Centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="7efa5-127">Some components were added in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="7efa5-128">**Ctrl** y arrastre desde los componentes de la vista a ViewController.h y agregue esos nuevos medios.</span><span class="sxs-lookup"><span data-stu-id="7efa5-128">**Ctrl** drag from the components in the view to ViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used to enable the buttons on the UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used to enabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="7efa5-129">En ViewController.h, agregue el `#define` siguiente justo debajo de las instrucciones de importación.</span><span class="sxs-lookup"><span data-stu-id="7efa5-129">In ViewController.h, add the following `#define` just below your import statements.</span></span> <span data-ttu-id="7efa5-130">Sustituya el marcador de posición *<Escriba su punto de conexión de back-end\>* por la URL de destino usada para implementar el back-end de la aplicación en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="7efa5-130">Substitute the *<Enter Your Backend Endpoint\>* placeholder with the Destination URL you used to deploy your app backend in the previous section.</span></span> <span data-ttu-id="7efa5-131">Por ejemplo, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="7efa5-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="7efa5-132">En el proyecto, cree una nueva **clase Cocoa Touch** denominada **RegisterClient** para interactuar con el back-end de ASP.NET que ha creado.</span><span class="sxs-lookup"><span data-stu-id="7efa5-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** to interface with the ASP.NET back-end you created.</span></span> <span data-ttu-id="7efa5-133">Cree la clase que hereda de `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="7efa5-133">Create the class inheriting from `NSObject`.</span></span> <span data-ttu-id="7efa5-134">Después agregue el siguiente código en RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="7efa5-134">Then add the following code in the RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="7efa5-135">En la actualización RegisterClient.m la sección `@interface` :</span><span class="sxs-lookup"><span data-stu-id="7efa5-135">In the RegisterClient.m update the `@interface` section:</span></span>
   
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
5. <span data-ttu-id="7efa5-136">Reemplace la sección `@implementation` en RegisterClient.m con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="7efa5-136">Replace the `@implementation` section in the RegisterClient.m with the following code.</span></span>

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

    <span data-ttu-id="7efa5-137">El código anterior implementa la lógica explicada en el artículo de referencia [Registro desde el back-end de la aplicación](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) usando NSURLSession para realizar llamadas REST al back-end de la aplicación y NSUserDefaults para almacenar localmente del identificador de registro devuelto por el Centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="7efa5-137">The code above implements the logic explained in the guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession to perform REST calls to your app backend, and NSUserDefaults to locally store the registrationId returned by the notification hub.</span></span>

    <span data-ttu-id="7efa5-138">Tenga en cuenta que esta clase requiere que su propiedad **authorizationHeader** esté establecida para que funcione correctamente.</span><span class="sxs-lookup"><span data-stu-id="7efa5-138">Note that this class requires its property **authorizationHeader** to be set in order to work properly.</span></span> <span data-ttu-id="7efa5-139">Esta propiedad la establece la clase **ViewController** después del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="7efa5-139">This property is set by the **ViewController** class after the log in.</span></span>

1. <span data-ttu-id="7efa5-140">En ViewController.h, agregue una instrucción `#import` a RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="7efa5-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="7efa5-141">A continuación, agregue una declaración para el token del dispositivo y haga referencia a una instancia `RegisterClient` en la sección `@interface`:</span><span class="sxs-lookup"><span data-stu-id="7efa5-141">Then add a declaration for the device token and reference to a `RegisterClient` instance in the `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="7efa5-142">En ViewController.m, agregue una declaración del método privado en la sección `@interface` :</span><span class="sxs-lookup"><span data-stu-id="7efa5-142">In ViewController.m, add a private method declaration in the `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create the Authorization header to perform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="7efa5-143">El siguiente fragmento de código no es un esquema de autenticación seguro; debe sustituir la implementación de **createAndSetAuthenticationHeaderWithUsername:AndPassword:** por el mecanismo de autenticación específico que genera un token de autenticación para ser consumido por la clase de cliente del registro, por ejemplo, OAuth, Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7efa5-143">The following snippet is not a secure authentication scheme, you should substitute the implementation of the **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token to be consumed by the register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="7efa5-144">A continuación, en la sección `@implementation` de ViewController.m agregue el siguiente código que agrega la implementación para establecer el encabezado de autenticación y el token del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7efa5-144">Then in the `@implementation` section of ViewController.m add the following code which adds the implementation for setting the device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="7efa5-145">Observe cómo al establecer el token del dispositivo se habilita el botón de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="7efa5-145">Note how setting the device token enables the log in button.</span></span> <span data-ttu-id="7efa5-146">Esto se debe a que, como una parte de la acción de inicio de sesión, el controlador de vista registrará notificaciones de inserción con el back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7efa5-146">This is becasue as a part of the login action, the view controller registers for push notifications with the app backend.</span></span> <span data-ttu-id="7efa5-147">Por lo tanto, no se desea que la acción Iniciar sesión sea accesible hasta que el token del dispositivo se haya configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="7efa5-147">Hence, we do not want Log In action to be accessible till the device token has been properly set up.</span></span> <span data-ttu-id="7efa5-148">Es posible que desacople el inicio de sesión del registro de inserción, siempre que lo primero ocurra antes que lo último.</span><span class="sxs-lookup"><span data-stu-id="7efa5-148">You can decouple the log in from the push registration as long as the former happens before the latter.</span></span>
2. <span data-ttu-id="7efa5-149">En ViewController.m, utilice los siguientes fragmentos de código para implementar el método de acción para el botón **Iniciar sesión** y un método para enviar el mensaje de notificación con el back-end ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7efa5-149">In ViewController.m, use the following snippets to implement the action method for your **Log In** button and a method to send the notification message using the ASP.NET backend.</span></span>
   
       - <span data-ttu-id="7efa5-150">(IBAction) LogInAction: remitente (Id.) {/ / crear el encabezado de autenticación y establecerla en el registro cliente NSString * username = en sí mismo. UsernameField.text;   Contraseña de NSString = en sí mismo. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="7efa5-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="7efa5-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="7efa5-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="7efa5-152">__weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken etiquetas: nil andCompletion:^(NSError* error) {Si (! error) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered correctamente!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="7efa5-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="7efa5-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="7efa5-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="7efa5-154">Pasar la etiqueta de pns y el nombre de usuario como parámetros con la dirección URL de REST para el back-end ASP.NET NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="7efa5-154">// Pass the pns and username tag as parameters with the REST URL to the ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="7efa5-155">Solicitud de NSMutableURLRequest = [NSMutableURLRequest requestWithURL:requestURL];    [solicitud setHTTPMethod:@"POST"];</span><span class="sxs-lookup"><span data-stu-id="7efa5-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="7efa5-156">Obtener la ficticia authenticationheader desde el cliente de registro NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [solicitud setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span><span class="sxs-lookup"><span data-stu-id="7efa5-156">// Get the mock authenticationheader from the register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="7efa5-157">Agregue el cuerpo del mensaje de notificación [solicitar setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [solicitar setHTTPBody: [mensaje dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="7efa5-157">//Add the notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="7efa5-158">La API de REST de la notificación de envío se ejecuta en el dataTask NSURLSessionDataTask de back-end ASP.NET * = [sesión dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *Error) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) respuesta;        Si (error || httpResponse.statusCode! = 200) {NSString* estado = [NSString stringWithFormat:@"Error estado para % @: % d\nError: %@\n", pns, httpResponse.statusCode, aparece el error];            dispatch_async(dispatch_get_main_queue(), ^ {/ / anexar texto ya que todas las llamadas PNS 3 también pueden tener información a la vista [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="7efa5-158">// Execute the send notification REST API on the ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information to view                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="7efa5-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="7efa5-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="7efa5-160">Actualice la acción para que el botón **Enviar notificación** utilice el back-end ASP.NET y envíela a cualquier PNS habilitada por un modificador.</span><span class="sxs-lookup"><span data-stu-id="7efa5-160">Update the action for the **Send Notification** button to use the ASP.NET backend and send to any PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="7efa5-161">En la función **ViewDidLoad**, agregue el siguiente código para crear una instancia de RegisterClient y establezca el delegado para sus campos de texto.</span><span class="sxs-lookup"><span data-stu-id="7efa5-161">In function **ViewDidLoad**, add the following to instantiate the RegisterClient instance and set the delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="7efa5-162">Ahora, en **AppDelegate.m**, quite todo el contenido del método **application:didRegisterForPushNotificationWithDeviceToken:** y reemplácelo por lo siguiente para asegurarse de que el controlador de vista contiene el token de dispositivo más reciente recuperado desde APN:</span><span class="sxs-lookup"><span data-stu-id="7efa5-162">Now in **AppDelegate.m**, remove all the content of the method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with the following to make sure that the view controller contains the latest device token retrieved from APNs:</span></span>
   
       // Add import to the top of the file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="7efa5-163">Finalmente, en **AppDelegate.m**, asegúrese de que tiene el siguiente método:</span><span class="sxs-lookup"><span data-stu-id="7efa5-163">Finally in **AppDelegate.m**, make sure you have the following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-the-application"></a><span data-ttu-id="7efa5-164">Prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="7efa5-164">Test the Application</span></span>
1. <span data-ttu-id="7efa5-165">En XCode, ejecute la aplicación en un dispositivo iOS físico (las notificaciones de inserción no funcionarán en el simulador).</span><span class="sxs-lookup"><span data-stu-id="7efa5-165">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="7efa5-166">En la interfaz de usuario de la aplicación iOS, escriba un nombre de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="7efa5-166">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="7efa5-167">Esta información puede ser cualquier cadena, pero deben tener ambos el mismo valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="7efa5-167">These can be any string, but they must both be the same string value.</span></span> <span data-ttu-id="7efa5-168">A continuación, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="7efa5-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="7efa5-169">Debería ver una ventana emergente que le informa del éxito de registro.</span><span class="sxs-lookup"><span data-stu-id="7efa5-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="7efa5-170">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7efa5-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="7efa5-171">En el campo de texto para la*etiqueta del nombre de usuario del destinatario* , escriba la etiqueta del nombre de usuario usada con el registro desde otro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7efa5-171">In the **Recipient username tag* text field, enter the user name tag used with the registration from another device.</span></span>
5. <span data-ttu-id="7efa5-172">Escriba un mensaje de notificación y haga clic en **Enviar notificación**.</span><span class="sxs-lookup"><span data-stu-id="7efa5-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="7efa5-173">Solo los dispositivos que tienen un registro con la etiqueta de nombre de usuario del destinatario reciben el mensaje de notificación.</span><span class="sxs-lookup"><span data-stu-id="7efa5-173">Only the devices that have a registration with the recipient user name tag receive the notification message.</span></span>  <span data-ttu-id="7efa5-174">Solo se envía a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="7efa5-174">It is only sent to those users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
