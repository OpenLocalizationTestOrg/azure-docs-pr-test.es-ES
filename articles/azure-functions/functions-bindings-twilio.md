---
title: Enlace de Twilio de Azure Functions | Microsoft Docs
description: "Entender cómo usar enlaces de Twilio con Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "funciones de azure, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 870e47ec7f8ce41ee4acadc7b8ed59298958acbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="send-sms-messages-from-azure-functions-using-the-twilio-output-binding"></a><span data-ttu-id="3a049-104">Envío de mensajes SMS desde Azure Functions mediante el enlace de salida de Twilio</span><span class="sxs-lookup"><span data-stu-id="3a049-104">Send SMS messages from Azure Functions using the Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="3a049-105">En este artículo se explica cómo configurar y usar enlaces de Twilio con Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3a049-105">This article explains how to configure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="3a049-106">Azure Functions admite enlaces de salida de Twilio para permitir a sus funciones enviar mensajes de texto SMS con unas cuantas líneas de código y una cuenta de [Twilio](https://www.twilio.com/).</span><span class="sxs-lookup"><span data-stu-id="3a049-106">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-the-twilio-output-binding"></a><span data-ttu-id="3a049-107">function.json para el enlace de salida de Twilio</span><span class="sxs-lookup"><span data-stu-id="3a049-107">function.json for the Twilio output binding</span></span>
<span data-ttu-id="3a049-108">El archivo function.json ofrece las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="3a049-108">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="3a049-109">`name`: nombre de variable usado en el código de función para el mensaje de texto SMS de Twilio.</span><span class="sxs-lookup"><span data-stu-id="3a049-109">`name` : Variable name used in function code for the Twilio SMS text message.</span></span>
* <span data-ttu-id="3a049-110">`type`: se debe establecer en *"twilioSms"*.</span><span class="sxs-lookup"><span data-stu-id="3a049-110">`type` : must be set to *"twilioSms"*.</span></span>
* <span data-ttu-id="3a049-111">`accountSid`: este valor debe establecerse en el nombre de una configuración de aplicación que contiene al SID de la cuenta de Twilio.</span><span class="sxs-lookup"><span data-stu-id="3a049-111">`accountSid` : This value must be set to the name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="3a049-112">`authToken`: este valor debe establecerse en el nombre de una configuración de aplicación que contiene el token de autenticación de Twilio.</span><span class="sxs-lookup"><span data-stu-id="3a049-112">`authToken` : This value must be set to the name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="3a049-113">`to`: este valor se establece en el número de teléfono al que se envía el texto SMS.</span><span class="sxs-lookup"><span data-stu-id="3a049-113">`to` : This value is set to the phone number that the SMS text is sent to.</span></span>
* <span data-ttu-id="3a049-114">`from`: este valor se establece en el número de teléfono desde el que se envía el texto del SMS.</span><span class="sxs-lookup"><span data-stu-id="3a049-114">`from` : This value is set to the phone number that the SMS text is sent from.</span></span>
* <span data-ttu-id="3a049-115">`direction` : debe establecerse en *out*.</span><span class="sxs-lookup"><span data-stu-id="3a049-115">`direction` : must be set to *"out"*.</span></span>
* <span data-ttu-id="3a049-116">`body`: este valor se puede usar para codificar el mensaje de texto SMS si no necesita establecerlo dinámicamente en el código de la función.</span><span class="sxs-lookup"><span data-stu-id="3a049-116">`body` : This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function.</span></span> 

<span data-ttu-id="3a049-117">Function.json de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3a049-117">Example function.json:</span></span>

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="3a049-118">Ejemplo de desencadenador de cola de C# con enlace de salida de Twilio</span><span class="sxs-lookup"><span data-stu-id="3a049-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="3a049-119">Sincrónico</span><span class="sxs-lookup"><span data-stu-id="3a049-119">Synchronous</span></span>
<span data-ttu-id="3a049-120">Este código de ejemplo sincrónico de un desencadenador de cola de Azure Storage usa un parámetro de salida para enviar un mensaje de texto a un cliente que ha realizado un pedido.</span><span class="sxs-lookup"><span data-stu-id="3a049-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter to send a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    message.Body = msg;
    message.To = order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="3a049-121">Asincrónico</span><span class="sxs-lookup"><span data-stu-id="3a049-121">Asynchronous</span></span>
<span data-ttu-id="3a049-122">Este código de ejemplo asincrónico de un desencadenador de cola de Azure Storage envía un mensaje de texto a un cliente que ha realizado un pedido.</span><span class="sxs-lookup"><span data-stu-id="3a049-122">This asynchronous example code for an Azure Storage queue trigger sends a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.To = order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="3a049-123">Ejemplo de desencadenador de cola de Node.js con enlace de salida de Twilio</span><span class="sxs-lookup"><span data-stu-id="3a049-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="3a049-124">En este ejemplo de Node.js se envía un mensaje de texto a un cliente que ha realizado un pedido.</span><span class="sxs-lookup"><span data-stu-id="3a049-124">This Node.js example sends a text message to a customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        to : myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="3a049-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3a049-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

