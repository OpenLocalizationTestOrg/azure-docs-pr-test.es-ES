---
title: Tutorial de noticias importantes de localizados de los centros de aaaNotification
description: "Obtenga información acerca de cómo toouse centros de notificaciones de Azure toosend localizar las notificaciones de noticias de separación."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: c454f5a3-a06b-45ac-91c7-f91210889b25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d273a6b384df311dea7b76ca83ccd94d9a989c4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a><span data-ttu-id="4393e-103">Utilice noticias de última hora de toosend localizado de los centros de notificaciones</span><span class="sxs-lookup"><span data-stu-id="4393e-103">Use Notification Hubs toosend localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4393e-104">C# para Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="4393e-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="4393e-105">iOS</span><span class="sxs-lookup"><span data-stu-id="4393e-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="4393e-106">Información general</span><span class="sxs-lookup"><span data-stu-id="4393e-106">Overview</span></span>
<span data-ttu-id="4393e-107">Este tema muestra cómo hello toouse **plantilla** característica de toobroadcast centros de notificaciones de Azure interrumpir las notificaciones de noticias que se han localizado según el idioma y el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4393e-107">This topic shows you how toouse hello **template** feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="4393e-108">En este tutorial debe comenzar con la aplicación de tienda Windows hello creado en [toosend de centros de notificaciones utilice noticias de última hora].</span><span class="sxs-lookup"><span data-stu-id="4393e-108">In this tutorial you start with hello Windows Store app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="4393e-109">Cuando haya terminado, que será capaz de tooregister para las categorías que le interesen, especifique un idioma en qué notificaciones de hello tooreceive y recibir sólo las notificaciones de inserción para las categorías de hello seleccionado en ese idioma.</span><span class="sxs-lookup"><span data-stu-id="4393e-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="4393e-110">Hay dos partes toothis escenario:</span><span class="sxs-lookup"><span data-stu-id="4393e-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="4393e-111">aplicación de la tienda de Windows Hello permite a cliente dispositivos toospecify un lenguaje y toodifferent toosubscribe importantes nuevas categorías;</span><span class="sxs-lookup"><span data-stu-id="4393e-111">hello Windows Store app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="4393e-112">back-end Hello emite notificaciones de hello, mediante hello **etiqueta** y **plantilla** características de los centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="4393e-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4393e-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4393e-113">Prerequisites</span></span>
<span data-ttu-id="4393e-114">Debe haber completado hello [toosend de centros de notificaciones utilice noticias de última hora] tutorial y tenga código de hello disponible, ya que este tutorial se basa directamente en ese código.</span><span class="sxs-lookup"><span data-stu-id="4393e-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="4393e-115">También necesita Visual Studio 2012 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4393e-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="4393e-116">Conceptos de plantilla</span><span class="sxs-lookup"><span data-stu-id="4393e-116">Template concepts</span></span>
<span data-ttu-id="4393e-117">En [toosend de centros de notificaciones utilice noticias de última hora] ha creado una aplicación que utiliza **etiquetas** toosubscribe toonotifications para categorías de noticias diferentes.</span><span class="sxs-lookup"><span data-stu-id="4393e-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="4393e-118">Sin embargo, muchas aplicaciones están dirigidas a varios mercados y requieren localización.</span><span class="sxs-lookup"><span data-stu-id="4393e-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="4393e-119">Esto significa que contenido Hola de hello las notificaciones tienen toobe localizado y entregado toohello corregir el conjunto de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4393e-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="4393e-120">En este tema le mostraremos cómo hello toouse **plantilla** característica centros de notificaciones tooeasily entregar adaptado notificaciones de noticias de separación.</span><span class="sxs-lookup"><span data-stu-id="4393e-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="4393e-121">Nota: una manera toosend adaptado notificaciones es toocreate varias versiones de cada etiqueta.</span><span class="sxs-lookup"><span data-stu-id="4393e-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="4393e-122">Por ejemplo, toosupport inglés, francés y mandarín, se necesita tres etiquetas diferentes para noticias internacionales: "world_en", "world_fr" y "world_ch".</span><span class="sxs-lookup"><span data-stu-id="4393e-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="4393e-123">A continuación, tendríamos a toosend una versión localizada de hello world noticias tooeach estas etiquetas.</span><span class="sxs-lookup"><span data-stu-id="4393e-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="4393e-124">En este tema se utilizan proliferación de hello tooavoid de plantillas de etiquetas y el requisito de Hola de enviar varios mensajes.</span><span class="sxs-lookup"><span data-stu-id="4393e-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="4393e-125">En un nivel alto, las plantillas son una manera toospecify cómo un dispositivo específico debe recibir una notificación.</span><span class="sxs-lookup"><span data-stu-id="4393e-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="4393e-126">plantilla de Hello especifica el formato de carga exacto de hello consultando tooproperties que forman parte del mensaje de saludo enviado por el back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4393e-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="4393e-127">En nuestro caso, enviaremos un mensaje independiente de la configuración regional que contiene todos los idiomas compatibles:</span><span class="sxs-lookup"><span data-stu-id="4393e-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="4393e-128">A continuación, se garantizará que los dispositivos se registren con una plantilla que hace referencia la propiedad correcta toohello.</span><span class="sxs-lookup"><span data-stu-id="4393e-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="4393e-129">Por ejemplo, una aplicación de la tienda de Windows que desea tooreceive un mensaje de notificación del sistema simple registrará para hello sigue template con todas las etiquetas correspondientes:</span><span class="sxs-lookup"><span data-stu-id="4393e-129">For instance, a Windows Store app that wants tooreceive a simple toast message will register for hello following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="4393e-130">Las plantillas son una característica muy eficaz de la que puede obtener más información en nuestro artículo [Plantillas](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="4393e-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="hello-app-user-interface"></a><span data-ttu-id="4393e-131">interfaz de usuario de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="4393e-131">hello app user interface</span></span>
<span data-ttu-id="4393e-132">Ahora modificaremos aplicación de noticias de última hora de hello que creó en el tema de hello [toosend de centros de notificaciones utilice noticias de última hora] toosend adaptado mediante plantillas de noticias de última hora.</span><span class="sxs-lookup"><span data-stu-id="4393e-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="4393e-133">En la aplicación de la Tienda Windows:</span><span class="sxs-lookup"><span data-stu-id="4393e-133">In your Windows Store app:</span></span>

<span data-ttu-id="4393e-134">Cambiar el tooinclude MainPage.xaml un cuadro combinado de configuración regional:</span><span class="sxs-lookup"><span data-stu-id="4393e-134">Change your MainPage.xaml tooinclude a locale combobox:</span></span>

    <Grid Margin="120, 58, 120, 80"  
            Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top"/>
        <ComboBox Name="Locale" HorizontalAlignment="Left" VerticalAlignment="Center" Width="200" Grid.Row="1" Grid.Column="0">
            <x:String>English</x:String>
            <x:String>French</x:String>
            <x:String>Mandarin</x:String>
        </ComboBox>
        <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="2" Grid.Column="0"/>
        <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="3" Grid.Column="0"/>
        <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="4" Grid.Column="0"/>
        <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="2" Grid.Column="1"/>
        <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="3" Grid.Column="1"/>
        <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="4" Grid.Column="1"/>
        <Button Content="Subscribe" HorizontalAlignment="Center" Grid.Row="5" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
    </Grid>

## <a name="building-hello-windows-store-client-app"></a><span data-ttu-id="4393e-135">Compilar la aplicación de cliente de la tienda Windows hello</span><span class="sxs-lookup"><span data-stu-id="4393e-135">Building hello Windows Store client app</span></span>
1. <span data-ttu-id="4393e-136">En la clase de notificaciones, agregue un tooyour del parámetro de configuración regional *StoreCategoriesAndSubscribe* y *SubscribeToCateories* métodos.</span><span class="sxs-lookup"><span data-stu-id="4393e-136">In your Notifications class, add a locale parameter tooyour  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
        public async Task<Registration> StoreCategoriesAndSubscribe(string locale, IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            ApplicationData.Current.LocalSettings.Values["locale"] = locale;
            return await SubscribeToCategories(categories);
        }
   
        public async Task<Registration> SubscribeToCategories(string locale, IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration. This makes supporting notifications across other platforms much easier.
            // Using hello localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="4393e-137">Tenga en cuenta que en lugar de Hola que realiza la llamada *RegisterNativeAsync* método llamamos *RegisterTemplateAsync*: se está registrando un formato de notificación específico en qué Hola plantilla depende de configuración regional de Hola.</span><span class="sxs-lookup"><span data-stu-id="4393e-137">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which hello template depends on hello locale.</span></span> <span data-ttu-id="4393e-138">También proporcionamos un nombre para la plantilla de hello ("localizedWNSTemplateExample"), dado que nos convenga tooregister más de una plantilla (por ejemplo uno para recibir notificaciones del sistema) y otro para iconos y necesitamos tooname en orden toobe puede tooupdate o eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="4393e-138">We also provide a name for hello template ("localizedWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="4393e-139">Tenga en cuenta que si un dispositivo se registra varias plantillas con hello misma etiqueta, un mensaje entrante de destino que se generará etiqueta varias notificaciones de entreguen dispositivo toohello (uno por cada plantilla).</span><span class="sxs-lookup"><span data-stu-id="4393e-139">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="4393e-140">Este comportamiento es útil cuando hello mismo mensaje lógico tiene tooresult en varias notificaciones visuales, por ejemplo que muestra un distintivo y una notificación del sistema en una aplicación de almacenamiento de Windows.</span><span class="sxs-lookup"><span data-stu-id="4393e-140">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="4393e-141">Agregue Hola siguiendo el método tooretrieve Hola configuración regional almacenado:</span><span class="sxs-lookup"><span data-stu-id="4393e-141">Add hello following method tooretrieve hello stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="4393e-142">En su MainPage.xaml.cs, el botón Actualizar controlador de clic recuperando el valor actual de Hola de cuadro combinado de configuración regional de Hola y proporcionar toohello call toohello notificaciones (clase), tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="4393e-142">In your MainPage.xaml.cs, update your button click handler by retrieving hello current value of hello Locale combo box and providing it toohello call toohello Notifications class, as shown:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var locale = (string)Locale.SelectedItem;
   
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(locale,
                 categories);
   
            var dialog = new MessageDialog("Locale: " + locale + " Subscribed to: " + 
                string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
4. <span data-ttu-id="4393e-143">Por último, en el archivo App.xaml.cs, asegúrese que tooupdate su `InitNotificationsAsync` método tooretrieve Hola configuración regional y usarla cuando se suscriba:</span><span class="sxs-lookup"><span data-stu-id="4393e-143">Finally, in your App.xaml.cs file, make sure tooupdate your `InitNotificationsAsync` method tooretrieve hello locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="4393e-144">Envío de notificaciones localizadas desde su backend</span><span class="sxs-lookup"><span data-stu-id="4393e-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[hello app user interface]: #ui
[Building hello Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[toosend de centros de notificaciones utilice noticias de última hora]: /manage/services/notification-hubs/breaking-news-dotnet

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
