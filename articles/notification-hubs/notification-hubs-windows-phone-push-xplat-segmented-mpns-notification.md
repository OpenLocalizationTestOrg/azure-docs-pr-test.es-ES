---
title: "aaaUse toosend de centros de notificaciones (Windows Phone) de noticias de última hora"
description: "Utilice la etiqueta de toouse de centros de notificaciones de Azure en toosend registros principales de la aplicación de Windows Phone tooa de noticias."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 3519a8701105f88198afe288e59e9204420234db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="d7ccc-103">Usar toosend centros de notificaciones noticias de última hora</span><span class="sxs-lookup"><span data-stu-id="d7ccc-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="d7ccc-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d7ccc-104">Overview</span></span>
<span data-ttu-id="d7ccc-105">Este tema muestra cómo toouse centros de notificaciones de Azure toobroadcast importantes noticias notificaciones tooa aplicación de Silverlight de Windows Phone 8.0/8.1.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="d7ccc-106">Si se dirige a tienda Windows o una aplicación de Windows Phone 8.1, consulte tootoohello [universales de Windows](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) versión.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="d7ccc-107">Cuando haya finalizado, se puede tooregister puede romper la categorías de noticias que le interesen y recibir notificaciones de inserción solo para esas categorías.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="d7ccc-108">Este escenario es un patrón común para muchas aplicaciones donde las notificaciones tienen toogroups toobe enviado de los usuarios que previamente se han declarado el interés en ellos, por ejemplo, aplicaciones de ventiladores de música, etcetera, lector RSS.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="d7ccc-109">Escenarios de difusión se habilitan mediante la inclusión de uno o varios *etiquetas* al crear un registro en el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="d7ccc-110">Cuando se envían las notificaciones tooa etiqueta, todos los dispositivos que se han registrado para la etiqueta de hello recibirá notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="d7ccc-111">Dado que las etiquetas son simplemente cadenas, no tiene toobe aprovisionado de antemano.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="d7ccc-112">Para obtener más información acerca de las etiquetas, consulte demasiado[notificación centros de enrutamiento y expresiones de etiqueta](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="d7ccc-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7ccc-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d7ccc-113">Prerequisites</span></span>
<span data-ttu-id="d7ccc-114">En este tema se basa en la aplicación hello que creó en [empezar a trabajar con los centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="d7ccc-114">This topic builds on hello app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="d7ccc-115">Antes de comenzar este tutorial, debe haber completado la [empezar a trabajar con los centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="d7ccc-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="d7ccc-116">Agregar categoría selección toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="d7ccc-116">Add category selection toohello app</span></span>
<span data-ttu-id="d7ccc-117">Hola primer paso es tooadd Hola UI elementos tooyour existente página principal que permiten Hola usuario tooselect categorías tooregister.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-117">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="d7ccc-118">categorías de Hello seleccionadas por el usuario se almacenan en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-118">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="d7ccc-119">Cuando se inicia la aplicación hello, se crea un registro de dispositivos en el centro de notificaciones con las categorías de hello seleccionado como etiquetas.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-119">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="d7ccc-120">Abrir archivo de proyecto de MainPage.xaml hello, a continuación, reemplace hello **cuadrícula** elementos denominados `TitlePanel` y `ContentPanel` con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="d7ccc-120">Open hello MainPage.xaml project file, then replace hello **Grid** elements named `TitlePanel` and `ContentPanel` with hello following code:</span></span>
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. <span data-ttu-id="d7ccc-121">En proyecto de hello, cree una nueva clase denominada **notificaciones**, agregar hello **público** modificador toohello definición de la clase, a continuación, agregue los siguiente hello **con** instrucciones toohello al nuevo archivo de código:</span><span class="sxs-lookup"><span data-stu-id="d7ccc-121">In hello project, create a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="d7ccc-122">Copia Hola siguiente de código en hello nueva **notificaciones** clase:</span><span class="sxs-lookup"><span data-stu-id="d7ccc-122">Copy hello following code into hello new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task toocomplete registration in hello ChannelUriUpdated event handler
        private TaskCompletionSource<Registration> registrationTask;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
            return categories != null ? categories.Split(',') : new string[0];
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            var categoriesAsString = string.Join(",", categories);
            var settings = IsolatedStorageSettings.ApplicationSettings;
            if (!settings.Contains("categories"))
            {
                settings.Add("categories", categoriesAsString);
            }
            else
            {
                settings["categories"] = categoriesAsString;
            }
            settings.Save();
   
            return await SubscribeToCategories();
        }
   
        public async Task<Registration> SubscribeToCategories()
        {
            registrationTask = new TaskCompletionSource<Registration>();
   
            var channel = HttpNotificationChannel.Find("MyPushChannel");
   
            if (channel == null)
            {
                channel = new HttpNotificationChannel("MyPushChannel");
                channel.Open();
                channel.BindToShellToast();
                channel.ChannelUriUpdated += channel_ChannelUriUpdated;
   
                // This is optional, used tooreceive notifications while hello app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete hello registrationTask here.  
            // If it is null, hello registrationTask will be completed in hello ChannelUriUpdated event handler.
            if (channel.ChannelUri != null)
            {
                await RegisterTemplate(channel.ChannelUri);
            }
   
            return await registrationTask.Task;
        }
   
        async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            await RegisterTemplate(e.ChannelUri);
        }
   
        async Task<Registration> RegisterTemplate(Uri channelUri)
        {
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // hello stored categories tags are passed with hello template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used tooreceive notifications while hello app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out hello information that was part of hello message.
            foreach (string key in e.Collection.Keys)
            {
                message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);
   
                if (string.Compare(
                    key,
                    "wp:Param",
                    System.Globalization.CultureInfo.InvariantCulture,
                    System.Globalization.CompareOptions.IgnoreCase) == 0)
                {
                    relativeUri = e.Collection[key];
                }
            }
   
            // Display a dialog of all hello fields in hello toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="d7ccc-123">Esta clase usa Hola aislada almacenamiento toostore Hola categorías de noticias que el dispositivo está tooreceive.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-123">This class uses hello isolated storage toostore hello categories of news that this device is tooreceive.</span></span> <span data-ttu-id="d7ccc-124">También contiene métodos tooregister para estas categorías mediante un [plantilla](notification-hubs-templates-cross-platform-push-messages.md) registrar la notificación.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-124">It also contains methods tooregister for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="d7ccc-125">En el archivo de proyecto de hello App.xaml.cs, agregar Hola después de la propiedad toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-125">In hello App.xaml.cs project file, add hello following property toohello **App** class.</span></span> <span data-ttu-id="d7ccc-126">Reemplace hello `<hub name>` y `<connection string with listen access>` marcadores de posición con la notificación concentrador hello y nombre de cadena de conexión para *DefaultListenSharedAccessSignature* que ha obtenido antes.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-126">Replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="d7ccc-127">Dado que las credenciales que se distribuyen con una aplicación cliente no son generalmente seguras, debe distribuir solo clave hello para el acceso de escucha con la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="d7ccc-128">Escuchar habilita el acceso que no se puede modificar su tooregister de aplicación para notificaciones, pero los registros existentes y no se enviarán las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-128">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="d7ccc-129">clave de acceso completa de Hola se usa en un servicio seguro back-end para enviar notificaciones y cambiar los registros existentes.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-129">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="d7ccc-130">En su MainPage.xaml.cs, agregue Hola después de línea:</span><span class="sxs-lookup"><span data-stu-id="d7ccc-130">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="d7ccc-131">En el archivo de proyecto de hello MainPage.xaml.cs, agregue Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="d7ccc-131">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
          var categories = new HashSet<string>();
          if (WorldCheckBox.IsChecked == true) categories.Add("World");
          if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
          if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
          if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
          if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
          if (SportsCheckBox.IsChecked == true) categories.Add("Sports");
   
          var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
          MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
             result.RegistrationId);
        }
   
    <span data-ttu-id="d7ccc-132">Este método crea una lista de categorías y se utiliza hello **notificaciones** clase toostore lista de hello en el almacenamiento local de Hola y registrar las etiquetas correspondientes Hola con el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-132">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="d7ccc-133">Cuando se cambian las categorías, se vuelve a crear el registro de hello con nuevas categorías de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-133">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="d7ccc-134">La aplicación ahora es capaz de toostore un conjunto de categorías en el almacenamiento local en el dispositivo de Hola y registrar con el centro de notificaciones de hello siempre que los cambios de usuarios Hola Hola selección de categorías.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-134">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="d7ccc-135">Registro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="d7ccc-135">Register for notifications</span></span>
<span data-ttu-id="d7ccc-136">Estos pasos se registran con el centro de notificaciones de Hola durante el inicio con las categorías de Hola que han sido almacenados en el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-136">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="d7ccc-137">Dado canal Hola URI asignado por hello servicio de notificaciones de inserción de Microsoft (MPNS) puede cambiar en cualquier momento, se deben registrar para notificaciones con frecuencia tooavoid errores de notificación.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-137">Because hello channel URI assigned by hello Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="d7ccc-138">En este ejemplo se registra para las notificaciones cada vez que inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-138">This example registers for notifications every time that hello app starts.</span></span> <span data-ttu-id="d7ccc-139">Para las aplicaciones que se ejecutan con frecuencia, más de una vez al día, puede probablemente Omitir ancho de banda de registro toopreserve si ha pasado menos de un día desde el registro de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-139">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="d7ccc-140">Abra el archivo App.xaml.cs de hello y agregue hello **async** modificador demasiado**Application_Launching** método y reemplazar Hola centros de notificaciones código de registro que agregó en [empezar a trabajar con los centros de notificaciones] con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="d7ccc-140">Open hello App.xaml.cs file and add hello **async** modifier too**Application_Launching** method and replace hello Notification Hubs registration code that you added in [Get started with Notification Hubs] with hello following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="d7ccc-141">Esto garantiza que cada vez que inicia la aplicación hello recupera categorías Hola desde el almacenamiento local y solicita un registro para estas categorías.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-141">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="d7ccc-142">En el archivo de proyecto de hello MainPage.xaml.cs, agregue Hola después el código que implementa hello **OnNavigatedTo** método:</span><span class="sxs-lookup"><span data-stu-id="d7ccc-142">In hello MainPage.xaml.cs project file, add hello following code that implements hello **OnNavigatedTo** method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
            if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
            if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
            if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
            if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
            if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
        }
   
    <span data-ttu-id="d7ccc-143">Esta página principal de Hola de actualizaciones basada en estado de Hola de previamente guardado categorías.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-143">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="d7ccc-144">aplicación Hello ahora está completa y puede almacenar un conjunto de categorías en hello dispositivo almacenamiento local usa tooregister con el centro de notificaciones de hello siempre que los cambios de usuarios Hola Hola selección de categorías.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-144">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="d7ccc-145">A continuación, definimos un back-end que puede enviar la aplicación de toothis de notificaciones de categoría.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-145">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="d7ccc-146">Envío de notificaciones con etiquetas</span><span class="sxs-lookup"><span data-stu-id="d7ccc-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="d7ccc-147">Ejecutar aplicación hello y generar notificaciones</span><span class="sxs-lookup"><span data-stu-id="d7ccc-147">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="d7ccc-148">En Visual Studio, presione F5 toocompile e iniciará la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-148">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="d7ccc-149">Tenga en cuenta que interfaz de usuario proporciona un conjunto de la aplicación hello alterna que le permite elegir Hola categorías toosubscribe a.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-149">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="d7ccc-150">Habilite uno o más elementos de alternancia de las categorías y, a continuación, haga clic en **Suscribirse**.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="d7ccc-151">aplicación Hello convierte categorías Hola seleccionado en las etiquetas y solicita un nuevo registro de dispositivo para etiquetas de hello seleccionada del centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-151">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="d7ccc-152">Hello categorías registrados se devuelve y se muestran en un cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-152">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="d7ccc-153">Después de recibir una confirmación de que sus categorías eran suscripción completado, ejecute las notificaciones de aplicación toosend consola de Hola para cada categorías.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-153">After receiving a confirmation that your categories were subscription completed, run hello console app toosend notifications for each categories.</span></span> <span data-ttu-id="d7ccc-154">Compruebe que sólo recibirá una notificación para categorías de Hola que se haya suscrito.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-154">Verify you only receive a notification for hello categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="d7ccc-155">Ha completado este tema.</span><span class="sxs-lookup"><span data-stu-id="d7ccc-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how toobroadcast breaking news by category. Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs toobroadcast localized breaking news]

    Learn how tooexpand hello breaking news app tooenable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how toopush notifications toospecific authenticated users. This is a good solution for sending notifications only toospecific users.
-->

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[empezar a trabajar con los centros de notificaciones]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/
[Use Notification Hubs toobroadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Phone]: ??

