---
title: aaaRun tareas en paralelo toouse recursos de proceso eficazmente - Azure Batch | Documentos de Microsoft
description: "Aumente la eficiencia y reduzca los costos usando menos nodos de proceso y ejecutando tareas simultáneas en cada nodo de un grupo de Lote de Azure"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a>Ejecutar tareas simultáneamente toomaximize uso de nodos de proceso por lotes 

Al ejecutar más de una tarea simultáneamente en cada nodo de proceso en el grupo de lote de Azure, puede maximizar el uso de recursos en un menor número de nodos de grupo de Hola. Para algunas cargas de trabajo, esto puede reducir los costos y el tiempo dedicado al trabajo.

Si bien algunos escenarios beneficiarán de dedicar todo de tarea única del tooa de recursos de un nodo, varias situaciones beneficiarán de lo que permite varias tooshare tareas esos recursos:

* **Minimizar la transferencia de datos** cuando las tareas son tooshare capaz de datos. En este escenario, puede reducir drásticamente los gastos de transferencia de datos mediante la copia de datos compartido tooa menor número de nodos y la ejecución de tareas en paralelo en cada nodo. Esto se aplica especialmente si Hola data toobe tooeach copiada de nodo debe transferirse entre las regiones geográficas.
* **Maximizar el uso de memoria** cuando las tareas requieren una gran cantidad de memoria, pero solo durante períodos breves y en momentos variables durante la ejecución. Puede emplear menos, pero más grandes, nodos con más de memoria de tooefficiently atender los picos de este tipo de proceso. Estos nodos tendría varias tareas que se ejecutan en paralelo en cada nodo, pero cada tarea podría sacar provecho de memoria abundantes los nodos hello en momentos diferentes.
* **Mitigar los límites de número de nodos** cuando se requiere la comunicación entre nodos dentro de un grupo. Actualmente, los grupos configurados para la comunicación entre nodos son nodos de proceso too50 limitado. Si cada nodo en un grupo de este tipo es capaz de tooexecute tareas en paralelo, un mayor número de tareas se pueden ejecutar simultáneamente.
* **Replicación de un clúster de cálculo local**, por ejemplo, cuando se mueve un tooAzure de entorno de proceso. Si su solución local actual ejecuta varias tareas por nodo de proceso, puede aumentar el número máximo de Hola de tareas de nodo toomore reflejan fielmente esa configuración.

## <a name="example-scenario"></a>Escenario de ejemplo
Como un tooillustrate de ejemplo Hola ventajas de la ejecución de tareas paralelas, supongamos que la aplicación de la tarea tiene requisitos de CPU y memoria que [estándar\_D1](../cloud-services/cloud-services-sizes-specs.md) nodos son suficientes. Sin embargo, en orden toofinish Hola trabajo en el tiempo necesario de hello 1.000 de estos nodos son necesarias.

En lugar de utilizar nodos Standard\_D1 con un núcleo de CPU, podría utilizar nodos [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) con 16 núcleos en cada nodo y habilitar la ejecución de tareas en paralelo. En este caso, se podría usar un *número de nodos 16 veces menor* ; es decir, en lugar de 1000 nodos, solo serían necesarios 63. Además, si los archivos de aplicación de gran tamaño o datos de referencia son necesarios para cada nodo, eficacia y la duración del trabajo se ve nuevamente mejorados puesto que los datos de hello tooonly copiada de 16 nodos.

## <a name="enable-parallel-task-execution"></a>Habilitación de la ejecución en paralelo de tareas
Configurar nodos de proceso para la ejecución de tareas paralelas en el nivel del grupo de Hola. Con la biblioteca de .NET de lotes de hello, establecer hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propiedad cuando se crea un grupo. Si utilizas Hola API de REST de proceso por lotes, establezca hello [maxTasksPerNode] [ rest_addpool] elemento de cuerpo de la solicitud de Hola durante la creación del grupo.

Lote de Azure permite tooset tareas máximas por nodo toofour veces (4 x) Hola número de núcleos de nodo. Por ejemplo, si hello grupo está configurado con nodos de tamaño "Grande" (cuatro núcleos), a continuación, `maxTasksPerNode` se puede establecer too16. Para obtener detalles sobre el número de Hola de núcleos para cada uno de los tamaños de nodo de hello, consulte [tamaños para servicios en la nube](../cloud-services/cloud-services-sizes-specs.md). Para obtener más información acerca de los límites de servicio, consulte [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md).

> [!TIP]
> Ser seguro tootake en hello cuenta `maxTasksPerNode` valor cuando se crea un [fórmula de Autoescala] [ enable_autoscaling] para el grupo. Por ejemplo, una fórmula que evalúe `$RunningTasks` podría verse afectada considerablemente por un aumento en las tareas por nodo. Consulte [Escalación automática de los nodos de ejecución en un grupo de Lote de Azure](batch-automatic-scaling.md) para obtener más información.
>
>

## <a name="distribution-of-tasks"></a>Distribución de tareas
Cuando los nodos de proceso de hello en un grupo pueden ejecutar tareas simultáneamente, es importante toospecify cómo desea Hola tareas toobe distribuyen por los nodos de hello en el grupo de Hola.

Mediante el uso de hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] propiedad, puede especificar que las tareas deben asignarse de manera uniforme en todos los nodos de grupo de hello ("propagación"). O bien, puede especificar que todas las tareas como sea posible deben asignarse tooeach nodo antes de que se asignan tareas tooanother nodo grupo de hello ("empaquetado").

Como ejemplo de cómo esta característica es útil, considere la posibilidad de grupo de Hola de [estándar\_D14](../cloud-services/cloud-services-sizes-specs.md) nodos (en el ejemplo de Hola anterior) que se configura con un [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] valor de 16. Si hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] está configurado con un [ComputeNodeFillType] [ fill_type] de *Pack*, usaría maximizar el uso de todos los 16 núcleos de cada nodo y permitir una [grupo de escalado automático](batch-automatic-scaling.md) tooprune los nodos de grupo de hello (nodos que no tienen tareas asignadas). Esto minimiza el uso de recursos y permite ahorrar dinero.

## <a name="batch-net-example"></a>Ejemplo de .NET Lote
Esto [.NET de lotes] [ api_net] fragmento de código de API muestra una solicitud toocreate un grupo que contiene cuatro nodos grandes con un máximo de cuatro tareas por nodo. Especifica una directiva que va a rellenar cada nodo con tareas anteriores tooassigning tareas tooanother nodo grupo de Hola de programación de tareas. Para obtener más información sobre cómo agregar grupos mediante el uso de hello API de .NET de lote, consulte [BatchClient.PoolOperations.CreatePool][poolcreate_net].

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a>Ejemplo de REST Lote
Esto [REST de lote] [ api_rest] API fragmento muestra una solicitud toocreate un grupo que contiene dos nodos de gran tamaño con un máximo de cuatro tareas por nodo. Para obtener más información sobre cómo agregar grupos mediante el uso de API de REST de hello, consulte [agregar una cuenta del grupo de tooan][rest_addpool].

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> Puede establecer hello `maxTasksPerNode` elemento y [MaxTasksPerComputeNode] [ maxtasks_net] propiedad solo en el momento de creación de grupo. No se pueden modificar después de haberlos creado.
>
>

## <a name="code-sample"></a>Código de ejemplo
Hola [ParallelNodeTasks] [ parallel_tasks_sample] proyecto en GitHub muestra el uso de Hola de hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propiedad.

Esta aplicación de consola de C# utiliza hello [.NET de lotes] [ api_net] toocreate biblioteca un grupo con uno o varios nodos de proceso. Un número configurable de tareas ejecuta en esas carga variable toosimulate de nodos. Resultado de la aplicación hello especifica qué nodos ejecutan cada tarea. aplicación Hello también proporciona un resumen de los parámetros de trabajo de Hola y duración. parte de resumen de Hola de salida de hello de dos ejecuciones diferentes de la aplicación de ejemplo de Hola aparece debajo.

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

primera ejecución de la aplicación de ejemplo de Hola de Hello muestra que con un solo nodo en el grupo de Hola y Hola predeterminada de una tarea por cada nodo, duración del trabajo de hello es en 30 minutos.

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

Hola segunda ejecución de programas de ejemplo de Hola una importante disminución de la duración del trabajo. Esto es porque el grupo de Hola se configuró con cuatro tareas por nodo, lo que permite a casi una cuarta parte de hora de Hola para trabajo de tareas paralelas a la ejecución toocomplete Hola.

> [!NOTE]
> las duraciones de trabajo de Hello en resúmenes de hello anteriores no incluyen el tiempo de creación de grupo. Cada uno de los trabajos de hello anteriores era grupos toopreviously enviado creado cuyos nodos de proceso que se encontraban en hello *inactivo* estado en tiempo de envío.
>
>

## <a name="next-steps"></a>Pasos siguientes
### <a name="batch-explorer-heat-map"></a>Mapa térmico de Batch Explorer
Hola [Explorador de lote de Azure][batch_explorer], uno de hello Azure Batch [aplicaciones de ejemplo][github_samples], contiene un *mapa térmico* característica que permite la visualización de la ejecución de la tarea. Cuando se está ejecutando el Hola [ParallelTasks] [ parallel_tasks_sample] aplicación de ejemplo, puede usar Hola mapa térmico característica tooeasily visualizar ejecución Hola de tareas en paralelo en cada nodo.

![Mapa térmico de Batch Explorer][1]

*Mapa térmico de Batch Explorer que muestra un grupo de cuatro nodos, donde cada nodo ejecuta actualmente cuatro tareas*

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
