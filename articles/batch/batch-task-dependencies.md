---
title: "Uso de las dependencias de las tareas para ejecutar tareas en función de la finalización de otras tareas: Azure Batch | Microsoft Docs"
description: "Cree tareas que dependan de la finalización de otras para procesar grandes cargas de trabajo de macrodatos similares y de estilo MapReduce en Azure Batch."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 465306d2de8d1dbe6ba1f0cd74be720b78a50de3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-task-dependencies-to-run-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="4519f-103">Creación de dependencias de tareas para ejecutar las tareas que dependan de otras tareas</span><span class="sxs-lookup"><span data-stu-id="4519f-103">Create task dependencies to run tasks that depend on other tasks</span></span>

<span data-ttu-id="4519f-104">Puede definir dependencias de tareas para ejecutar una tarea o un conjunto de tareas solo después de que se haya completado una tarea principal.</span><span class="sxs-lookup"><span data-stu-id="4519f-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="4519f-105">A continuación se indican algunos escenarios donde las dependencias de tareas son útiles:</span><span class="sxs-lookup"><span data-stu-id="4519f-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="4519f-106">Cargas de trabajo del estilo MapReduce en la nube.</span><span class="sxs-lookup"><span data-stu-id="4519f-106">MapReduce-style workloads in the cloud.</span></span>
* <span data-ttu-id="4519f-107">Trabajos cuyas tareas de procesamiento de datos se pueden expresar como un gráfico acíclico dirigido (DAG).</span><span class="sxs-lookup"><span data-stu-id="4519f-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="4519f-108">Procesos anteriores y posteriores a la representación, donde cada tarea se debe completar para que pueda comenzar la siguiente tarea.</span><span class="sxs-lookup"><span data-stu-id="4519f-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span></span>
* <span data-ttu-id="4519f-109">Cualquier otro trabajo en el que las tareas que siguen en la cadena dependen de las tareas que preceden en la cadena.</span><span class="sxs-lookup"><span data-stu-id="4519f-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span></span>

<span data-ttu-id="4519f-110">Con dependencias de la tarea de Batch, puede crear tareas que estén programadas para su ejecución en los nodos de proceso después de la finalización de una o varias tareas.</span><span class="sxs-lookup"><span data-stu-id="4519f-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span></span> <span data-ttu-id="4519f-111">Por ejemplo, puede crear un trabajo que represente cada fotograma de una película 3D con una tarea independiente y paralela.</span><span class="sxs-lookup"><span data-stu-id="4519f-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="4519f-112">La última tarea (la "tarea de combinación") no combina los fotogramas representados para crear la película completa hasta que todos los fotogramas se hayan representado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4519f-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="4519f-113">De forma predeterminada, las tareas dependientes están programadas para ejecutarse solo después de que la tarea principal se haya completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4519f-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span></span> <span data-ttu-id="4519f-114">Puede especificar una acción de dependencia para invalidar el comportamiento predeterminado y ejecutar tareas cuando se produce un error en la tarea principal.</span><span class="sxs-lookup"><span data-stu-id="4519f-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span></span> <span data-ttu-id="4519f-115">Consulte la sección [Acciones de dependencia](#dependency-actions) para más información.</span><span class="sxs-lookup"><span data-stu-id="4519f-115">See the [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="4519f-116">Puede crear tareas que dependan de otras en una relación de una a una o una a varias.</span><span class="sxs-lookup"><span data-stu-id="4519f-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="4519f-117">También puede crear una dependencia de intervalo, en la que una tarea depende de la finalización de un grupo de tareas dentro de un intervalo especificado de identificadores de tarea.</span><span class="sxs-lookup"><span data-stu-id="4519f-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="4519f-118">Puede combinar estos tres escenarios básicos para crear relaciones de varios a varios.</span><span class="sxs-lookup"><span data-stu-id="4519f-118">You can combine these three basic scenarios to create many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="4519f-119">Dependencias de tareas con Lote de .NET</span><span class="sxs-lookup"><span data-stu-id="4519f-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="4519f-120">En este artículo se describe cómo configurar las dependencias de tareas mediante la biblioteca de [.NET para Batch][net_msdn].</span><span class="sxs-lookup"><span data-stu-id="4519f-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="4519f-121">Primero le mostraremos cómo [habilitar la dependencia de tareas](#enable-task-dependencies) en sus trabajos y, después, le demostraremos cómo [configurar una tarea con dependencias](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="4519f-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="4519f-122">También se describe cómo especificar una acción de dependencia para ejecutar tareas dependientes, si se produce un error en la principal.</span><span class="sxs-lookup"><span data-stu-id="4519f-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span></span> <span data-ttu-id="4519f-123">Por último, se tratarán los [escenarios de dependencia](#dependency-scenarios) compatibles con Lote.</span><span class="sxs-lookup"><span data-stu-id="4519f-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="4519f-124">Habilitación de dependencias de tareas</span><span class="sxs-lookup"><span data-stu-id="4519f-124">Enable task dependencies</span></span>
<span data-ttu-id="4519f-125">Para utilizar la dependencia de tareas en la aplicación Batch, antes es preciso configurar el trabajo para usar dependencias de tareas.</span><span class="sxs-lookup"><span data-stu-id="4519f-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span></span> <span data-ttu-id="4519f-126">En .NET para Batch, habilítelo en [CloudJob][net_cloudjob] estableciendo su propiedad [UsesTaskDependencies][net_usestaskdependencies] en `true`:</span><span class="sxs-lookup"><span data-stu-id="4519f-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="4519f-127">En el fragmento de código anterior, "batchClient" es una instancia de la clase [BatchClient][net_batchclient].</span><span class="sxs-lookup"><span data-stu-id="4519f-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="4519f-128">Creación de tareas dependientes</span><span class="sxs-lookup"><span data-stu-id="4519f-128">Create dependent tasks</span></span>
<span data-ttu-id="4519f-129">Para crear una tarea que dependa de la finalización de una o varias tareas, puede especificar que la tarea "dependa" de las otras tareas.</span><span class="sxs-lookup"><span data-stu-id="4519f-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span></span> <span data-ttu-id="4519f-130">En .NET para Batch, configure la propiedad [CloudTask][net_cloudtask].[DependsOn][net_dependson] con una instancia de la clase [TaskDependencies][net_taskdependencies]:</span><span class="sxs-lookup"><span data-stu-id="4519f-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="4519f-131">Este fragmento de código crea una tarea dependiente con el identificador de tarea "Flowers".</span><span class="sxs-lookup"><span data-stu-id="4519f-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="4519f-132">La tarea "Flowers" depende de las tareas "Rain" y "Sun".</span><span class="sxs-lookup"><span data-stu-id="4519f-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="4519f-133">La tarea "Flowers" se programará para que se ejecute en un nodo de proceso solo después de las tareas "Rain" y "Sun" se hayan completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4519f-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="4519f-134">Se considera que una tarea se ha completado correctamente cuando se encuentra en estado de **completada** y su **código de salida** es `0`.</span><span class="sxs-lookup"><span data-stu-id="4519f-134">A task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="4519f-135">En .NET para Batch, esto significa que el valor de la propiedad [CloudTask][net_cloudtask].[State ][net_taskstate] es `Completed` y el valor de la propiedad [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] de CloudTask es `0`.</span><span class="sxs-lookup"><span data-stu-id="4519f-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="4519f-136">escenarios de dependencia</span><span class="sxs-lookup"><span data-stu-id="4519f-136">Dependency scenarios</span></span>
<span data-ttu-id="4519f-137">Hay tres escenarios de dependencia de tareas básicos que puede usar en Lote de Azure: uno a uno, uno a varios y la dependencia de intervalo de identificadores de tarea.</span><span class="sxs-lookup"><span data-stu-id="4519f-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="4519f-138">Estos se pueden combinar para proporcionar un cuarto escenario, varios a varios.</span><span class="sxs-lookup"><span data-stu-id="4519f-138">These can be combined to provide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="4519f-139">Escenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="4519f-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="4519f-140">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4519f-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="4519f-141">Uno a uno</span><span class="sxs-lookup"><span data-stu-id="4519f-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="4519f-142">*taskB* depende de *taskA*</span><span class="sxs-lookup"><span data-stu-id="4519f-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="4519f-143">Se programará que *taskB* no se ejecute hasta que *taskA* se haya completado correctamente</span><span class="sxs-lookup"><span data-stu-id="4519f-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="4519f-144">![Diagrama: dependencia de la tarea uno a uno][1]</span><span class="sxs-lookup"><span data-stu-id="4519f-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="4519f-145">Uno a varios</span><span class="sxs-lookup"><span data-stu-id="4519f-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="4519f-146">*taskC* depende de*taskA* y *taskB*.</span><span class="sxs-lookup"><span data-stu-id="4519f-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="4519f-147">Se programará que *taskC* no se ejecute hasta que *taskA* y *taskB* se hayan completado correctamente</span><span class="sxs-lookup"><span data-stu-id="4519f-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="4519f-148">![Diagrama: dependencia de la tarea uno a varios][2]</span><span class="sxs-lookup"><span data-stu-id="4519f-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="4519f-149">Intervalo de id. de tarea</span><span class="sxs-lookup"><span data-stu-id="4519f-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="4519f-150">*taskD* depende de una serie de tareas</span><span class="sxs-lookup"><span data-stu-id="4519f-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="4519f-151">Se programará que *taskD* no se ejecute hasta que las tareas con los identificadores del *1* al *10* se hayan completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4519f-151">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="4519f-152">![Diagrama: dependencia de intervalo de id. de tarea][3]</span><span class="sxs-lookup"><span data-stu-id="4519f-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="4519f-153">Puede crear relaciones de **varios a varios**, por ejemplo, donde las tareas C, D, E y F dependan de las tareas A y B. Esto es útil, por ejemplo, en escenarios de preprocesamiento en paralelo donde las tareas que siguen en la cadena dependen de la salida de varias tareas que preceden en la cadena.</span><span class="sxs-lookup"><span data-stu-id="4519f-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="4519f-154">En los ejemplos de esta sección, una tarea dependiente solo se ejecuta después de que las tareas principales se completen correctamente.</span><span class="sxs-lookup"><span data-stu-id="4519f-154">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span></span> <span data-ttu-id="4519f-155">Este comportamiento es el comportamiento predeterminado para una tarea dependiente.</span><span class="sxs-lookup"><span data-stu-id="4519f-155">This behavior is the default behavior for a dependent task.</span></span> <span data-ttu-id="4519f-156">Puede ejecutar una tarea dependiente después de que se produzca un error en una tarea principal especificando una acción de dependencia para invalidar el comportamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="4519f-156">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span></span> <span data-ttu-id="4519f-157">Consulte la sección [Acciones de dependencia](#dependency-actions) para más información.</span><span class="sxs-lookup"><span data-stu-id="4519f-157">See the [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="4519f-158">Uno a uno</span><span class="sxs-lookup"><span data-stu-id="4519f-158">One-to-one</span></span>
<span data-ttu-id="4519f-159">En una relación uno a uno, una tarea depende de la finalización correcta de una tarea principal.</span><span class="sxs-lookup"><span data-stu-id="4519f-159">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span></span> <span data-ttu-id="4519f-160">Para crear la dependencia, proporcione un identificador de tarea único al método estático [TaskDependencies][net_taskdependencies].[OnId][net_onid] cuando rellene la propiedad [DependsOn][net_dependson] de [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="4519f-160">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="4519f-161">Uno a varios</span><span class="sxs-lookup"><span data-stu-id="4519f-161">One-to-many</span></span>
<span data-ttu-id="4519f-162">En una relación uno a muchos, una tarea depende de la finalización correcta de varias tareas principales.</span><span class="sxs-lookup"><span data-stu-id="4519f-162">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span></span> <span data-ttu-id="4519f-163">Para crear la dependencia, proporcione una colección de identificadores de tarea al método estático [TaskDependencies][net_taskdependencies].[OnIds][net_onids] cuando rellene la propiedad [DependsOn][net_dependson] de [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="4519f-163">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="4519f-164">Intervalo de id. de tarea</span><span class="sxs-lookup"><span data-stu-id="4519f-164">Task ID range</span></span>
<span data-ttu-id="4519f-165">En un dependencia de un intervalo de tareas principales, una tarea depende de la finalización de tareas cuyos identificadores se encuentran dentro de un intervalo.</span><span class="sxs-lookup"><span data-stu-id="4519f-165">In a dependency on a range of parent tasks, a task depends on the the completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="4519f-166">Para crear la dependencia, proporcione el primer y el último identificador de tarea del intervalo al método estático [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] cuando rellene la propiedad [DependsOn][net_dependson] de [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="4519f-166">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4519f-167">Si usa intervalos de identificadores de tarea para las dependencias, dichos identificadores *deben* ser representaciones de cadena de valores enteros.</span><span class="sxs-lookup"><span data-stu-id="4519f-167">When you use task ID ranges for your dependencies, the task IDs in the range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="4519f-168">Todas las tareas del intervalo deben satisfacer la dependencia, ya sea completando correctamente o con un error lo que se asigna a una acción de dependencia establecida en **Satisfacer**.</span><span class="sxs-lookup"><span data-stu-id="4519f-168">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span></span> <span data-ttu-id="4519f-169">Consulte la sección [Acciones de dependencia](#dependency-actions) para más información.</span><span class="sxs-lookup"><span data-stu-id="4519f-169">See the [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // To use a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters to TaskIdRange,
    // but their ids (above) are string representations of the ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="4519f-170">Acciones de dependencia</span><span class="sxs-lookup"><span data-stu-id="4519f-170">Dependency actions</span></span>

<span data-ttu-id="4519f-171">De forma predeterminada, una tarea dependiente o un conjunto de tareas se ejecuta solo después de que una tarea principal se haya completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4519f-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="4519f-172">En algunos escenarios, puede que desee ejecutar tareas dependientes incluso si se produce un error en la tarea principal.</span><span class="sxs-lookup"><span data-stu-id="4519f-172">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span></span> <span data-ttu-id="4519f-173">Puede invalidar el comportamiento predeterminado especificando una acción de dependencia.</span><span class="sxs-lookup"><span data-stu-id="4519f-173">You can override the default behavior by specifying a dependency action.</span></span> <span data-ttu-id="4519f-174">Una acción de dependencia especifica si una tarea dependiente es apta para ejecutarse, según el éxito o fracaso de la tarea principal.</span><span class="sxs-lookup"><span data-stu-id="4519f-174">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span></span> 

<span data-ttu-id="4519f-175">Por ejemplo, suponga que una tarea dependiente está esperando los datos de la finalización de la tarea de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="4519f-175">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span></span> <span data-ttu-id="4519f-176">Si se produce un error en la tarea de nivel superior, la tarea dependiente aún puede ejecutarse con datos más antiguos.</span><span class="sxs-lookup"><span data-stu-id="4519f-176">If the upstream task fails, the dependent task may still be able to run using older data.</span></span> <span data-ttu-id="4519f-177">En este caso, una acción de dependencia puede especificar que la tarea dependiente es apta para ejecutarse a pesar del error de la tarea principal.</span><span class="sxs-lookup"><span data-stu-id="4519f-177">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span></span>

<span data-ttu-id="4519f-178">Una acción de dependencia se basa en una condición de salida para la tarea principal.</span><span class="sxs-lookup"><span data-stu-id="4519f-178">A dependency action is based on an exit condition for the parent task.</span></span> <span data-ttu-id="4519f-179">Puede especificar una acción de dependencia para cualquiera de las siguientes condiciones de salida; para. NET, consulte la clase [ExitConditions][net_exitconditions] para obtener detalles:</span><span class="sxs-lookup"><span data-stu-id="4519f-179">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="4519f-180">Cuando se produce un error de procesamiento previo.</span><span class="sxs-lookup"><span data-stu-id="4519f-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="4519f-181">Cuando se produce un error de carga de archivo.</span><span class="sxs-lookup"><span data-stu-id="4519f-181">When a file upload error occurs.</span></span> <span data-ttu-id="4519f-182">Si la tarea finaliza con un código de salida que se especificó mediante **exitCodes** o **exitCodeRanges** y, a continuación, encuentra un error de carga de archivo, la acción especificada por el código de salida tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="4519f-182">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span></span>
- <span data-ttu-id="4519f-183">Cuando la tarea finaliza con un código de salida definido por la propiedad **ExitCodes**.</span><span class="sxs-lookup"><span data-stu-id="4519f-183">When the task exits with an exit code defined by the **ExitCodes** property.</span></span>
- <span data-ttu-id="4519f-184">Cuando la tarea finaliza con un código de salida con error dentro de un intervalo especificado por la propiedad **ExitCodeRanges**.</span><span class="sxs-lookup"><span data-stu-id="4519f-184">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="4519f-185">El caso predeterminado, si la tarea finaliza con un código de salida no definido en **ExitCodes** o **ExitCodeRanges**, o si la tarea finaliza con un error de procesamiento previo y no se ha establecido la propiedad **PreProcessingError**, o si se produce un error de carga de archivo en la tarea y no se ha establecido la propiedad **FileUploadError**.</span><span class="sxs-lookup"><span data-stu-id="4519f-185">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="4519f-186">Para especificar una acción de dependencia en. NET, establezca la propiedad [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] para la condición de salida.</span><span class="sxs-lookup"><span data-stu-id="4519f-186">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span></span> <span data-ttu-id="4519f-187">La propiedad **DependencyAction** toma uno de dos valores:</span><span class="sxs-lookup"><span data-stu-id="4519f-187">The **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="4519f-188">El establecimiento de la propiedad **DependencyAction** en **Satisfacer** indica que las tareas dependientes son aptas para ejecutarse si la tarea principal sale con un error especificado.</span><span class="sxs-lookup"><span data-stu-id="4519f-188">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span></span>
- <span data-ttu-id="4519f-189">El establecimiento de la propiedad **DependencyAction** en **Bloquear** indica que las tareas dependientes no son aptas para ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="4519f-189">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span></span>

<span data-ttu-id="4519f-190">La configuración predeterminada para la propiedad **DependencyAction** es **Satisfacer** para el código de salida 0, y **Bloquear** para todas las demás condiciones de salida.</span><span class="sxs-lookup"><span data-stu-id="4519f-190">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="4519f-191">El fragmento de código siguiente establece la propiedad **DependencyAction** para una tarea principal.</span><span class="sxs-lookup"><span data-stu-id="4519f-191">The following code snippet sets the **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="4519f-192">Si la tarea principal finaliza con un error de procesamiento previo o con los códigos de error especificados, la tarea dependiente se bloquea.</span><span class="sxs-lookup"><span data-stu-id="4519f-192">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span></span> <span data-ttu-id="4519f-193">Si la tarea principal sale con cualquier otro error distinto de cero, la tarea dependiente es apta para ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="4519f-193">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span></span>

```csharp
// Task A is the parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with the specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible to run 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible to run depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="4519f-194">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4519f-194">Code sample</span></span>
<span data-ttu-id="4519f-195">El proyecto de ejemplo [TaskDependencies][github_taskdependencies] es uno de los ejemplos de código de [Azure Batch][github_samples] de GitHub.</span><span class="sxs-lookup"><span data-stu-id="4519f-195">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="4519f-196">Esta solución de Visual Studio muestra:</span><span class="sxs-lookup"><span data-stu-id="4519f-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="4519f-197">Cómo habilitar la dependencia de tareas en un trabajo</span><span class="sxs-lookup"><span data-stu-id="4519f-197">How to enable task dependency on a job</span></span>
- <span data-ttu-id="4519f-198">Cómo crear tareas que dependen de otras tareas</span><span class="sxs-lookup"><span data-stu-id="4519f-198">How to create tasks that depend on other tasks</span></span>
- <span data-ttu-id="4519f-199">Cómo ejecutar las tareas en un grupo de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="4519f-199">How to execute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4519f-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4519f-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="4519f-201">Implementación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4519f-201">Application deployment</span></span>
<span data-ttu-id="4519f-202">La característica [paquetes de aplicación](batch-application-packages.md) de Lote proporciona una manera sencilla de implementar y de cambiar la versión de las aplicaciones que las tareas ejecutan en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="4519f-202">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="4519f-203">Instalación de aplicaciones y datos de ensayo</span><span class="sxs-lookup"><span data-stu-id="4519f-203">Installing applications and staging data</span></span>
<span data-ttu-id="4519f-204">Consulte [Installing applications and staging data on Batch compute nodes][forum_post] (Instalación de aplicaciones y datos de ensayo en nodos de proceso de Batch) en el foro de Azure Batch para ver la información general sobre los métodos de preparación de los nodos para ejecutar tareas.</span><span class="sxs-lookup"><span data-stu-id="4519f-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span></span> <span data-ttu-id="4519f-205">Este artículo, escrito por uno de los miembros del equipo de Azure Batch, es una buena toma de contacto sobre las diferentes maneras de copiar aplicaciones, datos de entrada de tareas y otros archivos en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="4519f-205">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

<span data-ttu-id="4519f-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagrama: dependencia uno a uno"</span><span class="sxs-lookup"><span data-stu-id="4519f-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: one-to-one dependency"</span></span>
<span data-ttu-id="4519f-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagrama: dependencia uno a varios"</span><span class="sxs-lookup"><span data-stu-id="4519f-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: one-to-many dependency"</span></span>
<span data-ttu-id="4519f-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagrama: dependencia de intervalo de id. de tarea"</span><span class="sxs-lookup"><span data-stu-id="4519f-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: task id range dependency"</span></span>
