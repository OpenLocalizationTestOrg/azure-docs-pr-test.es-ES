---
title: "notificaciones de inserción de aaaSending con centros de notificaciones de Azure y Node.js"
description: "Obtenga información acerca de cómo toosend de centros de notificaciones de toouse notificaciones de inserción desde una aplicación Node.js."
keywords: "notificación push,notificaciones push,inserción de node.js,inserción de ios"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a>Envío de notificaciones push seguras con los Centros de notificaciones de Azure y Node.js
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a>Información general
> [!IMPORTANT]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).
> 
> 

Esta guía le mostrará cómo toosend notificaciones de inserción con ayuda de Hola de centros de notificaciones de Azure directamente desde una aplicación Node.js. 

escenarios de Hello descritos incluyen enviar tooapplications de notificaciones de inserción en hello siguientes plataformas:

* Android
* iOS
* Windows Phone
* Plataforma universal de Windows 

Para obtener más información sobre los centros de notificaciones, consulte hello [pasos](#next) sección.

## <a name="what-are-notification-hubs"></a>¿Qué son los Centros de notificaciones?
Centros de notificaciones de Azure proporcionan una infraestructura fácil de usar, multiplataforma y escalable para el envío de dispositivos de toomobile de notificaciones de inserción. Para obtener detalles sobre la infraestructura de servicio de hello, vea hello [centros de notificaciones de Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) página.

## <a name="create-a-nodejs-application"></a>Creación de una aplicación Node.js
Hola primer paso en este tutorial es crear una nueva aplicación Node.js en blanco. Para obtener instrucciones sobre cómo crear una aplicación Node.js, vea [crear e implementar un tooAzure de aplicación sitio Web de Node.js][nodejswebsite], [servicio de nube de Node.js] [ Node.js Cloud Service] con Windows PowerShell, o [sitio Web con WebMatrix].

## <a name="configure-your-application-toouse-notification-hubs"></a>Configurar los centros de notificaciones de la aplicación tooUse
toouse centros de notificaciones de Azure, necesitará toodownload y use hello Node.js [paquete azure](https://www.npmjs.com/package/azure), que incluye un conjunto integrado de bibliotecas de aplicación auxiliar que se comunican con servicios REST de notificación de inserción de Hola.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Usar el Administrador de paquetes de nodo (NPM) tooobtain Hola paquete
1. Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Linux) y desplazarse por las carpetas de toohello en la que creó la aplicación en blanco .
2. Tipo de **npm instalar azure sb** en la ventana de comandos de Hola.
3. También puede ejecutar manualmente hello **ls** o **dir** tooverify de comando que un **nodo\_módulos** se creó la carpeta. Dentro de esa carpeta, busque hello **azure** paquete, que contiene las bibliotecas de Hola que necesita tooaccess Hola centro de notificaciones.

> [!NOTE]
> Puede aprender más acerca de cómo instalar NPM en oficial de hello [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm). 
> 
> 

### <a name="import-hello-module"></a>Módulo de Hola de importación
Con un editor de texto, agregar Hola después de la parte superior de toohello de Hola **server.js** archivo de aplicación hello:

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a>Configuración de una conexión de Centro de notificaciones de Azure
Hola **NotificationHubService** objeto le permite trabajar con los centros de notificaciones. Hello código siguiente se crea un **NotificationHubService** objeto para el concentrador de notificación de hello denominado **hubname**. Agregar cerca de parte superior de Hola de hello **server.js** archivo, después de módulo de hello instrucción tooimport hello azure:

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

Hola conexión **connectionstring** se puede obtener el valor de hello [Portal de Azure] realizando Hola pasos:

1. En el panel de navegación izquierdo de hello, haga clic en **examinar**.
2. Seleccione **centros de notificaciones**y, a continuación, buscar Hola concentrador desea toouse de ejemplo de Hola. Puede hacer referencia a toohello [tutorial de introducción a Windows almacén](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) si necesita ayuda para crear un nuevo centro de notificaciones.
3. Seleccione **Configuración**.
4. Haga clic en **Directivas de acceso**. Verá las cadenas de conexión de acceso, tanto las compartidas como las de acceso completo.

![Portal de Azure: Centros de notificaciones](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> También puede recuperar la cadena de conexión de hello con hello **Get-AzureSbNamespace** cmdlet proporcionado por [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello **show de espacio de nombres de azure sb** con Hola [interfaz de línea de comandos de Azure (Azure CLI)](../cli-install-nodejs.md).
> 
> 

## <a name="general-architecture"></a>Arquitectura general
Hola **NotificationHubService** objeto expone Hola siguientes instancias de objeto para el envío de aplicaciones y dispositivos de toospecific de notificaciones de inserción:

* **Android** -usar hello **GcmService** objeto, que está disponible en **notificationHubService.gcm**
* **iOS** -usar hello **ApnsService** objeto, que puede tener acceso al **notificationHubService.apns**
* **Windows Phone** -usar hello **MpnsService** objeto, que está disponible en **notificationHubService.mpns**
* **Plataforma universal de Windows** -usar hello **WnsService** objeto, que está disponible en **notificationHubService.wns**

### <a name="how-to-send-push-notifications-tooandroid-applications"></a>Cómo: enviar aplicaciones tooAndroid de notificaciones de inserción
Hola **GcmService** objeto proporciona un **enviar** método que puede ser aplicaciones de tooAndroid de notificaciones de inserción de toosend usado. Hola **enviar** método acepta Hola parámetros siguientes:

* **Etiquetas** -Hola identificador de etiquetas. Si no se proporciona ninguna etiqueta, se enviará a notificación de hello tooall clientes.
* **Carga** -Hola JSON o la carga de cadena sin formato del mensaje.
* **Devolución de llamada** -Hola función de devolución de llamada.

Para obtener más información sobre el formato de carga de hello, vea hello **carga** sección de hello [implementar servidores de GCM](http://developer.android.com/google/gcm/server.html#payload) documento.

Hello código siguiente usa hello **GcmService** instancia expuesto por hello **NotificationHubService** toosend un tooall de notificación de inserción registrado los clientes.

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a>Cómo: enviar aplicaciones tooiOS de notificaciones de inserción
Igual al igual que con las aplicaciones de Android se ha descrito anteriormente, Hola **ApnsService** objeto proporciona un **enviar** método que puede ser aplicaciones de tooiOS de notificaciones de inserción de toosend usado. Hola **enviar** método acepta Hola parámetros siguientes:

* **Etiquetas** -Hola identificador de etiquetas. Si no se proporciona ninguna etiqueta, se enviará a notificación de hello tooall clientes.
* **Carga** : Hola JSON del mensaje o carga de cadena.
* **Devolución de llamada** -Hola función de devolución de llamada.

Para el formato de carga de Hola de más información, vea hello **carga de notificaciones** sección de hello [locales y Guía de programación de notificaciones de inserción](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) documento.

Hello código siguiente usa hello **ApnsService** instancia expuesto por hello **NotificationHubService** toosend una alerta de mensaje tooall clientes:

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a>Cómo: enviar aplicaciones de teléfono de tooWindows de notificaciones de inserción
Hola **MpnsService** objeto proporciona un **enviar** método que puede ser tooWindows de notificaciones de inserción toosend usado aplicaciones de teléfono. Hola **enviar** método acepta Hola parámetros siguientes:

* **Etiquetas** -Hola identificador de etiquetas. Si no se proporciona ninguna etiqueta, se enviará a notificación de hello tooall clientes.
* **Carga** -Hola carga XML del mensaje.
* **TargetName** - `toast` para notificaciones del sistema. `token` para notificaciones de icono.
* **Clase de notificación** -Hola prioridad de notificación de Hola. Vea hello **elementos de encabezado HTTP** sección de hello [notificaciones de inserción desde un servidor](http://msdn.microsoft.com/library/hh221551.aspx) documento para los valores válidos.
* **Options** : encabezados de solicitud opcionales.
* **Devolución de llamada** -Hola función de devolución de llamada.

Para obtener una lista de válido **TargetName**, **clases de notificación** y opciones de encabezado, desproteger hello [notificaciones de inserción desde un servidor](http://msdn.microsoft.com/library/hh221551.aspx) página.

Hola siguiente código de ejemplo utiliza hello **MpnsService** instancia expuesto por hello **NotificationHubService** toosend una notificación de inserción del sistema:

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a>Cómo: enviar aplicaciones de plataforma de Windows (UWP) tooUniversal de notificaciones de inserción
Hola **WnsService** objeto proporciona un **enviar** método que puede ser utilizados toosend inserción notificaciones tooUniversal plataforma Windows aplicaciones.  Hola **enviar** método acepta Hola parámetros siguientes:

* **Etiquetas** -Hola identificador de etiquetas. Si no se proporciona ninguna etiqueta, se enviará a notificación de hello clientes tooall registrado.
* **Carga** -carga de mensaje de Hola XML.
* **Tipo** -Hola tipo de notificación.
* **Options** : encabezados de solicitud opcionales.
* **Devolución de llamada** -Hola función de devolución de llamada.

Para obtener una lista de tipos y encabezados de solicitud válidos, consulte [Encabezados de respuesta y solicitud del servicio de notificaciones de inserción (aplicaciones de Windows en tiempo de ejecución)](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).

Hello código siguiente usa hello **WnsService** instancia expuesto por hello **NotificationHubService** toosend una aplicación de UWP notificaciones del sistema tooa de notificación de inserción:

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a>Pasos siguientes
fragmentos de código del ejemplo de Hola anteriores permiten tooeasily compilación servicio infraestructura toodeliver inserción notificaciones tooa amplia variedad de dispositivos. Ahora que conoce los fundamentos de hello del uso de los centros de notificaciones con node.js, siga estos toolearn de vínculos más información acerca de cómo puede ampliar estas capacidades aún más.

* Vea Hola referencia MSDN para [centros de notificaciones de Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).
* Visite hello [Azure SDK para el nodo] repositorio en GitHub para obtener más ejemplos y detalles de implementación.

[Azure SDK para el nodo]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[sitio Web con WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Portal de Azure]: https://portal.azure.com
