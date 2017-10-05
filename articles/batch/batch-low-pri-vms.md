---
title: "Ejecución de cargas de trabajo de Azure Batch en máquinas virtuales de prioridad baja rentables (versión preliminar) | Microsoft Docs"
description: "Aprenda a aprovisionar máquinas virtuales de prioridad baja para reducir el costo de las cargas de trabajo de Azure Batch."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 9bf0ac322020d8a8453011c3207c1930175db6d3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="a5af1-103">Uso de máquinas virtuales de prioridad baja con Batch (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="a5af1-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="a5af1-104">Azure Batch ofrece máquinas virtuales (VM) de prioridad baja para reducir el costo de las cargas de trabajo de Batch.</span><span class="sxs-lookup"><span data-stu-id="a5af1-104">Azure Batch offers low-priorty virtual machines (VMs) to reduce the cost of Batch workloads.</span></span> <span data-ttu-id="a5af1-105">Las máquinas virtuales de prioridad baja posibilitan nuevos tipos de cargas de trabajo de Batch al proporcionar elevada capacidad de proceso que también resulta económica.</span><span class="sxs-lookup"><span data-stu-id="a5af1-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="a5af1-106">Las máquinas virtuales de prioridad baja aprovechan la capacidad sobrante en Azure.</span><span class="sxs-lookup"><span data-stu-id="a5af1-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="a5af1-107">Al especificar máquinas virtuales de prioridad baja en sus grupos, Azure Batch puede usar automáticamente este excedente cuando esté disponible.</span><span class="sxs-lookup"><span data-stu-id="a5af1-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="a5af1-108">La ventaja en el uso de máquinas virtuales de prioridad baja es que esas máquinas virtuales se pueden reemplazar cuando no se encuentre disponible ninguna capacidad sobrante en Azure.</span><span class="sxs-lookup"><span data-stu-id="a5af1-108">The tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="a5af1-109">Por este motivo, estas máquinas son las más adecuadas para determinados tipos de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a5af1-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="a5af1-110">Use máquinas virtuales de prioridad baja para cargas de trabajo de procesamiento por lotes y asincrónicas en las que el tiempo de finalización del trabajo sea flexible y el trabajo se distribuya entre muchas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a5af1-110">Use low-priority VMs for batch and asynchronous processing workloads where the job completion time is flexible and the work is distributed across many VMs.</span></span>

<span data-ttu-id="a5af1-111">Las máquinas virtuales de prioridad baja son significativamente menos caras que las máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="a5af1-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="a5af1-112">Para más información sobre precios, consulte [Precios de Batch](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="a5af1-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="a5af1-113">Para obtener una explicación adicional sobre máquinas virtuales de prioridad baja, consulte el anuncio de entrada de blog: [Batch computing at a fraction of the price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/) (Computación por lotes a un precio reducido).</span><span class="sxs-lookup"><span data-stu-id="a5af1-113">For an additional discussion of low-priority VMs, see the blog post announcement: [Batch computing at a fraction of the price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5af1-114">Las máquinas virtuales de prioridad baja se encuentran actualmente en versión preliminar y solo están disponibles para cargas de trabajo que se ejecutan en Batch.</span><span class="sxs-lookup"><span data-stu-id="a5af1-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="a5af1-115">Casos de uso de máquinas virtuales de prioridad baja</span><span class="sxs-lookup"><span data-stu-id="a5af1-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="a5af1-116">Teniendo en cuenta las características de las máquinas virtuales de prioridad baja, ¿con qué cargas de trabajo se pueden y no pueden usar?</span><span class="sxs-lookup"><span data-stu-id="a5af1-116">Given the characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="a5af1-117">En general, las cargas de trabajo de procesamiento por lotes son una buena opción, ya que los trabajos se dividen en muchas tareas paralelas o hay muchos trabajos que se escalan horizontalmente y que se distribuyen en muchas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a5af1-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="a5af1-118">Para maximizar el uso de la capacidad sobrante en Azure, los trabajos adecuados se pueden escalar horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="a5af1-118">To maximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="a5af1-119">Puede que, en ocasiones, las máquinas virtuales no estén disponibles o se reemplacen; como resultado, la capacidad para los trabajos puede verse mermada y conducir a interrupciones de las tareas o la necesidad de ejecutarlas una y otra vez.</span><span class="sxs-lookup"><span data-stu-id="a5af1-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead to task interruption and reruns.</span></span> <span data-ttu-id="a5af1-120">Por tanto, los trabajos deben ser flexibles en el tiempo que pueden tardar en ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="a5af1-120">Jobs must therefore be flexible in the time they can take to run.</span></span>

-   <span data-ttu-id="a5af1-121">Los trabajos con tareas más largas pueden resultar más afectados si se interrumpen.</span><span class="sxs-lookup"><span data-stu-id="a5af1-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="a5af1-122">Si las tareas de larga ejecución implementan puntos de comprobación para guardar el progreso mientras se ejecutan, entonces el impacto de la interrupción será bastante menor.</span><span class="sxs-lookup"><span data-stu-id="a5af1-122">If long-running tasks implement checkpointing to save progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="a5af1-123">Las tareas con tiempos de ejecución más cortos tienden a funcionar mejor con máquinas virtuales de prioridad baja, ya que el impacto de la interrupción es mucho menor.</span><span class="sxs-lookup"><span data-stu-id="a5af1-123">Tasks with shorter execution times tend to work best with low-priority VMs as the impact of interruption is far less.</span></span>

-   <span data-ttu-id="a5af1-124">Los trabajos de MPI de larga ejecución que usan varias máquinas virtuales no son adecuados para usar máquinas virtuales de prioridad baja, ya que una máquina virtual reemplazada probablemente ocasionará que todo el trabajo tenga que ejecutarse de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a5af1-124">Long-running MPI jobs that utilize multiple VMs are not well suited to use low-priority VMs as one preempted VM will likely lead to the whole job having to be run again.</span></span>

<span data-ttu-id="a5af1-125">Algunos ejemplos de casos de uso de procesamiento por lotes adecuados para usar máquinas virtuales de prioridad baja son:</span><span class="sxs-lookup"><span data-stu-id="a5af1-125">Some examples of batch processing use cases well suited to use low-priority VMs are:</span></span>

-   <span data-ttu-id="a5af1-126">**Desarrollo y pruebas**: en concreto, si se están desarrollando soluciones a gran escala se pueden obtener ahorros significativos.</span><span class="sxs-lookup"><span data-stu-id="a5af1-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="a5af1-127">Aunque todos los tipos de pruebas pueden beneficiarse, será especialmente ventajoso para pruebas de carga y regresión a gran escala.</span><span class="sxs-lookup"><span data-stu-id="a5af1-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="a5af1-128">**Capacidad a petición complementaria** : las máquinas virtuales de prioridad baja pueden usarse para complementar las máquinas virtuales dedicadas normales; cuando están disponibles, los trabajos pueden escalarse y, por lo tanto, completarse más rápido con un costo menor; cuando no están disponibles, se puede contar con la línea base de máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="a5af1-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, the baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="a5af1-129">**Tiempo de ejecución flexible de los trabajos**: si hay flexibilidad en el tiempo en que tienen que completarse los trabajos, entonces se pueden tolerar posibles bajadas en la capacidad; sin embargo, con la adición de máquinas virtuales de prioridad baja, los trabajos se ejecutarán con frecuencia más rápido y con un costo menor.</span><span class="sxs-lookup"><span data-stu-id="a5af1-129">**Flexible job execution time**: If there is flexibility in the time jobs have to complete, then potential drops in capacity can be tolerated; however, with the addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="a5af1-130">Los grupos de Batch se pueden configurar para usar máquinas virtuales de prioridad baja de varias maneras, dependiendo de la flexibilidad en el tiempo de ejecución de los trabajos:</span><span class="sxs-lookup"><span data-stu-id="a5af1-130">Batch pools can be configured to use low-priority VMs in a few ways, depending on the flexibility in job execution time:</span></span>

-   <span data-ttu-id="a5af1-131">Las máquinas virtuales de prioridad baja solo se pueden usar en un grupo; Batch simplemente recuperará cualquier capacidad reemplazada cuando esté disponible.</span><span class="sxs-lookup"><span data-stu-id="a5af1-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="a5af1-132">Esta es la manera más barata de ejecutar trabajos, ya que solo se usan máquinas virtuales de prioridad baja.</span><span class="sxs-lookup"><span data-stu-id="a5af1-132">This is the cheapest way to execute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="a5af1-133">Las máquinas virtuales de prioridad baja se pueden usar conjuntamente con una línea de base fija de máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="a5af1-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="a5af1-134">El número fijo de máquinas virtuales dedicadas garantiza que siempre haya algo de capacidad para mantener el progreso de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="a5af1-134">The fixed number of dedicated VMs ensures there is always some capacity to keep a job progressing.</span></span>

-   <span data-ttu-id="a5af1-135">Puede haber una combinación dinámica de máquinas virtuales dedicadas y de prioridad baja, de modo que las máquinas virtuales de prioridad baja más baratas se usen únicamente cuando estén disponibles, pero las máquinas virtuales dedicadas de precio completo se escalen verticalmente cuando sea necesario, a fin de mantener una cantidad mínima de capacidad disponible para mantener el progreso de los trabajos.</span><span class="sxs-lookup"><span data-stu-id="a5af1-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but the full-priced dedicated VMs are scaled up when required, to keep a minimum amount of capacity available to keep the jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="a5af1-136">Compatibilidad de Batch con máquinas virtuales de prioridad baja</span><span class="sxs-lookup"><span data-stu-id="a5af1-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="a5af1-137">Azure Batch ofrece varias funcionalidades que facilitan el consumo y que se benefician de las máquinas virtuales de prioridad baja:</span><span class="sxs-lookup"><span data-stu-id="a5af1-137">Azure Batch provides several capabilities that make it easy to consume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="a5af1-138">Los grupos de Batch pueden contener tanto máquinas virtuales dedicadas como máquinas virtuales de prioridad baja.</span><span class="sxs-lookup"><span data-stu-id="a5af1-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="a5af1-139">El número de cada tipo de máquina virtual se puede especificar cuando se crea un grupo, o puede cambiarse en cualquier momento para un grupo ya existente, mediante la operación explícita de cambio de tamaño o el escalado automático.</span><span class="sxs-lookup"><span data-stu-id="a5af1-139">The number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using the explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="a5af1-140">El envío de trabajos y tareas puede permanecer sin cambios y no necesita preocuparse por los tipos de máquina virtual en el grupo.</span><span class="sxs-lookup"><span data-stu-id="a5af1-140">Job and task submission can remain unchanged and do not need to be concerned with the VM types in the pool.</span></span> <span data-ttu-id="a5af1-141">También se puede tener un grupo donde se usen completamente máquinas virtuales de prioridad baja para ejecutar trabajos lo más barato posible, pero volver a máquinas virtuales dedicadas si la capacidad desciende por debajo de un umbral mínimo, a fin de mantener los trabajos en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="a5af1-141">It is also possible to have a pool completely use low-priority VMs to run jobs as cheaply as possible, but spin up dedicated VMs if the capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="a5af1-142">Los grupos de Batch buscan automáticamente el número objetivo de máquinas virtuales de prioridad baja.</span><span class="sxs-lookup"><span data-stu-id="a5af1-142">Batch pools automatically seek to the target number of low-priority VMs.</span></span> <span data-ttu-id="a5af1-143">Si las máquinas virtuales se reemplazan, entonces Batch intenta reemplazar la capacidad perdida y volver al objetivo.</span><span class="sxs-lookup"><span data-stu-id="a5af1-143">If VMs are preempted, then Batch will attempt to replace the lost capacity and return to the target.</span></span>

-   <span data-ttu-id="a5af1-144">En el caso de que se interrumpan las tareas, Batch lo detectará y las pondrá automáticamente en cola para que se ejecuten de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a5af1-144">In the case of tasks being interrupted, Batch will detect and automatically requeue tasks to be run again.</span></span>

-   <span data-ttu-id="a5af1-145">Las máquinas virtuales de prioridad baja tienen una cuota de núcleos que difiere de la de las máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="a5af1-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="a5af1-146">La cuota para las máquinas virtuales de prioridad baja es mayor que la de las máquinas virtuales dedicadas, ya que las primeras tienen un precio inferior.</span><span class="sxs-lookup"><span data-stu-id="a5af1-146">The quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="a5af1-147">Consulte [Límites y cuotas del servicio Batch](batch-quota-limit.md#resource-quotas) para más información.</span><span class="sxs-lookup"><span data-stu-id="a5af1-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="a5af1-148">Las máquinas virtuales de prioridad baja no se admiten actualmente para cuentas de Batch donde se establece el modo de asignación de grupo en [Suscripción del usuario](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="a5af1-148">Low-priority VMs are not currently supported for Batch accounts where the pool allocation mode is set to [User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="a5af1-149">Creación y actualización de grupos</span><span class="sxs-lookup"><span data-stu-id="a5af1-149">Create and update pools</span></span>

<span data-ttu-id="a5af1-150">Un grupo de Batch puede contener tanto máquinas virtuales dedicadas como de prioridad baja (también conocidas como nodos de proceso).</span><span class="sxs-lookup"><span data-stu-id="a5af1-150">A Batch pool can contain both dedicated and low-priority VMs (also referred to as compute nodes).</span></span> <span data-ttu-id="a5af1-151">Puede establecer el número objetivo de nodos de proceso tanto para las máquinas virtuales dedicadas como para las de prioridad baja.</span><span class="sxs-lookup"><span data-stu-id="a5af1-151">You can set the target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="a5af1-152">El número de nodos objetivo especifica el número de máquinas virtuales que quiere tener en el grupo.</span><span class="sxs-lookup"><span data-stu-id="a5af1-152">The target number of nodes specifies the number of VMs you want to have in the pool.</span></span>

<span data-ttu-id="a5af1-153">Por ejemplo, para crear un grupo mediante máquinas virtuales de servicio en la nube de Azure con un objetivo de 5 máquinas virtuales dedicadas y 20 máquinas virtuales de prioridad baja:</span><span class="sxs-lookup"><span data-stu-id="a5af1-153">For example, to create a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="a5af1-154">Para crear un grupo mediante máquinas virtuales de Azure (en este caso, máquinas virtuales Linux) con un objetivo de 5 máquinas virtuales dedicadas y 20 máquinas virtuales de prioridad baja:</span><span class="sxs-lookup"><span data-stu-id="a5af1-154">To create a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="a5af1-155">Puede obtener el número actual de nodos tanto para las máquinas virtuales dedicadas como para las de prioridad baja:</span><span class="sxs-lookup"><span data-stu-id="a5af1-155">You can get the current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="a5af1-156">Los nodos de grupo tienen una propiedad que indica si el nodo es una máquina virtual dedicada o de prioridad baja:</span><span class="sxs-lookup"><span data-stu-id="a5af1-156">Pool nodes have a property to indicate if the node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="a5af1-157">Cuando se reemplazan uno o varios nodos de un grupo, la operación de enumeración de nodos seguirá devolviendo esos nodos, el número actual de nodos de prioridad baja permanecerá sin cambios, pero esos nodos tendrán su estado establecido como **reemplazado**.</span><span class="sxs-lookup"><span data-stu-id="a5af1-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, the current number of low-priority nodes will remain unchanged, but those nodes will have their state set to the **Preempted** state.</span></span> <span data-ttu-id="a5af1-158">Batch intentará encontrar máquinas virtuales de reemplazo y, si tiene éxito, los nodos pasarán a los estados **Creando** y luego **Iniciando** antes de estar disponibles para la ejecución de tareas, igual que los nuevos nodos.</span><span class="sxs-lookup"><span data-stu-id="a5af1-158">Batch will attempt to find replacement VMs and, if successful, the nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="a5af1-159">Escalado de un grupo que contiene máquinas virtuales de prioridad baja</span><span class="sxs-lookup"><span data-stu-id="a5af1-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="a5af1-160">Al igual que sucede con grupos que se componen únicamente de máquinas virtuales dedicadas, es posible escalar un grupo que contenga máquinas virtuales de prioridad baja mediante la llamada al método Resize o por medio de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="a5af1-160">As with pools solely consisting of dedicated VMs, it is possible to scale a pool containing low-priority VMs by calling the Resize method or by using auto-scale.</span></span>

<span data-ttu-id="a5af1-161">La operación de cambio de tamaño de grupo tiene un segundo parámetro opcional que actualiza el valor de **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="a5af1-161">The pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="a5af1-162">La fórmula de escalado automático de grupo admite máquinas virtuales de prioridad baja del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="a5af1-162">The pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="a5af1-163">Puede obtener o establecer el valor de la variable definida por el servicio **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="a5af1-163">You can get or set the value of the service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="a5af1-164">Puede obtener el valor de la variable definida por el servicio **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="a5af1-164">You can get the value of the service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="a5af1-165">Puede obtener el valor de la variable definida por el servicio **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="a5af1-165">You can get the value of the service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="a5af1-166">Esta variable devuelve el número de nodos en estado reemplazado y le permite escalar o reducir verticalmente el número de nodos dedicados, en función del número de nodos reemplazados que no estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="a5af1-166">This variable returns the number of nodes in the preempted state and allows you to scale up or down the number of dedicated nodes, depending on the number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="a5af1-167">Trabajos y tareas</span><span class="sxs-lookup"><span data-stu-id="a5af1-167">Jobs and tasks</span></span>

<span data-ttu-id="a5af1-168">Los trabajos y las tareas requieren muy poca compatibilidad con los nodos de prioridad baja; la única compatibilidad es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="a5af1-168">Jobs and tasks require very little support for low-priority nodes; the only support is as follows:</span></span>

-   <span data-ttu-id="a5af1-169">La propiedad JobManagerTask de un trabajo tiene una propiedad nueva, **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="a5af1-169">The JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="a5af1-170">Cuando esta propiedad es true, la tarea del administrador de trabajos se puede programar tanto en un nodo dedicado como de prioridad baja.</span><span class="sxs-lookup"><span data-stu-id="a5af1-170">When this property is true, the job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="a5af1-171">Si esta propiedad es false, la tarea del administrador de trabajos se programará solo para un nodo dedicado.</span><span class="sxs-lookup"><span data-stu-id="a5af1-171">If this property is false, the job manager task will be scheduled to a dedicated node only.</span></span>

-   <span data-ttu-id="a5af1-172">Una [variable de entorno](batch-compute-node-environment-variables.md) está disponible para una aplicación de tareas de modo que sea posible determinar si se ejecuta en un nodo de prioridad baja o dedicado.</span><span class="sxs-lookup"><span data-stu-id="a5af1-172">An [environment variable](batch-compute-node-environment-variables.md) is available to a task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="a5af1-173">La variable de entorno es AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="a5af1-173">The environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="a5af1-174">Control de reemplazos</span><span class="sxs-lookup"><span data-stu-id="a5af1-174">Handling preemption</span></span>

<span data-ttu-id="a5af1-175">En ocasiones las máquinas virtuales se pueden reemplazar; cuando esto sucede, Batch hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a5af1-175">VMs may occasionally be preempted; when this happens, Batch does the following:</span></span>

-   <span data-ttu-id="a5af1-176">Las máquinas virtuales reemplazadas tienen su estado actualizado a **Reemplazada**.</span><span class="sxs-lookup"><span data-stu-id="a5af1-176">The preempted VMs have their state updated to **Preempted**.</span></span>
-   <span data-ttu-id="a5af1-177">Si las tareas se estuvieran ejecutando en las máquinas virtuales del nodo reemplazado, esas tareas se pondrían de nuevo en cola y se volverían a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="a5af1-177">If tasks were running on the preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="a5af1-178">La máquina virtual se elimina en la práctica, lo que hace que se pierdan los datos almacenados localmente en ella.</span><span class="sxs-lookup"><span data-stu-id="a5af1-178">The VM is effectively deleted, leading to any data stored locally on the VM being lost.</span></span>
-   <span data-ttu-id="a5af1-179">El grupo intenta continuamente alcanzar el número objetivo de nodos de prioridad baja disponibles.</span><span class="sxs-lookup"><span data-stu-id="a5af1-179">The pool continually attempts to reach the target number of low-priority nodes available.</span></span> <span data-ttu-id="a5af1-180">Cuando se encuentra la capacidad de reemplazo, los nodos mantienen sus identificaciones, pero se reinicializan, pasando por los estados**Creando** e **Iniciando** antes de que estén disponibles para la programación de tareas.</span><span class="sxs-lookup"><span data-stu-id="a5af1-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="a5af1-181">Los recuentos de reemplazos están disponibles como una métrica en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a5af1-181">Preemption counts are available as a metric in the Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="a5af1-182">Métricas</span><span class="sxs-lookup"><span data-stu-id="a5af1-182">Metrics</span></span>

<span data-ttu-id="a5af1-183">Hay nuevas métricas disponibles en [Azure Portal ](https://portal.azure.com) para los nodos de baja prioridad.</span><span class="sxs-lookup"><span data-stu-id="a5af1-183">New metrics are available in the [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="a5af1-184">Estas son las métricas:</span><span class="sxs-lookup"><span data-stu-id="a5af1-184">These metrics are:</span></span>

- <span data-ttu-id="a5af1-185">Recuento de nodos de baja prioridad</span><span class="sxs-lookup"><span data-stu-id="a5af1-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="a5af1-186">Recuento de núcleos de baja prioridad</span><span class="sxs-lookup"><span data-stu-id="a5af1-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="a5af1-187">Recuento de nodos con prioridad</span><span class="sxs-lookup"><span data-stu-id="a5af1-187">Preempted Node Count</span></span>

<span data-ttu-id="a5af1-188">Para ver métricas en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="a5af1-188">To view metrics in the Azure portal:</span></span>

1. <span data-ttu-id="a5af1-189">Navegue a su cuenta de Batch en el portal y vea la configuración de dicha cuenta.</span><span class="sxs-lookup"><span data-stu-id="a5af1-189">Navigate to your Batch account in the portal, and view the settings for your Batch account.</span></span>
2. <span data-ttu-id="a5af1-190">Seleccione **Métricas** en la sección **Supervisión**.</span><span class="sxs-lookup"><span data-stu-id="a5af1-190">Select **Metrics** from the **Monitoring** section.</span></span>
3. <span data-ttu-id="a5af1-191">Seleccione las métricas que desea en la lista **Métricas disponibles**.</span><span class="sxs-lookup"><span data-stu-id="a5af1-191">Select the metrics you desire from the **Available Metrics** list.</span></span>

![Métricas para nodos de baja prioridad](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="a5af1-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a5af1-193">Next steps</span></span>

* <span data-ttu-id="a5af1-194">Consulte [Información general de las características de Lote para desarrolladores](batch-api-basics.md), donde encontrará información esencial para cualquier persona que vaya a utilizar Lote.</span><span class="sxs-lookup"><span data-stu-id="a5af1-194">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="a5af1-195">El artículo contiene información más detallada acerca de los recursos del servicio de Lote, como grupos, nodos, trabajos y tareas, así como las numerosas características de API que se pueden usar al compilar cualquier aplicación de Lote.</span><span class="sxs-lookup"><span data-stu-id="a5af1-195">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="a5af1-196">Obtenga información acerca de las [API y herramientas de Batch](batch-apis-tools.md) disponibles para la creación de soluciones de Batch.</span><span class="sxs-lookup"><span data-stu-id="a5af1-196">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
