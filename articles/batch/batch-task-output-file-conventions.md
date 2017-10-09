---
title: aaaPersist trabajos y tareas tooAzure almacenamiento con la biblioteca de hello convenciones de archivo de salida para .NET - Azure Batch | Documentos de Microsoft
description: "Obtenga información acerca de cómo hello de vista y tooAzure de salida de trabajo almacenamiento y biblioteca de toouse convenciones de archivos por lotes de Azure para .NET toopersist tarea por lotes persistido salida Hola portal de Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="4dfda-103">Conservar el trabajo y tareas tooAzure almacenamiento de datos con la biblioteca de convenciones de archivo por lotes de Hola para .NET toopersist</span><span class="sxs-lookup"><span data-stu-id="4dfda-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="4dfda-104">Datos de la tarea de toopersist unidireccional están hello de toouse [biblioteca convenciones de archivos por lotes de Azure para .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="4dfda-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="4dfda-105">Hello biblioteca convenciones de archivos simplifica el proceso de Hola de almacenar el resultado de la tarea tooAzure almacenamiento de datos y recuperarlos.</span><span class="sxs-lookup"><span data-stu-id="4dfda-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="4dfda-106">Puede usar Hola convenciones archivos biblioteca en código de cliente y de tarea &mdash; en código de la tarea para guardar archivos y en el cliente toolist de código y recuperarlos.</span><span class="sxs-lookup"><span data-stu-id="4dfda-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="4dfda-107">El código de la tarea también puede utilizar salida de hello tooretrieve Hola de biblioteca de tareas de nivel superior, como en un [las dependencias entre tareas](batch-task-dependencies.md) escenario.</span><span class="sxs-lookup"><span data-stu-id="4dfda-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="4dfda-108">tooretrieve archivos con la biblioteca de hello convenciones de archivo de salida, puede encontrar archivos de Hola para un determinado trabajo o tarea enumerándolos por identificador y el propósito.</span><span class="sxs-lookup"><span data-stu-id="4dfda-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="4dfda-109">No es necesario tooknow los nombres de Hola o ubicaciones de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dfda-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="4dfda-110">Por ejemplo, puede usar todos los archivos intermedios de toolist de biblioteca de hello convenciones de archivo para una tarea determinada u obtener un archivo de vista previa de un trabajo determinado.</span><span class="sxs-lookup"><span data-stu-id="4dfda-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="4dfda-111">A partir de la versión de 2017-05-01, Hola API del servicio por lotes admite tooAzure de datos de persistencia salida almacenamiento tareas y tareas de administrador de trabajos que se ejecutan en los grupos creados con la configuración de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dfda-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="4dfda-112">Hola API del servicio de lote proporciona una toopersist de manera sencilla de salida desde dentro del código de hello que crea una tarea y actúa como una biblioteca de convenciones de archivo toohello alternativo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="4dfda-113">Puede modificar el resultado de toopersist de las aplicaciones de cliente de lote sin necesidad de aplicación de hello tooupdate que se ejecuta la tarea.</span><span class="sxs-lookup"><span data-stu-id="4dfda-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="4dfda-114">Para obtener más información, consulte [tooAzure de datos de tarea almacenamiento con hello API del servicio de lote se conservan](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="4dfda-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="4dfda-115">¿Cuándo se puede utilizar el resultado de la tarea de toopersist de biblioteca Hola convenciones de archivo?</span><span class="sxs-lookup"><span data-stu-id="4dfda-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="4dfda-116">Lote de Azure proporciona toopersist más de una manera de resultado de la tarea.</span><span class="sxs-lookup"><span data-stu-id="4dfda-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="4dfda-117">Hola convenciones de archivos es mejor escenarios toothese adecuado:</span><span class="sxs-lookup"><span data-stu-id="4dfda-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="4dfda-118">Puede modificar fácilmente código de hello para la aplicación de Hola que la tarea está ejecutando archivos de toopersist con biblioteca de hello convenciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="4dfda-119">Desea toostream datos tooAzure almacenamiento mientras todavía se ejecuta la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="4dfda-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="4dfda-120">Desea que los datos de toopersist de los grupos creados con la configuración del servicio de nube de Hola o configuración de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dfda-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="4dfda-121">La aplicación cliente u otras tareas de hello toolocate de necesidades del trabajo y descargar los archivos de salida de tareas por Id. o por propósito.</span><span class="sxs-lookup"><span data-stu-id="4dfda-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="4dfda-122">Desea que el resultado de la tarea de tooview Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dfda-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="4dfda-123">Si su escenario difiere de los mencionados anteriormente, deberá tooconsider un enfoque diferente.</span><span class="sxs-lookup"><span data-stu-id="4dfda-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="4dfda-124">Para obtener más información sobre otras opciones para guardar resultado de la tarea, consulte [Persist trabajos y tareas de salida tooAzure almacenamiento](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="4dfda-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="4dfda-125">¿Qué es hello convenciones de archivo por lotes estándar?</span><span class="sxs-lookup"><span data-stu-id="4dfda-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="4dfda-126">Hola [estándar convenciones de archivo por lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) proporciona un esquema de nomenclatura para los contenedores de destino de Hola y toowhich de las rutas de acceso de blob se escriben los archivos de salida.</span><span class="sxs-lookup"><span data-stu-id="4dfda-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="4dfda-127">Archivos persistente tooAzure almacenamiento que se ajustan toohello archivo convenciones estándar están automáticamente disponibles para su visualización en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dfda-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="4dfda-128">portal de Hello es consciente de convención de nomenclatura de Hola y por lo que puede mostrar archivos que cumplen tooit.</span><span class="sxs-lookup"><span data-stu-id="4dfda-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="4dfda-129">biblioteca de convenciones de archivos de Hola para .NET nombres automáticamente a los contenedores de almacenamiento y los archivos de salida de tarea según toohello convenciones de archivo estándar.</span><span class="sxs-lookup"><span data-stu-id="4dfda-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="4dfda-130">biblioteca de convenciones de archivo Hello también proporciona métodos tooquery archivos de salida en el almacenamiento de Azure según toojob ID, Id. de tarea o propósito.</span><span class="sxs-lookup"><span data-stu-id="4dfda-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="4dfda-131">Si va a desarrollar con un lenguaje distinto de. NET, puede implementar por sí mismo Hola convenciones de archivo estándar en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4dfda-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="4dfda-132">Para obtener más información, consulte [sobre estándar de convenciones de archivo por lotes de hello](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="4dfda-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="4dfda-133">Vincular un tooyour de cuenta cuenta de lote de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="4dfda-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="4dfda-134">tooAzure de datos de salida de toopersist con biblioteca de hello convenciones de archivos de almacenamiento, primero debe vincular un tooyour de cuenta cuenta de lote de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dfda-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="4dfda-135">Si aún no lo ha hecho lo ha hecho, vincular un tooyour de cuenta de almacenamiento cuenta de lote mediante hello [portal de Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="4dfda-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="4dfda-136">Navegar por cuenta de lote tooyour Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dfda-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="4dfda-137">En **Configuración**, seleccione **Cuenta de Storage**.</span><span class="sxs-lookup"><span data-stu-id="4dfda-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="4dfda-138">Si no dispone de una cuenta de Storage asociada con su cuenta de Batch, haga clic en **Storage Account (None)** [Cuenta de Storage (ninguna)].</span><span class="sxs-lookup"><span data-stu-id="4dfda-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="4dfda-139">Seleccione una cuenta de almacenamiento de lista de Hola para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="4dfda-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="4dfda-140">Para obtener el mejor rendimiento, usar una cuenta de almacenamiento de Azure que se encuentra en hello misma región que Hola cuenta de lote donde se ejecutan las tareas.</span><span class="sxs-lookup"><span data-stu-id="4dfda-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="4dfda-141">Guardar datos de salida</span><span class="sxs-lookup"><span data-stu-id="4dfda-141">Persist output data</span></span>

<span data-ttu-id="4dfda-142">tarea y el trabajo de toopersist los datos con la biblioteca de hello convenciones de archivo de salida, crear un contenedor de almacenamiento de Azure, a continuación, guarde el contenedor de toohello de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="4dfda-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="4dfda-143">Hola de uso [biblioteca de cliente de almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage) en el contenedor de toohello tarea código tooupload Hola tarea salida.</span><span class="sxs-lookup"><span data-stu-id="4dfda-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="4dfda-144">Para más información sobre el trabajo con contenedores y blobs en Azure Storage, consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="4dfda-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="4dfda-145">Todas las salidas de trabajos y tareas se mantiene con biblioteca se almacenan en las convenciones de archivo Hola Hola mismo contenedor.</span><span class="sxs-lookup"><span data-stu-id="4dfda-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="4dfda-146">Si trata de un gran número de tareas toopersist archivos en hello mismo tiempo, [límites de limitación de almacenamiento](../storage/common/storage-performance-checklist.md#blobs) puede aplicarse.</span><span class="sxs-lookup"><span data-stu-id="4dfda-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="4dfda-147">Creación de contenedores de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4dfda-147">Create storage container</span></span>

<span data-ttu-id="4dfda-148">toopersist tarea salida tooAzure almacenamiento, crear primero un contenedor mediante una llamada a [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="4dfda-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="4dfda-149">Este método de extensión toma un objeto [CloudStorageAccount][net_cloudstorageaccount] como parámetro.</span><span class="sxs-lookup"><span data-stu-id="4dfda-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="4dfda-150">Crea un contenedor con nombre correspondiente toohello archivo convenciones estándar para que su contenido es reconocible de forma Hola métodos de recuperación hello y portal de Azure que se describe más adelante en el artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dfda-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="4dfda-151">Se coloca normalmente Hola código toocreate un contenedor en la aplicación cliente &mdash; Hola aplicación que crea los grupos, los trabajos y tareas.</span><span class="sxs-lookup"><span data-stu-id="4dfda-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="4dfda-152">Almacenamiento de las salidas de tarea</span><span class="sxs-lookup"><span data-stu-id="4dfda-152">Store task outputs</span></span>

<span data-ttu-id="4dfda-153">Ahora que ha preparado un contenedor de almacenamiento de Azure, las tareas pueden guardar el contenedor de salida toohello mediante hello [TaskOutputStorage] [ net_taskoutputstorage] clase encontrado en la biblioteca de convenciones de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dfda-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="4dfda-154">En el código de la tarea, cree primero un [TaskOutputStorage] [ net_taskoutputstorage] objeto, a continuación, cuando la tarea hello ha completado su trabajo, llame a hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] método toosave su almacenamiento tooAzure de salida.</span><span class="sxs-lookup"><span data-stu-id="4dfda-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="4dfda-155">Hola `kind` parámetro de hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) método clasifica Hola archivos persistentes.</span><span class="sxs-lookup"><span data-stu-id="4dfda-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="4dfda-156">Hay cuatro tipos predefinidos de [TaskOutputKind][net_taskoutputkind]: `TaskOutput`, `TaskPreview`, `TaskLog`, y `TaskIntermediate.`. También puede definir categorías personalizadas de salida.</span><span class="sxs-lookup"><span data-stu-id="4dfda-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="4dfda-157">Estos tipos de salida permiten toospecify qué tipo de salidas toolist cuando tarde realiza una consulta por lotes para hello conserva salidas de una tarea determinada.</span><span class="sxs-lookup"><span data-stu-id="4dfda-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="4dfda-158">En otras palabras, al enumerar salidas de Hola para una tarea, puede filtrar lista de hello en uno de los tipos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="4dfda-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="4dfda-159">Por ejemplo, "Deme hello *vista previa* de salida de tarea *109*."</span><span class="sxs-lookup"><span data-stu-id="4dfda-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="4dfda-160">Obtener más información sobre la lista y recuperar salidas aparece en [recuperar la salida](#retrieve-output) más adelante en el artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dfda-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="4dfda-161">Hello tipo de salida también determina dónde en hello Azure portal de un archivo determinado aparece: *TaskOutput*-archivos clasificados aparecen bajo **archivos de salida de la tarea**, y *TaskLog*archivos aparecen bajo **tareas registros**.</span><span class="sxs-lookup"><span data-stu-id="4dfda-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="4dfda-162">Almacenamiento de salidas de trabajos</span><span class="sxs-lookup"><span data-stu-id="4dfda-162">Store job outputs</span></span>

<span data-ttu-id="4dfda-163">Además resultados de las tareas de toostoring, puede almacenar salidas Hola asociados a un trabajo completo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="4dfda-164">Por ejemplo, en la tarea de mezcla de hello de un trabajo de procesamiento de la película, podría mantenerse película Hola totalmente representado como una salida de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="4dfda-165">Cuando se completa el trabajo, la aplicación cliente puede enumerar y recuperar salidas de hello para el trabajo de hello y no necesita tooquery Hola tareas individuales.</span><span class="sxs-lookup"><span data-stu-id="4dfda-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="4dfda-166">Almacenar la salida del trabajo por llamada hello [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] método y especifique hello [JobOutputKind] [ net_joboutputkind] y nombre de archivo:</span><span class="sxs-lookup"><span data-stu-id="4dfda-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="4dfda-167">Al igual que con hello **TaskOutputKind** tipo de resultados de tarea, usar hello [JobOutputKind] [ net_joboutputkind] toocategorize un trabajo de tipo de archivos persistentes.</span><span class="sxs-lookup"><span data-stu-id="4dfda-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="4dfda-168">Este parámetro le permite consultar toolater (lista) de un tipo específico de salida.</span><span class="sxs-lookup"><span data-stu-id="4dfda-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="4dfda-169">Hola **JobOutputKind** tipo incluye categorías de vista previa y de salida y admite la creación de categorías personalizadas.</span><span class="sxs-lookup"><span data-stu-id="4dfda-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="4dfda-170">Almacenamiento de los registros de tareas</span><span class="sxs-lookup"><span data-stu-id="4dfda-170">Store task logs</span></span>

<span data-ttu-id="4dfda-171">Además toopersisting un almacenamiento de información de archivo toodurable cuando una tarea o un trabajo se completa, puede que tenga archivos toopersist que se actualizan durante la ejecución de Hola de una tarea &mdash; archivos de registro o `stdout.txt` y `stderr.txt`, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="4dfda-172">Para este propósito, biblioteca de hello convenciones de archivos por lotes de Azure proporciona hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] método.</span><span class="sxs-lookup"><span data-stu-id="4dfda-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="4dfda-173">Con [SaveTrackedAsync][net_savetrackedasync], puede realizar un seguimiento de archivo de tooa de las actualizaciones en el nodo de hello (en un intervalo que especifique) y conservar esos tooAzure almacenamiento de las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="4dfda-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="4dfda-174">En el siguiente fragmento de código de hello, usamos [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` en el almacenamiento de Azure cada 15 segundos durante la ejecución de Hola de tarea hello:</span><span class="sxs-lookup"><span data-stu-id="4dfda-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="4dfda-175">sección de comentarios de Hola `Code tooprocess data and produce output file(s)` es un marcador de posición para el código de hello que normalmente realizaría la tarea.</span><span class="sxs-lookup"><span data-stu-id="4dfda-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="4dfda-176">Por ejemplo, es posible que tenga código que descargue datos desde Azure Storage y realice alguna transformación o cálculo en él.</span><span class="sxs-lookup"><span data-stu-id="4dfda-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="4dfda-177">parte importante de Hola de este fragmento de código demuestra cómo puede ajustar este código en un `using` tooperiodically bloque actualizar un archivo con [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="4dfda-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="4dfda-178">agente de nodo de Hello es un programa que se ejecuta en cada nodo de grupo de Hola y proporciona interfaz de comando y control de hello entre el nodo de Hola y el servicio por lotes Hola.</span><span class="sxs-lookup"><span data-stu-id="4dfda-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="4dfda-179">Hola `Task.Delay` llamada es necesaria al final de Hola de este `using` tooensure de bloque que Hola agente de nodo tiene contenido en tiempo de tooflush Hola del estándar toohello stdout.txt archivo en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dfda-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="4dfda-180">Sin este retraso, es posible toomiss Hola últimos segundos de salida.</span><span class="sxs-lookup"><span data-stu-id="4dfda-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="4dfda-181">Este retraso puede no ser necesario para todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="4dfda-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="4dfda-182">Al habilitar el archivo de seguimiento con **SaveTrackedAsync**, solo *anexa* archivo sometidas a seguimiento toohello son persistente tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4dfda-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="4dfda-183">Utilice este método sólo para el seguimiento de archivos de registro no girar u otros archivos que se escriben toowith anexar final de toohello de operaciones de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="4dfda-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="4dfda-184">Recuperación de datos de salidas</span><span class="sxs-lookup"><span data-stu-id="4dfda-184">Retrieve output data</span></span>

<span data-ttu-id="4dfda-185">Al recuperar la salida persistente con biblioteca de hello convenciones de archivos por lotes de Azure, puede hacerlo en forma centrado en tareas y trabajo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="4dfda-186">Puede solicitar Hola de salida para dada la tarea o trabajo sin necesidad de tooknow su ruta de acceso en el almacenamiento de Azure, o incluso su nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="4dfda-187">En su lugar, puede solicitar archivos de salida por el identificador de tarea o trabajo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="4dfda-188">Hello fragmento de código siguiente recorre en iteración las tareas de un trabajo, imprime información acerca de los archivos de salida de hello para la tarea hello y, a continuación, descarga los archivos desde el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4dfda-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="4dfda-189">Archivos de salida de la vista de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4dfda-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="4dfda-190">portal de Azure Hello muestra los archivos de salida de tarea y registros que son persistente tooa vinculan cuenta de almacenamiento de Azure mediante hello [estándar convenciones de archivo por lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="4dfda-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="4dfda-191">Puede implementar estas convenciones de hello un lenguaje de su elección, o puede usar biblioteca de hello convenciones de archivos en las aplicaciones. NET.</span><span class="sxs-lookup"><span data-stu-id="4dfda-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="4dfda-192">pantalla de hello tooenable los archivos de salida de portal de hello, debe cumplir Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="4dfda-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="4dfda-193">[Vincular una cuenta de almacenamiento de Azure](#requirement-linked-storage-account) tooyour cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="4dfda-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="4dfda-194">Cumplir las convenciones de nomenclatura toohello predefinida para los contenedores de almacenamiento y archivos al realizar la persistencia salidas.</span><span class="sxs-lookup"><span data-stu-id="4dfda-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="4dfda-195">Puede encontrar la definición de Hola de estas convenciones en biblioteca de convenciones de archivo hello [Léame][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="4dfda-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="4dfda-196">Si usas hello [convenciones de archivos por lotes de Azure] [ nuget_package] toopersist biblioteca su salida, los archivos se conservan según toohello convenciones de archivo estándar.</span><span class="sxs-lookup"><span data-stu-id="4dfda-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="4dfda-197">resultado de la tarea de tooview archivos y los registros en hello portal de Azure, navegue tarea toohello cuya salida que le interesen, a continuación, haga clic en **archivos de salida guardado** o **registros guardados**.</span><span class="sxs-lookup"><span data-stu-id="4dfda-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="4dfda-198">Esta imagen muestra hello **archivos de salida guardado** para la tarea hello con identificador "007":</span><span class="sxs-lookup"><span data-stu-id="4dfda-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="4dfda-199">![Resultados de las tareas hoja Hola portal de Azure][2]</span><span class="sxs-lookup"><span data-stu-id="4dfda-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="4dfda-200">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4dfda-200">Code sample</span></span>

<span data-ttu-id="4dfda-201">Hola [PersistOutputs] [ github_persistoutputs] proyecto de ejemplo es uno de hello [ejemplos de código de Azure Batch] [ github_samples] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="4dfda-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="4dfda-202">Esta solución de Visual Studio muestra cómo había salida toodurable almacenamiento de la tarea de toopersist de biblioteca de toouse Hola convenciones de archivos por lotes de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dfda-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="4dfda-203">Hola toorun de ejemplo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4dfda-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="4dfda-204">Proyecto abierto hello en **Visual Studio 2015 o versiones más recientes**.</span><span class="sxs-lookup"><span data-stu-id="4dfda-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="4dfda-205">Agregue el lote y el almacenamiento **las credenciales de cuentas** demasiado**AccountSettings.settings** en proyecto de Microsoft.Azure.Batch.Samples.Common Hola.</span><span class="sxs-lookup"><span data-stu-id="4dfda-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="4dfda-206">**Generar** (pero no podrán ejecutar) Hola solución.</span><span class="sxs-lookup"><span data-stu-id="4dfda-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="4dfda-207">Si se le solicita, restaure los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="4dfda-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="4dfda-208">Hola de uso tooupload portal Azure un [paquete de aplicación](batch-application-packages.md) para **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="4dfda-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="4dfda-209">Incluir hello `PersistOutputsTask.exe` y sus ensamblados dependientes en paquete de extensión .zip hello, identificador de la aplicación hello conjunto demasiado "PersistOutputsTask" y la aplicación hello empaquetar versión demasiado "1.0".</span><span class="sxs-lookup"><span data-stu-id="4dfda-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="4dfda-210">**Iniciar** Hola (ejecutar) **PersistOutputs** proyecto.</span><span class="sxs-lookup"><span data-stu-id="4dfda-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="4dfda-211">Cuando escriba toochoose solicitadas Hola persistencia tecnología toouse de ejecución ejemplo hello, **1** ejemplo de Hola a toorun con el resultado de la tarea de toopersist de biblioteca Hola convenciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4dfda-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4dfda-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="4dfda-213">Obtener la biblioteca de convenciones de archivo por lotes de Hola para .NET</span><span class="sxs-lookup"><span data-stu-id="4dfda-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="4dfda-214">biblioteca de convenciones de archivo por lotes de Hola para .NET está disponible en [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="4dfda-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="4dfda-215">biblioteca de Hello extiende hello [CloudJob] [ net_cloudjob] y [CloudTask] [ net_cloudtask] clases con nuevos métodos.</span><span class="sxs-lookup"><span data-stu-id="4dfda-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="4dfda-216">Consulte también hello [documentación de referencia](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) de la biblioteca de hello convenciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="4dfda-217">Hola [código fuente] [ github_file_conventions] para hello convenciones de archivo biblioteca está disponible en GitHub Hola SDK de Microsoft Azure para el repositorio. NET.</span><span class="sxs-lookup"><span data-stu-id="4dfda-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="4dfda-218">Exploración de otros métodos para guardar los datos de salida</span><span class="sxs-lookup"><span data-stu-id="4dfda-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="4dfda-219">Vea [Persist trabajos y tareas de salida tooAzure almacenamiento](batch-task-output.md) para obtener información general de conservar los datos de tarea y el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4dfda-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="4dfda-220">Vea [tooAzure de datos de tarea almacenamiento con hello API del servicio de lote se conservan](batch-task-output-files.md) toolearn toouse Hola API del servicio de lote toopersist cómo los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="4dfda-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Selectores de archivos de salida guardados y registros guardados en el portal"
[2]: ./media/batch-task-output/task-output-02.png "Resultados de las tareas hoja Hola portal de Azure"
