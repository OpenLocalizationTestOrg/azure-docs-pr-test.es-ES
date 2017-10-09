---
title: aaaGet comenzar con centros de notificaciones de Azure para aplicaciones Kindle | Documentos de Microsoft
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toosend push aplicación de notificaciones de tooa Kindle."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a>Introducción a Centros de notificaciones para aplicaciones Kindle
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Información general
Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push aplicación de notificaciones de tooa Kindle.
Creará una aplicación Kindle vacía que recibirá notificaciones push mediante Amazon Device Messaging (ADM).

## <a name="prerequisites"></a>Requisitos previos
Este tutorial requiere siguiente de hello:

* Obtener Hola Android SDK (se supone que va a usar Eclipse) de hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">sitio Android</a>.
* Siga los pasos de hello en <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">configuración del entorno de desarrollo</a> tooset del entorno de desarrollo para Kindle.

## <a name="add-a-new-app-toohello-developer-portal"></a>Agregar un nuevo portal para desarrolladores de aplicaciones toohello
1. En primer lugar, cree una aplicación Hola [portal para desarrolladores de Amazon].
   
    ![][0]
2. Hola copia **clave de aplicación**.
   
    ![][1]
3. En el portal de hello, haga clic en nombre de saludo de la aplicación y, a continuación, haga clic en hello **Device Messaging** ficha.
   
    ![][2]
4. Haga clic en **Create a New Security Profile** (Crear un nuevo perfil de seguridad) y, luego, cree un nuevo perfil de seguridad (por ejemplo, **perfil de seguridad TestAdm**). A continuación, haga clic en **Guardar**.
   
    ![][3]
5. Haga clic en **seguridad perfiles** perfil de seguridad de hello tooview que acaba de crear. Hola copia **Id. de cliente** y **secreto de cliente** valores para su uso posterior.
   
    ![][4]

## <a name="create-an-api-key"></a>Creación de una clave de API
1. Abra un símbolo del sistema con privilegios de administrador.
2. Desplazarse por las carpetas del SDK de Android toohello.
3. Escriba el siguiente comando de hello:
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. Para hello **keystore** contraseña, escriba **android**.
5. Hola copia **MD5** huellas digitales.
6. En el portal para desarrolladores de hello, en hello **mensajería** , haga clic en **Android/Kindle** y escriba el nombre hello del paquete de hello para la aplicación (por ejemplo, **com.sample.notificationhubtest**) hello y **MD5** valor y, a continuación, haga clic en **generar clave de API**.

## <a name="add-credentials-toohello-hub"></a>Agregar credenciales toohello centro
En el portal de hello, agregar toohello del Id. de cliente y secreto de cliente hello **configurar** ficha del centro de notificaciones.

## <a name="set-up-your-application"></a>Configuración de la aplicación
> [!NOTE]
> Al crear un aplicación, use al menos el nivel de API 17.
> 
> 

Agregar proyecto de Eclipse de hello ADM bibliotecas tooyour:

1. biblioteca ADM de tooobtain hello, [descargar Hola SDK]. Extraiga el archivo zip del SDK Hola.
2. En Eclipse, haga clic con el botón derecho en el proyecto y, a continuación, haga clic en **Propiedades**(Propiedades). Seleccione **Java Build Path** en Hola deja y, a continuación, seleccione Hola ** bibliotecas ** ficha situada en la parte superior de Hola. Haga clic en **agregar Jar externo**y el archivo hello seleccione `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` del directorio de hello en la que extrajo Hola SDK de Amazon.
3. Descargar hello NotificationHubs Android SDK (vínculo).
4. Descomprima el paquete de hello y, a continuación, arrastre el archivo hello `notification-hubs-sdk.jar` en hello `libs` carpeta en Eclipse.

Edite el ADM de toosupport manifiesto de aplicación:

1. Agregue el espacio de nombres de hello Amazon en elemento de manifiesto Hola raíz:

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. Agregue permisos como primer elemento de hello en el elemento manifiesto Hola. SUBSTITUTE **[el nombre del paquete]** con paquete de hello usa toocreate la aplicación.
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. Insertar Hola siguiente elemento como primer elemento secundario del elemento de la aplicación Hola Hola. Recuerde toosubstitute **[su nombre de servicio]** con el nombre de Hola de su controlador de mensajes ADM que cree en la sección siguiente de hello (paquete de hello incluidos) y reemplace **[el nombre del paquete]** con hello nombre del paquete con la que se creó la aplicación.
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a>Creación del controlador de mensajes de ADM
1. Cree una nueva clase que hereda de `com.amazon.device.messaging.ADMMessageHandlerBase` y asígnele el nombre `MyADMMessageHandler`, tal y como se muestra en hello figura siguiente:
   
    ![][6]
2. Agregue los siguiente hello `import` instrucciones:
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. Agregar Hola después el código de clase de Hola que ha creado. Recuerde toosubstitute Hola concentrador nombre de cadena de conexión y (escuchar):
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. Agregar Hola después código toohello `OnMessage()` método:
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. Agregar Hola después código toohello `OnRegistered` método:
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. Agregar Hola después código toohello `OnUnregistered` método:
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. Hola `MainActivity` método, agregue Hola después de la instrucción import:
   
        import com.amazon.device.messaging.ADM;
8. Agregar Hola siguiente código al final de Hola de hello `OnCreate` método:
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a>Agregar la aplicación de tooyour clave de API
1. En Eclipse, cree un nuevo archivo denominado **api_key.txt** en activos de hello directorio del proyecto.
2. Hola abrir archivo y copie Hola clave de API que generó en el portal para desarrolladores de Amazon Hola.

## <a name="run-hello-app"></a>Ejecutar aplicación hello
1. Inicie el emulador de Hola.
2. En el emulador de Windows hello, deslice el dedo desde la parte superior de Hola y haga clic en **configuración**y, a continuación, haga clic en **mi cuenta** y se registre con una cuenta válida de Amazon.
3. En Eclipse, ejecute la aplicación hello.

> [!NOTE]
> Si se produce un problema, compruebe la hora de hello del emulador de hello (o dispositivo). valor de tiempo de Hello debe ser precisa. tiempo de hello toochange del emulador en hello Kindle, puede ejecutar Hola siguiente comando desde el directorio de herramientas de la plataforma de SDK de Android:
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a>Envío de un mensaje
toosend un mensaje mediante el uso de. NET:

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[portal para desarrolladores de Amazon]: https://developer.amazon.com/home.html
[descargar Hola SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
