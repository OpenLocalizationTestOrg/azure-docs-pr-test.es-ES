---
title: aaaNotification concentradores adaptado importantes Tutorial de noticias para iOS
description: "Obtenga información acerca de cómo toouse centros de notificaciones de Bus de servicio de Azure toosend había adaptado importantes de las notificaciones de noticias (iOS)."
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
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a><span data-ttu-id="62286-103">Usar dispositivos de centros de notificaciones importantes toosend adaptado noticias tooiOS</span><span class="sxs-lookup"><span data-stu-id="62286-103">Use Notification Hubs toosend localized breaking news tooiOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62286-104">C# para Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="62286-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="62286-105">iOS</span><span class="sxs-lookup"><span data-stu-id="62286-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="62286-106">Información general</span><span class="sxs-lookup"><span data-stu-id="62286-106">Overview</span></span>
<span data-ttu-id="62286-107">Este tema muestra cómo hello toouse [plantillas](notification-hubs-templates-cross-platform-push-messages.md) característica de toobroadcast centros de notificaciones de Azure interrumpir las notificaciones de noticias que se han localizado según el idioma y el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="62286-107">This topic shows you how toouse hello [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="62286-108">En este tutorial debe comenzar con la aplicación de iOS de hello creado en [toosend de centros de notificaciones utilice noticias de última hora].</span><span class="sxs-lookup"><span data-stu-id="62286-108">In this tutorial you start with hello iOS app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="62286-109">Cuando haya terminado, que será capaz de tooregister para las categorías que le interesen, especifique un idioma en qué notificaciones de hello tooreceive y recibir sólo las notificaciones de inserción para las categorías de hello seleccionado en ese idioma.</span><span class="sxs-lookup"><span data-stu-id="62286-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="62286-110">Hay dos partes toothis escenario:</span><span class="sxs-lookup"><span data-stu-id="62286-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="62286-111">aplicación de iOS permite a cliente dispositivos toospecify un lenguaje y toodifferent toosubscribe importantes nuevas categorías;</span><span class="sxs-lookup"><span data-stu-id="62286-111">iOS app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="62286-112">back-end Hello emite notificaciones de hello, mediante hello **etiqueta** y **plantilla** características de los centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="62286-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62286-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="62286-113">Prerequisites</span></span>
<span data-ttu-id="62286-114">Debe haber completado hello [toosend de centros de notificaciones utilice noticias de última hora] tutorial y tenga código de hello disponible, ya que este tutorial se basa directamente en ese código.</span><span class="sxs-lookup"><span data-stu-id="62286-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="62286-115">Visual Studio 2012 o posterior es opcional.</span><span class="sxs-lookup"><span data-stu-id="62286-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="62286-116">Conceptos de plantilla</span><span class="sxs-lookup"><span data-stu-id="62286-116">Template concepts</span></span>
<span data-ttu-id="62286-117">En [toosend de centros de notificaciones utilice noticias de última hora] ha creado una aplicación que utiliza **etiquetas** toosubscribe toonotifications para categorías de noticias diferentes.</span><span class="sxs-lookup"><span data-stu-id="62286-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="62286-118">Sin embargo, muchas aplicaciones están dirigidas a varios mercados y requieren localización.</span><span class="sxs-lookup"><span data-stu-id="62286-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="62286-119">Esto significa que contenido Hola de hello las notificaciones tienen toobe localizado y entregado toohello corregir el conjunto de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="62286-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="62286-120">En este tema le mostraremos cómo hello toouse **plantilla** característica centros de notificaciones tooeasily entregar adaptado notificaciones de noticias de separación.</span><span class="sxs-lookup"><span data-stu-id="62286-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="62286-121">Nota: una manera toosend adaptado notificaciones es toocreate varias versiones de cada etiqueta.</span><span class="sxs-lookup"><span data-stu-id="62286-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="62286-122">Por ejemplo, toosupport inglés, francés y mandarín, se necesita tres etiquetas diferentes para noticias internacionales: "world_en", "world_fr" y "world_ch".</span><span class="sxs-lookup"><span data-stu-id="62286-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="62286-123">A continuación, tendríamos a toosend una versión localizada de hello world noticias tooeach estas etiquetas.</span><span class="sxs-lookup"><span data-stu-id="62286-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="62286-124">En este tema se utilizan proliferación de hello tooavoid de plantillas de etiquetas y el requisito de Hola de enviar varios mensajes.</span><span class="sxs-lookup"><span data-stu-id="62286-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="62286-125">En un nivel alto, las plantillas son una manera toospecify cómo un dispositivo específico debe recibir una notificación.</span><span class="sxs-lookup"><span data-stu-id="62286-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="62286-126">plantilla de Hello especifica el formato de carga exacto de hello consultando tooproperties que forman parte del mensaje de saludo enviado por el back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62286-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="62286-127">En nuestro caso, enviaremos un mensaje independiente de la configuración regional que contiene todos los idiomas compatibles:</span><span class="sxs-lookup"><span data-stu-id="62286-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="62286-128">A continuación, se garantizará que los dispositivos se registren con una plantilla que hace referencia la propiedad correcta toohello.</span><span class="sxs-lookup"><span data-stu-id="62286-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="62286-129">Por ejemplo, una aplicación de iOS que quiere tooregister para francés noticias registrará siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="62286-129">For instance,  an iOS app that wants tooregister for French news will register hello following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="62286-130">Las plantillas son una característica muy eficaz de la que puede obtener más información en nuestro artículo [Plantillas](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="62286-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="hello-app-user-interface"></a><span data-ttu-id="62286-131">interfaz de usuario de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="62286-131">hello app user interface</span></span>
<span data-ttu-id="62286-132">Ahora modificaremos aplicación de noticias de última hora de hello que creó en el tema de hello [toosend de centros de notificaciones utilice noticias de última hora] toosend adaptado mediante plantillas de noticias de última hora.</span><span class="sxs-lookup"><span data-stu-id="62286-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="62286-133">En su MainStoryboard_iPhone.storyboard, agregue un Control segmentados con lenguajes de hello tres que se admitirán: inglés, francés y mandarín.</span><span class="sxs-lookup"><span data-stu-id="62286-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with hello three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="62286-134">A continuación, realice tooadd seguro un IBOutlet en su ViewController.h tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="62286-134">Then make sure tooadd an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-hello-ios-app"></a><span data-ttu-id="62286-135">Aplicación de iOS de hello de creación</span><span class="sxs-lookup"><span data-stu-id="62286-135">Building hello iOS app</span></span>
1. <span data-ttu-id="62286-136">En su Notification.h agregue hello *retrieveLocale* método y modificar el almacén de Hola y suscribirse a métodos tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="62286-136">In your Notification.h add hello *retrieveLocale* method, and modify hello store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="62286-137">En su Notification.m, modifique hello *storeCategoriesAndSubscribe* método agregando el parámetro de configuración regional de Hola y almacenándolo en hello valores predeterminados del usuario:</span><span class="sxs-lookup"><span data-stu-id="62286-137">In your Notification.m, modify hello *storeCategoriesAndSubscribe* method, by adding hello locale parameter and storing it in hello user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="62286-138">A continuación, modificar hello *suscribirse* configuración regional de método tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="62286-138">Then modify hello *subscribe* method tooinclude hello locale:</span></span>
   
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
   
    <span data-ttu-id="62286-139">Tenga en cuenta cómo ahora estamos utilizando método hello *registerTemplateWithDeviceToken*, en lugar de *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="62286-139">Note how we are now using hello method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="62286-140">Cuando se registra para una plantilla tenemos plantilla json de tooprovide hello y también el nombre de plantilla de Hola (como nuestra aplicación conviene tooregister diferentes plantillas).</span><span class="sxs-lookup"><span data-stu-id="62286-140">When we register for a template we have tooprovide hello json template and also a name for hello template (as our app might want tooregister different templates).</span></span> <span data-ttu-id="62286-141">Asegúrese de tooregister seguro sus categorías como etiquetas, puesto que queremos toomake seguro tooreceive hello notifciations para las noticias.</span><span class="sxs-lookup"><span data-stu-id="62286-141">Make sure tooregister your categories as tags, as we want toomake sure tooreceive hello notifciations for those news.</span></span>
   
    <span data-ttu-id="62286-142">Agregar una configuración regional de método tooretrieve Hola de valores predeterminados del usuario hello:</span><span class="sxs-lookup"><span data-stu-id="62286-142">Add a method tooretrieve hello locale from hello user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="62286-143">Ahora que hemos modificado nuestra clase notificaciones, tenemos toomake seguro de que nuestros ViewController hace uso de hello UISegmentControl nuevo.</span><span class="sxs-lookup"><span data-stu-id="62286-143">Now that we modified our Notifications class, we have toomake sure that our ViewController makes use of hello new UISegmentControl.</span></span> <span data-ttu-id="62286-144">Agregar Hola línea siguiente en hello *viewDidLoad* método toomake seguro tooshow Hola configuración regional que está seleccionado actualmente:</span><span class="sxs-lookup"><span data-stu-id="62286-144">Add hello following line in hello *viewDidLoad* method toomake sure tooshow hello locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="62286-145">A continuación, en su *suscribirse* (método), cambiar su llamada toohello *storeCategoriesAndSubscribe* toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="62286-145">Then, in your *subscribe* method, change your call toohello *storeCategoriesAndSubscribe* toohello following:</span></span>
   
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
3. <span data-ttu-id="62286-146">Por último, tener hello tooupdate *didRegisterForRemoteNotificationsWithDeviceToken* método en su AppDelegate.m, por lo que puede actualizar correctamente el registro cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62286-146">Finally, you have tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="62286-147">Cambiar la llamada toohello *suscribirse* método de notificaciones con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="62286-147">Change your call toohello *subscribe* method of notifications with hello following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="62286-148">(Opcional) Envíe notificaciones de plantillas localizadas desde la aplicación de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="62286-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a><span data-ttu-id="62286-149">(opcional) Enviar notificaciones de plantilla localizada desde dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="62286-149">(optional) Send localized template notifications from hello device</span></span>
<span data-ttu-id="62286-150">Si no dispone de acceso tooVisual Studio o desea enviar notificaciones de la plantilla de hello adaptado directamente desde la aplicación hello en dispositivo Hola de prueba de toojust.</span><span class="sxs-lookup"><span data-stu-id="62286-150">If you don't have access tooVisual Studio, or want toojust test sending hello localized template notifications directly from hello app on hello device.</span></span>  <span data-ttu-id="62286-151">También puede simple agregar toohello de parámetros de plantilla de hello adaptado `SendNotificationRESTAPI` método definido en el tutorial anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="62286-151">You can simple add hello localized template parameters toohello `SendNotificationRESTAPI` method you defined in hello previous tutorial.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="62286-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="62286-152">Next Steps</span></span>
<span data-ttu-id="62286-153">Para obtener más información sobre el uso de plantillas, consulte:</span><span class="sxs-lookup"><span data-stu-id="62286-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="62286-154">[Notificación a los usuarios con los Centros de notificaciones de Azure: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="62286-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="62286-155">[Notificación a los usuarios con los Centros de notificaciones de Azure: Servicios móviles]</span><span class="sxs-lookup"><span data-stu-id="62286-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[toosend de centros de notificaciones utilice noticias de última hora]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notificación a los usuarios con los Centros de notificaciones de Azure: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notificación a los usuarios con los Centros de notificaciones de Azure: Servicios móviles]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
