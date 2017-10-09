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
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="7e708-104">Inserción enriquecida de los Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="7e708-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="7e708-105">Información general</span><span class="sxs-lookup"><span data-stu-id="7e708-105">Overview</span></span>
<span data-ttu-id="7e708-106">En orden tooengage a los usuarios con contenido enriquecido instantánea, una aplicación podría querer toopush más allá de texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="7e708-106">In order tooengage users with instant rich contents, an application might want toopush beyond plain text.</span></span> <span data-ttu-id="7e708-107">Estas notificaciones promueven las interacciones de los usuarios y presentan contenido como direcciones URL, sonidos, imágenes o cupones y más.</span><span class="sxs-lookup"><span data-stu-id="7e708-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="7e708-108">Este tutorial se basa en hello [informar a los usuarios](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tema y muestra cómo toosend insertar las notificaciones que incorporan cargas (por ejemplo, imagen).</span><span class="sxs-lookup"><span data-stu-id="7e708-108">This tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how toosend push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="7e708-109">Este tutorial es compatible con iOS 7 y 8.</span><span class="sxs-lookup"><span data-stu-id="7e708-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="7e708-110">En un alto nivel:</span><span class="sxs-lookup"><span data-stu-id="7e708-110">At a high level:</span></span>

1. <span data-ttu-id="7e708-111">Hola aplicación back-end:</span><span class="sxs-lookup"><span data-stu-id="7e708-111">hello app backend:</span></span>
   * <span data-ttu-id="7e708-112">Almacenes de Hola carga enriquecida (en este caso, la imagen) en almacenamiento de base de datos o local de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="7e708-112">Stores hello rich payload (in this case, image) in hello backend database/local storage</span></span>
   * <span data-ttu-id="7e708-113">Envía el Id. de este dispositivo de notificación enriquecido toohello</span><span class="sxs-lookup"><span data-stu-id="7e708-113">Sends ID of this rich notification toohello device</span></span>
2. <span data-ttu-id="7e708-114">Aplicación Hola dispositivo:</span><span class="sxs-lookup"><span data-stu-id="7e708-114">App on hello device:</span></span>
   * <span data-ttu-id="7e708-115">Contactos Hola solicitando la carga enriquecido Hola con el Id. de hello recibe de back-end</span><span class="sxs-lookup"><span data-stu-id="7e708-115">Contacts hello backend requesting hello rich payload with hello ID it receives</span></span>
   * <span data-ttu-id="7e708-116">Envía notificaciones a los usuarios en el dispositivo de hello cuando se completa la recuperación de datos y muestra la carga de hello inmediatamente cuando los usuarios pulsan toolearn más</span><span class="sxs-lookup"><span data-stu-id="7e708-116">Sends users notifications on hello device when data retrieval is complete, and shows hello payload immediately when users tap toolearn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="7e708-117">Proyecto WebAPI</span><span class="sxs-lookup"><span data-stu-id="7e708-117">WebAPI Project</span></span>
1. <span data-ttu-id="7e708-118">En Visual Studio, abra hello **AppBackend** proyecto que creó en hello [informar a los usuarios](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7e708-118">In Visual Studio, open hello **AppBackend** project that you created in hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="7e708-119">Obtener una imagen que desee toonotify a los usuarios y colocarla en un **img** carpeta en el directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7e708-119">Obtain an image you would like toonotify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="7e708-120">Haga clic en **mostrar todos los archivos** en hello en el Explorador de soluciones y haga clic en carpeta de hello demasiado**incluir en el proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7e708-120">Click **Show All Files** in hello Solution Explorer, and right-click hello folder too**Include In Project**.</span></span>
4. <span data-ttu-id="7e708-121">Con la imagen de hello seleccionada, cambiar su acción de compilación en la ventana Propiedades también**recurso incrustado**.</span><span class="sxs-lookup"><span data-stu-id="7e708-121">With hello image selected, change its Build Action in Properties window too**Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="7e708-122">En **Notifications.cs**, agregue Hola siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="7e708-122">In **Notifications.cs**, add hello following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="7e708-123">Hola de actualización completa **notificaciones** clase con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="7e708-123">Update hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="7e708-124">Ser tooreplace seguro de los marcadores de posición de hello con sus credenciales de base de datos central de notificaciones y el nombre de archivo de imagen.</span><span class="sxs-lookup"><span data-stu-id="7e708-124">Be sure tooreplace hello placeholders with your notification hub credentials and image file name.</span></span>
   
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
   > <span data-ttu-id="7e708-125">(opcional) Consulte demasiado[cómo tooembed y acceder a recursos con Visual C#](http://support.microsoft.com/kb/319292) para obtener más información acerca de cómo tooadd y obtener los recursos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7e708-125">(optional) Refer too[How tooembed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how tooadd and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="7e708-126">En **NotificationsController.cs**, volver a definir **NotificationsController** con hello siguientes fragmentos de código.</span><span class="sxs-lookup"><span data-stu-id="7e708-126">In **NotificationsController.cs**, redefine **NotificationsController**  with hello following snippets.</span></span> <span data-ttu-id="7e708-127">Esto envía un toodevice de Id. de la notificación inicial silenciosa enriquecida y permite la recuperación de cliente de imagen:</span><span class="sxs-lookup"><span data-stu-id="7e708-127">This sends an initial silent rich notification id toodevice and allows client-side retrieval of image:</span></span>
   
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
8. <span data-ttu-id="7e708-128">Ahora se implementará volver a este sitio Web de Azure de tooan de aplicación en orden toomake, accesible desde todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7e708-128">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="7e708-129">Haga doble clic en hello **AppBackend** de proyecto y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="7e708-129">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="7e708-130">Seleccione Sitio web Azure como destino de publicación.</span><span class="sxs-lookup"><span data-stu-id="7e708-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="7e708-131">Inicie sesión con su cuenta de Azure y seleccione un sitio Web nuevo o existente y tome nota de hello **dirección URL de destino** propiedad Hola **conexión** ficha. Nos referiremos toothis URL según su *punto de conexión de back-end* más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7e708-131">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="7e708-132">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="7e708-132">Click **Publish**.</span></span>

## <a name="modify-hello-ios-project"></a><span data-ttu-id="7e708-133">Modificar el proyecto de iOS de Hola</span><span class="sxs-lookup"><span data-stu-id="7e708-133">Modify hello iOS project</span></span>
<span data-ttu-id="7e708-134">Ahora que ha modificado su Hola solo de aplicación back-end toosend *identificador* de una notificación, se cambia su toohandle de aplicación de iOS ese identificador y recuperar mensajes enriquecido Hola desde el back-end.</span><span class="sxs-lookup"><span data-stu-id="7e708-134">Now that you have modified your app backend toosend just hello *id* of a notification, you will change your iOS app toohandle that id and retrieve hello rich message from your backend.</span></span>

1. <span data-ttu-id="7e708-135">Abra el proyecto de iOS y habilitar las notificaciones de remotas que va de destino principal de la aplicación tooyour en hello **destinos** sección.</span><span class="sxs-lookup"><span data-stu-id="7e708-135">Open your iOS project, and enable remote notifications by going tooyour main app target in hello **Targets** section.</span></span>
2. <span data-ttu-id="7e708-136">Haga clic en **capacidades**, activar **modos en segundo plano**y compruebe hello **notificaciones remoto** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="7e708-136">Click on **Capabilities**, turn on **Background Modes**, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="7e708-137">Vaya demasiado**Main.storyboard**y asegúrese de que tiene un controlador de vista (usan tooas inicio View-Controller en este tutorial) desde [notificar al usuario](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7e708-137">Go too**Main.storyboard**, and make sure you have a View Controller (refered tooas Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="7e708-138">Agregar un **controlador navegación** tooyour de guión gráfico y arrastre control tooHome View Controller toomake lo Hola **raíz vista** de navegación.</span><span class="sxs-lookup"><span data-stu-id="7e708-138">Add a **Navigation Controller** tooyour storyboard, and control-drag tooHome View Controller toomake it hello **root view** of navigation.</span></span> <span data-ttu-id="7e708-139">Asegúrese de hello seguro **es View-Controller inicial** en atributos inspector está seleccionado para hello controlador de navegación.</span><span class="sxs-lookup"><span data-stu-id="7e708-139">Make sure hello **Is Initial View Controller** in Attributes inspector is selected for hello Navigation Controller only.</span></span>
5. <span data-ttu-id="7e708-140">Agregar un **View Controller** toostoryboard y agregue un **imagen de vista**.</span><span class="sxs-lookup"><span data-stu-id="7e708-140">Add a **View Controller** toostoryboard and add an **Image View**.</span></span> <span data-ttu-id="7e708-141">Se trata de página Hola los usuarios verán cuando deciden toolearn más haciendo clic en notifiication Hola.</span><span class="sxs-lookup"><span data-stu-id="7e708-141">This is hello page users will see once they choose toolearn more by clicking on hello notifiication.</span></span> <span data-ttu-id="7e708-142">El guión gráfico debe tener el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e708-142">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="7e708-143">Haga clic en hello **inicio View Controller** en el guión gráfico y asegúrese de que tiene **homeViewController** como su **clase personalizada** y **Id. de guión gráfico**en inspector de identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e708-143">Click on hello **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under hello Identity inspector.</span></span>
7. <span data-ttu-id="7e708-144">Hola mismo controlador de vista de imagen como **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="7e708-144">Do hello same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="7e708-145">A continuación, cree una nueva clase de controlador de vista denominada **imageViewController** toohandle Hola interfaz de usuario que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="7e708-145">Then, create a new View Controller class titled **imageViewController** toohandle hello UI you just created.</span></span>
9. <span data-ttu-id="7e708-146">En **imageViewController.h**, agregar Hola siguientes declaraciones de interfaz del controlador de toohello.</span><span class="sxs-lookup"><span data-stu-id="7e708-146">In **imageViewController.h**, add hello following toohello controller's interface declarations.</span></span> <span data-ttu-id="7e708-147">Asegúrese de arrastrar toocontrol seguro desde Hola guión gráfico imagen Vista toothese propiedades toolink Hola dos:</span><span class="sxs-lookup"><span data-stu-id="7e708-147">Make sure toocontrol-drag from hello storyboard image view toothese properties toolink hello two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="7e708-148">En **imageViewController.m**, agregue siguiente Hola final Hola de **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="7e708-148">In **imageViewController.m**, add hello following at hello end of **viewDidload**:</span></span>
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="7e708-149">En **AppDelegate.m**, controlador de imagen de Hola de importación que creó:</span><span class="sxs-lookup"><span data-stu-id="7e708-149">In **AppDelegate.m**, import hello image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="7e708-150">Agregue una sección de la interfaz con hello siguiente declaración:</span><span class="sxs-lookup"><span data-stu-id="7e708-150">Add an interface section with hello following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="7e708-151">En **AppDelegate**, asegúrese de que la aplicación registra notificaciones silenciosas en **application: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="7e708-151">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="7e708-152">Sustituirlas Hola después de la implementación de **aplicación: didRegisterForRemoteNotificationsWithDeviceToken** guión gráfico de hello tootake cambia de interfaz de usuario en cuenta:</span><span class="sxs-lookup"><span data-stu-id="7e708-152">Subsitute in hello following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** tootake hello storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="7e708-153">A continuación, agregue Hola siguiendo métodos demasiado**AppDelegate.m** tooretrieve Hola imagen desde el punto de conexión y enviar una notificación local una vez completada la recuperación.</span><span class="sxs-lookup"><span data-stu-id="7e708-153">Then, add hello following methods too**AppDelegate.m** tooretrieve hello image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="7e708-154">Asegúrese de marcador de posición de seguro toosubstitute hello `{backend endpoint}` con su punto de conexión de back-end:</span><span class="sxs-lookup"><span data-stu-id="7e708-154">Make sure toosubstitute hello placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
3. <span data-ttu-id="7e708-155">Controlar la notificación local de hello anteriormente abriendo el controlador de vista de imagen de hello en **AppDelegate.m** con hello siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="7e708-155">Handle hello local notification above by opening up hello image view controller in **AppDelegate.m** with hello following methods:</span></span>
   
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

## <a name="run-hello-application"></a><span data-ttu-id="7e708-156">Ejecutar aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="7e708-156">Run hello Application</span></span>
1. <span data-ttu-id="7e708-157">En XCode, ejecute la aplicación hello en un dispositivo de E/s físicas (inserción notificaciones no funcionará en el simulador de hello).</span><span class="sxs-lookup"><span data-stu-id="7e708-157">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="7e708-158">En la aplicación de iOS de hello interfaz de usuario, escriba un nombre de usuario y una contraseña de hello mismo valor para la autenticación y haga clic en **inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="7e708-158">In hello iOS app UI, enter a username and password of hello same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="7e708-159">Haga clic en **Enviar inserción** y deberá ver una alerta en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e708-159">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="7e708-160">Si hace clic en **más**, podrá imagen toohello poner eligió tooinclude en el back-end de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7e708-160">If you click on **More**, you will be brought toohello image you chose tooinclude in your app backend.</span></span>
4. <span data-ttu-id="7e708-161">También puede hacer clic en **enviar inserción** e inmediatamente presione el botón de inicio de hello del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e708-161">You can also click **Send push** and immediately press hello home button of your device.</span></span> <span data-ttu-id="7e708-162">En unos momentos recibirá una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="7e708-162">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="7e708-163">Si puntear en él o haga clic en más, se encontrarán tooyour hello y aplicación de contenido de imagen enriquecido.</span><span class="sxs-lookup"><span data-stu-id="7e708-163">If you tap on it or click More, you will be brought tooyour app and hello rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
