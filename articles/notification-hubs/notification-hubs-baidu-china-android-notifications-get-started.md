---
title: aaaGet a trabajar con los centros de notificaciones de Azure mediante Baidu | Documentos de Microsoft
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toopush notificaciones tooAndroid dispositivos que utilizan Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Introducción a Notification Hubs con Baidu
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Información general
Inserción de Baidu en la nube es un servicio de nube chino que pueden usar dispositivos de toomobile de notificaciones de inserción de toosend. Este servicio es útil en China, donde entregar notificaciones de inserción tooAndroid es compleja debido a la presencia de Hola de tiendas de aplicaciones diferentes e inserte contenido de servicios, además toohello disponibilidad de dispositivos Android que no están conectado normalmente tooGCM (Google La nube de mensajería).

## <a name="prerequisites"></a>Requisitos previos
Este tutorial requiere lo siguiente:

* SDK de Android (se supone que usa Eclipse), que puede descargar desde hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">sitio Android</a>
* [Android SDK para Mobile Services]
* [Baidu Push Android SDK]

> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).
> 
> 

## <a name="create-a-baidu-account"></a>Creación de una cuenta de Baidu
toouse Baidu, debe tener una cuenta de Baidu. Si ya tiene una, inicie sesión en toohello [Baidu portal] y omitir el paso siguiente toohello. En caso contrario, vea Hola siguiendo las instrucciones sobre cómo toocreate una cuenta de Baidu.  

1. Vaya toohello [Baidu portal] y haga clic en hello**登录**(**inicio de sesión**) vínculo. Haga clic en**立即注册**toostart proceso de registro de la cuenta de hello.
   
   ![][1]
2. Escriba los detalles de hello necesario, teléfono o correo electrónico código de comprobación, la contraseña y la dirección y haga clic en **suscripción**.
   
   ![][2]
3. Se le enviará una dirección de correo electrónico toohello de correo electrónico que escribió con un vínculo tooactivate su cuenta de Baidu.
   
   ![][3]
4. Inicie sesión en la cuenta de correo electrónico de tooyour, abra el correo electrónico de activación de Baidu hello y haga clic en tooactivate de vínculo de activación de Hola su cuenta de Baidu.
   
   ![][4]

Una vez que tenga una cuenta de Baidu activada, inicie sesión en toohello [Baidu portal].

## <a name="register-as-a-baidu-developer"></a>Registro como desarrollador de Baidu
1. Una vez que han iniciado sesión en toohello [Baidu portal], haga clic en**更多 >>** (**más**).
   
      ![][5]
2. Desplácese hacia abajo en hello**站长与开发者服务 (Administrador de Web y servicios para desarrolladores)** sección y haga clic en**百度开放云平台**(**Baidu abrir plataforma de nube**).
   
      ![][6]
3. En la página siguiente de hello, haga clic en**开发者服务**(**servicios para desarrolladores**) en la esquina superior derecha de Hola.
   
      ![][7]
4. En la página siguiente de hello, haga clic en**注册开发者**(**desarrolladores registrado**) desde el menú de hello en la esquina superior derecha de Hola.
   
      ![][8]
5. Escriba su nombre, una descripción y un número de teléfono móvil para recibir un mensaje de texto de verificación y, a continuación, haga clic en **送验证码** (**Enviar código de verificación**). Para números de teléfono internacional, es necesario código de país de hello tooenclose entre paréntesis. Por ejemplo, para un número de Estados Unidos, es **(1) 1234567890**.
   
      ![][9]
6. A continuación, debe recibir un mensaje de texto con un número de verificación, tal y como se muestra en el siguiente ejemplo de Hola:
   
      ![][10]
7. Introducir número de verificación de Hola de mensaje de saludo en**验证码**(**código de confirmación**).
8. Por último, completar el registro de desarrollador de hello Aceptar hello Baidu contrato y haga clic en**提交**(**enviar**). Verá Hola después de la página de finalización correcta del registro:
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>Creación de un proyecto de inserción de nube Baidu
Cuando se crea un proyecto de inserción de nube Baidu, recibirá el identificador de la aplicación, la clave de API y la clave secreta.

1. Una vez que han iniciado sesión en toohello [Baidu portal], haga clic en**更多 >>** (**más**).
   
      ![][5]
2. Desplácese hacia abajo en hello**站长与开发者服务**(**administrador del sitio Web y servicios para desarrolladores**) sección y haga clic en**百度开放云平台**(**Baidu abrir plataforma de nube**).
   
      ![][6]
3. En la página siguiente de hello, haga clic en**开发者服务**(**servicios para desarrolladores**) en la esquina superior derecha de Hola.
   
      ![][7]
4. En la página siguiente de hello, haga clic en**云推送**(**de inserción en la nube**) de hello**云服务**(**servicios en la nube**) sección.
   
      ![][12]
5. Una vez haya un desarrollador registrado, vea**管理控制台**(**Management Console**) en el menú superior Hola. Haga clic en **开发者服务管理** (**Administración de servicios de desarrolladores**).
   
      ![][13]
6. En la página siguiente de hello, haga clic en**创建工程**(**crear proyecto**).
   
      ![][14]
7. Escriba un nombre de aplicación y haga clic en **创建** (**Crear**).
   
      ![][15]
8. Tras crear correctamente un proyecto de Baidu Cloud Push, se mostrará una página con el **AppID**, la **clave de API** y la **clave secreta**. Tome nota de la clave de API de Hola y de clave secreta, que se utilizará más adelante.
   
      ![][16]
9. Configurar el proyecto de hello las notificaciones de inserción, haga clic en**云推送**(**nube inserción**) en el panel izquierdo de Hola.
   
      ![][31]
10. En la página siguiente de hello, haga clic en hello**推送设置**(**Insertar configuración**) botón.
    
    ![][32]  
11. En la página de configuración de hello, agregue el nombre de paquete de Hola que va a usar en el proyecto Android en hello**应用包名**(**paquete de aplicación**) campo y, a continuación, haga clic en**保存设置**() **Guardar**).  
    
    ![][33]

Vea hello**保存成功!** (**Guardado correctamente**).

## <a name="configure-your-notification-hub"></a>Configuración de su Centro de notificaciones
1. Inicie sesión en toohello [Portal clásico de Azure]y, a continuación, haga clic en **+ nuevo** final Hola de pantalla de bienvenida.
2. Haga clic sucesivamente en **App Services**, **Service Bus**, **Centro de notificaciones** y, finalmente, en **Creación rápida**.
3. Proporcione un nombre para su **centro de notificaciones**, seleccione hello **región** hello y **Namespace** donde se creará este centro de notificaciones y, a continuación, haga clic en  **Crear un nuevo centro de notificaciones**.  
   
      ![][17]
4. Haga clic en el espacio de nombres de hello en el que se creó el centro de notificaciones y, a continuación, haga clic en **centros de notificaciones** en la parte superior de Hola.
   
      ![][18]
5. Centro de notificaciones de hello SELECT que creó y, a continuación, haga clic en **configurar** de menú superior Hola.
   
      ![][19]
6. Desplácese hacia abajo toohello **configuración de notificaciones de baidu** sección y escriba la clave de API de hello y una clave secreta que obtuvo de la consola de Baidu Hola previamente para su proyecto de inserción de la nube de Baidu. Haga clic en **Guardar**.
   
      ![][20]
7. Haga clic en hello **panel** pestaña princip Hola Hola central de notificaciones y, a continuación, haga clic en **ver cadenas de conexión**.
   
      ![][21]
8. Tome nota de hello **DefaultListenSharedAccessSignature** y **DefaultFullSharedAccessSignature** de hello **acceso a la información de conexión** ventana.
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a>Conectar el centro de notificaciones de toohello de aplicación
1. En Eclipse ADT, cree un nuevo proyecto de Android (**File** > **New** > **Android Application Project**).
   
    ![][23]
2. Escriba un **nombre de la aplicación** y asegúrese de que hello **mínimo necesario SDK** versión se establece demasiado**API 16: Android 4.1**.
   
    ![][24]
3. Haga clic en **siguiente** y continuar después de Asistente de hello hasta hello **Crear actividad** aparecerá la ventana. Asegúrese de que **actividad en blanco** está seleccionada y, por último, seleccione **finalizar** toocreate una nueva aplicación de Android.
   
    ![][25]
4. Asegúrese de que ese hello **destino de compilación del proyecto** se ha establecido correctamente.
   
    ![][26]
5. Descargar archivo de bases de datos centrales de notificación de 0.4.jar de Hola de hello **archivos** ficha de hello [notificación-concentradores-Android-SDK en Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4). Agregar Hola archivo toohello **bibliotecas** carpeta del proyecto de Eclipse y actualización hello *bibliotecas* carpeta.
6. Descargue y descomprima hello [Baidu Push Android SDK], abra hello **bibliotecas** carpeta y, a continuación, Hola copia **pushservice x.y.z** jar hello y archivo **armeabi**  &  **mips** carpetas en hello **bibliotecas** carpeta de la aplicación Android.
7. Abra hello **AndroidManifest.xml** archivos de sus Android del proyecto y agregar permisos de hello requeridos por hello Baidu SDK.
   
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
8. Agregar Hola **android: name** propiedad tooyour **aplicación** elemento **AndroidManifest.xml**, reemplazando *NombreDelProyecto* (para ejemplo, **com.example.BaiduTest**). Asegúrese de que este nombre del proyecto coincide con hello uno que configuró en la consola de Baidu Hola.
   
        <application android:name="yourprojectname.DemoApplication"
9. Agregar Hola siguiente configuración en el elemento de la aplicación hello después hello **. MainActivity** elemento de actividad, reemplazando *NombreDelProyecto* (por ejemplo, **com.example.BaiduTest**):
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. Agregue una nueva clase denominada **ConfigurationSettings.java** toohello proyecto.
    
     ![][28]
    
     ![][29]
11. Agregue Hola después tooit de código:
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    Establecer valor de Hola de **API_KEY** con recuperar desde el proyecto de nube de Baidu Hola anteriormente, **NotificationHubName** con su nombre de base de datos central de notificaciones de hello Portal clásico de Azure y  **NotificationHubConnectionString** con DefaultListenSharedAccessSignature de hello Portal clásico de Azure.
12. Agregue una nueva clase denominada **DemoApplication.java**y agregue Hola después tooit de código:
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. Agregue otra nueva clase denominada **MyPushMessageReceiver.java**y agregue Hola después tooit de código. Es clase hello que identificadores Hola notificaciones de inserción que se reciben del servidor de inserción de Baidu Hola.
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
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
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
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
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. Abra **MainActivity.java**y agregue Hola después toohello **onCreate** método:
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. Abra Hola siguiendo las instrucciones de importación en la parte superior de hello:
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a>Enviar notificaciones tooyour aplicación
Puede probar rápidamente recibir notificaciones en la aplicación mediante el envío de notificaciones en hello [portal de Azure](https://portal.azure.com/) con hello **enviar** situado en el centro de notificaciones de hello, como se muestra en hello después de pantalla:

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

Las notificaciones push se envían normalmente en un servicio back-end como Mobile Services o ASP.NET mediante una biblioteca compatible. Si una biblioteca no está disponible para el back-end, puede usar API de REST de hello toosend directamente los mensajes de notificación.

En este tutorial, se mantenga simple y solo muestra probar la aplicación cliente mediante el envío de notificaciones mediante Hola .NET SDK centrales de notificaciones en una aplicación de consola en lugar de un servicio back-end. Se recomienda hello [toousers de notificaciones de los centros de notificaciones de uso toopush](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial como paso siguiente de Hola para enviar notificaciones desde un back-end ASP.NET. Sin embargo, Hola siguiendo métodos puede utilizarse para enviar notificaciones:

* **Interfaz REST**: admitir la notificación en cualquier plataforma de back-end mediante hello [interfaz REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **SDK de .NET de Microsoft Azure notificación concentradores**: Hola Administrador de paquetes de Nuget para Visual Studio, ejecutar [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**: [cómo toouse centros de notificaciones de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Aplicaciones móviles**: para obtener un ejemplo de cómo toosend notificaciones desde un back-end de aplicaciones de Mobile de servicio de aplicación de Azure que se integra con centros de notificaciones, consulte [Agregar aplicación móvil de inserción notificaciones tooyour](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: para obtener un ejemplo de cómo toosend notificaciones mediante el uso de hello las API de REST, vea "cómo toouse centros de notificaciones de Java y PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(Opcional) Envío de notificaciones desde una aplicación de consola .NET
En esta sección, mostramos cómo enviar una notificación mediante una aplicación de consola .NET.

1. Cree una aplicación de consola nueva de Visual C#:
   
    ![][30]
2. En la ventana de la consola de administrador de paquetes de saludo, establecer hello **proyecto predeterminado** tooyour nuevo proyecto de aplicación de consola y, a continuación, en la ventana de la consola de hello, ejecute hello siguiente comando:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Esta instrucción agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. Archivo abierto hello **Program.cs** y agregue Hola siguiente instrucción using:
   
        using Microsoft.Azure.NotificationHubs;
4. En su `Program` clase, agregue Hola siguiente método y reemplace *DefaultFullSharedAccessSignatureSASConnectionString* y *NotificationHubName* con valores de hello que tenga.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. Agregar Hola siguiendo las líneas en el **Main** método:
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>Prueba de la aplicación
tootest conectar esta aplicación con un teléfono real, simplemente Hola equipo tooyour de teléfono mediante un cable USB. Esta acción carga la aplicación en el teléfono de hello adjuntada.

tootest esta aplicación con el emulador de Windows hello, en la barra de herramientas superior de hello Eclipse, haga clic en ejecutar **ejecutar**y, a continuación, seleccione la aplicación: se inicia el emulador de Windows hello, carga, y se ejecuta Hola aplicación.

aplicación Hello recupera hello 'userId' y 'channelId' de hello servicio de notificaciones de inserción de Baidu y se registra con el centro de notificaciones de Hola.

toosend una notificación de prueba, puede utilizar la pestaña depurar de Hola de hello Portal clásico de Azure. Si ha creado la aplicación de consola .NET de Hola para Visual Studio, simplemente presione tecla F5 de hello en aplicaciones de Visual Studio toorun Hola. aplicación Hello envía una notificación que aparece en el área de notificación superior de Hola de su dispositivo o emulador.

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Android SDK para Mobile Services]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[Portal clásico de Azure]: https://manage.windowsazure.com/
[Baidu portal]: http://www.baidu.com/
