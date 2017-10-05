---
title: Enlace de centros de notificaciones de Azure Functions | Microsoft Docs
description: "Descubra cómo utilizar los enlaces de centros de notificaciones en funciones de Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "funciones de azure, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: fa3d37b963c1bb6b58127b9180cd657d7b1dabcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="9a765-104">Enlace de salida de centros de notificaciones de Azure de funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="9a765-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="9a765-105">Este artículo explica cómo configurar y codificar enlaces de centros de notificaciones de Azure en funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a765-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="9a765-106">Las funciones pueden enviar notificaciones push mediante un Centro de notificaciones de Azure configurado con tan solo unas líneas de código.</span><span class="sxs-lookup"><span data-stu-id="9a765-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="9a765-107">Sin embargo, el Centro de notificaciones de Azure debe configurarse para los servicios de notificaciones de plataforma (PNS) que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="9a765-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="9a765-108">Para obtener más información sobre cómo configurar centros de notificaciones de Azure y desarrollar aplicaciones cliente que se registren para recibir notificaciones, consulte [Introducción a Centros de notificaciones](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) y haga clic en la plataforma de cliente de destino de la parte superior.</span><span class="sxs-lookup"><span data-stu-id="9a765-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="9a765-109">Las notificaciones que envía pueden ser nativas o de plantillas.</span><span class="sxs-lookup"><span data-stu-id="9a765-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="9a765-110">Las notificaciones nativas se envían a una plataforma de notificación específica, tal y como está configurado en la propiedad `platform` del enlace de salida.</span><span class="sxs-lookup"><span data-stu-id="9a765-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="9a765-111">Las notificaciones de plantillas pueden enviarse varias plataformas.</span><span class="sxs-lookup"><span data-stu-id="9a765-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="9a765-112">Propiedades del enlace de salida del Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="9a765-112">Notification hub output binding properties</span></span>
<span data-ttu-id="9a765-113">El archivo function.json ofrece las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="9a765-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="9a765-114">`name` : nombre de variable utilizado en el código de función para el mensaje del centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9a765-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="9a765-115">`type` : se debe establecer en *"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="9a765-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="9a765-116">`tagExpression` : las expresiones de etiqueta permiten especificar las notificaciones que se entregarán a un conjunto de dispositivos que se registraron para recibir las notificaciones que coincidan con estas expresiones.</span><span class="sxs-lookup"><span data-stu-id="9a765-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="9a765-117">Para obtener más información, consulte [Expresiones de etiqueta y enrutamiento](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="9a765-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="9a765-118">`hubName` : nombre del recurso del centro de notificaciones en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a765-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="9a765-119">`connection` : esta cadena de conexión debe ser una cadena de conexión de la **configuración de la aplicación** establecida en el valor *DefaultFullSharedAccessSignature* para el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9a765-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="9a765-120">`direction` : debe establecerse en *out*.</span><span class="sxs-lookup"><span data-stu-id="9a765-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="9a765-121">`platform`: la propiedad de plataforma indica la plataforma de notificación donde se enviará la notificación.</span><span class="sxs-lookup"><span data-stu-id="9a765-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="9a765-122">Debe ser uno de los siguientes valores: </span><span class="sxs-lookup"><span data-stu-id="9a765-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="9a765-123">De forma predeterminada, si se omite la propiedad de plataforma desde el enlace de salida, las notificaciones de plantilla se pueden usar para tener como destino cualquier plataforma configurada en el centro de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a765-123">By default, if the platform property is omitted from the output binding, template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="9a765-124">Para obtener más información sobre cómo utilizar plantillas en general para enviar notificaciones multiplataforma con un Centro de notificaciones de Azure, consulte [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) (Plantillas).</span><span class="sxs-lookup"><span data-stu-id="9a765-124">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="9a765-125">`apns`: Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="9a765-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="9a765-126">Para obtener más información sobre cómo configurar el Centro de notificaciones para APNS y recibir la notificación en una aplicación cliente, consulte [Envío de notificaciones push a iOS con Notification Hubs de Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9a765-126">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="9a765-127">`adm`: [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="9a765-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="9a765-128">Para obtener más información sobre cómo configurar el Centro de notificaciones para ADM y recibir la notificación en una aplicación de Kindle, consulte [Introducción a Notification Hubs para aplicaciones Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="9a765-128">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="9a765-129">`gcm`: [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="9a765-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="9a765-130">También se admite Firebase Cloud Messaging, que es la nueva versión de GCM.</span><span class="sxs-lookup"><span data-stu-id="9a765-130">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="9a765-131">Para obtener más información sobre cómo configurar el Centro de notificaciones para GCM o FCM y recibir la notificación en una aplicación cliente, consulte [Envío de notificaciones push a Android con Notification Hubs de Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9a765-131">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="9a765-132">`wns`: [servicios de notificaciones push de Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) (WNS) que tienen como destino plataformas Windows.</span><span class="sxs-lookup"><span data-stu-id="9a765-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="9a765-133">WNS también admite Windows Phone 8.1 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="9a765-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="9a765-134">Para obtener más información sobre cómo configurar el Centro de notificaciones para WNS y recibir la notificación en una aplicación de la Plataforma universal de Windows (UWP), consulte [Introducción a Notification Hubs para aplicaciones de la plataforma universal de Windows](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="9a765-134">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="9a765-135">`mpns`: [servicio de notificaciones push de Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx) (MPNS).</span><span class="sxs-lookup"><span data-stu-id="9a765-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="9a765-136">Esta plataforma es compatible con Windows Phone 8 y versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="9a765-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="9a765-137">Para obtener más información sobre cómo configurar el Centro de notificaciones para MPNS y recibir la notificación en una aplicación de Windows Phone, consulte [Envío de notificaciones push con Notification Hubs de Azure en Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md).</span><span class="sxs-lookup"><span data-stu-id="9a765-137">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="9a765-138">Function.json de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a765-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="9a765-139">Configuración de la cadena de conexión del Centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="9a765-139">Notification hub connection string setup</span></span>
<span data-ttu-id="9a765-140">Para usar un enlace de salida del Centro de notificaciones, debe configurar la cadena de conexión para él.</span><span class="sxs-lookup"><span data-stu-id="9a765-140">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="9a765-141">Puede hacerlo en la pestaña *Integrar* seleccionando el Centro de notificaciones o creando uno.</span><span class="sxs-lookup"><span data-stu-id="9a765-141">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="9a765-142">También puede agregar manualmente una cadena de conexión para un centro existente mediante la adición de una cadena de conexión para *DefaultFullSharedAccessSignature* al centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9a765-142">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="9a765-143">Esta cadena de conexión le proporciona sus permisos de acceso de función para enviar mensajes de notificación.</span><span class="sxs-lookup"><span data-stu-id="9a765-143">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="9a765-144">Al valor de la cadena de conexión *DefaultFullSharedAccessSignature* se puede acceder desde el botón **Claves** de la hoja principal del recurso del centro de notificaciones en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a765-144">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="9a765-145">Para agregar manualmente una cadena de conexión para su centro, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9a765-145">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="9a765-146">En la hoja **Function App** de Azure Portal, haga clic en **Configuración de Function App > Ir a Configuración de App Service**.</span><span class="sxs-lookup"><span data-stu-id="9a765-146">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="9a765-147">Vuelva a la hoja **Configuración** y haga clic en **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="9a765-147">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="9a765-148">Desplácese hacia abajo hasta la sección **Configuración de aplicación** y agregue una entrada con nombre para el valor *DefaultFullSharedAccessSignature* del Centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9a765-148">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="9a765-149">Haga referencia al nombre de la cadena de conexión de Configuración de aplicación en los enlaces de salida.</span><span class="sxs-lookup"><span data-stu-id="9a765-149">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="9a765-150">De forma parecida al valor **MyHubConnectionString** utilizado en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="9a765-150">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="9a765-151">Notificaciones nativas de APNS con desencadenadores de colas de C#</span><span class="sxs-lookup"><span data-stu-id="9a765-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="9a765-152">En este ejemplo, se muestra cómo utilizar los tipos definidos en la [biblioteca de Notification Hubs de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) para enviar una notificación de APNS nativa.</span><span class="sxs-lookup"><span data-stu-id="9a765-152">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="9a765-153">Notificaciones nativas de GCM con desencadenadores de colas de C#</span><span class="sxs-lookup"><span data-stu-id="9a765-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="9a765-154">En este ejemplo, se muestra cómo utilizar los tipos definidos en la [biblioteca de Notification Hubs de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) para enviar una notificación de GCM nativa.</span><span class="sxs-lookup"><span data-stu-id="9a765-154">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="9a765-155">Notificaciones nativas de WNS con desencadenadores de colas de C#</span><span class="sxs-lookup"><span data-stu-id="9a765-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="9a765-156">En este ejemplo, se muestra cómo utilizar los tipos definidos en la [biblioteca de Notification Hubs de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) para enviar una notificación de WNS nativa.</span><span class="sxs-lookup"><span data-stu-id="9a765-156">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
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
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="9a765-157">Ejemplo de plantillas para desencadenadores de temporizador de Node.js</span><span class="sxs-lookup"><span data-stu-id="9a765-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="9a765-158">En este ejemplo, se envía una notificación a un [registro de plantillas`message` que contiene ](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) y `location`.</span><span class="sxs-lookup"><span data-stu-id="9a765-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="9a765-159">Ejemplo de plantillas para desencadenadores de temporizador de F#</span><span class="sxs-lookup"><span data-stu-id="9a765-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="9a765-160">En este ejemplo, se envía una notificación a un [registro de plantillas`message` que contiene ](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) y `location`.</span><span class="sxs-lookup"><span data-stu-id="9a765-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="9a765-161">Ejemplo de plantilla con un parámetro de salida</span><span class="sxs-lookup"><span data-stu-id="9a765-161">Template example using an out parameter</span></span>
<span data-ttu-id="9a765-162">En este ejemplo, se envía una notificación a un [registro de plantillas](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contiene un marcador de posición `message` en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="9a765-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="9a765-163">Ejemplo de plantilla de función asincrónica</span><span class="sxs-lookup"><span data-stu-id="9a765-163">Template example with asynchronous function</span></span>
<span data-ttu-id="9a765-164">Si va a utilizar código asincrónico, no se admiten parámetros de salida.</span><span class="sxs-lookup"><span data-stu-id="9a765-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="9a765-165">En este caso, utilice `IAsyncCollector` para devolver la notificación de plantillas.</span><span class="sxs-lookup"><span data-stu-id="9a765-165">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="9a765-166">El código siguiente es un ejemplo asincrónico del anterior.</span><span class="sxs-lookup"><span data-stu-id="9a765-166">The following code is an asynchronous example of the code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="9a765-167">Ejemplo de plantilla con JSON</span><span class="sxs-lookup"><span data-stu-id="9a765-167">Template example using JSON</span></span>
<span data-ttu-id="9a765-168">En este ejemplo, se envía una notificación a un [registro de plantillas](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) que contiene un marcador de posición `message` en la plantilla mediante una cadena JSON válida.</span><span class="sxs-lookup"><span data-stu-id="9a765-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="9a765-169">Ejemplo de plantilla con tipos de biblioteca de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="9a765-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="9a765-170">En este ejemplo, se muestra cómo utilizar los tipos definidos en la [biblioteca de Notification Hubs de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="9a765-170">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="9a765-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a765-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

