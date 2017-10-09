
Esta sección muestra cómo toosend importantes noticias como etiqueta las notificaciones de plantilla desde una aplicación de consola .NET.

Si usas aplicaciones móviles, consulte toohello [agregar notificaciones de inserción para aplicaciones móviles] tutorial y seleccionar la plataforma en la parte superior de Hola.

Si desea toouse Java o PHP, consulte demasiado[cómo toouse centros de notificaciones de Java y PHP]. Puede enviar notificaciones desde cualquier back-end mediante la [Interfaz de REST de Notification Hubs].

Omita los pasos 1 a 3 Si ha creado la aplicación de consola de hello para enviar notificaciones cuando completa [empezar a trabajar con los centros de notificaciones].

1. En Visual Studio, cree una aplicación de consola en Visual C#:
   
       ![][13]
2. En el menú principal de Visual Studio de hello, haga clic en **herramientas**, **Administrador de paquetes de biblioteca**, y **Package Manager Console**, a continuación, en la ventana de la consola de hello, escriba lo siguiente y presione **Escriba**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello [paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification].
3. Abrir archivo hello Program.cs y agregue Hola siguiente `using` instrucción:
   
        using Microsoft.Azure.NotificationHubs;
4. Hola `Program` clase, agregue Hola siguiendo el método o reemplazarlo si ya existe:
   
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
   
    Este código envía una notificación de plantilla para cada uno de los seis etiquetas de hello en la matriz de cadenas de Hola. uso de Hola de etiquetas se asegura de que los dispositivos reciben notificaciones sólo para las categorías de hello registrado.
5. Hola por encima del código, reemplace hello `<hub name>` y `<connection string with full access>` marcadores de posición con la notificación concentrador hello y nombre de cadena de conexión para *DefaultFullSharedAccessSignature* desde panel Hola de su centro de notificaciones .
6. Agregar Hola después de las líneas de hello **Main** método:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Compile la aplicación de consola de hello.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[empezar a trabajar con los centros de notificaciones]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Interfaz de REST de Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[agregar notificaciones de inserción para aplicaciones móviles]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[cómo toouse centros de notificaciones de Java y PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
