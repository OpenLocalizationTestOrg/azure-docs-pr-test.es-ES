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
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="c556a-103">Registrar al usuario actual de hello las notificaciones de inserción mediante ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c556a-103">Register hello current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c556a-104">iOS</span><span class="sxs-lookup"><span data-stu-id="c556a-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c556a-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c556a-105">Overview</span></span>
<span data-ttu-id="c556a-106">Este tema muestra cómo toorequest Insertar registro de notificaciones con centros de notificaciones de Azure cuando el registro se realiza por la API Web de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c556a-106">This topic shows you how toorequest push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="c556a-107">Este tema amplían tutorial Hola [notificar a los usuarios con centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="c556a-107">This topic extends hello tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="c556a-108">Debe haber completado pasos Hola necesario en ese servicio móvil de toocreate tutorial Hola autenticado.</span><span class="sxs-lookup"><span data-stu-id="c556a-108">You must have already completed hello required steps in that tutorial toocreate hello authenticated mobile service.</span></span> <span data-ttu-id="c556a-109">Para obtener más información sobre Hola notificar al escenario de los usuarios, consulte [notificar a los usuarios con centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="c556a-109">For more information on hello notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="c556a-110">Actualización de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c556a-110">Update your app</span></span>
1. <span data-ttu-id="c556a-111">En su MainStoryboard_iPhone.storyboard, agregue Hola de los componentes siguientes de la biblioteca de objetos de hello:</span><span class="sxs-lookup"><span data-stu-id="c556a-111">In your MainStoryboard_iPhone.storyboard, add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="c556a-112">**Etiqueta**: "TooUser con centros de notificaciones de inserción"</span><span class="sxs-lookup"><span data-stu-id="c556a-112">**Label**: "Push tooUser with Notification Hubs"</span></span>
   * <span data-ttu-id="c556a-113">**Etiqueta**: "InstallationId"</span><span class="sxs-lookup"><span data-stu-id="c556a-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="c556a-114">**Etiqueta**: "User"</span><span class="sxs-lookup"><span data-stu-id="c556a-114">**Label**: "User"</span></span>
   * <span data-ttu-id="c556a-115">**Campo de texto**: "User"</span><span class="sxs-lookup"><span data-stu-id="c556a-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="c556a-116">**Etiqueta**: "Password"</span><span class="sxs-lookup"><span data-stu-id="c556a-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="c556a-117">**Campo de texto**: "Password"</span><span class="sxs-lookup"><span data-stu-id="c556a-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="c556a-118">**Botón**: "Login"</span><span class="sxs-lookup"><span data-stu-id="c556a-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="c556a-119">En este momento, el guión gráfico Hola siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="c556a-119">At this point, your storyboard looks like hello following:</span></span>
     
      ![][0]
2. <span data-ttu-id="c556a-120">En el editor de Asistente de hello, crear las salidas de todos los controles de hello cambiado y llamarlos, conectar los campos de texto hello con hello View-Controller (delegado) y crear un **acción** para hello **inicio de sesión** botón.</span><span class="sxs-lookup"><span data-stu-id="c556a-120">In hello assistant editor, create outlets for all hello switched controls and call them, connect hello text fields with hello View Controller (delegate), and create an **Action** for hello **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="c556a-121">Cree una clase denominada **DeviceInfo**, y Hola copia siguiendo el código en la sección de la interfaz de Hola de archivo hello DeviceInfo.h:</span><span class="sxs-lookup"><span data-stu-id="c556a-121">Create a class named **DeviceInfo**, and copy hello following code into hello interface section of hello file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="c556a-122">Copie Hola después el código de sección de implementación de Hola de archivo de hello DeviceInfo.m:</span><span class="sxs-lookup"><span data-stu-id="c556a-122">Copy hello following code in hello implementation section of hello DeviceInfo.m file:</span></span>
   
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
5. <span data-ttu-id="c556a-123">En PushToUserAppDelegate.h, agregue Hola después singleton de propiedad:</span><span class="sxs-lookup"><span data-stu-id="c556a-123">In PushToUserAppDelegate.h, add hello following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="c556a-124">Hola **didFinishLaunchingWithOptions** método PushToUserAppDelegate.m, agregar Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="c556a-124">In hello **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add hello following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="c556a-125">primera línea de Hello inicializa hello **DeviceInfo** singleton.</span><span class="sxs-lookup"><span data-stu-id="c556a-125">hello first line initializes hello **DeviceInfo** singleton.</span></span> <span data-ttu-id="c556a-126">Hola segunda línea inicia Hola registro para las notificaciones de inserción, que ya está presente es ya completados hello [empezar a trabajar con los centros de notificaciones] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c556a-126">hello second line starts hello registration for push notifications, which is already present is you have already completed hello [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="c556a-127">En PushToUserAppDelegate.m, implemente el método hello **didRegisterForRemoteNotificationsWithDeviceToken** en su AppDelegate y agregue el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="c556a-127">In PushToUserAppDelegate.m, implement hello method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add hello following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="c556a-128">Esto establece el token del dispositivo Hola para solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="c556a-128">This sets hello device token for hello request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c556a-129">En este punto, no debería haber ningún otro código en este método.</span><span class="sxs-lookup"><span data-stu-id="c556a-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="c556a-130">Si ya tiene una llamada toohello **registerNativeWithDeviceToken** método que se agregó al completar hello [empezar a trabajar con los centros de notificaciones](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial debe Comente o quite que llamar a.</span><span class="sxs-lookup"><span data-stu-id="c556a-130">If you already have a call toohello **registerNativeWithDeviceToken** method that was added when you completed hello [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="c556a-131">En archivo de PushToUserAppDelegate.m de hello, agregue Hola siguiendo el método de controlador:</span><span class="sxs-lookup"><span data-stu-id="c556a-131">In hello PushToUserAppDelegate.m file, add hello following handler method:</span></span>
   
   * <span data-ttu-id="c556a-132">información de usuario de aplicación (void):(UIApplication *) aplicación didReceiveRemoteNotification:(NSDictionary *) {NSLog (@"% @", información de usuario);   UIAlertView * alerta = [[UIAlertView alloc] initWithTitle:@"Notification" mensaje: [información de usuario objectForKey:@"inAppMessage]" delegado: nil cancelButtonTitle: @ otherButtonTitles:nil "Aceptar", nulo];   [Mostrar alerta]; }</span><span class="sxs-lookup"><span data-stu-id="c556a-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="c556a-133">Este método muestra una alerta en la interfaz de usuario de hello cuando la aplicación recibe notificaciones mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="c556a-133">This method displays an alert in hello UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="c556a-134">Abrir archivo de PushToUserViewController.m hello y teclado Hola devuelto en hello después de la implementación:</span><span class="sxs-lookup"><span data-stu-id="c556a-134">Open hello PushToUserViewController.m file, and return hello keyboard in hello following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="c556a-135">Hola **viewDidLoad** método hello PushToUserViewController.m archivo, inicializar etiqueta installationId de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="c556a-135">In hello **viewDidLoad** method in hello PushToUserViewController.m file, initialize hello installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="c556a-136">Agregue Hola propiedades de interfaz en PushToUserViewController.m siguientes:</span><span class="sxs-lookup"><span data-stu-id="c556a-136">Add hello following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="c556a-137">A continuación, agregue Hola después de la implementación:</span><span class="sxs-lookup"><span data-stu-id="c556a-137">Then, add hello following implementation:</span></span>
    
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
13. <span data-ttu-id="c556a-138">Copia Hola siguiente de código en hello **inicio de sesión** método de controlador creado por XCode:</span><span class="sxs-lookup"><span data-stu-id="c556a-138">Copy hello following code into hello **login** handler method created by XCode:</span></span>
    
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
    
    <span data-ttu-id="c556a-139">Este método obtiene un identificador de instalación y el canal de notificaciones de inserción y lo envía, junto con el tipo de dispositivo de hello, toohello autentica el método API de Web que crea un registro en los centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c556a-139">This method gets both an installation ID and channel for push notifications and sends it, along with hello device type, toohello authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="c556a-140">Esta API web se definió en [notificar a los usuarios con centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="c556a-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="c556a-141">Ahora que hello aplicación cliente se ha actualizado, devolver toohello [notificar a los usuarios con centros de notificaciones] y actualizar notificaciones de toosend de hello servicio móvil con centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c556a-141">Now that hello client app has been updated, return toohello [Notify users with Notification Hubs] and update hello mobile service toosend notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[notificar a los usuarios con centros de notificaciones]: /manage/services/notification-hubs/notify-users-aspnet

[empezar a trabajar con los centros de notificaciones]: /manage/services/notification-hubs/get-started-notification-hubs-ios
