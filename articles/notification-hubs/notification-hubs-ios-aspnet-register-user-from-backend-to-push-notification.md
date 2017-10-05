---
title: Registro del usuario actual para notificaciones push mediante una API web | Microsoft Docs
description: "Obtenga información acerca de cómo solicitar el registro de notificaciones de inserción en una aplicación iOS con los Centros de notificaciones de Azure al realizar el registro por la API web de ASP.NET."
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
ms.openlocfilehash: fd56bb2dd627b31f00363851a4e76484aa382988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="register-the-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="59018-103">Registro del usuario actual para las notificaciones de inserción mediante ASP.NET</span><span class="sxs-lookup"><span data-stu-id="59018-103">Register the current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59018-104">iOS</span><span class="sxs-lookup"><span data-stu-id="59018-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="59018-105">Información general</span><span class="sxs-lookup"><span data-stu-id="59018-105">Overview</span></span>
<span data-ttu-id="59018-106">En este tema se describe cómo solicitar el registro de las notificaciones de inserción con los Centros de notificaciones de Azure al realizar el registro mediante ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="59018-106">This topic shows you how to request push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="59018-107">Este tema amplía el tutorial [Notificación a los usuarios con los Centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="59018-107">This topic extends the tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="59018-108">Debe haber completado ya los pasos necesarios de ese tutorial para crear el servicio móvil autenticado.</span><span class="sxs-lookup"><span data-stu-id="59018-108">You must have already completed the required steps in that tutorial to create the authenticated mobile service.</span></span> <span data-ttu-id="59018-109">Para obtener más información acerca del escenario de notificación a los usuarios, consulte [Notificación a los usuarios con los Centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="59018-109">For more information on the notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="59018-110">Actualización de la aplicación</span><span class="sxs-lookup"><span data-stu-id="59018-110">Update your app</span></span>
1. <span data-ttu-id="59018-111">En su MainStoryboard_iPhone.storyboard, agregue los siguientes componentes desde la biblioteca de objetos:</span><span class="sxs-lookup"><span data-stu-id="59018-111">In your MainStoryboard_iPhone.storyboard, add the following components from the object library:</span></span>
   
   * <span data-ttu-id="59018-112">**Etiqueta**: "Push to User with Notification Hubs"</span><span class="sxs-lookup"><span data-stu-id="59018-112">**Label**: "Push to User with Notification Hubs"</span></span>
   * <span data-ttu-id="59018-113">**Etiqueta**: "InstallationId"</span><span class="sxs-lookup"><span data-stu-id="59018-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="59018-114">**Etiqueta**: "User"</span><span class="sxs-lookup"><span data-stu-id="59018-114">**Label**: "User"</span></span>
   * <span data-ttu-id="59018-115">**Campo de texto**: "User"</span><span class="sxs-lookup"><span data-stu-id="59018-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="59018-116">**Etiqueta**: "Password"</span><span class="sxs-lookup"><span data-stu-id="59018-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="59018-117">**Campo de texto**: "Password"</span><span class="sxs-lookup"><span data-stu-id="59018-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="59018-118">**Botón**: "Login"</span><span class="sxs-lookup"><span data-stu-id="59018-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="59018-119">En este punto, su storyboard debe presentar la siguiente apariencia:</span><span class="sxs-lookup"><span data-stu-id="59018-119">At this point, your storyboard looks like the following:</span></span>
     
      ![][0]
2. <span data-ttu-id="59018-120">En el editor del asistente, cree salidas para todos los controles cambiados y llámelos, conecte los campos de texto con el controlador de vista (delegado) y cree una **acción** para el botón de **inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="59018-120">In the assistant editor, create outlets for all the switched controls and call them, connect the text fields with the View Controller (delegate), and create an **Action** for the **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain the following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="59018-121">Cree una clase llamada **DeviceInfo**y copie el siguiente código en la sección de la interfaz del archivo DeviceInfo.h:</span><span class="sxs-lookup"><span data-stu-id="59018-121">Create a class named **DeviceInfo**, and copy the following code into the interface section of the file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="59018-122">Copie el siguiente código en la sección de implementación del archivo DeviceInfo.m:</span><span class="sxs-lookup"><span data-stu-id="59018-122">Copy the following code in the implementation section of the DeviceInfo.m file:</span></span>
   
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
   
                    //store the install ID so we don't generate a new one next time
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
5. <span data-ttu-id="59018-123">En PushToUserAppDelegate.h, agregue la siguiente propiedad singleton:</span><span class="sxs-lookup"><span data-stu-id="59018-123">In PushToUserAppDelegate.h, add the following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="59018-124">En el método **didFinishLaunchingWithOptions** en PushToUserAppDelegate.m, agregue el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="59018-124">In the **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add the following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="59018-125">La primera línea inicializa el singleton **DeviceInfo** .</span><span class="sxs-lookup"><span data-stu-id="59018-125">The first line initializes the **DeviceInfo** singleton.</span></span> <span data-ttu-id="59018-126">La segunda línea inicia el registro de notificaciones de inserción, que ya existe si ya ha completado el tutorial [Introducción a los Centros de notificaciones] .</span><span class="sxs-lookup"><span data-stu-id="59018-126">The second line starts the registration for push notifications, which is already present is you have already completed the [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="59018-127">En PushToUserAppDelegate.m, implemente el método **didRegisterForRemoteNotificationsWithDeviceToken** en su AppDelegate y agregue el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="59018-127">In PushToUserAppDelegate.m, implement the method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add the following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="59018-128">De este modo se configura el token del dispositivo para la solicitud.</span><span class="sxs-lookup"><span data-stu-id="59018-128">This sets the device token for the request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="59018-129">En este punto, no debería haber ningún otro código en este método.</span><span class="sxs-lookup"><span data-stu-id="59018-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="59018-130">Si ya tiene una llamada al método **registerNativeWithDeviceToken** que se agregó cuando realizó el tutorial [Introducción a los Centros de notificaciones](/manage/services/notification-hubs/get-started-notification-hubs-ios/) , debe convertir la llamada en comentario o borrarla.</span><span class="sxs-lookup"><span data-stu-id="59018-130">If you already have a call to the **registerNativeWithDeviceToken** method that was added when you completed the [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="59018-131">En el archivo PushToUserAppDelegate.m, agregue el siguiente método de controlador:</span><span class="sxs-lookup"><span data-stu-id="59018-131">In the PushToUserAppDelegate.m file, add the following handler method:</span></span>
   
   * <span data-ttu-id="59018-132">información de usuario de aplicación (void):(UIApplication *) aplicación didReceiveRemoteNotification:(NSDictionary *) {NSLog (@"% @", información de usuario);   UIAlertView * alerta = [[UIAlertView alloc] initWithTitle:@"Notification" mensaje: [información de usuario objectForKey:@"inAppMessage]" delegado: nil cancelButtonTitle: @ otherButtonTitles:nil "Aceptar", nulo];   [Mostrar alerta]; }</span><span class="sxs-lookup"><span data-stu-id="59018-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="59018-133">Este método muestra una alerta en la interfaz de usuario cuando su aplicación recibe notificaciones durante su ejecución.</span><span class="sxs-lookup"><span data-stu-id="59018-133">This method displays an alert in the UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="59018-134">Abra el archivo PushToUserViewController.m y escriba la siguiente implementación:</span><span class="sxs-lookup"><span data-stu-id="59018-134">Open the PushToUserViewController.m file, and return the keyboard in the following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="59018-135">En el método **viewDidLoad** del archivo PushToUserViewController.m, inicialice la etiqueta installationId como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="59018-135">In the **viewDidLoad** method in the PushToUserViewController.m file, initialize the installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="59018-136">Agregue las siguientes propiedades en la interfaz en PushToUserViewController.m:</span><span class="sxs-lookup"><span data-stu-id="59018-136">Add the following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="59018-137">Luego, agregue la siguiente implementación:</span><span class="sxs-lookup"><span data-stu-id="59018-137">Then, add the following implementation:</span></span>
    
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
13. <span data-ttu-id="59018-138">Copie el siguiente código en el método controlador **login** creado por XCode:</span><span class="sxs-lookup"><span data-stu-id="59018-138">Copy the following code into the **login** handler method created by XCode:</span></span>
    
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
    
    <span data-ttu-id="59018-139">Este método obtiene un ID de instalación y un canal para las notificaciones de inserción y los envía, junto con el tipo de dispositivo, al método de Web API autenticado que crea un registro en los Centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="59018-139">This method gets both an installation ID and channel for push notifications and sends it, along with the device type, to the authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="59018-140">Esta API web se definió en [Notificación a los usuarios con los Centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="59018-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="59018-141">Ahora que la aplicación de cliente se ha actualizado, regrese a [Notificación a los usuarios con los Centros de notificaciones] y actualice el servicio móvil para enviar notificaciones mediante Centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="59018-141">Now that the client app has been updated, return to the [Notify users with Notification Hubs] and update the mobile service to send notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
<span data-ttu-id="59018-142">[Notificación a los usuarios con los Centros de notificaciones]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="59018-142">[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet</span></span>

<span data-ttu-id="59018-143">[Introducción a los Centros de notificaciones]: /manage/services/notification-hubs/get-started-notification-hubs-ios</span><span class="sxs-lookup"><span data-stu-id="59018-143">[Get Started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-ios</span></span>
