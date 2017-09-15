



<span data-ttu-id="8f3eb-101">Cuando envía notificaciones de plantilla, solo es necesario proporcionar un conjunto de propiedades; en nuestro caso, enviaremos, por ejemplo, el conjunto de propiedades que contiene la versión localizada de las noticias de actualidad:</span><span class="sxs-lookup"><span data-stu-id="8f3eb-101">When you send template notifications you only need to provide a set of properties, in our case we will send the set of properties containing the localized version of the current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="8f3eb-102">En esta sección se muestra cómo enviar notificaciones con una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="8f3eb-102">This section shows how to send notifications using a console app</span></span>

<span data-ttu-id="8f3eb-103">El código incluido se difunde tanto a los dispositivos de la Tienda Windows como a los iOS, dado que el back-end puede difundir a cualquiera de los dispositivos compatibles.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-103">The included code broadcasts to both Windows Store and iOS devices, since the backend can broadcast to any of the supported devices.</span></span>

### <a name="to-send-notifications-using-a-c-console-app"></a><span data-ttu-id="8f3eb-104">Para enviar notificaciones mediante una aplicación de consola de C#</span><span class="sxs-lookup"><span data-stu-id="8f3eb-104">To send notifications using a C# console app</span></span>
<span data-ttu-id="8f3eb-105">Modifique el método `SendTemplateNotificationAsync` en la aplicación de consola que creó anteriormente con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-105">Modify the `SendTemplateNotificationAsync` method in the console app you previously created with the following code.</span></span> <span data-ttu-id="8f3eb-106">Observe cómo en este caso no hay necesidad de enviar varias notificaciones para diferentes configuraciones regionales y plataformas.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-106">Notice how in this case there is no need to send multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending the notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and the proper tags will receive the notifications. 
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


<span data-ttu-id="8f3eb-107">Tenga en cuenta que esta simple llamada entregará la noticia localizada a **todos** los dispositivos, con independencia de la plataforma, puesto que el Centro de notificaciones crea y entrega la carga nativa correcta a todos los dispositivos suscritos a una etiqueta específica.</span><span class="sxs-lookup"><span data-stu-id="8f3eb-107">Note that this simple call will deliver the localized piece of news to **all** your devices, irrespective of the platform, as your Notification Hub builds and delivers the correct native payload to all the devices subscribed to a specific tag.</span></span>

### <a name="sending-the-notification-with-mobile-services"></a><span data-ttu-id="8f3eb-108">Envío de la notificación con Servicios móviles</span><span class="sxs-lookup"><span data-stu-id="8f3eb-108">Sending the notification with Mobile Services</span></span>
<span data-ttu-id="8f3eb-109">En el programador de servicios móviles, puede usar el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="8f3eb-109">In your Mobile Service scheduler, you can use the following script:</span></span>

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


