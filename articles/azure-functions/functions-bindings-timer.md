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
# <a name="azure-functions-timer-trigger"></a>Desencadenador de temporizador de funciones de Azure

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo explica cómo temporizador tooconfigure y el código de desencadenadores en las funciones de Azure. Azure Functions incluye un enlace a un desencadenador de temporizador que le permite ejecutar su código de función según una programación definida. 

desencadenador de temporizador de Hello es compatible con varias instancias de escalado horizontal. Una sola instancia de una función de temporizador determinada se ejecuta en todas las instancias.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a>Desencadenador de temporizador
función de tooa de desencadenador de temporizador Hello usa Hola siguiente objeto JSON en hello `bindings` matriz de function.json:

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

Hola valo `schedule` es un [expresión CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que incluya estos seis campos: 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
>Muchas de las expresiones de cron Hola pueda encontrar en Internet omiten hello `{second}` campo. Si copia desde uno de ellos, necesita tooadjust para hello adicional `{second}` campo. Para obtener ejemplos específicos, vea [Programación de ejemplos](#examples) a continuación.

zona horaria Hola predeterminada que usa con expresiones de CRON hello es la hora Universal coordinada (UTC). toohave la expresión CRON basada en otra zona horaria, crear una nueva configuración de aplicación para la aplicación de la función denominada `WEBSITE_TIME_ZONE`. Conjunto Hola valor toohello nombre de hello deseado zona horaria como se muestra en hello [índice de zona horaria de Microsoft](https://msdn.microsoft.com/library/ms912391.aspx). 

Por ejemplo, la *Hora estándar del Este* (EST) es UTC-05:00. toohave el temporizador desencadenar activan a las 10:00 AM EST todos los días, Hola de uso siguiente expresión CRON que las cuentas para la zona horaria UTC:

```json
"schedule": "0 0 15 * * *",
``` 

Como alternativa, puede agregar una nueva configuración de aplicación para la aplicación de la función denominada `WEBSITE_TIME_ZONE` y establezca el valor de hello demasiado**hora estándar**.  A continuación, Hola siguiente expresión CRON podría utilizarse para 10:00 AM EST: 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a>Ejemplos de programación
Estos son algunos ejemplos de expresiones de CRON que puede utilizar para hello `schedule` propiedad. 

tootrigger una vez cada cinco minutos:

```json
"schedule": "0 */5 * * * *"
```

tootrigger una vez a la parte superior de Hola de cada hora:

```json
"schedule": "0 0 * * * *",
```

tootrigger una vez cada dos horas:

```json
"schedule": "0 0 */2 * * *",
```

una vez cada hora de 9 AM too5 tootrigger PM:

```json
"schedule": "0 0 9-17 * * *",
```

tootrigger a las 9:30 A.M. todos los días:

```json
"schedule": "0 30 9 * * *",
```

tootrigger a las 9:30 A.M. cada día de la semana:

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a>Uso del desencadenador
Cuando se invoca una función de desencadenador de temporizador, Hola [objeto de temporizador](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) se pasa a la función hello. Hello JSON siguiente es una representación de ejemplo Hola objeto de temporizador. 

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

## <a name="trigger-sample"></a>Ejemplo de desencadenador
Suponga que tiene Hola después de desencadenador de temporizador en hello `bindings` matriz de function.json:

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

Vea el ejemplo específico del idioma de Hola que lee al temporizador de hello toosee de objeto si se está ejecutando en tiempo de ejecución.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Ejemplo de desencadenador en C# #
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

### <a name="trigger-sample-in-f"></a>Ejemplo de desencadenador en F# #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Ejemplo de desencadenador en Node.js
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

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

