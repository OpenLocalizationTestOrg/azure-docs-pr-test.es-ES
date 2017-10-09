## <a name="webapi-project"></a><span data-ttu-id="ddb10-101">Proyecto WebAPI</span><span class="sxs-lookup"><span data-stu-id="ddb10-101">WebAPI Project</span></span>
1. <span data-ttu-id="ddb10-102">En Visual Studio, abra hello **AppBackend** proyecto que creó en hello **informar a los usuarios** tutorial.</span><span class="sxs-lookup"><span data-stu-id="ddb10-102">In Visual Studio, open hello **AppBackend** project that you created in hello **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="ddb10-103">En Notifications.cs, Hola de reemplazar todo **notificaciones** clase con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb10-103">In Notifications.cs, replace hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="ddb10-104">Ser seguro tooreplace Hola los marcadores de posición con la cadena de conexión (con acceso completo) para su centro de notificaciones y el nombre de la base de datos central de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddb10-104">Be sure tooreplace hello placeholders with your connection string (with full access) for your notification hub, and hello hub name.</span></span> <span data-ttu-id="ddb10-105">Puede obtener estos valores de hello [Portal clásico de Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ddb10-105">You can obtain these values from hello [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="ddb10-106">Este módulo ahora representa Hola diferentes proteger las notificaciones que se enviarán.</span><span class="sxs-lookup"><span data-stu-id="ddb10-106">This module now represents hello different secure notifications that will be sent.</span></span> <span data-ttu-id="ddb10-107">En una implementación completa, las notificaciones de Hola se almacenará en una base de datos; Para simplificar, en este caso se almacenarlos en memoria.</span><span class="sxs-lookup"><span data-stu-id="ddb10-107">In a complete implementation, hello notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
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

1. <span data-ttu-id="ddb10-108">En NotificationsController.cs, reemplace el código de hello en hello **NotificationsController** definición de la clase con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb10-108">In NotificationsController.cs, replace hello code inside hello **NotificationsController** class definition with hello following code.</span></span> <span data-ttu-id="ddb10-109">Este componente implementa un modo para la notificación de hello dispositivo tooretrieve Hola de forma segura y también proporciona una forma (por motivos de Hola de este tutorial) tootrigger dispositivos tooyour inserción segura.</span><span class="sxs-lookup"><span data-stu-id="ddb10-109">This component implements a way for hello device tooretrieve hello notification securely, and also provides a way (for hello purposes of this tutorial) tootrigger a secure push tooyour devices.</span></span> <span data-ttu-id="ddb10-110">Tenga en cuenta que cuando se envía el centro de notificaciones de hello notificación toohello, sólo enviamos una notificación sin formato con el Id. de Hola de notificación de hello (y ningún mensaje real):</span><span class="sxs-lookup"><span data-stu-id="ddb10-110">Note that when sending hello notification toohello notification hub, we only send a raw notification with hello ID of hello notification (and no actual message):</span></span>
   
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


<span data-ttu-id="ddb10-111">Tenga en cuenta que hello `Post` método ahora no envía una notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="ddb10-111">Note that hello `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="ddb10-112">Envía una notificación sin formato que contiene solo el identificador de notificación hello y no cualquier contenido confidencial.</span><span class="sxs-lookup"><span data-stu-id="ddb10-112">It sends a raw notification that contains only hello notification ID, and not any sensitive content.</span></span> <span data-ttu-id="ddb10-113">Además, asegúrese de hello toocomment seguro de operación para plataformas de hello para el que no tiene credenciales configuradas en el centro de notificaciones, tal y como producirán errores de envío.</span><span class="sxs-lookup"><span data-stu-id="ddb10-113">Also, make sure toocomment hello send operation for hello platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="ddb10-114">Ahora se implementará volver a este sitio Web de Azure de tooan de aplicación en orden toomake, accesible desde todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ddb10-114">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="ddb10-115">Haga doble clic en hello **AppBackend** de proyecto y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="ddb10-115">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="ddb10-116">Seleccione Sitio web Azure como destino de publicación.</span><span class="sxs-lookup"><span data-stu-id="ddb10-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="ddb10-117">Inicie sesión con su cuenta de Azure y seleccione un sitio Web nuevo o existente y tome nota de hello **dirección URL de destino** propiedad Hola **conexión** ficha. Nos referiremos toothis URL según su *punto de conexión de back-end* más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ddb10-117">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="ddb10-118">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="ddb10-118">Click **Publish**.</span></span>

