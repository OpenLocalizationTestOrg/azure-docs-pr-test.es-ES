---
title: aaaCreate tareas tooprepare trabajos y tareas completadas en nodos de proceso - Azure Batch | Documentos de Microsoft
description: "Usar datos de toominimize de tareas de preparación de nivel de trabajo transferir nodos de proceso por lotes de tooAzure y tareas de limpieza de nodo a la conclusión del trabajo de la versión."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="06f64-103">Ejecución de tareas de preparación y liberación de trabajos en nodos de proceso de Batch</span><span class="sxs-lookup"><span data-stu-id="06f64-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="06f64-104">A menudo, Azure Batch requiere algún tipo de configuración antes de ejecutar sus tareas y un mantenimiento posterior al trabajo una vez completadas sus tareas.</span><span class="sxs-lookup"><span data-stu-id="06f64-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="06f64-105">Tal vez necesite toodownload comunes tarea datos de entrada tooyour proceso nodos, o se puede cargar tooAzure de datos de salida de tareas almacenamiento una vez completado el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-105">You might need toodownload common task input data tooyour compute nodes, or upload task output data tooAzure Storage after hello job completes.</span></span> <span data-ttu-id="06f64-106">Puede usar **preparación del trabajo** y **trabajo versión** tareas tooperform estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="06f64-106">You can use **job preparation** and **job release** tasks tooperform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="06f64-107">Tareas de preparación y liberación de trabajos</span><span class="sxs-lookup"><span data-stu-id="06f64-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="06f64-108">Antes de ejecutarán las tareas de un trabajo, tarea de preparación del trabajo de hello ejecuta en todos los toorun programada nodos de proceso al menos una tarea.</span><span class="sxs-lookup"><span data-stu-id="06f64-108">Before a job's tasks run, hello job preparation task runs on all compute nodes scheduled toorun at least one task.</span></span> <span data-ttu-id="06f64-109">Una vez que se complete el trabajo de hello, tarea de liberación del trabajo de Hola se ejecuta en cada nodo de grupo de Hola que ejecuta al menos una tarea.</span><span class="sxs-lookup"><span data-stu-id="06f64-109">Once hello job is completed, hello job release task runs on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="06f64-110">Al igual que con las tareas normales de lote, puede especificar un toobe de línea de comandos que se invoca cuando una preparación del trabajo o se ejecuta la tarea de liberación.</span><span class="sxs-lookup"><span data-stu-id="06f64-110">As with normal Batch tasks, you can specify a command line toobe invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="06f64-111">Las tareas de preparación y liberación ofrecen características de tareas de Batch familiares, como la descarga de archivos ([archivos de recursos][net_job_prep_resourcefiles]), la ejecución con elevación de privilegios, las variables de entorno personalizadas, la duración máxima de ejecución, el número de reintentos y el tiempo de retención de archivos.</span><span class="sxs-lookup"><span data-stu-id="06f64-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="06f64-112">Hola siguientes secciones, aprenderá cómo hello toouse [JobPreparationTask] [ net_job_prep] y [JobReleaseTask] [ net_job_release] clases se encuentran en hello [.NET de lotes] [ api_net] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="06f64-112">In hello following sections, you'll learn how toouse hello [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in hello [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="06f64-113">Las tareas de preparación y liberación de trabajos son especialmente útiles en entornos de "grupo compartido", en los que un grupo de nodos de proceso persiste entre ejecuciones de trabajo y muchos trabajos lo usan.</span><span class="sxs-lookup"><span data-stu-id="06f64-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a><span data-ttu-id="06f64-114">Cuando toouse preparación del trabajo y tareas de la versión</span><span class="sxs-lookup"><span data-stu-id="06f64-114">When toouse job preparation and release tasks</span></span>
<span data-ttu-id="06f64-115">Preparación del trabajo y tareas de la versión de trabajo son una buena elección para hello siguientes situaciones:</span><span class="sxs-lookup"><span data-stu-id="06f64-115">Job preparation and job release tasks are a good fit for hello following situations:</span></span>

<span data-ttu-id="06f64-116">**Descarga de datos de tareas comunes**</span><span class="sxs-lookup"><span data-stu-id="06f64-116">**Download common task data**</span></span>

<span data-ttu-id="06f64-117">Trabajos por lotes requieren a menudo un conjunto común de datos como entrada para las tareas del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-117">Batch jobs often require a common set of data as input for hello job's tasks.</span></span> <span data-ttu-id="06f64-118">Por ejemplo, en los cálculos de análisis de riesgos diaria, datos de mercado son específicos del trabajo, pero common tareas tooall trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-118">For example, in daily risk analysis calculations, market data is job-specific, yet common tooall tasks in hello job.</span></span> <span data-ttu-id="06f64-119">Estos datos de mercado, a menudo varios gigabytes de tamaño, deben ser una sola vez tooeach descargado de nodos de proceso que puede utilizar cualquier tarea que se ejecuta en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-119">This market data, often several gigabytes in size, should be downloaded tooeach compute node only once so that any task that runs on hello node can use it.</span></span> <span data-ttu-id="06f64-120">Use un **tareas de preparación del trabajo** toodownload este nodo de tooeach datos antes ejecución Hola de trabajo de Hola de otras tareas.</span><span class="sxs-lookup"><span data-stu-id="06f64-120">Use a **job preparation task** toodownload this data tooeach node before hello execution of hello job's other tasks.</span></span>

<span data-ttu-id="06f64-121">**Trabajo persistente y resultado de la tarea**</span><span class="sxs-lookup"><span data-stu-id="06f64-121">**Delete job and task output**</span></span>

<span data-ttu-id="06f64-122">En un entorno compartido» grupo", donde los nodos de proceso del grupo no están dado de baja entre los trabajos, puede ser necesario toodelete datos del trabajo entre ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="06f64-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need toodelete job data between runs.</span></span> <span data-ttu-id="06f64-123">Es posible que tenga tooconserve espacio en disco en los nodos de Hola o cumplir las directivas de seguridad de su organización.</span><span class="sxs-lookup"><span data-stu-id="06f64-123">You might need tooconserve disk space on hello nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="06f64-124">Use un **tarea de liberación del trabajo** datos toodelete descargados por una tarea de preparación del trabajo, o generados durante la ejecución de la tarea.</span><span class="sxs-lookup"><span data-stu-id="06f64-124">Use a **job release task** toodelete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="06f64-125">**Retención de registro**</span><span class="sxs-lookup"><span data-stu-id="06f64-125">**Log retention**</span></span>

<span data-ttu-id="06f64-126">Puede ser conveniente tookeep una copia de archivos de registro que generan las tareas, o quizás archivos de volcado que se pueden generar aplicaciones con errores.</span><span class="sxs-lookup"><span data-stu-id="06f64-126">You might want tookeep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="06f64-127">Use un **tarea de liberación del trabajo** en tales casos toocompress y cargar este tooan datos [el almacenamiento de Azure] [ azure_storage] cuenta.</span><span class="sxs-lookup"><span data-stu-id="06f64-127">Use a **job release task** in such cases toocompress and upload this data tooan [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="06f64-128">Toopersist de otra manera datos se toouse Hola de salida de registros y otros trabajos y tareas [convenciones de archivos por lotes de Azure](batch-task-output.md) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="06f64-128">Another way toopersist logs and other job and task output data is toouse hello [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="06f64-129">tarea de preparación del trabajo</span><span class="sxs-lookup"><span data-stu-id="06f64-129">Job preparation task</span></span>
<span data-ttu-id="06f64-130">Antes de la ejecución de tareas de un trabajo, lote ejecuta la tarea de preparación del trabajo de hello en cada nodo de proceso que está programada toorun una tarea.</span><span class="sxs-lookup"><span data-stu-id="06f64-130">Before execution of a job's tasks, Batch executes hello job preparation task on each compute node that is scheduled toorun a task.</span></span> <span data-ttu-id="06f64-131">De manera predeterminada, Hola servicio por lotes espera toobe de tareas de preparación Hola trabajo completado antes de ejecutar tooexecute de hello tareas programadas en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-131">By default, hello Batch service waits for hello job preparation task toobe completed before running hello tasks scheduled tooexecute on hello node.</span></span> <span data-ttu-id="06f64-132">Sin embargo, puede configurar el servicio de hello no toowait.</span><span class="sxs-lookup"><span data-stu-id="06f64-132">However, you can configure hello service not toowait.</span></span> <span data-ttu-id="06f64-133">Si se reinicia el nodo de hello, tarea de preparación de hello trabajo se ejecuta de nuevo, pero también se puede deshabilitar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="06f64-133">If hello node restarts, hello job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="06f64-134">se ejecuta la tarea de preparación del trabajo de Hello solo en nodos que estén programada toorun una tarea.</span><span class="sxs-lookup"><span data-stu-id="06f64-134">hello job preparation task is executed only on nodes that are scheduled toorun a task.</span></span> <span data-ttu-id="06f64-135">Esto impide la ejecución innecesarios de Hola de una tarea de preparación en caso de que un nodo no está asignado a una tarea.</span><span class="sxs-lookup"><span data-stu-id="06f64-135">This prevents hello unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="06f64-136">Esto puede ocurrir cuando número Hola de tareas para un trabajo es menor que el número de Hola de nodos en un grupo.</span><span class="sxs-lookup"><span data-stu-id="06f64-136">This can occur when hello number of tasks for a job is less than hello number of nodes in a pool.</span></span> <span data-ttu-id="06f64-137">También se aplica cuando [ejecución de tareas simultáneas](batch-parallel-node-tasks.md) está habilitada, lo que deja a algunos nodos inactivo si recuento de tareas de hello es inferior a tareas simultáneas posibles total Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if hello task count is lower than hello total possible concurrent tasks.</span></span> <span data-ttu-id="06f64-138">No ejecutando tarea de preparación del trabajo de hello en nodos inactivos, puede ahorrar dinero en gastos de transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="06f64-138">By not running hello job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="06f64-139">[JobPreparationTask] [ net_job_prep_cloudjob] difiere de [CloudPool.StartTask] [ pool_starttask] en que JobPreparationTask se ejecuta en el inicio de Hola de cada trabajo, mientras que StartTask se ejecuta solo cuando un nodo de proceso en primer lugar une a un grupo o se reinicia.</span><span class="sxs-lookup"><span data-stu-id="06f64-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at hello start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="06f64-140">tarea de liberación del trabajo</span><span class="sxs-lookup"><span data-stu-id="06f64-140">Job release task</span></span>
<span data-ttu-id="06f64-141">Una vez que un trabajo está marcado como completada, la tarea de liberación del trabajo de Hola se ejecuta en cada nodo de grupo de Hola que ejecuta al menos una tarea.</span><span class="sxs-lookup"><span data-stu-id="06f64-141">Once a job is marked as completed, hello job release task is executed on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="06f64-142">El trabajo se marca como completado mediante la emisión de una solicitud de finalización.</span><span class="sxs-lookup"><span data-stu-id="06f64-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="06f64-143">Hola servicio por lotes, a continuación, Establece Hola estado del trabajo demasiado*terminación*, finaliza las tareas activas o en ejecución asociadas con el trabajo de Hola y ejecuta la tarea de liberación del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-143">hello Batch service then sets hello job state too*terminating*, terminates any active or running tasks associated with hello job, and runs hello job release task.</span></span> <span data-ttu-id="06f64-144">trabajo de Hello, a continuación, mueve toohello *completado* estado.</span><span class="sxs-lookup"><span data-stu-id="06f64-144">hello job then moves toohello *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="06f64-145">Eliminación de trabajo también ejecuta la tarea de liberación del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-145">Job deletion also executes hello job release task.</span></span> <span data-ttu-id="06f64-146">Sin embargo, si ya ha finalizado un trabajo, tarea de liberación de hello no se ejecuta una segunda vez si más adelante se elimina el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-146">However, if a job has already been terminated, hello release task is not run a second time if hello job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="06f64-147">Tareas de preparación y liberación de trabajos con Lote para .NET</span><span class="sxs-lookup"><span data-stu-id="06f64-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="06f64-148">asignar una tarea de preparación del trabajo, toouse una [JobPreparationTask] [ net_job_prep] del trabajo de objeto tooyour [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] propiedad .</span><span class="sxs-lookup"><span data-stu-id="06f64-148">toouse a job preparation task, assign a [JobPreparationTask][net_job_prep] object tooyour job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="06f64-149">Inicializar de forma similar, un [JobReleaseTask] [ net_job_release] y asígnele el nombre del trabajo de tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] hello tooset de propiedad tarea de liberación del trabajo.</span><span class="sxs-lookup"><span data-stu-id="06f64-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it tooyour job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property tooset hello job's release task.</span></span>

<span data-ttu-id="06f64-150">En este fragmento de código, `myBatchClient` es una instancia de [BatchClient][net_batch_client], y `myPool` es un grupo existente dentro de hello cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="06f64-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within hello Batch account.</span></span>

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="06f64-151">Tal y como se mencionó anteriormente, la tarea de versión de Hola se ejecuta cuando se finaliza o se elimina un trabajo.</span><span class="sxs-lookup"><span data-stu-id="06f64-151">As mentioned earlier, hello release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="06f64-152">Finalice un trabajo con [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="06f64-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="06f64-153">Elimine un trabajo con [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="06f64-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="06f64-154">Normalmente un trabajo se termina o elimina cuando se han completado sus tareas o cuando se ha alcanzado el tiempo de espera que haya definido.</span><span class="sxs-lookup"><span data-stu-id="06f64-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="06f64-155">Código de ejemplo en GitHub</span><span class="sxs-lookup"><span data-stu-id="06f64-155">Code sample on GitHub</span></span>
<span data-ttu-id="06f64-156">las tareas de preparación y la versión del trabajo de toosee en acción, visite hello [JobPrepRelease] [ job_prep_release_sample] proyecto de ejemplo en GitHub.</span><span class="sxs-lookup"><span data-stu-id="06f64-156">toosee job preparation and release tasks in action, check out hello [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="06f64-157">Esta aplicación de consola Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="06f64-157">This console application does hello following:</span></span>

1. <span data-ttu-id="06f64-158">Crea un grupo con dos nodos "pequeños".</span><span class="sxs-lookup"><span data-stu-id="06f64-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="06f64-159">Crea un trabajo con las tareas de preparación y de liberación del trabajo, además de las estándar.</span><span class="sxs-lookup"><span data-stu-id="06f64-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="06f64-160">Se ejecuta Hola tarea de preparación del trabajo, que escribe primero el archivo de texto de tooa de Id. de nodo de hello en el directorio "compartido" de un nodo.</span><span class="sxs-lookup"><span data-stu-id="06f64-160">Runs hello job preparation task, which first writes hello node ID tooa text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="06f64-161">Ejecuta una tarea en cada nodo que escribe su toohello de Id. de tarea mismo archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="06f64-161">Runs a task on each node that writes its task ID toohello same text file.</span></span>
5. <span data-ttu-id="06f64-162">Una vez que se completan todas las tareas (o se alcanza el tiempo de espera de hello), imprime el contenido de Hola de consola de toohello de archivos de texto de cada nodo.</span><span class="sxs-lookup"><span data-stu-id="06f64-162">Once all tasks are completed (or hello timeout is reached), prints hello contents of each node's text file toohello console.</span></span>
6. <span data-ttu-id="06f64-163">Cuando se completa el trabajo de hello, ejecuta archivo de hello trabajo versión tarea toodelete Hola de nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-163">When hello job is completed, runs hello job release task toodelete hello file from hello node.</span></span>
7. <span data-ttu-id="06f64-164">Hola imprime códigos de preparación del trabajo Hola de salida y las tareas para cada nodo en el que ejecuta la versión.</span><span class="sxs-lookup"><span data-stu-id="06f64-164">Prints hello exit codes of hello job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="06f64-165">Confirmación de tooallow de la ejecución de las pausas de eliminación de trabajo o grupo.</span><span class="sxs-lookup"><span data-stu-id="06f64-165">Pauses execution tooallow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="06f64-166">Resultado de la aplicación de ejemplo de Hola es siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="06f64-166">Output from hello sample application is similar toohello following:</span></span>

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> <span data-ttu-id="06f64-167">Pagar toohello variable creación y hora de inicio de nodos en un grupo nuevo (algunos nodos no están listos para tareas antes que otras), puede ver un resultado diferente.</span><span class="sxs-lookup"><span data-stu-id="06f64-167">Due toohello variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="06f64-168">En concreto, dado que las tareas de hello completan rápidamente, uno de los nodos del grupo de hello puede ejecutar todas las tareas del trabajo de Hola de.</span><span class="sxs-lookup"><span data-stu-id="06f64-168">Specifically, because hello tasks complete quickly, one of hello pool's nodes may execute all of hello job's tasks.</span></span> <span data-ttu-id="06f64-169">Si esto ocurre, observará que Hola prep del trabajo y tareas de la versión no existe para el nodo de Hola que no ejecutar ninguna tarea.</span><span class="sxs-lookup"><span data-stu-id="06f64-169">If this occurs, you will notice that hello job prep and release tasks do not exist for hello node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a><span data-ttu-id="06f64-170">Inspeccionar la preparación del trabajo y las tareas de la versión de Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="06f64-170">Inspect job preparation and release tasks in hello Azure portal</span></span>
<span data-ttu-id="06f64-171">Cuando se ejecuta la aplicación de ejemplo de Hola, puede usar hello [portal de Azure] [ portal] tooview Hola propiedades del trabajo de Hola y sus tareas, o incluso descargar archivo de texto compartida hello modificado por tareas del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-171">When you run hello sample application, you can use hello [Azure portal][portal] tooview hello properties of hello job and its tasks, or even download hello shared text file that is modified by hello job's tasks.</span></span>

<span data-ttu-id="06f64-172">Hola de captura de pantalla siguiente muestra hello **hoja de tareas de preparación** en el portal de Azure después de una ejecución de la aplicación de ejemplo de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="06f64-172">hello screenshot below shows hello **Preparation tasks blade** in hello Azure portal after a run of hello sample application.</span></span> <span data-ttu-id="06f64-173">Navegue toohello *JobPrepReleaseSampleJob* propiedades después de han completado las tareas (pero antes de eliminar el trabajo y grupo) y haga clic en **tareas de preparación** o **versión tareas** tooview sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="06f64-173">Navigate toohello *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** tooview their properties.</span></span>

![Propiedades de preparación del trabajo en el Portal de Azure][1]

## <a name="next-steps"></a><span data-ttu-id="06f64-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="06f64-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="06f64-176">paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="06f64-176">Application packages</span></span>
<span data-ttu-id="06f64-177">En la tarea de preparación de suma toohello trabajo, también puede utilizar hello [paquetes de aplicación](batch-application-packages.md) nodos para la ejecución de la tarea de ejecución de la característica de tooprepare de lote.</span><span class="sxs-lookup"><span data-stu-id="06f64-177">In addition toohello job preparation task, you can also use hello [application packages](batch-application-packages.md) feature of Batch tooprepare compute nodes for task execution.</span></span> <span data-ttu-id="06f64-178">Esta característica es especialmente útil para implementar aplicaciones que no requieren que se ejecute un instalador, aplicaciones que contienen muchos archivos (más de 100) o aplicaciones que requieren un control estricto de la versión.</span><span class="sxs-lookup"><span data-stu-id="06f64-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="06f64-179">Instalación de aplicaciones y datos de ensayo</span><span class="sxs-lookup"><span data-stu-id="06f64-179">Installing applications and staging data</span></span>
<span data-ttu-id="06f64-180">Este foro de MSDN proporciona información general de varios métodos de preparación de los nodos para la ejecución de tareas:</span><span class="sxs-lookup"><span data-stu-id="06f64-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="06f64-181">[Installing applications and staging data on Batch compute nodes][forum_post] (Instalación de aplicaciones y datos de ensayo en nodos de proceso de Batch)</span><span class="sxs-lookup"><span data-stu-id="06f64-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="06f64-182">Escrito por uno de los miembros del equipo de Azure Batch de hello, describe varias técnicas que puede usar los nodos de toocompute de aplicaciones y datos de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="06f64-182">Written by one of hello Azure Batch team members, it discusses several techniques that you can use toodeploy applications and data toocompute nodes.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
