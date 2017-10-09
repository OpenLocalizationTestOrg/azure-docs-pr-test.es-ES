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
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="77fd6-103">Ejecutar tareas simultáneamente toomaximize uso de nodos de proceso por lotes</span><span class="sxs-lookup"><span data-stu-id="77fd6-103">Run tasks concurrently toomaximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="77fd6-104">Al ejecutar más de una tarea simultáneamente en cada nodo de proceso en el grupo de lote de Azure, puede maximizar el uso de recursos en un menor número de nodos de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="77fd6-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in hello pool.</span></span> <span data-ttu-id="77fd6-105">Para algunas cargas de trabajo, esto puede reducir los costos y el tiempo dedicado al trabajo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="77fd6-106">Si bien algunos escenarios beneficiarán de dedicar todo de tarea única del tooa de recursos de un nodo, varias situaciones beneficiarán de lo que permite varias tooshare tareas esos recursos:</span><span class="sxs-lookup"><span data-stu-id="77fd6-106">While some scenarios benefit from dedicating all of a node's resources tooa single task, several situations benefit from allowing multiple tasks tooshare those resources:</span></span>

* <span data-ttu-id="77fd6-107">**Minimizar la transferencia de datos** cuando las tareas son tooshare capaz de datos.</span><span class="sxs-lookup"><span data-stu-id="77fd6-107">**Minimizing data transfer** when tasks are able tooshare data.</span></span> <span data-ttu-id="77fd6-108">En este escenario, puede reducir drásticamente los gastos de transferencia de datos mediante la copia de datos compartido tooa menor número de nodos y la ejecución de tareas en paralelo en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data tooa smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="77fd6-109">Esto se aplica especialmente si Hola data toobe tooeach copiada de nodo debe transferirse entre las regiones geográficas.</span><span class="sxs-lookup"><span data-stu-id="77fd6-109">This especially applies if hello data toobe copied tooeach node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="77fd6-110">**Maximizar el uso de memoria** cuando las tareas requieren una gran cantidad de memoria, pero solo durante períodos breves y en momentos variables durante la ejecución.</span><span class="sxs-lookup"><span data-stu-id="77fd6-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="77fd6-111">Puede emplear menos, pero más grandes, nodos con más de memoria de tooefficiently atender los picos de este tipo de proceso.</span><span class="sxs-lookup"><span data-stu-id="77fd6-111">You can employ fewer, but larger, compute nodes with more memory tooefficiently handle such spikes.</span></span> <span data-ttu-id="77fd6-112">Estos nodos tendría varias tareas que se ejecutan en paralelo en cada nodo, pero cada tarea podría sacar provecho de memoria abundantes los nodos hello en momentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="77fd6-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of hello nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="77fd6-113">**Mitigar los límites de número de nodos** cuando se requiere la comunicación entre nodos dentro de un grupo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="77fd6-114">Actualmente, los grupos configurados para la comunicación entre nodos son nodos de proceso too50 limitado.</span><span class="sxs-lookup"><span data-stu-id="77fd6-114">Currently, pools configured for inter-node communication are limited too50 compute nodes.</span></span> <span data-ttu-id="77fd6-115">Si cada nodo en un grupo de este tipo es capaz de tooexecute tareas en paralelo, un mayor número de tareas se pueden ejecutar simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="77fd6-115">If each node in such a pool is able tooexecute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="77fd6-116">**Replicación de un clúster de cálculo local**, por ejemplo, cuando se mueve un tooAzure de entorno de proceso.</span><span class="sxs-lookup"><span data-stu-id="77fd6-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment tooAzure.</span></span> <span data-ttu-id="77fd6-117">Si su solución local actual ejecuta varias tareas por nodo de proceso, puede aumentar el número máximo de Hola de tareas de nodo toomore reflejan fielmente esa configuración.</span><span class="sxs-lookup"><span data-stu-id="77fd6-117">If your current on-premises solution executes multiple tasks per compute node, you can increase hello maximum number of node tasks toomore closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="77fd6-118">Escenario de ejemplo</span><span class="sxs-lookup"><span data-stu-id="77fd6-118">Example scenario</span></span>
<span data-ttu-id="77fd6-119">Como un tooillustrate de ejemplo Hola ventajas de la ejecución de tareas paralelas, supongamos que la aplicación de la tarea tiene requisitos de CPU y memoria que [estándar\_D1](../cloud-services/cloud-services-sizes-specs.md) nodos son suficientes.</span><span class="sxs-lookup"><span data-stu-id="77fd6-119">As an example tooillustrate hello benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="77fd6-120">Sin embargo, en orden toofinish Hola trabajo en el tiempo necesario de hello 1.000 de estos nodos son necesarias.</span><span class="sxs-lookup"><span data-stu-id="77fd6-120">But, in order toofinish hello job in hello required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="77fd6-121">En lugar de utilizar nodos Standard\_D1 con un núcleo de CPU, podría utilizar nodos [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) con 16 núcleos en cada nodo y habilitar la ejecución de tareas en paralelo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="77fd6-122">En este caso, se podría usar un *número de nodos 16 veces menor* ; es decir, en lugar de 1000 nodos, solo serían necesarios 63.</span><span class="sxs-lookup"><span data-stu-id="77fd6-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="77fd6-123">Además, si los archivos de aplicación de gran tamaño o datos de referencia son necesarios para cada nodo, eficacia y la duración del trabajo se ve nuevamente mejorados puesto que los datos de hello tooonly copiada de 16 nodos.</span><span class="sxs-lookup"><span data-stu-id="77fd6-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since hello data is copied tooonly 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="77fd6-124">Habilitación de la ejecución en paralelo de tareas</span><span class="sxs-lookup"><span data-stu-id="77fd6-124">Enable parallel task execution</span></span>
<span data-ttu-id="77fd6-125">Configurar nodos de proceso para la ejecución de tareas paralelas en el nivel del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="77fd6-125">You configure compute nodes for parallel task execution at hello pool level.</span></span> <span data-ttu-id="77fd6-126">Con la biblioteca de .NET de lotes de hello, establecer hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propiedad cuando se crea un grupo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-126">With hello Batch .NET library, set hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="77fd6-127">Si utilizas Hola API de REST de proceso por lotes, establezca hello [maxTasksPerNode] [ rest_addpool] elemento de cuerpo de la solicitud de Hola durante la creación del grupo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-127">If you are using hello Batch REST API, set hello [maxTasksPerNode][rest_addpool] element in hello request body during pool creation.</span></span>

<span data-ttu-id="77fd6-128">Lote de Azure permite tooset tareas máximas por nodo toofour veces (4 x) Hola número de núcleos de nodo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-128">Azure Batch allows you tooset maximum tasks per node up toofour times (4x) hello number of node cores.</span></span> <span data-ttu-id="77fd6-129">Por ejemplo, si hello grupo está configurado con nodos de tamaño "Grande" (cuatro núcleos), a continuación, `maxTasksPerNode` se puede establecer too16.</span><span class="sxs-lookup"><span data-stu-id="77fd6-129">For example, if hello pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set too16.</span></span> <span data-ttu-id="77fd6-130">Para obtener detalles sobre el número de Hola de núcleos para cada uno de los tamaños de nodo de hello, consulte [tamaños para servicios en la nube](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="77fd6-130">For details on hello number of cores for each of hello node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="77fd6-131">Para obtener más información acerca de los límites de servicio, consulte [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="77fd6-131">For more information on service limits, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="77fd6-132">Ser seguro tootake en hello cuenta `maxTasksPerNode` valor cuando se crea un [fórmula de Autoescala] [ enable_autoscaling] para el grupo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-132">Be sure tootake into account hello `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="77fd6-133">Por ejemplo, una fórmula que evalúe `$RunningTasks` podría verse afectada considerablemente por un aumento en las tareas por nodo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="77fd6-134">Consulte [Escalación automática de los nodos de ejecución en un grupo de Lote de Azure](batch-automatic-scaling.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="77fd6-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="77fd6-135">Distribución de tareas</span><span class="sxs-lookup"><span data-stu-id="77fd6-135">Distribution of tasks</span></span>
<span data-ttu-id="77fd6-136">Cuando los nodos de proceso de hello en un grupo pueden ejecutar tareas simultáneamente, es importante toospecify cómo desea Hola tareas toobe distribuyen por los nodos de hello en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="77fd6-136">When hello compute nodes in a pool can execute tasks concurrently, it's important toospecify how you want hello tasks toobe distributed across hello nodes in hello pool.</span></span>

<span data-ttu-id="77fd6-137">Mediante el uso de hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] propiedad, puede especificar que las tareas deben asignarse de manera uniforme en todos los nodos de grupo de hello ("propagación").</span><span class="sxs-lookup"><span data-stu-id="77fd6-137">By using hello [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in hello pool ("spreading").</span></span> <span data-ttu-id="77fd6-138">O bien, puede especificar que todas las tareas como sea posible deben asignarse tooeach nodo antes de que se asignan tareas tooanother nodo grupo de hello ("empaquetado").</span><span class="sxs-lookup"><span data-stu-id="77fd6-138">Or you can specify that as many tasks as possible should be assigned tooeach node before tasks are assigned tooanother node in hello pool ("packing").</span></span>

<span data-ttu-id="77fd6-139">Como ejemplo de cómo esta característica es útil, considere la posibilidad de grupo de Hola de [estándar\_D14](../cloud-services/cloud-services-sizes-specs.md) nodos (en el ejemplo de Hola anterior) que se configura con un [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] valor de 16.</span><span class="sxs-lookup"><span data-stu-id="77fd6-139">As an example of how this feature is valuable, consider hello pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in hello example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="77fd6-140">Si hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] está configurado con un [ComputeNodeFillType] [ fill_type] de *Pack*, usaría maximizar el uso de todos los 16 núcleos de cada nodo y permitir una [grupo de escalado automático](batch-automatic-scaling.md) tooprune los nodos de grupo de hello (nodos que no tienen tareas asignadas).</span><span class="sxs-lookup"><span data-stu-id="77fd6-140">If hello [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) tooprune unused nodes from hello pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="77fd6-141">Esto minimiza el uso de recursos y permite ahorrar dinero.</span><span class="sxs-lookup"><span data-stu-id="77fd6-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="77fd6-142">Ejemplo de .NET Lote</span><span class="sxs-lookup"><span data-stu-id="77fd6-142">Batch .NET example</span></span>
<span data-ttu-id="77fd6-143">Esto [.NET de lotes] [ api_net] fragmento de código de API muestra una solicitud toocreate un grupo que contiene cuatro nodos grandes con un máximo de cuatro tareas por nodo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-143">This [Batch .NET][api_net] API code snippet shows a request toocreate a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="77fd6-144">Especifica una directiva que va a rellenar cada nodo con tareas anteriores tooassigning tareas tooanother nodo grupo de Hola de programación de tareas.</span><span class="sxs-lookup"><span data-stu-id="77fd6-144">It specifies a task scheduling policy that will fill each node with tasks prior tooassigning tasks tooanother node in hello pool.</span></span> <span data-ttu-id="77fd6-145">Para obtener más información sobre cómo agregar grupos mediante el uso de hello API de .NET de lote, consulte [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="77fd6-145">For more information on adding pools by using hello Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="77fd6-146">Ejemplo de REST Lote</span><span class="sxs-lookup"><span data-stu-id="77fd6-146">Batch REST example</span></span>
<span data-ttu-id="77fd6-147">Esto [REST de lote] [ api_rest] API fragmento muestra una solicitud toocreate un grupo que contiene dos nodos de gran tamaño con un máximo de cuatro tareas por nodo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-147">This [Batch REST][api_rest] API snippet shows a request toocreate a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="77fd6-148">Para obtener más información sobre cómo agregar grupos mediante el uso de API de REST de hello, consulte [agregar una cuenta del grupo de tooan][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="77fd6-148">For more information on adding pools by using hello REST API, see [Add a pool tooan account][rest_addpool].</span></span>

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
> <span data-ttu-id="77fd6-149">Puede establecer hello `maxTasksPerNode` elemento y [MaxTasksPerComputeNode] [ maxtasks_net] propiedad solo en el momento de creación de grupo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-149">You can set hello `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="77fd6-150">No se pueden modificar después de haberlos creado.</span><span class="sxs-lookup"><span data-stu-id="77fd6-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="77fd6-151">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="77fd6-151">Code sample</span></span>
<span data-ttu-id="77fd6-152">Hola [ParallelNodeTasks] [ parallel_tasks_sample] proyecto en GitHub muestra el uso de Hola de hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propiedad.</span><span class="sxs-lookup"><span data-stu-id="77fd6-152">hello [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates hello use of hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="77fd6-153">Esta aplicación de consola de C# utiliza hello [.NET de lotes] [ api_net] toocreate biblioteca un grupo con uno o varios nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="77fd6-153">This C# console application uses hello [Batch .NET][api_net] library toocreate a pool with one or more compute nodes.</span></span> <span data-ttu-id="77fd6-154">Un número configurable de tareas ejecuta en esas carga variable toosimulate de nodos.</span><span class="sxs-lookup"><span data-stu-id="77fd6-154">It executes a configurable number of tasks on those nodes toosimulate variable load.</span></span> <span data-ttu-id="77fd6-155">Resultado de la aplicación hello especifica qué nodos ejecutan cada tarea.</span><span class="sxs-lookup"><span data-stu-id="77fd6-155">Output from hello application specifies which nodes executed each task.</span></span> <span data-ttu-id="77fd6-156">aplicación Hello también proporciona un resumen de los parámetros de trabajo de Hola y duración.</span><span class="sxs-lookup"><span data-stu-id="77fd6-156">hello application also provides a summary of hello job parameters and duration.</span></span> <span data-ttu-id="77fd6-157">parte de resumen de Hola de salida de hello de dos ejecuciones diferentes de la aplicación de ejemplo de Hola aparece debajo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-157">hello summary portion of hello output from two different runs of hello sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="77fd6-158">primera ejecución de la aplicación de ejemplo de Hola de Hello muestra que con un solo nodo en el grupo de Hola y Hola predeterminada de una tarea por cada nodo, duración del trabajo de hello es en 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="77fd6-158">hello first execution of hello sample application shows that with a single node in hello pool and hello default setting of one task per node, hello job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="77fd6-159">Hola segunda ejecución de programas de ejemplo de Hola una importante disminución de la duración del trabajo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-159">hello second run of hello sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="77fd6-160">Esto es porque el grupo de Hola se configuró con cuatro tareas por nodo, lo que permite a casi una cuarta parte de hora de Hola para trabajo de tareas paralelas a la ejecución toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="77fd6-160">This is because hello pool was configured with four tasks per node, which allows for parallel task execution toocomplete hello job in nearly a quarter of hello time.</span></span>

> [!NOTE]
> <span data-ttu-id="77fd6-161">las duraciones de trabajo de Hello en resúmenes de hello anteriores no incluyen el tiempo de creación de grupo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-161">hello job durations in hello summaries above do not include pool creation time.</span></span> <span data-ttu-id="77fd6-162">Cada uno de los trabajos de hello anteriores era grupos toopreviously enviado creado cuyos nodos de proceso que se encontraban en hello *inactivo* estado en tiempo de envío.</span><span class="sxs-lookup"><span data-stu-id="77fd6-162">Each of hello jobs above was submitted toopreviously created pools whose compute nodes were in hello *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="77fd6-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="77fd6-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="77fd6-164">Mapa térmico de Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="77fd6-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="77fd6-165">Hola [Explorador de lote de Azure][batch_explorer], uno de hello Azure Batch [aplicaciones de ejemplo][github_samples], contiene un *mapa térmico* característica que permite la visualización de la ejecución de la tarea.</span><span class="sxs-lookup"><span data-stu-id="77fd6-165">hello [Azure Batch Explorer][batch_explorer], one of hello Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="77fd6-166">Cuando se está ejecutando el Hola [ParallelTasks] [ parallel_tasks_sample] aplicación de ejemplo, puede usar Hola mapa térmico característica tooeasily visualizar ejecución Hola de tareas en paralelo en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="77fd6-166">When you're executing hello [ParallelTasks][parallel_tasks_sample] sample application, you can use hello Heat Map feature tooeasily visualize hello execution of parallel tasks on each node.</span></span>

![Mapa térmico de Batch Explorer][1]

<span data-ttu-id="77fd6-168">*Mapa térmico de Batch Explorer que muestra un grupo de cuatro nodos, donde cada nodo ejecuta actualmente cuatro tareas*</span><span class="sxs-lookup"><span data-stu-id="77fd6-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
