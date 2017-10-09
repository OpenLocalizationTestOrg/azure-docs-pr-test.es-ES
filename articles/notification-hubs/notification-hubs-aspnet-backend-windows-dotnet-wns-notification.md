---
title: "aaaAzure los usuarios notificar a los centros de notificación con back-end de .NET"
description: "Obtenga información acerca de cómo toosend segura las notificaciones de inserción en Azure. Ejemplos de código escritos en C# mediante Hola .NET API."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="05083-104">Los Centros de notificaciones de Azure notifican a los usuarios con back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="05083-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="05083-105">Información general</span><span class="sxs-lookup"><span data-stu-id="05083-105">Overview</span></span>
<span data-ttu-id="05083-106">Compatibilidad de la notificación de inserción en Azure permite tooaccess una fácil de usar, multiplataforma y la infraestructura de inserción de escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa para dispositivos móviles plataformas.</span><span class="sxs-lookup"><span data-stu-id="05083-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="05083-107">Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push usuario de aplicación específica de tooa de notificaciones en un dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="05083-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="05083-108">Un back-end de ASP.NET WebAPI es tooauthenticate usa clientes.</span><span class="sxs-lookup"><span data-stu-id="05083-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="05083-109">Hola autenticadas usuario del cliente y etiqueta se agregará automáticamente al registro de hello back-end toonotification.</span><span class="sxs-lookup"><span data-stu-id="05083-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="05083-110">Esta etiqueta será toosend usado por las notificaciones de toogenerate de hello back-end para un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="05083-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="05083-111">Para obtener más información sobre cómo registrar para notificaciones mediante un aplicación de back-end, vea el tema de la Guía de hello [registrar desde su aplicación de back-end](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="05083-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="05083-112">Este tutorial se basa en el centro de notificaciones de Hola y el proyecto que creó en hello [empezar a trabajar con los centros de notificaciones] tutorial.</span><span class="sxs-lookup"><span data-stu-id="05083-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="05083-113">Este tutorial también es toohello de requisitos previos de hello [seguros Push] tutorial.</span><span class="sxs-lookup"><span data-stu-id="05083-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="05083-114">Después de haber completado los pasos de hello en este tutorial, puede continuar toohello [seguros Push] tutorial, que muestra cómo toomodify Hola código en este tutorial toosend una notificación de inserción de forma segura.</span><span class="sxs-lookup"><span data-stu-id="05083-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="05083-115">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="05083-115">Before you begin</span></span>
<span data-ttu-id="05083-116">Nos tomamos muy en serio sus comentarios.</span><span class="sxs-lookup"><span data-stu-id="05083-116">We do take your feedback seriously.</span></span> <span data-ttu-id="05083-117">Si tiene dificultades completar este tema o recomendaciones para mejorar el contenido, le agradeceríamos sus comentarios en la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="05083-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="05083-118">código de Hello completado para este tutorial se puede encontrar en GitHub [aquí](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="05083-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="05083-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="05083-119">Prerequisites</span></span>
<span data-ttu-id="05083-120">Antes de comenzar este tutorial, debe haber realizado los siguientes tutoriales de Servicios móviles:</span><span class="sxs-lookup"><span data-stu-id="05083-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="05083-121">[empezar a trabajar con los centros de notificaciones]</span><span class="sxs-lookup"><span data-stu-id="05083-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="05083-122">Crear el centro de notificaciones y reservar el nombre de la aplicación hello y registrar las notificaciones de tooreceive en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="05083-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="05083-123">En este tutorial se asume que ya ha completado estos pasos.</span><span class="sxs-lookup"><span data-stu-id="05083-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="05083-124">Si no es así, siga los pasos de hello en [Introducción a centros de notificaciones (tienda Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); en concreto, Hola secciones [registrar la aplicación para la tienda Windows hello](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) y [configurar el centro de notificaciones](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="05083-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="05083-125">En concreto, asegúrese de que ha escrito hello **SID del paquete** y **secreto de cliente** valores en el portal de hello, Hola **configurar** pestaña para el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="05083-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="05083-126">Este procedimiento de configuración se describe en la sección de hello [configurar el centro de notificaciones](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="05083-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="05083-127">Se trata de un paso importante: si las credenciales de hello en el portal de hello no coinciden con los especificados para el nombre de la aplicación hello que elija, la notificación de inserción de hello no se realizará correctamente.</span><span class="sxs-lookup"><span data-stu-id="05083-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="05083-128">Si usas aplicaciones móviles en el servicio de aplicación de Azure como el servicio back-end, vea hello [versión de aplicaciones móviles](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="05083-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="05083-129">Actualizar código de hello para el proyecto de cliente de Hola</span><span class="sxs-lookup"><span data-stu-id="05083-129">Update hello code for hello client project</span></span>
<span data-ttu-id="05083-130">En esta sección, actualizar código de hello en proyecto de hello ha completado de hello [empezar a trabajar con los centros de notificaciones] tutorial.</span><span class="sxs-lookup"><span data-stu-id="05083-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="05083-131">Hola ya debe ser asociado con el almacén de Hola y configurado para el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="05083-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="05083-132">En esta sección, agregará código toocall hello WebAPI back-end y usarlo para registrar y enviar notificaciones.</span><span class="sxs-lookup"><span data-stu-id="05083-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="05083-133">En Visual Studio, abra la solución de Hola de Hola que creó para hello [empezar a trabajar con los centros de notificaciones] tutorial.</span><span class="sxs-lookup"><span data-stu-id="05083-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="05083-134">En el Explorador de soluciones, haga clic en hello **(Windows 8.1)** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="05083-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="05083-135">En el lado izquierdo de hello, haga clic en **Online**.</span><span class="sxs-lookup"><span data-stu-id="05083-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="05083-136">Hola **búsqueda** , escriba **cliente Http**.</span><span class="sxs-lookup"><span data-stu-id="05083-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="05083-137">En la lista de resultados de hello, haga clic en **Microsoft HTTP Client Libraries**y, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="05083-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="05083-138">Completar la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="05083-138">Complete hello installation.</span></span>
6. <span data-ttu-id="05083-139">Nuevo en hello NuGet **búsqueda** , escriba **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="05083-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="05083-140">Instalar hello **Json.NET** paquete y ventana de hello, a continuación, cierre el Administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="05083-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="05083-141">Repita los pasos de hello anteriormente para hello **(Windows Phone 8.1)** Hola de proyecto tooinstall **JSON.NET** paquete NuGet para el proyecto de Windows Phone Hola.</span><span class="sxs-lookup"><span data-stu-id="05083-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="05083-142">En el Explorador de soluciones, en hello **(Windows 8.1)** proyecto de equipo y haga doble clic en **MainPage.xaml** tooopen en el editor de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="05083-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="05083-143">Hola **MainPage.xaml** código XML, reemplace hello `<Grid>` sección con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="05083-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="05083-144">Este código agrega un cuadro de texto Nombre de usuario y contraseña que Hola usuario se autenticará con.</span><span class="sxs-lookup"><span data-stu-id="05083-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="05083-145">También agrega cuadros de texto de mensaje de notificación de Hola y la etiqueta de nombre de usuario de Hola que debe recibir una notificación de hello:</span><span class="sxs-lookup"><span data-stu-id="05083-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="05083-146">En el Explorador de soluciones, en hello **(Windows Phone 8.1)** proyecto abierto **MainPage.xaml** y reemplazar Hola Windows Phone 8.1 `<Grid>` sección con el mismo código anterior.</span><span class="sxs-lookup"><span data-stu-id="05083-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="05083-147">interfaz de Hello debería ser similar toowhats que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="05083-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="05083-148">En el Explorador de soluciones, abra hello **MainPage.xaml.cs** archivo para hello **(Windows 8.1)** y **(Windows Phone 8.1)** proyectos.</span><span class="sxs-lookup"><span data-stu-id="05083-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="05083-149">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de ambos archivos:</span><span class="sxs-lookup"><span data-stu-id="05083-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="05083-150">En **MainPage.xaml.cs** para hello **(Windows 8.1)** y **(Windows Phone 8.1)** proyectos, agregar Hola siguiente miembro toohello `MainPage` clase.</span><span class="sxs-lookup"><span data-stu-id="05083-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="05083-151">Ser seguro tooreplace `<Enter Your Backend Endpoint>` con hello obtenida anteriormente el punto de conexión real de back-end.</span><span class="sxs-lookup"><span data-stu-id="05083-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="05083-152">Por ejemplo: `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="05083-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="05083-153">Agregar código de hello debajo de la clase MainPage de toohello en **MainPage.xaml.cs** para hello **(Windows 8.1)** y **(Windows Phone 8.1)** proyectos.</span><span class="sxs-lookup"><span data-stu-id="05083-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="05083-154">Hola `PushClick` método es hello haga clic en controlador de hello **enviar Push** botón.</span><span class="sxs-lookup"><span data-stu-id="05083-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="05083-155">Llama a tootrigger de back-end de hello un tooall notificación dispositivos con una etiqueta de nombre de usuario que coincide con hello `to_tag` parámetro.</span><span class="sxs-lookup"><span data-stu-id="05083-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="05083-156">mensaje de bienvenida de notificación se envía como contenido JSON en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="05083-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="05083-157">Hola `LoginAndRegisterClick` método es hello haga clic en controlador de hello **iniciar sesión y registrar** botón.</span><span class="sxs-lookup"><span data-stu-id="05083-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="05083-158">Almacena basic hello, a continuación, utiliza el token de autenticación en el almacenamiento local (tenga en cuenta que esto representa cualquier token que se utiliza el esquema de autenticación), `RegisterClient` tooregister para notificaciones mediante Hola back-end.</span><span class="sxs-lookup"><span data-stu-id="05083-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. <span data-ttu-id="05083-159">En el Explorador de soluciones, bajo hello **Shared** proyecto, abra hello **App.xaml.cs** archivo.</span><span class="sxs-lookup"><span data-stu-id="05083-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="05083-160">Buscar llamada Hola demasiado`InitNotificationsAsync()` en hello `OnLaunched()` controlador de eventos.</span><span class="sxs-lookup"><span data-stu-id="05083-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="05083-161">Convierta en comentario o eliminar llamada Hola demasiado`InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="05083-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="05083-162">controlador de botón de Hello agregada anteriormente inicializará en registros de notificación.</span><span class="sxs-lookup"><span data-stu-id="05083-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="05083-163">En el Explorador de soluciones, haga clic en hello **Shared** proyecto, a continuación, haga clic en **agregar**y, a continuación, haga clic en **clase**.</span><span class="sxs-lookup"><span data-stu-id="05083-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="05083-164">Nombre de la clase hello **RegisterClient.cs**, a continuación, haga clic en **Aceptar** clase de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="05083-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="05083-165">Esta clase ajustará Hola REST llamadas toocontact necesario Hola aplicación back-end, en orden tooregister las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="05083-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="05083-166">También localmente almacena hello *registrationIds* creado por hello centro de notificaciones como se detalla en [registrar desde su aplicación de back-end](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="05083-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="05083-167">Tenga en cuenta que usa un token de autorización almacenado en almacenamiento local al hacer clic en hello **iniciar sesión y registrar** botón.</span><span class="sxs-lookup"><span data-stu-id="05083-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="05083-168">Agregue los siguiente hello `using` instrucciones al principio de hello del archivo de RegisterClient.cs de hello:</span><span class="sxs-lookup"><span data-stu-id="05083-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="05083-169">Agregar Hola siguiente código dentro de hello `RegisterClient` definición de clase.</span><span class="sxs-lookup"><span data-stu-id="05083-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. <span data-ttu-id="05083-170">Guarde todos los cambios.</span><span class="sxs-lookup"><span data-stu-id="05083-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="05083-171">Probar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="05083-171">Testing hello Application</span></span>
1. <span data-ttu-id="05083-172">Inicie la aplicación hello en Windows 8.1 y Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="05083-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="05083-173">Para Windows Phone 8.1 puede ejecutar la instancia de hello en el emulador de Hola o un dispositivo real.</span><span class="sxs-lookup"><span data-stu-id="05083-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="05083-174">En la instancia de hello Windows 8.1 de la aplicación hello, escriba un **nombre de usuario** y **contraseña** tal y como se muestra en la siguiente pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="05083-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="05083-175">Debe diferir del nombre de usuario de Hola y la contraseña que se especifican en Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="05083-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="05083-176">Haga clic en **Iniciar sesión y registrarse** y compruebe que el cuadro de diálogo se muestre que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="05083-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="05083-177">Esto también le permitirá hello **enviar Push** botón.</span><span class="sxs-lookup"><span data-stu-id="05083-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="05083-178">En la instancia de hello Windows Phone 8.1, escriba una cadena de nombre de usuario con ambos hello **nombre de usuario** y **contraseña** campos, a continuación, haga clic en **inicio de sesión y registrar**.</span><span class="sxs-lookup"><span data-stu-id="05083-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="05083-179">A continuación, en hello **etiqueta de nombre de usuario de destinatario** , escriba el nombre de usuario de hello registrado en Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="05083-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="05083-180">Escriba un mensaje de notificación y haga clic en **Enviar inserción**.</span><span class="sxs-lookup"><span data-stu-id="05083-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="05083-181">Solo los dispositivos de Hola que han registrado con una etiqueta de nombre de usuario coincidente Hola reciban mensaje de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="05083-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="05083-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05083-182">Next Steps</span></span>
* <span data-ttu-id="05083-183">Si desea toosegment los usuarios por grupos de interés, vea [toosend de centros de notificaciones utilice noticias de última hora].</span><span class="sxs-lookup"><span data-stu-id="05083-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="05083-184">toolearn más información acerca de cómo toouse centros de notificaciones, consulte [instrucciones de los centros de notificación].</span><span class="sxs-lookup"><span data-stu-id="05083-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[empezar a trabajar con los centros de notificaciones]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[seguros Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[toosend de centros de notificaciones utilice noticias de última hora]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[instrucciones de los centros de notificación]: http://msdn.microsoft.com/library/jj927170.aspx
