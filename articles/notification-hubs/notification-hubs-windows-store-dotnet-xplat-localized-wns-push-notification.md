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
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a>Utilice noticias de última hora de toosend localizado de los centros de notificaciones
> [!div class="op_single_selector"]
> * [C# para Tienda Windows](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Información general
Este tema muestra cómo hello toouse **plantilla** característica de toobroadcast centros de notificaciones de Azure interrumpir las notificaciones de noticias que se han localizado según el idioma y el dispositivo. En este tutorial debe comenzar con la aplicación de tienda Windows hello creado en [toosend de centros de notificaciones utilice noticias de última hora]. Cuando haya terminado, que será capaz de tooregister para las categorías que le interesen, especifique un idioma en qué notificaciones de hello tooreceive y recibir sólo las notificaciones de inserción para las categorías de hello seleccionado en ese idioma.

Hay dos partes toothis escenario:

* aplicación de la tienda de Windows Hello permite a cliente dispositivos toospecify un lenguaje y toodifferent toosubscribe importantes nuevas categorías;
* back-end Hello emite notificaciones de hello, mediante hello **etiqueta** y **plantilla** características de los centros de notificaciones de Azure.

## <a name="prerequisites"></a>Requisitos previos
Debe haber completado hello [toosend de centros de notificaciones utilice noticias de última hora] tutorial y tenga código de hello disponible, ya que este tutorial se basa directamente en ese código.

También necesita Visual Studio 2012 o posterior.

## <a name="template-concepts"></a>Conceptos de plantilla
En [toosend de centros de notificaciones utilice noticias de última hora] ha creado una aplicación que utiliza **etiquetas** toosubscribe toonotifications para categorías de noticias diferentes.
Sin embargo, muchas aplicaciones están dirigidas a varios mercados y requieren localización. Esto significa que contenido Hola de hello las notificaciones tienen toobe localizado y entregado toohello corregir el conjunto de dispositivos.
En este tema le mostraremos cómo hello toouse **plantilla** característica centros de notificaciones tooeasily entregar adaptado notificaciones de noticias de separación.

Nota: una manera toosend adaptado notificaciones es toocreate varias versiones de cada etiqueta. Por ejemplo, toosupport inglés, francés y mandarín, se necesita tres etiquetas diferentes para noticias internacionales: "world_en", "world_fr" y "world_ch". A continuación, tendríamos a toosend una versión localizada de hello world noticias tooeach estas etiquetas. En este tema se utilizan proliferación de hello tooavoid de plantillas de etiquetas y el requisito de Hola de enviar varios mensajes.

En un nivel alto, las plantillas son una manera toospecify cómo un dispositivo específico debe recibir una notificación. plantilla de Hello especifica el formato de carga exacto de hello consultando tooproperties que forman parte del mensaje de saludo enviado por el back-end de la aplicación. En nuestro caso, enviaremos un mensaje independiente de la configuración regional que contiene todos los idiomas compatibles:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

A continuación, se garantizará que los dispositivos se registren con una plantilla que hace referencia la propiedad correcta toohello. Por ejemplo, una aplicación de la tienda de Windows que desea tooreceive un mensaje de notificación del sistema simple registrará para hello sigue template con todas las etiquetas correspondientes:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



Las plantillas son una característica muy eficaz de la que puede obtener más información en nuestro artículo [Plantillas](notification-hubs-templates-cross-platform-push-messages.md) . 

## <a name="hello-app-user-interface"></a>interfaz de usuario de aplicación Hola
Ahora modificaremos aplicación de noticias de última hora de hello que creó en el tema de hello [toosend de centros de notificaciones utilice noticias de última hora] toosend adaptado mediante plantillas de noticias de última hora.

En la aplicación de la Tienda Windows:

Cambiar el tooinclude MainPage.xaml un cuadro combinado de configuración regional:

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

## <a name="building-hello-windows-store-client-app"></a>Compilar la aplicación de cliente de la tienda Windows hello
1. En la clase de notificaciones, agregue un tooyour del parámetro de configuración regional *StoreCategoriesAndSubscribe* y *SubscribeToCateories* métodos.
   
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
   
    Tenga en cuenta que en lugar de Hola que realiza la llamada *RegisterNativeAsync* método llamamos *RegisterTemplateAsync*: se está registrando un formato de notificación específico en qué Hola plantilla depende de configuración regional de Hola. También proporcionamos un nombre para la plantilla de hello ("localizedWNSTemplateExample"), dado que nos convenga tooregister más de una plantilla (por ejemplo uno para recibir notificaciones del sistema) y otro para iconos y necesitamos tooname en orden toobe puede tooupdate o eliminarlos.
   
    Tenga en cuenta que si un dispositivo se registra varias plantillas con hello misma etiqueta, un mensaje entrante de destino que se generará etiqueta varias notificaciones de entreguen dispositivo toohello (uno por cada plantilla). Este comportamiento es útil cuando hello mismo mensaje lógico tiene tooresult en varias notificaciones visuales, por ejemplo que muestra un distintivo y una notificación del sistema en una aplicación de almacenamiento de Windows.
2. Agregue Hola siguiendo el método tooretrieve Hola configuración regional almacenado:
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. En su MainPage.xaml.cs, el botón Actualizar controlador de clic recuperando el valor actual de Hola de cuadro combinado de configuración regional de Hola y proporcionar toohello call toohello notificaciones (clase), tal como se muestra:
   
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
4. Por último, en el archivo App.xaml.cs, asegúrese que tooupdate su `InitNotificationsAsync` método tooretrieve Hola configuración regional y usarla cuando se suscriba:
   
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

## <a name="send-localized-notifications-from-your-back-end"></a>Envío de notificaciones localizadas desde su backend
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
