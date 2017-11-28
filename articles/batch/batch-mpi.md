---
title: tareas de varias instancias de aaaUse aplicaciones de MPI toorun - Azure Batch | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de interfaz de paso de mensajes (MPI) tooexecute mediante la tarea de varias instancias de hello escriban en el lote de Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="ffacb-103">Usar las aplicaciones de interfaz de paso de mensajes (MPI) de toorun de tareas de varias instancias de lote</span><span class="sxs-lookup"><span data-stu-id="ffacb-103">Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="ffacb-104">Tareas de varias instancias le permiten toorun una tarea de lote de Azure en varios nodos de ejecución al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="ffacb-104">Multi-instance tasks allow you toorun an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="ffacb-105">Estas tareas permiten escenarios de informática de alto rendimiento como las aplicaciones de interfaz de paso de mensajes (MPI) en Lote.</span><span class="sxs-lookup"><span data-stu-id="ffacb-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="ffacb-106">En este artículo, aprenderá cómo Hola mediante las tareas de varias instancias de tooexecute [.NET de lotes] [ api_net] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="ffacb-106">In this article, you learn how tooexecute multi-instance tasks using hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="ffacb-107">Aunque los ejemplos de hello en este artículo se centran en .NET de lotes, MS-MPI, y nodos de proceso de Windows, conceptos de tarea de varias instancias de Hola que se tratan aquí son tooother aplicables plataformas y tecnologías (Python y Intel MPI en nodos de Linux, por ejemplo).</span><span class="sxs-lookup"><span data-stu-id="ffacb-107">While hello examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, hello multi-instance task concepts discussed here are applicable tooother platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="ffacb-108">Información general de las tareas de instancias múltiples</span><span class="sxs-lookup"><span data-stu-id="ffacb-108">Multi-instance task overview</span></span>
<span data-ttu-id="ffacb-109">En el lote, cada tarea suele ejecutar en un nodo de proceso único--que envíe varias tareas tooa trabajo y Hola servicio por lotes programa cada tarea para su ejecución en un nodo.</span><span class="sxs-lookup"><span data-stu-id="ffacb-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks tooa job, and hello Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="ffacb-110">Sin embargo, mediante la configuración de una tarea **configuración de varias instancias**, puede indicar a lote tooinstead crear una tarea principal y varias subtareas que, a continuación, se ejecutan en varios nodos.</span><span class="sxs-lookup"><span data-stu-id="ffacb-110">However, by configuring a task's **multi-instance settings**, you tell Batch tooinstead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="ffacb-111">![Información general de las tareas de instancias múltiples][1]</span><span class="sxs-lookup"><span data-stu-id="ffacb-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="ffacb-112">Cuando se envía una tarea de trabajo de tooa de configuración de varias instancias, lote realiza varias tareas de instancia única de toomulti de pasos:</span><span class="sxs-lookup"><span data-stu-id="ffacb-112">When you submit a task with multi-instance settings tooa job, Batch performs several steps unique toomulti-instance tasks:</span></span>

1. <span data-ttu-id="ffacb-113">Hola servicio por lotes crea una **principal** y varios **subtareas** en función de la configuración de varias instancias de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-113">hello Batch service creates one **primary** and several **subtasks** based on hello multi-instance settings.</span></span> <span data-ttu-id="ffacb-114">número total de Hola de tareas (principales además de todas las subtareas) coincide con número de Hola de **instancias** (nodos de proceso) especificados en la configuración de varias instancias de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-114">hello total number of tasks (primary plus all subtasks) matches hello number of **instances** (compute nodes) you specify in hello multi-instance settings.</span></span>
2. <span data-ttu-id="ffacb-115">Lote designa uno de hello nodos de proceso como hello **maestro**, y programaciones Hola tooexecute tarea principal en el patrón de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-115">Batch designates one of hello compute nodes as hello **master**, and schedules hello primary task tooexecute on hello master.</span></span> <span data-ttu-id="ffacb-116">Programa hello subtareas tooexecute en el resto de Hola de tarea de hello proceso nodos toohello asignado varias instancias, una subtarea por nodo.</span><span class="sxs-lookup"><span data-stu-id="ffacb-116">It schedules hello subtasks tooexecute on hello remainder of hello compute nodes allocated toohello multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="ffacb-117">Hola principal y todas las subtareas descargar cualquiera **archivos de recursos comunes** especificados en la configuración de varias instancias de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-117">hello primary and all subtasks download any **common resource files** you specify in hello multi-instance settings.</span></span>
4. <span data-ttu-id="ffacb-118">Después de que se han descargado los archivos de recursos comunes de hello, hello principal y subtareas ejecutan hello **comando coordinación** especificados en la configuración de varias instancias de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-118">After hello common resource files have been downloaded, hello primary and subtasks execute hello **coordination command** you specify in hello multi-instance settings.</span></span> <span data-ttu-id="ffacb-119">comando de coordinación de Hello es nodos tooprepare normalmente se usan para ejecutar la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="ffacb-119">hello coordination command is typically used tooprepare nodes for executing hello task.</span></span> <span data-ttu-id="ffacb-120">Esto puede incluir a partir de servicios de fondo (como [Microsoft MPI][msmpi_msdn]del `smpd.exe`) y comprobar que los nodos de hello son mensajes de tooprocess listo entre nodos.</span><span class="sxs-lookup"><span data-stu-id="ffacb-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that hello nodes are ready tooprocess inter-node messages.</span></span>
5. <span data-ttu-id="ffacb-121">tarea principal de Hello ejecuta hello **comando de la aplicación** en el nodo principal de hello *después* comando de coordinación de Hola se ha completado correctamente por hello principal y todas las subtareas.</span><span class="sxs-lookup"><span data-stu-id="ffacb-121">hello primary task executes hello **application command** on hello master node *after* hello coordination command has been completed successfully by hello primary and all subtasks.</span></span> <span data-ttu-id="ffacb-122">comando de la aplicación Hello es Hola de línea de comandos de la propia tarea de varias instancias hello y se ejecuta solo por la tarea principal de hello.</span><span class="sxs-lookup"><span data-stu-id="ffacb-122">hello application command is hello command line of hello multi-instance task itself, and is executed only by hello primary task.</span></span> <span data-ttu-id="ffacb-123">En una solución basada en [MS-MPI][msmpi_msdn], se trata del lugar donde ejecuta la aplicación habilitada para MPI mediante `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="ffacb-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="ffacb-124">Aunque es funcionalmente distinto, Hola "tarea de varias instancias" no es un tipo de tarea único como hello [StartTask] [ net_starttask] o [JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="ffacb-124">Though it is functionally distinct, hello "multi-instance task" is not a unique task type like hello [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="ffacb-125">tarea de varias instancias de Hello es simplemente una tarea de lote estándar ([CloudTask] [ net_task] en .NET de lote) se configuró cuya configuración de varias instancias.</span><span class="sxs-lookup"><span data-stu-id="ffacb-125">hello multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="ffacb-126">En este artículo, nos referiremos toothis como hello **tareas varias instancias**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-126">In this article, we refer toothis as hello **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="ffacb-127">Requisitos de las tareas de instancias múltiples</span><span class="sxs-lookup"><span data-stu-id="ffacb-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="ffacb-128">Las tareas de múltiples instancias requieren un grupo con la **comunicación ente nodos habilitada** y la **ejecución simultánea de tareas deshabilitada**.</span><span class="sxs-lookup"><span data-stu-id="ffacb-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="ffacb-129">ejecución de tareas simultáneas toodisable, conjunto hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 de propiedad.</span><span class="sxs-lookup"><span data-stu-id="ffacb-129">toodisable concurrent task execution, set hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property too1.</span></span>

<span data-ttu-id="ffacb-130">Este fragmento de código muestra cómo toocreate un grupo de instancias múltiples tareas utilizando la biblioteca de .NET de lotes de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-130">This code snippet shows how toocreate a pool for multi-instance tasks using hello Batch .NET library.</span></span>

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> <span data-ttu-id="ffacb-131">Si intentas toorun deshabilitada una tarea de varias instancias en un grupo con la comunicación entre nodos, o con un *maxTasksPerNode* valor mayor que 1, nunca se programa la tarea hello--indefinidamente permanece en estado de "activo" Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-131">If you try toorun a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, hello task is never scheduled--it remains indefinitely in hello "active" state.</span></span> 
>
> <span data-ttu-id="ffacb-132">Se podrán ejecutar tareas de varias instancias solo en nodos de los grupos creados después del 14 de diciembre de 2015.</span><span class="sxs-lookup"><span data-stu-id="ffacb-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a><span data-ttu-id="ffacb-133">Usar un tooinstall StartTask MPI</span><span class="sxs-lookup"><span data-stu-id="ffacb-133">Use a StartTask tooinstall MPI</span></span>
<span data-ttu-id="ffacb-134">aplicaciones de MPI toorun con una tarea de varias instancias, primero debe tooinstall una implementación de MPI en nodos de proceso de hello en el grupo de hello (MS-MPI o MPI de Intel, por ejemplo).</span><span class="sxs-lookup"><span data-stu-id="ffacb-134">toorun MPI applications with a multi-instance task, you first need tooinstall an MPI implementation (MS-MPI or Intel MPI, for example) on hello compute nodes in hello pool.</span></span> <span data-ttu-id="ffacb-135">Se trata de un buen momento toouse una [StartTask][net_starttask], que se ejecuta cada vez que un nodo une a un grupo o se ha reiniciado.</span><span class="sxs-lookup"><span data-stu-id="ffacb-135">This is a good time toouse a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="ffacb-136">Este fragmento de código crea un StartTask que especifica el paquete de instalación de hello MS-MPI como un [archivo de recursos][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="ffacb-136">This code snippet creates a StartTask that specifies hello MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="ffacb-137">línea de comandos de la tarea de inicio de Hola se ejecuta después de archivo de recursos de hello es nodo toohello descargado.</span><span class="sxs-lookup"><span data-stu-id="ffacb-137">hello start task's command line is executed after hello resource file is downloaded toohello node.</span></span> <span data-ttu-id="ffacb-138">En este caso, la línea de comandos de hello realiza una instalación desatendida de MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="ffacb-138">In this case, hello command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="ffacb-139">Acceso directo a memoria remota (RDMA)</span><span class="sxs-lookup"><span data-stu-id="ffacb-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="ffacb-140">Cuando se elige un [tamaño compatibles con RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como A9 para hello nodos de cálculo en el grupo de lote, la aplicación de MPI puede aprovechar las ventajas de alto rendimiento, latencia baja memoria directa remota (RDMA) de acceso de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffacb-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for hello compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="ffacb-141">Busque los tamaños de hello especificados como "Capacidad RDMA" Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="ffacb-141">Look for hello sizes specified as "RDMA capable" in hello following articles:</span></span>

* <span data-ttu-id="ffacb-142">Grupos de **CloudServiceConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ffacb-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="ffacb-143">[Tamaños de Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (solo Windows)</span><span class="sxs-lookup"><span data-stu-id="ffacb-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="ffacb-144">Grupos de **VirtualMachineConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ffacb-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="ffacb-145">[Tamaños de las máquinas virtuales en Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="ffacb-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="ffacb-146">[Tamaños de las máquinas virtuales en Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="ffacb-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="ffacb-147">tootake aprovechar RDMA en [nodos de proceso de Linux](batch-linux-nodes.md), debe usar **MPI Intel** en nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-147">tootake advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on hello nodes.</span></span> <span data-ttu-id="ffacb-148">Para obtener más información acerca de los grupos CloudServiceConfiguration y VirtualMachineConfiguration, vea Hola sección Pool de hello [Introducción a la característica por lotes](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="ffacb-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see hello Pool section of hello [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="ffacb-149">Creación de una tarea de instancias múltiples con .NET de Lote</span><span class="sxs-lookup"><span data-stu-id="ffacb-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="ffacb-150">Ahora que hemos analizado los requisitos de grupo de hello e instalación de paquete MPI, vamos a crear la tarea de varias instancias de hello.</span><span class="sxs-lookup"><span data-stu-id="ffacb-150">Now that we've covered hello pool requirements and MPI package installation, let's create hello multi-instance task.</span></span> <span data-ttu-id="ffacb-151">En este fragmento de código, creamos una instancia de [CloudTask][net_task] estándar y luego configuramos su propiedad [MultiInstanceSettings][net_multiinstance_prop].</span><span class="sxs-lookup"><span data-stu-id="ffacb-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="ffacb-152">Como se mencionó anteriormente, tarea de varias instancias de hello no es un tipo de tarea distintos, pero una tarea por lotes estándar configurado con la configuración de varias instancias.</span><span class="sxs-lookup"><span data-stu-id="ffacb-152">As mentioned earlier, hello multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="ffacb-153">Tarea principal y subtareas</span><span class="sxs-lookup"><span data-stu-id="ffacb-153">Primary task and subtasks</span></span>
<span data-ttu-id="ffacb-154">Cuando creas Hola configuración de varias instancias de una tarea, especifique número Hola de nodos de proceso que son tareas de hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="ffacb-154">When you create hello multi-instance settings for a task, you specify hello number of compute nodes that are tooexecute hello task.</span></span> <span data-ttu-id="ffacb-155">Cuando se envía el trabajo de la tarea tooa hello, Hola servicio por lotes crea una **principal** tareas y suficientes **subtareas** que coincidan conjuntamente con número de Hola de nodos especificado.</span><span class="sxs-lookup"><span data-stu-id="ffacb-155">When you submit hello task tooa job, hello Batch service creates one **primary** task and enough **subtasks** that together match hello number of nodes you specified.</span></span>

<span data-ttu-id="ffacb-156">Estas tareas se asignan un identificador entero del intervalo de hello 0 demasiado*numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="ffacb-156">These tasks are assigned an integer id in hello range of 0 too*numberOfInstances* - 1.</span></span> <span data-ttu-id="ffacb-157">tarea de Hello con Id. 0 es tarea principal de hello y todos los otros identificadores son subtareas.</span><span class="sxs-lookup"><span data-stu-id="ffacb-157">hello task with id 0 is hello primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="ffacb-158">Por ejemplo, si creas Hola después de la configuración de varias instancias de una tarea, tarea principal de hello tendría un identificador de 0 y Hola subtareas tendría identificadores del 1 al 9.</span><span class="sxs-lookup"><span data-stu-id="ffacb-158">For example, if you create hello following multi-instance settings for a task, hello primary task would have an id of 0, and hello subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="ffacb-159">Nodo maestro</span><span class="sxs-lookup"><span data-stu-id="ffacb-159">Master node</span></span>
<span data-ttu-id="ffacb-160">Cuando se envía una tarea de varias instancias, Hola servicio por lotes designa uno de hello nodos de proceso como nodo de "maestro" hello y programaciones Hola tooexecute tarea principal en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-160">When you submit a multi-instance task, hello Batch service designates one of hello compute nodes as hello "master" node, and schedules hello primary task tooexecute on hello master node.</span></span> <span data-ttu-id="ffacb-161">Hola subtareas son tooexecute programada del resto de nodos de hello asignado la tarea de varias instancias de toohello Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-161">hello subtasks are scheduled tooexecute on hello remainder of hello nodes allocated toohello multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="ffacb-162">comando de coordinación</span><span class="sxs-lookup"><span data-stu-id="ffacb-162">Coordination command</span></span>
<span data-ttu-id="ffacb-163">Hola **comando coordinación** se ejecuta Hola principal y las subtareas.</span><span class="sxs-lookup"><span data-stu-id="ffacb-163">hello **coordination command** is executed by both hello primary and subtasks.</span></span>

<span data-ttu-id="ffacb-164">está bloqueando la invocación de Hola de comando de coordinación de hello--por lotes no ejecutan el comando de la aplicación hello hasta que el comando de coordinación de hello ha devuelto correctamente para todas las subtareas.</span><span class="sxs-lookup"><span data-stu-id="ffacb-164">hello invocation of hello coordination command is blocking--Batch does not execute hello application command until hello coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="ffacb-165">comando de coordinación de Hello, por tanto, debe iniciar los servicios de fondo requerido, compruebe que están listas para su uso y, a continuación, salir.</span><span class="sxs-lookup"><span data-stu-id="ffacb-165">hello coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="ffacb-166">Por ejemplo, este comando de coordinación en una solución mediante MS-MPI versión 7 inicia el servicio SMPD de hello en el nodo de hello, entonces se cierra:</span><span class="sxs-lookup"><span data-stu-id="ffacb-166">For example, this coordination command for a solution using MS-MPI version 7 starts hello SMPD service on hello node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="ffacb-167">Tenga en cuenta uso Hola de `start` en este comando de coordinación.</span><span class="sxs-lookup"><span data-stu-id="ffacb-167">Note hello use of `start` in this coordination command.</span></span> <span data-ttu-id="ffacb-168">Esto es necesario porque hello `smpd.exe` aplicación no se devuelve inmediatamente después de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="ffacb-168">This is required because hello `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="ffacb-169">Sin usar Hola Hola [iniciar] [ cmd_start] de comandos, este comando de coordinación no devolvería y, por tanto, bloquearían Hola aplicación ejecución del comando.</span><span class="sxs-lookup"><span data-stu-id="ffacb-169">Without hello use of hello [start][cmd_start] command, this coordination command would not return, and would therefore block hello application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="ffacb-170">Comando de aplicación</span><span class="sxs-lookup"><span data-stu-id="ffacb-170">Application command</span></span>
<span data-ttu-id="ffacb-171">Una vez que la tarea principal de hello y todas las subtareas han terminado de ejecutar el comando de coordinación de hello, línea de comandos de la tarea de varias instancias de Hola se ejecuta por la tarea principal de hello *sólo*.</span><span class="sxs-lookup"><span data-stu-id="ffacb-171">Once hello primary task and all subtasks have finished executing hello coordination command, hello multi-instance task's command line is executed by hello primary task *only*.</span></span> <span data-ttu-id="ffacb-172">Llamamos a este hello **comando aplicación** toodistinguish de comando de coordinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-172">We call this hello **application command** toodistinguish it from hello coordination command.</span></span>

<span data-ttu-id="ffacb-173">Para las aplicaciones de MS-MPI, use Hola aplicación comando tooexecute una aplicación habilitada para MPI con `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="ffacb-173">For MS-MPI applications, use hello application command tooexecute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="ffacb-174">Por ejemplo, este es un comando de aplicación para una solución mediante la versión 7 de MS-MPI:</span><span class="sxs-lookup"><span data-stu-id="ffacb-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="ffacb-175">Dado que MS-MPI `mpiexec.exe` usa Hola `CCP_NODES` variable de forma predeterminada (vea [variables de entorno](#environment-variables)) hello (ejemplo) se excluye la línea de comandos de la aplicación anterior.</span><span class="sxs-lookup"><span data-stu-id="ffacb-175">Because MS-MPI's `mpiexec.exe` uses hello `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) hello example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="ffacb-176">Variables de entorno</span><span class="sxs-lookup"><span data-stu-id="ffacb-176">Environment variables</span></span>
<span data-ttu-id="ffacb-177">Proceso por lotes crea varios [variables de entorno] [ msdn_env_var] tareas toomulti-instancia específica en hello nodos asignan la tarea de varias instancias de tooa de proceso.</span><span class="sxs-lookup"><span data-stu-id="ffacb-177">Batch creates several [environment variables][msdn_env_var] specific toomulti-instance tasks on hello compute nodes allocated tooa multi-instance task.</span></span> <span data-ttu-id="ffacb-178">Las líneas de comando de coordinación y la aplicación puede hacer referencia a estas variables de entorno, como puede Hola scripts y programas que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="ffacb-178">Your coordination and application command lines can reference these environment variables, as can hello scripts and programs they execute.</span></span>

<span data-ttu-id="ffacb-179">Hello siguientes variables de entorno se crean Hola servicio por lotes para su uso por las tareas de varias instancias:</span><span class="sxs-lookup"><span data-stu-id="ffacb-179">hello following environment variables are created by hello Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="ffacb-180">Para obtener detalles completos sobre estos y Hola otras variables de entorno de proceso por lotes proceso nodo, incluido su contenido y la visibilidad, vea [variables de entorno de nodo de proceso][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="ffacb-180">For full details on these and hello other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="ffacb-181">ejemplo de código de Hello MPI de Linux de lote contiene un ejemplo de cómo se pueden utilizar algunas de estas variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="ffacb-181">hello Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="ffacb-182">Hola [coordinación cmd] [ coord_cmd_example] Bash script descarga la aplicación comunes y los archivos de entrada desde el almacenamiento de Azure, permite a un recurso compartido de Network File System (NFS) en el nodo principal de Hola y configura Hola otros nodos asignar tareas de varias instancias de toohello como clientes NFS.</span><span class="sxs-lookup"><span data-stu-id="ffacb-182">hello [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on hello master node, and configures hello other nodes allocated toohello multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="ffacb-183">Archivos de recursos</span><span class="sxs-lookup"><span data-stu-id="ffacb-183">Resource files</span></span>
<span data-ttu-id="ffacb-184">Hay dos conjuntos de tooconsider de archivos de recursos para tareas de varias instancias: **archivos de recursos comunes** que *todos los* descargar tareas (ambos principal y subtareas), hello y **dearchivosderecursos** especificado para hello varias instancias de tareas, que *sólo Hola principal* descargas de tareas.</span><span class="sxs-lookup"><span data-stu-id="ffacb-184">There are two sets of resource files tooconsider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and hello **resource files** specified for hello multi-instance task itself, which *only hello primary* task downloads.</span></span>

<span data-ttu-id="ffacb-185">Puede especificar uno o varios **archivos de recursos comunes** en la configuración de varias instancias de Hola para una tarea.</span><span class="sxs-lookup"><span data-stu-id="ffacb-185">You can specify one or more **common resource files** in hello multi-instance settings for a task.</span></span> <span data-ttu-id="ffacb-186">Estos archivos de recursos comunes se descargan desde [el almacenamiento de Azure](../storage/common/storage-introduction.md) en cada nodo **directorio compartido de tarea** Hola principal y todas las subtareas.</span><span class="sxs-lookup"><span data-stu-id="ffacb-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by hello primary and all subtasks.</span></span> <span data-ttu-id="ffacb-187">Puede tener acceso a directorio compartido de hello tareas de líneas de comandos de la aplicación y la coordinación mediante hello `AZ_BATCH_TASK_SHARED_DIR` variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="ffacb-187">You can access hello task shared directory from application and coordination command lines by using hello `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="ffacb-188">Hola `AZ_BATCH_TASK_SHARED_DIR` ruta de acceso es idéntico en cada tarea de varias instancias de nodo toohello asignado, lo que puede compartir un comando único coordinación entre Hola principal y todas las subtareas.</span><span class="sxs-lookup"><span data-stu-id="ffacb-188">hello `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated toohello multi-instance task, thus you can share a single coordination command between hello primary and all subtasks.</span></span> <span data-ttu-id="ffacb-189">Lote no "compartir" directorio de hello en un sentido de acceso remoto, pero puede usar como un montaje o compartir punto tal y como se mencionó anteriormente en la sugerencia de hello en variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="ffacb-189">Batch does not "share" hello directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in hello tip on environment variables.</span></span>

<span data-ttu-id="ffacb-190">Archivos de recursos que especifique para la propia tarea de varias instancias hello son directorio de trabajo de la tarea de toohello descargado, `AZ_BATCH_TASK_WORKING_DIR`, de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ffacb-190">Resource files that you specify for hello multi-instance task itself are downloaded toohello task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="ffacb-191">Tal y como se ha mencionado, en cambio toocommon archivos de recursos, solo tarea principal de hello descarga archivos de recursos especificados para la propia tarea de varias instancias Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-191">As mentioned, in contrast toocommon resource files, only hello primary task downloads resource files specified for hello  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffacb-192">Utilice siempre las variables de entorno de hello `AZ_BATCH_TASK_SHARED_DIR` y `AZ_BATCH_TASK_WORKING_DIR` directorios de toothese toorefer en las líneas de comando.</span><span class="sxs-lookup"><span data-stu-id="ffacb-192">Always use hello environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese directories in your command lines.</span></span> <span data-ttu-id="ffacb-193">No intente manualmente las rutas de acceso de tooconstruct Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-193">Do not attempt tooconstruct hello paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="ffacb-194">Duración de la tarea</span><span class="sxs-lookup"><span data-stu-id="ffacb-194">Task lifetime</span></span>
<span data-ttu-id="ffacb-195">duración de Hola de duración de hello tarea principal controles Hola de tarea de hello todo varias instancias.</span><span class="sxs-lookup"><span data-stu-id="ffacb-195">hello lifetime of hello primary task controls hello lifetime of hello entire multi-instance task.</span></span> <span data-ttu-id="ffacb-196">Cuando se cierra Hola principal, se terminan todas Hola subtareas.</span><span class="sxs-lookup"><span data-stu-id="ffacb-196">When hello primary exits, all of hello subtasks are terminated.</span></span> <span data-ttu-id="ffacb-197">código de salida de Hello de hello principal es el código de salida de hello de tarea hello y es, por tanto, toodetermine usado Hola éxito o error de tarea de Hola para fines de reintento.</span><span class="sxs-lookup"><span data-stu-id="ffacb-197">hello exit code of hello primary is hello exit code of hello task, and is therefore used toodetermine hello success or failure of hello task for retry purposes.</span></span>

<span data-ttu-id="ffacb-198">Si se produce un error en cualquiera de las subtareas hello, salir con un código de retorno distinto de cero, por ejemplo, hello todo varias instancias tarea genera un error.</span><span class="sxs-lookup"><span data-stu-id="ffacb-198">If any of hello subtasks fail, exiting with a non-zero return code, for example, hello entire multi-instance task fails.</span></span> <span data-ttu-id="ffacb-199">tarea de varias instancias de Hello, a continuación, se terminan y se vuelve a intentar la tooits límite de reintentos.</span><span class="sxs-lookup"><span data-stu-id="ffacb-199">hello multi-instance task is then terminated and retried, up tooits retry limit.</span></span>

<span data-ttu-id="ffacb-200">Cuando se elimina una tarea de varias instancias, también se eliminan por servicio por lotes de Hola Hola principal y todas las subtareas.</span><span class="sxs-lookup"><span data-stu-id="ffacb-200">When you delete a multi-instance task, hello primary and all subtasks are also deleted by hello Batch service.</span></span> <span data-ttu-id="ffacb-201">Todos los directorios de subtarea y sus archivos se eliminan de los nodos de proceso de hello, como ocurre con una tarea estándar.</span><span class="sxs-lookup"><span data-stu-id="ffacb-201">All subtask directories and their files are deleted from hello compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="ffacb-202">[TaskConstraints] [ net_taskconstraints] para una tarea de varias instancias, como hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], y [RetentionTime] [ net_taskconstraint_retention] se respetan las propiedades, como son para una tarea estándar y aplicar toohello principal y todas las subtareas.</span><span class="sxs-lookup"><span data-stu-id="ffacb-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply toohello primary and all subtasks.</span></span> <span data-ttu-id="ffacb-203">Sin embargo, si cambia hello [RetentionTime] [ net_taskconstraint_retention] propiedad después de agregar el trabajo de toohello tarea hello varias instancias, este cambio es tarea principal toohello solo aplicada.</span><span class="sxs-lookup"><span data-stu-id="ffacb-203">However, if you change hello [RetentionTime][net_taskconstraint_retention] property after adding hello multi-instance task toohello job, this change is applied only toohello primary task.</span></span> <span data-ttu-id="ffacb-204">Todas las subtareas de hello contribuyen toouse Hola original [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="ffacb-204">All of hello subtasks continue toouse hello original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="ffacb-205">Lista de tareas recientes de un nodo de proceso refleja identificador hello de una subtarea si tareas recientes Hola formaba parte de una tarea de varias instancias.</span><span class="sxs-lookup"><span data-stu-id="ffacb-205">A compute node's recent task list reflects hello id of a subtask if hello recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="ffacb-206">Obtención de información sobre las subtareas</span><span class="sxs-lookup"><span data-stu-id="ffacb-206">Obtain information about subtasks</span></span>
<span data-ttu-id="ffacb-207">información de tooobtain en subtareas mediante .NET de lote Hola biblioteca, llamada hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] método.</span><span class="sxs-lookup"><span data-stu-id="ffacb-207">tooobtain information on subtasks by using hello Batch .NET library, call hello [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="ffacb-208">Este método devuelve información sobre todas las subtareas y obtener información acerca de hello proceso nodo que ejecuta tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-208">This method returns information on all subtasks, and information about hello compute node that executed hello tasks.</span></span> <span data-ttu-id="ffacb-209">De esta información, puede determinar el directorio de raíz de cada subtarea, Id. de grupo de hello, su estado actual, código de salida y mucho más.</span><span class="sxs-lookup"><span data-stu-id="ffacb-209">From this information, you can determine each subtask's root directory, hello pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="ffacb-210">Esta información se puede utilizar en combinación con hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] archivos de subtarea de método tooobtain Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-210">You can use this information in combination with hello [PoolOperations.GetNodeFile][poolops_getnodefile] method tooobtain hello subtask's files.</span></span> <span data-ttu-id="ffacb-211">Tenga en cuenta que este método no devuelve información de la tarea principal de hello (Id. 0).</span><span class="sxs-lookup"><span data-stu-id="ffacb-211">Note that this method does not return information for hello primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="ffacb-212">A menos que se indique lo contrario, los métodos de .NET de lotes que operan en Hola varias instancias [CloudTask] [ net_task] propio aplicar *sólo* toohello de tarea principal.</span><span class="sxs-lookup"><span data-stu-id="ffacb-212">Unless otherwise stated, Batch .NET methods that operate on hello multi-instance [CloudTask][net_task] itself apply *only* toohello primary task.</span></span> <span data-ttu-id="ffacb-213">Por ejemplo, cuando se llama a hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles] método en una tarea de varias instancias, se devuelven únicamente los archivos de la tarea principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-213">For example, when you call hello [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only hello primary task's files are returned.</span></span>
>
>

<span data-ttu-id="ffacb-214">Hello fragmento de código siguiente muestra cómo tooobtain subtarea información, así como contenido del archivo de solicitud de nodos de hello en el que ejecuta.</span><span class="sxs-lookup"><span data-stu-id="ffacb-214">hello following code snippet shows how tooobtain subtask information, as well as request file contents from hello nodes on which they executed.</span></span>

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a><span data-ttu-id="ffacb-215">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ffacb-215">Code sample</span></span>
<span data-ttu-id="ffacb-216">Hola [MultiInstanceTasks] [ github_mpi] ejemplo de código en GitHub muestra cómo toouse una instancia de varias tareas toorun una [MS-MPI] [ msmpi_msdn] aplicación de nodos de proceso por lotes.</span><span class="sxs-lookup"><span data-stu-id="ffacb-216">hello [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how toouse a multi-instance task toorun an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="ffacb-217">Siga los pasos de hello en [preparación](#preparation) y [ejecución](#execution) ejemplo de Hola a toorun.</span><span class="sxs-lookup"><span data-stu-id="ffacb-217">Follow hello steps in [Preparation](#preparation) and [Execution](#execution) toorun hello sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="ffacb-218">Preparación</span><span class="sxs-lookup"><span data-stu-id="ffacb-218">Preparation</span></span>
1. <span data-ttu-id="ffacb-219">Siga los dos primeros pasos de hello en [cómo toocompile y ejecutar un programa sencillo de MS-MPI][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="ffacb-219">Follow hello first two steps in [How toocompile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="ffacb-220">Esto cumple hello prerequesites para hello siguiendo el paso.</span><span class="sxs-lookup"><span data-stu-id="ffacb-220">This satisfies hello prerequesites for hello following step.</span></span>
2. <span data-ttu-id="ffacb-221">Crear un *versión* versión de hello [MPIHelloWorld] [ helloworld_proj] programa de MPI de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ffacb-221">Build a *Release* version of hello [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="ffacb-222">Se trata de un programa hello que se ejecutará en los nodos de proceso mediante la tarea de varias instancias de hello.</span><span class="sxs-lookup"><span data-stu-id="ffacb-222">This is hello program that will be run on compute nodes by hello multi-instance task.</span></span>
3. <span data-ttu-id="ffacb-223">Cree un archivo zip que contenga `MPIHelloWorld.exe` (creado en el paso 2) y `MSMpiSetup.exe` (descargado en el paso 1).</span><span class="sxs-lookup"><span data-stu-id="ffacb-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="ffacb-224">Cargue este archivo zip como un paquete de aplicación en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="ffacb-224">You'll upload this zip file as an application package in hello next step.</span></span>
4. <span data-ttu-id="ffacb-225">Hola de uso [portal de Azure] [ portal] toocreate un lote [aplicación](batch-application-packages.md) denominado "MPIHelloWorld" y especifique el archivo zip de hello creado en el paso anterior de hello como versión "1.0" de paquete de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-225">Use hello [Azure portal][portal] toocreate a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify hello zip file you created in hello previous step as version "1.0" of hello application package.</span></span> <span data-ttu-id="ffacb-226">Para más información, consulte [Carga y administración de aplicaciones](batch-application-packages.md#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="ffacb-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="ffacb-227">Crear un *versión* versión de `MPIHelloWorld.exe` para que no tengan tooinclude las dependencias adicionales (por ejemplo, `msvcp140d.dll` o `vcruntime140d.dll`) en el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ffacb-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have tooinclude any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="ffacb-228">Ejecución</span><span class="sxs-lookup"><span data-stu-id="ffacb-228">Execution</span></span>
1. <span data-ttu-id="ffacb-229">Descargar hello [ejemplos de lote de azure] [ github_samples_zip] desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="ffacb-229">Download hello [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="ffacb-230">Abra hello MultiInstanceTasks **solución** en Visual Studio 2015 o versiones más recientes.</span><span class="sxs-lookup"><span data-stu-id="ffacb-230">Open hello MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="ffacb-231">Hola `MultiInstanceTasks.sln` archivo de solución se encuentra en:</span><span class="sxs-lookup"><span data-stu-id="ffacb-231">hello `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="ffacb-232">Escriba sus credenciales de cuenta de lote y el almacenamiento en `AccountSettings.settings` en hello **Microsoft.Azure.Batch.Samples.Common** proyecto.</span><span class="sxs-lookup"><span data-stu-id="ffacb-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="ffacb-233">**Compilar y ejecutar** el aplicación de ejemplo de Hola MultiInstanceTasks solución tooexecute Hola MPI en nodos de cálculo en un grupo de lote.</span><span class="sxs-lookup"><span data-stu-id="ffacb-233">**Build and run** hello MultiInstanceTasks solution tooexecute hello MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="ffacb-234">*Opcional*: Hola de uso [portal de Azure] [ portal] o hello [Explorer lote] [ batch_explorer] tooexamine grupo de ejemplo de Hola, trabajo, y tarea ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") antes de eliminar los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ffacb-234">*Optional*: Use hello [Azure portal][portal] or hello [Batch Explorer][batch_explorer] tooexamine hello sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete hello resources.</span></span>

> [!TIP]
> <span data-ttu-id="ffacb-235">Si no tiene Visual Studio, puede descargar gratis [Visual Studio Community][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="ffacb-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="ffacb-236">Resultado de `MultiInstanceTasks.exe` es similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="ffacb-236">Output from `MultiInstanceTasks.exe` is similar toohello following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="ffacb-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ffacb-237">Next steps</span></span>
* <span data-ttu-id="ffacb-238">blog del equipo de lote de Azure y Microsoft HPC Hola describe [MPI compatibilidad con Linux en Azure Batch][blog_mpi_linux]e incluye información sobre el uso de [OpenFOAM] [ openfoam] con el lote.</span><span class="sxs-lookup"><span data-stu-id="ffacb-238">hello Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="ffacb-239">Puede encontrar ejemplos de código de Python para hello [ejemplo OpenFOAM en GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="ffacb-239">You can find Python code samples for hello [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="ffacb-240">Obtenga información acerca de cómo demasiado[crear grupos de nodos de proceso de Linux](batch-linux-nodes.md) para su uso en sus soluciones de MPI de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffacb-240">Learn how too[create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Información general de instancias múltiples"
