---
title: "Uso de tareas de instancias múltiples para ejecutar aplicaciones de MPI: Azure Batch | Microsoft Docs"
description: "Obtenga información sobre cómo ejecutar aplicaciones de Interfaz de paso de mensajes (MPI) con el tipo de tarea de instancias múltiples en Lote de Azure."
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
ms.openlocfilehash: 77d12d6d48b22dfb3e7f09f273dffc11401bb15f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-multi-instance-tasks-to-run-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="a88dc-103">Uso de tareas de instancias múltiples para ejecutar aplicaciones de la Interfaz de paso de mensajes (MPI) en Batch</span><span class="sxs-lookup"><span data-stu-id="a88dc-103">Use multi-instance tasks to run Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="a88dc-104">Las tareas de instancias múltiples le permiten ejecutar una tarea de Lote de Azure en varios nodos de proceso al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="a88dc-104">Multi-instance tasks allow you to run an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="a88dc-105">Estas tareas permiten escenarios de informática de alto rendimiento como las aplicaciones de interfaz de paso de mensajes (MPI) en Lote.</span><span class="sxs-lookup"><span data-stu-id="a88dc-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="a88dc-106">En este artículo, aprenderá a ejecutar tareas de instancias múltiples mediante la biblioteca [.NET de Batch][api_net].</span><span class="sxs-lookup"><span data-stu-id="a88dc-106">In this article, you learn how to execute multi-instance tasks using the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="a88dc-107">Aunque los ejemplos de este artículo se centran en .NET de Batch, MS-MPI y los nodos de proceso de Windows, los conceptos de tareas de múltiples instancias aquí tratados son aplicables a otras plataformas y tecnologías (Python e Intel MPI en nodos de Linux, por ejemplo).</span><span class="sxs-lookup"><span data-stu-id="a88dc-107">While the examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, the multi-instance task concepts discussed here are applicable to other platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="a88dc-108">Información general de las tareas de instancias múltiples</span><span class="sxs-lookup"><span data-stu-id="a88dc-108">Multi-instance task overview</span></span>
<span data-ttu-id="a88dc-109">En Lote, cada tarea se ejecuta normalmente en un solo nodo de proceso: se envían varias tareas a un trabajo y el servicio Lote programa la ejecución de cada tarea en un nodo.</span><span class="sxs-lookup"><span data-stu-id="a88dc-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks to a job, and the Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="a88dc-110">No obstante, si establece la **configuración de instancias múltiples** en una tarea, le estará diciendo a Batch que cree una tarea principal y varias tareas secundarias que se ejecutarán después en varios nodos.</span><span class="sxs-lookup"><span data-stu-id="a88dc-110">However, by configuring a task's **multi-instance settings**, you tell Batch to instead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="a88dc-111">![Información general de las tareas de instancias múltiples][1]</span><span class="sxs-lookup"><span data-stu-id="a88dc-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="a88dc-112">Al enviar una tarea con configuración de instancias múltiples a un trabajo, el servicio Lote realiza  varios pasos que son específicos de las tareas de instancias múltiples:</span><span class="sxs-lookup"><span data-stu-id="a88dc-112">When you submit a task with multi-instance settings to a job, Batch performs several steps unique to multi-instance tasks:</span></span>

1. <span data-ttu-id="a88dc-113">El servicio Batch crea una tarea **principal** y varias tareas **secundarias** en función de la configuración de instancias múltiples definida.</span><span class="sxs-lookup"><span data-stu-id="a88dc-113">The Batch service creates one **primary** and several **subtasks** based on the multi-instance settings.</span></span> <span data-ttu-id="a88dc-114">El número total de tareas (principales y todas las subtareas) coincide con el número de **instancias** (nodos de proceso) especificado en la configuración de múltiples instancias.</span><span class="sxs-lookup"><span data-stu-id="a88dc-114">The total number of tasks (primary plus all subtasks) matches the number of **instances** (compute nodes) you specify in the multi-instance settings.</span></span>
2. <span data-ttu-id="a88dc-115">Batch designa uno de los nodos de proceso como el **maestro**, y programa la tarea principal para que se ejecute en el maestro.</span><span class="sxs-lookup"><span data-stu-id="a88dc-115">Batch designates one of the compute nodes as the **master**, and schedules the primary task to execute on the master.</span></span> <span data-ttu-id="a88dc-116">Programa las subtareas para que se ejecuten en el resto de los nodos de proceso asignados a la tarea de múltiples instancias, una subtarea por nodo.</span><span class="sxs-lookup"><span data-stu-id="a88dc-116">It schedules the subtasks to execute on the remainder of the compute nodes allocated to the multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="a88dc-117">Estas tareas, tanto la principal como las subtareas, descargan los **archivos de recursos comunes** que se especifican en la configuración de múltiples instancias.</span><span class="sxs-lookup"><span data-stu-id="a88dc-117">The primary and all subtasks download any **common resource files** you specify in the multi-instance settings.</span></span>
4. <span data-ttu-id="a88dc-118">Cuando se han descargado los archivos de recursos comunes, la tarea principal y las subtareas ejecutan el **comando de coordinación** que se especifica en la configuración de instancias múltiples.</span><span class="sxs-lookup"><span data-stu-id="a88dc-118">After the common resource files have been downloaded, the primary and subtasks execute the **coordination command** you specify in the multi-instance settings.</span></span> <span data-ttu-id="a88dc-119">El comando de coordinación normalmente se utiliza para preparar los nodos para ejecutar la tarea.</span><span class="sxs-lookup"><span data-stu-id="a88dc-119">The coordination command is typically used to prepare nodes for executing the task.</span></span> <span data-ttu-id="a88dc-120">Esto puede incluir iniciar servicios en segundo plano (como los de [Microsoft MPI][msmpi_msdn]`smpd.exe`) y comprobar que los nodos están listos para procesar los mensajes entre nodos.</span><span class="sxs-lookup"><span data-stu-id="a88dc-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that the nodes are ready to process inter-node messages.</span></span>
5. <span data-ttu-id="a88dc-121">La tarea principal ejecuta el **comando de aplicación** en el nodo maestro *después de* que la principal y todas las subtareas hayan completado correctamente el comando de coordinación.</span><span class="sxs-lookup"><span data-stu-id="a88dc-121">The primary task executes the **application command** on the master node *after* the coordination command has been completed successfully by the primary and all subtasks.</span></span> <span data-ttu-id="a88dc-122">Solo la tarea principal ejecuta el comando de aplicación, que es la línea de comandos especificada de la tarea de múltiples instancias.</span><span class="sxs-lookup"><span data-stu-id="a88dc-122">The application command is the command line of the multi-instance task itself, and is executed only by the primary task.</span></span> <span data-ttu-id="a88dc-123">En una solución basada en [MS-MPI][msmpi_msdn], se trata del lugar donde ejecuta la aplicación habilitada para MPI mediante `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="a88dc-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="a88dc-124">Aunque es funcionalmente distinta, la "tarea de instancias múltiples" no es un tipo de tarea única como [StartTask][net_starttask] o [JobPreparationTask][net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="a88dc-124">Though it is functionally distinct, the "multi-instance task" is not a unique task type like the [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="a88dc-125">La tarea de instancias múltiples es simplemente una tarea de Batch estándar ([CloudTask][net_task] en .NET de Batch) cuya opción de instancias múltiples se ha configurado.</span><span class="sxs-lookup"><span data-stu-id="a88dc-125">The multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="a88dc-126">En este artículo, nos referiremos a ella como **tarea de instancias múltiples**.</span><span class="sxs-lookup"><span data-stu-id="a88dc-126">In this article, we refer to this as the **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="a88dc-127">Requisitos de las tareas de instancias múltiples</span><span class="sxs-lookup"><span data-stu-id="a88dc-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="a88dc-128">Las tareas de múltiples instancias requieren un grupo con la **comunicación ente nodos habilitada** y la **ejecución simultánea de tareas deshabilitada**.</span><span class="sxs-lookup"><span data-stu-id="a88dc-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="a88dc-129">Para deshabilitar la ejecución de tareas simultáneas, establezca la propiedad [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) en 1.</span><span class="sxs-lookup"><span data-stu-id="a88dc-129">To disable concurrent task execution, set the [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property to 1.</span></span>

<span data-ttu-id="a88dc-130">Este fragmento de código muestra cómo crear un grupo para tareas de varias instancias mediante la biblioteca de .NET de Batch.</span><span class="sxs-lookup"><span data-stu-id="a88dc-130">This code snippet shows how to create a pool for multi-instance tasks using the Batch .NET library.</span></span>

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
> <span data-ttu-id="a88dc-131">Si intenta ejecutar una tarea de instancias múltiples en un grupo con la comunicación entre nodos deshabilitada o con un valor de *maxTasksPerNode* superior a 1, la tarea nunca será programada, sino que permanecerá indefinidamente en estado "activo".</span><span class="sxs-lookup"><span data-stu-id="a88dc-131">If you try to run a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, the task is never scheduled--it remains indefinitely in the "active" state.</span></span> 
>
> <span data-ttu-id="a88dc-132">Se podrán ejecutar tareas de varias instancias solo en nodos de los grupos creados después del 14 de diciembre de 2015.</span><span class="sxs-lookup"><span data-stu-id="a88dc-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-to-install-mpi"></a><span data-ttu-id="a88dc-133">Uso de StartTask para instalar MPI</span><span class="sxs-lookup"><span data-stu-id="a88dc-133">Use a StartTask to install MPI</span></span>
<span data-ttu-id="a88dc-134">Para ejecutar aplicaciones MPI con una tarea de instancias múltiples, primero debe instalar una implementación de MPI (por ejemplo, MS-MPI o Intel MPI) en los nodos de proceso del grupo.</span><span class="sxs-lookup"><span data-stu-id="a88dc-134">To run MPI applications with a multi-instance task, you first need to install an MPI implementation (MS-MPI or Intel MPI, for example) on the compute nodes in the pool.</span></span> <span data-ttu-id="a88dc-135">Es un buen momento para utilizar una instancia de [StartTask][net_starttask], que se ejecuta cada vez que un nodo se une a un grupo o se ha reiniciado.</span><span class="sxs-lookup"><span data-stu-id="a88dc-135">This is a good time to use a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="a88dc-136">En este fragmento de código se crea un objeto StartTask que especifica el paquete de instalación de MS-MPI como un [archivo de recursos][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="a88dc-136">This code snippet creates a StartTask that specifies the MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="a88dc-137">La línea de comandos de la tarea de inicio se ejecuta una vez que el archivo de recurso se ha descargado en el nodo.</span><span class="sxs-lookup"><span data-stu-id="a88dc-137">The start task's command line is executed after the resource file is downloaded to the node.</span></span> <span data-ttu-id="a88dc-138">En este caso, la línea de comandos realiza una instalación desatendida de MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="a88dc-138">In this case, the command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for the pool which we use for installing MS-MPI on
// the nodes as they join the pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit the fully configured pool to the Batch service to actually create
// the pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="a88dc-139">Acceso directo a memoria remota (RDMA)</span><span class="sxs-lookup"><span data-stu-id="a88dc-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="a88dc-140">Cuando elige el [tamaño con capacidad RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como A9 para los nodos de proceso del grupo de Batch, la aplicación de MPI puede aprovechar la red de acceso directo a memoria remota (RDMA) de alto rendimiento y baja latencia de Azure.</span><span class="sxs-lookup"><span data-stu-id="a88dc-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for the compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="a88dc-141">Consulte los tamaños compatibles con RDMA en los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="a88dc-141">Look for the sizes specified as "RDMA capable" in the following articles:</span></span>

* <span data-ttu-id="a88dc-142">Grupos de **CloudServiceConfiguration**</span><span class="sxs-lookup"><span data-stu-id="a88dc-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="a88dc-143">[Tamaños de Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (solo Windows)</span><span class="sxs-lookup"><span data-stu-id="a88dc-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="a88dc-144">Grupos de **VirtualMachineConfiguration**</span><span class="sxs-lookup"><span data-stu-id="a88dc-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="a88dc-145">[Tamaños de las máquinas virtuales en Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="a88dc-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="a88dc-146">[Tamaños de las máquinas virtuales en Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="a88dc-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="a88dc-147">Para sacar el máximo provecho a RDMA en los [nodos de proceso de Linux](batch-linux-nodes.md), debe utilizar **Intel MPI** en esos nodos.</span><span class="sxs-lookup"><span data-stu-id="a88dc-147">To take advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on the nodes.</span></span> <span data-ttu-id="a88dc-148">Para obtener más información sobre los grupos de CloudServiceConfiguration y VirtualMachineConfiguration, consulte la sección [Grupo](batch-api-basics.md) de la información general sobre las características de Batch.</span><span class="sxs-lookup"><span data-stu-id="a88dc-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see the Pool section of the [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="a88dc-149">Creación de una tarea de instancias múltiples con .NET de Lote</span><span class="sxs-lookup"><span data-stu-id="a88dc-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="a88dc-150">Ahora que hemos analizado los requisitos de grupo y la instalación del paquete MPI, vamos a crear la tarea de instancias múltiples.</span><span class="sxs-lookup"><span data-stu-id="a88dc-150">Now that we've covered the pool requirements and MPI package installation, let's create the multi-instance task.</span></span> <span data-ttu-id="a88dc-151">En este fragmento de código, creamos una instancia de [CloudTask][net_task] estándar y luego configuramos su propiedad [MultiInstanceSettings][net_multiinstance_prop].</span><span class="sxs-lookup"><span data-stu-id="a88dc-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="a88dc-152">Como se mencionó anteriormente, la tarea de instancias múltiples no es un tipo de tarea distinto, sino una tarea de Lote estándar configurada con la opción de instancias múltiples.</span><span class="sxs-lookup"><span data-stu-id="a88dc-152">As mentioned earlier, the multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create the multi-instance task. Its command line is the "application command"
// and will be executed *only* by the primary, and only after the primary and
// subtasks execute the CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure the task's MultiInstanceSettings. The CoordinationCommandLine will be executed by
// the primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit the task to the job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on the nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="a88dc-153">Tarea principal y subtareas</span><span class="sxs-lookup"><span data-stu-id="a88dc-153">Primary task and subtasks</span></span>
<span data-ttu-id="a88dc-154">Cuando se crea la configuración de instancias múltiples para una tarea, se especifica el número de nodos de proceso que ejecutarán la tarea.</span><span class="sxs-lookup"><span data-stu-id="a88dc-154">When you create the multi-instance settings for a task, you specify the number of compute nodes that are to execute the task.</span></span> <span data-ttu-id="a88dc-155">Cuando se envía la tarea a un trabajo, el servicio Batch crea una tarea **principal** y suficientes **subtareas** que, juntas, coinciden con el número de nodos especificado.</span><span class="sxs-lookup"><span data-stu-id="a88dc-155">When you submit the task to a job, the Batch service creates one **primary** task and enough **subtasks** that together match the number of nodes you specified.</span></span>

<span data-ttu-id="a88dc-156">A estas tareas se les asigna a un identificador entero del intervalo de 0 a *numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="a88dc-156">These tasks are assigned an integer id in the range of 0 to *numberOfInstances* - 1.</span></span> <span data-ttu-id="a88dc-157">La tarea con el identificador 0 es la tarea principal y todos los demás identificadores son subtareas.</span><span class="sxs-lookup"><span data-stu-id="a88dc-157">The task with id 0 is the primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="a88dc-158">Por ejemplo, si crea la siguiente configuración de instancias múltiples para una tarea, la tarea principal tendrá un identificador de 0 y las subtareas tendrán los identificadores del 1 al 9.</span><span class="sxs-lookup"><span data-stu-id="a88dc-158">For example, if you create the following multi-instance settings for a task, the primary task would have an id of 0, and the subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="a88dc-159">Nodo maestro</span><span class="sxs-lookup"><span data-stu-id="a88dc-159">Master node</span></span>
<span data-ttu-id="a88dc-160">Cuando se envía una tarea de múltiples instancias, el servicio Batch designa uno de los nodos de proceso como el nodo "maestro" y programa la tarea principal para que se ejecute en el nodo maestro.</span><span class="sxs-lookup"><span data-stu-id="a88dc-160">When you submit a multi-instance task, the Batch service designates one of the compute nodes as the "master" node, and schedules the primary task to execute on the master node.</span></span> <span data-ttu-id="a88dc-161">Las subtareas se programan para ejecutarse en el resto de los nodos asignados a la tarea de múltiples instancias.</span><span class="sxs-lookup"><span data-stu-id="a88dc-161">The subtasks are scheduled to execute on the remainder of the nodes allocated to the multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="a88dc-162">comando de coordinación</span><span class="sxs-lookup"><span data-stu-id="a88dc-162">Coordination command</span></span>
<span data-ttu-id="a88dc-163">El **comando de coordinación** ejecuta tanto tareas principales como subtareas.</span><span class="sxs-lookup"><span data-stu-id="a88dc-163">The **coordination command** is executed by both the primary and subtasks.</span></span>

<span data-ttu-id="a88dc-164">La invocación del comando de coordinación se bloquea: el servicio Lote no ejecuta el comando de aplicación hasta que el comando de coordinación se ha devuelto correctamente para todas las subtareas.</span><span class="sxs-lookup"><span data-stu-id="a88dc-164">The invocation of the coordination command is blocking--Batch does not execute the application command until the coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="a88dc-165">Por lo tanto, el comando de coordinación debe iniciar los servicios en segundo plano necesarios, comprobar que están listos para utilizarse y luego cerrarse.</span><span class="sxs-lookup"><span data-stu-id="a88dc-165">The coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="a88dc-166">Por ejemplo, este comando de coordinación para una solución que utiliza la versión 7 de MS-MPI inicia el servicio SMPD en el nodo y luego se cierra:</span><span class="sxs-lookup"><span data-stu-id="a88dc-166">For example, this coordination command for a solution using MS-MPI version 7 starts the SMPD service on the node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="a88dc-167">Observe el uso de `start` en este comando de coordinación.</span><span class="sxs-lookup"><span data-stu-id="a88dc-167">Note the use of `start` in this coordination command.</span></span> <span data-ttu-id="a88dc-168">Esto es necesario porque la aplicación `smpd.exe` no devuelve resultados inmediatamente después de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="a88dc-168">This is required because the `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="a88dc-169">Sin el uso del comando [start][cmd_start], este comando de coordinación no devolvería resultados y, por tanto, impediría que se ejecutara el comando de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a88dc-169">Without the use of the [start][cmd_start] command, this coordination command would not return, and would therefore block the application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="a88dc-170">Comando de aplicación</span><span class="sxs-lookup"><span data-stu-id="a88dc-170">Application command</span></span>
<span data-ttu-id="a88dc-171">Una vez que la tarea principal y todas las subtareas han terminado de ejecutar el comando de coordinación, *solo*la tarea principal ejecuta la línea de comandos de la tarea de instancias múltiples.</span><span class="sxs-lookup"><span data-stu-id="a88dc-171">Once the primary task and all subtasks have finished executing the coordination command, the multi-instance task's command line is executed by the primary task *only*.</span></span> <span data-ttu-id="a88dc-172">Llamaremos a este el **comando de aplicación** para distinguirlo del comando de coordinación.</span><span class="sxs-lookup"><span data-stu-id="a88dc-172">We call this the **application command** to distinguish it from the coordination command.</span></span>

<span data-ttu-id="a88dc-173">Para las aplicaciones de MS-MPI, use el comando de aplicación para ejecutar la aplicación habilitada para MPI con `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="a88dc-173">For MS-MPI applications, use the application command to execute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="a88dc-174">Por ejemplo, este es un comando de aplicación para una solución mediante la versión 7 de MS-MPI:</span><span class="sxs-lookup"><span data-stu-id="a88dc-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="a88dc-175">Dado que `mpiexec.exe` de MS-MPI utiliza la variable `CCP_NODES` de forma predeterminada (consulte [Variables de entorno](#environment-variables)), la línea de comandos de aplicación del ejemplo anterior la excluye.</span><span class="sxs-lookup"><span data-stu-id="a88dc-175">Because MS-MPI's `mpiexec.exe` uses the `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) the example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="a88dc-176">Variables de entorno</span><span class="sxs-lookup"><span data-stu-id="a88dc-176">Environment variables</span></span>
<span data-ttu-id="a88dc-177">Batch crea varias [variables de entorno][msdn_env_var] específicas de las tareas de múltiples instancias en los nodos de proceso asignados a una tarea de múltiples instancias.</span><span class="sxs-lookup"><span data-stu-id="a88dc-177">Batch creates several [environment variables][msdn_env_var] specific to multi-instance tasks on the compute nodes allocated to a multi-instance task.</span></span> <span data-ttu-id="a88dc-178">Las líneas de comando de coordinación y de la aplicación pueden hacer referencia a estas variables de entorno, como los scripts y programas que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="a88dc-178">Your coordination and application command lines can reference these environment variables, as can the scripts and programs they execute.</span></span>

<span data-ttu-id="a88dc-179">Las siguientes variables de entorno las crea el servicio Batch para su uso por las tareas de múltiples instancias:</span><span class="sxs-lookup"><span data-stu-id="a88dc-179">The following environment variables are created by the Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="a88dc-180">Para obtener detalles completos sobre estas y las demás variables de entorno del nodo de proceso de Batch, incluido su contenido y la visibilidad, consulte [Variables de entorno del nodo de proceso][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="a88dc-180">For full details on these and the other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="a88dc-181">El ejemplo de código de Linux MPI de Batch contiene un ejemplo de cómo se pueden usar varias de estas variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="a88dc-181">The Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="a88dc-182">El script de Batch [coordination-cmd][coord_cmd_example] descarga archivos de aplicación y entrada comunes desde Azure Storage, permite a un recurso compartido de Network File System (NFS) en el nodo maestro y configura los demás nodos asignados a la tarea de múltiples instancias, como clientes NFS.</span><span class="sxs-lookup"><span data-stu-id="a88dc-182">The [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on the master node, and configures the other nodes allocated to the multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="a88dc-183">Archivos de recursos</span><span class="sxs-lookup"><span data-stu-id="a88dc-183">Resource files</span></span>
<span data-ttu-id="a88dc-184">Hay dos conjuntos de archivos de recursos que se deben tener en cuenta para las tareas de múltiples instancias: **archivos de recursos comunes** que descargan *todas* las tareas (tanto principales como subtareas) y **archivos de recursos** especificados para la propia tarea de múltiples instancias, que descarga *solo la tarea principal*.</span><span class="sxs-lookup"><span data-stu-id="a88dc-184">There are two sets of resource files to consider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and the **resource files** specified for the multi-instance task itself, which *only the primary* task downloads.</span></span>

<span data-ttu-id="a88dc-185">Puede especificar uno o más **archivos de recursos comunes** en la configuración de instancias múltiples de una tarea.</span><span class="sxs-lookup"><span data-stu-id="a88dc-185">You can specify one or more **common resource files** in the multi-instance settings for a task.</span></span> <span data-ttu-id="a88dc-186">La tarea principal y todas las subtareas descargan estos archivos de recursos comunes desde el [Azure Storage](../storage/common/storage-introduction.md) en el **directorio compartido de tareas** de cada nodo.</span><span class="sxs-lookup"><span data-stu-id="a88dc-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by the primary and all subtasks.</span></span> <span data-ttu-id="a88dc-187">Puede tener acceso al directorio compartido de tareas desde las líneas de comandos de coordinación y aplicación mediante la variable de entorno `AZ_BATCH_TASK_SHARED_DIR` .</span><span class="sxs-lookup"><span data-stu-id="a88dc-187">You can access the task shared directory from application and coordination command lines by using the `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="a88dc-188">La ruta de acceso `AZ_BATCH_TASK_SHARED_DIR` es idéntica en todos los nodos asignados a la tarea de múltiples instancias, por lo que puede compartir un único comando de coordinación entre el principal y todas las subtareas.</span><span class="sxs-lookup"><span data-stu-id="a88dc-188">The `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated to the multi-instance task, thus you can share a single coordination command between the primary and all subtasks.</span></span> <span data-ttu-id="a88dc-189">Batch no "comparte" el directorio en un sentido de acceso remoto, pero puede usarlo como un montaje o punto de recurso compartido, tal como se mencionó anteriormente en la información sobre las variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="a88dc-189">Batch does not "share" the directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in the tip on environment variables.</span></span>

<span data-ttu-id="a88dc-190">Los archivos de recursos que especifique para la propia tarea de múltiples instancias se descargan en el directorio de trabajo de la tarea, `AZ_BATCH_TASK_WORKING_DIR`, de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a88dc-190">Resource files that you specify for the multi-instance task itself are downloaded to the task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="a88dc-191">Como se mencionó, a diferencia de los archivos de recursos comunes, solo la tarea principal descarga los archivos de recursos especificados para la propia tarea de múltiples instancias.</span><span class="sxs-lookup"><span data-stu-id="a88dc-191">As mentioned, in contrast to common resource files, only the primary task downloads resource files specified for the  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a88dc-192">Utilice siempre las variables de entorno `AZ_BATCH_TASK_SHARED_DIR` y `AZ_BATCH_TASK_WORKING_DIR` para hacer referencia a estos directorios en las líneas de comando.</span><span class="sxs-lookup"><span data-stu-id="a88dc-192">Always use the environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` to refer to these directories in your command lines.</span></span> <span data-ttu-id="a88dc-193">No intente construir las rutas de acceso manualmente.</span><span class="sxs-lookup"><span data-stu-id="a88dc-193">Do not attempt to construct the paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="a88dc-194">Duración de la tarea</span><span class="sxs-lookup"><span data-stu-id="a88dc-194">Task lifetime</span></span>
<span data-ttu-id="a88dc-195">La duración de la tarea principal controla la duración de toda la tarea de instancias múltiples.</span><span class="sxs-lookup"><span data-stu-id="a88dc-195">The lifetime of the primary task controls the lifetime of the entire multi-instance task.</span></span> <span data-ttu-id="a88dc-196">Cuando se cierra la tarea principal, todas las subtareas se terminan.</span><span class="sxs-lookup"><span data-stu-id="a88dc-196">When the primary exits, all of the subtasks are terminated.</span></span> <span data-ttu-id="a88dc-197">El código de salida de la tarea principal es el código de salida de la tarea y, por tanto, se utiliza para determinar el éxito o fracaso de la tarea con fines de reintento.</span><span class="sxs-lookup"><span data-stu-id="a88dc-197">The exit code of the primary is the exit code of the task, and is therefore used to determine the success or failure of the task for retry purposes.</span></span>

<span data-ttu-id="a88dc-198">Si se produce un error en alguna de las subtareas, por ejemplo, se cierra con un código de error distinto de cero, la tarea de instancias múltiples entera dará error.</span><span class="sxs-lookup"><span data-stu-id="a88dc-198">If any of the subtasks fail, exiting with a non-zero return code, for example, the entire multi-instance task fails.</span></span> <span data-ttu-id="a88dc-199">Entonces la tarea de instancias múltiples se termina y se reintenta, hasta su límite de reintento.</span><span class="sxs-lookup"><span data-stu-id="a88dc-199">The multi-instance task is then terminated and retried, up to its retry limit.</span></span>

<span data-ttu-id="a88dc-200">Cuando se elimina una tarea de instancias múltiples, el servicio Lote también elimina la tarea principal y todas las subtareas.</span><span class="sxs-lookup"><span data-stu-id="a88dc-200">When you delete a multi-instance task, the primary and all subtasks are also deleted by the Batch service.</span></span> <span data-ttu-id="a88dc-201">Todos los directorios de subtarea y sus archivos se eliminan de los nodos de proceso, igual que en el caso de una tarea estándar.</span><span class="sxs-lookup"><span data-stu-id="a88dc-201">All subtask directories and their files are deleted from the compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="a88dc-202">Los valores de [TaskConstraints][net_taskconstraints] para una tarea de instancias múltiples, como las propiedades [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock] y [RetentionTime][net_taskconstraint_retention], se respetan ya que son para una tarea estándar, y se aplican a la tarea principal y a todas las subtareas.</span><span class="sxs-lookup"><span data-stu-id="a88dc-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as the [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply to the primary and all subtasks.</span></span> <span data-ttu-id="a88dc-203">Sin embargo, si cambia la propiedad [RetentionTime][net_taskconstraint_retention] después de agregar la tarea de instancias múltiples al trabajo, este cambio solo se aplica a la tarea principal.</span><span class="sxs-lookup"><span data-stu-id="a88dc-203">However, if you change the [RetentionTime][net_taskconstraint_retention] property after adding the multi-instance task to the job, this change is applied only to the primary task.</span></span> <span data-ttu-id="a88dc-204">Todas las subtareas seguirán usando la propiedad [RetentionTime][net_taskconstraint_retention] original.</span><span class="sxs-lookup"><span data-stu-id="a88dc-204">All of the subtasks continue to use the original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="a88dc-205">La lista de tareas recientes de un nodo de proceso reflejará el identificador de una subtarea si la tarea reciente era parte de una tarea de instancias múltiples.</span><span class="sxs-lookup"><span data-stu-id="a88dc-205">A compute node's recent task list reflects the id of a subtask if the recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="a88dc-206">Obtención de información sobre las subtareas</span><span class="sxs-lookup"><span data-stu-id="a88dc-206">Obtain information about subtasks</span></span>
<span data-ttu-id="a88dc-207">Para obtener información sobre las subtareas mediante la biblioteca .NET de Batch, llame al método [CloudTask.ListSubtasks][net_task_listsubtasks].</span><span class="sxs-lookup"><span data-stu-id="a88dc-207">To obtain information on subtasks by using the Batch .NET library, call the [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="a88dc-208">Este método devuelve información sobre todas las subtareas e información sobre el nodo de proceso que ejecuta las tareas.</span><span class="sxs-lookup"><span data-stu-id="a88dc-208">This method returns information on all subtasks, and information about the compute node that executed the tasks.</span></span> <span data-ttu-id="a88dc-209">A partir de esta información, puede determinar el directorio raíz de cada subtarea, el identificador de grupo, su estado actual, el código de salida, etc.</span><span class="sxs-lookup"><span data-stu-id="a88dc-209">From this information, you can determine each subtask's root directory, the pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="a88dc-210">Esta información se puede utilizar en combinación con el método [PoolOperations.GetNodeFile][poolops_getnodefile] para obtener los archivos de la subtarea.</span><span class="sxs-lookup"><span data-stu-id="a88dc-210">You can use this information in combination with the [PoolOperations.GetNodeFile][poolops_getnodefile] method to obtain the subtask's files.</span></span> <span data-ttu-id="a88dc-211">Tenga en cuenta que este método no devuelve información de la tarea principal (id. 0).</span><span class="sxs-lookup"><span data-stu-id="a88dc-211">Note that this method does not return information for the primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="a88dc-212">A menos que se indique lo contrario, los métodos .NET de Batch que operan en la propia clase [CloudTask][net_task] de varias instancias, *solo* se aplican a la tarea principal.</span><span class="sxs-lookup"><span data-stu-id="a88dc-212">Unless otherwise stated, Batch .NET methods that operate on the multi-instance [CloudTask][net_task] itself apply *only* to the primary task.</span></span> <span data-ttu-id="a88dc-213">Por ejemplo, al llamar al método [CloudTask.ListNodeFiles][net_task_listnodefiles] en una tarea de instancias múltiples, solo se devuelven los archivos de la tarea principal.</span><span class="sxs-lookup"><span data-stu-id="a88dc-213">For example, when you call the [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only the primary task's files are returned.</span></span>
>
>

<span data-ttu-id="a88dc-214">El fragmento de código siguiente muestra cómo obtener información de la subtarea y cómo solicitar contenido de archivos de los nodos en los que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="a88dc-214">The following code snippet shows how to obtain subtask information, as well as request file contents from the nodes on which they executed.</span></span>

```csharp
// Obtain the job and the multi-instance task from the Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain the list of subtasks for the task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over the subtasks and print their stdout and stderr
// output if the subtask has completed
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

## <a name="code-sample"></a><span data-ttu-id="a88dc-215">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a88dc-215">Code sample</span></span>
<span data-ttu-id="a88dc-216">En el ejemplo de código [MultiInstanceTasks][github_mpi] que se encuentra en GitHub se muestra cómo puede usarse una tarea de instancias múltiples para ejecutar una aplicación de [MS-MPI][msmpi_msdn] en los nodos de proceso de Batch.</span><span class="sxs-lookup"><span data-stu-id="a88dc-216">The [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how to use a multi-instance task to run an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="a88dc-217">Siga los pasos que se describen en las secciones [Preparación](#preparation) y [Ejecución](#execution) para ejecutar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a88dc-217">Follow the steps in [Preparation](#preparation) and [Execution](#execution) to run the sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="a88dc-218">Preparación</span><span class="sxs-lookup"><span data-stu-id="a88dc-218">Preparation</span></span>
1. <span data-ttu-id="a88dc-219">Siga los dos primeros pasos que se indican en [Compilación y ejecución de un sencillo programa de MS-MPI][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="a88dc-219">Follow the first two steps in [How to compile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="a88dc-220">De este modo, cumplirá los requisitos necesarios para el siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="a88dc-220">This satisfies the prerequesites for the following step.</span></span>
2. <span data-ttu-id="a88dc-221">Compile una versión de *lanzamiento* del programa de ejemplo [MPIHelloWorld][helloworld_proj] de MPI.</span><span class="sxs-lookup"><span data-stu-id="a88dc-221">Build a *Release* version of the [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="a88dc-222">La tarea de instancias múltiples ejecutará este programa en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="a88dc-222">This is the program that will be run on compute nodes by the multi-instance task.</span></span>
3. <span data-ttu-id="a88dc-223">Cree un archivo zip que contenga `MPIHelloWorld.exe` (creado en el paso 2) y `MSMpiSetup.exe` (descargado en el paso 1).</span><span class="sxs-lookup"><span data-stu-id="a88dc-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="a88dc-224">En el siguiente paso, cargará este archivo zip como paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a88dc-224">You'll upload this zip file as an application package in the next step.</span></span>
4. <span data-ttu-id="a88dc-225">Use [Azure Portal][portal] para crear una [aplicación](batch-application-packages.md) de Batch llamada "MPIHelloWorld" y establezca el archivo zip que creó en el paso anterior como versión "1.0" del paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a88dc-225">Use the [Azure portal][portal] to create a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify the zip file you created in the previous step as version "1.0" of the application package.</span></span> <span data-ttu-id="a88dc-226">Para más información, consulte [Carga y administración de aplicaciones](batch-application-packages.md#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="a88dc-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="a88dc-227">Cree una versión de *lanzamiento* de `MPIHelloWorld.exe` para que no tenga que incluir otras dependencias (por ejemplo, `msvcp140d.dll` o `vcruntime140d.dll`) en el paquete de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a88dc-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have to include any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="a88dc-228">Ejecución</span><span class="sxs-lookup"><span data-stu-id="a88dc-228">Execution</span></span>
1. <span data-ttu-id="a88dc-229">Descargue [azure-batch-samples][github_samples_zip] de GitHub.</span><span class="sxs-lookup"><span data-stu-id="a88dc-229">Download the [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="a88dc-230">Abra la **solución** MultiInstanceTasks en Visual Studio 2015 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="a88dc-230">Open the MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="a88dc-231">El archivo de solución de `MultiInstanceTasks.sln` se encuentra en:</span><span class="sxs-lookup"><span data-stu-id="a88dc-231">The `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="a88dc-232">En el proyecto **Microsoft.Azure.Batch.Samples.Common**, especifique las credenciales de la cuenta de Batch y Storage en `AccountSettings.settings`.</span><span class="sxs-lookup"><span data-stu-id="a88dc-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in the **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="a88dc-233">**Compile y ejecute** la solución MultiInstanceTasks. De este modo, ejecutará la aplicación de ejemplo de MPI en los nodos de proceso de un grupo de Batch.</span><span class="sxs-lookup"><span data-stu-id="a88dc-233">**Build and run** the MultiInstanceTasks solution to execute the MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="a88dc-234">*Opcional*: puede usar [Azure Portal][portal] o el [explorador de Batch][batch_explorer] para examinar el grupo, el trabajo y la tarea de ejemplo ("MultiInstanceSamplePool", "MultiInstanceSampleJob" y "MultiInstanceSampleTask") antes de eliminar los recursos.</span><span class="sxs-lookup"><span data-stu-id="a88dc-234">*Optional*: Use the [Azure portal][portal] or the [Batch Explorer][batch_explorer] to examine the sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete the resources.</span></span>

> [!TIP]
> <span data-ttu-id="a88dc-235">Si no tiene Visual Studio, puede descargar gratis [Visual Studio Community][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="a88dc-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="a88dc-236">La salida de `MultiInstanceTasks.exe` será similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="a88dc-236">Output from `MultiInstanceTasks.exe` is similar to the following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] to job [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks to complete...

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

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="a88dc-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a88dc-237">Next steps</span></span>
* <span data-ttu-id="a88dc-238">En el blog Microsoft HPC & Azure Batch Team se trata sobre la [compatibilidad de MPI para Linux en Azure Batch][blog_mpi_linux], e incluye información sobre el uso de [OpenFOAM][openfoam] con Batch.</span><span class="sxs-lookup"><span data-stu-id="a88dc-238">The Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="a88dc-239">Puede encontrar ejemplos de código de Python para el [ejemplo de OpenFOAM en GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="a88dc-239">You can find Python code samples for the [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="a88dc-240">Aprenda a [crear grupos de nodos de proceso de Linux](batch-linux-nodes.md) para utilizarlos en soluciones de MPI con Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="a88dc-240">Learn how to [create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

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
