---
title: "Creación de tareas para preparar trabajos y completarlos en nodos de proceso - Azure Batch | Microsoft Docs"
description: "Utilice las tareas de preparación en el nivel de trabajo para minimizar la transferencia de datos a los nodos de proceso de Azure Batch y las tareas de liberación para la limpieza del nodo tras la finalización del trabajo."
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
ms.openlocfilehash: 6a2525c02ce7bd3969469d2e28a5fccc948f89b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="14181-103">Ejecución de tareas de preparación y liberación de trabajos en nodos de proceso de Batch</span><span class="sxs-lookup"><span data-stu-id="14181-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="14181-104">A menudo, Azure Batch requiere algún tipo de configuración antes de ejecutar sus tareas y un mantenimiento posterior al trabajo una vez completadas sus tareas.</span><span class="sxs-lookup"><span data-stu-id="14181-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="14181-105">Puede ser necesario descargar los datos de entrada de tareas comunes en los nodos de proceso, o bien cargar datos de salida de tareas en Azure Storage una vez completado el trabajo.</span><span class="sxs-lookup"><span data-stu-id="14181-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span></span> <span data-ttu-id="14181-106">Puede usar las tareas de **preparación del trabajo** y **liberación del trabajo** para realizar estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="14181-106">You can use **job preparation** and **job release** tasks to perform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="14181-107">Tareas de preparación y liberación de trabajos</span><span class="sxs-lookup"><span data-stu-id="14181-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="14181-108">Antes de ejecutar las tareas de un trabajo, la tarea de preparación del trabajo se ejecuta en todos los nodos de proceso programados para ejecutar al menos una tarea.</span><span class="sxs-lookup"><span data-stu-id="14181-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span></span> <span data-ttu-id="14181-109">Cuando el trabajo se ha completado, la tarea de liberación del trabajo se ejecuta en cada nodo del grupo que ejecutó al menos una tarea.</span><span class="sxs-lookup"><span data-stu-id="14181-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="14181-110">Al igual que con las tareas normales de Batch, puede especificar una línea de comandos para que se invoque cuando se ejecute una tarea de preparación o liberación.</span><span class="sxs-lookup"><span data-stu-id="14181-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="14181-111">Las tareas de preparación y liberación ofrecen características de tareas de Batch familiares, como la descarga de archivos ([archivos de recursos][net_job_prep_resourcefiles]), la ejecución con elevación de privilegios, las variables de entorno personalizadas, la duración máxima de ejecución, el número de reintentos y el tiempo de retención de archivos.</span><span class="sxs-lookup"><span data-stu-id="14181-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="14181-112">En las siguientes secciones, aprenderá cómo utilizar las clases [JobPreparationTask][net_job_prep] y [JobReleaseTask][net_job_release] que se encuentran en la biblioteca de [.NET para Batch][api_net].</span><span class="sxs-lookup"><span data-stu-id="14181-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="14181-113">Las tareas de preparación y liberación de trabajos son especialmente útiles en entornos de "grupo compartido", en los que un grupo de nodos de proceso persiste entre ejecuciones de trabajo y muchos trabajos lo usan.</span><span class="sxs-lookup"><span data-stu-id="14181-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a><span data-ttu-id="14181-114">Uso de las tareas de preparación y liberación de trabajos</span><span class="sxs-lookup"><span data-stu-id="14181-114">When to use job preparation and release tasks</span></span>
<span data-ttu-id="14181-115">Las tareas de preparación y liberación de trabajos son una buena opción en las situaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="14181-115">Job preparation and job release tasks are a good fit for the following situations:</span></span>

<span data-ttu-id="14181-116">**Descarga de datos de tareas comunes**</span><span class="sxs-lookup"><span data-stu-id="14181-116">**Download common task data**</span></span>

<span data-ttu-id="14181-117">A menudo, los trabajos de Lote requieren un conjunto común de datos como entrada para las tareas del trabajo.</span><span class="sxs-lookup"><span data-stu-id="14181-117">Batch jobs often require a common set of data as input for the job's tasks.</span></span> <span data-ttu-id="14181-118">Por ejemplo, en cálculos de análisis de riesgos diarios, los datos de mercado son específicos del trabajo, pero comunes a todas las tareas incluidas en él.</span><span class="sxs-lookup"><span data-stu-id="14181-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span></span> <span data-ttu-id="14181-119">Estos datos de mercado, a menudo con un tamaño de varios gigabytes, deben descargarse en cada nodo de proceso una sola vez, para que cualquier tarea que se ejecuta en el nodo pueda usarlos.</span><span class="sxs-lookup"><span data-stu-id="14181-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span></span> <span data-ttu-id="14181-120">Puede usar una **tarea de preparación del trabajo** para descargar estos datos en cada nodo antes de la ejecución de otras tareas del trabajo.</span><span class="sxs-lookup"><span data-stu-id="14181-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span></span>

<span data-ttu-id="14181-121">**Trabajo persistente y resultado de la tarea**</span><span class="sxs-lookup"><span data-stu-id="14181-121">**Delete job and task output**</span></span>

<span data-ttu-id="14181-122">En un entorno de "grupo compartido", cuando no se dan de baja los nodos de proceso de un grupo entre los trabajos, puede ser necesario eliminar datos del trabajo entre ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="14181-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span></span> <span data-ttu-id="14181-123">Puede ser necesario conservar espacio en disco en los nodos o cumplir las directivas de seguridad de su organización.</span><span class="sxs-lookup"><span data-stu-id="14181-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="14181-124">Use una **tarea de liberación del trabajo** para eliminar los datos descargados por una tarea de preparación del trabajo o generados durante la ejecución de la tarea.</span><span class="sxs-lookup"><span data-stu-id="14181-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="14181-125">**Retención de registro**</span><span class="sxs-lookup"><span data-stu-id="14181-125">**Log retention**</span></span>

<span data-ttu-id="14181-126">Puede que desee conservar una copia de los archivos de registro generados por las tareas o quizás los archivos de volcado de memoria generados por aplicaciones con errores.</span><span class="sxs-lookup"><span data-stu-id="14181-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="14181-127">Puede usar una **tarea de liberación del trabajo** en estos casos para comprimir y cargar estos datos en una cuenta de [Azure Storage][azure_storage].</span><span class="sxs-lookup"><span data-stu-id="14181-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="14181-128">Otra manera de conservar los registros y otros datos de salida de los trabajos y las tareas es usar la biblioteca [Azure Batch File Conventions](batch-task-output.md) (Convenciones de archivos de Azure Batch).</span><span class="sxs-lookup"><span data-stu-id="14181-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="14181-129">tarea de preparación del trabajo</span><span class="sxs-lookup"><span data-stu-id="14181-129">Job preparation task</span></span>
<span data-ttu-id="14181-130">Antes de ejecutar las tareas de un trabajo, Batch ejecuta la tarea de preparación del trabajo en cada nodo de proceso programado para ejecutar una tarea.</span><span class="sxs-lookup"><span data-stu-id="14181-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span></span> <span data-ttu-id="14181-131">De forma predeterminada, el servicio Batch esperará hasta que la tarea de preparación del trabajo se complete antes de ejecutar las tareas programadas para ejecutarse en el nodo.</span><span class="sxs-lookup"><span data-stu-id="14181-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span></span> <span data-ttu-id="14181-132">Sin embargo, puede configurar el servicio para que no espere.</span><span class="sxs-lookup"><span data-stu-id="14181-132">However, you can configure the service not to wait.</span></span> <span data-ttu-id="14181-133">Si se reinicia el nodo, la tarea de preparación del trabajo se ejecutará de nuevo, pero también puede deshabilitar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="14181-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="14181-134">La tarea de preparación del trabajo solo se ejecuta en los nodos programados para ejecutar una tarea.</span><span class="sxs-lookup"><span data-stu-id="14181-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span></span> <span data-ttu-id="14181-135">Esto impide la ejecución innecesaria de una tarea de preparación en caso de que un nodo no tenga una tarea asignada.</span><span class="sxs-lookup"><span data-stu-id="14181-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="14181-136">Esto puede ocurrir cuando el número de tareas de un trabajo es menor que el número de nodos de un grupo.</span><span class="sxs-lookup"><span data-stu-id="14181-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span></span> <span data-ttu-id="14181-137">También se aplica cuando la [ejecución de tareas simultáneas](batch-parallel-node-tasks.md) está habilitada, lo que deja algunos nodos inactivos si el número de tareas es menor que el total de posibles tareas simultáneas.</span><span class="sxs-lookup"><span data-stu-id="14181-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span></span> <span data-ttu-id="14181-138">Si no ejecuta la tarea de preparación del trabajo en nodos inactivos, puede ahorrar dinero en gastos de transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="14181-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="14181-139">[JobPreparationTask][net_job_prep_cloudjob] difiere de [CloudPool.StartTask][pool_starttask] en que JobPreparationTask se ejecuta al principio de cada trabajo, mientras que StartTask solo se ejecuta cuando un nodo de proceso se une por primera vez a un grupo o se reinicia.</span><span class="sxs-lookup"><span data-stu-id="14181-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="14181-140">tarea de liberación del trabajo</span><span class="sxs-lookup"><span data-stu-id="14181-140">Job release task</span></span>
<span data-ttu-id="14181-141">Cuando un trabajo se marca como completado, se ejecuta la tarea de liberación del trabajo en cada nodo del grupo que ejecutó al menos una tarea.</span><span class="sxs-lookup"><span data-stu-id="14181-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="14181-142">El trabajo se marca como completado mediante la emisión de una solicitud de finalización.</span><span class="sxs-lookup"><span data-stu-id="14181-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="14181-143">A continuación, el servicio Batch establece el estado del trabajo en *terminando*, finaliza las tareas activas o en ejecución asociadas al trabajo y ejecuta la tarea de liberación del trabajo.</span><span class="sxs-lookup"><span data-stu-id="14181-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span></span> <span data-ttu-id="14181-144">A continuación, el trabajo se mueve al estado *completado* .</span><span class="sxs-lookup"><span data-stu-id="14181-144">The job then moves to the *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="14181-145">La eliminación de un trabajo también ejecuta la tarea de liberación del trabajo.</span><span class="sxs-lookup"><span data-stu-id="14181-145">Job deletion also executes the job release task.</span></span> <span data-ttu-id="14181-146">Sin embargo, si un trabajo ya se ha terminado, la tarea no se ejecuta una segunda vez si el trabajo se va a eliminar más adelante.</span><span class="sxs-lookup"><span data-stu-id="14181-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="14181-147">Tareas de preparación y liberación de trabajos con Lote para .NET</span><span class="sxs-lookup"><span data-stu-id="14181-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="14181-148">Para usar una tarea de preparación del trabajo, asigne un objeto [JobPreparationTask][net_job_prep] a la propiedad [CloudJob.JobPreparationTask][net_job_prep_cloudjob] del trabajo.</span><span class="sxs-lookup"><span data-stu-id="14181-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="14181-149">De forma similar, para establecer la tarea de liberación del trabajo, inicialice una [JobReleaseTask][net_job_release] y asígnela a la propiedad [CloudJob.JobReleaseTask][net_job_prep_cloudjob] del trabajo.</span><span class="sxs-lookup"><span data-stu-id="14181-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span></span>

<span data-ttu-id="14181-150">En este fragmento de código, `myBatchClient` es una instancia de [BatchClient][net_batch_client] y `myPool` es un grupo existente en la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="14181-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span></span>

```csharp
// Create the CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify the command lines for the job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign the job preparation task to the job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign the job release task to the job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="14181-151">Como se mencionó antes, la tarea de liberación se ejecuta cuando se finaliza o se elimina un trabajo.</span><span class="sxs-lookup"><span data-stu-id="14181-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="14181-152">Finalice un trabajo con [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="14181-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="14181-153">Elimine un trabajo con [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="14181-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="14181-154">Normalmente un trabajo se termina o elimina cuando se han completado sus tareas o cuando se ha alcanzado el tiempo de espera que haya definido.</span><span class="sxs-lookup"><span data-stu-id="14181-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="14181-155">Código de ejemplo en GitHub</span><span class="sxs-lookup"><span data-stu-id="14181-155">Code sample on GitHub</span></span>
<span data-ttu-id="14181-156">Para ver cómo funcionan las tareas de preparación y liberación del trabajo, consulte el proyecto de ejemplo [JobPrepRelease][job_prep_release_sample] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="14181-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="14181-157">Esta aplicación de consola hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="14181-157">This console application does the following:</span></span>

1. <span data-ttu-id="14181-158">Crea un grupo con dos nodos "pequeños".</span><span class="sxs-lookup"><span data-stu-id="14181-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="14181-159">Crea un trabajo con las tareas de preparación y de liberación del trabajo, además de las estándar.</span><span class="sxs-lookup"><span data-stu-id="14181-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="14181-160">Ejecuta la tarea de preparación del trabajo, que en primer lugar escribe el identificador de nodo en un archivo de texto en el directorio "shared" de un nodo.</span><span class="sxs-lookup"><span data-stu-id="14181-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="14181-161">Ejecuta una tarea en cada nodo que escribe su identificador de tarea en el mismo archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="14181-161">Runs a task on each node that writes its task ID to the same text file.</span></span>
5. <span data-ttu-id="14181-162">Una vez que se han completado todas las tareas (o se alcanza el tiempo de espera), imprime el contenido del archivo de texto de cada nodo en la consola.</span><span class="sxs-lookup"><span data-stu-id="14181-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span></span>
6. <span data-ttu-id="14181-163">Cuando se ha completado el trabajo, ejecuta la tarea de liberación del trabajo para eliminar el archivo del nodo.</span><span class="sxs-lookup"><span data-stu-id="14181-163">When the job is completed, runs the job release task to delete the file from the node.</span></span>
7. <span data-ttu-id="14181-164">Imprime los códigos de salida de las tareas de preparación y liberación del trabajo para cada nodo donde se ejecutaron.</span><span class="sxs-lookup"><span data-stu-id="14181-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="14181-165">Pausa la ejecución para permitir la confirmación de la eliminación del trabajo o el grupo.</span><span class="sxs-lookup"><span data-stu-id="14181-165">Pauses execution to allow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="14181-166">La salida de la aplicación de ejemplo es similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="14181-166">Output from the sample application is similar to the following:</span></span>

```
Attempting to create pool: JobPrepReleaseSamplePool
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

Waiting for job JobPrepReleaseSampleJob to reach state Completed
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

Sample complete, hit ENTER to exit...
```

> [!NOTE]
> <span data-ttu-id="14181-167">Debido a la creación de variables y a la hora de inicio de los nodos en un nuevo grupo (algunos nodos están listos para las tareas antes que otros), puede que la salida sea diferente.</span><span class="sxs-lookup"><span data-stu-id="14181-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="14181-168">En concreto, como las tareas se realizan rápidamente, uno de los nodos del grupo podría ejecutar todas las tareas del trabajo.</span><span class="sxs-lookup"><span data-stu-id="14181-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span></span> <span data-ttu-id="14181-169">Si esto sucede, observará que las tareas de preparación y liberación del trabajo no existen para el nodo que no ha ejecutado ninguna tarea.</span><span class="sxs-lookup"><span data-stu-id="14181-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a><span data-ttu-id="14181-170">Inspección de las tareas de preparación y liberación en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="14181-170">Inspect job preparation and release tasks in the Azure portal</span></span>
<span data-ttu-id="14181-171">Cuando ejecute la aplicación de ejemplo, puede usar [Azure Portal][portal] para ver las propiedades del trabajo y sus tareas, o incluso descargar el archivo de texto compartido modificado por las tareas del trabajo.</span><span class="sxs-lookup"><span data-stu-id="14181-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span></span>

<span data-ttu-id="14181-172">La captura de pantalla siguiente muestra la **hoja de tareas de preparación** en Azure Portal después de una ejecución de la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="14181-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span></span> <span data-ttu-id="14181-173">Vaya a las propiedades *JobPrepReleaseSampleJob* después de que sus tareas se hayan completado (pero antes de eliminar el trabajo y el grupo) y haga clic en **Tareas de preparación** o **Tareas de liberación** para ver sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="14181-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span></span>

![Propiedades de preparación del trabajo en el Portal de Azure][1]

## <a name="next-steps"></a><span data-ttu-id="14181-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14181-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="14181-176">Paquetes de aplicación</span><span class="sxs-lookup"><span data-stu-id="14181-176">Application packages</span></span>
<span data-ttu-id="14181-177">Además de la tarea de preparación del trabajo, puede usar la característica de [paquetes de aplicación](batch-application-packages.md) de Batch para preparar los nodos de proceso de cara a la ejecución de tareas.</span><span class="sxs-lookup"><span data-stu-id="14181-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span></span> <span data-ttu-id="14181-178">Esta característica es especialmente útil para implementar aplicaciones que no requieren que se ejecute un instalador, aplicaciones que contienen muchos archivos (más de 100) o aplicaciones que requieren un control estricto de la versión.</span><span class="sxs-lookup"><span data-stu-id="14181-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="14181-179">Instalación de aplicaciones y datos de ensayo</span><span class="sxs-lookup"><span data-stu-id="14181-179">Installing applications and staging data</span></span>
<span data-ttu-id="14181-180">Este foro de MSDN proporciona información general de varios métodos de preparación de los nodos para la ejecución de tareas:</span><span class="sxs-lookup"><span data-stu-id="14181-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="14181-181">[Installing applications and staging data on Batch compute nodes][forum_post] (Instalación de aplicaciones y datos de ensayo en nodos de proceso de Batch)</span><span class="sxs-lookup"><span data-stu-id="14181-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="14181-182">Escrito por uno de los miembros del equipo de Azure Batch, describe varias técnicas que puede utilizar para implementar aplicaciones y datos en los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="14181-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span></span>

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
