<span data-ttu-id="66c6b-101">Use el procedimiento Hola que corresponda al tipo de proyecto de back-end&mdash;cualquier [back-end de .NET](#dotnet) o [Node.js back-end](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="66c6b-101">Use hello procedure that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="66c6b-102"><a name="dotnet"></a>Proyecto de back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="66c6b-102"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="66c6b-103">En Visual Studio, haga clic en proyecto de servidor de Hola y haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="66c6b-103">In Visual Studio, right-click hello server project, and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="66c6b-104">Busque `Microsoft.Azure.NotificationHubs` y, después, haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="66c6b-104">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="66c6b-105">Esto instala la biblioteca de cliente de hello centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="66c6b-105">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="66c6b-106">En la carpeta de controladores de hello, abra TodoItemController.cs y agregue la siguiente hello `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="66c6b-106">In hello Controllers folder, open TodoItemController.cs and add hello following `using` statements:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. <span data-ttu-id="66c6b-107">Reemplace hello `PostTodoItem` método con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="66c6b-107">Replace hello `PostTodoItem` method with hello following code:</span></span>  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
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

            // Android payload
            var androidNotificationPayload = "{ \"data\" : {\"message\":\"" + item.Text + "\"}}";

            try
            {
                // Send hello push notification and log hello results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write hello success result toohello logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write hello failure result toohello logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. <span data-ttu-id="66c6b-108">Volver a publicar el proyecto de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="66c6b-108">Republish hello server project.</span></span>

### <span data-ttu-id="66c6b-109"><a name="nodejs"></a>Proyecto de back-end de Node.js</span><span class="sxs-lookup"><span data-stu-id="66c6b-109"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="66c6b-110">Si ya no lo ha hecho, [Descargar proyecto de inicio rápido de hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), o use otro hello [editor en línea en el portal de Azure hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="66c6b-110">If you haven't already done so, [download hello quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="66c6b-111">Reemplace el código existente en archivo de hello todoitem.js de Hola por hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="66c6b-111">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a GCM native notification.
                    context.push.gcm.send(null, payload, function (error) {
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

    <span data-ttu-id="66c6b-112">Este modo envía una notificación de GCM que contiene hello item.text Cuando se inserta un nuevo elemento de lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="66c6b-112">This sends a GCM notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="66c6b-113">Al editar el archivo hello en el equipo local, volver a publicar el proyecto de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="66c6b-113">When editing hello file in your local computer, republish hello server project.</span></span>
