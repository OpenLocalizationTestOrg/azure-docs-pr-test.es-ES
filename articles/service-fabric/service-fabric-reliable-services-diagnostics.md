---
title: "aaaStateful diagnósticos de servicios de confianza | Documentos de Microsoft"
description: "Funcionalidad de diagnóstico para Reliable Services con estado"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ae0e8f99-69ab-4d45-896d-1fa80ed45659
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 6200800b858957c06039d9af062633b12a446318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>Funcionalidad de diagnóstico para Reliable Services con estado
Hola Stateful confiable servicios StatefulServiceBase clase emite [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) eventos que pueden ser utilizado toodebug Hola servicio, proporcione información sobre cómo está funcionando en tiempo de ejecución de Hola y ayudar a solucionar problemas.

## <a name="eventsource-events"></a>Eventos EventSource
Hola EventSource nombre hello Stateful confiable servicios StatefulServiceBase clase es "Microsoft-ServiceFabric-Services". Eventos de este origen de eventos aparecen en el [eventos de diagnósticos de](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) ventana cuando se servicio hello [depurar en Visual Studio](service-fabric-debugging-your-application.md).

Otros ejemplos de herramientas y tecnologías que ayudan a recopilar o ver eventos EventSource son [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Microsoft Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) y [Microsoft TraceEvent Library](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

## <a name="events"></a>Eventos
| Nombre del evento | Id. de evento | Nivel | Descripción del evento |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |Informativo |Emitido cuando se inicia la tarea RunAsync del servicio |
| StatefulRunAsyncCancellation |2 |Informativo |Emitido cuando se cancela la tarea RunAsync del servicio |
| StatefulRunAsyncCompletion |3 |Informativo |Emitido cuando se completa la tarea RunAsync del servicio |
| StatefulRunAsyncSlowCancellation |4 |Warning (Advertencia) |Genera cuando service Coredispatcher transcurrirán cancelación toocomplete demasiado larga |
| StatefulRunAsyncFailure |5 |Error |Emitido cuando la tarea RunAsync del servicio genera una excepción |

## <a name="interpret-events"></a>Interpretar eventos
Eventos StatefulRunAsyncInvocation, StatefulRunAsyncCompletion y StatefulRunAsyncCancellation son útiles toohello servicio writer toounderstand Hola ciclo de vida de un servicio, así como tiempo Hola para cuando un servicio se inicia, cancelado o completado . Esto puede ser útil al depurar problemas de servicio o el ciclo de vida de servicio de Hola de descripción.

Escritores del servicio deben prestar especial atención tooStatefulRunAsyncSlowCancellation y StatefulRunAsyncFailure eventos porque indican problemas con el servicio de Hola.

StatefulRunAsyncFailure se genera cada vez que Hola servicio RunAsync() tarea produce una excepción. Normalmente, una excepción indica un error o un error en el servicio de Hola. Además, excepción de hello hace hello toofail del servicio, por lo que ha movido tooa otro nodo. Esto puede ser una operación costosa y puede retrasar las solicitudes entrantes mientras se mueve el servicio de Hola. Escritores del servicio deben determinar causa Hola de excepción de hello y, si es posible, solucionarla.

StatefulRunAsyncSlowCancellation se genera cada vez que una solicitud de cancelación para la tarea de hello Coredispatcher tarda más de cuatro segundos. Cuando un servicio tarda demasiado toocomplete cancelación, afecta a la capacidad de Hola para hello servicio toobe rápidamente reiniciada en otro nodo. Esto puede afectar a Hola la disponibilidad general del servicio de Hola.

## <a name="next-steps"></a>Pasos siguientes
* [Proveedores de EventSource en PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
