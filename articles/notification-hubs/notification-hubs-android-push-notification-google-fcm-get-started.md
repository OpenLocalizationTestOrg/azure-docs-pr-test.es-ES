---
title: "aaaSending tooAndroid de notificaciones de inserción con centros de notificaciones de Azure y la mensajería de nube de Firebase | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure y la mensajería de nube de Firebase toopush dispositivos de tooAndroid notificaciones."
services: notification-hubs
documentationcenter: android
keywords: "notificaciones push,notificación push,notificación push android, fcm, firebase cloud messaging"
author: ysxu
manager: erikre
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: d2e57437ac7b0ef77abf048f991043620621e58d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a>Enviar tooAndroid de notificaciones de inserción con centros de notificaciones de Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Información general
> [!IMPORTANT]
> En este tema se muestran las notificaciones push con Firebase Cloud Messaging (FCM) de Google. Si todavía se usa Conexión compartida a Internet (GCM, Google Cloud Messaging), vea [tooAndroid de notificaciones de inserción de envío con centros de notificaciones de Azure y GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

Este tutorial muestra cómo toouse centros de notificaciones de Azure y mensajería de nube de Firebase toosend aplicación Android de tooan de notificaciones push.
Creará una aplicación de Android en blanco que reciba notificaciones push mediante Firebase Cloud Messaging (FCM).

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

código de Hello completado para este tutorial puede descargarse desde GitHub [aquí](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).

## <a name="prerequisites"></a>Requisitos previos
> [!IMPORTANT]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).
> 
> 

* Además la cuenta activa de Azure tooan mencionados anteriormente, este tutorial requiere la versión más reciente de Hola de [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).
* Android 2.3, o una versión superior, para Firebase Cloud Messaging.
* Para Firebase Cloud Messaging, se requiere la revisión 27 del repositorio de Google, o una revisión posterior.
* Google Play Services 9.0.2, o una versión superior, para Firebase Cloud Messaging.
* La realización de este tutorial es un requisito previo para todos los tutoriales de Centros de notificaciones para aplicaciones Android.

## <a name="create-a-new-android-studio-project"></a>Creación de un nuevo proyecto de Android Studio
1. En Android Studio, inicie un nuevo proyecto de Android Studio.
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. Elija hello **teléfono y tableta** forman hello y factor **mínimo SDK** que desea toosupport. A continuación, haga clic en **Siguiente**.
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. Elija **actividad vacía** para la actividad principal de hello, haga clic en **siguiente**y, a continuación, haga clic en **finalizar**.

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Creación de un proyecto que admita Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Configuración de un centro de notificaciones nuevo
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6. Hola **configuración** hoja de su centro de notificaciones, seleccione **Notification Services** y, a continuación, **Google (GCM)**. Escriba Hola FCM servidor clave que copió anteriormente de hello [consola Firebase](https://firebase.google.com/console/) y haga clic en **guardar**.

&emsp;&emsp;![Centros de notificaciones de Azure: Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

El centro de notificaciones está ahora configurado toowork con Firebase Messagin de nube y tener tooboth de cadenas de conexión de hello registrar su aplicación tooreceive y enviar notificaciones de inserción.

## <a id="connecting-app"></a>Conectar el centro de notificaciones de toohello de aplicación
### <a name="add-google-play-services-toohello-project"></a>Agregar proyecto de Google Play services toohello
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Incorporación de bibliotecas de Centros de notificaciones de Azure
1. Hola `Build.Gradle` archivo para hello **aplicación**, agregar Hola después de las líneas de hello **dependencias** sección.
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. Agregar Hola después repositorio después de hello **dependencias** sección.
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a>Actualizando hello AndroidManifest.xml.
1. toosupport FCM, debemos implementar un servicio de agente de escucha de Id. de instancia en el código que se usa demasiado[obtener tokens de registro](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) con [FirebaseInstanceId API de Google](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId). En este tutorial se denominará clase hello `MyInstanceIDService`. 
   
    Agregar Hola siguiente servicio definición toohello AndroidManifest.xml el archivo, dentro de hello `<application>` etiqueta. 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. Una vez que hemos recibido el token de registro FCM de hello FirebaseInstanceId API, se usará demasiado[registrar con hello centro de notificaciones de Azure](notification-hubs-push-notification-registration-management.md). Se admite este registro de hello plano utilizando un `IntentService` denominado `RegistrationIntentService`. Este servicio también será responsable de actualizar el token de registro de FCM.
   
    Agregar Hola siguiente servicio definición toohello AndroidManifest.xml el archivo, dentro de hello `<application>` etiqueta. 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. También definirá un notificaciones de tooreceive de receptor. Agregar Hola siguiente receptor definición toohello AndroidManifest.xml el archivo, dentro de hello `<application>` etiqueta. Reemplace hello `<your package>` Hola de marcador de posición con el nombre del paquete real se muestran en la parte superior de Hola de hello `AndroidManifest.xml` archivo.
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. Agregar Hola después FCM necesario relacionados con permisos por debajo de hello `</application>` etiqueta. Asegúrese de que tooreplace `<your package>` con el nombre del paquete Hola se muestran en la parte superior de Hola de hello `AndroidManifest.xml` archivo.
   
    Para obtener más información sobre estos permisos, consulte [la instalación de una aplicación cliente de GCM para Android](https://developers.google.com/cloud-messaging/android/client#manifest) y [migrar una aplicación de cliente de GCM para Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a>Incorporación de código
1. Hola vista de proyecto, expanda **aplicación** > **src** > **principal** > **java**. Haga clic con el botón derecho en la carpeta del paquete en **java**, haga clic en **Nuevo** y, a continuación, haga clic en **Clase Java**. Agregue una clase nueva llamada `NotificationSettings`. 
   
    ![Android Studio: nueva clase Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    Asegúrese de que tooupdate Hola estos tres marcadores de posición en hello después el código de hello `NotificationSettings` clase:
   
   * **Id. de remitente**: Hola Id. de remitente obtenido anteriormente en hello **Cloud Messaging** ficha de la configuración del proyecto en hello [consola Firebase](https://firebase.google.com/console/).
   * **HubListenConnectionString**: Hola **DefaultListenAccessSignature** cadena de conexión para el concentrador. Puede copiar esa cadena de conexión, haga clic en **las directivas de acceso** en hello **configuración** hoja de su centro de hello [Portal de Azure].
   * **HubName**: usar el nombre de su centro de notificaciones que aparece en la hoja de concentrador de Hola Hola Hola [Portal de Azure].
     
     `NotificationSettings` :
     
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       }
2. Mediante pasos de hello anteriores, agregue otra nueva clase denominada `MyInstanceIDService`. Se trata de nuestra implementación de servicio de escucha de Instance ID.
   
    Llame código de Hello para esta clase nuestro `IntentService` demasiado[actualización Hola FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) en segundo plano de Hola.
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. Agregue otra clase tooyour proyecto denominado, `RegistrationIntentService`. Se trata de implementación de Hola para nuestro `IntentService` que controlará [actualizar token FCM de hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) y [registrar con el centro de notificaciones de hello](notification-hubs-push-notification-registration-management.md).
   
    Usar hello siguiente código para esta clase.
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {
   
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if hello token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete registration", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. En su `MainActivity` de clases, agregue los siguientes hello `import` instrucciones anteriores Hola declaración de clase.
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. Agregar Hola siguiendo los miembros privados en parte superior de hello de la clase hello. Usaremos estos [comprobar la disponibilidad de hello de servicios de Google Play según las recomendaciones de Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. En su `MainActivity` clase, agregue Hola método toohello lanzamiento de servicios de Google Play. 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. En su `MainActivity` clase, agregue Hola después el código que se comprobará para servicios de Google Play antes de llamar a su `IntentService` tooget su token de registro FCM y registrarse con el centro de notificaciones.
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. Hola `OnCreate` método de hello `MainActivity` clase, agregue Hola siguiendo el proceso de registro de hello toostart de código cuando se crea la actividad.
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. Agregar estos métodos adicionales toohello `MainActivity` tooverify estado y el informe Estado de la aplicación en la aplicación.
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. Hola `ToastNotify` método usa hello *"Hola mundo"* `TextView` tooreport estado y notificaciones de forma persistente en la aplicación hello de control. En el diseño activity_main.xml, agregue Hola siguiente Id. de ese control.
   
       android:id="@+id/text_hello"
9. A continuación, agregaremos una subclase para nuestro receptor que definimos en hello AndroidManifest.xml. Agregue otra clase tooyour proyecto denominado `MyHandler`.
10. Agregar Hola siguiendo las instrucciones de importación en la parte superior de Hola de `MyHandler.java`:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. Agregar Hola después el código de hello `MyHandler` clase lo que una subclase de `com.microsoft.windowsazure.notifications.NotificationsHandler`.
    
    Este código invalida hello `OnReceive` método, por lo que el controlador de hello informará de las notificaciones que se reciben. controlador de Hello envía también Administrador de Android notificaciones de toohello de notificación de inserción de hello mediante hello `sendNotification()` método. Hola `sendNotification()` el método debe ejecutarse cuando no se está ejecutando la aplicación hello y se recibe una notificación.
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. En Android Studio en la barra de menús de hello, haga clic en **generar** > **volver a generar el proyecto** toomake seguro de que no están presentes en el código errores.
13. Ejecutar la aplicación hello en el dispositivo y comprobar que se registra correctamente con el centro de notificaciones de Hola. 
    
    > [!NOTE]
    > Registro puede producir un error en el lanzamiento inicial de hello hasta hello `onTokenRefresh()` se llama al método de servicio de Id. de instancia. actualización de Hello debe iniciar un registro correcto con el centro de notificaciones de Hola.
    > 
    > 

## <a name="sending-push-notifications"></a>Envío de notificaciones push
Puede probar recibiendo notificaciones de inserción en la aplicación mediante el envío de ellos a través de hello [Portal de Azure] -busque hello **solución de problemas** sección en la hoja de la base de datos central de hello, tal y como se muestra a continuación.

![Centros de notificaciones de Azure: envío de prueba](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a>(Opcional) Enviar notificaciones de inserción directamente desde la aplicación hello
> [!IMPORTANT]
> Este ejemplo de envío de notificaciones de la aplicación de cliente de hello se proporciona con fines de aprendizaje. Puesto que esto requerirá hello `DefaultFullSharedAccessSignature` toobe presente en la aplicación de cliente de hello, expone el riesgo de toohello de concentrador de notificación que un usuario puede obtener acceso no autorizado de toosend notificaciones tooyour clientes.
> 
> 

Lo habitual es enviar notificaciones mediante un servidor back-end. En algunos casos, conviene toobe toosend capaz de notificaciones de inserción directamente desde la aplicación de cliente de Hola. Esta sección explica cómo Hola toosend notificaciones de cliente hello mediante [API de REST de concentrador de notificación de Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).

1. En la vista de proyecto de Android Studio, expanda **App** > **src** > **main** > **res** > **layout**. Abra hello `activity_main.xml` diseño de archivo y haga clic en hello **texto** ficha tooupdate Hola contenido de texto hello archivo. Actualícelo con código de hello siguiente, que agrega las nuevas `Button` y `EditText` centro de notificaciones de toohello de mensajes de notificación de inserción de controles para el envío. Agregue este código en la parte inferior de hello, justo delante `</RelativeLayout>`.
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. En la vista de proyecto de Android Studio, expanda **App** > **src** > **main** > **res** > **values**. Abra hello `strings.xml` de archivos y agregar valores de cadena de Hola que hace referencia Hola nueva `Button` y `EditText` controles. Agregue estos elementos en la parte inferior de Hola de archivo hello, justo delante `</resources>`.
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. En su `NotificationSetting.java` , agregue Hola después configuración toohello `NotificationSettings` clase.
   
    Actualización `HubFullAccess` con hello **DefaultFullSharedAccessSignature** cadena de conexión para el concentrador. Esta cadena de conexión se puede copiar desde hello [Portal de Azure] haciendo clic en **las directivas de acceso** en hello **configuración** hoja para el centro de notificaciones.
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. En su `MainActivity.java` , agregue la siguiente hello `import` instrucciones anteriores hello `MainActivity` clase.
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. En su `MainActivity.java` , agregue Hola después de miembros en la parte superior de Hola de hello `MainActivity` clase.    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. Debe crear un tooauthenticate de token de firma de acceso de Software (SaS) en un centro de notificaciones de entrada solicitud toosend mensajes tooyour. Esto se hace mediante el análisis Hola datos clave de cadena de conexión de hello y, a continuación, crear Hola token de SaS, tal y como se mencionó en hello [conceptos comunes](http://msdn.microsoft.com/library/azure/dn495627.aspx) referencia de la API de REST. Hola siguiente código es una implementación de ejemplo.
   
    En `MainActivity.java`, agregar Hola siguiendo el método toohello `MainActivity` clase tooparse la cadena de conexión.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. En `MainActivity.java`, agregar Hola siguiendo el método toohello `MainActivity` clase toocreate un token de autenticación de SaS.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. En `MainActivity.java`, agregar Hola siguiendo el método toohello `MainActivity` Hola de clase toohandle **enviar notificación** clic de botón y enviar una notificación de inserción de hello concentrador de toohello de mensajes mediante el uso de Hola integrados API de REST.
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a>Prueba de la aplicación
#### <a name="push-notifications-in-hello-emulator"></a>Notificaciones de inserción en el emulador de Hola
Si desea que las notificaciones de inserción de tootest dentro de un emulador, asegúrese de que la imagen del emulador admite el nivel de API de Google de Hola que eligió para su aplicación. Si la imagen no es compatible con nativo APIs Google, terminará con hello **servicio\_no\_disponible** excepción.

Además toohello anterior, asegúrese de que ha agregado el tooyour de cuenta de Google ejecución del emulador en **configuración** > **cuentas**. En caso contrario, está penada por la tooregister intentos con GCM en hello **autenticación\_error** excepción.

#### <a name="running-hello-application"></a>Ejecuta la aplicación hello
1. Ejecutar aplicación hello y observe que se notifica el Id. del registro de hello para un registro correcto.
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. Escriba un toobe de mensaje de notificación enviado tooall dispositivos Android que han registrado con el concentrador de Hola.
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. Presione **Enviar notificación**. Los dispositivos que tienen la ejecución de la aplicación de hello mostrará un `AlertDialog` instancia con el mensaje de notificación de inserción de saludo. Dispositivos que no tienen la ejecución de la aplicación de hello pero que se registraron anteriormente para las notificaciones de inserción recibirá una notificación en hello Administrador de notificaciones Android. Los pueden verse deslizando hacia abajo desde la esquina superior izquierda de Hola.
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a>Pasos siguientes
Se recomienda hello [toousers de notificaciones de los centros de notificaciones de uso toopush] tutorial como paso siguiente Hola. Le mostraremos cómo toosend notificaciones desde un back-end ASP.NET con etiquetas tootarget determinados usuarios.

Si desea toosegment los usuarios por grupos de interés, desproteger hello [toosend de centros de notificaciones utilice noticias de última hora] tutorial.

toolearn obtener más información sobre los centros de notificaciones, consulte nuestro [instrucciones de los centros de notificación].

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[instrucciones de los centros de notificación]: notification-hubs-push-notification-overview.md
[toousers de notificaciones de los centros de notificaciones de uso toopush]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend de centros de notificaciones utilice noticias de última hora]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Portal de Azure]: https://portal.azure.com
