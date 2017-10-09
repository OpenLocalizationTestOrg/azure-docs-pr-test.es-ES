<span data-ttu-id="1b7b4-101">En esta sección, actualizar código en su toosend de proyecto de back-end existente de aplicaciones móviles una notificación de inserción cada vez que se agrega un nuevo elemento.</span><span class="sxs-lookup"><span data-stu-id="1b7b4-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="1b7b4-102">Esto se realiza gracias hello [plantilla](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) característica de centros de notificaciones de Azure, habilitar inserciones de multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="1b7b4-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="1b7b4-103">Hello varios clientes registrados para las notificaciones de inserción mediante plantillas y una inserción universal solo puede obtener tooall plataformas de cliente.</span><span class="sxs-lookup"><span data-stu-id="1b7b4-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="1b7b4-104">Elija uno de hello siguiendo los procedimientos que corresponda al tipo de proyecto de back-end&mdash;cualquier [back-end de .NET](#dotnet) o [Node.js back-end](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="1b7b4-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="1b7b4-105"><a name="dotnet"></a>Proyecto de back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="1b7b4-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="1b7b4-106">En Visual Studio, haga clic en proyecto de servidor de Hola y haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1b7b4-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="1b7b4-107">Busque `Microsoft.Azure.NotificationHubs` y, después, haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="1b7b4-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="1b7b4-108">Esto instala la biblioteca de centros de notificaciones de Hola para enviar notificaciones desde el back-end.</span><span class="sxs-lookup"><span data-stu-id="1b7b4-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="1b7b4-109">En el proyecto de servidor hello, abra **controladores** > **TodoItemController.cs**y agregue Hola siguientes instrucciones using:</span><span class="sxs-lookup"><span data-stu-id="1b7b4-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="1b7b4-110">Hola **PostTodoItem** método, agregar Hola siguiente código después de la llamada de hello demasiado**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="1b7b4-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="1b7b4-111">Este modo envía una notificación de plantilla que contiene el elemento de saludo. Texto cuando se inserta un nuevo elemento.</span><span class="sxs-lookup"><span data-stu-id="1b7b4-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="1b7b4-112">Volver a publicar el proyecto de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b7b4-112">Republish hello server project.</span></span>

### <span data-ttu-id="1b7b4-113"><a name="nodejs"></a>Proyecto de back-end de Node.js</span><span class="sxs-lookup"><span data-stu-id="1b7b4-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="1b7b4-114">Si ya no lo ha hecho, [Descargar proyecto de back-end de inicio rápido de hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), o use otro hello [editor en línea en el portal de Azure hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="1b7b4-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="1b7b4-115">Reemplace el código existente hello en todoitem.js por hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b7b4-115">Replace hello existing code in todoitem.js with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
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

    <span data-ttu-id="1b7b4-116">Este modo envía una notificación de plantilla que contiene hello item.text Cuando se inserta un nuevo elemento.</span><span class="sxs-lookup"><span data-stu-id="1b7b4-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="1b7b4-117">Al editar el archivo hello en el equipo local, volver a publicar el proyecto de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b7b4-117">When editing hello file on your local computer, republish hello server project.</span></span>
