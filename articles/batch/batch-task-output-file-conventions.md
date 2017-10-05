---
title: 'Guardar salidas de trabajos y tareas en Azure Storage con la biblioteca de convenciones de archivo para .NET: Azure Batch | Microsoft Docs'
description: Aprenda a usar la biblioteca de convenciones de archivo para .NET de Azure Batch para guardar las salidas de trabajos y tareas en Azure Storage, y ver las salidas guardadas en Azure Portal.
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
ms.openlocfilehash: a9de327c20463469bc91d9720aa17333a36f919e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="persist-job-and-task-data-to-azure-storage-with-the-batch-file-conventions-library-for-net-to-persist"></a><span data-ttu-id="3da0b-103">Guardar datos de trabajos y tareas en Azure Storage con la biblioteca de convenciones de archivo para .NET</span><span class="sxs-lookup"><span data-stu-id="3da0b-103">Persist job and task data to Azure Storage with the Batch File Conventions library for .NET to persist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="3da0b-104">Una manera de guardar los datos de tareas consiste en usar la [biblioteca de convenciones de archivo para .NET de Azure Batch][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="3da0b-104">One way to persist task data is to use the [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="3da0b-105">La biblioteca de convenciones de archivo simplifica el proceso de almacenamiento de los datos de salida de tareas en Azure Storage y su recuperación posterior.</span><span class="sxs-lookup"><span data-stu-id="3da0b-105">The File Conventions library simplifies the process of storing task output data to Azure Storage and retrieving it.</span></span> <span data-ttu-id="3da0b-106">Puede usarla en el código de tarea y en el de cliente.&mdash;En el código de tarea, para almacenar los archivos y en el código de cliente, para mostrarlos y recuperarlos.</span><span class="sxs-lookup"><span data-stu-id="3da0b-106">You can use the File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code to list and retrieve them.</span></span> <span data-ttu-id="3da0b-107">El código de la tarea también puede usar la biblioteca para recuperar las salidas de las tareas precedentes de la cadena, como en un escenario con [dependencias entre tareas](batch-task-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="3da0b-107">Your task code can also use the library to retrieve the output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="3da0b-108">Para recuperar los archivos de salida con la biblioteca de convenciones de archivo, puede buscar los archivos de un trabajo o tarea determinados enumerándolos por identificador y finalidad.</span><span class="sxs-lookup"><span data-stu-id="3da0b-108">To retrieve output files with the File Conventions library, you can locate the files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="3da0b-109">No es necesario conocer los nombres o ubicaciones de los archivos.</span><span class="sxs-lookup"><span data-stu-id="3da0b-109">You don't need to know the names or locations of the files.</span></span> <span data-ttu-id="3da0b-110">Por ejemplo, puede usar la biblioteca de convenciones de archivo para mostrar todos los archivos intermedios de una tarea determinada u obtener un archivo de vista previa de un trabajo determinado.</span><span class="sxs-lookup"><span data-stu-id="3da0b-110">For example, you can use the File Conventions library to list all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="3da0b-111">Empezando por la versión del 1 de mayo de 2017, la API del servicio Batch permite guardar datos de salida en Azure Storage para tareas simples y tareas de administrador de trabajos que se ejecutan en los grupos creados con la configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3da0b-111">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools created with the virtual machine configuration.</span></span> <span data-ttu-id="3da0b-112">La API del servicio Batch proporciona una manera sencilla para guardar la salida desde dentro del código que permite crear una tarea y que actúa como una alternativa a la biblioteca de convenciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-112">The Batch service API provides a simple way to persist output from within the code that creates a task and serves as an alternative to the File Conventions library.</span></span> <span data-ttu-id="3da0b-113">Puede modificar las aplicaciones de cliente de Batch para guardar la salida sin necesidad de actualizar la aplicación que la tarea está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="3da0b-113">You can modify your Batch client applications to persist output without needing to update the application that your task is running.</span></span> <span data-ttu-id="3da0b-114">Para más información, consulte [Almacenamiento de datos de tareas en Azure Storage con la API del servicio Batch](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="3da0b-114">For more information, see [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-the-file-conventions-library-to-persist-task-output"></a><span data-ttu-id="3da0b-115">¿Cuándo se puede usar la biblioteca de convenciones de archivo para guardar salidas de tareas?</span><span class="sxs-lookup"><span data-stu-id="3da0b-115">When do I use the File Conventions library to persist task output?</span></span>

<span data-ttu-id="3da0b-116">Azure Batch proporciona más de una manera de guardar las salidas de tareas.</span><span class="sxs-lookup"><span data-stu-id="3da0b-116">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="3da0b-117">Las convenciones de archivo se adaptan mejor a estos escenarios:</span><span class="sxs-lookup"><span data-stu-id="3da0b-117">The File Conventions is best suited to these scenarios:</span></span>

- <span data-ttu-id="3da0b-118">Puede modificar fácilmente el código de la aplicación que la tarea está ejecutando para guardar los archivos mediante la biblioteca de convenciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-118">You can easily modify the code for the application that your task is running to persist files using the File Conventions library.</span></span>
- <span data-ttu-id="3da0b-119">Quiere transmitir datos a Azure Storage mientras la tarea está aún en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="3da0b-119">You want to stream data to Azure Storage while the task is still running.</span></span>
- <span data-ttu-id="3da0b-120">Quiere almacenar los datos de grupos creados con la configuración de servicios en la nube o la configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3da0b-120">You want to persist data from pools created with either the cloud service configuration or the virtual machine configuration.</span></span>
- <span data-ttu-id="3da0b-121">La aplicación cliente u otras tareas del trabajo deben encontrar y descargar los archivos de salida de tarea por identificador o finalidad.</span><span class="sxs-lookup"><span data-stu-id="3da0b-121">Your client application or other tasks in the job needs to locate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="3da0b-122">Quiere ver la salida de tarea en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3da0b-122">You want to view task output in the Azure portal.</span></span>

<span data-ttu-id="3da0b-123">Si su escenario es diferente de los mencionados anteriormente, considere la adopción de un enfoque diferente.</span><span class="sxs-lookup"><span data-stu-id="3da0b-123">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="3da0b-124">Para más información sobre otras opciones para guardar la salida de tareas, consulte [Guardar salidas de trabajos y tareas en Azure Storage](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="3da0b-124">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-the-batch-file-conventions-standard"></a><span data-ttu-id="3da0b-125">¿Qué es el estándar de convenciones de archivo de Batch?</span><span class="sxs-lookup"><span data-stu-id="3da0b-125">What is the Batch File Conventions standard?</span></span>

<span data-ttu-id="3da0b-126">El [estándar de convenciones de archivo de Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) proporciona un esquema de nombres para los contenedores de destino y las rutas de acceso de blob en los que se escriben los archivos de salida.</span><span class="sxs-lookup"><span data-stu-id="3da0b-126">The [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for the destination containers and blob paths to which your output files are written.</span></span> <span data-ttu-id="3da0b-127">Los archivos guardados en Azure Storage que cumplen el estándar de convenciones de archivo están automáticamente disponibles para su visualización en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3da0b-127">Files persisted to Azure Storage that adhere to the File Conventions standard are automatically available for viewing in the Azure portal.</span></span> <span data-ttu-id="3da0b-128">El portal es compatible con la convención de nomenclatura y, por eso, puede mostrar los archivos que lo cumplen.</span><span class="sxs-lookup"><span data-stu-id="3da0b-128">The portal is aware of the naming convention and so can display files that adhere to it.</span></span>

<span data-ttu-id="3da0b-129">La biblioteca de convenciones de archivo para .NET asigna automáticamente nombres a los contenedores de almacenamiento y a los archivos de salidas de tareas según el estándar de convenciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-129">The File Conventions library for .NET automatically names your storage containers and task output files according to the File Conventions standard.</span></span> <span data-ttu-id="3da0b-130">La biblioteca de convenciones de archivo también proporciona métodos para consultar los archivos de salida en Azure Storage según el identificador de trabajo, de tarea o la finalidad.</span><span class="sxs-lookup"><span data-stu-id="3da0b-130">The File Conventions library also provides methods to query output files in Azure Storage according to job ID, task ID, or purpose.</span></span>   

<span data-ttu-id="3da0b-131">Si va a desarrollar con un lenguaje distinto de. NET, puede implementar el estándar de convenciones de archivo en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="3da0b-131">If you are developing with a language other than .NET, you can implement the File Conventions standard yourself in your application.</span></span> <span data-ttu-id="3da0b-132">Para más información, consulte [Acerca del estándar de convenciones de archivo de Batch](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="3da0b-132">For more information, see [About the Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-to-your-batch-account"></a><span data-ttu-id="3da0b-133">Vinculación de una cuenta de Azure Storage a la cuenta de Batch</span><span class="sxs-lookup"><span data-stu-id="3da0b-133">Link an Azure Storage account to your Batch account</span></span>

<span data-ttu-id="3da0b-134">Para guardar los datos de salida en Azure Storage mediante la biblioteca de convenciones de archivo y poder verlos en Azure Portal, debe vincular primero una cuenta de Azure Storage a su cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="3da0b-134">To persist output data to Azure Storage using the File Conventions library, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="3da0b-135">Si aún no lo ha hecho, vincule una cuenta de Azure Storage a la cuenta de Batch mediante [Azure Portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="3da0b-135">If you haven't done so already, link a Storage account to your Batch account by using the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="3da0b-136">Vaya a la cuenta de Batch en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3da0b-136">Navigate to your Batch account in the Azure portal.</span></span> 
2. <span data-ttu-id="3da0b-137">En **Configuración**, seleccione **Cuenta de Storage**.</span><span class="sxs-lookup"><span data-stu-id="3da0b-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="3da0b-138">Si no dispone de una cuenta de Storage asociada con su cuenta de Batch, haga clic en **Storage Account (None)** [Cuenta de Storage (ninguna)].</span><span class="sxs-lookup"><span data-stu-id="3da0b-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="3da0b-139">Seleccione una cuenta de Storage de la lista para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="3da0b-139">Select a Storage account from the list for your subscription.</span></span> <span data-ttu-id="3da0b-140">Para obtener el mejor rendimiento, utilice una cuenta de Azure Storage que esté en la misma región que la cuenta de Batch en la que se ejecutan las tareas.</span><span class="sxs-lookup"><span data-stu-id="3da0b-140">For best performance, use an Azure Storage account that is in the same region as the Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="3da0b-141">Guardar datos de salida</span><span class="sxs-lookup"><span data-stu-id="3da0b-141">Persist output data</span></span>

<span data-ttu-id="3da0b-142">Para guardar los datos de salida de trabajos y tareas con la biblioteca de convenciones de archivo, cree un contenedor en Azure Storage y, a continuación, guarde la salida en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="3da0b-142">To persist job and task output data with the File Conventions library, create a container in Azure Storage, then save the output to the container.</span></span> <span data-ttu-id="3da0b-143">Use la [biblioteca de cliente de Azure Storage para .NET](https://www.nuget.org/packages/WindowsAzure.Storage) en el código de tarea para cargar la salida de la tarea en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="3da0b-143">Use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code to upload the task output to the container.</span></span> 

<span data-ttu-id="3da0b-144">Para más información sobre el trabajo con contenedores y blobs en Azure Storage, consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="3da0b-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="3da0b-145">Todas las salidas de trabajos y tareas guardados con la biblioteca de convenciones de archivo se almacenan en el mismo contenedor.</span><span class="sxs-lookup"><span data-stu-id="3da0b-145">All job and task outputs persisted with the File Conventions library are stored in the same container.</span></span> <span data-ttu-id="3da0b-146">Si un gran número de tareas intenta guardar archivos al mismo tiempo, se pueden aplicar [límites de almacenamiento](../storage/common/storage-performance-checklist.md#blobs).</span><span class="sxs-lookup"><span data-stu-id="3da0b-146">If a large number of tasks try to persist files at the same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="3da0b-147">Creación de contenedores de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3da0b-147">Create storage container</span></span>

<span data-ttu-id="3da0b-148">Para guardar las salidas de tareas en Azure Storage, primero cree un contenedor mediante una llamada a [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="3da0b-148">To persist task output to Azure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="3da0b-149">Este método de extensión toma un objeto [CloudStorageAccount][net_cloudstorageaccount] como parámetro.</span><span class="sxs-lookup"><span data-stu-id="3da0b-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="3da0b-150">Crea un contenedor denominado según el estándar convenciones de archivo, por lo que su contenido es reconocible para Azure Portal y los métodos de recuperación que se describen más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-150">It creates a container named according to the File Conventions standard,so that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span></span>

<span data-ttu-id="3da0b-151">Normalmente se coloca el código para crear un contenedor en la aplicación cliente &mdash;, la aplicación que crea los grupos, los trabajos y las tareas.</span><span class="sxs-lookup"><span data-stu-id="3da0b-151">You typically place the code to create a container in your client application &mdash; the application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference to the linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create the blob storage container for the outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="3da0b-152">Almacenamiento de las salidas de tarea</span><span class="sxs-lookup"><span data-stu-id="3da0b-152">Store task outputs</span></span>

<span data-ttu-id="3da0b-153">Ahora que ha preparado un contenedor en Azure Storage, las tareas pueden guardar las salidas en el contenedor mediante la clase [TaskOutputStorage][net_taskoutputstorage] que se encuentra en la biblioteca de convenciones de archivos.</span><span class="sxs-lookup"><span data-stu-id="3da0b-153">Now that you've prepared a container in Azure Storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the File Conventions library.</span></span>

<span data-ttu-id="3da0b-154">En el código de la tarea, cree primero un objeto [TaskOutputStorage][net_taskoutputstorage] y, luego, cuando la tarea haya finalizado su trabajo, llame al método [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] para guardar su salida en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3da0b-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code to process data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="3da0b-155">El parámetro `kind` del método [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) permite clasificar los archivos guardados.</span><span class="sxs-lookup"><span data-stu-id="3da0b-155">The `kind` parameter of the [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes the persisted files.</span></span> <span data-ttu-id="3da0b-156">Hay cuatro tipos predefinidos de [TaskOutputKind][net_taskoutputkind]: `TaskOutput`, `TaskPreview`, `TaskLog`, y `TaskIntermediate.`. También puede definir categorías personalizadas de salida.</span><span class="sxs-lookup"><span data-stu-id="3da0b-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="3da0b-157">Estos tipos de salidas le permiten especificar qué tipo de salidas se deben mostrar cuándo se realiza una consulta a Lote relacionada con las salidas guardadas de una tarea dada.</span><span class="sxs-lookup"><span data-stu-id="3da0b-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span></span> <span data-ttu-id="3da0b-158">En otras palabras, cuando muestra las salidas de una tarea, puede filtrar la lista por uno de los tipos de salida.</span><span class="sxs-lookup"><span data-stu-id="3da0b-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span></span> <span data-ttu-id="3da0b-159">Por ejemplo, "dame la salida *preview* de la tarea *109*".</span><span class="sxs-lookup"><span data-stu-id="3da0b-159">For example, "Give me the *preview* output for task *109*."</span></span> <span data-ttu-id="3da0b-160">Aparece más información sobre la presentación y recuperación de salidas en la sección [Recuperación de salidas](#retrieve-output) más adelante en el artículo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span></span>

> [!TIP]
> <span data-ttu-id="3da0b-161">La variante de salida también determina en qué lugar de Azure Portal aparece un archivo determinado. Los archivos categorizados como *TaskOutput* aparecen en **Archivos de salida de tarea**, y los archivos *TaskLog*, en **Registros de tareas**.</span><span class="sxs-lookup"><span data-stu-id="3da0b-161">The output kind also determines where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="3da0b-162">Almacenamiento de salidas de trabajos</span><span class="sxs-lookup"><span data-stu-id="3da0b-162">Store job outputs</span></span>

<span data-ttu-id="3da0b-163">Además de almacenar las salidas de tareas, puede almacenar las salidas asociadas a un trabajo completo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span></span> <span data-ttu-id="3da0b-164">Por ejemplo, en la tarea de combinación de un trabajo de representación de una película, podría guardar la película totalmente representada como una salida de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span></span> <span data-ttu-id="3da0b-165">Cuando se completa el trabajo, la aplicación cliente puede mostrar y recuperar las salidas del trabajo y no es necesario consultar las tareas individuales.</span><span class="sxs-lookup"><span data-stu-id="3da0b-165">When your job is completed, your client application can list and retrieve the outputs for the job, and does not need to query the individual tasks.</span></span>

<span data-ttu-id="3da0b-166">Almacene la salida del trabajo mediante una llamada al método [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] y especifique el [JobOutputKind][net_joboutputkind] y el nombre de archivo:</span><span class="sxs-lookup"><span data-stu-id="3da0b-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="3da0b-167">Al igual que con el tipo **TaskOutputKind** para las salidas de tareas, utilice el tipo [JobOutputKind][net_joboutputkind] para clasificar los archivos guardados de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-167">As with the **TaskOutputKind** type for task outputs, you use the [JobOutputKind][net_joboutputkind] type to categorize a job's persisted files.</span></span> <span data-ttu-id="3da0b-168">Este parámetro permite realizar consultas posteriores (mostrar) para un tipo específico de salida.</span><span class="sxs-lookup"><span data-stu-id="3da0b-168">This parameter allows you to later query for (list) a specific type of output.</span></span> <span data-ttu-id="3da0b-169">El tipo **JobOutputKind** incluye las categorías de salida y de vista previa y admite la creación de categorías personalizadas.</span><span class="sxs-lookup"><span data-stu-id="3da0b-169">The **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="3da0b-170">Almacenamiento de los registros de tareas</span><span class="sxs-lookup"><span data-stu-id="3da0b-170">Store task logs</span></span>

<span data-ttu-id="3da0b-171">Además de guardar un archivo en un almacenamiento duradero cuando se completa una tarea o trabajo, es posible que necesite guardar los archivos que se actualizan durante la ejecución de una tarea, los archivos de registro de &mdash;, o `stdout.txt` y `stderr.txt`, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-171">In addition to persisting a file to durable storage when a task or job completes, you may need to persist files that are updated during the execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="3da0b-172">Para ello, la biblioteca Azure Batch File Conventions proporciona el método [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="3da0b-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="3da0b-173">Con [SaveTrackedAsync][net_savetrackedasync], puede realizar un seguimiento de las actualizaciones de un archivo del nodo (durante un intervalo especificado) y almacenar esas actualizaciones en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3da0b-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span></span>

<span data-ttu-id="3da0b-174">En el siguiente fragmento de código, utilizamos [SaveTrackedAsync][net_savetrackedasync] para actualizar `stdout.txt` en Azure Storage cada 15 segundos durante la ejecución de la tarea:</span><span class="sxs-lookup"><span data-stu-id="3da0b-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// The primary task logic is wrapped in a using statement that sends updates to
// the stdout.txt blob in Storage every 15 seconds while the task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code to process data and produce output file(s) */

    // We are tracking the disk file to save our standard output, but the
    // node agent may take up to 3 seconds to flush the stdout stream to
    // disk. So give the file a moment to catch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="3da0b-175">La sección comentada `Code to process data and produce output file(s)` es simplemente un marcador de posición para el código que normalmente realizaría la tarea.</span><span class="sxs-lookup"><span data-stu-id="3da0b-175">The commented section `Code to process data and produce output file(s)` is a placeholder for the code that your task would normally perform.</span></span> <span data-ttu-id="3da0b-176">Por ejemplo, es posible que tenga código que descargue datos desde Azure Storage y realice alguna transformación o cálculo en él.</span><span class="sxs-lookup"><span data-stu-id="3da0b-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="3da0b-177">La parte importante de este fragmento de código demuestra cómo puede encapsular ese código en un bloque `using` para actualizar periódicamente un archivo con [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="3da0b-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="3da0b-178">El agente de nodo es un programa que se ejecuta en cada nodo del grupo y proporciona la interfaz de comandos y control entre el nodo y el servicio Batch.</span><span class="sxs-lookup"><span data-stu-id="3da0b-178">The node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="3da0b-179">Se necesita la llamada `Task.Delay` al final de este bloque `using` para asegurarse de que el agente de nodo tiene tiempo de vaciar el contenido de la salida estándar en el archivo stdout.txt del nodo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-179">The `Task.Delay` call is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node.</span></span> <span data-ttu-id="3da0b-180">Sin este retraso, es posible que se pierdan los últimos segundos de salida.</span><span class="sxs-lookup"><span data-stu-id="3da0b-180">Without this delay, it is possible to miss the last few seconds of output.</span></span> <span data-ttu-id="3da0b-181">Este retraso puede no ser necesario para todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="3da0b-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="3da0b-182">Si habilita el seguimiento de archivos con **SaveTrackedAsync**, solo se guardan en Azure Storage los *anexos* al archivo de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="3da0b-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* to the tracked file are persisted to Azure Storage.</span></span> <span data-ttu-id="3da0b-183">Utilice este método solo para el seguimiento de archivos de registro no rotatorios u otros archivos escritos con operaciones de anexión al final del archivo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-183">Use this method only for tracking non-rotating log files or other files that are written to with append operations to the end of the file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="3da0b-184">Recuperación de datos de salidas</span><span class="sxs-lookup"><span data-stu-id="3da0b-184">Retrieve output data</span></span>

<span data-ttu-id="3da0b-185">Cuando recupera la salida guardada mediante la biblioteca de convenciones de archivos de Lote de Azure, lo hace basándose en las tareas y trabajos.</span><span class="sxs-lookup"><span data-stu-id="3da0b-185">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="3da0b-186">Puede solicitar la salida de una tarea o trabajo determinado sin necesidad de conocer su ruta de acceso en Azure Storage o incluso sin conocer el nombre del archivo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-186">You can request the output for given task or job without needing to know its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="3da0b-187">En su lugar, puede solicitar archivos de salida por el identificador de tarea o trabajo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="3da0b-188">El fragmento de código siguiente procesa una iteración de las tareas de un trabajo, imprime información sobre los archivos de salida de la tarea y luego descarga los archivos desde Storage.</span><span class="sxs-lookup"><span data-stu-id="3da0b-188">The following code snippet iterates through a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span></span>

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

## <a name="view-output-files-in-the-azure-portal"></a><span data-ttu-id="3da0b-189">Visualización de archivos de salida en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3da0b-189">View output files in the Azure portal</span></span>

<span data-ttu-id="3da0b-190">Azure Portal muestra los archivos de salidas y los registros de las tareas que se guardan en una cuenta de Azure Storage vinculada mediante el [estándar de convenciones de archivo de Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="3da0b-190">The Azure portal displays task output files and logs that are persisted to a linked Azure Storage account using the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="3da0b-191">Puede implementar usted mismo estas convenciones en un lenguaje de su elección, o puede usar la biblioteca de convenciones de archivo en las aplicaciones. NET.</span><span class="sxs-lookup"><span data-stu-id="3da0b-191">You can implement these conventions yourself in the a language of your choice, or you can use the File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="3da0b-192">Para habilitar la presentación de los archivos de salidas en el portal, debe cumplir con los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="3da0b-192">To enable the display of your output files in the portal, you must satisfy the following requirements:</span></span>

1. <span data-ttu-id="3da0b-193">[Vincular una cuenta de Almacenamiento de Azure](#requirement-linked-storage-account) a la cuenta de Lote.</span><span class="sxs-lookup"><span data-stu-id="3da0b-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span></span>
2. <span data-ttu-id="3da0b-194">Cumplir las convenciones de nomenclatura predefinidas para los contenedores y archivos de almacenamiento al guardar salidas.</span><span class="sxs-lookup"><span data-stu-id="3da0b-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="3da0b-195">Puede encontrar la definición de estas convenciones en el archivo [LÉAME][github_file_conventions_readme] de la biblioteca de convenciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-195">You can find the definition of these conventions in the File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="3da0b-196">Si utiliza la biblioteca de [convenciones de archivo de Azure Batch][nuget_package] para guardar la salida, los archivos se guardarán según el estándar de convenciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, your files are persisted according to the File Conventions standard.</span></span>

<span data-ttu-id="3da0b-197">Para ver los archivos de salidas y registros de las tareas en Azure Portal, navegue hasta la tarea en cuya salida está interesado y, después, haga clic en **Archivos de salida guardados** o **Registros guardados**.</span><span class="sxs-lookup"><span data-stu-id="3da0b-197">To view task output files and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="3da0b-198">Esta imagen muestra los **archivos de salida guardados** para la tarea con identificador "007":</span><span class="sxs-lookup"><span data-stu-id="3da0b-198">This image shows the **Saved output files** for the task with ID "007":</span></span>

<span data-ttu-id="3da0b-199">![Hoja de salidas de tareas de Azure Portal][2]</span><span class="sxs-lookup"><span data-stu-id="3da0b-199">![Task outputs blade in the Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="3da0b-200">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3da0b-200">Code sample</span></span>

<span data-ttu-id="3da0b-201">El proyecto de ejemplo [PersistOutputs][github_persistoutputs] es uno de los ejemplos de código de [Azure Batch][github_samples] de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3da0b-201">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="3da0b-202">Esta solución de Visual Studio muestra cómo utilizar la biblioteca de convenciones de archivos de Azure Batch para guardar la salida de las tareas en un almacenamiento duradero.</span><span class="sxs-lookup"><span data-stu-id="3da0b-202">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span></span> <span data-ttu-id="3da0b-203">Para ejecutar el ejemplo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3da0b-203">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="3da0b-204">Abra el proyecto en **Visual Studio 2015 o una versión más reciente**.</span><span class="sxs-lookup"><span data-stu-id="3da0b-204">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="3da0b-205">Agregue las **credenciales de cuenta** de Batch y Storage a **AccountSettings.settings** al proyecto Microsoft.Azure.Batch.Samples.Common.</span><span class="sxs-lookup"><span data-stu-id="3da0b-205">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="3da0b-206">**Compile** (pero no ejecute) la solución.</span><span class="sxs-lookup"><span data-stu-id="3da0b-206">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="3da0b-207">Si se le solicita, restaure los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="3da0b-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="3da0b-208">Use el Portal de Azure para cargar un [paquete de aplicación](batch-application-packages.md) para **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="3da0b-208">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="3da0b-209">Incluya el archivo `PersistOutputsTask.exe` y los ensamblados dependientes en el paquete zip, establezca el identificador de la aplicación en "PersistOutputsTask" y la versión del paquete de aplicación en "1.0".</span><span class="sxs-lookup"><span data-stu-id="3da0b-209">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="3da0b-210">**Inicie** (ejecute) el proyecto**PersistOutputs**.</span><span class="sxs-lookup"><span data-stu-id="3da0b-210">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="3da0b-211">Cuando se le solicite que elija la tecnología de guardado que desea usar para ejecutar el ejemplo, escriba **1** para ejecutarlo mediante la biblioteca de convenciones de archivo para guardar la salida de la tarea.</span><span class="sxs-lookup"><span data-stu-id="3da0b-211">When prompted to choose the persistence technology to use for running the sample, enter **1** to run the sample using the File Conventions library to persist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3da0b-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3da0b-212">Next steps</span></span>

### <a name="get-the-batch-file-conventions-library-for-net"></a><span data-ttu-id="3da0b-213">Obtención de la biblioteca de convenciones de archivo para .NET de Batch</span><span class="sxs-lookup"><span data-stu-id="3da0b-213">Get the Batch File Conventions library for .NET</span></span>

<span data-ttu-id="3da0b-214">Esta biblioteca está disponible en [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="3da0b-214">The Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="3da0b-215">La biblioteca permite extender las clases [CloudJob][net_cloudjob] y [CloudTask][net_cloudtask] con nuevos métodos.</span><span class="sxs-lookup"><span data-stu-id="3da0b-215">The library extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="3da0b-216">Consulte también la [documentación de referencia](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) de la biblioteca de convenciones de archivo.</span><span class="sxs-lookup"><span data-stu-id="3da0b-216">Also see the [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for the File Conventions library.</span></span>

<span data-ttu-id="3da0b-217">Puede encontrar el [código fuente][github_file_conventions] de la biblioteca de convenciones de archivo en GitHub en el repositorio del Microsoft Azure SDK para .NET.</span><span class="sxs-lookup"><span data-stu-id="3da0b-217">The [source code][github_file_conventions] for the File Conventions library is available on GitHub in the Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="3da0b-218">Exploración de otros métodos para guardar los datos de salida</span><span class="sxs-lookup"><span data-stu-id="3da0b-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="3da0b-219">Consulte [Guardar salidas de trabajos y tareas en Azure Storage](batch-task-output.md) para obtener información general sobre cómo guardar datos de tareas y trabajos.</span><span class="sxs-lookup"><span data-stu-id="3da0b-219">See [Persist job and task output to Azure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="3da0b-220">Consulte [Almacenamiento de datos de tareas en Azure Storage con la API del servicio Batch](batch-task-output-files.md) para aprender a usar la API del servicio Batch para guardar los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="3da0b-220">See [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md) to learn how to use the Batch service API to persist output data.</span></span>

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
[2]: ./media/batch-task-output/task-output-02.png "Hoja de salidas de tareas de Azure Portal"
