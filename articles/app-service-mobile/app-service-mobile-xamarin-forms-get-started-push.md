---
title: "aaaAdd inserción notificaciones tooyour Xamarin.Forms aplicación | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Azure services toosend multiplataforma inserción notificaciones tooyour Xamarin.Forms aplicaciones."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a>Agregar aplicación de Xamarin.Forms de tooyour de notificaciones de inserción
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Información general
En este tutorial, agregará proyectos Hola de tooall de notificaciones de inserción que dan como resultado de hello [inicio rápido de Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md). Esto significa que se envía una notificación de inserción clientes multiplataforma de tooall cada vez que se inserta un registro.

Si no usa Hola descarga el proyecto de servidor de inicio rápido, se necesita Hola paquete de extensión de notificación de inserción. Para obtener más información, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Requisitos previos
Para iOS, necesitará una [suscripción de Apple Developer Program](https://developer.apple.com/programs/ios/) y un dispositivo de iOS físico. Hola [simulador de iOS no admite notificaciones de inserción](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).

## <a name="configure-hub"></a>Configurar un Centro de notificaciones
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Actualizar notificaciones de inserción de hello servidor proyecto toosend
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a>Configurar y ejecutar el proyecto de Android de hello (opcional)
Completar esta sección tooenable las notificaciones de inserción hello Xamarin.Forms Droid proyecto para Android.

### <a name="enable-firebase-cloud-messaging-fcm"></a>Habilitar la mensajería en la nube Firebase (FCM)
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a>Configurar solicitudes de inserción de hello aplicaciones móviles back-end toosend mediante FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a>Agregar proyecto de Android de toohello de notificaciones de inserción
Con hello back-end configurado con FCM, puede agregar componentes y códigos tooregister de cliente de toohello con FCM. También puede registrar las notificaciones de inserción con centros de notificaciones de Azure a través de hello aplicaciones móviles volver finalizar y recibir notificaciones.

1. Hola **Droid** proyecto de equipo y haga clic en hello **componentes** carpeta y haga clic en **obtener más componentes de...** . A continuación, busque hello **el cliente de mensajería de nube de Google** componente y agregue el proyecto de toohello. Este componente es compatible con las notificaciones push para un proyecto de Xamarin para Android.
2. Abrir archivo de proyecto de hello MainActivity.cs y agregue Hola siguiente instrucción al principio de hello del archivo de hello:

        using Gcm.Client;
3. Agregar Hola después código toohello **OnCreate** llamada al método después de hello demasiado**LoadApplication**:

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. Agregue un nuevo método auxiliar **CreateAndShowDialog** , como sigue:

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. Agregar Hola después código toohello **MainActivity** clase:

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    Esto expone Hola actual **MainActivity** de instancia, por lo que podemos ejecutar en el subproceso de interfaz de usuario principal de Hola.
6. Inicializar hello `instance` variable al principio de Hola de hello **OnCreate** método, tal como se indica a continuación.

        // Set hello current instance of MainActivity.
        instance = this;
7. Agregar un nuevo toohello de archivo de clase **Droid** proyecto denominado `GcmService.cs`y asegúrese de seguro siguiente hello **con** instrucciones están presentes en la parte superior de hello del archivo hello:

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. Agregar Hola siguiendo las solicitudes de permiso al principio de hello del archivo de hello, después de hello **con** instrucciones y antes de hello **espacio de nombres** declaración.

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. Agregar Hola tras el espacio de nombres de clase definición toohello.

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > Reemplace **<PROJECT_NUMBER>** por el número de proyecto que anotó antes.    
   >
   >
10. Reemplace Hola vacía **GcmService** clase con hello siguiente código, que usa el receptor de difusión de hello nueva:

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. Agregar Hola después código toohello **GcmService** clase. Esto invalida hello **OnRegistered** controlador de eventos e implementa un **registrar** método.

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    Tenga en cuenta que este código usa hello `messageParam` parámetro en el registro de plantilla de Hola.
12. Agregar Hola después el código que implementa **OnMessage**:

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    Esto controla las notificaciones entrantes y los envía toobe manager toohello notificación que muestra.
13. **GcmServiceBase** también requiere hello tooimplement **OnUnRegistered** y **OnError** métodos de controlador, lo que puede hacer lo siguiente:

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

Ahora, está listo pruebas notificaciones de inserción en la aplicación hello que se ejecuta en un dispositivo Android u Hola emulador.

### <a name="test-push-notifications-in-your-android-app"></a>Prueba de las notificaciones push en la aplicación de Android
Hola dos primeros pasos son necesarios cuando se está probando en un emulador.

1. Asegúrese de que se va a implementar tooor depuración en un dispositivo virtual que tiene Google APIs establecer como destino de hello, tal y como se muestra a continuación, en el Administrador de dispositivos virtuales Android Hola.
2. Agregar un dispositivo Android de Google cuenta toohello haciendo clic en **aplicaciones** > **configuración** > **Agregar cuenta**. A continuación, siga Hola indicaciones tooadd un dispositivo existente de toohello de cuenta de Google o toocreate uno nuevo.
3. En Visual Studio o Xamarin Studio, haga clic en hello **Droid** del proyecto y haga clic en **establecer como proyecto de inicio**.
4. Haga clic en **ejecutar** toobuild Hola proyecto e iniciar aplicación hello en el emulador o dispositivo Android.
5. En la aplicación hello, escriba una tarea y, a continuación, haga clic en hello signo más (**+**) icono.
6. Compruebe que se recibe una notificación cuando se agrega un artículo.

## <a name="configure-and-run-hello-ios-project-optional"></a>Configurar y ejecutar el proyecto de iOS de hello (opcional)
Esta sección es para ejecutar el proyecto de iOS de Xamarin Hola para dispositivos iOS. Puede omitir esta sección si no está trabajando con dispositivos iOS.

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a>Centro de notificaciones de Hola de configuración de APNS
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

A continuación, configurará configuración del proyecto de iOS de hello en Xamarin Studio o Visual Studio.

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a>Agregar aplicación de iOS de tooyour de notificaciones de inserción
1. Hola **iOS** del proyecto, abra AppDelegate.cs y agregue Hola después de la parte superior de toohello de instrucción del archivo de código de hello.

        using Newtonsoft.Json.Linq;
2. Hola **AppDelegate** de clases, agregue una invalidación para hello **RegisteredForRemoteNotifications** tooregister de eventos para las notificaciones:

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. En **AppDelegate**, agregar Hola después de invalidación para hello **DidReceiveRemoteNotification** controlador de eventos:

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    Este método controla las notificaciones entrantes mientras se ejecuta la aplicación hello.
4. Hola **AppDelegate** clase, agregue Hola después código toohello **FinishedLaunching** método:

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    Tras esto, se habilita la compatibilidad con las notificaciones remotas y el registro de inserción de solicitudes.

La aplicación ya está actualizado toosupport notificaciones de inserción.

#### <a name="test-push-notifications-in-your-ios-app"></a>Prueba de las notificaciones push en su aplicación de iOS
1. Haga clic en proyecto de iOS de Hola y haga clic en **establecer como proyecto de inicio**.
2. Hola presione **ejecutar** botón o **F5** en Visual Studio toobuild Hola proyecto e iniciar aplicación hello en un dispositivo iOS. A continuación, haga clic en **Aceptar** tooaccept notificaciones de inserción.

   > [!NOTE]
   > Debe aceptar de forma explícita las notificaciones push desde su aplicación. Esta solicitud sólo produce a Hola primera vez que Hola se ejecuta la aplicación.
   >
   >
3. En la aplicación hello, escriba una tarea y, a continuación, haga clic en hello signo más (**+**) icono.
4. Compruebe que se recibe una notificación y, a continuación, haga clic en **Aceptar** toodismiss Hola notificación.

## <a name="configure-and-run-windows-projects-optional"></a>Configuración y ejecución de proyectos de Windows (opcional)
En esta sección es para ejecutar Hola Xamarin.Forms WinApp y WinPhone81 proyectos para dispositivos de Windows. Estos pasos también son compatibles con los proyectos de Plataforma universal de Windows (UWP). Puede omitir esta sección si no está trabajando con dispositivos Windows.

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a>Registro de la aplicación de Windows para notificaciones de inserción en el Servicio de notificaciones de Windows (WNS)
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a>Centro de notificaciones de Hola de configuración de WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a>Agregar aplicación de Windows de tooyour de notificaciones de inserción
1. En Visual Studio, abra **App.xaml.cs** en una ventana de proyecto y agregar Hola siguiendo las instrucciones.

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    Reemplace `<your_TodoItemManager_portable_class_namespace>` con hello espacio de nombres del proyecto portátil que contiene Hola `TodoItemManager` clase.
2. En App.xaml.cs, agregue el siguiente de hello **InitNotificationsAsync** método:

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    Este método obtiene el canal de notificación de inserción de Hola y registra un notificaciones de plantilla de tooreceive plantilla desde el centro de notificaciones. Una notificación de plantilla que admita *messageParam* se entregarán toothis cliente.
3. En App.xaml.cs, actualice hello **OnLaunched** definición de método de controlador de eventos mediante la adición de hello `async` modificador. A continuación, agregue Hola después de la línea de código al final de hello del método hello:

        await InitNotificationsAsync();

    Esto garantiza que se crea o se actualiza cada vez que se inicia la aplicación hello registro de notificaciones de inserción de Hola. Es importante toodo esta tooguarantee que Hola WNS inserción canal siempre está activo.  
4. En el Explorador de soluciones de Visual Studio, abra hello **Package.appxmanifest** de archivos y establecer **capaz de recibir** demasiado**Sí** en **notificaciones**.
5. Compilar la aplicación hello y compruebe que no dispone de ningún error. La aplicación cliente ahora debe registrar para notificaciones de plantilla de Hola de hello que terminar de aplicaciones móviles de nuevo. Repita esta sección para cada proyecto de Windows de la solución.

#### <a name="test-push-notifications-in-your-windows-app"></a>Prueba de las notificaciones push en su aplicación de Windows
1. En Visual Studio, haga clic con el botón derecho en un proyecto de Windows y luego haga clic en **Establecer como proyecto de inicio**.
2. Hola presione **ejecutar** botón proyecto de hello toobuild e iniciar la aplicación hello.
3. En la aplicación hello, escriba un nombre para un todoitem nueva y, a continuación, haga clic en hello signo más (**+**) tooadd de icono.
4. Compruebe que se recibe una notificación cuando se agrega el elemento de saludo.

## <a name="next-steps"></a>Pasos siguientes
Puede obtener más información sobre las notificaciones de inserción:

* [Diagnosticar problemas de notificaciones push](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  : existen varias razones para que las notificaciones se pierdan o no lleguen a los dispositivos. Este tema muestra cómo hacer que tooanalyze y averiguar la raíz de Hola de errores de notificación de inserción.

También puede seguir en tooone de hello tutoriales:

* [Agregar aplicación de autenticación tooyour](app-service-mobile-xamarin-forms-get-started-users.md)  
  Obtenga información acerca de cómo tooauthenticate a los usuarios de la aplicación con un proveedor de identidades.
* [Activación de la sincronización sin conexión para la aplicación de Windows](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Obtenga información acerca de cómo tooadd compatibilidad sin conexión para la aplicación mediante el uso de aplicaciones móviles de un back-end. La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;aun cuando no haya conexión de red.

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
