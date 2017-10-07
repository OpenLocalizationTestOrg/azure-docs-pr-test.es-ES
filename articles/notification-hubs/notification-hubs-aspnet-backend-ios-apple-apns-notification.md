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
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="4af46-104">Los Centros de notificaciones de Azure notifican a los usuarios para iOS con back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="4af46-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="4af46-105">Información general</span><span class="sxs-lookup"><span data-stu-id="4af46-105">Overview</span></span>
<span data-ttu-id="4af46-106">Compatibilidad de la notificación de inserción en Azure permite tooaccess una fácil de usar, multiplataforma y la infraestructura de inserción de escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa para dispositivos móviles plataformas.</span><span class="sxs-lookup"><span data-stu-id="4af46-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="4af46-107">Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push usuario de aplicación específica de tooa de notificaciones en un dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="4af46-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="4af46-108">Un back-end de ASP.NET WebAPI es tooauthenticate usa clientes y las notificaciones de toogenerate, como se muestra en el tema de la Guía de hello [registrar desde su aplicación de back-end](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="4af46-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="4af46-109">Este tutorial asume que ha creado y configurado el centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4af46-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="4af46-110">Este tutorial también es toohello de requisitos previos de hello [seguros de inserción (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="4af46-110">This tutorial is also hello prerequisite toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="4af46-111">Si desea toouse Mobile aplicaciones como el servicio back-end, vea hello [Mobile Apps empezar a trabajar con inserción](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="4af46-111">If you want toouse Mobile Apps as your backend service, see hello [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="4af46-112">Modificación de la aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="4af46-112">Modify your iOS app</span></span>
1. <span data-ttu-id="4af46-113">Abra Hola única página ver la aplicación que creó en hello [Introducción a centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="4af46-113">Open hello Single Page view app you created in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4af46-114">En esta sección asumimos que configuró el proyecto con un nombre de organización vacío.</span><span class="sxs-lookup"><span data-stu-id="4af46-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="4af46-115">De lo contrario, deberá tooprepend los nombres de clase de tooall de nombre de organización.</span><span class="sxs-lookup"><span data-stu-id="4af46-115">If not, you will need tooprepend your organization name tooall class names.</span></span>
   > 
   > 
2. <span data-ttu-id="4af46-116">En su Main.storyboard agregar componentes de Hola que se muestra en la captura de pantalla de hello debajo de la biblioteca de objetos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4af46-116">In your Main.storyboard add hello components shown in hello screenshot below from hello object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="4af46-117">**Nombre de usuario**: UITextField de A con el texto de marcador de posición, *escriba el nombre de usuario*, inmediatamente debajo de hello enviar etiqueta results y restringida toohello dejados y los márgenes de la derecha y debajo de Hola enviar etiqueta de resultados.</span><span class="sxs-lookup"><span data-stu-id="4af46-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath hello send results label and constrained toohello left and right margins and beneath hello send results label.</span></span>
   * <span data-ttu-id="4af46-118">**Contraseña**: UITextField de A con el texto de marcador de posición, *escribir la contraseña*, inmediatamente debajo Hola campo de texto Nombre de usuario y toohello restringida izquierda y a la derecha de los márgenes y por debajo del campo de texto Nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="4af46-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath hello username text field and constrained toohello left and right margins and beneath hello username text field.</span></span> <span data-ttu-id="4af46-119">Comprobar hello **proteger la entrada de texto** opción Hola Inspector de atributo, en *devolver clave*.</span><span class="sxs-lookup"><span data-stu-id="4af46-119">Check hello **Secure Text Entry** option in hello Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="4af46-120">**Inicie sesión**: UIButton A la etiqueta inmediatamente debajo del campo de texto de contraseña de Hola y desactive la opción hello **habilitado** opción Hola Inspector de atributos, en *contenido del Control*</span><span class="sxs-lookup"><span data-stu-id="4af46-120">**Log in**: A UIButton labeled immediately beneath hello password text field and uncheck hello **Enabled** option in hello Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="4af46-121">**WNS**: etiqueta y el envío de conmutador tooenable Hola notificación del servicio de notificación de Windows si han pasado el programa de instalación en el concentrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="4af46-121">**WNS**: Label and switch tooenable sending hello notification Windows Notification Service if it has been setup on hello hub.</span></span> <span data-ttu-id="4af46-122">Vea hello [Introducción a Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="4af46-122">See hello [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="4af46-123">**GCM**: etiqueta y el envío de conmutador tooenable Hola tooGoogle de notificación de mensajería en la nube si han pasado el programa de instalación en el concentrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="4af46-123">**GCM**: Label and switch tooenable sending hello notification tooGoogle Cloud Messaging if it has been setup on hello hub.</span></span> <span data-ttu-id="4af46-124">Consulte el tutorial [introductorio de Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="4af46-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="4af46-125">**APN**: etiqueta y el envío de conmutador tooenable Hola notificación toohello servicio de notificación de plataforma de Apple.</span><span class="sxs-lookup"><span data-stu-id="4af46-125">**APNS**: Label and switch tooenable sending hello notification toohello Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="4af46-126">**Recipent Username**: UITextField de A con el texto de marcador de posición, *etiqueta de nombre de usuario de destinatario*, inmediatamente debajo de hello GCM etiquetar y restringida toohello izquierdo y derecho márgenes y debajo de hello GCM etiquetar.</span><span class="sxs-lookup"><span data-stu-id="4af46-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath hello GCM label and constrained toohello left and right margins and beneath hello GCM label.</span></span>

    <span data-ttu-id="4af46-127">Se agregaron algunos componentes en hello [Introducción a centros de notificaciones (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="4af46-127">Some components were added in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="4af46-128">**CTRL** arrastre desde componentes de hello en hello vista tooViewController.h y agregue estas nuevas salidas.</span><span class="sxs-lookup"><span data-stu-id="4af46-128">**Ctrl** drag from hello components in hello view tooViewController.h and add these new outlets.</span></span>
   
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
2. <span data-ttu-id="4af46-129">En ViewController.h, agregue el siguiente hello `#define` justo debajo de las instrucciones de importación.</span><span class="sxs-lookup"><span data-stu-id="4af46-129">In ViewController.h, add hello following `#define` just below your import statements.</span></span> <span data-ttu-id="4af46-130">Hola sustituto *< escriba el extremo de back-end\>*  marcador de posición con hello usa toodeploy el back-end de aplicación en la sección anterior de Hola de dirección URL de destino.</span><span class="sxs-lookup"><span data-stu-id="4af46-130">Substitute hello *<Enter Your Backend Endpoint\>* placeholder with hello Destination URL you used toodeploy your app backend in hello previous section.</span></span> <span data-ttu-id="4af46-131">Por ejemplo, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="4af46-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="4af46-132">En el proyecto, cree un nuevo **cacao Touch clase** denominado **RegisterClient** toointerface con hello ASP.NET back-end que creó.</span><span class="sxs-lookup"><span data-stu-id="4af46-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** toointerface with hello ASP.NET back-end you created.</span></span> <span data-ttu-id="4af46-133">Crear clase de Hola que hereda de `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="4af46-133">Create hello class inheriting from `NSObject`.</span></span> <span data-ttu-id="4af46-134">A continuación, agregue Hola después el código de hello RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="4af46-134">Then add hello following code in hello RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="4af46-135">Hola RegisterClient.m actualizar hello `@interface` sección:</span><span class="sxs-lookup"><span data-stu-id="4af46-135">In hello RegisterClient.m update hello `@interface` section:</span></span>
   
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
5. <span data-ttu-id="4af46-136">Reemplace hello `@implementation` sección Hola RegisterClient.m con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="4af46-136">Replace hello `@implementation` section in hello RegisterClient.m with hello following code.</span></span>

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

    <span data-ttu-id="4af46-137">código de Hello anterior implementa la lógica de hello explicado en el artículo de guía de hello [registrar desde su aplicación de back-end](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) con NSURLSession tooperform REST llama backend de la aplicación de tooyour y NSUserDefaults toolocally almacén Hola Identificador devuelto por el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="4af46-137">hello code above implements hello logic explained in hello guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession tooperform REST calls tooyour app backend, and NSUserDefaults toolocally store hello registrationId returned by hello notification hub.</span></span>

    <span data-ttu-id="4af46-138">Tenga en cuenta que esta clase requiere la propiedad **authorizationHeader** toobe establecida en orden toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="4af46-138">Note that this class requires its property **authorizationHeader** toobe set in order toowork properly.</span></span> <span data-ttu-id="4af46-139">Esta propiedad se establece por hello **ViewController** tras Hola del registro la clase.</span><span class="sxs-lookup"><span data-stu-id="4af46-139">This property is set by hello **ViewController** class after hello log in.</span></span>

1. <span data-ttu-id="4af46-140">En ViewController.h, agregue una instrucción `#import` a RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="4af46-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="4af46-141">A continuación, agregue una declaración para el token del dispositivo de Hola y hacer referencia a tooa `RegisterClient` instancia Hola `@interface` sección:</span><span class="sxs-lookup"><span data-stu-id="4af46-141">Then add a declaration for hello device token and reference tooa `RegisterClient` instance in hello `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="4af46-142">En ViewController.m, agregue una declaración de método privado en hello `@interface` sección:</span><span class="sxs-lookup"><span data-stu-id="4af46-142">In ViewController.m, add a private method declaration in hello `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="4af46-143">Hello fragmento de código siguiente no es un esquema de autenticación segura, se debe sustituir implementación Hola de hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** con su mecanismo de autenticación concreto genera un toobe de token de autenticación utilizado por hello register clase de cliente, por ejemplo, OAuth, Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4af46-143">hello following snippet is not a secure authentication scheme, you should substitute hello implementation of hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token toobe consumed by hello register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="4af46-144">A continuación, en hello `@implementation` sección de ViewController.m agregar Hola después el código que agrega la implementación de Hola para configuración Hola dispositivo símbolo (token) y autenticación de encabezado.</span><span class="sxs-lookup"><span data-stu-id="4af46-144">Then in hello `@implementation` section of ViewController.m add hello following code which adds hello implementation for setting hello device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="4af46-145">Tenga en cuenta cómo el token del dispositivo de configuración Hola permite Hola botón Iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="4af46-145">Note how setting hello device token enables hello log in button.</span></span> <span data-ttu-id="4af46-146">Esto es porque como parte de la acción de inicio de sesión de hello, controlador de vista de hello registra las notificaciones de inserción con back-end de aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4af46-146">This is becasue as a part of hello login action, hello view controller registers for push notifications with hello app backend.</span></span> <span data-ttu-id="4af46-147">Por lo tanto, no queremos que en el registro de acción toobe accesibles hasta que el token del dispositivo Hola se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4af46-147">Hence, we do not want Log In action toobe accessible till hello device token has been properly set up.</span></span> <span data-ttu-id="4af46-148">Puede desacoplar Hola sesión de registro de inserción de hello como primero Hola se realiza antes que este último Hola.</span><span class="sxs-lookup"><span data-stu-id="4af46-148">You can decouple hello log in from hello push registration as long as hello former happens before hello latter.</span></span>
2. <span data-ttu-id="4af46-149">En ViewController.m, usar hello siguiendo el método de acción de fragmentos de código tooimplement Hola para su **inicio de sesión** botón y un método toosend Hola mensaje de notificación utilizando Hola back-end ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4af46-149">In ViewController.m, use hello following snippets tooimplement hello action method for your **Log In** button and a method toosend hello notification message using hello ASP.NET backend.</span></span>
   
       - <span data-ttu-id="4af46-150">(IBAction) LogInAction: remitente (Id.) {/ / crear el encabezado de autenticación y establecerla en el registro cliente NSString * username = en sí mismo. UsernameField.text;   Contraseña de NSString = en sí mismo. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="4af46-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="4af46-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="4af46-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="4af46-152">__weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken etiquetas: nil andCompletion:^(NSError* error) {Si (! error) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered correctamente!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="4af46-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="4af46-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="4af46-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="4af46-154">Pasar la etiqueta de pns y el nombre de usuario de hello como parámetros con la dirección URL de REST de hello toohello ASP.NET back-end NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="4af46-154">// Pass hello pns and username tag as parameters with hello REST URL toohello ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="4af46-155">Solicitud de NSMutableURLRequest = [NSMutableURLRequest requestWithURL:requestURL];    [solicitud setHTTPMethod:@"POST"];</span><span class="sxs-lookup"><span data-stu-id="4af46-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="4af46-156">Obtener Hola ficticia authenticationheader de cliente de registro de hello NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [solicitud setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span><span class="sxs-lookup"><span data-stu-id="4af46-156">// Get hello mock authenticationheader from hello register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="4af46-157">Agregue el cuerpo del mensaje de notificación de hello [solicitar setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [solicitar setHTTPBody: [mensaje dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="4af46-157">//Add hello notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="4af46-158">Notificación de envío de hello API de REST se ejecuta en hello ASP.NET back-end NSURLSessionDataTask * dataTask = [sesión dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *Error) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) respuesta;        Si (error || httpResponse.statusCode! = 200) {NSString* estado = [NSString stringWithFormat:@"Error estado para % @: % d\nError: %@\n", pns, httpResponse.statusCode, aparece el error];            dispatch_async(dispatch_get_main_queue(), ^ {/ / anexar texto ya que todas las llamadas PNS 3 también pueden tener información tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="4af46-158">// Execute hello send notification REST API on hello ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information tooview                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="4af46-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="4af46-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="4af46-160">Actualizar la acción de Hola para hello **enviar notificación** botón toouse Hola ASP.NET back-end y enviar tooany PNS gracias a un conmutador.</span><span class="sxs-lookup"><span data-stu-id="4af46-160">Update hello action for hello **Send Notification** button toouse hello ASP.NET backend and send tooany PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="4af46-161">En la función **ViewDidLoad**, agregue Hola posterior tooinstantiate hello RegisterClient instancia y establece el delegado de Hola para los campos de texto.</span><span class="sxs-lookup"><span data-stu-id="4af46-161">In function **ViewDidLoad**, add hello following tooinstantiate hello RegisterClient instance and set hello delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="4af46-162">Ahora, en **AppDelegate.m**, quitar todo el contenido del método hello hello **aplicación: didRegisterForPushNotificationWithDeviceToken:** y reemplazarlo con hello después toomake seguro que Hola vista controlador contiene hello más reciente dispositivo token recuperado de APNs:</span><span class="sxs-lookup"><span data-stu-id="4af46-162">Now in **AppDelegate.m**, remove all hello content of hello method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with hello following toomake sure that hello view controller contains hello latest device token retrieved from APNs:</span></span>
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="4af46-163">Por último, en **AppDelegate.m**, asegúrese de que tienen Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="4af46-163">Finally in **AppDelegate.m**, make sure you have hello following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a><span data-ttu-id="4af46-164">Hola aplicación de prueba</span><span class="sxs-lookup"><span data-stu-id="4af46-164">Test hello Application</span></span>
1. <span data-ttu-id="4af46-165">En XCode, ejecute la aplicación hello en un dispositivo de E/s físicas (inserción notificaciones no funcionará en el simulador de hello).</span><span class="sxs-lookup"><span data-stu-id="4af46-165">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="4af46-166">En la aplicación de iOS de hello interfaz de usuario, escriba un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="4af46-166">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="4af46-167">Pueden ser cualquier cadena, pero ambos deben ser Hola mismo valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="4af46-167">These can be any string, but they must both be hello same string value.</span></span> <span data-ttu-id="4af46-168">A continuación, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="4af46-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="4af46-169">Debería ver una ventana emergente que le informa del éxito de registro.</span><span class="sxs-lookup"><span data-stu-id="4af46-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="4af46-170">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4af46-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="4af46-171">Hola **etiqueta de nombre de usuario de destinatario* texto, escriba la etiqueta de nombre de usuario de hello utilizado con el registro de hello desde otro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4af46-171">In hello **Recipient username tag* text field, enter hello user name tag used with hello registration from another device.</span></span>
5. <span data-ttu-id="4af46-172">Escriba un mensaje de notificación y haga clic en **Enviar notificación**.</span><span class="sxs-lookup"><span data-stu-id="4af46-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="4af46-173">Solo los dispositivos de Hola que tienen un registro con la etiqueta de nombre de usuario del destinatario de Hola reciban mensaje de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4af46-173">Only hello devices that have a registration with hello recipient user name tag receive hello notification message.</span></span>  <span data-ttu-id="4af46-174">Sólo se envía a los usuarios de toothose.</span><span class="sxs-lookup"><span data-stu-id="4af46-174">It is only sent toothose users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
