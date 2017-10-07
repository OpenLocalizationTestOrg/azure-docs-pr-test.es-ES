---
title: "tareas de toorun de dependencias de tarea aaaUse se basan en la realización de Hola de otras tareas - Azure Batch | Documentos de Microsoft"
description: "Crear tareas que dependen de finalización de Hola de otras tareas para procesar estilo MapReduce y grandes cantidades de datos similar cargas de trabajo en el lote de Azure."
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
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="a42c1-103">Crear tareas de toorun que dependen de otras tareas de las dependencias entre tareas</span><span class="sxs-lookup"><span data-stu-id="a42c1-103">Create task dependencies toorun tasks that depend on other tasks</span></span>

<span data-ttu-id="a42c1-104">Puede definir tareas dependencias toorun una tarea o un conjunto de tareas solo después de que se ha completado una tarea primaria.</span><span class="sxs-lookup"><span data-stu-id="a42c1-104">You can define task dependencies toorun a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="a42c1-105">A continuación se indican algunos escenarios donde las dependencias de tareas son útiles:</span><span class="sxs-lookup"><span data-stu-id="a42c1-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="a42c1-106">Cargas de trabajo de estilo MapReduce en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a42c1-106">MapReduce-style workloads in hello cloud.</span></span>
* <span data-ttu-id="a42c1-107">Trabajos cuyas tareas de procesamiento de datos se pueden expresar como un gráfico acíclico dirigido (DAG).</span><span class="sxs-lookup"><span data-stu-id="a42c1-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="a42c1-108">Procesos de representación anterior y posterior a la representación, donde cada tarea debe completar para poder iniciar la tarea siguiente de hello.</span><span class="sxs-lookup"><span data-stu-id="a42c1-108">Pre-rendering and post-rendering processes, where each task must complete before hello next task can begin.</span></span>
* <span data-ttu-id="a42c1-109">Cualquier otro trabajo en la que dependen de tareas de nivel inferiores en la salida de hello de tareas de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="a42c1-109">Any other job in which downstream tasks depend on hello output of upstream tasks.</span></span>

<span data-ttu-id="a42c1-110">Con las dependencias de tareas de lote, puede crear tareas que están programadas para ejecutarse en nodos de proceso después de finalizar las tareas primarias de uno o más Hola.</span><span class="sxs-lookup"><span data-stu-id="a42c1-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after hello completion of one or more parent tasks.</span></span> <span data-ttu-id="a42c1-111">Por ejemplo, puede crear un trabajo que represente cada fotograma de una película 3D con una tarea independiente y paralela.</span><span class="sxs-lookup"><span data-stu-id="a42c1-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="a42c1-112">tarea final de Hello: Hola "tarea de mezcla--" hello representa fotogramas en hello toda la película sólo después de que todos los marcos de combinaciones se han correctamente representado.</span><span class="sxs-lookup"><span data-stu-id="a42c1-112">hello final task--hello "merge task"--merges hello rendered frames into hello complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="a42c1-113">De forma predeterminada, las tareas dependientes están programadas para ejecutarse solo después de hello primario tarea se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="a42c1-113">By default, dependent tasks are scheduled for execution only after hello parent task has completed successfully.</span></span> <span data-ttu-id="a42c1-114">Puede especificar un comportamiento predeterminado de dependencia acción toooverride hello y ejecutar tareas cuando se produce un error en la tarea primaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="a42c1-114">You can specify a dependency action toooverride hello default behavior and run tasks when hello parent task fails.</span></span> <span data-ttu-id="a42c1-115">Vea hello [acciones de dependencia](#dependency-actions) sección para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a42c1-115">See hello [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="a42c1-116">Puede crear tareas que dependan de otras en una relación de una a una o una a varias.</span><span class="sxs-lookup"><span data-stu-id="a42c1-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="a42c1-117">También puede crear una dependencia de intervalo que depende una tarea en la realización de Hola de un grupo de tareas dentro de un intervalo de Id. de tarea especificado.</span><span class="sxs-lookup"><span data-stu-id="a42c1-117">You can also create a range dependency where a task depends on hello completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="a42c1-118">Puede combinar estas relaciones de varios a varios de tres escenarios básicos toocreate.</span><span class="sxs-lookup"><span data-stu-id="a42c1-118">You can combine these three basic scenarios toocreate many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="a42c1-119">Dependencias de tareas con Lote de .NET</span><span class="sxs-lookup"><span data-stu-id="a42c1-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="a42c1-120">En este artículo se describe cómo tooconfigure las dependencias de tareas mediante el uso de Hola [.NET de lotes] [ net_msdn] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="a42c1-120">In this article, we discuss how tooconfigure task dependencies by using hello [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="a42c1-121">En primer lugar le mostraremos cómo demasiado[habilitar la dependencia de la tarea](#enable-task-dependencies) en los trabajos y, a continuación, se muestra cómo demasiado[configurar una tarea con dependencias](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="a42c1-121">We first show you how too[enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how too[configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="a42c1-122">También se describe cómo toospecify una dependencia acción toorun tareas dependientes si primario Hola se produce un error.</span><span class="sxs-lookup"><span data-stu-id="a42c1-122">We also describe how toospecify a dependency action toorun dependent tasks if hello parent fails.</span></span> <span data-ttu-id="a42c1-123">Por último, analizamos hello [escenarios de dependencia](#dependency-scenarios) admitido por lote.</span><span class="sxs-lookup"><span data-stu-id="a42c1-123">Finally, we discuss hello [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="a42c1-124">Habilitación de dependencias de tareas</span><span class="sxs-lookup"><span data-stu-id="a42c1-124">Enable task dependencies</span></span>
<span data-ttu-id="a42c1-125">toouse las dependencias de tareas en la aplicación de lote, primero debe configurar las dependencias de tareas de hello trabajo toouse.</span><span class="sxs-lookup"><span data-stu-id="a42c1-125">toouse task dependencies in your Batch application, you must first configure hello job toouse task dependencies.</span></span> <span data-ttu-id="a42c1-126">En .NET de lote, habilitarla en su [CloudJob] [ net_cloudjob] estableciendo su [UsesTaskDependencies] [ net_usestaskdependencies] propiedad demasiado`true`:</span><span class="sxs-lookup"><span data-stu-id="a42c1-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property too`true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="a42c1-127">Hola anterior fragmento de código, "batchClient" es una instancia de hello [BatchClient] [ net_batchclient] clase.</span><span class="sxs-lookup"><span data-stu-id="a42c1-127">In hello preceding code snippet, "batchClient" is an instance of hello [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="a42c1-128">Creación de tareas dependientes</span><span class="sxs-lookup"><span data-stu-id="a42c1-128">Create dependent tasks</span></span>
<span data-ttu-id="a42c1-129">toocreate una tarea que depende de una o varias tareas de elemento primario de finalización de hello, puede especificar que Hola tarea "depende" hello otras tareas.</span><span class="sxs-lookup"><span data-stu-id="a42c1-129">toocreate a task that depends on hello completion of one or more parent tasks, you can specify that hello task "depends on" hello other tasks.</span></span> <span data-ttu-id="a42c1-130">En .NET de lote, configurar hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] propiedad con una instancia de hello [TaskDependencies] [ net_taskdependencies] clase:</span><span class="sxs-lookup"><span data-stu-id="a42c1-130">In Batch .NET, configure hello [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of hello [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="a42c1-131">Este fragmento de código crea una tarea dependiente con el identificador de tarea "Flowers".</span><span class="sxs-lookup"><span data-stu-id="a42c1-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="a42c1-132">Hello "Flores" tarea depende de las tareas "Raicilla" y "Sun".</span><span class="sxs-lookup"><span data-stu-id="a42c1-132">hello "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="a42c1-133">Tarea "Flores" estará toorun programada en un nodo de proceso solo después de las tareas "Raicilla" y "Sun" se han completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="a42c1-133">Task "Flowers" will be scheduled toorun on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="a42c1-134">Una tarea se considera toobe completó correctamente cuando se encuentra en hello **completado** estado y su **código de salida** es `0`.</span><span class="sxs-lookup"><span data-stu-id="a42c1-134">A task is considered toobe completed successfully when it is in hello **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="a42c1-135">En .NET de lotes, esto significa un [CloudTask][net_cloudtask].[ Estado] [ net_taskstate] valor de propiedad de `Completed` y Hola del CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] es el valor de la propiedad `0`.</span><span class="sxs-lookup"><span data-stu-id="a42c1-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and hello CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="a42c1-136">escenarios de dependencia</span><span class="sxs-lookup"><span data-stu-id="a42c1-136">Dependency scenarios</span></span>
<span data-ttu-id="a42c1-137">Hay tres escenarios de dependencia de tareas básicos que puede usar en Lote de Azure: uno a uno, uno a varios y la dependencia de intervalo de identificadores de tarea.</span><span class="sxs-lookup"><span data-stu-id="a42c1-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="a42c1-138">Puede tratarse de combinado tooprovide un cuarto escenario, varios a varios.</span><span class="sxs-lookup"><span data-stu-id="a42c1-138">These can be combined tooprovide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="a42c1-139">Escenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="a42c1-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="a42c1-140">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a42c1-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="a42c1-141">Uno a uno</span><span class="sxs-lookup"><span data-stu-id="a42c1-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="a42c1-142">*taskB* depende de *taskA*</span><span class="sxs-lookup"><span data-stu-id="a42c1-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="a42c1-143">Se programará que *taskB* no se ejecute hasta que *taskA* se haya completado correctamente</span><span class="sxs-lookup"><span data-stu-id="a42c1-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="a42c1-144">![Diagrama: dependencia de la tarea uno a uno][1]</span><span class="sxs-lookup"><span data-stu-id="a42c1-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="a42c1-145">Uno a varios</span><span class="sxs-lookup"><span data-stu-id="a42c1-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="a42c1-146">*taskC* depende de*taskA* y *taskB*.</span><span class="sxs-lookup"><span data-stu-id="a42c1-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="a42c1-147">Se programará que *taskC* no se ejecute hasta que *taskA* y *taskB* se hayan completado correctamente</span><span class="sxs-lookup"><span data-stu-id="a42c1-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="a42c1-148">![Diagrama: dependencia de la tarea uno a varios][2]</span><span class="sxs-lookup"><span data-stu-id="a42c1-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="a42c1-149">Intervalo de id. de tarea</span><span class="sxs-lookup"><span data-stu-id="a42c1-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="a42c1-150">*taskD* depende de una serie de tareas</span><span class="sxs-lookup"><span data-stu-id="a42c1-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="a42c1-151">*taskD* no se programará para su ejecución hasta que las tareas de hello con identificadores *1* a través de *10* se han completado correctamente</span><span class="sxs-lookup"><span data-stu-id="a42c1-151">*taskD* will not be scheduled for execution until hello tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="a42c1-152">![Diagrama: dependencia de intervalo de id. de tarea][3]</span><span class="sxs-lookup"><span data-stu-id="a42c1-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="a42c1-153">Puede crear **-to-many** relaciones, como donde tareas C, D, E y F cada dependen de las tareas A y B. Esto es útil, por ejemplo, en escenarios de procesamiento paralelo que dependen de las tareas de nivel inferiores en la salida de hello de varias tareas de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="a42c1-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on hello output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="a42c1-154">En los ejemplos de hello en esta sección, se ejecuta una tarea dependiente solo después de que las tareas primarias de Hola se completan correctamente.</span><span class="sxs-lookup"><span data-stu-id="a42c1-154">In hello examples in this section, a dependent task runs only after hello parent tasks complete successfully.</span></span> <span data-ttu-id="a42c1-155">Este comportamiento es el comportamiento predeterminado de Hola para una tarea dependiente.</span><span class="sxs-lookup"><span data-stu-id="a42c1-155">This behavior is hello default behavior for a dependent task.</span></span> <span data-ttu-id="a42c1-156">Puede ejecutar una tarea dependiente después de que se produce un error en una tarea primaria especificando un comportamiento predeterminado de dependencia acción toooverride Hola.</span><span class="sxs-lookup"><span data-stu-id="a42c1-156">You can run a dependent task after a parent task fails by specifying a dependency action toooverride hello default behavior.</span></span> <span data-ttu-id="a42c1-157">Vea hello [acciones de dependencia](#dependency-actions) sección para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a42c1-157">See hello [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="a42c1-158">Uno a uno</span><span class="sxs-lookup"><span data-stu-id="a42c1-158">One-to-one</span></span>
<span data-ttu-id="a42c1-159">En una relación uno a uno, una tarea depende de la finalización correcta de Hola de tarea de un elemento primario.</span><span class="sxs-lookup"><span data-stu-id="a42c1-159">In a one-to-one relationship, a task depends on hello successful completion of one parent task.</span></span> <span data-ttu-id="a42c1-160">toocreate Hola dependencia, proporcione un toohello de Id. de tarea única [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] método estático al rellenar hello [DependsOn] [ net_dependson] propiedad de [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="a42c1-160">toocreate hello dependency, provide a single task ID toohello [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="a42c1-161">Uno a varios</span><span class="sxs-lookup"><span data-stu-id="a42c1-161">One-to-many</span></span>
<span data-ttu-id="a42c1-162">En una relación uno a varios, una tarea depende de finalización de Hola de varias tareas de elemento primario.</span><span class="sxs-lookup"><span data-stu-id="a42c1-162">In a one-to-many relationship, a task depends on hello completion of multiple parent tasks.</span></span> <span data-ttu-id="a42c1-163">toocreate Hola dependencia, proporcionar una serie de tareas identificadores toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] método estático al rellenar hello [DependsOn] [ net_dependson] propiedad de [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="a42c1-163">toocreate hello dependency, provide a collection of task IDs toohello [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

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

### <a name="task-id-range"></a><span data-ttu-id="a42c1-164">Intervalo de id. de tarea</span><span class="sxs-lookup"><span data-stu-id="a42c1-164">Task ID range</span></span>
<span data-ttu-id="a42c1-165">Una dependencia en un intervalo de las tareas primarias, una tarea depende de la finalización de Hola de Hola de tareas cuyos identificadores se encuentran dentro de un intervalo.</span><span class="sxs-lookup"><span data-stu-id="a42c1-165">In a dependency on a range of parent tasks, a task depends on hello hello completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="a42c1-166">dependencia de hello toocreate, proporcionar hello en primer lugar y última tarea con identificadores de hello intervalo toohello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] método estático al rellenar hello [DependsOn] [ net_dependson] propiedad de [CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="a42c1-166">toocreate hello dependency, provide hello first and last task IDs in hello range toohello [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a42c1-167">Cuando utiliza intervalos de Id. de tarea para sus dependencias, Hola identificadores de tarea en el intervalo de hello *debe* ser representaciones de cadena de valores enteros.</span><span class="sxs-lookup"><span data-stu-id="a42c1-167">When you use task ID ranges for your dependencies, hello task IDs in hello range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="a42c1-168">Cada tarea en el intervalo de hello debe satisfacer dependencia hello, completando correctamente o completando con un error de acción de la dependencia de tooa asignado establecida demasiado**satisfacción**.</span><span class="sxs-lookup"><span data-stu-id="a42c1-168">Every task in hello range must satisfy hello dependency, either by completing successfully or by completing with a failure that’s mapped tooa dependency action set too**Satisfy**.</span></span> <span data-ttu-id="a42c1-169">Vea hello [acciones de dependencia](#dependency-actions) sección para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a42c1-169">See hello [Dependency actions](#dependency-actions) section for details.</span></span>
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
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="a42c1-170">Acciones de dependencia</span><span class="sxs-lookup"><span data-stu-id="a42c1-170">Dependency actions</span></span>

<span data-ttu-id="a42c1-171">De forma predeterminada, una tarea dependiente o un conjunto de tareas se ejecuta solo después de que una tarea principal se haya completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="a42c1-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="a42c1-172">En algunos escenarios, puede que desee tareas dependientes toorun incluso si se produce un error en la tarea primaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="a42c1-172">In some scenarios, you may want toorun dependent tasks even if hello parent task fails.</span></span> <span data-ttu-id="a42c1-173">Puede invalidar el comportamiento predeterminado de hello mediante la especificación de una acción de dependencia.</span><span class="sxs-lookup"><span data-stu-id="a42c1-173">You can override hello default behavior by specifying a dependency action.</span></span> <span data-ttu-id="a42c1-174">Una acción de dependencia especifica si una tarea dependiente es toorun apto, en función de hello éxito o fracaso de la tarea primaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="a42c1-174">A dependency action specifies whether a dependent task is eligible toorun, based on hello success or failure of hello parent task.</span></span> 

<span data-ttu-id="a42c1-175">Por ejemplo, suponga que una tarea dependiente está esperando los datos desde la finalización de Hola de tarea de nivel superior de hello.</span><span class="sxs-lookup"><span data-stu-id="a42c1-175">For example, suppose that a dependent task is awaiting data from hello completion of hello upstream task.</span></span> <span data-ttu-id="a42c1-176">Si se produce un error en la tarea de nivel superior de hello, tarea dependiente Hola todavía puede ser capaz de toorun con los datos más antiguos.</span><span class="sxs-lookup"><span data-stu-id="a42c1-176">If hello upstream task fails, hello dependent task may still be able toorun using older data.</span></span> <span data-ttu-id="a42c1-177">En este caso, una acción de dependencia puede especificar que dicha tarea dependiente de hello es elegible toorun a pesar del error Hola de tarea principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a42c1-177">In this case, a dependency action can specify that hello dependent task is eligible toorun despite hello failure of hello parent task.</span></span>

<span data-ttu-id="a42c1-178">Una acción de dependencia se basa en una condición de salida para la tarea primaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="a42c1-178">A dependency action is based on an exit condition for hello parent task.</span></span> <span data-ttu-id="a42c1-179">Puede especificar una acción de dependencia para cualquiera de hello después de condiciones de salida; para. NET, vea hello [ExitConditions] [ net_exitconditions] clase para obtener más información:</span><span class="sxs-lookup"><span data-stu-id="a42c1-179">You can specify a dependency action for any of hello following exit conditions; for .NET, see hello [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="a42c1-180">Cuando se produce un error de procesamiento previo.</span><span class="sxs-lookup"><span data-stu-id="a42c1-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="a42c1-181">Cuando se produce un error de carga de archivo.</span><span class="sxs-lookup"><span data-stu-id="a42c1-181">When a file upload error occurs.</span></span> <span data-ttu-id="a42c1-182">Si tarea hello finaliza con un código de salida que se especificó mediante **exitCodes** o **exitCodeRanges**y, a continuación, encuentra un error de carga de archivo, la acción de hello especificado por el código de hello salida tiene prioridad.</span><span class="sxs-lookup"><span data-stu-id="a42c1-182">If hello task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, hello action specified by hello exit code takes precedence.</span></span>
- <span data-ttu-id="a42c1-183">Cuando termina la tarea hello con un código de salida definido por hello **ExitCodes** propiedad.</span><span class="sxs-lookup"><span data-stu-id="a42c1-183">When hello task exits with an exit code defined by hello **ExitCodes** property.</span></span>
- <span data-ttu-id="a42c1-184">Cuando finaliza la tarea hello con un código de salida que se encuentra dentro de un intervalo especificado por hello **ExitCodeRanges** propiedad.</span><span class="sxs-lookup"><span data-stu-id="a42c1-184">When hello task exits with an exit code that falls within a range specified by hello **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="a42c1-185">Hola caso predeterminado, si la tarea hello finaliza con un código de salida no definido en **ExitCodes** o **ExitCodeRanges**, o si la tarea hello finaliza con un error y Hola previa al procesamiento **PreProcessingError**  propiedad no está establecida o si hello se produce un error de tarea con un archivo carga hello y error **FileUploadError** propiedad no está establecida.</span><span class="sxs-lookup"><span data-stu-id="a42c1-185">hello default case, if hello task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if hello task exits with a pre-processing error and hello **PreProcessingError** property is not set, or if hello task fails with a file upload error and hello **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="a42c1-186">una acción de dependencia en. NET, conjunto hello toospecify [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] propiedad Hola condición de salida.</span><span class="sxs-lookup"><span data-stu-id="a42c1-186">toospecify a dependency action in .NET, set hello [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for hello exit condition.</span></span> <span data-ttu-id="a42c1-187">Hola **DependencyAction** propiedad toma uno de dos valores:</span><span class="sxs-lookup"><span data-stu-id="a42c1-187">hello **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="a42c1-188">Hola configuración **DependencyAction** propiedad demasiado**satisfacción** indica que las tareas dependientes son elegible toorun si la tarea primaria de Hola se cierra con un error especificado.</span><span class="sxs-lookup"><span data-stu-id="a42c1-188">Setting hello **DependencyAction** property too**Satisfy** indicates that dependent tasks are eligible toorun if hello parent task exits with a specified error.</span></span>
- <span data-ttu-id="a42c1-189">Hola configuración **DependencyAction** propiedad demasiado**bloque** indica que las tareas dependientes no están toorun elegible.</span><span class="sxs-lookup"><span data-stu-id="a42c1-189">Setting hello **DependencyAction** property too**Block** indicates that dependent tasks are not eligible toorun.</span></span>

<span data-ttu-id="a42c1-190">Hola configuración predeterminada de hello **DependencyAction** propiedad es **satisfacción** para código de salida 0, y **bloque** para todas las demás condiciones de salida.</span><span class="sxs-lookup"><span data-stu-id="a42c1-190">hello default setting for hello **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="a42c1-191">Hello fragmento de código siguiente establece hello **DependencyAction** propiedad para una tarea primaria.</span><span class="sxs-lookup"><span data-stu-id="a42c1-191">hello following code snippet sets hello **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="a42c1-192">Si tarea primaria de Hola se cierra con un error de procesamiento previo o con Hola Hola dependientes códigos de error especificado, la tarea se bloquea.</span><span class="sxs-lookup"><span data-stu-id="a42c1-192">If hello parent task exits with a pre-processing error, or with hello specified error codes, hello dependent task is blocked.</span></span> <span data-ttu-id="a42c1-193">Si la tarea primaria de hello finaliza con cualquier otro error distinto de cero, tarea dependiente hello es toorun elegible.</span><span class="sxs-lookup"><span data-stu-id="a42c1-193">If hello parent task exits with any other non-zero error, hello dependent task is eligible toorun.</span></span>

```csharp
// Task A is hello parent task.
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
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="a42c1-194">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a42c1-194">Code sample</span></span>
<span data-ttu-id="a42c1-195">Hola [TaskDependencies] [ github_taskdependencies] proyecto de ejemplo es uno de hello [ejemplos de código de Azure Batch] [ github_samples] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="a42c1-195">hello [TaskDependencies][github_taskdependencies] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="a42c1-196">Esta solución de Visual Studio muestra:</span><span class="sxs-lookup"><span data-stu-id="a42c1-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="a42c1-197">¿Cómo tooenable tareas depende de un trabajo</span><span class="sxs-lookup"><span data-stu-id="a42c1-197">How tooenable task dependency on a job</span></span>
- <span data-ttu-id="a42c1-198">¿Cómo toocreate las tareas que dependen de otras tareas</span><span class="sxs-lookup"><span data-stu-id="a42c1-198">How toocreate tasks that depend on other tasks</span></span>
- <span data-ttu-id="a42c1-199">¿Cómo tooexecute las tareas en un grupo de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="a42c1-199">How tooexecute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a42c1-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a42c1-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="a42c1-201">Implementación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a42c1-201">Application deployment</span></span>
<span data-ttu-id="a42c1-202">Hola [paquetes de aplicación](batch-application-packages.md) característica de lote proporciona una manera fácil de implementar tooboth y la versión nodos de aplicaciones de Hola que se ejecutan las tareas en ejecución.</span><span class="sxs-lookup"><span data-stu-id="a42c1-202">hello [application packages](batch-application-packages.md) feature of Batch provides an easy way tooboth deploy and version hello applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="a42c1-203">Instalación de aplicaciones y datos de ensayo</span><span class="sxs-lookup"><span data-stu-id="a42c1-203">Installing applications and staging data</span></span>
<span data-ttu-id="a42c1-204">Vea [nodos de proceso de instalación de aplicaciones y datos en lotes de almacenamiento provisional] [ forum_post] en el foro de Azure Batch Hola para obtener información general de métodos para preparar los nodos toorun tareas.</span><span class="sxs-lookup"><span data-stu-id="a42c1-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in hello Azure Batch forum for an overview of methods for preparing your nodes toorun tasks.</span></span> <span data-ttu-id="a42c1-205">Escrito por uno de los miembros del equipo de Azure Batch de hello, que esta entrada es un buen manual en las aplicaciones de toocopy de maneras diferentes de Hola, datos de entrada de tarea y otro archivos tooyour nodos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a42c1-205">Written by one of hello Azure Batch team members, this post is a good primer on hello different ways toocopy applications, task input data, and other files tooyour compute nodes.</span></span>

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

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagrama: dependencia uno a uno"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagrama: dependencia uno a varios"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagrama: dependencia de intervalo de id. de tarea"
