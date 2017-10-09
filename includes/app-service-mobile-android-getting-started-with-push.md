1. <span data-ttu-id="aa9a1-101">En su **aplicación** proyecto, archivo abierto hello `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-101">In your **app** project, open hello file `AndroidManifest.xml`.</span></span> <span data-ttu-id="aa9a1-102">En el código de hello en hello dos pasos siguientes, reemplace  *`**my_app_package**`*  con nombre Hola Hola del paquete de aplicación para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-102">In hello code in hello next two steps, replace *`**my_app_package**`* with hello name of hello app package for your project.</span></span> <span data-ttu-id="aa9a1-103">Este es el valor de Hola de hello `package` atributo de hello `manifest` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-103">This is hello value of hello `package` attribute of hello `manifest` tag.</span></span>
2. <span data-ttu-id="aa9a1-104">Agregue los siguientes permisos nuevo después de hello existente de hello `uses-permission` elemento:</span><span class="sxs-lookup"><span data-stu-id="aa9a1-104">Add hello following new permissions after hello existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="aa9a1-105">Agregar Hola siguiente código después de hello `application` etiqueta de apertura:</span><span class="sxs-lookup"><span data-stu-id="aa9a1-105">Add hello following code after hello `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="aa9a1-106">Archivo abierto hello *ToDoActivity.java*y agregue Hola después de la instrucción import:</span><span class="sxs-lookup"><span data-stu-id="aa9a1-106">Open hello file *ToDoActivity.java*, and add hello following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="aa9a1-107">Agregar Hola después de la clase toohello variable privada.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-107">Add hello following private variable toohello class.</span></span> <span data-ttu-id="aa9a1-108">Reemplace  *`<PROJECT_NUMBER>`*  con número de proyecto de hello asignado por Google tooyour aplicación Hola anterior procedimiento.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-108">Replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google tooyour app in hello preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="aa9a1-109">Cambiar la definición de Hola de *MobileServiceClient* de **privada** demasiado**estáticos públicos**, por lo que ahora el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="aa9a1-109">Change hello definition of *MobileServiceClient* from **private** too**public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="aa9a1-110">Agregar un nuevo notificaciones toohandle de clase.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-110">Add a new class toohandle notifications.</span></span> <span data-ttu-id="aa9a1-111">En el Explorador de proyectos, abra hello **src** > **principal** > **java** nodos y nodo de nombre del paquete de Hola de menú contextual.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-111">In Project Explorer, open hello **src** > **main** > **java** nodes, and right-click hello package name node.</span></span> <span data-ttu-id="aa9a1-112">Haga clic en **Nuevo** y en **Clase Java**.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="aa9a1-113">En **Nombre** escriba `MyHandler` y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="aa9a1-114">En el archivo de MyHandler hello, reemplace la declaración de clase de hello con:</span><span class="sxs-lookup"><span data-stu-id="aa9a1-114">In hello MyHandler file, replace hello class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="aa9a1-115">Agregar Hola siguiendo las instrucciones de importación para hello `MyHandler` clase:</span><span class="sxs-lookup"><span data-stu-id="aa9a1-115">Add hello following import statements for hello `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="aa9a1-116">A continuación, agregue este miembro toohello `MyHandler` clase:</span><span class="sxs-lookup"><span data-stu-id="aa9a1-116">Next add this member toohello `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="aa9a1-117">Hola `MyHandler` clase, agregue Hola después Hola de código toooverride **onRegistered** método, que registra el dispositivo con el centro de notificaciones del servicio móvil de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-117">In hello `MyHandler` class, add hello following code toooverride hello **onRegistered** method, which registers your device with hello mobile service notification hub.</span></span>

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       <span data-ttu-id="aa9a1-118">}</span><span class="sxs-lookup"><span data-stu-id="aa9a1-118">}</span></span>
13. <span data-ttu-id="aa9a1-119">Hola `MyHandler` clase, agregue Hola después Hola de código toooverride **onReceive** método, que hace que hello toodisplay de notificación cuando se recibe.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-119">In hello `MyHandler` class, add hello following code toooverride hello **onReceive** method, which causes hello notification toodisplay when it is received.</span></span>

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       <span data-ttu-id="aa9a1-120">}</span><span class="sxs-lookup"><span data-stu-id="aa9a1-120">}</span></span>
14. <span data-ttu-id="aa9a1-121">En el archivo de TodoActivity.java hello, actualizar hello **onCreate** método de hello *ToDoActivity* clase clase de controlador de notificación de tooregister Hola.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-121">Back in hello TodoActivity.java file, update hello **onCreate** method of hello *ToDoActivity* class tooregister hello notification handler class.</span></span> <span data-ttu-id="aa9a1-122">Realizar tooadd seguro este código después de hello *MobileServiceClient* se crea una instancia.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-122">Make sure tooadd this code after hello *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="aa9a1-123">La aplicación ya está actualizado toosupport notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="aa9a1-123">Your app is now updated toosupport push notifications.</span></span>
