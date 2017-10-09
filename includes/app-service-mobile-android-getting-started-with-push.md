1. En su **aplicación** proyecto, archivo abierto hello `AndroidManifest.xml`. En el código de hello en hello dos pasos siguientes, reemplace  *`**my_app_package**`*  con nombre Hola Hola del paquete de aplicación para el proyecto. Este es el valor de Hola de hello `package` atributo de hello `manifest` etiqueta.
2. Agregue los siguientes permisos nuevo después de hello existente de hello `uses-permission` elemento:

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. Agregar Hola siguiente código después de hello `application` etiqueta de apertura:

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. Archivo abierto hello *ToDoActivity.java*y agregue Hola después de la instrucción import:

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. Agregar Hola después de la clase toohello variable privada. Reemplace  *`<PROJECT_NUMBER>`*  con número de proyecto de hello asignado por Google tooyour aplicación Hola anterior procedimiento.

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. Cambiar la definición de Hola de *MobileServiceClient* de **privada** demasiado**estáticos públicos**, por lo que ahora el siguiente aspecto:

        public static MobileServiceClient mClient;
7. Agregar un nuevo notificaciones toohandle de clase. En el Explorador de proyectos, abra hello **src** > **principal** > **java** nodos y nodo de nombre del paquete de Hola de menú contextual. Haga clic en **Nuevo** y en **Clase Java**.
8. En **Nombre** escriba `MyHandler` y, después, haga clic en **Aceptar**.

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. En el archivo de MyHandler hello, reemplace la declaración de clase de hello con:

        public class MyHandler extends NotificationsHandler {
10. Agregar Hola siguiendo las instrucciones de importación para hello `MyHandler` clase:

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. A continuación, agregue este miembro toohello `MyHandler` clase:

        public static final int NOTIFICATION_ID = 1;
12. Hola `MyHandler` clase, agregue Hola después Hola de código toooverride **onRegistered** método, que registra el dispositivo con el centro de notificaciones del servicio móvil de Hola.

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
       }
13. Hola `MyHandler` clase, agregue Hola después Hola de código toooverride **onReceive** método, que hace que hello toodisplay de notificación cuando se recibe.

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
       }
14. En el archivo de TodoActivity.java hello, actualizar hello **onCreate** método de hello *ToDoActivity* clase clase de controlador de notificación de tooregister Hola. Realizar tooadd seguro este código después de hello *MobileServiceClient* se crea una instancia.

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    La aplicación ya está actualizado toosupport notificaciones de inserción.
