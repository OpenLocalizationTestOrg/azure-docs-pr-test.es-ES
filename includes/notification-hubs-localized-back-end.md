



<span data-ttu-id="33b50-101">Cuando se envían notificaciones de plantilla que solo necesita tooprovide un conjunto de propiedades, en nuestro caso enviaremos conjunto Hola de propiedades que contienen versiones localizadas de Hola de noticias de hello actual, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="33b50-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="33b50-102">Esta sección se muestra cómo las notificaciones de toosend desde una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="33b50-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="33b50-103">Hola incluía código difusiones tooboth Windows almacén y dispositivos iOS, puesto que Hola back-end puede difundir tooany de dispositivos de hello admitida.</span><span class="sxs-lookup"><span data-stu-id="33b50-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="33b50-104">notificaciones de toosend mediante una aplicación de consola de C#</span><span class="sxs-lookup"><span data-stu-id="33b50-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="33b50-105">Modificar hello `SendTemplateNotificationAsync` método de aplicación de consola de hello creado previamente con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="33b50-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="33b50-106">Observe cómo en este caso no hay ninguna necesidad de toosend varias notificaciones para distintas configuraciones regionales y plataformas.</span><span class="sxs-lookup"><span data-stu-id="33b50-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

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


<span data-ttu-id="33b50-107">Tenga en cuenta que esta llamada simple cumplirán lo fragmento localizada de Hola de noticias demasiado**todos los** los dispositivos, independientemente de la plataforma de hello, como el centro de notificaciones genera y entrega Hola correcto de dispositivos de carga nativo tooall Hola suscrito tooa etiqueta específica.</span><span class="sxs-lookup"><span data-stu-id="33b50-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="33b50-108">Enviar notificación de hello con servicios móviles</span><span class="sxs-lookup"><span data-stu-id="33b50-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="33b50-109">En el programador de servicio móvil, puede utilizar Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="33b50-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

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


