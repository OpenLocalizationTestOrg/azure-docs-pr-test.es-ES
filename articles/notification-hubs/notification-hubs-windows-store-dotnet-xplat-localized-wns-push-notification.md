---
title: "Tutorial de últimas noticias localizadas sobre los Centros de notificaciones"
description: "Obtenga información sobre cómo usar Centros de notificaciones de Azure para enviar notificaciones de noticias de última hora localizadas."
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
ms.openlocfilehash: e864e832b4c50644bf4062dee29d34ff9fe2774e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news"></a><span data-ttu-id="0fd90-103">Uso de los Centros de notificaciones para enviar noticias de última hora localizadas</span><span class="sxs-lookup"><span data-stu-id="0fd90-103">Use Notification Hubs to send localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0fd90-104">C# para Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="0fd90-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="0fd90-105">iOS</span><span class="sxs-lookup"><span data-stu-id="0fd90-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="0fd90-106">Información general</span><span class="sxs-lookup"><span data-stu-id="0fd90-106">Overview</span></span>
<span data-ttu-id="0fd90-107">Este tema muestra cómo usar la característica de **plantilla** de los Centros de notificaciones de Azure para difundir notificaciones de noticias de última hora localizadas por lenguaje y dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0fd90-107">This topic shows you how to use the **template** feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="0fd90-108">En este tutorial comenzará con la aplicación de la Tienda Windows que se creó en el tutorial [Uso de los Centros de notificaciones para enviar noticias de última hora].</span><span class="sxs-lookup"><span data-stu-id="0fd90-108">In this tutorial you start with the Windows Store app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="0fd90-109">Una vez que lo haya completado, podrá registrarse en las categorías que le interesan, especificar un idioma para recibir las notificaciones y recibir solo notificaciones de inserción para las categorías seleccionadas en dicho idioma.</span><span class="sxs-lookup"><span data-stu-id="0fd90-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="0fd90-110">Este escenario tiene dos partes:</span><span class="sxs-lookup"><span data-stu-id="0fd90-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="0fd90-111">La aplicación de la Tienda Windows permite que los dispositivos cliente especifiquen un idioma y se suscriban a distintas categorías de noticias de última hora.</span><span class="sxs-lookup"><span data-stu-id="0fd90-111">the Windows Store app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="0fd90-112">el back-end difunde las notificaciones, mediante las características de **etiqueta** y **plantilla** de los Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="0fd90-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fd90-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0fd90-113">Prerequisites</span></span>
<span data-ttu-id="0fd90-114">Debe haber completado el tutorial [Uso de los Centros de notificaciones para enviar noticias de última hora] y debe tener disponible el código, porque este tutorial se basa directamente en ese código.</span><span class="sxs-lookup"><span data-stu-id="0fd90-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="0fd90-115">También necesita Visual Studio 2012 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0fd90-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="0fd90-116">Conceptos de plantilla</span><span class="sxs-lookup"><span data-stu-id="0fd90-116">Template concepts</span></span>
<span data-ttu-id="0fd90-117">En el tutorial [Uso de los Centros de notificaciones para enviar noticias de última hora] creó una aplicación que utilizó **etiquetas** para suscribirse a notificaciones para distintas categorías de noticias.</span><span class="sxs-lookup"><span data-stu-id="0fd90-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="0fd90-118">Sin embargo, muchas aplicaciones están dirigidas a varios mercados y requieren localización.</span><span class="sxs-lookup"><span data-stu-id="0fd90-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="0fd90-119">Esto significa que el contenido de las notificaciones mismas se debe localizar y entregar al conjunto de dispositivos correcto.</span><span class="sxs-lookup"><span data-stu-id="0fd90-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="0fd90-120">En este tema podremos mostrar cómo usar la característica de **plantilla** de Notification Hubs para entregar fácilmente notificaciones de noticias de última hora localizadas.</span><span class="sxs-lookup"><span data-stu-id="0fd90-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="0fd90-121">Nota: una forma de enviar notificaciones localizadas es crear varias versiones de cada etiqueta.</span><span class="sxs-lookup"><span data-stu-id="0fd90-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="0fd90-122">Por ejemplo, para admitir inglés, francés y chino mandarín, necesitaríamos tres etiquetas distintas para noticias mundiales: "world_en", "world_fr" y "world_ch".</span><span class="sxs-lookup"><span data-stu-id="0fd90-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="0fd90-123">Luego tendríamos que enviar una versión localizada de las noticias mundiales a cada una de estas etiquetas.</span><span class="sxs-lookup"><span data-stu-id="0fd90-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="0fd90-124">En este tema usamos plantillas para evitar la proliferación de etiquetas y el requisito de enviar varios mensajes.</span><span class="sxs-lookup"><span data-stu-id="0fd90-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="0fd90-125">A un alto nivel, las plantillas son una forma de especificar la manera en que un dispositivo específico debe recibir una notificación.</span><span class="sxs-lookup"><span data-stu-id="0fd90-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="0fd90-126">La plantilla especifica el formato de carga exacto haciendo referencia a las propiedades que forman parte del mensaje enviado por el back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0fd90-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="0fd90-127">En nuestro caso, enviaremos un mensaje independiente de la configuración regional que contiene todos los idiomas compatibles:</span><span class="sxs-lookup"><span data-stu-id="0fd90-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="0fd90-128">Esto garantizará que los dispositivos se registren con una plantilla que hace referencia a la propiedad correcta.</span><span class="sxs-lookup"><span data-stu-id="0fd90-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="0fd90-129">Por ejemplo, una aplicación de la Tienda Windows que quiere recibir un simple mensaje del sistema se registrará en la plantilla siguiente con las etiquetas correspondientes:</span><span class="sxs-lookup"><span data-stu-id="0fd90-129">For instance, a Windows Store app that wants to receive a simple toast message will register for the following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="0fd90-130">Las plantillas son una característica muy eficaz de la que puede obtener más información en nuestro artículo [Plantillas](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="0fd90-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="the-app-user-interface"></a><span data-ttu-id="0fd90-131">Interfaz de usuario de la aplicación</span><span class="sxs-lookup"><span data-stu-id="0fd90-131">The app user interface</span></span>
<span data-ttu-id="0fd90-132">Ahora modificaremos la aplicación de noticias de última hora que creó en el tema [Uso de los Centros de notificaciones para enviar noticias de última hora] a fin de enviar noticias de este tipo localizadas con la utilización de las plantillas.</span><span class="sxs-lookup"><span data-stu-id="0fd90-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="0fd90-133">En la aplicación de la Tienda Windows:</span><span class="sxs-lookup"><span data-stu-id="0fd90-133">In your Windows Store app:</span></span>

<span data-ttu-id="0fd90-134">Modifique el archivo MainPage.xaml para que incluya un cuadro combinado de configuración regional:</span><span class="sxs-lookup"><span data-stu-id="0fd90-134">Change your MainPage.xaml to include a locale combobox:</span></span>

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

## <a name="building-the-windows-store-client-app"></a><span data-ttu-id="0fd90-135">Compilación de la aplicación cliente de la Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="0fd90-135">Building the Windows Store client app</span></span>
1. <span data-ttu-id="0fd90-136">En la clase Notifications, agregue un parámetro de configuración regional a los métodos *StoreCategoriesAndSubscribe* y *SubscribeToCategories*.</span><span class="sxs-lookup"><span data-stu-id="0fd90-136">In your Notifications class, add a locale parameter to your  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
            // Using the localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="0fd90-137">Tenga en cuenta que, en lugar de llamar al método *RegisterNativeAsync*, llamaremos a *RegisterTemplateAsync*: estamos registrando un formato de notificación específico en el que la plantilla depende de la configuración regional.</span><span class="sxs-lookup"><span data-stu-id="0fd90-137">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which the template depends on the locale.</span></span> <span data-ttu-id="0fd90-138">Asimismo, proporcionamos un nombre para la plantilla ("localizedWNSTemplateExample"), ya que es posible que queramos registrar más de una (por ejemplo, una para las notificaciones del sistema y otra de iconos) y es necesario asignarles un nombre para poder actualizarlas o eliminarlas.</span><span class="sxs-lookup"><span data-stu-id="0fd90-138">We also provide a name for the template ("localizedWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="0fd90-139">Tenga en cuenta que, si un dispositivo registra varias plantillas con la misma etiqueta, el envío de un mensaje destinado a dicha etiqueta dará como resultado la entrega de varias notificaciones al dispositivo (una para cada plantilla).</span><span class="sxs-lookup"><span data-stu-id="0fd90-139">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="0fd90-140">Este comportamiento resulta útil cuando un mismo mensaje lógico debe dar como resultado varias notificaciones visuales que muestren, por ejemplo, tanto un distintivo como una notificación del sistema en una aplicación de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="0fd90-140">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="0fd90-141">Agregue el método siguiente para recuperar la configuración regional almacenada:</span><span class="sxs-lookup"><span data-stu-id="0fd90-141">Add the following method to retrieve the stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="0fd90-142">En el archivo MainPage.xaml.cs, actualice el controlador de clics de botón; para ello, recupere el valor actual del cuadro combinado de configuración regional y ofrézcalo a la llamada a la clase Notifications, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="0fd90-142">In your MainPage.xaml.cs, update your button click handler by retrieving the current value of the Locale combo box and providing it to the call to the Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="0fd90-143">Por último, en su archivo App.xaml.cs, asegúrese de actualizar su método `InitNotificationsAsync` para recuperar la configuración regional y usarla al suscribirse:</span><span class="sxs-lookup"><span data-stu-id="0fd90-143">Finally, in your App.xaml.cs file, make sure to update your `InitNotificationsAsync` method to retrieve the locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="0fd90-144">Envío de notificaciones localizadas desde su backend</span><span class="sxs-lookup"><span data-stu-id="0fd90-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[The app user interface]: #ui
[Building the Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
<span data-ttu-id="0fd90-145">[Uso de los Centros de notificaciones para enviar noticias de última hora]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="0fd90-145">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
