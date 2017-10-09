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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="3b2a9-103">Usar toosend centros de notificaciones noticias de última hora</span><span class="sxs-lookup"><span data-stu-id="3b2a9-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="3b2a9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="3b2a9-104">Overview</span></span>
<span data-ttu-id="3b2a9-105">Este tema muestra cómo toouse centros de notificaciones de Azure toobroadcast importantes noticias notificaciones tooan aplicación de iOS.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan iOS app.</span></span> <span data-ttu-id="3b2a9-106">Cuando haya finalizado, se puede tooregister puede romper la categorías de noticias que le interesen y recibir notificaciones de inserción solo para esas categorías.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="3b2a9-107">Este escenario es un patrón común para muchas aplicaciones donde las notificaciones tienen toogroups toobe enviado de los usuarios que previamente se han declarado el interés en ellos, por ejemplo, aplicaciones de ventiladores de música, etcetera, lector RSS.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="3b2a9-108">Escenarios de difusión se habilitan mediante la inclusión de uno o varios *etiquetas* al crear un registro en el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="3b2a9-109">Cuando se envían las notificaciones tooa etiqueta, todos los dispositivos que se han registrado para la etiqueta de hello recibirá notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="3b2a9-110">Dado que las etiquetas son simplemente cadenas, no tiene toobe aprovisionado de antemano.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="3b2a9-111">Para obtener más información acerca de las etiquetas, consulte demasiado[notificación centros de enrutamiento y expresiones de etiqueta](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="3b2a9-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b2a9-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3b2a9-112">Prerequisites</span></span>
<span data-ttu-id="3b2a9-113">En este tema se basa en la aplicación hello que creó en [empezar a trabajar con los centros de notificaciones][get-started].</span><span class="sxs-lookup"><span data-stu-id="3b2a9-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="3b2a9-114">Antes de comenzar este tutorial, debe haber completado la [Introducción a Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="3b2a9-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="3b2a9-115">Agregar categoría selección toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="3b2a9-115">Add category selection toohello app</span></span>
<span data-ttu-id="3b2a9-116">Hola primer paso es tooadd Hola UI elementos tooyour guión gráfico existente que permiten Hola usuario tooselect categorías tooregister.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-116">hello first step is tooadd hello UI elements tooyour existing storyboard that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="3b2a9-117">categorías de Hello seleccionadas por el usuario se almacenan en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="3b2a9-118">Cuando se inicia la aplicación hello, se crea un registro de dispositivos en el centro de notificaciones con las categorías de hello seleccionado como etiquetas.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="3b2a9-119">En su MainStoryboard_iPhone.storyboard agregue Hola de los componentes siguientes de la biblioteca de objetos de hello:</span><span class="sxs-lookup"><span data-stu-id="3b2a9-119">In your MainStoryboard_iPhone.storyboard add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="3b2a9-120">Una etiqueta con el texto "Breaking News",</span><span class="sxs-lookup"><span data-stu-id="3b2a9-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="3b2a9-121">Etiquetas con los textos de categoría "World", "Politics", "Business", "Technology", "Science", "Sports",</span><span class="sxs-lookup"><span data-stu-id="3b2a9-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="3b2a9-122">Seis modificadores, uno por cada categoría, establezca cada conmutador **estado** toobe **desactivar** de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-122">Six switches, one per category, set each switch **State** toobe **Off** by default.</span></span>
   * <span data-ttu-id="3b2a9-123">Un botón etiquetado con "Subscribe"</span><span class="sxs-lookup"><span data-stu-id="3b2a9-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="3b2a9-124">El guión gráfico debe tener el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="3b2a9-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="3b2a9-125">En el editor de Asistente de hello, cree las salidas de todos los conmutadores de Hola y llamarlos "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span><span class="sxs-lookup"><span data-stu-id="3b2a9-125">In hello assistant editor, create outlets for all hello switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="3b2a9-126">Cree una Acción para el botón con nombre "subscribe".</span><span class="sxs-lookup"><span data-stu-id="3b2a9-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="3b2a9-127">El ViewController.h debe contener grupos Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="3b2a9-127">Your ViewController.h should contain hello following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="3b2a9-128">Cree una nueva **clase Cocoa Touch** denominada `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="3b2a9-129">Copie Hola después el código de sección de la interfaz de Hola de archivo hello Notifications.h:</span><span class="sxs-lookup"><span data-stu-id="3b2a9-129">Copy hello following code in hello interface section of hello file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="3b2a9-130">Agregue Hola después tooNotifications.m la directiva de importación:</span><span class="sxs-lookup"><span data-stu-id="3b2a9-130">Add hello following import directive tooNotifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="3b2a9-131">Copie Hola después el código en la sección de implementación de Hola de archivo hello Notifications.m.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-131">Copy hello following code in hello implementation section of hello file Notifications.m.</span></span>
   
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



    <span data-ttu-id="3b2a9-132">Esta clase usa almacenamiento local toostore y recuperar las categorías de Hola de noticias que van a recibir este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-132">This class uses local storage toostore and retrieve hello categories of news that this device will receive.</span></span> <span data-ttu-id="3b2a9-133">Además, contiene un tooregister de método para estas categorías mediante un [plantilla](notification-hubs-templates-cross-platform-push-messages.md) registro.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-133">Also, it contains a method tooregister for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="3b2a9-134">En el archivo de AppDelegate.h hello, agregue una instrucción import para Notifications.h y agregar una propiedad de una instancia de clase de las notificaciones de hello:</span><span class="sxs-lookup"><span data-stu-id="3b2a9-134">In hello AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of hello Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="3b2a9-135">Hola **didFinishLaunchingWithOptions** método AppDelegate.m, agregar Hola código tooinitialize Hola notificaciones instancia a partir del método hello Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-135">In hello **didFinishLaunchingWithOptions** method in AppDelegate.m, add hello code tooinitialize hello notifications instance at hello beginning of hello method.</span></span>  
   
    <span data-ttu-id="3b2a9-136">`HUBNAME`y `HUBLISTENACCESS` (definido en hubinfo.h) ya debe disponer de hello `<hub name>` y `<connection string with listen access>` marcadores de posición se reemplazan con la notificación concentrador hello y nombre de cadena de conexión para *DefaultListenSharedAccessSignature*que ha obtenido antes</span><span class="sxs-lookup"><span data-stu-id="3b2a9-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have hello `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="3b2a9-137">Dado que las credenciales que se distribuyen con una aplicación cliente no son generalmente seguras, debe distribuir solo clave hello para el acceso de escucha con la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="3b2a9-138">Escuchar habilita el acceso que no se puede modificar su tooregister de aplicación para notificaciones, pero los registros existentes y no se enviarán las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-138">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="3b2a9-139">clave de acceso completa de Hola se usa en un servicio seguro back-end para enviar notificaciones y cambiar los registros existentes.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-139">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="3b2a9-140">Hola **didRegisterForRemoteNotificationsWithDeviceToken** método en AppDelegate.m, reemplace el código de hello en método hello con hello después de la clase de código toopass hello dispositivo toohello token las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-140">In hello **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace hello code in hello method with hello following code toopass hello device token toohello notifications class.</span></span> <span data-ttu-id="3b2a9-141">clase de notificaciones de Hello llevará a cabo Hola registrarse para recibir notificaciones con las categorías de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-141">hello notifications class will perform hello registering for notifications with hello categories.</span></span> <span data-ttu-id="3b2a9-142">Si el usuario de hello cambia las selecciones de categorías, llamamos a hello `subscribeWithCategories` método en respuesta toohello **suscribirse** tooupdate botón ellos.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-142">If hello user changes category selections, we call hello `subscribeWithCategories` method in response toohello **subscribe** button tooupdate them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3b2a9-143">Dado que puede cambiar símbolo (token) de dispositivo de hello asignado por el servicio de notificación de inserción de Apple (APNS) de Hola en cualquier momento, se deben registrar para notificaciones con frecuencia tooavoid errores de notificación.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-143">Because hello device token assigned by hello Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="3b2a9-144">En este ejemplo se registra para la notificación cada vez que inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-144">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="3b2a9-145">Para las aplicaciones que se ejecutan con frecuencia, más de una vez al día, puede probablemente Omitir ancho de banda de registro toopreserve si ha pasado menos de un día desde el registro de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-145">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
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

    <span data-ttu-id="3b2a9-146">Tenga en cuenta que en este momento no debería haber ningún otro código en hello **didRegisterForRemoteNotificationsWithDeviceToken** método.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-146">Note that at this point there should be no other code in hello **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="3b2a9-147">Hello métodos siguientes deben estar ya presentes en AppDelegate.m complete hello [empezar a trabajar con los centros de notificaciones] [ get-started] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-147">hello following methods should already be present in AppDelegate.m from completing hello [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="3b2a9-148">De lo contrario, agréguelos.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-148">If not, add them.</span></span>
   
    <span data-ttu-id="3b2a9-149">-(void) MessageBox:(NSString *) título mensaje:(NSString *) messageText {}</span><span class="sxs-lookup"><span data-stu-id="3b2a9-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="3b2a9-150">}</span><span class="sxs-lookup"><span data-stu-id="3b2a9-150">}</span></span>
   
   * <span data-ttu-id="3b2a9-151">aplicación (void):(UIApplication *) aplicación didReceiveRemoteNotification: (NSDictionary *) información de usuario {NSLog (@"% @", información de usuario);   [mensaje self MessageBox:@"Notification": [valueForKey:@"alert [información de usuario objectForKey:@"aps"]"]]; }</span><span class="sxs-lookup"><span data-stu-id="3b2a9-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="3b2a9-152">Este método controla las notificaciones que recibe cuando se está ejecutando, mostrando una sencilla aplicación hello **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-152">This method handles notifications received when hello app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="3b2a9-153">En ViewController.m, agregue una instrucción de importación para hello AppDelegate.h y copiar después el código en hello genera XCode **suscribirse** método.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-153">In ViewController.m, add a import statement for AppDelegate.h and copy hello following code into hello XCode-generated **subscribe** method.</span></span> <span data-ttu-id="3b2a9-154">Este código actualizará Hola notificación registro toouse Hola nuevas etiquetas de categoría Hola usuario ha elegido en la interfaz de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-154">This code will update hello notification registration toouse hello new category tags hello user has chosen in hello user interface.</span></span>
   
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
   
   <span data-ttu-id="3b2a9-155">Este método crea un **NSMutableArray** de categorías y se utiliza hello **notificaciones** lista de clases toostore Hola Hola local almacenamiento registros Hola correspondiente etiquetas y con el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-155">This method creates an **NSMutableArray** of categories and uses hello **Notifications** class toostore hello list in hello local storage and registers hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="3b2a9-156">Cuando se cambian las categorías, se vuelve a crear el registro de hello con nuevas categorías de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-156">When categories are changed, hello registration is recreated with hello new categories.</span></span>
3. <span data-ttu-id="3b2a9-157">En ViewController.m, agregue Hola después el código de hello **viewDidLoad** interfaz de usuario de método tooset Hola basadas en categorías de hello guardado previamente.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-157">In ViewController.m, add hello following code in hello **viewDidLoad** method tooset hello user interface based on hello previously saved categories.</span></span>

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="3b2a9-158">aplicación Hello ahora puede almacenar un conjunto de categorías en hello dispositivo almacenamiento local usa tooregister con el centro de notificaciones de hello cada vez que inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-158">hello app can now store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello app starts.</span></span>  <span data-ttu-id="3b2a9-159">usuario de Hello puede cambiar la selección de Hola de categorías en tiempo de ejecución y haga clic en hello **suscribirse** registro de hello tooupdate de método para dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-159">hello user can change hello selection of categories at runtime and click hello **subscribe** method tooupdate hello registration for hello device.</span></span> <span data-ttu-id="3b2a9-160">A continuación, actualizará Hola Hola de toosend aplicación importantes notificaciones de noticias directamente en la propia aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-160">Next, you will update hello app toosend hello breaking news notifications directly in hello app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="3b2a9-161">(Opcional) Envío de notificaciones con etiquetas</span><span class="sxs-lookup"><span data-stu-id="3b2a9-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="3b2a9-162">Si no tienes acceso tooVisual Studio, puede omitir la sección siguiente toohello y enviar notificaciones desde la propia aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-162">If you don't have access tooVisual Studio, you can skip toohello next section and send notifications from hello app itself.</span></span> <span data-ttu-id="3b2a9-163">También puede enviar notificación de plantilla adecuados de Hola de hello [Portal clásico de Azure] usando pestaña de depuración de hello en el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-163">You can also send hello proper template notification from hello [Azure Classic Portal] using hello debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a><span data-ttu-id="3b2a9-164">(opcional) Enviar notificaciones de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="3b2a9-164">(optional) Send notifications from hello device</span></span>
<span data-ttu-id="3b2a9-165">Normalmente se enviaría notificaciones por un servicio back-end, pero puede enviar notificaciones de noticias de separación directamente desde la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from hello app.</span></span> <span data-ttu-id="3b2a9-166">toodo esto actualizaremos hello `SendNotificationRESTAPI` método que hemos definido en hello [empezar a trabajar con los centros de notificaciones] [ get-started] tutorial.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-166">toodo this we will update hello `SendNotificationRESTAPI` method that we defined in hello [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="3b2a9-167">Hola de actualización de ViewController.m `SendNotificationRESTAPI` método como sigue para que acepta un parámetro para la etiqueta de categoría de Hola y las envía Hola apropiado [plantilla](notification-hubs-templates-cross-platform-push-messages.md) notificación.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-167">In ViewController.m update hello `SendNotificationRESTAPI` method as follows so that it accepts a parameter for hello category tag and sends hello proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
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
2. <span data-ttu-id="3b2a9-168">Hola de actualización de ViewController.m **enviar notificación** acción tal como se muestra en el código de hello que sigue.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-168">In ViewController.m update hello **Send Notification** action as shown in hello code that follows.</span></span> <span data-ttu-id="3b2a9-169">Para que envíe notificaciones de hello utilizando cada etiqueta de forma individual y enviar toomultiple plataformas.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-169">So that it will send hello notifications using each tag individually and send toomultiple platforms.</span></span>

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



1. <span data-ttu-id="3b2a9-170">Recompile el proyecto y asegúrese de que no haya errores de compilación.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="3b2a9-171">Ejecutar aplicación hello y generar notificaciones</span><span class="sxs-lookup"><span data-stu-id="3b2a9-171">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="3b2a9-172">Presione Hola ejecutar botón toobuild Hola proyecto y de iniciar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-172">Press hello Run button toobuild hello project and start hello app.</span></span> <span data-ttu-id="3b2a9-173">Seleccione algunos tooand de toosubscribe de opciones de separación de noticias, a continuación, presione hello **suscribir** botón.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-173">Select some breaking news options toosubscribe tooand then press hello **Subscribe** button.</span></span> <span data-ttu-id="3b2a9-174">Debería ver un cuadro de diálogo que indica hello las notificaciones se han suscrito.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-174">You should see a dialog indicating hello notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="3b2a9-175">Cuando eliges **suscribir**, Hola Hola seleccionado categorías de aplicación se convierte en etiquetas y solicita un nuevo registro de dispositivo para etiquetas de hello seleccionada del centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-175">When you choose **Subscribe**, hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span>
2. <span data-ttu-id="3b2a9-176">Escriba un toobe de mensaje enviado como noticias de última hora, a continuación, presione hello **enviar notificación** botón.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-176">Enter a message toobe sent as breaking news then press hello **Send Notification** button.</span></span> <span data-ttu-id="3b2a9-177">También puede ejecutar las notificaciones toogenerate de aplicación de hello .NET consola.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-177">Alternatively, run hello .NET console app toogenerate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="3b2a9-178">Cada noticias de toobreaking dispositivo suscrito recibirá notificaciones de noticias de separación de hello que acabamos de enviar.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-178">Each device subscribed toobreaking news will receive hello breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b2a9-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b2a9-179">Next steps</span></span>
<span data-ttu-id="3b2a9-180">En este tutorial hemos visto cómo toobroadcast noticias de última hora por categoría.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-180">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="3b2a9-181">Considere la posibilidad de completar uno de hello tutoriales que indican errores de otros escenarios avanzados de centros de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="3b2a9-181">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="3b2a9-182">**[Utilice noticias de última hora de toobroadcast localizado de los centros de notificaciones]**</span><span class="sxs-lookup"><span data-stu-id="3b2a9-182">**[Use Notification Hubs toobroadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="3b2a9-183">Obtenga información acerca de cómo hello tooexpand interrumpir el envío de noticias aplicación tooenable localizar las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="3b2a9-183">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
