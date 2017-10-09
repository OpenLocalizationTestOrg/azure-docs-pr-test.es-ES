---
title: desencadenador de temporizador de funciones aaaAzure | Documentos de Microsoft
description: "Comprender cómo toouse temporizador desencadena en funciones de Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 17fca22372dbc55d4684c8c099cc97923a7d3cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="0a9a3-104">Desencadenador de temporizador de funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="0a9a3-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0a9a3-105">Este artículo explica cómo temporizador tooconfigure y el código de desencadenadores en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-105">This article explains how tooconfigure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="0a9a3-106">Azure Functions incluye un enlace a un desencadenador de temporizador que le permite ejecutar su código de función según una programación definida.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="0a9a3-107">desencadenador de temporizador de Hello es compatible con varias instancias de escalado horizontal. Una sola instancia de una función de temporizador determinada se ejecuta en todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-107">hello timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="0a9a3-108">Desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="0a9a3-108">Timer trigger</span></span>
<span data-ttu-id="0a9a3-109">función de tooa de desencadenador de temporizador Hello usa Hola siguiente objeto JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-109">hello timer trigger tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="0a9a3-110">Hola valo `schedule` es un [expresión CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que incluya estos seis campos:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-110">hello value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="0a9a3-111">Muchas de las expresiones de cron Hola pueda encontrar en Internet omiten hello `{second}` campo.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-111">Many of hello cron expressions you find online omit hello `{second}` field.</span></span> <span data-ttu-id="0a9a3-112">Si copia desde uno de ellos, necesita tooadjust para hello adicional `{second}` campo.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-112">If you copy from one of them, you need tooadjust for hello extra `{second}` field.</span></span> <span data-ttu-id="0a9a3-113">Para obtener ejemplos específicos, vea [Programación de ejemplos](#examples) a continuación.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="0a9a3-114">zona horaria Hola predeterminada que usa con expresiones de CRON hello es la hora Universal coordinada (UTC).</span><span class="sxs-lookup"><span data-stu-id="0a9a3-114">hello default time zone used with hello CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="0a9a3-115">toohave la expresión CRON basada en otra zona horaria, crear una nueva configuración de aplicación para la aplicación de la función denominada `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-115">toohave your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="0a9a3-116">Conjunto Hola valor toohello nombre de hello deseado zona horaria como se muestra en hello [índice de zona horaria de Microsoft](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a9a3-116">Set hello value toohello name of hello desired time zone as shown in hello [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="0a9a3-117">Por ejemplo, la *Hora estándar del Este* (EST) es UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="0a9a3-118">toohave el temporizador desencadenar activan a las 10:00 AM EST todos los días, Hola de uso siguiente expresión CRON que las cuentas para la zona horaria UTC:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-118">toohave your timer trigger fire at 10:00 AM EST every day, use hello following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="0a9a3-119">Como alternativa, puede agregar una nueva configuración de aplicación para la aplicación de la función denominada `WEBSITE_TIME_ZONE` y establezca el valor de hello demasiado**hora estándar**.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set hello value too**Eastern Standard Time**.</span></span>  <span data-ttu-id="0a9a3-120">A continuación, Hola siguiente expresión CRON podría utilizarse para 10:00 AM EST:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-120">Then hello following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="0a9a3-121">Ejemplos de programación</span><span class="sxs-lookup"><span data-stu-id="0a9a3-121">Schedule examples</span></span>
<span data-ttu-id="0a9a3-122">Estos son algunos ejemplos de expresiones de CRON que puede utilizar para hello `schedule` propiedad.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-122">Here are some samples of CRON expressions you can use for hello `schedule` property.</span></span> 

<span data-ttu-id="0a9a3-123">tootrigger una vez cada cinco minutos:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-123">tootrigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="0a9a3-124">tootrigger una vez a la parte superior de Hola de cada hora:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-124">tootrigger once at hello top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="0a9a3-125">tootrigger una vez cada dos horas:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-125">tootrigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="0a9a3-126">una vez cada hora de 9 AM too5 tootrigger PM:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-126">tootrigger once every hour from 9 AM too5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="0a9a3-127">tootrigger a las 9:30 A.M. todos los días:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-127">tootrigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="0a9a3-128">tootrigger a las 9:30 A.M. cada día de la semana:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-128">tootrigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="0a9a3-129">Uso del desencadenador</span><span class="sxs-lookup"><span data-stu-id="0a9a3-129">Trigger usage</span></span>
<span data-ttu-id="0a9a3-130">Cuando se invoca una función de desencadenador de temporizador, Hola [objeto de temporizador](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) se pasa a la función hello.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-130">When a timer trigger function is invoked, hello [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into hello function.</span></span> <span data-ttu-id="0a9a3-131">Hello JSON siguiente es una representación de ejemplo Hola objeto de temporizador.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-131">hello following JSON is an example representation of hello timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="0a9a3-132">Ejemplo de desencadenador</span><span class="sxs-lookup"><span data-stu-id="0a9a3-132">Trigger sample</span></span>
<span data-ttu-id="0a9a3-133">Suponga que tiene Hola después de desencadenador de temporizador en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="0a9a3-133">Suppose you have hello following timer trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="0a9a3-134">Vea el ejemplo específico del idioma de Hola que lee al temporizador de hello toosee de objeto si se está ejecutando en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0a9a3-134">See hello language-specific sample that reads hello timer object toosee whether it's running late.</span></span>

* [<span data-ttu-id="0a9a3-135">C#</span><span class="sxs-lookup"><span data-stu-id="0a9a3-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="0a9a3-136">F#</span><span class="sxs-lookup"><span data-stu-id="0a9a3-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="0a9a3-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="0a9a3-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="0a9a3-138">Ejemplo de desencadenador en C#</span><span class="sxs-lookup"><span data-stu-id="0a9a3-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="0a9a3-139">Ejemplo de desencadenador en F#</span><span class="sxs-lookup"><span data-stu-id="0a9a3-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="0a9a3-140">Ejemplo de desencadenador en Node.js</span><span class="sxs-lookup"><span data-stu-id="0a9a3-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="0a9a3-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a9a3-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

