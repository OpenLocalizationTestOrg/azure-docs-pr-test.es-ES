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
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>Conservar el trabajo y tareas tooAzure almacenamiento de datos con la biblioteca de convenciones de archivo por lotes de Hola para .NET toopersist 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Datos de la tarea de toopersist unidireccional están hello de toouse [biblioteca convenciones de archivos por lotes de Azure para .NET][nuget_package]. Hello biblioteca convenciones de archivos simplifica el proceso de Hola de almacenar el resultado de la tarea tooAzure almacenamiento de datos y recuperarlos. Puede usar Hola convenciones archivos biblioteca en código de cliente y de tarea &mdash; en código de la tarea para guardar archivos y en el cliente toolist de código y recuperarlos. El código de la tarea también puede utilizar salida de hello tooretrieve Hola de biblioteca de tareas de nivel superior, como en un [las dependencias entre tareas](batch-task-dependencies.md) escenario. 

tooretrieve archivos con la biblioteca de hello convenciones de archivo de salida, puede encontrar archivos de Hola para un determinado trabajo o tarea enumerándolos por identificador y el propósito. No es necesario tooknow los nombres de Hola o ubicaciones de archivos de Hola. Por ejemplo, puede usar todos los archivos intermedios de toolist de biblioteca de hello convenciones de archivo para una tarea determinada u obtener un archivo de vista previa de un trabajo determinado.

> [!TIP]
> A partir de la versión de 2017-05-01, Hola API del servicio por lotes admite tooAzure de datos de persistencia salida almacenamiento tareas y tareas de administrador de trabajos que se ejecutan en los grupos creados con la configuración de máquina virtual de Hola. Hola API del servicio de lote proporciona una toopersist de manera sencilla de salida desde dentro del código de hello que crea una tarea y actúa como una biblioteca de convenciones de archivo toohello alternativo. Puede modificar el resultado de toopersist de las aplicaciones de cliente de lote sin necesidad de aplicación de hello tooupdate que se ejecuta la tarea. Para obtener más información, consulte [tooAzure de datos de tarea almacenamiento con hello API del servicio de lote se conservan](batch-task-output-files.md).
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>¿Cuándo se puede utilizar el resultado de la tarea de toopersist de biblioteca Hola convenciones de archivo?

Lote de Azure proporciona toopersist más de una manera de resultado de la tarea. Hola convenciones de archivos es mejor escenarios toothese adecuado:

- Puede modificar fácilmente código de hello para la aplicación de Hola que la tarea está ejecutando archivos de toopersist con biblioteca de hello convenciones de archivo.
- Desea toostream datos tooAzure almacenamiento mientras todavía se ejecuta la tarea hello.
- Desea que los datos de toopersist de los grupos creados con la configuración del servicio de nube de Hola o configuración de máquina virtual de Hola.
- La aplicación cliente u otras tareas de hello toolocate de necesidades del trabajo y descargar los archivos de salida de tareas por Id. o por propósito. 
- Desea que el resultado de la tarea de tooview Hola portal de Azure.

Si su escenario difiere de los mencionados anteriormente, deberá tooconsider un enfoque diferente. Para obtener más información sobre otras opciones para guardar resultado de la tarea, consulte [Persist trabajos y tareas de salida tooAzure almacenamiento](batch-task-output.md). 

## <a name="what-is-hello-batch-file-conventions-standard"></a>¿Qué es hello convenciones de archivo por lotes estándar?

Hola [estándar convenciones de archivo por lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) proporciona un esquema de nomenclatura para los contenedores de destino de Hola y toowhich de las rutas de acceso de blob se escriben los archivos de salida. Archivos persistente tooAzure almacenamiento que se ajustan toohello archivo convenciones estándar están automáticamente disponibles para su visualización en hello portal de Azure. portal de Hello es consciente de convención de nomenclatura de Hola y por lo que puede mostrar archivos que cumplen tooit.

biblioteca de convenciones de archivos de Hola para .NET nombres automáticamente a los contenedores de almacenamiento y los archivos de salida de tarea según toohello convenciones de archivo estándar. biblioteca de convenciones de archivo Hello también proporciona métodos tooquery archivos de salida en el almacenamiento de Azure según toojob ID, Id. de tarea o propósito.   

Si va a desarrollar con un lenguaje distinto de. NET, puede implementar por sí mismo Hola convenciones de archivo estándar en la aplicación. Para obtener más información, consulte [sobre estándar de convenciones de archivo por lotes de hello](batch-task-output.md#about-the-batch-file-conventions-standard).

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>Vincular un tooyour de cuenta cuenta de lote de almacenamiento de Azure

tooAzure de datos de salida de toopersist con biblioteca de hello convenciones de archivos de almacenamiento, primero debe vincular un tooyour de cuenta cuenta de lote de almacenamiento de Azure. Si aún no lo ha hecho lo ha hecho, vincular un tooyour de cuenta de almacenamiento cuenta de lote mediante hello [portal de Azure](https://portal.azure.com):

1. Navegar por cuenta de lote tooyour Hola portal de Azure. 
2. En **Configuración**, seleccione **Cuenta de Storage**.
3. Si no dispone de una cuenta de Storage asociada con su cuenta de Batch, haga clic en **Storage Account (None)** [Cuenta de Storage (ninguna)].
4. Seleccione una cuenta de almacenamiento de lista de Hola para su suscripción. Para obtener el mejor rendimiento, usar una cuenta de almacenamiento de Azure que se encuentra en hello misma región que Hola cuenta de lote donde se ejecutan las tareas.

## <a name="persist-output-data"></a>Guardar datos de salida

tarea y el trabajo de toopersist los datos con la biblioteca de hello convenciones de archivo de salida, crear un contenedor de almacenamiento de Azure, a continuación, guarde el contenedor de toohello de salida de hello. Hola de uso [biblioteca de cliente de almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage) en el contenedor de toohello tarea código tooupload Hola tarea salida. 

Para más información sobre el trabajo con contenedores y blobs en Azure Storage, consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

> [!WARNING]
> Todas las salidas de trabajos y tareas se mantiene con biblioteca se almacenan en las convenciones de archivo Hola Hola mismo contenedor. Si trata de un gran número de tareas toopersist archivos en hello mismo tiempo, [límites de limitación de almacenamiento](../storage/common/storage-performance-checklist.md#blobs) puede aplicarse.
> 
> 

### <a name="create-storage-container"></a>Creación de contenedores de almacenamiento

toopersist tarea salida tooAzure almacenamiento, crear primero un contenedor mediante una llamada a [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]. Este método de extensión toma un objeto [CloudStorageAccount][net_cloudstorageaccount] como parámetro. Crea un contenedor con nombre correspondiente toohello archivo convenciones estándar para que su contenido es reconocible de forma Hola métodos de recuperación hello y portal de Azure que se describe más adelante en el artículo de Hola.

Se coloca normalmente Hola código toocreate un contenedor en la aplicación cliente &mdash; Hola aplicación que crea los grupos, los trabajos y tareas.

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

### <a name="store-task-outputs"></a>Almacenamiento de las salidas de tarea

Ahora que ha preparado un contenedor de almacenamiento de Azure, las tareas pueden guardar el contenedor de salida toohello mediante hello [TaskOutputStorage] [ net_taskoutputstorage] clase encontrado en la biblioteca de convenciones de archivos de Hola.

En el código de la tarea, cree primero un [TaskOutputStorage] [ net_taskoutputstorage] objeto, a continuación, cuando la tarea hello ha completado su trabajo, llame a hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] método toosave su almacenamiento tooAzure de salida.

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

Hola `kind` parámetro de hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) método clasifica Hola archivos persistentes. Hay cuatro tipos predefinidos de [TaskOutputKind][net_taskoutputkind]: `TaskOutput`, `TaskPreview`, `TaskLog`, y `TaskIntermediate.`. También puede definir categorías personalizadas de salida.

Estos tipos de salida permiten toospecify qué tipo de salidas toolist cuando tarde realiza una consulta por lotes para hello conserva salidas de una tarea determinada. En otras palabras, al enumerar salidas de Hola para una tarea, puede filtrar lista de hello en uno de los tipos de salida de hello. Por ejemplo, "Deme hello *vista previa* de salida de tarea *109*." Obtener más información sobre la lista y recuperar salidas aparece en [recuperar la salida](#retrieve-output) más adelante en el artículo de Hola.

> [!TIP]
> Hello tipo de salida también determina dónde en hello Azure portal de un archivo determinado aparece: *TaskOutput*-archivos clasificados aparecen bajo **archivos de salida de la tarea**, y *TaskLog*archivos aparecen bajo **tareas registros**.
> 
> 

### <a name="store-job-outputs"></a>Almacenamiento de salidas de trabajos

Además resultados de las tareas de toostoring, puede almacenar salidas Hola asociados a un trabajo completo. Por ejemplo, en la tarea de mezcla de hello de un trabajo de procesamiento de la película, podría mantenerse película Hola totalmente representado como una salida de trabajo. Cuando se completa el trabajo, la aplicación cliente puede enumerar y recuperar salidas de hello para el trabajo de hello y no necesita tooquery Hola tareas individuales.

Almacenar la salida del trabajo por llamada hello [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] método y especifique hello [JobOutputKind] [ net_joboutputkind] y nombre de archivo:

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

Al igual que con hello **TaskOutputKind** tipo de resultados de tarea, usar hello [JobOutputKind] [ net_joboutputkind] toocategorize un trabajo de tipo de archivos persistentes. Este parámetro le permite consultar toolater (lista) de un tipo específico de salida. Hola **JobOutputKind** tipo incluye categorías de vista previa y de salida y admite la creación de categorías personalizadas.

### <a name="store-task-logs"></a>Almacenamiento de los registros de tareas

Además toopersisting un almacenamiento de información de archivo toodurable cuando una tarea o un trabajo se completa, puede que tenga archivos toopersist que se actualizan durante la ejecución de Hola de una tarea &mdash; archivos de registro o `stdout.txt` y `stderr.txt`, por ejemplo. Para este propósito, biblioteca de hello convenciones de archivos por lotes de Azure proporciona hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] método. Con [SaveTrackedAsync][net_savetrackedasync], puede realizar un seguimiento de archivo de tooa de las actualizaciones en el nodo de hello (en un intervalo que especifique) y conservar esos tooAzure almacenamiento de las actualizaciones.

En el siguiente fragmento de código de hello, usamos [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` en el almacenamiento de Azure cada 15 segundos durante la ejecución de Hola de tarea hello:

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

sección de comentarios de Hola `Code tooprocess data and produce output file(s)` es un marcador de posición para el código de hello que normalmente realizaría la tarea. Por ejemplo, es posible que tenga código que descargue datos desde Azure Storage y realice alguna transformación o cálculo en él. parte importante de Hola de este fragmento de código demuestra cómo puede ajustar este código en un `using` tooperiodically bloque actualizar un archivo con [SaveTrackedAsync][net_savetrackedasync].

agente de nodo de Hello es un programa que se ejecuta en cada nodo de grupo de Hola y proporciona interfaz de comando y control de hello entre el nodo de Hola y el servicio por lotes Hola. Hola `Task.Delay` llamada es necesaria al final de Hola de este `using` tooensure de bloque que Hola agente de nodo tiene contenido en tiempo de tooflush Hola del estándar toohello stdout.txt archivo en el nodo de Hola. Sin este retraso, es posible toomiss Hola últimos segundos de salida. Este retraso puede no ser necesario para todos los archivos.

> [!NOTE]
> Al habilitar el archivo de seguimiento con **SaveTrackedAsync**, solo *anexa* archivo sometidas a seguimiento toohello son persistente tooAzure almacenamiento. Utilice este método sólo para el seguimiento de archivos de registro no girar u otros archivos que se escriben toowith anexar final de toohello de operaciones de archivo hello.
> 
> 

## <a name="retrieve-output-data"></a>Recuperación de datos de salidas

Al recuperar la salida persistente con biblioteca de hello convenciones de archivos por lotes de Azure, puede hacerlo en forma centrado en tareas y trabajo. Puede solicitar Hola de salida para dada la tarea o trabajo sin necesidad de tooknow su ruta de acceso en el almacenamiento de Azure, o incluso su nombre de archivo. En su lugar, puede solicitar archivos de salida por el identificador de tarea o trabajo.

Hello fragmento de código siguiente recorre en iteración las tareas de un trabajo, imprime información acerca de los archivos de salida de hello para la tarea hello y, a continuación, descarga los archivos desde el almacenamiento.

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

## <a name="view-output-files-in-hello-azure-portal"></a>Archivos de salida de la vista de hello portal de Azure

portal de Azure Hello muestra los archivos de salida de tarea y registros que son persistente tooa vinculan cuenta de almacenamiento de Azure mediante hello [estándar convenciones de archivo por lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Puede implementar estas convenciones de hello un lenguaje de su elección, o puede usar biblioteca de hello convenciones de archivos en las aplicaciones. NET.

pantalla de hello tooenable los archivos de salida de portal de hello, debe cumplir Hola según los requisitos:

1. [Vincular una cuenta de almacenamiento de Azure](#requirement-linked-storage-account) tooyour cuenta de lote.
2. Cumplir las convenciones de nomenclatura toohello predefinida para los contenedores de almacenamiento y archivos al realizar la persistencia salidas. Puede encontrar la definición de Hola de estas convenciones en biblioteca de convenciones de archivo hello [Léame][github_file_conventions_readme]. Si usas hello [convenciones de archivos por lotes de Azure] [ nuget_package] toopersist biblioteca su salida, los archivos se conservan según toohello convenciones de archivo estándar.

resultado de la tarea de tooview archivos y los registros en hello portal de Azure, navegue tarea toohello cuya salida que le interesen, a continuación, haga clic en **archivos de salida guardado** o **registros guardados**. Esta imagen muestra hello **archivos de salida guardado** para la tarea hello con identificador "007":

![Resultados de las tareas hoja Hola portal de Azure][2]

## <a name="code-sample"></a>Código de ejemplo

Hola [PersistOutputs] [ github_persistoutputs] proyecto de ejemplo es uno de hello [ejemplos de código de Azure Batch] [ github_samples] en GitHub. Esta solución de Visual Studio muestra cómo había salida toodurable almacenamiento de la tarea de toopersist de biblioteca de toouse Hola convenciones de archivos por lotes de Azure. Hola toorun de ejemplo, siga estos pasos:

1. Proyecto abierto hello en **Visual Studio 2015 o versiones más recientes**.
2. Agregue el lote y el almacenamiento **las credenciales de cuentas** demasiado**AccountSettings.settings** en proyecto de Microsoft.Azure.Batch.Samples.Common Hola.
3. **Generar** (pero no podrán ejecutar) Hola solución. Si se le solicita, restaure los paquetes NuGet.
4. Hola de uso tooupload portal Azure un [paquete de aplicación](batch-application-packages.md) para **PersistOutputsTask**. Incluir hello `PersistOutputsTask.exe` y sus ensamblados dependientes en paquete de extensión .zip hello, identificador de la aplicación hello conjunto demasiado "PersistOutputsTask" y la aplicación hello empaquetar versión demasiado "1.0".
5. **Iniciar** Hola (ejecutar) **PersistOutputs** proyecto.
6. Cuando escriba toochoose solicitadas Hola persistencia tecnología toouse de ejecución ejemplo hello, **1** ejemplo de Hola a toorun con el resultado de la tarea de toopersist de biblioteca Hola convenciones de archivo. 

## <a name="next-steps"></a>Pasos siguientes

### <a name="get-hello-batch-file-conventions-library-for-net"></a>Obtener la biblioteca de convenciones de archivo por lotes de Hola para .NET

biblioteca de convenciones de archivo por lotes de Hola para .NET está disponible en [NuGet][nuget_package]. biblioteca de Hello extiende hello [CloudJob] [ net_cloudjob] y [CloudTask] [ net_cloudtask] clases con nuevos métodos. Consulte también hello [documentación de referencia](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) de la biblioteca de hello convenciones de archivo.

Hola [código fuente] [ github_file_conventions] para hello convenciones de archivo biblioteca está disponible en GitHub Hola SDK de Microsoft Azure para el repositorio. NET. 

### <a name="explore-other-approaches-for-persisting-output-data"></a>Exploración de otros métodos para guardar los datos de salida

- Vea [Persist trabajos y tareas de salida tooAzure almacenamiento](batch-task-output.md) para obtener información general de conservar los datos de tarea y el trabajo.
- Vea [tooAzure de datos de tarea almacenamiento con hello API del servicio de lote se conservan](batch-task-output-files.md) toolearn toouse Hola API del servicio de lote toopersist cómo los datos de salida.

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
