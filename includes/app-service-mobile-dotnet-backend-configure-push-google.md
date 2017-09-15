<span data-ttu-id="2485b-101">Use el procedimiento que se ajuste al tipo de proyecto de back-end&mdash;: [back-end de .NET](#dotnet) o [back-end de Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="2485b-101">Use the procedure that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="2485b-102"><a name="dotnet"></a>Proyecto de back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="2485b-102"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="2485b-103">En Visual Studio, haga clic con el botón derecho en el proyecto de servidor, haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2485b-103">In Visual Studio, right-click the server project, and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="2485b-104">Busque `Microsoft.Azure.NotificationHubs` y, después, haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="2485b-104">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="2485b-105">Esto instala la biblioteca de cliente de Centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="2485b-105">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="2485b-106">En la carpeta Controladores, abra TodoItemController.cs y agregue las siguientes instrucciones `using` :</span><span class="sxs-lookup"><span data-stu-id="2485b-106">In the Controllers folder, open TodoItemController.cs and add the following `using` statements:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. <span data-ttu-id="2485b-107">Reemplace el método `PostTodoItem` por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="2485b-107">Replace the `PostTodoItem` method with the following code:</span></span>  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
            // Get the settings for the server project.
            HttpConfiguration config = this.Configuration;

            MobileAppSettingsDictionary settings =
                this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

            // Get the Notification Hubs credentials for the Mobile App.
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
                // Send the push notification and log the results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write the success result to the logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write the failure result to the logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. <span data-ttu-id="2485b-108">Vuelva a publicar el proyecto de servidor.</span><span class="sxs-lookup"><span data-stu-id="2485b-108">Republish the server project.</span></span>

### <span data-ttu-id="2485b-109"><a name="nodejs"></a>Proyecto de back-end de Node.js</span><span class="sxs-lookup"><span data-stu-id="2485b-109"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="2485b-110">Si aún no lo ha hecho, [descargue el proyecto de inicio rápido](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) o utilice el [editor en línea de Azure Portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="2485b-110">If you haven't already done so, [download the quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="2485b-111">Reemplace el código existente en el archivo todoitem.js por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2485b-111">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;  

    <span data-ttu-id="2485b-112">Esta acción envía una notificación de GCM que contiene el item.text cuando se inserta un nuevo elemento todo.</span><span class="sxs-lookup"><span data-stu-id="2485b-112">This sends a GCM notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="2485b-113">Cuando edite el archivo en el equipo local, vuelva a publicar el proyecto de servidor.</span><span class="sxs-lookup"><span data-stu-id="2485b-113">When editing the file in your local computer, republish the server project.</span></span>
