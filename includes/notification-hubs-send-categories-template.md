
<span data-ttu-id="877cb-101">Esta sección muestra cómo toosend importantes noticias como etiqueta las notificaciones de plantilla desde una aplicación de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="877cb-101">This section shows how toosend breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="877cb-102">Si usas aplicaciones móviles, consulte toohello [agregar notificaciones de inserción para aplicaciones móviles] tutorial y seleccionar la plataforma en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="877cb-102">If you are using Mobile Apps please refer toohello [Add push notifications for Mobile Apps] tutorial and select your platform at hello top.</span></span>

<span data-ttu-id="877cb-103">Si desea toouse Java o PHP, consulte demasiado[cómo toouse centros de notificaciones de Java y PHP].</span><span class="sxs-lookup"><span data-stu-id="877cb-103">If you want toouse Java or PHP refer too[How toouse Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="877cb-104">Puede enviar notificaciones desde cualquier back-end mediante la [Interfaz de REST de Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="877cb-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="877cb-105">Omita los pasos 1 a 3 Si ha creado la aplicación de consola de hello para enviar notificaciones cuando completa [empezar a trabajar con los centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="877cb-105">Skip steps 1-3 if you created hello console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="877cb-106">En Visual Studio, cree una aplicación de consola en Visual C#:</span><span class="sxs-lookup"><span data-stu-id="877cb-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="877cb-107">En el menú principal de Visual Studio de hello, haga clic en **herramientas**, **Administrador de paquetes de biblioteca**, y **Package Manager Console**, a continuación, en la ventana de la consola de hello, escriba lo siguiente y presione **Escriba**:</span><span class="sxs-lookup"><span data-stu-id="877cb-107">In hello Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in hello console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="877cb-108">Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello [paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification].</span><span class="sxs-lookup"><span data-stu-id="877cb-108">This adds a reference toohello Azure Notification Hubs SDK using hello [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="877cb-109">Abrir archivo hello Program.cs y agregue Hola siguiente `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="877cb-109">Open hello file Program.cs and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="877cb-110">Hola `Program` clase, agregue Hola siguiendo el método o reemplazarlo si ya existe:</span><span class="sxs-lookup"><span data-stu-id="877cb-110">In hello `Program` class, add hello following method, or replace it if it already exists:</span></span>
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    <span data-ttu-id="877cb-111">Este código envía una notificación de plantilla para cada uno de los seis etiquetas de hello en la matriz de cadenas de Hola.</span><span class="sxs-lookup"><span data-stu-id="877cb-111">This code sends a template notification for each of hello six tags in hello string array.</span></span> <span data-ttu-id="877cb-112">uso de Hola de etiquetas se asegura de que los dispositivos reciben notificaciones sólo para las categorías de hello registrado.</span><span class="sxs-lookup"><span data-stu-id="877cb-112">hello use of tags makes sure that devices receive notifications only for hello registered categories.</span></span>
5. <span data-ttu-id="877cb-113">Hola por encima del código, reemplace hello `<hub name>` y `<connection string with full access>` marcadores de posición con la notificación concentrador hello y nombre de cadena de conexión para *DefaultFullSharedAccessSignature* desde panel Hola de su centro de notificaciones .</span><span class="sxs-lookup"><span data-stu-id="877cb-113">In hello above code, replace hello `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and hello connection  string for *DefaultFullSharedAccessSignature* from hello dashboard of your notification hub.</span></span>
6. <span data-ttu-id="877cb-114">Agregar Hola después de las líneas de hello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="877cb-114">Add hello following lines in hello **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="877cb-115">Compile la aplicación de consola de hello.</span><span class="sxs-lookup"><span data-stu-id="877cb-115">Build hello console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[empezar a trabajar con los centros de notificaciones]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Interfaz de REST de Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[agregar notificaciones de inserción para aplicaciones móviles]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[cómo toouse centros de notificaciones de Java y PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
