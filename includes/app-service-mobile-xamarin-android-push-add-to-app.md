1. <span data-ttu-id="0e362-101">Cree una nueva clase en el proyecto Hola denominado `ToDoBroadcastReceiver`.</span><span class="sxs-lookup"><span data-stu-id="0e362-101">Create a new class in hello project called `ToDoBroadcastReceiver`.</span></span>
2. <span data-ttu-id="0e362-102">Agregue los siguiente hello mediante instrucciones demasiado**ToDoBroadcastReceiver** clase:</span><span class="sxs-lookup"><span data-stu-id="0e362-102">Add hello following using statements too**ToDoBroadcastReceiver** class:</span></span>
   
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="0e362-103">Agregar Hola siguiendo las solicitudes de permiso entre hello **con** hello e instrucciones **espacio de nombres** declaración:</span><span class="sxs-lookup"><span data-stu-id="0e362-103">Add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
4. <span data-ttu-id="0e362-104">Reemplazar existente hello **ToDoBroadcastReceiver** definición por siguiente hello de la clase:</span><span class="sxs-lookup"><span data-stu-id="0e362-104">Replace hello existing **ToDoBroadcastReceiver** class definition with hello following:</span></span>
   
        [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, 
        Categories = new string[] { "@PACKAGE_NAME@" })]
        public class ToDoBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            // Set hello Google app ID.
            public static string[] senderIDs = new string[] { "<PROJECT_NUMBER>" };
        }
   
    <span data-ttu-id="0e362-105">Hola por encima del código, debe reemplazar  *`<PROJECT_NUMBER>`*  con número de proyecto de hello asignado por Google al aprovisionar la aplicación en el portal para desarrolladores de hello Google.</span><span class="sxs-lookup"><span data-stu-id="0e362-105">In hello above code, you must replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google when you provisioned your app in hello Google developer portal.</span></span> 
5. <span data-ttu-id="0e362-106">En el archivo de proyecto de hello ToDoBroadcastReceiver.cs, agregar Hola después el código que define hello **PushHandlerService** clase:</span><span class="sxs-lookup"><span data-stu-id="0e362-106">In hello ToDoBroadcastReceiver.cs project file, add hello following code that defines hello **PushHandlerService** class:</span></span>
   
        // hello ServiceAttribute must be applied toohello class.
        [Service] 
        public class PushHandlerService : GcmServiceBase
        {
            public static string RegistrationID { get; private set; }
   
            public PushHandlerService() : base(ToDoBroadcastReceiver.senderIDs) { }
        }
   
    <span data-ttu-id="0e362-107">Tenga en cuenta que esta clase se deriva de **GcmServiceBase** ese hello y **servicio** debe ser el atributo aplicado toothis clase.</span><span class="sxs-lookup"><span data-stu-id="0e362-107">Note that this class derives from **GcmServiceBase** and that hello **Service** attribute must be applied toothis class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0e362-108">Hola **GcmServiceBase** clase implementa hello **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** y  **OnError()** métodos.</span><span class="sxs-lookup"><span data-stu-id="0e362-108">hello **GcmServiceBase** class implements hello **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** and **OnError()** methods.</span></span> <span data-ttu-id="0e362-109">Debe invalidar estos métodos en hello **PushHandlerService** clase.</span><span class="sxs-lookup"><span data-stu-id="0e362-109">You must override these methods in hello **PushHandlerService** class.</span></span>
   > 
   > 
6. <span data-ttu-id="0e362-110">Agregar Hola después código toohello **PushHandlerService** clase que invalide hello **OnRegistered** controlador de eventos.</span><span class="sxs-lookup"><span data-stu-id="0e362-110">Add hello following code toohello **PushHandlerService** class that overrides hello **OnRegistered** event handler.</span></span> 
   
        protected override void OnRegistered(Context context, string registrationId)
        {
            System.Diagnostics.Debug.WriteLine("hello device has been registered with GCM.", "Success!");
   
            // Get hello MobileServiceClient from hello current activity instance.
            MobileServiceClient client = ToDoActivity.CurrentActivity.CurrentClient;
            var push = client.GetPush();
   
            // Define a message body for GCM.
            const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
            // Define hello template registration as JSON.
            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
              {"body", templateBodyGCM }
            };
   
            try
            {
                // Make sure we run hello registration on hello same thread as hello activity, 
                // tooavoid threading errors.
                ToDoActivity.CurrentActivity.RunOnUiThread(
   
                    // Register hello template with Notification Hubs.
                    async () => await push.RegisterAsync(registrationId, templates));
   
                System.Diagnostics.Debug.WriteLine(
                    string.Format("Push Installation Id", push.InstallationId.ToString()));
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(
                    string.Format("Error with Azure push registration: {0}", ex.Message));
            }
        }
   
    <span data-ttu-id="0e362-111">Este método usa Hola devuelve GCM tooregister de Id. de registro con Azure para las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="0e362-111">This method uses hello returned GCM registration ID tooregister with Azure for push notifications.</span></span> <span data-ttu-id="0e362-112">Las etiquetas pueden solo pueden agregarse toohello registro después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="0e362-112">Tags can only be added toohello registration after it is created.</span></span> <span data-ttu-id="0e362-113">Para obtener más información, consulte [Cómo: agregar etiquetas tooa dispositivo instalación tooenable inserción-a-etiquetas](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span><span class="sxs-lookup"><span data-stu-id="0e362-113">For more information, see [How to: Add tags tooa device installation tooenable push-to-tags](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span></span>
7. <span data-ttu-id="0e362-114">Invalidar hello **OnMessage** método **PushHandlerService** con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="0e362-114">Override hello **OnMessage** method in **PushHandlerService** with hello following code:</span></span>
   
       protected override void OnMessage(Context context, Intent intent)
       {          
           string message = string.Empty;
   
           // Extract hello push notification message from hello intent.
           if (intent.Extras.ContainsKey("message"))
           {
               message = intent.Extras.Get("message").ToString();
               var title = "New item added:";
   
               // Create a notification manager toosend hello notification.
               var notificationManager = 
                   GetSystemService(Context.NotificationService) as NotificationManager;
   
               // Create a new intent tooshow hello notification in hello UI. 
               PendingIntent contentIntent = 
                   PendingIntent.GetActivity(context, 0, 
                   new Intent(this, typeof(ToDoActivity)), 0);              
   
               // Create hello notification using hello builder.
               var builder = new Notification.Builder(context);
               builder.SetAutoCancel(true);
               builder.SetContentTitle(title);
               builder.SetContentText(message);
               builder.SetSmallIcon(Resource.Drawable.ic_launcher);
               builder.SetContentIntent(contentIntent);
               var notification = builder.Build();
   
               // Display hello notification in hello Notifications Area.
               notificationManager.Notify(1, notification);
   
           }
       }
8. <span data-ttu-id="0e362-115">Invalidar hello **OnUnRegistered()** y **OnError()** métodos con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="0e362-115">Override hello **OnUnRegistered()** and **OnError()** methods with hello following code.</span></span>
   
       protected override void OnUnRegistered(Context context, string registrationId)
       {
           throw new NotImplementedException();
       }
   
       protected override void OnError(Context context, string errorId)
       {
           System.Diagnostics.Debug.WriteLine(
               string.Format("Error occurred in hello notification: {0}.", errorId));
       }

