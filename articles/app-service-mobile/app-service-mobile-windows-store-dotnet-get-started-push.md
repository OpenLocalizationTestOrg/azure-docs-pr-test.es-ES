---
title: "aplicación de plataforma Universal de Windows (UWP) de aaaAdd inserción notificaciones tooyour | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse aplicaciones de Mobile de servicio de aplicación de Azure y los centros de notificaciones de Azure toosend push notificaciones tooyour plataforma Universal de Windows (UWP) aplicaciones."
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
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="a9f70-103">Agregar aplicación de Windows de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="a9f70-103">Add push notifications tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="a9f70-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a9f70-104">Overview</span></span>
<span data-ttu-id="a9f70-105">En este tutorial, agregará toohello de notificaciones de inserción [inicio rápido de Windows](app-service-mobile-windows-store-dotnet-get-started.md) del proyecto para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.</span><span class="sxs-lookup"><span data-stu-id="a9f70-105">In this tutorial, you add push notifications toohello [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="a9f70-106">Si no usa Hola descarga el proyecto de servidor de inicio rápido, se necesita Hola paquete de extensión de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="a9f70-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="a9f70-107">Vea [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a9f70-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="a9f70-108"><a name="configure-hub"></a>Configurar un Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="a9f70-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="a9f70-109">Registro de la aplicación para notificaciones push</span><span class="sxs-lookup"><span data-stu-id="a9f70-109">Register your app for push notifications</span></span>
<span data-ttu-id="a9f70-110">Se necesita toosubmit su toohello aplicación tienda Windows, después de configura su toointegrate de project server con servicios de notificación de Windows (WNS) toosend inserción.</span><span class="sxs-lookup"><span data-stu-id="a9f70-110">You need toosubmit your app toohello Windows Store, then configure your server project toointegrate with Windows Notification Services (WNS) toosend push.</span></span>

1. <span data-ttu-id="a9f70-111">En Visual Studio Solution Explorer, el proyecto de aplicación UWP de Hola de menú contextual, haga clic en **almacén** > **asociar aplicación con hello almacén...** .</span><span class="sxs-lookup"><span data-stu-id="a9f70-111">In Visual Studio Solution Explorer, right-click hello UWP app project, click **Store** > **Associate App with hello Store...**.</span></span>

    ![Asociar aplicación con la Tienda Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="a9f70-113">En el Asistente de hello, haga clic en **siguiente**, inicie sesión con su cuenta de Microsoft, escriba un nombre para la aplicación en **reservar un nuevo nombre de aplicación**, a continuación, haga clic en **reserva**.</span><span class="sxs-lookup"><span data-stu-id="a9f70-113">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="a9f70-114">Después de registro de una aplicación Hola es Hola se creó correctamente, seleccione Nuevo nombre de aplicación, haga clic en **siguiente**y, a continuación, haga clic en **asociar**.</span><span class="sxs-lookup"><span data-stu-id="a9f70-114">After hello app registration is successfully created, select hello new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="a9f70-115">Esto agrega manifiesto de aplicación Hola necesario tienda Windows registro información toohello.</span><span class="sxs-lookup"><span data-stu-id="a9f70-115">This adds hello required Windows Store registration information toohello application manifest.</span></span>  
4. <span data-ttu-id="a9f70-116">Navegue toohello [centro de desarrollo de Windows](https://dev.windows.com/en-us/overview), iniciar sesión con tu cuenta de Microsoft, haga clic en nuevo registro de aplicación hello en **mis aplicaciones**, a continuación, expanda **servicios**  >  **Notificaciones de inserción**.</span><span class="sxs-lookup"><span data-stu-id="a9f70-116">Navigate toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click hello new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="a9f70-117">Hola **notificaciones de inserción** página, haga clic en **sitio de los servicios de Live** en **servicios móviles de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="a9f70-117">In hello **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="a9f70-118">En la página de registro de hello, tome nota del valor de hello en **secretos de aplicación** hello y **SID del paquete**, que a continuación utilizará tooconfigure su aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="a9f70-118">In hello registration page, make a note of hello value under **Application secrets** and hello **Package SID**, which you will next use tooconfigure your mobile app backend.</span></span>

    ![Asociar aplicación con la Tienda Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="a9f70-120">secreto de cliente de Hola y el SID del paquete son credenciales de seguridad importantes.</span><span class="sxs-lookup"><span data-stu-id="a9f70-120">hello client secret and package SID are important security credentials.</span></span> <span data-ttu-id="a9f70-121">No los comparta con nadie ni los distribuya con su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9f70-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="a9f70-122">Hola **Id. de aplicación** se utiliza con la autenticación de Microsoft Account de hello tooconfigure secreto.</span><span class="sxs-lookup"><span data-stu-id="a9f70-122">hello **Application Id** is used with hello secret tooconfigure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a><span data-ttu-id="a9f70-123">Configurar notificaciones de inserción de hello back-end toosend</span><span class="sxs-lookup"><span data-stu-id="a9f70-123">Configure hello backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="a9f70-124"><a id="update-service"></a>Actualizar notificaciones de inserción de hello server toosend</span><span class="sxs-lookup"><span data-stu-id="a9f70-124"><a id="update-service"></a>Update hello server toosend push notifications</span></span>
<span data-ttu-id="a9f70-125">Utilice Hola procedimiento siguiente que corresponda al tipo de proyecto de back-end&mdash;cualquier [back-end de .NET](#dotnet) o [Node.js back-end](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="a9f70-125">Use hello procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="a9f70-126"><a name="dotnet"></a>Proyecto de back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="a9f70-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="a9f70-127">En Visual Studio, haga clic en proyecto de servidor de Hola y haga clic en **administrar paquetes de NuGet**, busque Microsoft.Azure.NotificationHubs, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="a9f70-127">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="a9f70-128">Esto instala la biblioteca de cliente de hello centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="a9f70-128">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="a9f70-129">Expanda **controladores**, abra TodoItemController.cs y agregue Hola siguientes instrucciones using:</span><span class="sxs-lookup"><span data-stu-id="a9f70-129">Expand **Controllers**, open TodoItemController.cs, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="a9f70-130">Hola **PostTodoItem** método, agregar Hola siguiente código después de la llamada de hello demasiado**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="a9f70-130">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="a9f70-131">Este código indica una notificación de inserción de toosend de concentrador de notificación de Hola después de un nuevo elemento de inserción.</span><span class="sxs-lookup"><span data-stu-id="a9f70-131">This code tells hello notification hub toosend a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="a9f70-132">Volver a publicar el proyecto de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9f70-132">Republish hello server project.</span></span>

### <span data-ttu-id="a9f70-133"><a name="nodejs"></a>Proyecto de back-end de Node.js</span><span class="sxs-lookup"><span data-stu-id="a9f70-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="a9f70-134">Si ya no lo ha hecho, [Descargar proyecto de inicio rápido de hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) o persona use hello [editor en línea en el portal de Azure hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="a9f70-134">If you haven't already done so, [download hello quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="a9f70-135">Reemplace el código existente en archivo de hello todoitem.js de Hola por hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="a9f70-135">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
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
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="a9f70-136">Este modo envía una notificación de WNS que contiene hello item.text Cuando se inserta un nuevo elemento de lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="a9f70-136">This sends a WNS toast notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="a9f70-137">Al editar el archivo hello en el equipo local, volver a publicar el proyecto de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9f70-137">When editing hello file on your local computer, republish hello server project.</span></span>

## <span data-ttu-id="a9f70-138"><a id="update-app"></a>Agregar aplicación de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="a9f70-138"><a id="update-app"></a>Add push notifications tooyour app</span></span>
<span data-ttu-id="a9f70-139">Después, debe registrarse la aplicación para recibir notificaciones push en el inicio.</span><span class="sxs-lookup"><span data-stu-id="a9f70-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="a9f70-140">Si ya se ha habilitado la autenticación, asegúrese de que ese Hola usuario inicia sesión antes de intentar tooregister para las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="a9f70-140">When you have already enabled authentication, make sure that hello user signs-in before trying tooregister for push notifications.</span></span>

1. <span data-ttu-id="a9f70-141">Abra hello **App.xaml.cs** archivo de proyecto y agregue el siguiente de hello `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="a9f70-141">Open hello **App.xaml.cs** project file and add hello following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="a9f70-142">En Hola el mismo archivo, agregue la siguiente hello **InitNotificationsAsync** toohello de definición de método **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="a9f70-142">In hello same file, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="a9f70-143">Este código recupera hello URI del canal para la aplicación hello de WNS y, a continuación, registra ese URI del canal con la aplicación de servicio de aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="a9f70-143">This code retrieves hello ChannelURI for hello app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="a9f70-144">En parte superior de Hola de hello **OnLaunched** controlador de eventos de **App.xaml.cs**, agregar hello **async** definición de método de modificador toohello y agregue el siguiente de hello llamada toohello nueva  **InitNotificationsAsync** método, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="a9f70-144">At hello top of hello **OnLaunched** event handler in **App.xaml.cs**, add hello **async** modifier toohello method definition and add hello following call toohello new **InitNotificationsAsync** method, as in hello following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="a9f70-145">Esto garantiza que hello que channeluri de corta duración se registra cada vez que se inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a9f70-145">This guarantees that hello short-lived ChannelURI is registered each time hello application is launched.</span></span>
4. <span data-ttu-id="a9f70-146">Recompile el proyecto de aplicación para UWP.</span><span class="sxs-lookup"><span data-stu-id="a9f70-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="a9f70-147">La aplicación ya está listo tooreceive recibir notificaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="a9f70-147">Your app is now ready tooreceive toast notifications.</span></span>

## <span data-ttu-id="a9f70-148"><a id="test"></a>Prueba de las notificaciones de inserción en su aplicación</span><span class="sxs-lookup"><span data-stu-id="a9f70-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="a9f70-149"><a id="more"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9f70-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="a9f70-150">Más información sobre las notificaciones de inserción:</span><span class="sxs-lookup"><span data-stu-id="a9f70-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="a9f70-151">Cómo toouse Hola administra a cliente para aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="a9f70-151">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="a9f70-152">Plantillas de proporcionan inserciones de flexibilidad toosend multiplataforma e inserciones localizados.</span><span class="sxs-lookup"><span data-stu-id="a9f70-152">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="a9f70-153">Obtenga información acerca de cómo tooregister plantillas.</span><span class="sxs-lookup"><span data-stu-id="a9f70-153">Learn how tooregister templates.</span></span>
* [<span data-ttu-id="a9f70-154">Diagnosticar problemas de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="a9f70-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="a9f70-155">: existen varias razones para que las notificaciones se pierdan o no lleguen a los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a9f70-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="a9f70-156">Este tema muestra cómo hacer que tooanalyze y averiguar la raíz de Hola de errores de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="a9f70-156">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="a9f70-157">Considere la posibilidad de continuar en tooone de hello tutoriales:</span><span class="sxs-lookup"><span data-stu-id="a9f70-157">Consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="a9f70-158">Agregar aplicación de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="a9f70-158">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="a9f70-159">Obtenga información acerca de cómo tooauthenticate a los usuarios de la aplicación con un proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="a9f70-159">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="a9f70-160">Habilitación de la sincronización sin conexión para su aplicación</span><span class="sxs-lookup"><span data-stu-id="a9f70-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="a9f70-161">Obtenga información acerca de cómo tooadd sin conexión son compatibles con la aplicación con un aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="a9f70-161">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="a9f70-162">Sincronización sin conexión permite a los usuarios finales toointeract con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;incluso cuando no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="a9f70-162">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
