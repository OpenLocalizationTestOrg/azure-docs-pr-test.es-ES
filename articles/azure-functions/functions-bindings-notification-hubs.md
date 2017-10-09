---
title: enlace de centro de notificaciones de las funciones de aaaAzure | Documentos de Microsoft
description: "Comprender cómo toouse enlace de centro de notificaciones de Azure en las funciones de Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a>Enlace de salida de centros de notificaciones de Azure de funciones de Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo se explica cómo tooconfigure y el código de enlaces de centro de notificaciones de Azure en las funciones de Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Las funciones pueden enviar notificaciones push mediante un Centro de notificaciones de Azure configurado con tan solo unas líneas de código. Sin embargo, Hola centro de notificaciones de Azure debe configurarse para servicios de notificaciones de plataforma (PNS) que desee toouse Hola. Para obtener más información sobre cómo configurar un centro de notificaciones de Azure y desarrollar una aplicación cliente que inscribirse en las notificaciones de tooreceive, consulte [Introducción a centros de notificaciones](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) y haga clic en la plataforma de cliente de destino en hello Arriba.

pueden ser notificaciones Hola que envía notificaciones nativas o notificaciones de plantilla. Notificaciones nativas como destino una plataforma de notificación específico que esté establecida en hello `platform` propiedad de hello el enlace de salida. Una notificación de plantilla puede ser usado tootarget varias plataformas.   

## <a name="notification-hub-output-binding-properties"></a>Propiedades del enlace de salida del Centro de notificaciones
archivo de Hello function.json proporciona Hola propiedades siguientes:

* `name`: Nombre variable utilizado en el código de función para el mensaje de bienvenida de concentrador de notificación.
* `type`: se debe establecer demasiado*"notificationHub"*.
* `tagExpression`: Expresiones de etiqueta permiten toospecify que se entregan las notificaciones tooa conjunto de dispositivos que se hayan registrado tooreceive notificaciones que coinciden con la expresión de la etiqueta de Hola.  Para obtener más información, consulte [Expresiones de etiqueta y enrutamiento](../notification-hubs/notification-hubs-tags-segment-push-message.md).
* `hubName`: Nombre del recurso de concentrador de notificación de Hola Hola portal de Azure.
* `connection`: Esta cadena de conexión debe ser un **configuración de la aplicación** cadena de conexión configurada toohello *DefaultFullSharedAccessSignature* valor para el centro de notificaciones.
* `direction`: se debe establecer demasiado*"out"*. 
* `platform`: propiedad de la plataforma de hello indica la plataforma de notificación de hello dirige la notificación. Debe ser uno de hello siguientes valores:
  * De forma predeterminada, si se omite la propiedad de la plataforma de Hola de salida de hello de enlace, las notificaciones de plantilla pueden ser usado tootarget cualquier plataforma configurado en hello centro de notificaciones de Azure. Para obtener más información sobre cómo utilizar plantillas en general toosend entre las notificaciones de plataforma con un centro de notificaciones de Azure, consulte [plantillas](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).
  * `apns`: Apple Push Notification Service. Para obtener más información sobre cómo configurar centro de notificaciones de Hola para APNS y recibir la notificación de hello en una aplicación cliente, consulte [tooiOS de notificaciones de inserción de envío con centros de notificaciones de Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm`: [Amazon Device Messaging](https://developer.amazon.com/device-messaging). Para obtener más información sobre cómo configurar centro de notificaciones de Hola para ADM y recibir la notificación de hello en una aplicación Kindle, consulte [Introducción a centros de notificaciones para las aplicaciones de Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm`: [Google Cloud Messaging](https://developers.google.com/cloud-messaging/). También se admite la mensajería de nube de firebase, que es una versión nueva de GCM Hola. Para obtener más información sobre cómo configurar centro de notificaciones de Hola para GCM/FCM y recibir la notificación de hello en una aplicación de cliente de Android, consulte [tooAndroid de notificaciones de inserción de envío con centros de notificaciones de Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns`: [servicios de notificaciones push de Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) (WNS) que tienen como destino plataformas Windows. WNS también admite Windows Phone 8.1 y versiones posteriores. Para obtener más información sobre cómo configurar centro de notificaciones de Hola para WNS y recibir la notificación de hello en una aplicación de plataforma Universal de Windows (UWP), consulte [Introducción a la notificación de concentradores para aplicaciones universales de Windows plataforma](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns`: [servicio de notificaciones push de Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx) (MPNS). Esta plataforma es compatible con Windows Phone 8 y versiones anteriores. Para obtener más información sobre cómo configurar centro de notificaciones de Hola para MPNS y recibir la notificación de hello en una aplicación de Windows Phone, consulte [envío de notificaciones de inserción con centros de notificaciones de Azure en Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

Function.json de ejemplo:

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a>Configuración de la cadena de conexión del Centro de notificaciones
el enlace de salida toouse un centro de notificaciones, debe configurar la cadena de conexión de hello para el concentrador de Hola. Esto puede hacerse en hello *integrar* ficha seleccionando el centro de notificaciones o crear uno nuevo. 

También puede agregar manualmente una cadena de conexión para un centro existente mediante la adición de una cadena de conexión para hello *DefaultFullSharedAccessSignature* tooyour centro de notificaciones. Esta cadena de conexión proporciona el acceso de la función de mensajes de notificación de permiso toosend. Hola *DefaultFullSharedAccessSignature* valor de cadena de conexión puede tener acceso desde hello **claves** botón en la hoja principal de Hola de su recurso de base de datos central de notificación en hello portal de Azure. toomanually agregar una cadena de conexión para el concentrador, Hola uso pasos: 

1. En hello **aplicación de la función** hoja de hello portal de Azure, haga clic en **configuración de la aplicación de función > Ir configuración del servicio tooApp**.
2. Hola **configuración** hoja, haga clic en **configuración de la aplicación**.
3. Desplácese hacia abajo toohello **configuración de la aplicación** sección y agregue una entrada con nombre para *DefaultFullSharedAccessSignature* valor para el centro de notificaciones.
4. Hacer referencia a la aplicación establecer el nombre de la cadena en hello enlaces de salida. Similar demasiado**MyHubConnectionString** utilizados en el ejemplo de Hola anterior.

## <a name="apns-native-notifications-with-c-queue-triggers"></a>Notificaciones nativas de APNS con desencadenadores de colas de C#
Este ejemplo muestra cómo se definen los tipos de toouse en hello [biblioteca de los centros de notificaciones de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend una notificación nativa de APNS. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>Notificaciones nativas de GCM con desencadenadores de colas de C#
Este ejemplo muestra cómo se definen los tipos de toouse en hello [biblioteca de los centros de notificaciones de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend una notificación de GCM nativo. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a>Notificaciones nativas de WNS con desencadenadores de colas de C#
Este ejemplo muestra cómo se definen los tipos de toouse en hello [biblioteca de los centros de notificaciones de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend un WNS nativo Introducción notificación del sistema. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants toobe added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a>Ejemplo de plantillas para desencadenadores de temporizador de Node.js
En este ejemplo, se envía una notificación a un [registro de plantillas`message` que contiene ](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) y `location`.

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a>Ejemplo de plantillas para desencadenadores de temporizador de F#
En este ejemplo, se envía una notificación a un [registro de plantillas`message` que contiene ](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) y `location`.

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a>Ejemplo de plantilla con un parámetro de salida
En este ejemplo se envía una notificación un [registro de plantilla](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contiene un `message` marcador de posición en la plantilla de Hola.

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a>Ejemplo de plantilla de función asincrónica
Si va a utilizar código asincrónico, no se admiten parámetros de salida. En este caso use `IAsyncCollector` tooreturn la notificación de plantilla. Hello código siguiente es un ejemplo de código de hello anterior asincrónico. 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a>Ejemplo de plantilla con JSON
En este ejemplo se envía una notificación un [registro de plantilla](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contiene un `message` marcador de posición en la plantilla de hello mediante una cadena JSON válida.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>Ejemplo de plantilla con tipos de biblioteca de Notification Hubs
Este ejemplo muestra cómo se definen los tipos de toouse en hello [biblioteca de los centros de notificaciones de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/). 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

