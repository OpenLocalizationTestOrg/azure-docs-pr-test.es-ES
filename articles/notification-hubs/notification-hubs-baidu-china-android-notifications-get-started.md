---
title: "Introducción a Notification Hubs con Baidu | Microsoft Docs"
description: "En este tutorial aprenderá a usar Azure Notification Hubs para enviar notificaciones push a dispositivos Android mediante Baidu."
services: notification-hubs
documentationcenter: android
author: kpiteira
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/29/2017
ms.author: kapiteir
ms.openlocfilehash: 91f20a6e0ff6c2dd512879e9ab3c9369dab5d8ff
ms.sourcegitcommit: 5735491874429ba19607f5f81cd4823e4d8c8206
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Introducción a Notification Hubs con Baidu
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

La inserción de nube Baidu es un servicio de nube chino que puede utilizar para enviar notificaciones de inserción a dispositivos móviles. 

Dado que Google Play y FCM (Firebase Cloud Messaging) no están disponibles en China, es necesario usar tiendas de aplicaciones y servicios push diferentes. Baidu es uno de ellos y el utilizado actualmente por Notifications Hub.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial requiere lo siguiente:

* Android SDK (damos por hecho que usa Android Studio), que puede descargar en el <a href="http://go.microsoft.com/fwlink/?LinkId=389797">sitio de Android</a>
* [Baidu Push Android SDK]

> [!NOTE]
> Para completar este tutorial, deberá tener una cuenta de Azure activa. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).
> 
> 

## <a name="create-a-baidu-account"></a>Creación de una cuenta de Baidu
Para usar Baidu, tiene que tener una cuenta de Baidu. Si ya tiene una, inicie sesión en el [portal de Baidu] y vaya al paso siguiente. De lo contrario, consulte las siguientes instrucciones sobre cómo crear una cuenta de Baidu.  

1. Vaya al [portal de Baidu] y haga clic en el vínculo **登录** (**Iniciar sesión**). Haga clic en **立即注册** (**Registrarse ahora**) para iniciar el proceso de registro de cuenta.
   
    ![Registro de Baidu](./media/notification-hubs-baidu-get-started/BaiduRegistration.png)

2. Especifique los detalles necesarios (teléfono o dirección de correo electrónico, la contraseña y el código de verificación) y haga clic en 注册 **Suscripción**.
   
    ![Entrada del registro de Baidu](./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png)

3. Se le envía un mensaje de correo electrónico a la dirección que especificó con un vínculo para activar su cuenta de Baidu.
   
    ![Confirmación del registro de Baidu](./media/notification-hubs-baidu-get-started/BaiduConfirmation.png)

4. Inicie sesión en su cuenta de correo electrónico, abra el mensaje de correo electrónico de activación de Baidu y haga clic en el vínculo de activación para activar su cuenta de Baidu.
   
    ![Correo electrónico de activación de Baidu](./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png)

Una vez activada la cuenta de Baidu, inicie sesión en el [portal de Baidu].

## <a name="create-a-baidu-cloud-push-project"></a>Creación de un proyecto de inserción de nube Baidu
Cuando se crea un proyecto de inserción de nube Baidu, recibirá el identificador de la aplicación, la clave de API y la clave secreta.

1. Una vez que haya iniciado sesión en el [portal de Baidu], haga clic en **更多 >>** (**más**).
   
    ![Registro: más](./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png)

2. Desplácese hacia abajo en la sección **站长与开发者服务** (**Administrador de web y servicios para desarrolladores**) y haga clic en **百度开放云平台** (**Baidu Cloud Push**).
   
    ![Plataforma de nube abierta de Baidu](./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png)

3. En la siguiente página, haga clic en **登录** (**Inicio de sesión**) en la esquina superior derecha.
   
    ![Inicio de sesión de Baidu](./media/notification-hubs-baidu-get-started/BaiduLogin.png)

4. A continuación, haga clic en**创建应用** (**Crear aplicación**) en esta página.

    ![Crear aplicación de Baidu](./media/notification-hubs-baidu-get-started/BaiduCreateApplication.png)

5. En la siguiente página, haga clic en 创建新应用 (**Crear nueva aplicación**).
   
    ![Crear nueva aplicación de Baidu](./media/notification-hubs-baidu-get-started/BaiduCreateNewApplication.png)

6. Escriba un nombre de aplicación y haga clic en 创建 (**Crear**).
   
    ![](./media/notification-hubs-baidu-get-started/BaiduCreateApplicationDoCreate.png)

7. Tras crear correctamente un proyecto de Baidu Cloud Push, se mostrará una página con el **AppID**, la **clave de API** y la **clave secreta**. Tome nota de la clave de API y la clave secreta que se usarán más adelante.
   
    ![Secretos de inserción de Baidu](./media/notification-hubs-baidu-get-started/BaiduGetSecrets.png)

8. Configure el proyecto para las notificaciones push haciendo clic en 云推送 (**Crear notificación**) en el panel izquierdo.
   
    ![](./media/notification-hubs-baidu-get-started/BaiduCreateNotification.png)


## <a name="configure-a-new-notification-hub"></a>Configuración de un centro de notificaciones nuevo
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]


&emsp;&emsp;6. En su centro de notificaciones, seleccione **Notification Services** (Servicios de notificaciones) y, luego, **Baidu (Android China)**.

&emsp;&emsp;![Centros de notificaciones de Azure: Baidu](./media/notification-hubs-baidu-get-started/AzureNotificationServicesBaidu.png)

&emsp;&emsp;7. Desplácese hasta la sección de configuración de notificaciones de Baidu. Escriba la clave de API y la clave secreta que ha obtenido en la consola de Baidu, en el proyecto Baidu Cloud Push. A continuación, haga clic en Guardar.

&emsp;&emsp;![Centros de notificaciones de Azure: secretos de Baidu](./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png)

El centro de notificaciones ya está configurado para funcionar con Baidu. También tiene las **cadenas de conexión** para registrar la aplicación tanto para enviar como para recibir notificaciones push.

Tome nota del valor de `DefaultListenSharedAccessSignature` y de `DefaultFullSharedAccessSignature` desde la ventana de información de conexión de acceso.

## <a name="connect-your-app-to-the-notification-hub"></a>Conexión de la aplicación al Centro de notificaciones
1. En Android Studio, cree un nuevo proyecto de Android (Archivo > Nuevo > Nuevo proyecto).

    ![Centros de notificaciones de Azure: nuevo proyecto de Baidu](./media/notification-hubs-baidu-get-started/AndroidNewProject.png)

2.  Escriba un nombre de la aplicación y asegúrese de que la versión de SDK mínima requerido esté establecida en API 16: Android 4.1. **Asegúrese también de que el nombre del paquete (应用包名) es el mismo que en el portal de Baidu Cloud Push**

    ![Azure Notifications Hubs: Baidu Min SDK1](./media/notification-hubs-baidu-get-started/AndroidMinSDK.png)
    ![Azure Notifications Hubs: Baidu Min SDK2](./media/notification-hubs-baidu-get-started/AndroidMinSDK2.png)

3.  Haga clic en Siguiente y siga las instrucciones del asistente hasta llegar a la ventana Create Activity (Crear actividad). Asegúrese de que está seleccionada la opción Empty Activity (Actividad vacía) y, finalmente, seleccione Finish (Finalizar) para crear una nueva aplicación de Android.

    ![Centros de notificaciones de Azure: agregar actividad de Baidu](./media/notification-hubs-baidu-get-started/AndroidAddActivity.png)

4.  Asegúrese de que Project Build Target (Destino de compilación del proyecto) esté establecido correctamente.

5.  Después, agregue las bibliotecas de Azure Notification Hubs. En el archivo `Build.Gradle` de la aplicación, agregue las siguientes líneas en la sección de dependencias.

    ```javascript
    compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
    ```

    Agregue el repositorio siguiente después de la sección de dependencias.

    ```javascript
    repositories {
        maven {
            url "http://dl.bintray.com/microsoftazuremobile/SDK"
        }
    }
    ```

    Para evitar el conflicto de la lista, es necesario que agregue el siguiente código en **Manifest.xml**.

    ```xml
    <manifest package="YOUR.PACKAGE.NAME"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:android="http://schemas.android.com/apk/res/android">
    ```

    y, en la etiqueta `<application/>`:

    ```xml
    <application
        tools:replace="android:allowBackup,icon,theme,label">
    ```

6.  Descargue y descomprima [Baidu Push Android SDK]. Copie el archivo `pushservice-x.y.z jar` en la carpeta de bibliotecas. A continuación, copie los archivos `.so` en las carpetas `src/main/jniLibs` (cree una nueva carpeta) de la aplicación Android.

    ![Azure Notification Hubs: bibliotecas del SDK de Baidu](./media/notification-hubs-baidu-get-started/BaiduSDKLib.png)

7. Haga clic con el botón derecho en el archivo pushervice-x.y.z.jar en la carpeta de bibliotecas, y haga clic en Agregar como biblioteca para incluir esta biblioteca en el proyecto.

    ![Azure Notifications Hubs: agregar como biblioteca de Baidu](./media/notification-hubs-baidu-get-started/BaiduAddAsALib.jpg)

8. Abra el archivo **AndroidManifest.xml** de su proyecto de Android y agregue los permisos que requiere el SDK de Baidu. **Reemplace `YOURPACKAGENAME` con el nombre del paquete**.

    ```xml
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
    <uses-permission android:name="android.permission.WRITE_SETTINGS" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
    <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
    <uses-permission android:name="android.permission.EXPAND_STATUS_BAR" />
    !! <uses-permission android:name="baidu.push.permission.WRITE_PUSHINFOPROVIDER.YOURPACKAGENAME" />
    !!<permission android:name="baidu.push.permission.WRITE_PUSHINFOPROVIDER.YOURPACKAGENAME"android:protectionLevel="normal" />

    ```

9. Agregue la siguiente configuración al elemento application después del elemento de actividad `.MainActivity` reemplazando *yourprojectname* (por ejemplo, `com.example.BaiduTest`):

    ```xml
    <activity
        android:name="com.baidu.android.pushservice.richmedia.MediaViewActivity"
        android:configChanges="orientation|keyboardHidden"
        android:label="MediaViewActivity" />
    <activity
        android:name="com.baidu.android.pushservice.richmedia.MediaListActivity"
        android:configChanges="orientation|keyboardHidden"
        android:label="MediaListActivity"
        android:launchMode="singleTask" />
 
    <!-- Push application definition message -->
    <receiver android:name=".MyPushMessageReceiver">
        <intent-filter>

            <!-- receive push message-->
            <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
            <!-- receive bind,unbind,fetch,delete.. message-->
            <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
            <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
        </intent-filter>
    </receiver>

    <receiver
        android:name="com.baidu.android.pushservice.PushServiceReceiver"
        android:process=":bdservice_v1">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
            <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
            <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            <action android:name="com.baidu.android.pushservice.action.media.CLICK" />
            <action android:name="android.intent.action.MEDIA_MOUNTED" />
            <action android:name="android.intent.action.USER_PRESENT" />
            <action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
            <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
        </intent-filter>
    </receiver>

    <receiver
        android:name="com.baidu.android.pushservice.RegistrationReceiver"
        android:process=":bdservice_v1">
        <intent-filter>
            <action android:name="com.baidu.android.pushservice.action.METHOD" />
            <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
        </intent-filter>
        <intent-filter>
            <action android:name="android.intent.action.PACKAGE_REMOVED" />

            <data android:scheme="package" />
        </intent-filter>
    </receiver>

    <service
        android:name="com.baidu.android.pushservice.PushService"
        android:exported="true"
        android:process=":bdservice_v1">
        <intent-filter>
            <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
        </intent-filter>
    </service>

    <service
        android:name="com.baidu.android.pushservice.CommandService"
        android:exported="true" />

    <!-- Adapt the ContentProvider declaration required for the Android N system, and the write permissions include the application package name-->
    <provider
        android:name="com.baidu.android.pushservice.PushInfoProvider"
        android:authorities="com.baidu.push.example.bdpush"
        android:exported="true"
        android:protectionLevel="signature"
        android:writePermission="baidu.push.permission.WRITE_PUSHINFOPROVIDER. yourprojectname  " />

    <!-- API Key of the Baidu application -->
    <meta-data
        android:name="api_key"
        !!   android:value="api_key" />
    </application>
    ```

10. Agregue una nueva clase denominada `ConfigurationSettings.java` al proyecto.

    ```java
    public class ConfigurationSettings {
        public static String API_KEY = "...";
        public static String NotificationHubName = "...";
        public static String NotificationHubConnectionString = "...";
    }
    ```
    
    Establezca el valor de la cadena `API_KEY` con el valor de API_KEY desde Baidu Cloud Project.
    
    Establezca el valor de la cadena `NotificationHubName`con el nombre del centro de notificaciones desde [Azure Portal]; y, a continuación, `NotificationHubConnectionString` con `DefaultListenSharedAccessSignature` desde [Azure Portal].

11. Abra MainActivity.java y agregue lo siguiente al método onCreate:

    ```java
    PushManager.startWork(this, PushConstants.LOGIN_TYPE_API_KEY,  API_KEY );
    ```

12. Agregue una nueva clase denominada `MyPushMessageReceiver.java` y agréguele el código siguiente. Es la clase que controla las notificaciones push que se reciben del servidor push de Baidu.

    ```java
    package your.package.name;

    import android.content.Context;
    import android.content.Intent;
    import android.os.AsyncTask;
    import android.text.TextUtils;
    import android.util.Log;

    import com.baidu.android.pushservice.PushMessageReceiver;
    import com.microsoft.windowsazure.messaging.NotificationHub;
    import org.json.JSONException;
    import org.json.JSONObject;

    import java.util.List;

    public class MyPushMessageReceiver extends PushMessageReceiver {

        public static final String TAG = MyPushMessageReceiver.class
                .getSimpleName();
        public static NotificationHub hub = null;
        public static String mChannelId, mUserId;

        @Override
        public void onBind(Context context, int errorCode, String appid,
                        String userId, String channelId, String requestId) {
            String responseString = "onBind errorCode=" + errorCode + " appid="
                    + appid + " userId=" + userId + " channelId=" + channelId
                    + " requestId=" + requestId;
            Log.d(TAG, responseString);

            if (errorCode == 0) {
                // Binding successful
                Log.d(TAG, " Binding successful");
            }
            try {
                if (hub == null) {
                    hub = new NotificationHub(
                            ConfigurationSettings.NotificationHubName,
                            ConfigurationSettings.NotificationHubConnectionString,
                            context);
                    Log.i(TAG, "Notification hub initialized");
                }
            } catch (Exception e) {
                Log.e(TAG, e.getMessage());
            }
            mChannelId = channelId;
            mUserId = userId;

            registerWithNotificationHubs();
        }
        private void registerWithNotificationHubs() {

            new AsyncTask<Void, Void, Void>() {
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        hub.registerBaidu(mUserId, mChannelId);
                        Log.i(TAG, "Registered with Notification Hub - '"
                                + ConfigurationSettings.NotificationHubName + "'"
                                + " with UserId - '"
                                + mUserId + "' and Channel Id - '"
                                + mChannelId + "'");
                    } catch (Exception e) {
                        Log.e(TAG, e.getMessage());
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

        @Override
        public void onMessage(Context context, String message,
                            String customContentString) {
            String messageString = " onMessage=\"" + message
                    + "\" customContentString=" + customContentString;
            Log.d(TAG, messageString);
            if (!TextUtils.isEmpty(customContentString)) {
                JSONObject customJson = null;
                try {
                    customJson = new JSONObject(customContentString);
                    String myvalue = null;
                    if (!customJson.isNull("mykey")) {
                        myvalue = customJson.getString("mykey");
                    }
                } catch (JSONException e) {
                    e.printStackTrace();
                }
            }

        }

        @Override
        public void onNotificationArrived(Context context, String title, String description, String customContentString) {
            String notifyString = " Notice Arrives onNotificationArrived  title=\"" + title
                    + "\" description=\"" + description + "\" customContent="
                    + customContentString;
            Log.d(TAG, notifyString);
            if (!TextUtils.isEmpty(customContentString)) {
                JSONObject customJson = null;
                try {
                    customJson = new JSONObject(customContentString);
                    String myvalue = null;
                    if (!customJson.isNull("mykey")) {
                        myvalue = customJson.getString("mykey");
                    }
                } catch (JSONException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                }
            }
        }

        @Override
        public void onNotificationClicked(Context context, String title, String description, String customContentString) {
            String notifyString = " onNotificationClicked title=\"" + title + "\" description=\""
                    + description + "\" customContent=" + customContentString;
            Log.d(TAG, notifyString);
            Intent intent = new Intent(context.getApplicationContext(),MainActivity.class);
            intent.putExtra("title",title);
            intent.putExtra("description",description);
            intent.putExtra("isFromNotify",true);
            intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
            context.getApplicationContext().startActivity(intent);

        }

        @Override
        public void onSetTags(Context context, int errorCode,
                            List<String> successTags, List<String> failTags, String requestId) {
            String responseString = "onSetTags errorCode=" + errorCode
                    + " successTags=" + successTags + " failTags=" + failTags
                    + " requestId=" + requestId;
            Log.d(TAG, responseString);

        }

        @Override
        public void onDelTags(Context context, int errorCode,
                            List<String> successTags, List<String> failTags, String requestId) {
            String responseString = "onDelTags errorCode=" + errorCode
                    + " successTags=" + successTags + " failTags=" + failTags
                    + " requestId=" + requestId;
            Log.d(TAG, responseString);

        }

        @Override
        public void onListTags(Context context, int errorCode, List<String> tags,
                            String requestId) {
            String responseString = "onListTags errorCode=" + errorCode + " tags="
                    + tags;
            Log.d(TAG, responseString);

        }

        @Override
        public void onUnbind(Context context, int errorCode, String requestId) {
            String responseString = "onUnbind errorCode=" + errorCode
                    + " requestId = " + requestId;
            Log.d(TAG, responseString);

            if (errorCode == 0) {
                // Unbinding is successful
                Log.d(TAG, " Unbinding is successful ");
            }
        }
    }
    ```

## <a name="send-notifications-to-your-app"></a>Envío de notificaciones a la aplicación

Para probar de forma rápida la recepción de notificaciones desde [Azure Portal]: use el botón **Enviar** en la pantalla de configuración del centro de notificaciones, tal como se muestra en las pantallas que aparecen a continuación:

![](./media/notification-hubs-baidu-get-started/BaiduTestSendButton.png)
![](./media/notification-hubs-baidu-get-started/BaiduTestSend.png)

Las notificaciones push se envían normalmente en un servicio back-end como Mobile Services o ASP.NET mediante una biblioteca compatible. Si no hay disponible una biblioteca para su back-end, puede usar la API de REST directamente para enviar mensajes de notificación.

Por simplicidad, este tutorial utiliza una aplicación de consola como demostración sobre cómo enviar una notificación con el SDK de .NET. Sin embargo, se recomienda seguir el tutorial [Azure Notification Hubs notifica a los usuarios con back-end de .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) como paso siguiente para enviar notificaciones desde un back-end de ASP.NET. 

Estos son los distintos enfoques para enviar notificaciones:
* **Interfaz de REST**: puede admitir notificaciones en cualquier plataforma de back-end mediante la [interfaz de REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **SDK para .NET de Microsoft Azure Notification Hubs**: en el Administrador de paquetes NuGet para Visual Studio, ejecute [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**: [Uso de Notification Hubs desde Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Mobile Apps**: para ver un ejemplo de cómo enviar notificaciones desde un back-end de Azure App Service Mobile Apps integrado en Notification Hubs, consulte [Incorporación de notificaciones push a la aplicación móvil](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: para ver un ejemplo de cómo enviar notificaciones con las API de REST, consulte "Uso de Notification Hubs desde Java o PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(Opcional) Envío de notificaciones desde una aplicación de consola .NET
En esta sección, mostramos cómo enviar una notificación mediante una aplicación de consola .NET.

1. Cree una aplicación de consola nueva de Visual C#:
   
    ![](./media/notification-hubs-baidu-get-started/ConsoleProject.png)

2. En la ventana de la Consola del Administrador de paquetes, seleccione en **Proyecto predeterminado** el nuevo proyecto de aplicación de consola y, a continuación, ejecute el siguiente comando en la ventana de la consola:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Esta instrucción agrega una referencia al SDK de Azure Notification Hubs mediante el <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet Microsoft.Azure.NotificationHubs</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)

3. Abra el archivo `Program.cs` y agregue la siguiente instrucción using:
   
    ```csharp
    using Microsoft.Azure.NotificationHubs;
    ```

4. En la clase `Program`, agregue el método siguiente y reemplace `DefaultFullSharedAccessSignatureSASConnectionString` y `NotificationHubName` con los valores que tenga.
   
    ```csharp
    private static async void SendNotificationAsync()
    {
        NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
        string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
        var result = await hub.SendBaiduNativeNotificationAsync(message);
    }
    ```

5. Agregue las siguientes líneas al método `Main` :

    ```csharp
    SendNotificationAsync();
    Console.ReadLine();
    ```

## <a name="test-your-app"></a>Prueba de la aplicación

Para realizar una prueba de la aplicación con un teléfono real, conéctelo al equipo mediante un cable USB. Esta acción carga la aplicación en el teléfono vinculado.

Para probar esta aplicación con el emulador, en la barra de herramientas superior de Android Studio, haga clic en **Run**(Ejecutar) y seleccione la aplicación: se inicia el emulador y se carga y ejecuta la aplicación.

La aplicación recupera los valores de `userId` y `channelId` desde el servicio de notificaciones push de Baidu y se registra con el centro de notificaciones.

Para enviar una notificación de prueba, puede usar la pestaña de depuración de [Azure Portal]. Si compila la aplicación de la consola .NET para Visual Studio, presione simplemente la tecla F5 en Visual Studio para ejecutar la aplicación. La aplicación envía una notificación que aparece en el área de notificación superior del dispositivo o emulador.

<!-- URLs. -->
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu Push Android SDK]: http://push.baidu.com/sdk/push_client_sdk_for_android
[Azure Portal]: https://portal.azure.com/
[portal de Baidu]: http://www.baidu.com/
