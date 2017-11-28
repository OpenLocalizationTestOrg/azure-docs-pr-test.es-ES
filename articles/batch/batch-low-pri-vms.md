---
title: "las cargas de trabajo por lotes de Azure aaaRun en máquinas virtuales de prioridad baja rentables (versión preliminar) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo Hola de tooreduce de las máquinas virtuales de prioridad baja tooprovision de costo de las cargas de trabajo de lote de Azure."
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
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="97766-103">Uso de máquinas virtuales de prioridad baja con Batch (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="97766-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="97766-104">Lote de Azure ofrece costo de hello tooreduce de baja prioridad las máquinas virtuales (VM) de las cargas de trabajo por lotes.</span><span class="sxs-lookup"><span data-stu-id="97766-104">Azure Batch offers low-priorty virtual machines (VMs) tooreduce hello cost of Batch workloads.</span></span> <span data-ttu-id="97766-105">Las máquinas virtuales de prioridad baja posibilitan nuevos tipos de cargas de trabajo de Batch al proporcionar elevada capacidad de proceso que también resulta económica.</span><span class="sxs-lookup"><span data-stu-id="97766-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="97766-106">Las máquinas virtuales de prioridad baja aprovechan la capacidad sobrante en Azure.</span><span class="sxs-lookup"><span data-stu-id="97766-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="97766-107">Al especificar máquinas virtuales de prioridad baja en sus grupos, Azure Batch puede usar automáticamente este excedente cuando esté disponible.</span><span class="sxs-lookup"><span data-stu-id="97766-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="97766-108">contrapartida de Hello para el uso de máquinas virtuales de prioridad baja es que pueden ser adelantadas esas máquinas virtuales cuando no hay exceso de capacidad está disponible en Azure.</span><span class="sxs-lookup"><span data-stu-id="97766-108">hello tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="97766-109">Por este motivo, estas máquinas son las más adecuadas para determinados tipos de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="97766-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="97766-110">Use máquinas virtuales de prioridad baja para cargas de trabajo de procesamiento asincrónico en tiempo de finalización del trabajo de hello es flexible y trabajo Hola se distribuye entre muchas máquinas virtuales y lote.</span><span class="sxs-lookup"><span data-stu-id="97766-110">Use low-priority VMs for batch and asynchronous processing workloads where hello job completion time is flexible and hello work is distributed across many VMs.</span></span>

<span data-ttu-id="97766-111">Las máquinas virtuales de prioridad baja son significativamente menos caras que las máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="97766-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="97766-112">Para más información sobre precios, consulte [Precios de Batch](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="97766-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="97766-113">Para obtener una explicación adicional de máquinas virtuales de prioridad baja, consulte el anuncio de entrada de blog de hello: [por lotes informática en una fracción del precio de hello](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="97766-113">For an additional discussion of low-priority VMs, see hello blog post announcement: [Batch computing at a fraction of hello price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97766-114">Las máquinas virtuales de prioridad baja se encuentran actualmente en versión preliminar y solo están disponibles para cargas de trabajo que se ejecutan en Batch.</span><span class="sxs-lookup"><span data-stu-id="97766-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="97766-115">Casos de uso de máquinas virtuales de prioridad baja</span><span class="sxs-lookup"><span data-stu-id="97766-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="97766-116">Proporciona características de Hola de máquinas virtuales de prioridad baja, qué cargas de trabajo pueden y no pueden usarlos?</span><span class="sxs-lookup"><span data-stu-id="97766-116">Given hello characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="97766-117">En general, las cargas de trabajo de procesamiento por lotes son una buena opción, ya que los trabajos se dividen en muchas tareas paralelas o hay muchos trabajos que se escalan horizontalmente y que se distribuyen en muchas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="97766-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="97766-118">uso de toomaximize de exceso de capacidad en los trabajos de Azure, que se puede puede escalar horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="97766-118">toomaximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="97766-119">En ocasiones, las máquinas virtuales no estén disponibles o se adelantará, lo que dará como resultado de capacidad reducida para trabajos y puede provocar la vuelve a ejecutar y la interrupción de tootask.</span><span class="sxs-lookup"><span data-stu-id="97766-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead tootask interruption and reruns.</span></span> <span data-ttu-id="97766-120">Trabajos, por tanto, deben ser flexibles en el tiempo de Hola que pueden tomar toorun.</span><span class="sxs-lookup"><span data-stu-id="97766-120">Jobs must therefore be flexible in hello time they can take toorun.</span></span>

-   <span data-ttu-id="97766-121">Los trabajos con tareas más largas pueden resultar más afectados si se interrumpen.</span><span class="sxs-lookup"><span data-stu-id="97766-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="97766-122">Si de larga ejecución tareas implementan progreso toosave de puntos de comprobación que se ejecutan, a continuación, el impacto de interrupción sería mucho menor.</span><span class="sxs-lookup"><span data-stu-id="97766-122">If long-running tasks implement checkpointing toosave progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="97766-123">Tareas con tiempos de ejecución suelen mejor toowork con máquinas virtuales de prioridad baja como impacto Hola de interrupción es mucho menor.</span><span class="sxs-lookup"><span data-stu-id="97766-123">Tasks with shorter execution times tend toowork best with low-priority VMs as hello impact of interruption is far less.</span></span>

-   <span data-ttu-id="97766-124">Trabajos MPI que usan varias máquinas virtuales no están toouse idóneo de larga ejecución máquinas virtuales de prioridad baja como una máquina virtual adelantamiento van a tener toobe, vuelva a ejecutar el trabajo de cliente potencial es probable que toohello entero.</span><span class="sxs-lookup"><span data-stu-id="97766-124">Long-running MPI jobs that utilize multiple VMs are not well suited toouse low-priority VMs as one preempted VM will likely lead toohello whole job having toobe run again.</span></span>

<span data-ttu-id="97766-125">Algunos ejemplos de procesamiento por lotes usan casos toouse adapta perfectamente las máquinas virtuales de prioridad baja son:</span><span class="sxs-lookup"><span data-stu-id="97766-125">Some examples of batch processing use cases well suited toouse low-priority VMs are:</span></span>

-   <span data-ttu-id="97766-126">**Desarrollo y pruebas**: en concreto, si se están desarrollando soluciones a gran escala se pueden obtener ahorros significativos.</span><span class="sxs-lookup"><span data-stu-id="97766-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="97766-127">Aunque todos los tipos de pruebas pueden beneficiarse, será especialmente ventajoso para pruebas de carga y regresión a gran escala.</span><span class="sxs-lookup"><span data-stu-id="97766-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="97766-128">**Complementar capacidad a petición**: máquinas virtuales de prioridad baja se pueden utilizar para complementar la VM regular dedicadas - si está disponible, trabajos pueden escalar y, por lo tanto, para reducir el costo, realizar más rápidas; cuando no esté disponible, línea de base de Hola de dedicado máquinas virtuales están disponibles.</span><span class="sxs-lookup"><span data-stu-id="97766-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, hello baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="97766-129">**Tiempo de ejecución de trabajo flexible**: si hay flexibilidad en los trabajos del temporizador hello tiene toocomplete, a continuación, pueden tolerar caídas potencials de capacidad; sin embargo, con hello suma de los trabajos de las máquinas virtuales de prioridad baja se ejecutará con frecuencia más rápido y para un menor costo.</span><span class="sxs-lookup"><span data-stu-id="97766-129">**Flexible job execution time**: If there is flexibility in hello time jobs have toocomplete, then potential drops in capacity can be tolerated; however, with hello addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="97766-130">Grupos de proceso por lotes pueden ser configurado toouse máquinas virtuales de prioridad baja de varias maneras, dependiendo de la flexibilidad de hello en tiempo de ejecución del trabajo:</span><span class="sxs-lookup"><span data-stu-id="97766-130">Batch pools can be configured toouse low-priority VMs in a few ways, depending on hello flexibility in job execution time:</span></span>

-   <span data-ttu-id="97766-131">Las máquinas virtuales de prioridad baja solo se pueden usar en un grupo; Batch simplemente recuperará cualquier capacidad reemplazada cuando esté disponible.</span><span class="sxs-lookup"><span data-stu-id="97766-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="97766-132">Se trata de los trabajos de tooexecute de manera más baratos hello como máquinas virtuales de prioridad baja sólo se utilizan.</span><span class="sxs-lookup"><span data-stu-id="97766-132">This is hello cheapest way tooexecute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="97766-133">Las máquinas virtuales de prioridad baja se pueden usar conjuntamente con una línea de base fija de máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="97766-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="97766-134">Hello número fijo de máquinas virtuales dedicadas garantiza que es siempre algunos tookeep capacidad un progreso del trabajo.</span><span class="sxs-lookup"><span data-stu-id="97766-134">hello fixed number of dedicated VMs ensures there is always some capacity tookeep a job progressing.</span></span>

-   <span data-ttu-id="97766-135">Puede haber dinámica combinación de máquinas virtuales de prioridad baja y dedicadas, para que las máquinas virtuales de prioridad baja baratas se usan únicamente cuando esté disponible, pero Hola precio completo dedicado las máquinas virtuales se escalan cuando sea necesario, tookeep una cantidad mínima de trabajos de capacidad disponible tookeep Hola progreso.</span><span class="sxs-lookup"><span data-stu-id="97766-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but hello full-priced dedicated VMs are scaled up when required, tookeep a minimum amount of capacity available tookeep hello jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="97766-136">Compatibilidad de Batch con máquinas virtuales de prioridad baja</span><span class="sxs-lookup"><span data-stu-id="97766-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="97766-137">Lote de Azure proporciona varias funciones que hace más fácil tooconsume y beneficiarán de las máquinas virtuales de prioridad baja:</span><span class="sxs-lookup"><span data-stu-id="97766-137">Azure Batch provides several capabilities that make it easy tooconsume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="97766-138">Los grupos de Batch pueden contener tanto máquinas virtuales dedicadas como máquinas virtuales de prioridad baja.</span><span class="sxs-lookup"><span data-stu-id="97766-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="97766-139">número de Hola de cada tipo de máquina virtual puede especificarse cuando se crea un grupo, o cambiar en cualquier momento para un grupo existente, mediante la operación de cambio de tamaño explícito de Hola o con escala automática.</span><span class="sxs-lookup"><span data-stu-id="97766-139">hello number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using hello explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="97766-140">Envío de trabajos y tareas puede permanecer sin cambios y no es necesario tener en cuenta los tipos de VM de hello en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="97766-140">Job and task submission can remain unchanged and do not need to be concerned with hello VM types in hello pool.</span></span> <span data-ttu-id="97766-141">También es posible toohave un grupo completamente utilice prioridad baja máquinas virtuales toorun trabajos de manera más asequible como sea posible, pero de spin up dedicadas máquinas virtuales si la capacidad de hello cae por debajo de un umbral mínimo, para mantener los trabajos que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="97766-141">It is also possible toohave a pool completely use low-priority VMs toorun jobs as cheaply as possible, but spin up dedicated VMs if hello capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="97766-142">Grupos de lote automáticamente búsqueda toohello número de destino de máquinas virtuales de prioridad baja.</span><span class="sxs-lookup"><span data-stu-id="97766-142">Batch pools automatically seek toohello target number of low-priority VMs.</span></span> <span data-ttu-id="97766-143">Si las máquinas virtuales son adelantadas, lote intentará hello tooreplace pierde la capacidad y el destino de toohello devuelto.</span><span class="sxs-lookup"><span data-stu-id="97766-143">If VMs are preempted, then Batch will attempt tooreplace hello lost capacity and return toohello target.</span></span>

-   <span data-ttu-id="97766-144">En caso de hello de tareas que se interrumpa, lote detectará y poner automáticamente toobe de tareas, vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="97766-144">In hello case of tasks being interrupted, Batch will detect and automatically requeue tasks toobe run again.</span></span>

-   <span data-ttu-id="97766-145">Las máquinas virtuales de prioridad baja tienen una cuota de núcleos que difiere de la de las máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="97766-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="97766-146">Hola comillas de cierre para máquinas virtuales de prioridad baja es mayor que el de las máquinas virtuales dedicadas, porque las máquinas virtuales de prioridad baja costo es menor.</span><span class="sxs-lookup"><span data-stu-id="97766-146">hello quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="97766-147">Consulte [Límites y cuotas del servicio Batch](batch-quota-limit.md#resource-quotas) para más información.</span><span class="sxs-lookup"><span data-stu-id="97766-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="97766-148">Máquinas virtuales de prioridad baja no se admiten actualmente para las cuentas de lote donde se establece el modo de asignación de grupo de hello demasiado[suscripción usuario](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="97766-148">Low-priority VMs are not currently supported for Batch accounts where hello pool allocation mode is set too[User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="97766-149">Creación y actualización de grupos</span><span class="sxs-lookup"><span data-stu-id="97766-149">Create and update pools</span></span>

<span data-ttu-id="97766-150">Un grupo de lote puede contener dedicadas y prioridad baja de máquinas virtuales (también denominados tooas calcular nodos).</span><span class="sxs-lookup"><span data-stu-id="97766-150">A Batch pool can contain both dedicated and low-priority VMs (also referred tooas compute nodes).</span></span> <span data-ttu-id="97766-151">Puede establecer el número de destino de Hola de nodos de proceso para las máquinas virtuales dedicadas y prioridad baja.</span><span class="sxs-lookup"><span data-stu-id="97766-151">You can set hello target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="97766-152">número de destino de nodos Hello especifica el número de Hola de máquinas virtuales que desee toohave en grupo Hola.</span><span class="sxs-lookup"><span data-stu-id="97766-152">hello target number of nodes specifies hello number of VMs you want toohave in hello pool.</span></span>

<span data-ttu-id="97766-153">Por ejemplo, toocreate a un grupo con máquinas virtuales del servicio de nube de Azure con un destino de 5 había dedicado a las máquinas virtuales y 20 máquinas virtuales de prioridad baja:</span><span class="sxs-lookup"><span data-stu-id="97766-153">For example, toocreate a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="97766-154">toocreate a un grupo con máquinas virtuales de Azure (en este caso, las máquinas virtuales de Linux) con un destino de 5 había dedicado a las máquinas virtuales y 20 máquinas virtuales de prioridad baja:</span><span class="sxs-lookup"><span data-stu-id="97766-154">toocreate a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="97766-155">Puede obtener el número actual de Hola de nodos para máquinas virtuales dedicadas y de baja prioridad:</span><span class="sxs-lookup"><span data-stu-id="97766-155">You can get hello current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="97766-156">Nodos de grupo tienen una propiedad tooindicate si el nodo de hello es una máquina virtual dedicada o baja:</span><span class="sxs-lookup"><span data-stu-id="97766-156">Pool nodes have a property tooindicate if hello node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="97766-157">Cuando se ve relegados uno o varios nodos en un grupo, una operación de nodos de la lista en el grupo también devolverá los nodos, número actual de Hola de nodos de prioridad baja permanecerán sin cambios, pero esos nodos tendrán su estado establecido toothe **cambiado**estado.</span><span class="sxs-lookup"><span data-stu-id="97766-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, hello current number of low-priority nodes will remain unchanged, but those nodes will have their state set toothe **Preempted** state.</span></span> <span data-ttu-id="97766-158">Lote intentará toofind reemplazo máquinas virtuales y, si es correcto, nodos de hello pasará a través de **crear** y, a continuación, **iniciando** Estados antes de estar disponibles para la ejecución de la tarea, al igual que los nuevos nodos.</span><span class="sxs-lookup"><span data-stu-id="97766-158">Batch will attempt toofind replacement VMs and, if successful, hello nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="97766-159">Escalado de un grupo que contiene máquinas virtuales de prioridad baja</span><span class="sxs-lookup"><span data-stu-id="97766-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="97766-160">Como con grupos formada únicamente por máquinas virtuales dedicadas, es posible tooscale una grupo de contenedor prioridad baja las máquinas virtuales llamando al método de cambio de tamaño de Hola o mediante el uso de escala automática.</span><span class="sxs-lookup"><span data-stu-id="97766-160">As with pools solely consisting of dedicated VMs, it is possible tooscale a pool containing low-priority VMs by calling hello Resize method or by using auto-scale.</span></span>

<span data-ttu-id="97766-161">operación de cambio de tamaño de bloque Hello toma un parámetro opcional en segundo lugar que actualiza el valor de **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="97766-161">hello pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="97766-162">fórmula de escala automática de grupo de Hello es compatible con las máquinas virtuales de prioridad baja como sigue:</span><span class="sxs-lookup"><span data-stu-id="97766-162">hello pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="97766-163">Puede obtener o establecer valor de hello de la variable definida por el servicio de hello **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="97766-163">You can get or set hello value of hello service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="97766-164">Puede obtener valor de saludo de la variable definida por el servicio de hello **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="97766-164">You can get hello value of hello service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="97766-165">Puede obtener valor de saludo de la variable definida por el servicio de hello **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="97766-165">You can get hello value of hello service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="97766-166">Esta variable devuelve número Hola de nodos Hola adelantadas estado y le permite escalar hacia arriba o hacia abajo el número de Hola de nodos dedicados, según el número de Hola de adelantamiento nodos que no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="97766-166">This variable returns hello number of nodes in hello preempted state and allows you to scale up or down hello number of dedicated nodes, depending on hello number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="97766-167">Trabajos y tareas</span><span class="sxs-lookup"><span data-stu-id="97766-167">Jobs and tasks</span></span>

<span data-ttu-id="97766-168">Trabajos y tareas que requieren compatibilidad con muy poco para los nodos de prioridad baja; solo se admite Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="97766-168">Jobs and tasks require very little support for low-priority nodes; hello only support is as follows:</span></span>

-   <span data-ttu-id="97766-169">Hola JobManagerTask propiedad de un trabajo tiene una propiedad nueva, **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="97766-169">hello JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="97766-170">Cuando esta propiedad es true, se puede programar la tarea del Administrador de trabajos de Hola en un nodo dedicado o baja.</span><span class="sxs-lookup"><span data-stu-id="97766-170">When this property is true, hello job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="97766-171">Si esta propiedad es false, tarea del Administrador de trabajos de hello será tooa programada sólo nodo dedicado.</span><span class="sxs-lookup"><span data-stu-id="97766-171">If this property is false, hello job manager task will be scheduled tooa dedicated node only.</span></span>

-   <span data-ttu-id="97766-172">Un [variable de entorno](batch-compute-node-environment-variables.md) es aplicación de la tarea de tooa disponibles para que pueda determinar si se está ejecutando en un nodo de prioridad baja o dedicado.</span><span class="sxs-lookup"><span data-stu-id="97766-172">An [environment variable](batch-compute-node-environment-variables.md) is available tooa task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="97766-173">variable de entorno de Hello es AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="97766-173">hello environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="97766-174">Control de reemplazos</span><span class="sxs-lookup"><span data-stu-id="97766-174">Handling preemption</span></span>

<span data-ttu-id="97766-175">Máquinas virtuales en ocasiones pueden tener preferencia sobre; Cuando esto sucede, lote Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="97766-175">VMs may occasionally be preempted; when this happens, Batch does hello following:</span></span>

-   <span data-ttu-id="97766-176">Hello adelantamiento de máquinas virtuales tienen su estado actualizan también**cambiado**.</span><span class="sxs-lookup"><span data-stu-id="97766-176">hello preempted VMs have their state updated too**Preempted**.</span></span>
-   <span data-ttu-id="97766-177">Si las tareas que se estaban ejecutando en hello adelantadas máquinas virtuales de nodos, dichas tareas se poner en cola y se vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="97766-177">If tasks were running on hello preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="97766-178">Hola VM también se elimina, datos tooany almacenados localmente en hello VM se pierde una vez más importantes.</span><span class="sxs-lookup"><span data-stu-id="97766-178">hello VM is effectively deleted, leading tooany data stored locally on hello VM being lost.</span></span>
-   <span data-ttu-id="97766-179">grupo de Hello continuamente intentos de número de destino de hello tooreach de prioridad baja nodos disponibles.</span><span class="sxs-lookup"><span data-stu-id="97766-179">hello pool continually attempts tooreach hello target number of low-priority nodes available.</span></span> <span data-ttu-id="97766-180">Cuando se encuentra la capacidad de reemplazo, los nodos mantienen sus identificaciones, pero se reinicializan, pasando por los estados**Creando** e **Iniciando** antes de que estén disponibles para la programación de tareas.</span><span class="sxs-lookup"><span data-stu-id="97766-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="97766-181">Recuentos de adelantamiento están disponibles como una métrica en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="97766-181">Preemption counts are available as a metric in hello Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="97766-182">Métricas</span><span class="sxs-lookup"><span data-stu-id="97766-182">Metrics</span></span>

<span data-ttu-id="97766-183">Nuevas métricas están disponibles en hello [portal de Azure](https://portal.azure.com) para los nodos de prioridad baja.</span><span class="sxs-lookup"><span data-stu-id="97766-183">New metrics are available in hello [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="97766-184">Estas son las métricas:</span><span class="sxs-lookup"><span data-stu-id="97766-184">These metrics are:</span></span>

- <span data-ttu-id="97766-185">Recuento de nodos de baja prioridad</span><span class="sxs-lookup"><span data-stu-id="97766-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="97766-186">Recuento de núcleos de baja prioridad</span><span class="sxs-lookup"><span data-stu-id="97766-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="97766-187">Recuento de nodos con prioridad</span><span class="sxs-lookup"><span data-stu-id="97766-187">Preempted Node Count</span></span>

<span data-ttu-id="97766-188">métricas de tooview Hola portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="97766-188">tooview metrics in hello Azure portal:</span></span>

1. <span data-ttu-id="97766-189">Navegue tooyour cuenta de lote en el portal de Hola y ver la configuración de Hola para su cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="97766-189">Navigate tooyour Batch account in hello portal, and view hello settings for your Batch account.</span></span>
2. <span data-ttu-id="97766-190">Seleccione **métricas** de hello **supervisión** sección.</span><span class="sxs-lookup"><span data-stu-id="97766-190">Select **Metrics** from hello **Monitoring** section.</span></span>
3. <span data-ttu-id="97766-191">Seleccione las métricas de Hola que desee de hello **métricas disponibles** lista.</span><span class="sxs-lookup"><span data-stu-id="97766-191">Select hello metrics you desire from hello **Available Metrics** list.</span></span>

![Métricas para nodos de baja prioridad](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="97766-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97766-193">Next steps</span></span>

* <span data-ttu-id="97766-194">Hola de lectura [Introducción a la característica por lotes para los desarrolladores](batch-api-basics.md), información esencial para todo aquel que preparar toouse por lotes.</span><span class="sxs-lookup"><span data-stu-id="97766-194">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="97766-195">artículo de Hello contiene información más detallada sobre los recursos del servicio por lotes como hello, nodos, trabajos y las tareas y grupos de muchas características de la API que puede usar al compilar la aplicación de lote.</span><span class="sxs-lookup"><span data-stu-id="97766-195">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="97766-196">Obtenga información acerca de hello [herramientas y API de lote](batch-apis-tools.md) disponibles para la creación de soluciones de lote.</span><span class="sxs-lookup"><span data-stu-id="97766-196">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
