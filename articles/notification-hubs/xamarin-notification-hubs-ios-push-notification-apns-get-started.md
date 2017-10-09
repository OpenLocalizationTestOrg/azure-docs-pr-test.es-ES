---
title: "aaaiOS notificaciones de inserción con centros de notificaciones para las aplicaciones de Xamarin | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toosend push aplicación de iOS de notificaciones de tooa Xamarin."
services: notification-hubs
keywords: "notificaciones push de ios,mensajes de inserción,notificaciones push,mensaje de notificación"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a>Notificaciones push de iOS con Centros de notificaciones para aplicaciones Xamarin
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Información general
> [!IMPORTANT]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push aplicación de iOS de tooan de notificaciones.
Se creará una aplicación de Xamarin.iOS en blanco que recibe notificaciones de inserción mediante hello [servicio de notificaciones de inserción de Apple (APN)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html). Cuando haya terminado, podrá toouse capaz de su toobroadcast de base de datos central de notificaciones de inserción dispositivos Hola notificaciones tooall que ejecuta la aplicación. Hello terminado código está disponible en hello [NotificationHubs aplicación] [ GitHub] ejemplo.

Este tutorial muestra el escenario de difusión mensajes de Hola simple inserción con centros de notificaciones.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial requiere siguiente de hello:

* [Xcode 6.0][Install Xcode]
* Un dispositivo compatible con iOS 7.0 (o una versión posterior)
* Pertenencia al programa para desarrolladores de iOS
* [Xamarin Studio]
  
  > [!NOTE]
  > Debido a los requisitos de configuración para las notificaciones de inserción de iOS, debe implementar y probar la aplicación de ejemplo de Hola en un dispositivo físico iOS (iPhone o iPad) en lugar de en el simulador de Hola.
  > 
  > 

La realización de este tutorial es un requisito previo para todos los demás tutoriales de Centros de notificaciones para aplicaciones Xamarin para iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a>Configuración de su Centro de notificaciones
En esta sección le guía a través de la creación de un nuevo centro de notificaciones y configurar la autenticación con APNS mediante hello **. p12** certificado de inserción que creó. Si desea toouse un centro de notificaciones que ya haya creado, puede omitir toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p>Puesto que queremos conexión de APN hello tooconfigure, Hola Portal de Azure, abra la configuración del centro de notificaciones, ande haga clic en <b>Notification Services</b>y, a continuación, haga clic en hello <b>Apple (APN)</b> elemento de lista de Hola. Una vez terminado, haga clic en <b>cargar certificado</b> y seleccione hello <b>. p12</b> certificado que exportó anteriormente, así como la contraseña de hello para el certificado de Hola.</p>

<p>Asegúrese de que tooselect <b>espacio aislado</b> modo desde que se van a enviar inserción los mensajes en un entorno de desarrollo. Usar solo hello <b>producción</b> establecer si desea toousers de notificaciones de inserción de toosend que ya ha adquirido la aplicación desde el almacén de Hola.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

El centro de notificaciones está ahora configurado toowork con APNS, y tiene la aplicación de tooregister de cadenas de conexión de Hola y enviar notificaciones de inserción.

## <a name="connect-your-app-toohello-notification-hub"></a>Conectar el centro de notificaciones de toohello de aplicación
#### <a name="create-a-new-project"></a>Crear un nuevo proyecto
1. En Xamarin Studio, cree un nuevo proyecto de iOS y seleccione hello **API unificada** > **única aplicación de vista** plantilla.
   
     ![Xamarin Studio: Selección del tipo de aplicación][31]
2. Agregue un componente de mensajería de Azure toohello de referencia. Hola vista de soluciones, haga clic en hello **componentes** carpeta de su proyecto y elija **obtener más componentes**. Busque hello **la mensajería de Azure** componentes y agregue Hola componente tooyour proyecto.
3. En **AppDelegate.cs**, agregue Hola siguiente instrucción using:
   
        using WindowsAzure.Messaging;
4. Declare una instancia de **SBNotificationHub**:
   
        private SBNotificationHub Hub { get; set; }
5. Crear un **Constants.cs** clase con hello siguientes variables:
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. En **AppDelegate.cs**, actualizar **FinishedLaunching()** siguiente de Hola toomatch:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. Invalidar hello **RegisteredForRemoteNotifications()** método **AppDelegate.cs**:
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. Invalidar hello **ReceivedRemoteNotification()** método **AppDelegate.cs**:
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. Cree Hola siguiente **ProcessNotification()** método **AppDelegate.cs**:
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > Puede elegir toooverride **FailedToRegisterForRemoteNotifications()** toohandle situaciones como no hay ninguna conexión de red. Esto es especialmente importante que usuario Hola podría iniciar la aplicación en modo sin conexión (por ejemplo, avión) y desee inserción toohandle aplicación tooyour específico de escenarios de mensajería.
   > 
   > 
10. Ejecute la aplicación hello en el dispositivo.

## <a name="sending-push-notifications"></a>Envío de notificaciones push
Puede probar recibiendo notificaciones de inserción en la aplicación mediante el envío de notificaciones en hello [Portal de Azure] a través de hello **probar envío** capacidad en hello **solución de problemas** conjunto de herramientas y a la derecha en la página de concentrador de notificación hello, como se muestra en la siguiente pantalla de bienvenida.

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

Las notificaciones push se envían normalmente en un servicio back-end como Servicios móviles o ASP.NET mediante una biblioteca compatible. También puede utilizar Hola API de REST directamente toosend inserción mensajes si una biblioteca no está disponible en el escenario. 

En este tutorial, agregaremos simplificar y solo muestran probar la aplicación cliente mediante el envío de notificaciones mediante Hola .NET SDK centrales de notificaciones en una aplicación de consola en lugar de un servicio back-end. Se recomienda hello [toousers de notificaciones de los centros de notificaciones de uso toopush](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial como paso siguiente de Hola para enviar notificaciones desde un back-end ASP.NET. Sin embargo, Hola siguiendo métodos puede utilizarse para enviar notificaciones:

* **Interfaz REST**: puede admitir la notificación de inserción en cualquier plataforma de back-end mediante hello [interfaz REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **SDK de .NET de Microsoft Azure notificación concentradores**: Hola Administrador de paquetes de Nuget para Visual Studio, ejecutar [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [cómo toouse centros de notificaciones de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).

**Aplicaciones móviles**: para obtener un ejemplo de cómo toosend notificaciones desde un back-end de aplicaciones de Mobile de servicio de aplicación de Azure que se integra con centros de notificaciones, consulte [Agregar aplicación móvil de inserción notificaciones tooyour](../app-service-mobile/app-service-mobile-ios-get-started-push.md).

* **Java / PHP**: para obtener un ejemplo de cómo las notificaciones de inserción de toosend mediante el uso de hello las API de REST, vea "cómo toouse centros de notificaciones de Java y PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a>Envío de notificaciones push desde una aplicación de consola .NET (opcional)
En esta sección, enviará notificaciones push con una aplicación sencilla de consola .NET. Para fines de Hola de este ejemplo, se cambiará el entorno de desarrollo de Windows tooa que tiene Visual Studio instalado.

1. En Visual Studio, cree una nueva aplicación de consola en Visual C#:
   
       ![Visual Studio - Create a new console application][213]
2. En Visual Studio, haga clic en **Herramientas**, **Administrador de paquetes NuGet** y, después, en **Consola del Administrador de paquetes**.
   
    consola del Administrador de paquetes de saludo debe aparecer toohello acoplada inferior del área de trabajo de Visual Studio.
3. En la ventana de la consola de administrador de paquetes de saludo, establecer hello **proyecto predeterminado** tooyour nuevo proyecto de aplicación de consola y, a continuación, en la ventana de la consola de hello, ejecute hello siguiente comando:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Abra hello `Program.cs` de archivos y agregue Hola siguiente `using` instrucción, garantizando así que podemos usar Azure clases y funciones dentro de la clase principal:
   
        using Microsoft.Azure.NotificationHubs;
5. En su `Program` clase, agregue Hola siguiendo el método (no olvide hello tooreplace **cadena de conexión** y **nombre del concentrador**):
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. Agregar Hola después de las líneas de su `Main` método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Presione aplicación Hola de hello F5 toorun clave. En unos segundos, verá que aparece una notificación push en su dispositivo. Si usas Wi-Fi o una red de datos móviles, asegúrese de que haya una conexión a internet activa en el dispositivo de Hola.

Puede encontrar todas las cargas posibles Hola Hola Apple [locales y Guía de programación de notificaciones de inserción].

#### <a name="optional-send-notifications-from-a-mobile-service"></a>Envío de notificaciones desde un servicio móvil (opcional)
En esta sección, enviaremos notificaciones push mediante un servicio móvil a través de un script de Node.

toosend una notificación mediante el uso de un servicio móvil, siga [empezar a trabajar con servicios móviles]y, a continuación:

1. Inicie sesión en toohello [Portal clásico de Azure]y seleccione su servicio móvil.
2. Seleccione hello **programador** ficha en la parte superior de Hola.
   
       ![Azure Classic Portal - Scheduler][215]
3. Cree un nuevo trabajo programado, inserte un nombre y seleccione **A petición**.
   
       ![Azure Classic Portal - Create new job][216]
4. Cuando se crea el trabajo de hello, haga clic en el nombre del trabajo de Hola. A continuación, haga clic en hello **Script** ficha en la barra superior Hola.
5. Inserte la siguiente secuencia de comandos dentro de la función de programador de Hola. Asegúrese de los marcadores de posición hello tooreplace seguro con la notificación concentrador hello y nombre de cadena de conexión para *DefaultFullSharedAccessSignature* que ha obtenido antes. Haga clic en **Guardar**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. Haga clic en **ejecutar una vez** en la barra de la parte inferior de Hola. Debe recibir una alerta en el dispositivo.

## <a name="next-steps"></a>Pasos siguientes
En este sencillo ejemplo, difunden tooall de notificaciones de inserción los dispositivos iOS. En el orden tootarget a usuarios específicos, consulte tutorial toohello [toousers de notificaciones de los centros de notificaciones de uso toopush]. Si desea que toosegment los usuarios por grupos de interés, puede leer [toosend de centros de notificaciones utilice noticias de última hora]. Más información acerca de cómo toouse centros de notificaciones de [Guía de centros de notificaciones] y Hola [iOS de centros de notificaciones cómo-toofor].

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[empezar a trabajar con servicios móviles]: /develop/mobile/tutorials/get-started-xamarin-ios
[Portal clásico de Azure]: https://manage.windowsazure.com/
[Guía de centros de notificaciones]: http://msdn.microsoft.com/library/jj927170.aspx
[iOS de centros de notificaciones cómo-toofor]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[toousers de notificaciones de los centros de notificaciones de uso toopush]: /manage/services/notification-hubs/notify-users-aspnet
[toosend de centros de notificaciones utilice noticias de última hora]: /manage/services/notification-hubs/breaking-news-dotnet

[locales y Guía de programación de notificaciones de inserción]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Portal de Azure]: https://portal.azure.com
