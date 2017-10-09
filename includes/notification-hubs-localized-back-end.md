



Cuando se envían notificaciones de plantilla que solo necesita tooprovide un conjunto de propiedades, en nuestro caso enviaremos conjunto Hola de propiedades que contienen versiones localizadas de Hola de noticias de hello actual, por ejemplo:

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


Esta sección se muestra cómo las notificaciones de toosend desde una aplicación de consola

Hola incluía código difusiones tooboth Windows almacén y dispositivos iOS, puesto que Hola back-end puede difundir tooany de dispositivos de hello admitida.

### <a name="toosend-notifications-using-a-c-console-app"></a>notificaciones de toosend mediante una aplicación de consola de C#
Modificar hello `SendTemplateNotificationAsync` método de aplicación de consola de hello creado previamente con el siguiente código de hello. Observe cómo en este caso no hay ninguna necesidad de toosend varias notificaciones para distintas configuraciones regionales y plataformas.

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


Tenga en cuenta que esta llamada simple cumplirán lo fragmento localizada de Hola de noticias demasiado**todos los** los dispositivos, independientemente de la plataforma de hello, como el centro de notificaciones genera y entrega Hola correcto de dispositivos de carga nativo tooall Hola suscrito tooa etiqueta específica.

### <a name="sending-hello-notification-with-mobile-services"></a>Enviar notificación de hello con servicios móviles
En el programador de servicio móvil, puede utilizar Hola siguiente secuencia de comandos:

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });


