En esta sección, actualizar código en su toosend de proyecto de back-end existente de aplicaciones móviles una notificación de inserción cada vez que se agrega un nuevo elemento. Esto se realiza gracias hello [plantilla](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) característica de centros de notificaciones de Azure, habilitar inserciones de multiplataforma. Hello varios clientes registrados para las notificaciones de inserción mediante plantillas y una inserción universal solo puede obtener tooall plataformas de cliente.

Elija uno de hello siguiendo los procedimientos que corresponda al tipo de proyecto de back-end&mdash;cualquier [back-end de .NET](#dotnet) o [Node.js back-end](#nodejs).

### <a name="dotnet"></a>Proyecto de back-end de .NET
1. En Visual Studio, haga clic en proyecto de servidor de Hola y haga clic en **administrar paquetes de NuGet**. Busque `Microsoft.Azure.NotificationHubs` y, después, haga clic en **Instalar**. Esto instala la biblioteca de centros de notificaciones de Hola para enviar notificaciones desde el back-end.
2. En el proyecto de servidor hello, abra **controladores** > **TodoItemController.cs**y agregue Hola siguientes instrucciones using:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. Hola **PostTodoItem** método, agregar Hola siguiente código después de la llamada de hello demasiado**InsertAsync**:  

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

    Este modo envía una notificación de plantilla que contiene el elemento de saludo. Texto cuando se inserta un nuevo elemento.
4. Volver a publicar el proyecto de servidor de Hola.

### <a name="nodejs"></a>Proyecto de back-end de Node.js
1. Si ya no lo ha hecho, [Descargar proyecto de back-end de inicio rápido de hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), o use otro hello [editor en línea en el portal de Azure hello](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Reemplace el código existente hello en todoitem.js por hello siguiente:

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

    Este modo envía una notificación de plantilla que contiene hello item.text Cuando se inserta un nuevo elemento.
3. Al editar el archivo hello en el equipo local, volver a publicar el proyecto de servidor de Hola.
