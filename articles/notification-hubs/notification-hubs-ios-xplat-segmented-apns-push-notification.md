---
title: "Tutorial de noticias de última hora en los Centros de notificaciones: iOS"
description: "Obtenga información acerca del uso de Centros de notificaciones de Azure para enviar notificaciones de noticias de última hora en dispositivos iOS."
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
ms.openlocfilehash: dc47250db6fb3a2853dae24e02bda236154d93fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="a3eab-103">Uso de los Centros de notificaciones para enviar noticias de última hora</span><span class="sxs-lookup"><span data-stu-id="a3eab-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="a3eab-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a3eab-104">Overview</span></span>
<span data-ttu-id="a3eab-105">Este tema muestra cómo puede usar Azure Notification Hubs para difundir notificaciones de noticias de última hora en una aplicación iOS.</span><span class="sxs-lookup"><span data-stu-id="a3eab-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an iOS app.</span></span> <span data-ttu-id="a3eab-106">Cuando lo complete, podrá registrar las categorías de noticias de última hora en las que esté interesado y recibir solo notificaciones de inserción para esas categorías.</span><span class="sxs-lookup"><span data-stu-id="a3eab-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="a3eab-107">Este escenario es un patrón común para muchas aplicaciones en las que las notificaciones tienen que enviarse a grupos de usuarios que han mostrado previamente interés en ellas, por ejemplo, lectores RSS, aplicaciones para aficionados a la música, etc.</span><span class="sxs-lookup"><span data-stu-id="a3eab-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="a3eab-108">Los escenarios de difusión se habilitan mediante la inclusión de una o más *etiquetas* cuando se crea un registro en el Centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="a3eab-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="a3eab-109">Cuando las notificaciones se envían a una etiqueta, todos los dispositivos registrados para la etiqueta recibirán la notificación.</span><span class="sxs-lookup"><span data-stu-id="a3eab-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="a3eab-110">Puesto que las etiquetas son cadenas simples, no tendrán que aprovisionarse antes.</span><span class="sxs-lookup"><span data-stu-id="a3eab-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="a3eab-111">Para información sobre las etiquetas, consulte [Expresiones de etiqueta y enrutamiento de los Centros de notificaciones](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="a3eab-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3eab-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a3eab-112">Prerequisites</span></span>
<span data-ttu-id="a3eab-113">Este tema se basa en la aplicación que creó en [Introducción a Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="a3eab-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="a3eab-114">Antes de comenzar este tutorial, debe haber completado la [Introducción a Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="a3eab-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="a3eab-115">Adición de una selección de categorías a la aplicación</span><span class="sxs-lookup"><span data-stu-id="a3eab-115">Add category selection to the app</span></span>
<span data-ttu-id="a3eab-116">El primer paso es agregar los elementos de la interfaz de usuario al guión gráfico existente que permiten al usuario seleccionar las categorías que se van a registrar.</span><span class="sxs-lookup"><span data-stu-id="a3eab-116">The first step is to add the UI elements to your existing storyboard that enable the user to select categories to register.</span></span> <span data-ttu-id="a3eab-117">Las categorías seleccionadas por un usuario se almacenan en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a3eab-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="a3eab-118">Cuando la aplicación se inicia, se crea un registro de dispositivos en el Centro de notificaciones con las categorías seleccionadas como etiquetas.</span><span class="sxs-lookup"><span data-stu-id="a3eab-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="a3eab-119">En MainStoryboard_iPhone.storyboard, agregue los siguientes componentes desde la biblioteca de objetos:</span><span class="sxs-lookup"><span data-stu-id="a3eab-119">In your MainStoryboard_iPhone.storyboard add the following components from the object library:</span></span>
   
   * <span data-ttu-id="a3eab-120">Una etiqueta con el texto "Breaking News",</span><span class="sxs-lookup"><span data-stu-id="a3eab-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="a3eab-121">Etiquetas con los textos de categoría "World", "Politics", "Business", "Technology", "Science", "Sports",</span><span class="sxs-lookup"><span data-stu-id="a3eab-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="a3eab-122">Seis modificadores, uno por categoría, establecen que el **estado** de cada modificador sea **Off** (Desactivado) de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a3eab-122">Six switches, one per category, set each switch **State** to be **Off** by default.</span></span>
   * <span data-ttu-id="a3eab-123">Un botón etiquetado con "Subscribe"</span><span class="sxs-lookup"><span data-stu-id="a3eab-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="a3eab-124">El guión gráfico debe tener el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="a3eab-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="a3eab-125">En el editor del asistente, cree medios para todos los modificadores y llámelos "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch" y "SportsSwitch".</span><span class="sxs-lookup"><span data-stu-id="a3eab-125">In the assistant editor, create outlets for all the switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="a3eab-126">Cree una Acción para el botón con nombre "subscribe".</span><span class="sxs-lookup"><span data-stu-id="a3eab-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="a3eab-127">ViewController.h debe contener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a3eab-127">Your ViewController.h should contain the following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="a3eab-128">Cree una nueva **clase Cocoa Touch** denominada `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="a3eab-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="a3eab-129">Copie el siguiente código en la sección de interfaz del archivo Notifications.h:</span><span class="sxs-lookup"><span data-stu-id="a3eab-129">Copy the following code in the interface section of the file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="a3eab-130">Agregue la siguiente directiva de importación a Notifications.m:</span><span class="sxs-lookup"><span data-stu-id="a3eab-130">Add the following import directive to Notifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="a3eab-131">Copie el siguiente código en la sección de implementación del archivo Notifications.m:</span><span class="sxs-lookup"><span data-stu-id="a3eab-131">Copy the following code in the implementation section of the file Notifications.m.</span></span>
   
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



    <span data-ttu-id="a3eab-132">Esta clase usa el almacenamiento local para almacenar y recuperar las categorías de noticias que este dispositivo ha de recibir.</span><span class="sxs-lookup"><span data-stu-id="a3eab-132">This class uses local storage to store and retrieve the categories of news that this device will receive.</span></span> <span data-ttu-id="a3eab-133">También contiene un método para registrar estas categorías mediante un registro [Plantilla](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="a3eab-133">Also, it contains a method to register for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="a3eab-134">En el archivo AppDelegate.h, agregue una instrucción de importación para Notifications.h y agregue una propiedad de una instancia de la clase de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="a3eab-134">In the AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of the Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="a3eab-135">En el método **didFinishLaunchingWithOptions** de AppDelegate.m, agregue el código para inicializar la instancia de notificaciones al comienzo del método.</span><span class="sxs-lookup"><span data-stu-id="a3eab-135">In the **didFinishLaunchingWithOptions** method in AppDelegate.m, add the code to initialize the notifications instance at the beginning of the method.</span></span>  
   
    <span data-ttu-id="a3eab-136">`HUBNAME` y `HUBLISTENACCESS` (que se definen en hubinfo.h) deberían tener ya reemplazados los marcadores de posición `<hub name>` y `<connection string with listen access>` por el nombre del centro de notificaciones y la cadena de conexión de *DefaultListenSharedAccessSignature* que obtuvo anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a3eab-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have the `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="a3eab-137">Puesto que las credenciales que se distribuyen con una aplicación de cliente no son normalmente seguras, solo debe distribuir la clave para el acceso de escucha con la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="a3eab-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="a3eab-138">El acceso de escucha permite a la aplicación el registro de notificaciones, pero los registros existentes no pueden modificarse y las notificaciones no se pueden enviar.</span><span class="sxs-lookup"><span data-stu-id="a3eab-138">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="a3eab-139">La clave de acceso completo se usa en un servicio back-end protegido para el envío de notificaciones y el cambio de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="a3eab-139">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="a3eab-140">En el método **didRegisterForRemoteNotificationsWithDeviceToken** de AppDelegate.m, reemplace el código en el método por el código siguiente para pasar el token del dispositivo a la clase de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="a3eab-140">In the **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace the code in the method with the following code to pass the device token to the notifications class.</span></span> <span data-ttu-id="a3eab-141">La clase de notificaciones realizará el registro para las notificaciones con las categorías.</span><span class="sxs-lookup"><span data-stu-id="a3eab-141">The notifications class will perform the registering for notifications with the categories.</span></span> <span data-ttu-id="a3eab-142">Si el usuario cambia las selecciones de categoría, llamamos al método `subscribeWithCategories` en respuesta al botón **subscribe** para actualizarlas.</span><span class="sxs-lookup"><span data-stu-id="a3eab-142">If the user changes category selections, we call the `subscribeWithCategories` method in response to the **subscribe** button to update them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a3eab-143">Puesto que el token del dispositivo asignado por el Servicio de notificaciones de inserción de Apple (APNS) puede cambiar en cualquier momento, debe registrar las notificaciones con frecuencia para evitar errores de notificación.</span><span class="sxs-lookup"><span data-stu-id="a3eab-143">Because the device token assigned by the Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="a3eab-144">En este ejemplo se registra la notificación cada vez que se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3eab-144">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="a3eab-145">En las aplicaciones que se ejecutan con frecuencia, más de una vez al día, es posible que pueda omitir el registro para conservar el ancho de banda si pasa menos de un día del registro previo.</span><span class="sxs-lookup"><span data-stu-id="a3eab-145">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves the categories from local storage and requests a registration for these categories
        // each time the app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="a3eab-146">Tenga en cuenta que, en este punto, no debe haber otro código en el método **didRegisterForRemoteNotificationsWithDeviceToken** .</span><span class="sxs-lookup"><span data-stu-id="a3eab-146">Note that at this point there should be no other code in the **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="a3eab-147">Los métodos siguientes deben estar ya presentes en AppDelegate.m complete la [empezar a trabajar con los centros de notificaciones] [ get-started] tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3eab-147">The following methods should already be present in AppDelegate.m from completing the [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="a3eab-148">De lo contrario, agréguelos.</span><span class="sxs-lookup"><span data-stu-id="a3eab-148">If not, add them.</span></span>
   
    <span data-ttu-id="a3eab-149">-(void) MessageBox:(NSString *) título mensaje:(NSString *) messageText {}</span><span class="sxs-lookup"><span data-stu-id="a3eab-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="a3eab-150">}</span><span class="sxs-lookup"><span data-stu-id="a3eab-150">}</span></span>
   
   * <span data-ttu-id="a3eab-151">aplicación (void):(UIApplication *) aplicación didReceiveRemoteNotification: (NSDictionary *) información de usuario {NSLog (@"% @", información de usuario);   [mensaje self MessageBox:@"Notification": [valueForKey:@"alert [información de usuario objectForKey:@"aps"]"]]; }</span><span class="sxs-lookup"><span data-stu-id="a3eab-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="a3eab-152">Este método controla las notificaciones recibidas cuando la aplicación está en ejecución mostrando un **UIAlert**sencillo.</span><span class="sxs-lookup"><span data-stu-id="a3eab-152">This method handles notifications received when the app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="a3eab-153">En ViewController.m, agregue una instrucción de importación para AppDelegate.h y copie el código siguiente en método **subscribe** generado por XCode.</span><span class="sxs-lookup"><span data-stu-id="a3eab-153">In ViewController.m, add a import statement for AppDelegate.h and copy the following code into the XCode-generated **subscribe** method.</span></span> <span data-ttu-id="a3eab-154">Este código actualizará el registro de notificación para usar las nuevas etiquetas de categoría que el usuario ha elegido en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="a3eab-154">This code will update the notification registration to use the new category tags the user has chosen in the user interface.</span></span>
   
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
   
   <span data-ttu-id="a3eab-155">Este método crea un objeto **NSMutableArray** de categorías y usa la clase **Notifications** para almacenar la lista en el almacenamiento local y registrar las etiquetas correspondientes en el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="a3eab-155">This method creates an **NSMutableArray** of categories and uses the **Notifications** class to store the list in the local storage and registers the corresponding tags with your notification hub.</span></span> <span data-ttu-id="a3eab-156">Cuando se modifican las categorías, el registro vuelve a crearse con las nuevas categorías.</span><span class="sxs-lookup"><span data-stu-id="a3eab-156">When categories are changed, the registration is recreated with the new categories.</span></span>
3. <span data-ttu-id="a3eab-157">En ViewController.m, agregue el siguiente código en el método **viewDidLoad** para establecer la interfaz de usuario según las categorías previamente guardadas.</span><span class="sxs-lookup"><span data-stu-id="a3eab-157">In ViewController.m, add the following code in the **viewDidLoad** method to set the user interface based on the previously saved categories.</span></span>

        // This updates the UI on startup based on the status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="a3eab-158">La aplicación ahora almacena un conjunto de categorías en el almacenamiento local del dispositivo usado para registrarse en el Centro de notificaciones cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3eab-158">The app can now store a set of categories in the device local storage used to register with the notification hub whenever the app starts.</span></span>  <span data-ttu-id="a3eab-159">El usuario puede cambiar la selección de categorías en tiempo de ejecución y hacer clic en el método **subscribe** para actualizar el registro para el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a3eab-159">The user can change the selection of categories at runtime and click the **subscribe** method to update the registration for the device.</span></span> <span data-ttu-id="a3eab-160">A continuación, actualizará la aplicación para que envíe notificaciones de noticias de última directamente en la propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3eab-160">Next, you will update the app to send the breaking news notifications directly in the app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="a3eab-161">(Opcional) Envío de notificaciones con etiquetas</span><span class="sxs-lookup"><span data-stu-id="a3eab-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="a3eab-162">Si no tiene acceso a Visual Studio, puede pasar a la siguiente sección y enviar notificaciones desde la propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3eab-162">If you don't have access to Visual Studio, you can skip to the next section and send notifications from the app itself.</span></span> <span data-ttu-id="a3eab-163">También puede enviar la notificación de plantilla adecuada desde el [Portal de Azure clásico] mediante la pestaña de depuración para el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="a3eab-163">You can also send the proper template notification from the [Azure Classic Portal] using the debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-the-device"></a><span data-ttu-id="a3eab-164">(Opcional) Enviar notificaciones desde el dispositivo</span><span class="sxs-lookup"><span data-stu-id="a3eab-164">(optional) Send notifications from the device</span></span>
<span data-ttu-id="a3eab-165">Normalmente se pueden enviar notificaciones por un servicio de back-end pero puede enviar notificaciones de última hora directamente desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3eab-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from the app.</span></span> <span data-ttu-id="a3eab-166">Para ello se actualizará el `SendNotificationRESTAPI` método que hemos definido en el [empezar a trabajar con los centros de notificaciones] [ get-started] tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3eab-166">To do this we will update the `SendNotificationRESTAPI` method that we defined in the [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="a3eab-167">En ViewController.m actualice el método `SendNotificationRESTAPI` como sigue para que tome un parámetro para la etiqueta de categoría y que envíe una notificación de [plantilla](notification-hubs-templates-cross-platform-push-messages.md) adecuada.</span><span class="sxs-lookup"><span data-stu-id="a3eab-167">In ViewController.m update the `SendNotificationRESTAPI` method as follows so that it accepts a parameter for the category tag and sends the proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct the messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated the token to be used in the authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the template notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add the category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
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
2. <span data-ttu-id="a3eab-168">En ViewController.m actualice la acción **Enviar notificación** , tal como se muestra en el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="a3eab-168">In ViewController.m update the **Send Notification** action as shown in the code that follows.</span></span> <span data-ttu-id="a3eab-169">De esta forma, se enviarán las notificaciones mediante cada etiqueta individualmente y se enviarán a varias plataformas.</span><span class="sxs-lookup"><span data-stu-id="a3eab-169">So that it will send the notifications using each tag individually and send to multiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send the message as breaking news for each category to WNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="a3eab-170">Recompile el proyecto y asegúrese de que no haya errores de compilación.</span><span class="sxs-lookup"><span data-stu-id="a3eab-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="a3eab-171">Ejecución de la aplicación y generación de notificaciones</span><span class="sxs-lookup"><span data-stu-id="a3eab-171">Run the app and generate notifications</span></span>
1. <span data-ttu-id="a3eab-172">Presione el botón Ejecutar para compilar el proyecto e iniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3eab-172">Press the Run button to build the project and start the app.</span></span> <span data-ttu-id="a3eab-173">Seleccione algunas opciones de noticias de última hora para suscribirse y después presione el botón **Subscribe** .</span><span class="sxs-lookup"><span data-stu-id="a3eab-173">Select some breaking news options to subscribe to and then press the **Subscribe** button.</span></span> <span data-ttu-id="a3eab-174">Debería ver un cuadro de diálogo que indica que las notificaciones se han suscrito.</span><span class="sxs-lookup"><span data-stu-id="a3eab-174">You should see a dialog indicating the notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="a3eab-175">Al elegir **Subscribe**, la aplicación convierte las categorías seleccionadas en etiquetas y solicita un nuevo registro de dispositivo para las etiquetas seleccionadas desde el Centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="a3eab-175">When you choose **Subscribe**, the app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span>
2. <span data-ttu-id="a3eab-176">Escriba un mensaje que se enviará como noticias de última hora y luego presione el botón **Enviar notificación** .</span><span class="sxs-lookup"><span data-stu-id="a3eab-176">Enter a message to be sent as breaking news then press the **Send Notification** button.</span></span> <span data-ttu-id="a3eab-177">También puede ejecutar la aplicación de la consola .NET para generar notificaciones.</span><span class="sxs-lookup"><span data-stu-id="a3eab-177">Alternatively, run the .NET console app to generate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="a3eab-178">Cada dispositivo suscrito a las noticias de última hora recibirá las notificaciones de las noticias importantes que acaba de enviar.</span><span class="sxs-lookup"><span data-stu-id="a3eab-178">Each device subscribed to breaking news will receive the breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3eab-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3eab-179">Next steps</span></span>
<span data-ttu-id="a3eab-180">En este tutorial hemos aprendido cómo difundir noticias de última hora por categoría.</span><span class="sxs-lookup"><span data-stu-id="a3eab-180">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="a3eab-181">Considere la posibilidad de llevar a cabo uno de los siguientes tutoriales que destacan otros escenarios de Centros de notificaciones avanzados:</span><span class="sxs-lookup"><span data-stu-id="a3eab-181">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="a3eab-182">**[Uso de Notification Hubs para difundir noticias de última hora localizadas]**</span><span class="sxs-lookup"><span data-stu-id="a3eab-182">**[Use Notification Hubs to broadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="a3eab-183">Conozca cómo expandir la aplicación de noticias de última hora para habilitar el envío de notificaciones localizadas.</span><span class="sxs-lookup"><span data-stu-id="a3eab-183">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="a3eab-184">[Uso de Notification Hubs para difundir noticias de última hora localizadas]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="a3eab-184">[Use Notification Hubs to broadcast localized breaking news]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
<span data-ttu-id="a3eab-185">[Portal de Azure clásico]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="a3eab-185">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
