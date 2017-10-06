---
title: "aaaUse toosend de centros de notificaciones (Windows Universal) de noticias de última hora"
description: "Usar centros de notificaciones de Azure con las etiquetas en toosend de registro de hello importantes noticias tooa aplicación universal de Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f102d286d2c7bd387fcfa2c7eab2ba31a0298517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Usar toosend centros de notificaciones noticias de última hora
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Información general
Este tema muestra cómo toouse centros de notificaciones de Azure toobroadcast importantes noticias notificaciones tooa tienda Windows o la aplicación de Windows Phone 8.1 (no de Silverlight). Si desea usar Windows Phone 8.1 Silverlight, consulte toohello [de Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) versión. Cuando haya finalizado, se puede tooregister puede romper la categorías de noticias que le interesen y recibir notificaciones de inserción solo para esas categorías. Este escenario es un patrón común para muchas aplicaciones donde las notificaciones tienen toogroups toobe enviado de los usuarios que previamente se han declarado el interés en ellos, por ejemplo, lector RSS, aplicaciones para ventiladores de música y así sucesivamente. 

Escenarios de difusión se habilitan mediante la inclusión de uno o varios *etiquetas* al crear un registro en el centro de notificaciones de Hola. Cuando se envían las notificaciones tooa etiqueta, todos los dispositivos que se han registrado para la etiqueta de hello recibirá notificación de Hola. Dado que las etiquetas son simplemente cadenas, no tiene toobe aprovisionado de antemano. Para obtener más información acerca de las etiquetas, consulte demasiado[notificación centros de enrutamiento y expresiones de etiqueta](notification-hubs-tags-segment-push-message.md).

> [!NOTE]
> Los proyectos de Tienda Windows y Windows Phone versión 8.1 y versiones anteriores no se admiten en Visual Studio 2017.  Para más información, consulte [Compatibilidad y destinatarios de la plataforma de Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs). 

## <a name="prerequisites"></a>Requisitos previos
En este tema se basa en la aplicación hello que creó en [empezar a trabajar con los centros de notificaciones][get-started]. Antes de comenzar este tutorial, debe haber completado la [Introducción a Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Agregar categoría selección toohello aplicación
Hola primer paso es tooadd Hola UI elementos tooyour existente página principal que permiten Hola usuario tooselect categorías tooregister. categorías de Hello seleccionadas por el usuario se almacenan en el dispositivo de Hola. Cuando se inicia la aplicación hello, se crea un registro de dispositivos en el centro de notificaciones con las categorías de hello seleccionado como etiquetas.

1. Abra el archivo de proyecto de hello MainPage.xaml y, a continuación, Hola copia sigue código Hola **cuadrícula** elemento:
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>
2. Haga hello **Shared** del proyecto y agregue una nueva clase denominada **notificaciones**, agregar hello **público** modificador toohello definición de clase, a continuación, agregue Hola después **con** nuevo archivo de código de instrucciones toohello:
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. Copia Hola siguiente de código en hello nueva **notificaciones** clase:
   
        private NotificationHub hub;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            return await SubscribeToCategories(categories);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
            return categories != null ? categories.Split(','): new string[0];
        }
   
        public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    Esta clase usa categorías de hello almacenamiento local toostore Hola de noticias que este dispositivo tiene tooreceive. Tenga en cuenta que en lugar de Hola que realiza la llamada *RegisterNativeAsync* método llamamos *RegisterTemplateAsync* tooregister para categorías de hello mediante un registro de plantilla. 
   
    También proporcionamos un nombre para la plantilla de hello ("simpleWNSTemplateExample"), dado que nos convenga tooregister más de una plantilla (por ejemplo uno para recibir notificaciones del sistema) y otro para iconos y necesitamos tooname en orden toobe puede tooupdate o eliminarlos.
   
    Tenga en cuenta que si un dispositivo se registra varias plantillas con hello misma etiqueta, un mensaje entrante de destino que se generará etiqueta varias notificaciones de entreguen dispositivo toohello (uno por cada plantilla). Este comportamiento es útil cuando hello mismo mensaje lógico tiene tooresult en varias notificaciones visuales, por ejemplo que muestra un distintivo y una notificación del sistema en una aplicación de almacenamiento de Windows.
   
    Para más información sobre el uso de plantillas, vea [Plantillas](notification-hubs-templates-cross-platform-push-messages.md).
4. En el archivo de proyecto de hello App.xaml.cs, agregar Hola después de la propiedad toohello **aplicación** clase:
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    Esta propiedad es toocreate usado y tener acceso un **notificaciones** instancia.
   
    Hola por encima del código, reemplace hello `<hub name>` y `<connection string with listen access>` marcadores de posición con la notificación concentrador hello y nombre de cadena de conexión para *DefaultListenSharedAccessSignature* que ha obtenido antes.
   
   > [!NOTE]
   > Dado que las credenciales que se distribuyen con una aplicación cliente no son generalmente seguras, debe distribuir solo clave hello para el acceso de escucha con la aplicación cliente. Escuchar habilita el acceso que no se puede modificar su tooregister de aplicación para notificaciones, pero los registros existentes y no se enviarán las notificaciones. clave de acceso completa de Hola se usa en un servicio seguro back-end para enviar notificaciones y cambiar los registros existentes.
   > 
   > 
5. En su MainPage.xaml.cs, agregue Hola después de línea:
   
        using Windows.UI.Popups;
6. En el archivo de proyecto de hello MainPage.xaml.cs, agregue Hola siguiente método:
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
            var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
   
    Este método crea una lista de categorías y se utiliza hello **notificaciones** clase toostore lista de hello en el almacenamiento local de Hola y registrar las etiquetas correspondientes Hola con el centro de notificaciones. Cuando se cambian las categorías, se vuelve a crear el registro de hello con nuevas categorías de Hola.

La aplicación ahora es capaz de toostore un conjunto de categorías en el almacenamiento local en el dispositivo de Hola y registrar con el centro de notificaciones de hello siempre que los cambios de usuarios Hola Hola selección de categorías.

## <a name="register-for-notifications"></a>Registro de notificaciones
Estos pasos se registran con el centro de notificaciones de Hola durante el inicio con las categorías de Hola que han sido almacenados en el almacenamiento local.

> [!NOTE]
> Dado canal Hola URI asignado por hello servicios de notificación de Windows (WNS) puede cambiar en cualquier momento, se deben registrar para notificaciones con frecuencia tooavoid errores de notificación. En este ejemplo se registra para la notificación cada vez que inicia la aplicación hello. Para las aplicaciones que se ejecutan con frecuencia, más de una vez al día, puede probablemente Omitir ancho de banda de registro toopreserve si ha pasado menos de un día desde el registro de hello anterior.
> 
> 

1. Abra Hola Hola de archivo y actualización de App.xaml.cs **InitNotificationsAsync** Hola de toouse método `notifications` toosubscribe clase basadas en categorías.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    Esto garantiza que cada vez que inicia la aplicación hello recupera categorías Hola desde el almacenamiento local y solicita un registro para estas categorías. Hola **InitNotificationsAsync** método se creó como parte del programa Hola a [empezar a trabajar con los centros de notificaciones] [ get-started] tutorial.
2. En el archivo de proyecto de hello MainPage.xaml.cs, agregar Hola después código toohello *OnNavigatedTo* método:
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldToggle.IsOn = true;
            if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
            if (categories.Contains("Business")) BusinessToggle.IsOn = true;
            if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
            if (categories.Contains("Science")) ScienceToggle.IsOn = true;
            if (categories.Contains("Sports")) SportsToggle.IsOn = true;
        }
   
    Esta página principal de Hola de actualizaciones basada en estado de Hola de previamente guardado categorías.

aplicación Hello ahora está completa y puede almacenar un conjunto de categorías en hello dispositivo almacenamiento local usa tooregister con el centro de notificaciones de hello siempre que los cambios de usuarios Hola Hola selección de categorías. A continuación, definimos un back-end que puede enviar la aplicación de toothis de notificaciones de categoría.

## <a name="sending-tagged-notifications"></a>Envío de notificaciones con etiquetas
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Ejecutar aplicación hello y generar notificaciones
1. En Visual Studio, presione F5 toocompile e iniciará la aplicación hello.
   
    ![][1]
   
    Tenga en cuenta que interfaz de usuario proporciona un conjunto de la aplicación hello alterna que le permite elegir Hola categorías toosubscribe a.
2. Habilite uno o más elementos de alternancia de las categorías y, a continuación, haga clic en **Suscribirse**.
   
    aplicación Hello convierte categorías Hola seleccionado en las etiquetas y solicita un nuevo registro de dispositivo para etiquetas de hello seleccionada del centro de notificaciones de Hola. Hello categorías registrados se devuelve y se muestran en un cuadro de diálogo.
   
    ![][19]
3. Enviar una nueva notificación de back-end de hello en uno de hello siguientes formas:
   
   * **Aplicación de consola:** iniciar la aplicación de consola de hello.
   * **Java/PHP:** ejecute su aplicación/script.
     
     Las notificaciones para las categorías de hello seleccionado aparecen como notificaciones del sistema.
     
     ![][14]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial hemos visto cómo toobroadcast noticias de última hora por categoría. Considere la posibilidad de completar uno de hello tutoriales que indican errores de otros escenarios avanzados de centros de notificaciones:

* [Utilice noticias de última hora de toobroadcast localizado de los centros de notificaciones]
  
    Obtenga información acerca de cómo hello tooexpand interrumpir el envío de noticias aplicación tooenable localizar las notificaciones.

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[Utilice noticias de última hora de toobroadcast localizado de los centros de notificaciones]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
