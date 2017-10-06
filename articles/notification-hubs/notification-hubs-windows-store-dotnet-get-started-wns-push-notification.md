---
title: "aaaGet a trabajar con Azure notificación concentradores para aplicaciones universales de Windows plataforma | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo toouse centros de notificaciones de Azure toopush notificaciones tooa aplicación de plataforma Universal de Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>Introducción a Notification Hubs para aplicaciones de la plataforma universal de Windows
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Información general
Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push notificaciones tooa plataforma Universal de Windows (UWP) aplicaciones.

En este tutorial, creará una aplicación de tienda Windows en blanco que recibe notificaciones de inserción mediante Hola servicios de notificación de inserción de Windows (WNS). Cuando haya terminado, podrá toouse capaz de su toobroadcast de base de datos central de notificaciones de inserción dispositivos Hola notificaciones tooall que ejecuta la aplicación.

## <a name="before-you-begin"></a>Antes de empezar
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

código de Hello completado para este tutorial se puede encontrar en GitHub [aquí](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).

## <a name="prerequisites"></a>Requisitos previos
Este tutorial requiere siguiente de hello:

* [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) o posterior
* [Herramientas de desarrollo de aplicaciones universales de Windows instaladas](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* Una cuenta activa de Azure <br/>En caso de no tener cuenta, puede crear una de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).
* Una cuenta de la Tienda Windows activa

Completar este tutorial es un requisito previo para todos los tutoriales de Notification Hubs para aplicaciones de la plataforma universal de Windows.

## <a name="register-your-app-for-hello-windows-store"></a>Registrar la aplicación para hello tienda Windows
aplicaciones de tooUWP de notificaciones de inserción toosend, debe asociar la tienda Windows toohello de aplicación. A continuación, debe configurar su toointegrate de concentrador de notificación con WNS.

1. Si todavía no ha registrado su aplicación, vaya a toohello [centro de desarrollo de Windows](https://dev.windows.com/overview), inicie sesión con su cuenta de Microsoft y, a continuación, haga clic en **crear una nueva aplicación**.

2. Escriba un nombre para la aplicación y haga clic en **Reservar nombre de aplicación**. Se crea un nuevo registro de la Tienda Windows para su aplicación.

3. En Visual Studio, cree un nuevo proyecto de Visual C# aplicaciones de la tienda mediante el uso de hello universales de Windows **aplicación vacía** plantilla y haga clic en **Aceptar**.

4. Acepte valores predeterminados de hello para el destino de Hola y versiones de plataforma mínima.

5. En el Explorador de soluciones, proyecto de aplicación de tienda de Windows de Hola de menú contextual, haga clic en **almacén**y, a continuación, haga clic en **asociar aplicación con hello almacén...** . Hola **asociar la aplicación con hello tienda Windows** aparece el Asistente para.

6. En el Asistente de hello, inicie sesión con su cuenta de Microsoft.

7. Haga clic en la aplicación hello que registró en el paso 2, haga clic en **siguiente**y, a continuación, haga clic en **asociar**. Esto agrega manifiesto de aplicación Hola necesario tienda Windows registro información toohello.

8. En hello [centro de desarrollo de Windows](http://dev.windows.com/overview) página de la aplicación nueva, haga clic en **servicios**, haga clic en **notificaciones de inserción**y, a continuación, haga clic en **estado de MPNS**.

9. Haga clic en **New Notification** (Nueva notificación).

10. Haga clic en la plantilla **Blank (Toast)** (En blanco [sistema]) y luego haga clic en **OK** (Aceptar).

11. Escriba el **nombre** de la notificación y el mensaje de **contexto** visual. A continuación, haga clic en **Save as draft** (Guardar como borrador).

12. Navegue toohello [Portal de registro de aplicación](http://apps.dev.microsoft.com) e inicie sesión.

13. Haga clic en el nombre de la aplicación. Tome nota de hello **secreto de aplicación** hello y contraseña **identificador de seguridad (SID) de paquete** ubicado en hello **tienda Windows** configuración de plataforma.

     > [AZURE.WARNING]
    secreto de aplicación Hola y el SID del paquete son credenciales de seguridad importantes. No los comparta con nadie ni los distribuya con su aplicación.

## <a name="configure-your-notification-hub"></a>Configuración de su Centro de notificaciones
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Seleccione hello <b>Notification Services</b> hello y opción <b>de Windows (WNS)</b> opción. A continuación, escriba Hola <b>secreto de aplicación</b> contraseña Hola <b>clave de seguridad</b> campo. Escriba su <b>SID del paquete</b> valor que ha obtenido de WNS en la sección anterior de hello y, a continuación, haga clic en <b>guardar</b>.</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

El centro de notificaciones está ahora configurado toowork con WNS, y tiene la aplicación de tooregister de cadenas de conexión de Hola y enviar notificaciones.

## <a name="connect-your-app-toohello-notification-hub"></a>Conectar el centro de notificaciones de toohello de aplicación
1. En Visual Studio, haga clic en soluciones de hello y, a continuación, haga clic en **administrar paquetes de NuGet**.
   
    Esto muestra hello **administrar paquetes de NuGet** cuadro de diálogo.
2. Busque `WindowsAzure.Messaging.Managed` y haga clic en **instalar**y acepte los términos de Hola de uso.
   
    ![][20]
   
    Esto descarga, se instala y se agrega una biblioteca de referencia para la mensajería de Azure de toohello para Windows mediante el uso de Hola <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">paquete WindowsAzure.Messaging.Managed NuGet</a>.
3. Abrir archivo de proyecto de hello App.xaml.cs y agregue Hola siguiente `using` instrucciones. 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. En App.xaml.cs, agregue Hola siguiente **InitNotificationsAsync** toohello de definición de método **aplicación** clase:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    Este código recupera el URI del canal de hello para la aplicación hello de WNS y, a continuación, registra ese URI del canal con el centro de notificaciones.
   
   > [!NOTE]
   > Asegúrese de tooreplace seguro Hola marcador de posición "el nombre de base de datos central" con el nombre de Hola de centro de notificaciones de Hola que aparece en hello Portal de Azure. También reemplace el marcador de posición de cadena de conexión de hello con hello **DefaultListenSharedAccessSignature** cadena de conexión que obtiene de hello **directivas de acceso** página del centro de notificaciones en un sección anterior.
   > 
   > 
5. En parte superior de Hola de hello **OnLaunched** controlador de eventos en App.xaml.cs, agregue Hola después llamada toohello nueva **InitNotificationsAsync** método:
   
        InitNotificationsAsync();
   
    Esto garantiza que ese canal Hola que URI está registrado en el centro de notificaciones que se inicia cada aplicación Hola de tiempo.
6. Hola presione **F5** toorun clave Hola aplicación. Se muestra un cuadro de diálogo emergente que contiene la clave de registro de hello.

La aplicación ya está listo tooreceive recibir notificaciones del sistema.

## <a name="send-notifications"></a>Envío de notificaciones
Puede probar rápidamente recibir notificaciones en la aplicación mediante el envío de notificaciones en hello [Portal de Azure](https://portal.azure.com/) con hello **probar envío** situado en el centro de notificaciones de hello, como se muestra en la siguiente pantalla de bienvenida.

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

Las notificaciones push se envían normalmente en un servicio back-end como Mobile Services o ASP.NET mediante una biblioteca compatible. También puede utilizar Hola API de REST directamente si una biblioteca no está disponible para el back-end de los mensajes de notificación toosend. 

En este tutorial, agregaremos simplificar y solo muestran probar la aplicación cliente mediante el envío de notificaciones mediante Hola .NET SDK centrales de notificaciones en una aplicación de consola en lugar de un servicio back-end. Se recomienda hello [toousers de notificaciones de los centros de notificaciones de uso toopush] tutorial como paso siguiente de Hola para enviar notificaciones desde un back-end ASP.NET. Sin embargo, Hola siguiendo métodos puede utilizarse para enviar notificaciones:

* **Interfaz REST**: admitir la notificación en cualquier plataforma de back-end mediante hello [interfaz REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **SDK de .NET de Microsoft Azure notificación concentradores**: Hola Administrador de paquetes de Nuget para Visual Studio, ejecutar [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [cómo toouse centros de notificaciones de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Aplicaciones móviles de Azure**: para obtener un ejemplo de cómo toosend notificaciones desde una aplicación móvil de Azure que se integra con centros de notificaciones, consulte [agregar notificaciones de inserción para aplicaciones móviles](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: para obtener un ejemplo de cómo toosend notificaciones mediante el uso de hello las API de REST, vea "cómo toouse centros de notificaciones de Java y PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-console-app"></a>(Opcional) Enviar notificaciones desde una aplicación de consola
notificaciones de toosend mediante el uso de una aplicación de consola .NET siguen estos pasos. 

1. Solución de Hola de menú contextual, seleccione **agregar** y **nuevo proyecto...** y, a continuación, en **Visual C#**, haga clic en **Windows** y **aplicación de consola**y haga clic en **Aceptar**.
   
    Esto agrega una nueva solución de toohello para aplicaciones de Visual C# consola. También puede hacer esto en una solución separada.

2. En Visual Studio, haga clic en **Herramientas**, **Administrador de paquetes NuGet** y, después, en **Consola del Administrador de paquetes**.
   
    Esto muestra hello consola de administrador de paquetes en Visual Studio.
3. En la ventana de la consola de administrador de paquetes de saludo, establecer hello **proyecto predeterminado** tooyour nuevo proyecto de aplicación de consola y, a continuación, en la ventana de la consola de hello, ejecute hello siguiente comando:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Esto agrega un toohello referencia SDK de centros de notificaciones de Azure con hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">paquete NuGet de bases de datos centrales de Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Abra el archivo Program.cs de hello y agregue Hola siguiente `using` instrucción:
   
        using Microsoft.Azure.NotificationHubs;
5. Hola **programa** clase, agregue Hola siguiente método:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > Asegúrese de que usar cadena de conexión de hello tiene **completa** acceso, no **escuchar** acceso. cadena de acceso de la escucha de Hello no tiene las notificaciones de toosend de permisos.
   > 
   > 
6. Agregar Hola después de las líneas de hello **Main** método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Haga clic en proyecto de aplicación de consola de hello en Visual Studio y haga clic en **establecer como proyecto de inicio** tooset como proyecto de inicio de Hola. A continuación, presione hello **F5** aplicación de hello toorun de clave.
   
    Debería recibir una notificación del sistema en todos los dispositivos registrados. Banner de notificación del sistema de hello clic o pulsando en carga la aplicación hello.

Puede encontrar todas las cargas de hello admitida Hola [catálogo del sistema], [catálogo iconos], y [información general de identificación] temas en MSDN.

## <a name="next-steps"></a>Pasos siguientes
En este sencillo ejemplo, envía notificaciones difusión tooall los dispositivos de Windows mediante el portal de Hola o una aplicación de consola. Se recomienda hello [toousers de notificaciones de los centros de notificaciones de uso toopush] tutorial como paso siguiente Hola. Le mostraremos cómo toosend notificaciones desde un back-end ASP.NET con etiquetas tootarget determinados usuarios.

Si desea toosegment los usuarios por grupos de interés, vea [toosend de centros de notificaciones utilice noticias de última hora]. 

toolearn obtener más información sobre los centros de notificaciones, consulte [instrucciones de los centros de notificación](notification-hubs-push-notification-overview.md).

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[toousers de notificaciones de los centros de notificaciones de uso toopush]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend de centros de notificaciones utilice noticias de última hora]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[catálogo del sistema]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[catálogo iconos]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[información general de identificación]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
