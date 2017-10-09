## <a name="webapi-project"></a>Proyecto WebAPI
1. En Visual Studio, abra hello **AppBackend** proyecto que creó en hello **informar a los usuarios** tutorial.
2. En Notifications.cs, Hola de reemplazar todo **notificaciones** clase con el siguiente código de hello. Ser seguro tooreplace Hola los marcadores de posición con la cadena de conexión (con acceso completo) para su centro de notificaciones y el nombre de la base de datos central de Hola. Puede obtener estos valores de hello [Portal clásico de Azure](http://manage.windowsazure.com). Este módulo ahora representa Hola diferentes proteger las notificaciones que se enviarán. En una implementación completa, las notificaciones de Hola se almacenará en una base de datos; Para simplificar, en este caso se almacenarlos en memoria.
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. En NotificationsController.cs, reemplace el código de hello en hello **NotificationsController** definición de la clase con el siguiente código de hello. Este componente implementa un modo para la notificación de hello dispositivo tooretrieve Hola de forma segura y también proporciona una forma (por motivos de Hola de este tutorial) tootrigger dispositivos tooyour inserción segura. Tenga en cuenta que cuando se envía el centro de notificaciones de hello notificación toohello, sólo enviamos una notificación sin formato con el Id. de Hola de notificación de hello (y ningún mensaje real):
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


Tenga en cuenta que hello `Post` método ahora no envía una notificación del sistema. Envía una notificación sin formato que contiene solo el identificador de notificación hello y no cualquier contenido confidencial. Además, asegúrese de hello toocomment seguro de operación para plataformas de hello para el que no tiene credenciales configuradas en el centro de notificaciones, tal y como producirán errores de envío.

1. Ahora se implementará volver a este sitio Web de Azure de tooan de aplicación en orden toomake, accesible desde todos los dispositivos. Haga doble clic en hello **AppBackend** de proyecto y seleccione **publicar**.
2. Seleccione Sitio web Azure como destino de publicación. Inicie sesión con su cuenta de Azure y seleccione un sitio Web nuevo o existente y tome nota de hello **dirección URL de destino** propiedad Hola **conexión** ficha. Nos referiremos toothis URL según su *punto de conexión de back-end* más adelante en este tutorial. Haga clic en **Publicar**.

