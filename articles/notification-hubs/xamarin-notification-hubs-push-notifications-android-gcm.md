---
title: aaaGet a trabajar con los centros de notificaciones para las aplicaciones de Xamarin.Android | Documentos de Microsoft
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toosend push notificaciones tooa aplicación Xamarin para Android."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a>Introducción a Centros de notificaciones con Xamarin para Android
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Información general
Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push aplicación de notificaciones de tooa Xamarin.Android.
Creará una aplicación Xamarin.Android en blanco que reciba notificaciones push mediante el servicio de mensajería en la nube de Google (GCM). Cuando haya terminado, podrá toouse capaz de su toobroadcast de base de datos central de notificaciones de inserción dispositivos Hola notificaciones tooall que ejecuta la aplicación. Hello terminado código está disponible en hello [NotificationHubs aplicación] [ GitHub] ejemplo.

Este tutorial muestra el escenario sencillo de difusión hello en usar centros de notificaciones.

## <a name="before-you-begin"></a>Antes de empezar
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

código de Hello completado para este tutorial se puede encontrar en GitHub [aquí](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).

## <a name="prerequisites"></a>Requisitos previos
Este tutorial requiere siguiente de hello:

* Las instrucciones de instalación completas de Visual Studio con Xamarin en Windows o Xamarin Studio en Mac OS X se encuentran en [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx).
* Cuenta de Google activa
* [Componente de mensajería de Azure]
* [Componente del Cliente de mensajería en la nube de Google]

Completar este tutorial es un requisito previo para todos los demás tutoriales de Centros de notificaciones para aplicaciones Xamarin.Android.

> [!IMPORTANT]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).
> 
> 

## <a name="enable-google-cloud-messaging"></a>Habilitación del servicio de mensajería en la nube de Google
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a>Configuración de su Centro de notificaciones
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p>Haga clic en hello <b>configurar</b> ficha en la parte superior de hello, escriba Hola <b>clave de API</b> valor obtenidas en la sección anterior de hello y, a continuación, haga clic en <b>guardar</b>.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)

El centro de notificaciones está ahora configurado toowork con GCM y tiene tooboth de cadenas de conexión de hello registrar los notificaciones de tooreceive de aplicación y las notificaciones de inserción de toosend.

## <a name="connect-your-app-toohello-notification-hub"></a>Conectar el centro de notificaciones de toohello de aplicación
### <a name="create-a-new-project"></a>Crear un nuevo proyecto
1. En Xamarin Studio, haga clic en **Nueva solución**, haga clic en **Aplicación Android**, y luego en **Siguiente**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. Escriba su **Nombre de la aplicación** e **Identificador**. Haga clic en hello **las plataformas de destino** que desee toosupport y, a continuación, haga clic en **siguiente** y **crear**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    Esto crea un nuevo proyecto de Android.

1. Abrir propiedades del proyecto Hola haciendo clic en el proyecto nuevo en hello vista soluciones y elegir **opciones**. Seleccione hello **aplicación Android** elemento Hola **generar** sección.
   
    Asegúrese de que la primera letra Hola de su **nombre del paquete** es en minúscula.
   
   > [!IMPORTANT]
   > Hola la primera letra del nombre del paquete Hola debe estar en minúsculas. De lo contrario, recibirá errores de manifiesto de la aplicación al registrar **BroadcastReceiver** y **IntentFilter** para las notificaciones push siguientes.
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. Si lo desea, un conjunto de hello **versión mínimo Android** tooanother nivel de API.
3. Si lo desea, un conjunto de hello **versión de destino Android** toohello otra versión de API que desea tootarget (debe ser el nivel de API 8 o posterior).

Haga clic en **Aceptar** y cuadro de diálogo de opciones de proyecto de hello cerrar.

### <a name="add-hello-required-components-tooyour-project"></a>Agregar proyecto de tooyour de componentes necesarios de Hola
Hola Google nube cliente de mensajería disponible en el almacén de componentes de Xamarin Hola simplifica el proceso Hola de admitir las notificaciones de inserción en Xamarin.Android.

1. Haga clic en carpeta de componentes de hello en aplicación Xamarin.Android y elija **obtener más componentes**.
2. Busque hello **la mensajería de Azure** componentes y agregue el proyecto de toohello.
3. Busque hello **el cliente de mensajería de nube de Google** componentes y agregue el proyecto de toohello.

### <a name="set-up-notification-hubs-in-your-project"></a>Configuración de los centros de notificaciones en su proyecto
1. Recopile Hola siguiendo la información de la aplicación ni notificación al centro Android:
   
   * **GoogleProjectNumber**: obtener este valor de número de proyecto de información general de saludo de la aplicación en hello Portal para desarrolladores de Google. Realiza una nota de este valor anteriormente cuando se creó la aplicación hello en el portal de Hola.
   * **Cadena de conexión de escucha**: en panel de Hola Hola [Portal clásico de Azure], haga clic en **ver cadenas de conexión**. Hola copia *DefaultListenSharedAccessSignature* cadena de conexión para este valor.
   * **Nombre del concentrador**: este es el nombre de Hola de su centro de hello [Portal clásico de Azure]. Por ejemplo, *mynotificationhub2*.
     
     Crear un **Constants.cs** clase para el proyecto de Xamarin y definir Hola después de valores constantes en la clase hello. Reemplace los marcadores de posición de hello con sus valores.
     
       public static class Constants   {
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       }
2. Agregue los siguiente hello mediante instrucciones demasiado**MainActivity.cs**:
   
        using Android.Util;
        using Gcm.Client;
3. Agregar un toohello de variable de instancia `MainActivity` clase que será usado tooshow un cuadro de diálogo Alerta cuando se ejecuta la aplicación hello:
   
        public static MainActivity instance;
4. Crear hello siguiente método Hola **MainActivity** clase:
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. Hola `OnCreate` método **MainActivity.cs**, inicializar hello `instance` variable y agregue una llamada demasiado`RegisterWithGCM`:
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. Cree una nueva clase, **MyBroadcastReceiver**.
   
   > [!NOTE]
   > Más adelante, se explicará cómo crear una clase **BroadcastReceiver** desde el principio. Sin embargo, una creación rápida toomanually alternativo **MyBroadcastReceiver.cs** es toorefer toohello **GcmService.cs** archivo encontrado en el proyecto de Xamarin.Android de ejemplo de Hola incluido con hello [Ejemplos de NotificationHubs][GitHub]. Duplicar **GcmService.cs** y cambiar los nombres de clase puede tener también un toostart perfectos.
   > 
   > 
7. Agregue los siguiente hello mediante instrucciones demasiado**MyBroadcastReceiver.cs** (que hace referencia el componente de toohello y el ensamblado que agregó anteriormente):
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. En **MyBroadcastReceiver.cs**, agregar Hola siguiendo las solicitudes de permiso entre hello **con** hello e instrucciones **espacio de nombres** declaración:
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. En **MyBroadcastReceiver.cs**, cambiar hello **MyBroadcastReceiver** clase siguiente de Hola toomatch:
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. Agregue otra clase en **MyBroadcastReceiver.cs** llamada **PushHandlerService** que derive de **GcmServiceBase**. Realizar seguro hello tooapply **servicio** toohello clase de atributos:
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. **GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** y **OnError()**. Nuestro **PushHandlerService** clase de implementación debe invalidar estos métodos, y estos métodos se activarán en toointeracting de respuesta con el centro de notificaciones de Hola.
12. Invalidar hello **OnRegistered()** método **PushHandlerService** mediante el uso de hello siguiente código:
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > Hola **OnRegistered()** código encima, tenga en cuenta Hola capacidad toospecify etiquetas tooregister para los canales de mensajes específicos.
    > 
    > 
13. Invalidar hello **OnMessage** método **PushHandlerService** mediante el uso de hello siguiente código:
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. Agregue los siguiente hello **createNotification** y **dialogNotify** métodos demasiado**PushHandlerService** para informar a los usuarios cuando se recibe una notificación.
    
    > [!NOTE]
    > El diseño de notificaciones en Android versión 5.0 y posteriores representa un cambio significativo respecto al de las versiones anteriores. Si se prueba en Android 5.0 o versiones posteriores, aplicación hello deberá toobe ejecuta tooreceive Hola notification. Para más información, consulte [Notificaciones de Android](http://go.microsoft.com/fwlink/?LinkId=615880).
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. Reemplace los miembros abstractos **OnUnRegistered()**, **OnRecoverableError()** y **OnError()** para que el código se compile:
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a>Ejecutar la aplicación en el emulador Hola
Si ejecuta esta aplicación en el emulador de hello, asegúrese de que utiliza un dispositivos virtuales Android (AVD) que es compatible con Google APIs.

> [!IMPORTANT]
> Notificaciones de inserción de orden tooreceive, debe configurar una cuenta de Google en el dispositivo Virtual Android. (En el emulador de Windows hello, navegue demasiado**configuración** y haga clic en **Agregar cuenta**.) Además, asegúrese de que ese emulador hello es toohello conectado Internet.
> 
> [!NOTE]
> El diseño de notificaciones en Android versión 5.0 y posteriores representa un cambio significativo respecto al de las versiones anteriores. Para más información, consulte [Notificaciones de Android](http://go.microsoft.com/fwlink/?LinkId=615880).
> 
> 

1. En **Tools** (Herramientas), haga clic en **Open Android Emulator Manager** (Abrir Administrador de emulador Android), seleccione su dispositivo y, a continuación, haga clic en **Edit** (Editar).
   
      ![][18]
2. Seleccione **API de Google** en **Destino** y, luego, haga clic en **Aceptar**.
   
      ![][19]
3. En la barra de herramientas superior hello, haga clic en **ejecutar**y, a continuación, seleccione la aplicación. Esto inicia el emulador de Hola y ejecuta la aplicación hello.
   
   aplicación Hello recupera hello *registrationId* de GCM y se registra con el centro de notificaciones de Hola.

## <a name="send-notifications-from-your-backend"></a>Envío de notificaciones desde su backend
Puede probar recibir notificaciones en la aplicación mediante el envío de notificaciones en hello [Portal clásico de Azure] a través de hello depurar pestaña en el centro de notificaciones de hello, como se muestra en la siguiente pantalla de bienvenida.

![][30]

Las notificaciones push se envían normalmente en un servicio back-end como Servicios móviles o ASP.NET mediante una biblioteca compatible. También puede utilizar Hola API de REST directamente si una biblioteca no está disponible para el back-end de los mensajes de notificación toosend.

Esta es una lista de algunos otros tutoriales que puede que desee tooreview para enviar notificaciones:

* ASP.NET: Vea [toousers de notificaciones de los centros de notificaciones de uso toopush].
* Java de bases de datos centrales de notificación Azure SDK: vea [cómo toouse centros de notificaciones desde Java](notification-hubs-java-push-notification-tutorial.md) para enviar notificaciones de Java. Esto se probó en Eclipse para el desarrollo de Android.
* PHP: Vea [cómo toouse centros de notificaciones de PHP](notification-hubs-php-push-notification-tutorial.md).

En las subsecciones siguientes de Hola de tutorial de hello, enviar notificaciones mediante el uso de una aplicación de consola .NET y mediante el uso de un servicio móvil a través de una secuencia de comandos de nodo.

#### <a name="optional-send-notifications-by-using-a-net-app"></a>Envío de notificaciones mediante una aplicación .NET (opcional)
En esta sección enviará notificaciones con una aplicación de consola .NET.

1. Cree una aplicación de consola nueva de Visual C#:
   
      ![][20]
2. En Visual Studio, haga clic en **Herramientas**, **Administrador de paquetes NuGet** y, después, en **Consola del Administrador de paquetes**.
   
    Esto muestra hello consola de administrador de paquetes en Visual Studio.
3. En la ventana de la consola de administrador de paquetes de saludo, establecer hello **proyecto predeterminado** tooyour nuevo proyecto de aplicación de consola y, a continuación, en la ventana de la consola de hello, ejecute hello siguiente comando:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Abra el archivo Program.cs de hello y agregue Hola siguiente `using` instrucción:
   
        using Microsoft.Azure.NotificationHubs;
5. En su `Program` clase, agregue Hola siguiendo el método. Actualizar el texto de marcador de posición de hello con su *DefaultFullSharedAccessSignature* nombre de concentrador y la cadena de conexión de hello [Portal clásico de Azure].
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. Agregar Hola siguiendo las líneas en el **Main** método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Presione aplicación Hola de hello F5 toorun clave. Debería recibir una notificación en aplicación hello.
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a>Envío de notificaciones mediante un servicio móvil (opcional)
1. Siga [Introducción a Servicios móviles].
2. Inicie sesión en toohello [Portal clásico de Azure]y seleccione su servicio móvil.
3. Seleccione hello **programador** ficha en la parte superior de Hola.
   
      ![][22]
4. Cree un nuevo trabajo programado, inserte un nombre y seleccione **A petición**.
   
      ![][23]
5. Cuando se crea el trabajo de hello, haga clic en el nombre del trabajo de Hola. A continuación, haga clic en hello **Script** ficha en la barra superior Hola.
6. Inserte la siguiente secuencia de comandos dentro de la función de programador de Hola. Asegúrese de los marcadores de posición hello tooreplace seguro con la notificación concentrador hello y nombre de cadena de conexión para *DefaultFullSharedAccessSignature* que ha obtenido antes. Haga clic en **Guardar**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. Haga clic en **ejecutar una vez** en la barra de la parte inferior de Hola. Debería recibir una notificación del sistema.

## <a name="next-steps"></a>Pasos siguientes
En este sencillo ejemplo, difunden notificaciones tooall sus dispositivos Android. En el orden tootarget a usuarios específicos, consulte tutorial toohello [toousers de notificaciones de los centros de notificaciones de uso toopush]. Si desea que toosegment los usuarios por grupos de interés, puede leer [toosend de centros de notificaciones utilice noticias de última hora]. Más información acerca de cómo toouse centros de notificaciones de [Guía de centros de notificaciones] y Hola [centros de notificaciones toofor cómo Android].

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Introducción a Servicios móviles]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[Portal clásico de Azure]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Guía de centros de notificaciones]: http://msdn.microsoft.com/library/jj927170.aspx
[centros de notificaciones toofor cómo Android]: http://msdn.microsoft.com/library/dn282661.aspx

[toousers de notificaciones de los centros de notificaciones de uso toopush]: /manage/services/notification-hubs/notify-users-aspnet
[toosend de centros de notificaciones utilice noticias de última hora]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Componente del Cliente de mensajería en la nube de Google]: http://components.xamarin.com/view/GCMClient/
[Componente de mensajería de Azure]: http://components.xamarin.com/view/azure-messaging
