---
title: "Ejecución de tareas en paralelo para usar recursos de procesos con eficacia - Azure Batch | Microsoft Docs"
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
ms.openlocfilehash: 6903552d907a1ddb21d3b678e2d224b4b5e35b77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-concurrently-to-maximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="941a5-103">Ejecución simultánea de tareas para maximizar el uso de los nodos de proceso de Batch</span><span class="sxs-lookup"><span data-stu-id="941a5-103">Run tasks concurrently to maximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="941a5-104">A través de la ejecución simultánea de más de una tarea en cada nodo de proceso dentro del grupo de Lote de Azure, puede maximizar el uso de recursos en un menor número de nodos en el grupo.</span><span class="sxs-lookup"><span data-stu-id="941a5-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span></span> <span data-ttu-id="941a5-105">Para algunas cargas de trabajo, esto puede reducir los costos y el tiempo dedicado al trabajo.</span><span class="sxs-lookup"><span data-stu-id="941a5-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="941a5-106">Aunque en algunos casos puede resultar beneficioso que todos los recursos de un nodo estén dedicados a una sola tarea, en otras situaciones será conveniente permitir que varias tareas compartan esos recursos:</span><span class="sxs-lookup"><span data-stu-id="941a5-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span></span>

* <span data-ttu-id="941a5-107">**Minimizar la transferencia de datos** cuando las tareas son capaces de compartir datos.</span><span class="sxs-lookup"><span data-stu-id="941a5-107">**Minimizing data transfer** when tasks are able to share data.</span></span> <span data-ttu-id="941a5-108">En este escenario, puede reducir considerablemente los gastos de transferencia de datos copiando datos compartidos en un número menor de nodos y ejecutando tareas en paralelo en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="941a5-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="941a5-109">Esto es válido especialmente si los datos que se copian en cada nodo deben transferirse entre regiones geográficas.</span><span class="sxs-lookup"><span data-stu-id="941a5-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="941a5-110">**Maximizar el uso de memoria** cuando las tareas requieren una gran cantidad de memoria, pero solo durante períodos breves y en momentos variables durante la ejecución.</span><span class="sxs-lookup"><span data-stu-id="941a5-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="941a5-111">Puede emplear menos nodos de ejecución, pero de mayor tamaño y con más memoria, para controlar de forma eficaz dichos aumentos.</span><span class="sxs-lookup"><span data-stu-id="941a5-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span></span> <span data-ttu-id="941a5-112">Estos nodos tendrían varias tareas ejecutándose en paralelo en cada nodo, pero cada tarea aprovecharía la abundante memoria de los nodos en distintos momentos.</span><span class="sxs-lookup"><span data-stu-id="941a5-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="941a5-113">**Mitigar los límites de número de nodos** cuando se requiere la comunicación entre nodos dentro de un grupo.</span><span class="sxs-lookup"><span data-stu-id="941a5-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="941a5-114">Actualmente, los grupos configurados para la comunicación entre nodos están limitados a 50 nodos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="941a5-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span></span> <span data-ttu-id="941a5-115">Si cada uno de los nodos de este tipo de grupo es capaz de ejecutar tareas en paralelo, el número de tareas que se podrán ejecutar simultáneamente será mayor.</span><span class="sxs-lookup"><span data-stu-id="941a5-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="941a5-116">**Replicar en un clúster de proceso local**, como cuando mueve por primera vez un entorno de procesos a Azure.</span><span class="sxs-lookup"><span data-stu-id="941a5-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span></span> <span data-ttu-id="941a5-117">Si la solución local existente ejecuta varias tareas en cada nodo de proceso, puede aumentar el número máximo de tareas de nodo para que refleje con mayor fidelidad esa configuración.</span><span class="sxs-lookup"><span data-stu-id="941a5-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="941a5-118">Escenario de ejemplo</span><span class="sxs-lookup"><span data-stu-id="941a5-118">Example scenario</span></span>
<span data-ttu-id="941a5-119">Para ilustrar las ventajas de la ejecución de tareas en paralelo, imaginemos que la aplicación de la tarea tiene unos requisitos de CPU y memoria que hacen que el tamaño de nodo [Standard\_StandardD1](../cloud-services/cloud-services-sizes-specs.md) sea suficiente.</span><span class="sxs-lookup"><span data-stu-id="941a5-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="941a5-120">Pero, para ejecutar el trabajo en el tiempo requerido, se necesitan 1.000 nodos de ese tipo.</span><span class="sxs-lookup"><span data-stu-id="941a5-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="941a5-121">En lugar de utilizar nodos Standard\_D1 con un núcleo de CPU, podría utilizar nodos [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) con 16 núcleos en cada nodo y habilitar la ejecución de tareas en paralelo.</span><span class="sxs-lookup"><span data-stu-id="941a5-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="941a5-122">En este caso, se podría usar un *número de nodos 16 veces menor* ; es decir, en lugar de 1000 nodos, solo serían necesarios 63.</span><span class="sxs-lookup"><span data-stu-id="941a5-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="941a5-123">Además, si para cada nodo son necesarios datos de referencia o archivos de aplicación de gran tamaño, la eficiencia y la duración del trabajo también se mejoran, ya que los datos se copian en solo 16 nodos.</span><span class="sxs-lookup"><span data-stu-id="941a5-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="941a5-124">Habilitación de la ejecución en paralelo de tareas</span><span class="sxs-lookup"><span data-stu-id="941a5-124">Enable parallel task execution</span></span>
<span data-ttu-id="941a5-125">Los nodos de proceso para la ejecución en paralelo de tareas se configuran a nivel de grupo.</span><span class="sxs-lookup"><span data-stu-id="941a5-125">You configure compute nodes for parallel task execution at the pool level.</span></span> <span data-ttu-id="941a5-126">Con la biblioteca de .NET para Batch, establezca la propiedad [CloudPool.MaxTasksPerComputeNode][maxtasks_net] al crear un grupo.</span><span class="sxs-lookup"><span data-stu-id="941a5-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="941a5-127">Si usa la API de REST de Batch, establezca el elemento [maxTasksPerNode][rest_addpool] en el cuerpo de la solicitud durante la creación del grupo.</span><span class="sxs-lookup"><span data-stu-id="941a5-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span></span>

<span data-ttu-id="941a5-128">Lote de Azure permite una configuración máxima de tareas por nodo que casi cuadriplica el número de núcleos de nodo.</span><span class="sxs-lookup"><span data-stu-id="941a5-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span></span> <span data-ttu-id="941a5-129">Por ejemplo, si el grupo está configurado con nodos de tamaño "Grande" (cuatro núcleos), `maxTasksPerNode` se puede establecer en 16.</span><span class="sxs-lookup"><span data-stu-id="941a5-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span></span> <span data-ttu-id="941a5-130">Para más información sobre el número de núcleos de cada uno de los tamaños de nodo, consulte [Tamaños de los servicios en la nube](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="941a5-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="941a5-131">Para más información sobre los límites del servicio, consulte [Cuotas y límites del servicio de Lote de Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="941a5-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="941a5-132">Asegúrese de tener en cuenta el valor `maxTasksPerNode` al construir una [fórmula de escalado automático][enable_autoscaling] para el grupo.</span><span class="sxs-lookup"><span data-stu-id="941a5-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="941a5-133">Por ejemplo, una fórmula que evalúe `$RunningTasks` podría verse afectada considerablemente por un aumento en las tareas por nodo.</span><span class="sxs-lookup"><span data-stu-id="941a5-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="941a5-134">Consulte [Escalación automática de los nodos de ejecución en un grupo de Lote de Azure](batch-automatic-scaling.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="941a5-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="941a5-135">Distribución de tareas</span><span class="sxs-lookup"><span data-stu-id="941a5-135">Distribution of tasks</span></span>
<span data-ttu-id="941a5-136">Cuando los nodos de proceso dentro de un grupo pueden ejecutar tareas de forma simultánea, es importante especificar cómo desea que se distribuyan las tareas entre los nodos del grupo.</span><span class="sxs-lookup"><span data-stu-id="941a5-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span></span>

<span data-ttu-id="941a5-137">Mediante la propiedad [CloudPool.TaskSchedulingPolicy][task_schedule], puede especificar que las tareas se deberían asignar de manera uniforme entre todos los nodos del grupo ("propagación").</span><span class="sxs-lookup"><span data-stu-id="941a5-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span></span> <span data-ttu-id="941a5-138">O bien, puede especificar que se deberían asignar todas las tareas posibles a cada nodo antes de asignarlas a otro nodo del grupo ("empaquetado").</span><span class="sxs-lookup"><span data-stu-id="941a5-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span></span>

<span data-ttu-id="941a5-139">Como ejemplo de por qué esta característica es importante, considere el grupo de nodos [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) (en el ejemplo anterior) configurado con un valor [CloudPool.MaxTasksPerComputeNode][maxtasks_net] de 16.</span><span class="sxs-lookup"><span data-stu-id="941a5-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="941a5-140">Si [CloudPool.TaskSchedulingPolicy][task_schedule] se configura con un [ComputeNodeFillType][fill_type] de *Pack*, se podría maximizar el uso de los 16 núcleos de cada nodo y permitir que un [grupo con escalado automático](batch-automatic-scaling.md) elimine los nodos sin usar del grupo (nodos sin tareas asignadas).</span><span class="sxs-lookup"><span data-stu-id="941a5-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="941a5-141">Esto minimiza el uso de recursos y permite ahorrar dinero.</span><span class="sxs-lookup"><span data-stu-id="941a5-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="941a5-142">Ejemplo de .NET Lote</span><span class="sxs-lookup"><span data-stu-id="941a5-142">Batch .NET example</span></span>
<span data-ttu-id="941a5-143">En este fragmento código de la API de [.NET para Batch][api_net], se muestra una solicitud para crear un grupo que contiene cuatro nodos de gran tamaño con un máximo de cuatro tareas por nodo.</span><span class="sxs-lookup"><span data-stu-id="941a5-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="941a5-144">Se especifica una directiva de programación de tareas que llenará cada nodo de tareas antes de asignarlas a otro nodo del grupo.</span><span class="sxs-lookup"><span data-stu-id="941a5-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span></span> <span data-ttu-id="941a5-145">Para obtener más información sobre cómo agregar grupos mediante la API de .NET para Batch, consulte [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="941a5-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="941a5-146">Ejemplo de REST Lote</span><span class="sxs-lookup"><span data-stu-id="941a5-146">Batch REST example</span></span>
<span data-ttu-id="941a5-147">En este fragmento de la API de [REST de Batch][api_rest], se muestra una solicitud para crear un grupo que contiene dos nodos de gran tamaño con un máximo de cuatro tareas por nodo.</span><span class="sxs-lookup"><span data-stu-id="941a5-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="941a5-148">Para obtener más información sobre cómo agregar grupos mediante la API de REST, consulte [Agregar un grupo a una cuenta][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="941a5-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span></span>

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
> <span data-ttu-id="941a5-149">Solo puede establecer el elemento `maxTasksPerNode` y la propiedad [MaxTasksPerComputeNode][maxtasks_net] en el momento de crear el grupo.</span><span class="sxs-lookup"><span data-stu-id="941a5-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="941a5-150">No se pueden modificar después de haberlos creado.</span><span class="sxs-lookup"><span data-stu-id="941a5-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="941a5-151">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="941a5-151">Code sample</span></span>
<span data-ttu-id="941a5-152">El proyecto [ParallelNodeTasks][parallel_tasks_sample] en GitHub muestra el uso de la propiedad [CloudPool.MaxTasksPerComputeNode][maxtasks_net].</span><span class="sxs-lookup"><span data-stu-id="941a5-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="941a5-153">Esta aplicación de consola de C# utiliza la biblioteca de [.NET para Batch][api_net] para crear un grupo con uno o más nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="941a5-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span></span> <span data-ttu-id="941a5-154">Ejecuta un número configurable de tareas en esos nodos para simular una carga variable.</span><span class="sxs-lookup"><span data-stu-id="941a5-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span></span> <span data-ttu-id="941a5-155">Los resultados de la aplicación especifican qué nodos han ejecutado cada tarea.</span><span class="sxs-lookup"><span data-stu-id="941a5-155">Output from the application specifies which nodes executed each task.</span></span> <span data-ttu-id="941a5-156">La aplicación también proporciona un resumen de los parámetros de trabajo y la duración.</span><span class="sxs-lookup"><span data-stu-id="941a5-156">The application also provides a summary of the job parameters and duration.</span></span> <span data-ttu-id="941a5-157">Abajo se muestra la parte de resumen de los resultados de dos ejecuciones diferentes de la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="941a5-157">The summary portion of the output from two different runs of the sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="941a5-158">La primera ejecución de la aplicación de ejemplo muestra que, con un solo nodo en el grupo y la configuración predeterminada de una tarea por nodo, la duración del trabajo es superior a 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="941a5-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="941a5-159">La segunda ejecución del ejemplo muestra una disminución notable en la duración del trabajo.</span><span class="sxs-lookup"><span data-stu-id="941a5-159">The second run of the sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="941a5-160">Esto se debe a que el grupo se configuró con cuatro tareas por nodo, lo que permite la ejecución en paralelo de tareas de forma que el trabajo se completa en casi una cuarta parte del tiempo.</span><span class="sxs-lookup"><span data-stu-id="941a5-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span></span>

> [!NOTE]
> <span data-ttu-id="941a5-161">La duración del trabajo en los resúmenes anteriores no incluye el tiempo de creación del grupo.</span><span class="sxs-lookup"><span data-stu-id="941a5-161">The job durations in the summaries above do not include pool creation time.</span></span> <span data-ttu-id="941a5-162">Cada uno de los trabajos anteriores se envió a grupos ya creados cuyos nodos de proceso se encontraban en el estado *inactivo* en el momento del envío.</span><span class="sxs-lookup"><span data-stu-id="941a5-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="941a5-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="941a5-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="941a5-164">Mapa térmico de Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="941a5-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="941a5-165">El [Azure Batch Explorer][batch_explorer], una de las aplicaciones de ejemplo de [Azure Batch][github_samples], contiene una característica denominada *Mapa térmico* que proporciona una vista de la ejecución de tareas.</span><span class="sxs-lookup"><span data-stu-id="941a5-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="941a5-166">Cuando ejecuta la aplicación de ejemplo [ParallelTasks][parallel_tasks_sample], puede usar la característica Mapa térmico para ver fácilmente la ejecución de tareas paralelas en cada nodo.</span><span class="sxs-lookup"><span data-stu-id="941a5-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span></span>

![Mapa térmico de Batch Explorer][1]

<span data-ttu-id="941a5-168">*Mapa térmico de Batch Explorer que muestra un grupo de cuatro nodos, donde cada nodo ejecuta actualmente cuatro tareas*</span><span class="sxs-lookup"><span data-stu-id="941a5-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
