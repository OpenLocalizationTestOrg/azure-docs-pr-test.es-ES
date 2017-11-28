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
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a><span data-ttu-id="0fcd1-104">Enviar mensajes SMS desde funciones de Azure con hello Twilio el enlace de salida</span><span class="sxs-lookup"><span data-stu-id="0fcd1-104">Send SMS messages from Azure Functions using hello Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0fcd1-105">Este artículo se explica cómo tooconfigure y usar enlaces de Twilio con funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-105">This article explains how tooconfigure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="0fcd1-106">Las funciones de Azure es compatible con Twilio salida enlaces tooenable el texto SMS de funciones toosend mensajes con unas pocas líneas de código y un [Twilio](https://www.twilio.com/) cuenta.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-106">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-hello-twilio-output-binding"></a><span data-ttu-id="0fcd1-107">enlace de salida de Twilio de Function.JSON para hello</span><span class="sxs-lookup"><span data-stu-id="0fcd1-107">function.json for hello Twilio output binding</span></span>
<span data-ttu-id="0fcd1-108">archivo de Hello function.json proporciona Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="0fcd1-108">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="0fcd1-109">`name`: Nombre variable utilizado en el código de función para hello mensaje de texto SMS Twilio.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-109">`name` : Variable name used in function code for hello Twilio SMS text message.</span></span>
* <span data-ttu-id="0fcd1-110">`type`: se debe establecer demasiado*"twilioSms"*.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-110">`type` : must be set too*"twilioSms"*.</span></span>
* <span data-ttu-id="0fcd1-111">`accountSid`: Este valor debe establecerse toohello nombre de una configuración de aplicación que contiene al Sid de la cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-111">`accountSid` : This value must be set toohello name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="0fcd1-112">`authToken`: Este valor debe establecerse toohello nombre de una configuración de aplicación que contiene el token de autenticación de Twilio.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-112">`authToken` : This value must be set toohello name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="0fcd1-113">`to`: Este valor se establece el número de teléfono de toohello texto SMS de Hola se envía a.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-113">`to` : This value is set toohello phone number that hello SMS text is sent to.</span></span>
* <span data-ttu-id="0fcd1-114">`from`: Este valor se establece el número de teléfono de toohello texto SMS de Hola se envía desde.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-114">`from` : This value is set toohello phone number that hello SMS text is sent from.</span></span>
* <span data-ttu-id="0fcd1-115">`direction`: se debe establecer demasiado*"out"*.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-115">`direction` : must be set too*"out"*.</span></span>
* <span data-ttu-id="0fcd1-116">`body`: Este valor puede ser el mensaje de texto SMS de toohard usa código Hola si no necesita tooset dinámicamente en Hola de código para la función.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-116">`body` : This value can be used toohard code hello SMS text message if you don't need tooset it dynamically in hello code for your function.</span></span> 

<span data-ttu-id="0fcd1-117">Function.json de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0fcd1-117">Example function.json:</span></span>

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="0fcd1-118">Ejemplo de desencadenador de cola de C# con enlace de salida de Twilio</span><span class="sxs-lookup"><span data-stu-id="0fcd1-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="0fcd1-119">Sincrónico</span><span class="sxs-lookup"><span data-stu-id="0fcd1-119">Synchronous</span></span>
<span data-ttu-id="0fcd1-120">Este código de ejemplo sincrónica de un desencadenador de la cola de almacenamiento de Azure usa un fuera parámetro toosend un cliente de tooa de mensaje de texto que ha realizado un pedido.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter toosend a text message tooa customer who placed an order.</span></span>

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

#### <a name="asynchronous"></a><span data-ttu-id="0fcd1-121">Asincrónico</span><span class="sxs-lookup"><span data-stu-id="0fcd1-121">Asynchronous</span></span>
<span data-ttu-id="0fcd1-122">Este código de ejemplo asincrónico de un desencadenador de la cola de almacenamiento de Azure envía a un cliente de tooa de mensaje de texto que ha realizado un pedido.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-122">This asynchronous example code for an Azure Storage queue trigger sends a text message tooa customer who placed an order.</span></span>

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

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="0fcd1-123">Ejemplo de desencadenador de cola de Node.js con enlace de salida de Twilio</span><span class="sxs-lookup"><span data-stu-id="0fcd1-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="0fcd1-124">En este ejemplo de Node.js envía a un cliente de tooa de mensaje de texto que ha realizado un pedido.</span><span class="sxs-lookup"><span data-stu-id="0fcd1-124">This Node.js example sends a text message tooa customer who placed an order.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0fcd1-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0fcd1-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

