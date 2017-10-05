---
title: Desencadenador de temporizador de Azure Functions | Microsoft Docs
description: "Descubra cómo utilizar desencadenadores de temporizador en funciones de Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "funciones de azure, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 6a97ab8508f889b77d064a5da70e3c726d62900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="fe1e1-104">Desencadenador de temporizador de funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="fe1e1-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="fe1e1-105">En este artículo se explica cómo configurar y codificar desencadenadores de temporizador en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="fe1e1-106">Azure Functions incluye un enlace a un desencadenador de temporizador que le permite ejecutar su código de función según una programación definida.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="fe1e1-107">El desencadenador de temporizador admite varias instancias de escalado horizontal. Una sola instancia de una función de temporizador determinada se ejecuta en todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="fe1e1-108">Desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="fe1e1-108">Timer trigger</span></span>
<span data-ttu-id="fe1e1-109">El desencadenador de temporizador de una función usa el siguiente objeto JSON en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="fe1e1-110">El valor de `schedule` es una [expresión CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que incluye estos seis campos:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="fe1e1-111">En muchas de las expresiones CRON que se encuentran en Internet se omite el campo `{second}`.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="fe1e1-112">Si copia alguna de ellas, deberá ajustarla para el campo `{second}` adicional.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="fe1e1-113">Para obtener ejemplos específicos, vea [Programación de ejemplos](#examples) a continuación.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="fe1e1-114">La zona horaria predeterminada que se usa con las expresiones CRON es la Hora universal coordinada (UTC).</span><span class="sxs-lookup"><span data-stu-id="fe1e1-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="fe1e1-115">Para que la expresión CRON se base en otra zona horaria, cree una nueva configuración de aplicación para la aplicación de función denominada `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="fe1e1-116">Establezca el valor en el nombre de la zona horaria deseada como se muestra en [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx) (Índice de zona horaria de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="fe1e1-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="fe1e1-117">Por ejemplo, la *Hora estándar del Este* (EST) es UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="fe1e1-118">Para que el desencadenador de temporizador se dispare a las 10 a.m. (Hora estándar), use la siguiente expresión CRON que representa la zona horaria UTC:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="fe1e1-119">Si lo prefiere, puede agregar una nueva configuración de aplicación para la aplicación de función denominada `WEBSITE_TIME_ZONE` y establecer el valor en **Hora estándar del Este**.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="fe1e1-120">A continuación, se podría usar la siguiente expresión CRON para las 10:00 EST:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="fe1e1-121">Ejemplos de programación</span><span class="sxs-lookup"><span data-stu-id="fe1e1-121">Schedule examples</span></span>
<span data-ttu-id="fe1e1-122">Estos son algunos ejemplos de expresiones CRON que puede utilizar para la propiedad `schedule`.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="fe1e1-123">Para que se desencadene una vez cada cinco minutos:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="fe1e1-124">Para desencadenar una vez al principio de cada hora:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="fe1e1-125">Para desencadenar una vez cada dos horas:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="fe1e1-126">Para desencadenar una vez cada hora de las 9:00 a las 17:00:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="fe1e1-127">Para desencadenar a las 9:30 cada día:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="fe1e1-128">Para desencadenar a 9:30 cada día comprendido entre lunes y viernes:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="fe1e1-129">Uso del desencadenador</span><span class="sxs-lookup"><span data-stu-id="fe1e1-129">Trigger usage</span></span>
<span data-ttu-id="fe1e1-130">Cuando se invoca una función de desencadenador de temporizador, se pasa a esta el [objeto de temporizador](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs).</span><span class="sxs-lookup"><span data-stu-id="fe1e1-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="fe1e1-131">La siguiente función JSON es un ejemplo que representa el objeto de temporizador.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-131">The following JSON is an example representation of the timer object.</span></span> 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="fe1e1-132">Ejemplo de desencadenador</span><span class="sxs-lookup"><span data-stu-id="fe1e1-132">Trigger sample</span></span>
<span data-ttu-id="fe1e1-133">Supongamos que el siguiente desencadenador de temporizador se encuentra en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="fe1e1-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="fe1e1-134">Vea el ejemplo específico del lenguaje que lee el objeto de temporizador para comprobar si se retrasa.</span><span class="sxs-lookup"><span data-stu-id="fe1e1-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="fe1e1-135">C#</span><span class="sxs-lookup"><span data-stu-id="fe1e1-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="fe1e1-136">F#</span><span class="sxs-lookup"><span data-stu-id="fe1e1-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="fe1e1-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="fe1e1-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="fe1e1-138">Ejemplo de desencadenador en C#</span><span class="sxs-lookup"><span data-stu-id="fe1e1-138">Trigger sample in C#</span></span> #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="fe1e1-139">Ejemplo de desencadenador en F#</span><span class="sxs-lookup"><span data-stu-id="fe1e1-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="fe1e1-140">Ejemplo de desencadenador en Node.js</span><span class="sxs-lookup"><span data-stu-id="fe1e1-140">Trigger sample in Node.js</span></span>
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="fe1e1-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe1e1-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

