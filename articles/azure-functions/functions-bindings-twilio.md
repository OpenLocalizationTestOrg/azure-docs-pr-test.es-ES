---
title: enlace de funciones Twilio aaaAzure | Documentos de Microsoft
description: "Comprender cómo toouse Twilio enlaces con funciones de Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 882853947850e7d6795ca5b2f3fb6b9a83ede182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a>Enviar mensajes SMS desde funciones de Azure con hello Twilio el enlace de salida
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo se explica cómo tooconfigure y usar enlaces de Twilio con funciones de Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Las funciones de Azure es compatible con Twilio salida enlaces tooenable el texto SMS de funciones toosend mensajes con unas pocas líneas de código y un [Twilio](https://www.twilio.com/) cuenta. 

## <a name="functionjson-for-hello-twilio-output-binding"></a>enlace de salida de Twilio de Function.JSON para hello
archivo de Hello function.json proporciona Hola propiedades siguientes:

* `name`: Nombre variable utilizado en el código de función para hello mensaje de texto SMS Twilio.
* `type`: se debe establecer demasiado*"twilioSms"*.
* `accountSid`: Este valor debe establecerse toohello nombre de una configuración de aplicación que contiene al Sid de la cuenta de Twilio.
* `authToken`: Este valor debe establecerse toohello nombre de una configuración de aplicación que contiene el token de autenticación de Twilio.
* `to`: Este valor se establece el número de teléfono de toohello texto SMS de Hola se envía a.
* `from`: Este valor se establece el número de teléfono de toohello texto SMS de Hola se envía desde.
* `direction`: se debe establecer demasiado*"out"*.
* `body`: Este valor puede ser el mensaje de texto SMS de toohard usa código Hola si no necesita tooset dinámicamente en Hola de código para la función. 

Function.json de ejemplo:

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a>Ejemplo de desencadenador de cola de C# con enlace de salida de Twilio
#### <a name="synchronous"></a>Sincrónico
Este código de ejemplo sincrónica de un desencadenador de la cola de almacenamiento de Azure usa un fuera parámetro toosend un cliente de tooa de mensaje de texto que ha realizado un pedido.

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    message.Body = msg;
    message.too= order.mobileNumber;
}
```

#### <a name="asynchronous"></a>Asincrónico
Este código de ejemplo asincrónico de un desencadenador de la cola de almacenamiento de Azure envía a un cliente de tooa de mensaje de texto que ha realizado un pedido.

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.too= order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a>Ejemplo de desencadenador de cola de Node.js con enlace de salida de Twilio
En este ejemplo de Node.js envía a un cliente de tooa de mensaje de texto que ha realizado un pedido.

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        too: myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

