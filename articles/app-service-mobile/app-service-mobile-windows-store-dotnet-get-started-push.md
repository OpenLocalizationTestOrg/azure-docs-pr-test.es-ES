---
title: "Incorporación de notificaciones push a una aplicación de la Plataforma universal de Windows (UWP) | Microsoft Docs"
description: "Obtenga información acerca de cómo usar Aplicaciones móviles del Servicio de aplicaciones de Azure y Centros de notificaciones de Azure para enviar notificaciones push a la aplicación de la Plataforma universal de Windows (UWP)."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: a14bb0320c1f6a563f766a6a0fad5cf556fe7b70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="93419-103">Incorporación de notificaciones push a la aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="93419-103">Add push notifications to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="93419-104">Información general</span><span class="sxs-lookup"><span data-stu-id="93419-104">Overview</span></span>
<span data-ttu-id="93419-105">En este tutorial, agregará notificaciones de inserción al proyecto de [inicio rápido de Windows](app-service-mobile-windows-store-dotnet-get-started.md) para que cada vez que se envíe una notificación de inserción al dispositivo, se inserte un registro.</span><span class="sxs-lookup"><span data-stu-id="93419-105">In this tutorial, you add push notifications to the [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="93419-106">Si no usa el proyecto de servidor de inicio rápido descargado, necesitará el paquete de extensión de la notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="93419-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="93419-107">Vea [Trabajar con el SDK de servidor de back-end de .NET para Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="93419-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="93419-108"><a name="configure-hub"></a>Configurar un Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="93419-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="93419-109">Registro de la aplicación para notificaciones push</span><span class="sxs-lookup"><span data-stu-id="93419-109">Register your app for push notifications</span></span>
<span data-ttu-id="93419-110">Debe enviar la aplicación a la Tienda Windows y, después, configurar el proyecto de servidor para integrarlo con los Servicios de notificaciones de Windows (WNS) para enviar la inserción.</span><span class="sxs-lookup"><span data-stu-id="93419-110">You need to submit your app to the Windows Store, then configure your server project to integrate with Windows Notification Services (WNS) to send push.</span></span>

1. <span data-ttu-id="93419-111">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto de aplicación UWP y luego haga clic en **Tienda** > **Asociar aplicación con la Tienda...**.</span><span class="sxs-lookup"><span data-stu-id="93419-111">In Visual Studio Solution Explorer, right-click the UWP app project, click **Store** > **Associate App with the Store...**.</span></span>

    ![Asociar aplicación con la Tienda Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="93419-113">En el asistente, haga clic en **Siguiente**, inicie sesión con su cuenta Microsoft, escriba un nombre para la aplicación en **Reserve un nuevo nombre de aplicación** y haga clic en **Reservar**.</span><span class="sxs-lookup"><span data-stu-id="93419-113">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="93419-114">Después de crear correctamente el registro de la aplicación, seleccione el nuevo nombre de la aplicación, haga clic en **Siguiente** y, después, en **Asociar**.</span><span class="sxs-lookup"><span data-stu-id="93419-114">After the app registration is successfully created, select the new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="93419-115">Se agrega la información de registro necesaria de la Tienda Windows al manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="93419-115">This adds the required Windows Store registration information to the application manifest.</span></span>  
4. <span data-ttu-id="93419-116">Navegue al [Centro de desarrollo de Windows](https://dev.windows.com/en-us/overview), inicie sesión con su cuenta Microsoft, haga clic en el nuevo registro de aplicación en **Mis aplicaciones** y, luego, expanda **Servicios** > **Notificaciones push**.</span><span class="sxs-lookup"><span data-stu-id="93419-116">Navigate to the [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click the new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="93419-117">En la página **Notificaciones push**, haga clic en el **sitio de Servicios Live** en **Microsoft Azure Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="93419-117">In the **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="93419-118">En la página de registro, anote los valores de **Secretos de aplicación** y **SID del paquete**, que va a utilizar a continuación para configurar el back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="93419-118">In the registration page, make a note of the value under **Application secrets** and the **Package SID**, which you will next use to configure your mobile app backend.</span></span>

    ![Asociar aplicación con la Tienda Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="93419-120">El secreto de cliente y el SID del paquete son credenciales de seguridad importantes.</span><span class="sxs-lookup"><span data-stu-id="93419-120">The client secret and package SID are important security credentials.</span></span> <span data-ttu-id="93419-121">No los comparta con nadie ni los distribuya con su aplicación.</span><span class="sxs-lookup"><span data-stu-id="93419-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="93419-122">El **Id. de aplicación** se usa con el secreto para configurar la autenticación de la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93419-122">The **Application Id** is used with the secret to configure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-the-backend-to-send-push-notifications"></a><span data-ttu-id="93419-123">Configuración del back-end para enviar notificaciones push</span><span class="sxs-lookup"><span data-stu-id="93419-123">Configure the backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="93419-124"><a id="update-service"></a>Actualización del servidor para enviar notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="93419-124"><a id="update-service"></a>Update the server to send push notifications</span></span>
<span data-ttu-id="93419-125">Use uno de los procedimientos siguientes que se ajusten al tipo de proyecto de back-end&mdash;: [back-end de .NET](#dotnet) o [back-end de Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="93419-125">Use the procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="93419-126"><a name="dotnet"></a>Proyecto de back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="93419-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="93419-127">En Visual Studio, haga clic con el botón derecho en el proyecto de servidor, haga clic en **Administrar paquetes NuGet**, busque Microsoft.Azure.NotificationHubs y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="93419-127">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="93419-128">Esto instala la biblioteca de cliente de Centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="93419-128">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="93419-129">Expanda **Controladores**, abra TodoItemController.cs y agregue las siguientes instrucciones using:</span><span class="sxs-lookup"><span data-stu-id="93419-129">Expand **Controllers**, open TodoItemController.cs, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="93419-130">En el método **PostTodoItem**, agregue el código siguiente después de la llamada a **InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="93419-130">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create the notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send the push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="93419-131">Este código indica al centro de notificaciones que envíe una notificación push después de la inserción de un elemento nuevo.</span><span class="sxs-lookup"><span data-stu-id="93419-131">This code tells the notification hub to send a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="93419-132">Vuelva a publicar el proyecto de servidor.</span><span class="sxs-lookup"><span data-stu-id="93419-132">Republish the server project.</span></span>

### <span data-ttu-id="93419-133"><a name="nodejs"></a>Proyecto de back-end de Node.js</span><span class="sxs-lookup"><span data-stu-id="93419-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="93419-134">Si aún no lo ha hecho, [descargue el proyecto de inicio rápido](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) o utilice el [editor en línea de Azure Portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="93419-134">If you haven't already done so, [download the quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="93419-135">Reemplace el código existente en el archivo todoitem.js por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="93419-135">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the WNS payload that contains the new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="93419-136">Esta acción envía una notificación del sistema de WNS que contiene el item.text cuando se inserta un nuevo elemento todo.</span><span class="sxs-lookup"><span data-stu-id="93419-136">This sends a WNS toast notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="93419-137">Cuando edite el archivo en el equipo local, vuelva a publicar el proyecto de servidor.</span><span class="sxs-lookup"><span data-stu-id="93419-137">When editing the file on your local computer, republish the server project.</span></span>

## <span data-ttu-id="93419-138"><a id="update-app"></a>Incorporación de notificaciones de inserción a la aplicación</span><span class="sxs-lookup"><span data-stu-id="93419-138"><a id="update-app"></a>Add push notifications to your app</span></span>
<span data-ttu-id="93419-139">Después, debe registrarse la aplicación para recibir notificaciones push en el inicio.</span><span class="sxs-lookup"><span data-stu-id="93419-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="93419-140">Cuando tenga habilitada la autenticación, asegúrese de que el usuario inicia sesión antes de intentar registrarse para recibir notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="93419-140">When you have already enabled authentication, make sure that the user signs-in before trying to register for push notifications.</span></span>

1. <span data-ttu-id="93419-141">Abra el archivo de proyecto **App.xaml.cs** y agregue las siguientes instrucciones `using`:</span><span class="sxs-lookup"><span data-stu-id="93419-141">Open the **App.xaml.cs** project file and add the following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="93419-142">En el mismo archivo, agregue la siguiente definición del método **InitNotificationsAsync** a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="93419-142">In the same file, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register the channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="93419-143">Este código recupera el valor de ChannelURI de la aplicación desde WNS y, a continuación, lo registra con sus Aplicaciones móviles del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="93419-143">This code retrieves the ChannelURI for the app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="93419-144">En la parte superior del controlador de eventos **OnLaunched**, en **App.xaml.cs**, agregue el modificador **async** a la definición del método y agregue la siguiente llamada al nuevo método **InitNotificationsAsync**, como se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="93419-144">At the top of the **OnLaunched** event handler in **App.xaml.cs**, add the **async** modifier to the method definition and add the following call to the new **InitNotificationsAsync** method, as in the following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="93419-145">Esto garantiza que el valor de ChannelURI de corta duración se registra cada vez que se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="93419-145">This guarantees that the short-lived ChannelURI is registered each time the application is launched.</span></span>
4. <span data-ttu-id="93419-146">Recompile el proyecto de aplicación para UWP.</span><span class="sxs-lookup"><span data-stu-id="93419-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="93419-147">La carpeta ahora ya está lista para recibir notificaciones.</span><span class="sxs-lookup"><span data-stu-id="93419-147">Your app is now ready to receive toast notifications.</span></span>

## <span data-ttu-id="93419-148"><a id="test"></a>Prueba de las notificaciones push en su aplicación</span><span class="sxs-lookup"><span data-stu-id="93419-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="93419-149"><a id="more"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="93419-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="93419-150">Más información sobre las notificaciones de inserción:</span><span class="sxs-lookup"><span data-stu-id="93419-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="93419-151">Uso del cliente administrado para Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="93419-151">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="93419-152">: las plantillas proporcionan flexibilidad para enviar inserciones multiplataforma e inserciones localizadas.</span><span class="sxs-lookup"><span data-stu-id="93419-152">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="93419-153">Sepa cómo registrar plantillas.</span><span class="sxs-lookup"><span data-stu-id="93419-153">Learn how to register templates.</span></span>
* [<span data-ttu-id="93419-154">Diagnosticar problemas de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="93419-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="93419-155">: existen varias razones para que las notificaciones se pierdan o no lleguen a los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="93419-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="93419-156">En este tema se muestra cómo analizar y descubrir la causa principal de los errores de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="93419-156">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="93419-157">También podría continuar con uno de los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="93419-157">Consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="93419-158">Incorporación de la autenticación a la aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="93419-158">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="93419-159">: aprenda a autenticar a los usuarios de su aplicación con un proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="93419-159">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="93419-160">Activación de la sincronización sin conexión para la aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="93419-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="93419-161">: aprenda a agregar compatibilidad sin conexión a su aplicación con un back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="93419-161">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="93419-162">La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil (ver, agregar o modificar datos) aun cuando no haya conexión de red.</span><span class="sxs-lookup"><span data-stu-id="93419-162">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
