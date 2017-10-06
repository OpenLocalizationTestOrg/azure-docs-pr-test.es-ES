---
title: aaaMonitor progreso del trabajo por el recuento de las tareas por estado - Azure Batch | Documentos de Microsoft
description: "Supervisar el progreso de Hola de un trabajo mediante una llamada a operación obtener recuentos de tarea de hello toocount tareas para un trabajo. Puede obtener un recuento de las tareas activas, en ejecución y completadas, y de las tareas que se realizaron correctamente o no."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: 03957d8a3d678bf44587f3bc7f988a76885c2af0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a>Recuento de tareas por estado toomonitor progreso del trabajo (vista previa)

Lote de Azure proporciona un progreso de hello toomonitor de manera eficaz de un trabajo mientras se ejecuta sus tareas. Puede llamar a hello [obtener recuentos de tarea] [ rest_get_task_counts] toofind operación cuántas tareas están en un estado activo, ejecución o completado, y el número tenga concluyó correctamente o no. Contando el número de Hola de tareas en cada estado, más fácilmente puede mostrar el usuario de tooa de progreso del trabajo de Hola o detectar retrasos inesperados o errores que pueden afectar al trabajo de Hola.

> [!IMPORTANT]
> Hola operación obtener recuentos de tareas está actualmente en vista previa y aún no está disponible en la administración pública de Azure y Azure China, Alemania de Azure. 
>
>

## <a name="how-tasks-are-counted"></a>Recuento de las tareas

Hola operación obtener recuentos de tarea cuenta tareas por estado, como se indica a continuación:

- Una tarea se cuenta como **active** cuando está en cola y puede toorun, pero no está asignado actualmente tooa de nodos de proceso. También se considera una tarea como **activa** si depende de una tarea primaria que no se ha completado. Para obtener más información sobre las dependencias entre tareas, consulte [crear dependencias entre tareas toorun tareas que dependen de otras tareas](batch-task-dependencies.md). 
- Una tarea se cuenta como **ejecuta** cuando se ha asignado el nodo de proceso de tooa, pero no se ha completado. Una tarea se cuenta como **ejecutando** cuando su estado sea `preparing` o `running`, como se indica por hello [obtener información acerca de una tarea] [ rest_get_task] operación.
- Una tarea se cuenta como **completado** cuando ya no es elegible toorun. Una tarea que se cuenta como **completada** normalmente ha finalizado correctamente, o ha finalizado de forma incorrecta pero ha agotado su límite de reintentos. 

Hola operación obtener recuentos de tareas también informa de cuántas tareas se realizó correctamente o no. Lote determina si una tarea ha se ha realizado correctamente o no comprobando hello **resultado** propiedad de hello [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] propiedad:

    - Una tarea se cuenta como **se realizó correctamente** si el resultado de hello de ejecución de la tarea es `success`.
    - Una tarea se cuenta como **no se pudo** si el resultado de hello de ejecución de la tarea es `failure`.

Para más información sobre los estados de las tareas, consulte [Obtención de información sobre una tarea][rest_get_task].

Hello .NET código siguiente muestra cómo tooretrieve tarea recuentos por estado: 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
Console.WriteLine("ValidationStatus: {0}", taskCounts.ValidationStatus);
```

> [!NOTE]
> Puede usar un patrón similar para REST y otros lenguajes compatibles tooget tarea recuentos para un trabajo. 
> 
> 

## <a name="consistency-checking-for-task-counts"></a>Comprobación de coherencia de los recuentos de tareas

servicio de lote de Hello agrega recuentos de tarea mediante la recopilación de datos de varias partes de un sistema distribuido asincrónico. tooensure esa tarea recuentos son correctos, lote proporciona una validación adicional para los recuentos de estado mediante la realización de comprobaciones de coherencia en varios componentes del sistema de Hola. Lote realiza estas comprobaciones de coherencia mientras hay menos de 200.000 tareas en el trabajo de Hola. En hello improbable que la comprobación de coherencia Hola encuentra errores, lote corrige resultado de hello de operación de obtener recuentos de las tareas de hello en función de los resultados de Hola Hola de comprobación de coherencia. Hola comprobación de coherencia es un tooensure medida adicional que los clientes que se basan en hello operación obtener recuentos de tarea obtienen información adecuada de Hola que necesita para su solución.

Hola **validationStatus** propiedad en la respuesta de hello indica si el lote ha realizado la comprobación de coherencia Hola. Si el lote no ha sido toocheck capaz de recuentos de estado con Estados real Hola mantenidos en el sistema de hello, Hola **validationStatus** propiedad se establece demasiado`unvalidated`. Por motivos de rendimiento por lotes no realizará la comprobación de coherencia de hello si Hola trabajo incluye más de 200.000 tareas, Hola así **validationStatus** propiedad puede establecerse demasiado`unvalidated` en este caso. Sin embargo, recuento de tareas de hello no es necesariamente incorrecto en este caso, tal y como es muy improbable que incluso una pérdida de datos muy limitados. 

Cuando una tarea cambia de estado, canalización de agregación de hello procesa el cambio de hello en pocos segundos. Hola operación obtener recuentos de tarea refleja recuentos de tarea hello actualizado dentro de ese período. Sin embargo, si un cambio en un estado de la tarea de errores de canalización de agregación de hello, a continuación, cambio no es registra hasta el siguiente paso de validación Hola. Durante este tiempo, recuentos de tareas pueden resultar ligeramente imprecisos debido toohello eventos que faltan, pero se ha corregido en el paso de validación siguiente Hola.

## <a name="best-practices-for-counting-a-jobs-tasks"></a>Procedimientos recomendados para el recuento de las tareas de un trabajo

Llamar a la operación obtener recuentos de tarea de hello es tooreturn de manera más eficaz de hello un recuento básico de las tareas de un trabajo por estado. Si está utilizando la versión de servicio de lote de 2017-06-01.5.1, se recomienda escribir o actualizar su toouse código obtener recuentos de tarea.

Hola operación obtener recuentos de tarea no está disponible en las versiones de servicio de lote anteriores a 2017-06-01.5.1. Si está utilizando una versión anterior del servicio de hello, a continuación, utilice una lista de tareas de toocount de consulta en un trabajo en su lugar. Para obtener más información, consulte [crear consultas eficazmente los recursos de proceso por lotes toolist](batch-efficient-list-queries.md).

## <a name="next-steps"></a>Pasos siguientes

* Vea hello [Introducción a la característica por lotes](batch-api-basics.md) toolearn más información sobre características y conceptos del servicio por lotes. Hola artículo describe los recursos de proceso por lotes principales hello como grupos, los nodos de proceso, trabajos y tareas y proporciona información general de las características del servicio de Hola.
* Información sobre conceptos básicos de Hola de desarrollar una aplicación habilitada por lotes con hello [biblioteca de cliente .NET de lote](batch-dotnet-get-started.md) o [Python](batch-python-tutorial.md). Estos artículos introductorios guiarán a través de una aplicación que utiliza tooexecute de servicio de lote de hello una carga de trabajo en varios nodos de ejecución.


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job
