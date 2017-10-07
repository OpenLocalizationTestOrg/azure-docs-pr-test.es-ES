---
title: "notificaciones de inserción de aaaSending con centros de notificaciones de Azure en Windows Phone | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo las notificaciones de toouse centros de notificaciones de Azure toopush tooa Windows Phone 8 o una aplicación de Silverlight de Windows Phone 8.1."
services: notification-hubs
documentationcenter: windows
keywords: "notificación push, notificación push, notificación push de windows phone"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>Envío de notificaciones push con los Centros de notificaciones de Azure en Windows Phone
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Información general
> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).
> 
> 

Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend aplicación de Windows Phone 8 o Windows Phone 8.1 Silverlight tooa notificaciones de inserción. Si desea usar Windows Phone 8.1 (no de Silverlight), a continuación, consulte toohello [universales de Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) versión.
En este tutorial, creará una aplicación de Windows Phone 8 en blanco que recibe notificaciones de inserción mediante Hola servicio de notificaciones de inserción de Microsoft (MPNS). Cuando haya terminado, podrá toouse capaz de su toobroadcast de base de datos central de notificaciones de inserción dispositivos Hola notificaciones tooall que ejecuta la aplicación.

> [!NOTE]
> Hola notificación centros de Windows Phone SDK no admite el uso de hello servicios de notificación de inserción de Windows (WNS) con aplicaciones de Silverlight de Windows Phone 8.1. toouse WNS (en lugar de MPNS) con aplicaciones de Silverlight de Windows Phone 8.1, siga hello [centros de notificaciones: tutorial de Windows Phone Silverlight], que usa las API de REST.
> 
> 

tutorial de Hello muestra el escenario sencillo de difusión hello en usar centros de notificaciones.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial requiere siguiente de hello:

* [Visual Studio 2012 Express para Windows Phone], o una versión posterior.

La realización de este tutorial es un requisito previo para todos los demás tutoriales de Centros de notificaciones para aplicaciones de Windows Phone 8.

## <a name="create-your-notification-hub"></a>Creación de su centro de notificaciones
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Haga clic en hello <b>Notification Services</b> sección (dentro de <i>configuración</i>), haga clic en <b>Windows Phone (MPNS)</b> y, a continuación, haga clic en hello <b>Habilitar inserción no autenticadas </b> casilla de verificación.</p>
</li>
</ol>

&emsp;&emsp;![Portal de Azure: Habilitación de notificaciones push sin autenticar.](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

El concentrador ahora es notificación creada y configurada toosend no autenticado de Windows Phone.

> [!NOTE]
> Este tutorial usa MPNS en modo sin autenticar. Modo MPNS no autenticado incluye restricciones en las notificaciones que puede enviar tooeach canal. Es compatible con los centros de notificaciones [MPNS autenticado modo](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) permitiéndole tooupload su certificado.
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>Conectar el centro de notificaciones de toohello de aplicación
1. En Visual Studio, cree una aplicación nueva de Windows Phone 8.
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    En Visual Studio 2013 Update 2 o versiones posteriores, cree en su lugar una aplicación Silverlight de Windows Phone.
   
    ![Visual Studio, nuevo proyecto, aplicación vacía, Windows Phone Silverlight][11]
2. En Visual Studio, haga clic en soluciones de hello y, a continuación, haga clic en **administrar paquetes de NuGet**.
   
    Esto muestra hello **administrar paquetes de NuGet** cuadro de diálogo.
3. Busque `WindowsAzure.Messaging.Managed` y haga clic en **instalar**y, a continuación, acepte los términos de Hola de uso.
   
    ![Visual Studio, Administrador de paquetes NuGet][20]
   
    Esto descarga, se instala y se agrega una biblioteca de referencia para la mensajería de Azure de toohello para Windows mediante el uso de Hola <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">paquete WindowsAzure.Messaging.Managed NuGet</a>.
4. Abra el archivo hello App.xaml.cs y agregue Hola siguiente `using` instrucciones:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. Agregar Hola siguiente código en la parte superior de Hola de **Application_Launching** método en App.xaml.cs:
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > Hola valor **MyPushChannel** es un índice que está toolookup usa un canal existente en hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) colección. Si no hay uno ya allí, cree una nueva entrada con ese nombre.
   > 
   > 
   
    Asegúrese de que tooinsert Hola nombre de la cadena de conexión de concentrador y Hola llamada **DefaultListenSharedAccessSignature** que obtuvo en la sección anterior de Hola.
    Este código recupera el URI del canal de hello para la aplicación hello de MPNS y, a continuación, registra ese URI del canal con el centro de notificaciones. También se garantiza que ese canal Hola que URI está registrado en el centro de notificaciones que se inicia cada aplicación Hola de tiempo.
   
   > [!NOTE]
   > Este tutorial, envía un dispositivo de toohello de notificación de notificación del sistema. Cuando se envía una notificación de mosaico, en su lugar, debe llamar a hello **BindToShellTile** método en el canal de Hola. toosupport notificaciones notificaciones del sistema y el icono, llame a ambos **BindToShellTile** y **BindToShellToast**.
   > 
   > 
6. En el Explorador de soluciones, expanda **propiedades**, abra hello `WMAppManifest.xml` de archivos, haga clic en hello **capacidades** pestaña y asegúrese de que ese hello **ID_CAP_PUSH_NOTIFICATION** se comprueba la capacidad.
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. Hola presione `F5` toorun clave Hola aplicación.
   
    Se muestra un mensaje de registro en la aplicación hello.
8. Aplicación de hello cerrar.  
   
   > [!NOTE]
   > tooreceive una notificación de inserción del sistema, aplicación hello no debe disponer en primer plano de Hola.
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>Envío de notificaciones push desde su backend
Puede enviar notificaciones de inserción con centros de notificaciones desde cualquier back-end a través de hello público <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfaz REST</a>. En este tutorial, enviará notificaciones push con una aplicación de consola .NET. 

Para obtener un ejemplo de cómo toosend notificaciones de inserción desde un back-end de WebAPI de ASP.NET que se integra con centros de notificaciones, consulte [Azure notificación centros de informar a los usuarios con back-end de .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).  

Para obtener un ejemplo de cómo las notificaciones de inserción de toosend mediante el uso de Hola [API de REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), visite [cómo toouse centros de notificaciones de Java](notification-hubs-java-push-notification-tutorial.md) y [cómo toouse centros de notificaciones de PHP](notification-hubs-php-push-notification-tutorial.md) .

1. Solución de Hola de menú contextual, seleccione **agregar** y **nuevo proyecto...** y, a continuación, en **Visual C#**, haga clic en **Windows** y **aplicación de consola**y haga clic en **Aceptar**.
   
       ![Visual Studio - New Project - Console Application][6]
   
    Esto agrega una nueva solución de toohello para aplicaciones de Visual C# consola. También puede hacer esto en una solución separada.
2. Haga clic en **Herramientas**, **Administrador de paquetes de biblioteca** y **Consola del Administrador de paquetes**.
   
    Esto muestra hello Package Manager Console.
3. Hola **Package Manager Console** (ventana), conjunto hello **proyecto predeterminado** tooyour nuevo proyecto de aplicación de consola y, a continuación, en la ventana de la consola de hello, ejecute hello siguiente comando:
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.
4. Abra hello `Program.cs` de archivos y agregue Hola siguiente `using` instrucción:
   
        using Microsoft.Azure.NotificationHubs;
5. Hola `Program` clase, agregue Hola siguiente método:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    Realizar seguro hello tooreplace `<hub name>` marcador de posición con nombre de hello del centro de notificaciones de Hola que aparece en el portal de Hola. También, Reemplazar marcador de posición de cadena de conexión de hello con cadena de conexión de hello llama **DefaultFullSharedAccessSignature** que obtuvo en la sección de Hola "Configurar el centro de notificaciones".
   
   > [!NOTE]
   > Asegúrese de que usar cadena de conexión de hello con **completa** acceso, no **escuchar** acceso. cadena de acceso de la escucha de Hello no tiene las notificaciones de inserción de toosend de permisos.
   > 
   > 
6. Agregar Hola línea siguiente en su `Main` método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Con su Windows Phone emulador que se ejecuta y el proyecto de aplicación de consola de aplicación Hola cerrado, establezca como Hola predeterminado el proyecto de inicio y, a continuación, presione hello `F5` toorun clave Hola aplicación.
   
    Recibirá una notificación push del sistema. Al puntear en banner de notificación de hello carga la aplicación hello.

Puede encontrar todas las cargas posibles Hola Hola [catálogo del sistema] y [catálogo iconos] temas en MSDN.

## <a name="next-steps"></a>Pasos siguientes
En este sencillo ejemplo, difunden tooall de notificaciones de inserción los dispositivos Windows Phone 8. 

En el orden tootarget a usuarios específicos, consulte toohello [toousers de notificaciones de los centros de notificaciones de uso toopush] tutorial. 

Si desea que toosegment los usuarios por grupos de interés, puede leer [toosend de centros de notificaciones utilice noticias de última hora]. 

Más información acerca de cómo toouse centros de notificaciones de [instrucciones de los centros de notificación].

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express para Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[instrucciones de los centros de notificación]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[toousers de notificaciones de los centros de notificaciones de uso toopush]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend de centros de notificaciones utilice noticias de última hora]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[catálogo del sistema]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[catálogo iconos]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[centros de notificaciones: tutorial de Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

