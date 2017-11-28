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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="20bc0-103">Usar toosend centros de notificaciones noticias de última hora</span><span class="sxs-lookup"><span data-stu-id="20bc0-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="20bc0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="20bc0-104">Overview</span></span>
<span data-ttu-id="20bc0-105">Este tema muestra cómo toouse centros de notificaciones de Azure toobroadcast importantes noticias notificaciones tooa tienda Windows o la aplicación de Windows Phone 8.1 (no de Silverlight).</span><span class="sxs-lookup"><span data-stu-id="20bc0-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="20bc0-106">Si desea usar Windows Phone 8.1 Silverlight, consulte toohello [de Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) versión.</span><span class="sxs-lookup"><span data-stu-id="20bc0-106">If you are targeting Windows Phone 8.1 Silverlight, please refer toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="20bc0-107">Cuando haya finalizado, se puede tooregister puede romper la categorías de noticias que le interesen y recibir notificaciones de inserción solo para esas categorías.</span><span class="sxs-lookup"><span data-stu-id="20bc0-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="20bc0-108">Este escenario es un patrón común para muchas aplicaciones donde las notificaciones tienen toogroups toobe enviado de los usuarios que previamente se han declarado el interés en ellos, por ejemplo, lector RSS, aplicaciones para ventiladores de música y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="20bc0-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="20bc0-109">Escenarios de difusión se habilitan mediante la inclusión de uno o varios *etiquetas* al crear un registro en el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="20bc0-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="20bc0-110">Cuando se envían las notificaciones tooa etiqueta, todos los dispositivos que se han registrado para la etiqueta de hello recibirá notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="20bc0-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="20bc0-111">Dado que las etiquetas son simplemente cadenas, no tiene toobe aprovisionado de antemano.</span><span class="sxs-lookup"><span data-stu-id="20bc0-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="20bc0-112">Para obtener más información acerca de las etiquetas, consulte demasiado[notificación centros de enrutamiento y expresiones de etiqueta](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="20bc0-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="20bc0-113">Los proyectos de Tienda Windows y Windows Phone versión 8.1 y versiones anteriores no se admiten en Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="20bc0-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="20bc0-114">Para más información, consulte [Compatibilidad y destinatarios de la plataforma de Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="20bc0-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="20bc0-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="20bc0-115">Prerequisites</span></span>
<span data-ttu-id="20bc0-116">En este tema se basa en la aplicación hello que creó en [empezar a trabajar con los centros de notificaciones][get-started].</span><span class="sxs-lookup"><span data-stu-id="20bc0-116">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="20bc0-117">Antes de comenzar este tutorial, debe haber completado la [Introducción a Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="20bc0-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="20bc0-118">Agregar categoría selección toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="20bc0-118">Add category selection toohello app</span></span>
<span data-ttu-id="20bc0-119">Hola primer paso es tooadd Hola UI elementos tooyour existente página principal que permiten Hola usuario tooselect categorías tooregister.</span><span class="sxs-lookup"><span data-stu-id="20bc0-119">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="20bc0-120">categorías de Hello seleccionadas por el usuario se almacenan en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="20bc0-120">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="20bc0-121">Cuando se inicia la aplicación hello, se crea un registro de dispositivos en el centro de notificaciones con las categorías de hello seleccionado como etiquetas.</span><span class="sxs-lookup"><span data-stu-id="20bc0-121">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="20bc0-122">Abra el archivo de proyecto de hello MainPage.xaml y, a continuación, Hola copia sigue código Hola **cuadrícula** elemento:</span><span class="sxs-lookup"><span data-stu-id="20bc0-122">Open hello MainPage.xaml project file, then copy hello following code in hello **Grid** element:</span></span>
   
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
2. <span data-ttu-id="20bc0-123">Haga hello **Shared** del proyecto y agregue una nueva clase denominada **notificaciones**, agregar hello **público** modificador toohello definición de clase, a continuación, agregue Hola después **con** nuevo archivo de código de instrucciones toohello:</span><span class="sxs-lookup"><span data-stu-id="20bc0-123">Right click hello **Shared** project and add a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="20bc0-124">Copia Hola siguiente de código en hello nueva **notificaciones** clase:</span><span class="sxs-lookup"><span data-stu-id="20bc0-124">Copy hello following code into hello new **Notifications** class:</span></span>
   
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
   
    <span data-ttu-id="20bc0-125">Esta clase usa categorías de hello almacenamiento local toostore Hola de noticias que este dispositivo tiene tooreceive.</span><span class="sxs-lookup"><span data-stu-id="20bc0-125">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="20bc0-126">Tenga en cuenta que en lugar de Hola que realiza la llamada *RegisterNativeAsync* método llamamos *RegisterTemplateAsync* tooregister para categorías de hello mediante un registro de plantilla.</span><span class="sxs-lookup"><span data-stu-id="20bc0-126">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync* tooregister for hello categories using a template registration.</span></span> 
   
    <span data-ttu-id="20bc0-127">También proporcionamos un nombre para la plantilla de hello ("simpleWNSTemplateExample"), dado que nos convenga tooregister más de una plantilla (por ejemplo uno para recibir notificaciones del sistema) y otro para iconos y necesitamos tooname en orden toobe puede tooupdate o eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="20bc0-127">We also provide a name for hello template ("simpleWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="20bc0-128">Tenga en cuenta que si un dispositivo se registra varias plantillas con hello misma etiqueta, un mensaje entrante de destino que se generará etiqueta varias notificaciones de entreguen dispositivo toohello (uno por cada plantilla).</span><span class="sxs-lookup"><span data-stu-id="20bc0-128">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="20bc0-129">Este comportamiento es útil cuando hello mismo mensaje lógico tiene tooresult en varias notificaciones visuales, por ejemplo que muestra un distintivo y una notificación del sistema en una aplicación de almacenamiento de Windows.</span><span class="sxs-lookup"><span data-stu-id="20bc0-129">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="20bc0-130">Para más información sobre el uso de plantillas, vea [Plantillas](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="20bc0-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="20bc0-131">En el archivo de proyecto de hello App.xaml.cs, agregar Hola después de la propiedad toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="20bc0-131">In hello App.xaml.cs project file, add hello following property toohello **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="20bc0-132">Esta propiedad es toocreate usado y tener acceso un **notificaciones** instancia.</span><span class="sxs-lookup"><span data-stu-id="20bc0-132">This property is used toocreate and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="20bc0-133">Hola por encima del código, reemplace hello `<hub name>` y `<connection string with listen access>` marcadores de posición con la notificación concentrador hello y nombre de cadena de conexión para *DefaultListenSharedAccessSignature* que ha obtenido antes.</span><span class="sxs-lookup"><span data-stu-id="20bc0-133">In hello above code, replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="20bc0-134">Dado que las credenciales que se distribuyen con una aplicación cliente no son generalmente seguras, debe distribuir solo clave hello para el acceso de escucha con la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="20bc0-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="20bc0-135">Escuchar habilita el acceso que no se puede modificar su tooregister de aplicación para notificaciones, pero los registros existentes y no se enviarán las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="20bc0-135">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="20bc0-136">clave de acceso completa de Hola se usa en un servicio seguro back-end para enviar notificaciones y cambiar los registros existentes.</span><span class="sxs-lookup"><span data-stu-id="20bc0-136">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="20bc0-137">En su MainPage.xaml.cs, agregue Hola después de línea:</span><span class="sxs-lookup"><span data-stu-id="20bc0-137">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="20bc0-138">En el archivo de proyecto de hello MainPage.xaml.cs, agregue Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="20bc0-138">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="20bc0-139">Este método crea una lista de categorías y se utiliza hello **notificaciones** clase toostore lista de hello en el almacenamiento local de Hola y registrar las etiquetas correspondientes Hola con el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="20bc0-139">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="20bc0-140">Cuando se cambian las categorías, se vuelve a crear el registro de hello con nuevas categorías de Hola.</span><span class="sxs-lookup"><span data-stu-id="20bc0-140">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="20bc0-141">La aplicación ahora es capaz de toostore un conjunto de categorías en el almacenamiento local en el dispositivo de Hola y registrar con el centro de notificaciones de hello siempre que los cambios de usuarios Hola Hola selección de categorías.</span><span class="sxs-lookup"><span data-stu-id="20bc0-141">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="20bc0-142">Registro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="20bc0-142">Register for notifications</span></span>
<span data-ttu-id="20bc0-143">Estos pasos se registran con el centro de notificaciones de Hola durante el inicio con las categorías de Hola que han sido almacenados en el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="20bc0-143">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="20bc0-144">Dado canal Hola URI asignado por hello servicios de notificación de Windows (WNS) puede cambiar en cualquier momento, se deben registrar para notificaciones con frecuencia tooavoid errores de notificación.</span><span class="sxs-lookup"><span data-stu-id="20bc0-144">Because hello channel URI assigned by hello Windows Notification Service (WNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="20bc0-145">En este ejemplo se registra para la notificación cada vez que inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="20bc0-145">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="20bc0-146">Para las aplicaciones que se ejecutan con frecuencia, más de una vez al día, puede probablemente Omitir ancho de banda de registro toopreserve si ha pasado menos de un día desde el registro de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="20bc0-146">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="20bc0-147">Abra Hola Hola de archivo y actualización de App.xaml.cs **InitNotificationsAsync** Hola de toouse método `notifications` toosubscribe clase basadas en categorías.</span><span class="sxs-lookup"><span data-stu-id="20bc0-147">Open hello App.xaml.cs file and update hello **InitNotificationsAsync** method toouse hello `notifications` class toosubscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="20bc0-148">Esto garantiza que cada vez que inicia la aplicación hello recupera categorías Hola desde el almacenamiento local y solicita un registro para estas categorías.</span><span class="sxs-lookup"><span data-stu-id="20bc0-148">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="20bc0-149">Hola **InitNotificationsAsync** método se creó como parte del programa Hola a [empezar a trabajar con los centros de notificaciones] [ get-started] tutorial.</span><span class="sxs-lookup"><span data-stu-id="20bc0-149">hello **InitNotificationsAsync** method was created as part of hello [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="20bc0-150">En el archivo de proyecto de hello MainPage.xaml.cs, agregar Hola después código toohello *OnNavigatedTo* método:</span><span class="sxs-lookup"><span data-stu-id="20bc0-150">In hello MainPage.xaml.cs project file, add hello following code toohello *OnNavigatedTo* method:</span></span>
   
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
   
    <span data-ttu-id="20bc0-151">Esta página principal de Hola de actualizaciones basada en estado de Hola de previamente guardado categorías.</span><span class="sxs-lookup"><span data-stu-id="20bc0-151">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="20bc0-152">aplicación Hello ahora está completa y puede almacenar un conjunto de categorías en hello dispositivo almacenamiento local usa tooregister con el centro de notificaciones de hello siempre que los cambios de usuarios Hola Hola selección de categorías.</span><span class="sxs-lookup"><span data-stu-id="20bc0-152">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="20bc0-153">A continuación, definimos un back-end que puede enviar la aplicación de toothis de notificaciones de categoría.</span><span class="sxs-lookup"><span data-stu-id="20bc0-153">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="20bc0-154">Envío de notificaciones con etiquetas</span><span class="sxs-lookup"><span data-stu-id="20bc0-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="20bc0-155">Ejecutar aplicación hello y generar notificaciones</span><span class="sxs-lookup"><span data-stu-id="20bc0-155">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="20bc0-156">En Visual Studio, presione F5 toocompile e iniciará la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="20bc0-156">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="20bc0-157">Tenga en cuenta que interfaz de usuario proporciona un conjunto de la aplicación hello alterna que le permite elegir Hola categorías toosubscribe a.</span><span class="sxs-lookup"><span data-stu-id="20bc0-157">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="20bc0-158">Habilite uno o más elementos de alternancia de las categorías y, a continuación, haga clic en **Suscribirse**.</span><span class="sxs-lookup"><span data-stu-id="20bc0-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="20bc0-159">aplicación Hello convierte categorías Hola seleccionado en las etiquetas y solicita un nuevo registro de dispositivo para etiquetas de hello seleccionada del centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="20bc0-159">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="20bc0-160">Hello categorías registrados se devuelve y se muestran en un cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="20bc0-160">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="20bc0-161">Enviar una nueva notificación de back-end de hello en uno de hello siguientes formas:</span><span class="sxs-lookup"><span data-stu-id="20bc0-161">Send a new notification from hello backend in one of hello following ways:</span></span>
   
   * <span data-ttu-id="20bc0-162">**Aplicación de consola:** iniciar la aplicación de consola de hello.</span><span class="sxs-lookup"><span data-stu-id="20bc0-162">**Console app:** start hello console app.</span></span>
   * <span data-ttu-id="20bc0-163">**Java/PHP:** ejecute su aplicación/script.</span><span class="sxs-lookup"><span data-stu-id="20bc0-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="20bc0-164">Las notificaciones para las categorías de hello seleccionado aparecen como notificaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="20bc0-164">Notifications for hello selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="20bc0-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="20bc0-165">Next steps</span></span>
<span data-ttu-id="20bc0-166">En este tutorial hemos visto cómo toobroadcast noticias de última hora por categoría.</span><span class="sxs-lookup"><span data-stu-id="20bc0-166">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="20bc0-167">Considere la posibilidad de completar uno de hello tutoriales que indican errores de otros escenarios avanzados de centros de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="20bc0-167">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="20bc0-168">[Utilice noticias de última hora de toobroadcast localizado de los centros de notificaciones]</span><span class="sxs-lookup"><span data-stu-id="20bc0-168">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="20bc0-169">Obtenga información acerca de cómo hello tooexpand interrumpir el envío de noticias aplicación tooenable localizar las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="20bc0-169">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
