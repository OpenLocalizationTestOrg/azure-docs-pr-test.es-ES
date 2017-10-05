---
title: "Tutorial de últimas noticias localizadas sobre los Centros de notificaciones para iOS"
description: "Obtenga información acerca de los Centros de notificaciones del Bus de servicio de Azure para enviar notificaciones de noticias de última hora localizadas (iOS)."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: fd2b7d9dfd4f432bbcbaa3ed76f8bec0b9677e17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news-to-ios-devices"></a><span data-ttu-id="ba410-103">Uso de los Centros de notificaciones para enviar noticias de última hora localizadas a dispositivos iOS</span><span class="sxs-lookup"><span data-stu-id="ba410-103">Use Notification Hubs to send localized breaking news to iOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba410-104">C# para Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="ba410-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="ba410-105">iOS</span><span class="sxs-lookup"><span data-stu-id="ba410-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ba410-106">Información general</span><span class="sxs-lookup"><span data-stu-id="ba410-106">Overview</span></span>
<span data-ttu-id="ba410-107">En este tema se muestra cómo usar la característica de [plantillas](notification-hubs-templates-cross-platform-push-messages.md) de los Centros de notificaciones de Azure para difundir notificaciones de noticias de última hora localizadas por lenguaje y dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ba410-107">This topic shows you how to use the [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="ba410-108">En este tutorial comenzará con la aplicación de iOS que se creó en [Uso de Centros de notificaciones para enviar noticias de última hora].</span><span class="sxs-lookup"><span data-stu-id="ba410-108">In this tutorial you start with the iOS app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="ba410-109">Una vez que lo haya completado, podrá registrarse en las categorías que le interesan, especificar un idioma para recibir las notificaciones y recibir solo notificaciones de inserción para las categorías seleccionadas en dicho idioma.</span><span class="sxs-lookup"><span data-stu-id="ba410-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="ba410-110">Este escenario tiene dos partes:</span><span class="sxs-lookup"><span data-stu-id="ba410-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="ba410-111">La aplicación iOS permite que los dispositivos cliente especifiquen un idioma y que se suscriban a distintas categorías de noticias de última hora;</span><span class="sxs-lookup"><span data-stu-id="ba410-111">iOS app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="ba410-112">El back-end difunde las notificaciones mediante las características **etiqueta** y **plantilla** de Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="ba410-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba410-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ba410-113">Prerequisites</span></span>
<span data-ttu-id="ba410-114">Debe haber completado el tutorial [Uso de Centros de notificaciones para enviar noticias de última hora] y debe tener disponible el código, porque este tutorial se basa directamente en ese código.</span><span class="sxs-lookup"><span data-stu-id="ba410-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="ba410-115">Visual Studio 2012 o posterior es opcional.</span><span class="sxs-lookup"><span data-stu-id="ba410-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="ba410-116">Conceptos de plantilla</span><span class="sxs-lookup"><span data-stu-id="ba410-116">Template concepts</span></span>
<span data-ttu-id="ba410-117">En el tutorial [Uso de Centros de notificaciones para enviar noticias de última hora] creó una aplicación que utilizó **etiquetas** para suscribirse a notificaciones para distintas categorías de noticias.</span><span class="sxs-lookup"><span data-stu-id="ba410-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="ba410-118">Sin embargo, muchas aplicaciones están dirigidas a varios mercados y requieren localización.</span><span class="sxs-lookup"><span data-stu-id="ba410-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="ba410-119">Esto significa que el contenido de las notificaciones mismas se debe localizar y entregar al conjunto de dispositivos correcto.</span><span class="sxs-lookup"><span data-stu-id="ba410-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="ba410-120">En este tema podremos mostrar cómo usar la característica de **plantilla** de Notification Hubs para entregar fácilmente notificaciones de noticias de última hora localizadas.</span><span class="sxs-lookup"><span data-stu-id="ba410-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="ba410-121">Nota: una forma de enviar notificaciones localizadas es crear varias versiones de cada etiqueta.</span><span class="sxs-lookup"><span data-stu-id="ba410-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="ba410-122">Por ejemplo, para admitir inglés, francés y chino mandarín, necesitaríamos tres etiquetas distintas para noticias mundiales: "world_en", "world_fr" y "world_ch".</span><span class="sxs-lookup"><span data-stu-id="ba410-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="ba410-123">Luego tendríamos que enviar una versión localizada de las noticias mundiales a cada una de estas etiquetas.</span><span class="sxs-lookup"><span data-stu-id="ba410-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="ba410-124">En este tema usamos plantillas para evitar la proliferación de etiquetas y el requisito de enviar varios mensajes.</span><span class="sxs-lookup"><span data-stu-id="ba410-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="ba410-125">A un alto nivel, las plantillas son una forma de especificar la manera en que un dispositivo específico debe recibir una notificación.</span><span class="sxs-lookup"><span data-stu-id="ba410-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="ba410-126">La plantilla especifica el formato de carga exacto haciendo referencia a las propiedades que forman parte del mensaje enviado por el back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ba410-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="ba410-127">En nuestro caso, enviaremos un mensaje independiente de la configuración regional que contiene todos los idiomas compatibles:</span><span class="sxs-lookup"><span data-stu-id="ba410-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="ba410-128">Esto garantizará que los dispositivos se registren con una plantilla que hace referencia a la propiedad correcta.</span><span class="sxs-lookup"><span data-stu-id="ba410-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="ba410-129">Por ejemplo, una aplicación iOS que quiera registrarse para noticias en francés se registrará de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="ba410-129">For instance,  an iOS app that wants to register for French news will register the following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="ba410-130">Las plantillas son una característica muy eficaz de la que puede obtener más información en nuestro artículo [Plantillas](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="ba410-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="the-app-user-interface"></a><span data-ttu-id="ba410-131">Interfaz de usuario de la aplicación</span><span class="sxs-lookup"><span data-stu-id="ba410-131">The app user interface</span></span>
<span data-ttu-id="ba410-132">Ahora modificaremos la aplicación de noticias de última hora que creó en el tema [Uso de Centros de notificaciones para enviar noticias de última hora] a fin de enviar noticias de este tipo localizadas con la utilización de las plantillas.</span><span class="sxs-lookup"><span data-stu-id="ba410-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="ba410-133">En MainStoryboard_iPhone.storyboard, agregue un control segmentado con los tres idiomas compatibles: inglés, francés y chino mandarín.</span><span class="sxs-lookup"><span data-stu-id="ba410-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with the three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="ba410-134">A continuación, asegúrese de agregar un IBOutlet en ViewController.h tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="ba410-134">Then make sure to add an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-the-ios-app"></a><span data-ttu-id="ba410-135">Creación de la aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="ba410-135">Building the iOS app</span></span>
1. <span data-ttu-id="ba410-136">En Notification.h, agregue el método *retrieveLocale* , modifique el almacén y suscríbase a métodos tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="ba410-136">In your Notification.h add the *retrieveLocale* method, and modify the store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="ba410-137">En Notification.m, modifique el método *storeCategoriesAndSubscribe* agregando el parámetro de configuración regional y almacenándolo en los valores predeterminados del usuario:</span><span class="sxs-lookup"><span data-stu-id="ba410-137">In your Notification.m, modify the *storeCategoriesAndSubscribe* method, by adding the locale parameter and storing it in the user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="ba410-138">Luego modifique el método *subscribe* para incluir la configuración regional:</span><span class="sxs-lookup"><span data-stu-id="ba410-138">Then modify the *subscribe* method to include the locale:</span></span>
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    <span data-ttu-id="ba410-139">Observe cómo usamos ahora el método *registerTemplateWithDeviceToken*, en lugar de *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="ba410-139">Note how we are now using the method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="ba410-140">Cuando nos registramos para obtener una plantilla, tenemos que proporcionar la plantilla json y también ponerle un nombre (dado que nuestra aplicación puede querer registrar distintas plantillas).</span><span class="sxs-lookup"><span data-stu-id="ba410-140">When we register for a template we have to provide the json template and also a name for the template (as our app might want to register different templates).</span></span> <span data-ttu-id="ba410-141">Asegúrese de registrar sus categorías como etiquetas, debido a que queremos asegurarnos de recibir las notificaciones para dichas noticias.</span><span class="sxs-lookup"><span data-stu-id="ba410-141">Make sure to register your categories as tags, as we want to make sure to receive the notifciations for those news.</span></span>
   
    <span data-ttu-id="ba410-142">Agregue un método para recuperar la configuración regional a partir de los ajustes predeterminados del usuario:</span><span class="sxs-lookup"><span data-stu-id="ba410-142">Add a method to retrieve the locale from the user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="ba410-143">Ahora que hemos modificado nuestra clase de notificaciones, debemos asegurarnos de que nuestro ViewController utilice el nuevo UISegmentControl.</span><span class="sxs-lookup"><span data-stu-id="ba410-143">Now that we modified our Notifications class, we have to make sure that our ViewController makes use of the new UISegmentControl.</span></span> <span data-ttu-id="ba410-144">Agregue la siguiente línea en el método *viewDidLoad* para asegurarse de mostrar la configuración regional actualmente seleccionada:</span><span class="sxs-lookup"><span data-stu-id="ba410-144">Add the following line in the *viewDidLoad* method to make sure to show the locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="ba410-145">A continuación, en el método *subscribe*, cambie la llamada a *storeCategoriesAndSubscribe* por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ba410-145">Then, in your *subscribe* method, change your call to the *storeCategoriesAndSubscribe* to the following:</span></span>
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. <span data-ttu-id="ba410-146">Finalmente, debe actualizar el método *didRegisterForRemoteNotificationsWithDeviceToken* en AppDelegate.m, para que pueda actualizar correctamente el registro cuando se inicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ba410-146">Finally, you have to update the *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="ba410-147">Cambie la llamada al método *subscribe* de notificaciones con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ba410-147">Change your call to the *subscribe* method of notifications with the following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="ba410-148">(Opcional) Envíe notificaciones de plantillas localizadas desde la aplicación de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="ba410-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-the-device"></a><span data-ttu-id="ba410-149">(Opcional) Enviar notificaciones de plantillas localizadas desde el dispositivo</span><span class="sxs-lookup"><span data-stu-id="ba410-149">(optional) Send localized template notifications from the device</span></span>
<span data-ttu-id="ba410-150">Si no tiene acceso a Visual Studio, o simplemente quiere probar el envío de las notificaciones de plantilla localizadas directamente desde la aplicación del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ba410-150">If you don't have access to Visual Studio, or want to just test sending the localized template notifications directly from the app on the device.</span></span>  <span data-ttu-id="ba410-151">Simplemente puede agregar los parámetros de plantilla localizada al método `SendNotificationRESTAPI` que ha definido en el tutorial anterior.</span><span class="sxs-lookup"><span data-stu-id="ba410-151">You can simple add the localized template parameters to the `SendNotificationRESTAPI` method you defined in the previous tutorial.</span></span>

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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

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




## <a name="next-steps"></a><span data-ttu-id="ba410-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba410-152">Next Steps</span></span>
<span data-ttu-id="ba410-153">Para obtener más información sobre el uso de plantillas, consulte:</span><span class="sxs-lookup"><span data-stu-id="ba410-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="ba410-154">[Notificación a los usuarios con los Centros de notificaciones de Azure: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="ba410-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="ba410-155">[Notificación a los usuarios con los Centros de notificaciones de Azure: Servicios móviles]</span><span class="sxs-lookup"><span data-stu-id="ba410-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="ba410-156">[Uso de Centros de notificaciones para enviar noticias de última hora]: /manage/services/notification-hubs/breaking-news-ios</span><span class="sxs-lookup"><span data-stu-id="ba410-156">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-ios</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
<span data-ttu-id="ba410-157">[Notificación a los usuarios con los Centros de notificaciones de Azure: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="ba410-157">[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="ba410-158">[Notificación a los usuarios con los Centros de notificaciones de Azure: Servicios móviles]: /manage/services/notification-hubs/notify-users</span><span class="sxs-lookup"><span data-stu-id="ba410-158">[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users</span></span>
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
