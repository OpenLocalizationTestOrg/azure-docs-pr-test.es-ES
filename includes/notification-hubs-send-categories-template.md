
<span data-ttu-id="d7b2d-101">En esta sección se muestra cómo enviar noticias de última hora como notificaciones de plantillas con etiquetas desde una aplicación de consola .NET.</span><span class="sxs-lookup"><span data-stu-id="d7b2d-101">This section shows how to send breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="d7b2d-102">Si usa aplicaciones Móviles, consulte el tutorial [Incorporación de notificaciones push para Mobile Apps] y seleccione su plataforma en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="d7b2d-102">If you are using Mobile Apps please refer to the [Add push notifications for Mobile Apps] tutorial and select your platform at the top.</span></span>

<span data-ttu-id="d7b2d-103">Si desea utilizar Java o PHP, consulte [Uso de Notification Hubs desde Java/PHP].</span><span class="sxs-lookup"><span data-stu-id="d7b2d-103">If you want to use Java or PHP refer to [How to use Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="d7b2d-104">Puede enviar notificaciones desde cualquier back-end mediante la [Interfaz de REST de Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="d7b2d-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="d7b2d-105">Omita los pasos 1-3 si creó la aplicación de consola para enviar notificaciones cuando completó [Introducción a Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="d7b2d-105">Skip steps 1-3 if you created the console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="d7b2d-106">En Visual Studio, cree una aplicación de consola en Visual C#:</span><span class="sxs-lookup"><span data-stu-id="d7b2d-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="d7b2d-107">En el menú principal de Visual Studio, haga clic sucesivamente en **Herramientas**, **Administrador de paquetes de la biblioteca** y **Consola del administrador de paquetes**, y luego, en la ventana de la consola, escriba lo siguiente y presione **Entrar**:</span><span class="sxs-lookup"><span data-stu-id="d7b2d-107">In the Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in the console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="d7b2d-108">Así se agrega una referencia al SDK de Centros de notificaciones de Azure mediante el [paquete NuGet Microsoft.Azure.Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="d7b2d-108">This adds a reference to the Azure Notification Hubs SDK using the [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="d7b2d-109">Abra el archivo Program.cs y agregue la siguiente instrucción `using` :</span><span class="sxs-lookup"><span data-stu-id="d7b2d-109">Open the file Program.cs and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="d7b2d-110">En la clase `Program` , agregue el siguiente método o reemplácelo si ya existe:</span><span class="sxs-lookup"><span data-stu-id="d7b2d-110">In the `Program` class, add the following method, or replace it if it already exists:</span></span>
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending the notification as a template notification. All template registrations that contain
            // "messageParam" and the proper tags will receive the notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    <span data-ttu-id="d7b2d-111">Este código envía una notificación de plantilla para cada una de las seis etiquetas en la matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="d7b2d-111">This code sends a template notification for each of the six tags in the string array.</span></span> <span data-ttu-id="d7b2d-112">El uso de etiquetas ofrece la seguridad de que los dispositivos reciben notificaciones solo de las categorías registradas.</span><span class="sxs-lookup"><span data-stu-id="d7b2d-112">The use of tags makes sure that devices receive notifications only for the registered categories.</span></span>
5. <span data-ttu-id="d7b2d-113">En el código anterior, reemplace los marcadores de posición `<hub name>` y `<connection string with full access>` por su nombre del centro de notificaciones y la cadena de conexión para *DefaultFullSharedAccessSignature* del panel de su centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d7b2d-113">In the above code, replace the `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and the connection  string for *DefaultFullSharedAccessSignature* from the dashboard of your notification hub.</span></span>
6. <span data-ttu-id="d7b2d-114">Agregue las siguientes líneas al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="d7b2d-114">Add the following lines in the **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="d7b2d-115">Compile la aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="d7b2d-115">Build the console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
<span data-ttu-id="d7b2d-116">[Introducción a Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="d7b2d-116">[Get started with Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="d7b2d-117">[Interfaz de REST de Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span><span class="sxs-lookup"><span data-stu-id="d7b2d-117">[Notification Hubs REST interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span></span>
<span data-ttu-id="d7b2d-118">[Incorporación de notificaciones push para Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="d7b2d-118">[Add push notifications for Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="d7b2d-119">[Uso de Notification Hubs desde Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span><span class="sxs-lookup"><span data-stu-id="d7b2d-119">[How to use Notification Hubs from Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span></span>
<span data-ttu-id="d7b2d-120">[paquete NuGet Microsoft.Azure.Notification Hubs]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span><span class="sxs-lookup"><span data-stu-id="d7b2d-120">[Microsoft.Azure.Notification Hubs NuGet package]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span></span>
