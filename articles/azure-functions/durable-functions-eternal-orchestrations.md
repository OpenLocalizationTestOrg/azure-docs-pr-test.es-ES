---
title: 'Orquestaciones infinitas en Durable Functions: Azure'
description: "Aprenda a implementar orquestaciones infinitas mediante la extensión Durable Functions para Azure Functions."
services: functions
author: cgillum
manager: cfowler
editor: 
tags: 
keywords: 
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: 1256e7f0286d9eb6ea6498b024fba41eb9f6a641
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="eternal-orchestrations-in-durable-functions-azure-functions"></a>Orquestaciones infinitas en Durable Functions (Azure Functions)

Las *orquestaciones infinitas* son funciones de orquestador que nunca terminan. Son útiles si desea usar [Durable Functions](durable-functions-overview.md) con agregadores y con cualquier escenario que requiera un bucle infinito.

## <a name="orchestration-history"></a>Historial de orquestación

Como se explica en [Puntos de control y reproducción](durable-functions-checkpointing-and-replay.md), Durable Task Framework realiza un seguimiento del historial de cada función de orquestación. Este historial crecerá continuamente siempre y cuando la función de orquestador siga programando nuevo trabajo. Si la función de orquestador entra en un bucle infinito y programa trabajo continuamente, este historial podría alcanzar un tamaño crítico y provocar problemas de rendimiento considerables. El concepto de *orquestación infinita* se diseñó para mitigar este tipo de problemas en aplicaciones que necesitan bucles infinitos.

## <a name="resetting-and-restarting"></a>Restablecimiento y reinicio

En lugar de utilizar bucles infinitos, las funciones de orquestador restablecen su estado mediante una llamada al método [ContinueAsNew](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_ContinueAsNew_). Este método toma un único parámetro serializable con JSON, que se convierte en la nueva entrada para la siguiente generación de función de orquestador.

Cuando se llama a `ContinueAsNew`, la instancia pone en cola un mensaje para sí misma antes de cerrarse. El mensaje reinicia la instancia con el nuevo valor de entrada. Se conserva el mismo identificador de instancia, pero el historial de la función de orquestador se trunca eficazmente.

> [!NOTE]
> Durable Task Framework mantiene el mismo identificador de instancia, pero internamente crea un nuevo *identificador de ejecución* para la función de orquestador que `ContinueAsNew` restablece. Por lo general, este identificador de ejecución no se expone externamente, pero puede ser útil conocerlo al depurar la ejecución de la orquestación.

## <a name="periodic-work-example"></a>Ejemplo de trabajo periódico

Un caso práctico de orquestaciones infinitas es el del código que se necesita para realizar trabajo periódico indefinidamente.

```csharp
[FunctionName("Periodic_Cleanup_Loop")]
public static async Task Run(
    [OrchestrationTrigger] DurableOrchestrationContext context)
{
    await context.CallActivityAsync("DoCleanup");

    // sleep for one hour between cleanups
    DateTime nextCleanup = context.CurrentUtcDateTime.AddHours(1);
    await context.CreateTimer<string>(nextCleanup);

    context.ContinueAsNew(null);
}
```

La diferencia entre este ejemplo y una función desencadenada por temporizador es que aquí los tiempos del desencadenador de limpieza no se basan en una programación. Por ejemplo, una programación CRON que ejecuta una función cada hora lo hará a la 1:00, 2:00, 3:00, etc. y potencialmente podría encontrarse con problemas de superposición. Sin embargo, en este ejemplo, si la limpieza tarda 30 minutos, se programará a la 1:00, 2:30, 4:00, etc., de forma que no habrá posibilidad alguna de superposición.

## <a name="counter-example"></a>Ejemplo de contador

El siguiente es un ejemplo simplificado de una función de *contador* que escucha eventos de *incremento* y *decremento* indefinidamente.

```csharp
[FunctionName("SimpleCounter")]
public static async Task Run(
    [OrchestrationTrigger] DurableOrchestrationContext context)
{
    int counterState = context.GetInput<int>();

    string operation = await context.WaitForExternalEvent<string>("operation");

    if (operation == "incr")
    {
        counterState++;
    }
    else if (operation == "decr")
    {
        counterState--;
    }
    
    context.ContinueAsNew(counterState);
}
```

## <a name="exit-from-an-eternal-orchestration"></a>Salir de una orquestación infinita

Si en algún momento fuera necesario completar una función de orquestador, lo único que debe hacer es *no* llamar a `ContinueAsNew` y dejar que la función se cierre.

Si una función de orquestador está en un bucle infinito y debe detenerse, use el método [TerminateAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_TerminateAsync_) para detenerla. Para más información, consulte el artículo sobre la [administración de instancias](durable-functions-instance-management.md).

## <a name="next-steps"></a>pasos siguientes

> [!div class="nextstepaction"]
> [Más información acerca de cómo implementar orquestaciones singleton](durable-functions-singletons.md)

> [!div class="nextstepaction"]
> [Ejecutar una orquestación infinita de ejemplo](durable-functions-counter.md)
