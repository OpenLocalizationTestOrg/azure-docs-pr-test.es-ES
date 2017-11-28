---
title: "Inserción enriquecida de los Centros de notificaciones de Azure"
description: "Obtenga información acerca de cómo enviar notificaciones de inserción enriquecidas a una aplicación iOS desde Azure. Ejemplos de código escritos en Objective-C y C#."
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
ms.openlocfilehash: 394efdc2dfaff0666bc23d8a448b0a00d414da99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="2f880-104">Inserción enriquecida de los Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="2f880-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="2f880-105">Información general</span><span class="sxs-lookup"><span data-stu-id="2f880-105">Overview</span></span>
<span data-ttu-id="2f880-106">Para interactuar con los usuarios con contenido enriquecido instantánea, una aplicación que desee insertar más allá de texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="2f880-106">In order to engage users with instant rich contents, an application might want to push beyond plain text.</span></span> <span data-ttu-id="2f880-107">Estas notificaciones promueven las interacciones de los usuarios y presentan contenido como direcciones URL, sonidos, imágenes o cupones y más.</span><span class="sxs-lookup"><span data-stu-id="2f880-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="2f880-108">En este tutorial se trata el tema [Notificación a los usuarios](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) se muestra cómo enviar notificaciones push que incorporan cargas (por ejemplo, imágenes).</span><span class="sxs-lookup"><span data-stu-id="2f880-108">This tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how to send push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="2f880-109">Este tutorial es compatible con iOS 7 y 8.</span><span class="sxs-lookup"><span data-stu-id="2f880-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="2f880-110">En un alto nivel:</span><span class="sxs-lookup"><span data-stu-id="2f880-110">At a high level:</span></span>

1. <span data-ttu-id="2f880-111">El back-end de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="2f880-111">The app backend:</span></span>
   * <span data-ttu-id="2f880-112">Almacena la carga enriquecida (en este caso, la imagen) en el almacenamiento local y la base de datos back-end</span><span class="sxs-lookup"><span data-stu-id="2f880-112">Stores the rich payload (in this case, image) in the backend database/local storage</span></span>
   * <span data-ttu-id="2f880-113">Envía el identificador de esta notificación enriquecida al dispositivo</span><span class="sxs-lookup"><span data-stu-id="2f880-113">Sends ID of this rich notification to the device</span></span>
2. <span data-ttu-id="2f880-114">Aplicación en el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="2f880-114">App on the device:</span></span>
   * <span data-ttu-id="2f880-115">Se comunica con el back-end que solicita la carga enriquecida con el identificador que recibe</span><span class="sxs-lookup"><span data-stu-id="2f880-115">Contacts the backend requesting the rich payload with the ID it receives</span></span>
   * <span data-ttu-id="2f880-116">Envía notificaciones de usuarios en el dispositivo cuando se completa la recuperación de datos y muestra la carga inmediatamente cuando los usuarios pulsan para obtener más información</span><span class="sxs-lookup"><span data-stu-id="2f880-116">Sends users notifications on the device when data retrieval is complete, and shows the payload immediately when users tap to learn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="2f880-117">Proyecto WebAPI</span><span class="sxs-lookup"><span data-stu-id="2f880-117">WebAPI Project</span></span>
1. <span data-ttu-id="2f880-118">En Visual Studio, abra el proyecto **AppBackend** que creó en el tutorial [Notificación a usuarios](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="2f880-118">In Visual Studio, open the **AppBackend** project that you created in the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="2f880-119">Obtenga una imagen con la que le gustaría notificar a los usuarios y póngala e una carpeta **img** del directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2f880-119">Obtain an image you would like to notify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="2f880-120">Haga clic en **Mostrar todos los archivos** en el Explorador de soluciones y haga clic con el botón derecho en la carpeta para **Incluir en el proyecto**.</span><span class="sxs-lookup"><span data-stu-id="2f880-120">Click **Show All Files** in the Solution Explorer, and right-click the folder to **Include In Project**.</span></span>
4. <span data-ttu-id="2f880-121">Con la imagen seleccionada, cambie su acción de generación en la ventana Propiedades a **Recurso incrustado**.</span><span class="sxs-lookup"><span data-stu-id="2f880-121">With the image selected, change its Build Action in Properties window to **Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="2f880-122">En **Notifications.cs**, agregue la siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="2f880-122">In **Notifications.cs**, add the following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="2f880-123">Actualice toda la clase **Notifications** con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="2f880-123">Update the whole **Notifications** class with the following code.</span></span> <span data-ttu-id="2f880-124">Asegúrese de reemplazar los marcadores de posición con las credenciales del centro de notificaciones y el nombre de archivo de la imagen.</span><span class="sxs-lookup"><span data-stu-id="2f880-124">Be sure to replace the placeholders with your notification hub credentials and image file name.</span></span>
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message to display to users
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
                // Placeholders: replace with the connection string (with full access) for your notification hub and the hub name from the Azure Classics Portal
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
   > <span data-ttu-id="2f880-125">(opcional) Vea [Insertar y acceder a recursos con Visual C#](http://support.microsoft.com/kb/319292) para más información sobre cómo agregar y obtener los recursos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2f880-125">(optional) Refer to [How to embed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how to add and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="2f880-126">En **NotificationsController.cs**, vuelva a definir **NotificationsController** con los siguientes fragmentos de código.</span><span class="sxs-lookup"><span data-stu-id="2f880-126">In **NotificationsController.cs**, redefine **NotificationsController**  with the following snippets.</span></span> <span data-ttu-id="2f880-127">Esto envía un identificador de notificación enriquecida silencioso inicial y permite la recuperación de imagen en el cliente:</span><span class="sxs-lookup"><span data-stu-id="2f880-127">This sends an initial silent rich notification id to device and allows client-side retrieval of image:</span></span>
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) to client
        public async Task<HttpResponseMessage> Post() {
            // Replace the placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification to apns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. <span data-ttu-id="2f880-128">Ahora implementaremos de nuevo esta aplicación en un sitio web de Azure a fin de que sea accesible para todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="2f880-128">Now we will re-deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="2f880-129">Haga clic con el botón derecho en el proyecto **AppBackend** y, a continuación, seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="2f880-129">Right-click on the **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="2f880-130">Seleccione Sitio web Azure como destino de publicación.</span><span class="sxs-lookup"><span data-stu-id="2f880-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="2f880-131">Inicie sesión con su cuenta de Azure, seleccione un sitio web nuevo o existente y anote la propiedad **Dirección URL de destino** en la pestaña **Conexión**.</span><span class="sxs-lookup"><span data-stu-id="2f880-131">Log in with your Azure account and select an existing or new Website, and make a note of the **destination URL** property in the **Connection** tab.</span></span> <span data-ttu-id="2f880-132">Más tarde en este tutorial haremos referencia a esta dirección URL como *extremo de backend* .</span><span class="sxs-lookup"><span data-stu-id="2f880-132">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="2f880-133">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="2f880-133">Click **Publish**.</span></span>

## <a name="modify-the-ios-project"></a><span data-ttu-id="2f880-134">Modificación del proyecto iOS</span><span class="sxs-lookup"><span data-stu-id="2f880-134">Modify the iOS project</span></span>
<span data-ttu-id="2f880-135">Ahora que ha modificado el back-end de la aplicación para enviar solo el *id* de una notificación, cambiará la aplicación iOS para controlar ese identificador y recuperar el mensaje enriquecido desde el back-end.</span><span class="sxs-lookup"><span data-stu-id="2f880-135">Now that you have modified your app backend to send just the *id* of a notification, you will change your iOS app to handle that id and retrieve the rich message from your backend.</span></span>

1. <span data-ttu-id="2f880-136">Abra el proyecto iOS y habilite las notificaciones remotas yendo a su destino de la aplicación principal en la sección **Destinos** .</span><span class="sxs-lookup"><span data-stu-id="2f880-136">Open your iOS project, and enable remote notifications by going to your main app target in the **Targets** section.</span></span>
2. <span data-ttu-id="2f880-137">Haga clic en **Funciones**, active los **Modos en segundo plano** y active la casilla **Notificaciones remotas**.</span><span class="sxs-lookup"><span data-stu-id="2f880-137">Click on **Capabilities**, turn on **Background Modes**, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="2f880-138">Vaya a **Main.storyboard**y asegúrese de que dispone de un Controlador de vista (al que se hace referencia en este tutorial como Controlador de vista de inicio) en el tutorial [Notificación a usuarios](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="2f880-138">Go to **Main.storyboard**, and make sure you have a View Controller (refered to as Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="2f880-139">Agregue un **Controlador de navegación** al guion gráfico y mantenga presionada la tecla Control mientras lo arrastra al Controlador de vista de inicio para convertirlo en la **vista raíz** de la navegación.</span><span class="sxs-lookup"><span data-stu-id="2f880-139">Add a **Navigation Controller** to your storyboard, and control-drag to Home View Controller to make it the **root view** of navigation.</span></span> <span data-ttu-id="2f880-140">Asegúrese de que esté seleccionado **Is Initial View Controller** en el Inspector de atributos solo para el Controlador de navegación.</span><span class="sxs-lookup"><span data-stu-id="2f880-140">Make sure the **Is Initial View Controller** in Attributes inspector is selected for the Navigation Controller only.</span></span>
5. <span data-ttu-id="2f880-141">Agregue un **Controlador de vista** al guion gráfico y agregue una **Vista de imagen**.</span><span class="sxs-lookup"><span data-stu-id="2f880-141">Add a **View Controller** to storyboard and add an **Image View**.</span></span> <span data-ttu-id="2f880-142">Esta es la página que verán los usuarios una vez que deseen obtener más información al hacer clic en la notificación.</span><span class="sxs-lookup"><span data-stu-id="2f880-142">This is the page users will see once they choose to learn more by clicking on the notifiication.</span></span> <span data-ttu-id="2f880-143">El guión gráfico debe tener el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f880-143">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="2f880-144">Haga clic en el **Controlador de vista de inicio** en el guion gráfico y asegúrese de que tiene **homeViewController** como su **Clase personalizada** e **Id. de guion gráfico** en el Inspector de identidad.</span><span class="sxs-lookup"><span data-stu-id="2f880-144">Click on the **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under the Identity inspector.</span></span>
7. <span data-ttu-id="2f880-145">Haga lo mismo para el Controlador de vista de imagen como **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="2f880-145">Do the same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="2f880-146">Luego cree una nueva clase de controlador de vista con título **imageViewController** para controlar la interfaz de usuario que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="2f880-146">Then, create a new View Controller class titled **imageViewController** to handle the UI you just created.</span></span>
9. <span data-ttu-id="2f880-147">En **imageViewController.h**, agregue lo siguiente a las declaraciones de la interfaz del controlador.</span><span class="sxs-lookup"><span data-stu-id="2f880-147">In **imageViewController.h**, add the following to the controller's interface declarations.</span></span> <span data-ttu-id="2f880-148">Asegúrese de mantener presionada la tecla Control mientras arrastra la vista de la imagen del guión gráfico a estas propiedades para vincularlas:</span><span class="sxs-lookup"><span data-stu-id="2f880-148">Make sure to control-drag from the storyboard image view to these properties to link the two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="2f880-149">En **imageViewController.m**, agregue lo siguiente al final de **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="2f880-149">In **imageViewController.m**, add the following at the end of **viewDidload**:</span></span>
    
        // Display the UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="2f880-150">En **AppDelegate.m**, importe el controlador de imagen que creó:</span><span class="sxs-lookup"><span data-stu-id="2f880-150">In **AppDelegate.m**, import the image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="2f880-151">Agregue una sección de interfaz con la siguiente declaración:</span><span class="sxs-lookup"><span data-stu-id="2f880-151">Add an interface section with the following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect to Image View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="2f880-152">En **AppDelegate**, asegúrese de que la aplicación registra notificaciones silenciosas en **application: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="2f880-152">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="2f880-153">Reemplace la siguiente implementación para **application:didRegisterForRemoteNotificationsWithDeviceToken** a fin de considerar los cambios en la interfaz de usuario del guion gráfico:</span><span class="sxs-lookup"><span data-stu-id="2f880-153">Subsitute in the following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** to take the storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at the root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="2f880-154">A continuación, agregue los siguientes métodos a **AppDelegate.m** para recuperar la imagen del extremo y enviar una notificación local cuando la recuperación se complete.</span><span class="sxs-lookup"><span data-stu-id="2f880-154">Then, add the following methods to **AppDelegate.m** to retrieve the image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="2f880-155">Asegúrese de sustituir el marcador de posición `{backend endpoint}` por el extremo del back-end:</span><span class="sxs-lookup"><span data-stu-id="2f880-155">Make sure to substitute the placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
                   // From NSData to UIImage
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
   
                       // "5" is arbitrary here to give you enough time to quit out of the app and receive push notifications
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
           // Add "else if" here to handle more types of rich content such as url, sound files, etc.
       }
3. <span data-ttu-id="2f880-156">Controle la notificación local anterior abriendo el controlador de vista de imagen en **AppDelegate.m** con los siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="2f880-156">Handle the local notification above by opening up the image view controller in **AppDelegate.m** with the following methods:</span></span>
   
       // Helper: redirect users to image view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image to image view controller
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
           // Add "else if" here to handle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-the-application"></a><span data-ttu-id="2f880-157">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2f880-157">Run the Application</span></span>
1. <span data-ttu-id="2f880-158">En XCode, ejecute la aplicación en un dispositivo iOS físico (las notificaciones de inserción no funcionarán en el simulador).</span><span class="sxs-lookup"><span data-stu-id="2f880-158">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="2f880-159">En la interfaz de usuario de aplicación de iOS, escriba un nombre de usuario y una contraseña del mismo valor para la autenticación y haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="2f880-159">In the iOS app UI, enter a username and password of the same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="2f880-160">Haga clic en **Enviar inserción** y deberá ver una alerta en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f880-160">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="2f880-161">Si hace clic en **Más**, verá la imagen que eligió para incluirla en el back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f880-161">If you click on **More**, you will be brought to the image you chose to include in your app backend.</span></span>
4. <span data-ttu-id="2f880-162">También puede hacer clic en **Enviar inserción** y presionar inmediatamente el botón de inicio del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2f880-162">You can also click **Send push** and immediately press the home button of your device.</span></span> <span data-ttu-id="2f880-163">En unos momentos recibirá una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="2f880-163">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="2f880-164">Si pulsa en ella o hace clic en Más, verá la aplicación y el contenido de imagen enriquecida.</span><span class="sxs-lookup"><span data-stu-id="2f880-164">If you tap on it or click More, you will be brought to your app and the rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
