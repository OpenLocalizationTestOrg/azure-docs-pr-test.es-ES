
* <span data-ttu-id="c2762-101">**Back-end de .NET (C#)**:</span><span class="sxs-lookup"><span data-stu-id="c2762-101">**.NET backend (C#)**:</span></span>      
  
  1. <span data-ttu-id="c2762-102">En Visual Studio, haga clic en proyecto de servidor de Hola y haga clic en **administrar paquetes de NuGet**, busque `Microsoft.Azure.NotificationHubs`, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="c2762-102">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.NotificationHubs`, then click **Install**.</span></span> <span data-ttu-id="c2762-103">Esto instala la biblioteca de centros de notificaciones de Hola para enviar notificaciones desde el back-end.</span><span class="sxs-lookup"><span data-stu-id="c2762-103">This installs hello Notification Hubs library for sending notifications from your backend.</span></span>
  2. <span data-ttu-id="c2762-104">En el proyecto de Visual Studio de hello back-end, abra **controladores** > **TodoItemController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c2762-104">In hello backend's Visual Studio project, open **Controllers** > **TodoItemController.cs**.</span></span> <span data-ttu-id="c2762-105">Hola parte superior de archivo hello, agregue el siguiente de hello `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="c2762-105">At hello top of hello file, add hello following `using` statement:</span></span>
     
          using Microsoft.Azure.Mobile.Server.Config;
          using Microsoft.Azure.NotificationHubs;

    3. <span data-ttu-id="c2762-106">Reemplace hello `PostTodoItem` método con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="c2762-106">Replace hello `PostTodoItem` method with hello following code:</span></span>  

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

                // iOS payload
                var appleNotificationPayload = "{\"aps\":{\"alert\":\"" + item.Text + "\"}}";

                try
                {
                    // Send hello push notification and log hello results.
                    var result = await hub.SendAppleNativeNotificationAsync(appleNotificationPayload);

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

    4. <span data-ttu-id="c2762-107">Volver a publicar el proyecto de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2762-107">Republish hello server project.</span></span>

* <span data-ttu-id="c2762-108">**Back-end de Node.js** :</span><span class="sxs-lookup"><span data-stu-id="c2762-108">**Node.js backend** :</span></span> 
  
  1. <span data-ttu-id="c2762-109">Si ya no lo ha hecho, [Descargar proyecto de inicio rápido de hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) o persona use hello [editor en línea en el portal de Azure hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="c2762-109">If you haven't already done so, [download hello quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>    
  2. <span data-ttu-id="c2762-110">Reemplace el script de Hola todoitem.js tabla con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="c2762-110">Replace hello todoitem.js table script with hello following code:</span></span>

            var azureMobileApps = require('azure-mobile-apps'),
                promises = require('azure-mobile-apps/src/utilities/promises'),
                logger = require('azure-mobile-apps/src/logger');

            var table = azureMobileApps.table();

            // When adding record, send a push notification via APNS
            table.insert(function (context) {
                // For details of hello Notification Hubs JavaScript SDK, 
                // see http://aka.ms/nodejshubs
                logger.info('Running TodoItem.insert');

                // Create a payload that contains hello new item Text.
                var payload = "{\"aps\":{\"alert\":\"" + context.item.text + "\"}}";

                // Execute hello insert; Push as a post-execute action when results are returned as a Promise.
                return context.execute()
                    .then(function (results) {
                        // Only do hello push if configured
                        if (context.push) {
                            context.push.apns.send(null, payload, function (error) {
                                if (error) {
                                    logger.error('Error while sending push notification: ', error);
                                } else {
                                    logger.info('Push notification sent successfully!');
                                }
                            });
                        }
                        return results;
                    })
                    .catch(function (error) {
                        logger.error('Error while running context.execute: ', error);
                    });
            });

            module.exports = table;

    2. <span data-ttu-id="c2762-111">Al editar el archivo hello en el equipo local, volver a publicar el proyecto de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2762-111">When editing hello file on your local computer, republish hello server project.</span></span>
