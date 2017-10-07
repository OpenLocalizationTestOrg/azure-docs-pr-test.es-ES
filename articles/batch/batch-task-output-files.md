---
title: aaaPersist trabajos y tareas de salida tooAzure almacenamiento con hello API del servicio de Azure Batch | Documentos de Microsoft
description: "Obtenga información acerca de cómo trabajos y tareas de lote toopersist toouse API del servicio de lote de salida tooAzure almacenamiento."
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>Conservar datos tooAzure almacenamiento de tarea con hello API del servicio de lote

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

A partir de la versión de 2017-05-01, Hola API del servicio por lotes admite tooAzure de datos de persistencia salida almacenamiento tareas y tareas de administrador de trabajos que se ejecutan en grupos con la configuración de máquina virtual de Hola. Cuando se agrega una tarea, puede especificar un contenedor de almacenamiento de Azure como destino de hello para la salida de la tarea hello. el servicio de lote de Hello, a continuación, escribe cualquier contenedor de toothat de datos de salida cuando se completa la tarea hello.

Se está ejecutando un Hola de toousing ventaja lote resultado de la tarea de servicio API toopersist es que no es necesario aplicación Hola toomodify Hola tarea. En su lugar, con aplicación de cliente de tooyour de algunas modificaciones simples, puede conservar la salida de la tarea de Hola desde dentro del código de hello crea la tarea hello.   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>¿Cuando usa el resultado de la tarea toopersist Hola API del servicio de lote?

Lote de Azure proporciona toopersist más de una manera de resultado de la tarea. Utilizar Hola API del servicio de lote es un método cómodo que es mejor escenarios toothese adecuado:

- Desea toowrite código toopersist resultado de la tarea desde dentro de la aplicación cliente, sin modificar la aplicación hello que se ejecuta la tarea.
- Desea que los resultados de toopersist de tareas por lotes y las tareas de administrador en los grupos creados con la configuración de máquina virtual de Hola.
- Desea que el contenedor de almacenamiento Azure tooan toopersist de salida con un nombre arbitrario.
- Desea que el contenedor de almacenamiento de Azure toopersist salida tooan denominado toohello correspondiente [estándar convenciones de archivo por lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

Si su escenario difiere de los mencionados anteriormente, deberá tooconsider un enfoque diferente. Por ejemplo, API del servicio de lote de hello no actualmente admite tooAzure de salida de transmisión por secuencias almacenamiento mientras se ejecuta la tarea hello. toostream de salida, considere el uso de la biblioteca de convenciones de archivo por lotes hello, está disponible para. NET. Para otros idiomas, necesitará tooimplement su propia solución. Para obtener más información sobre otras opciones para guardar resultado de la tarea, consulte [Persist trabajos y tareas de salida tooAzure almacenamiento](batch-task-output.md). 

## <a name="create-a-container-in-azure-storage"></a>Creación de un contenedor en Azure Storage

salida de la tarea de toopersist tooAzure almacenamiento, deberá toocreate un contenedor que actúa como destino de Hola para los archivos de salida. Crear contenedor de hello antes de ejecutar la tarea, preferiblemente antes de enviar el trabajo. contenedor de hello toocreate, biblioteca de cliente de almacenamiento de Azure adecuada de uso Hola o SDK. Para obtener más información acerca de las API de almacenamiento de Azure, vea hello [documentación del almacenamiento de Azure](https://docs.microsoft.com/azure/storage/).

Por ejemplo, si está escribiendo la aplicación en C#, utilice hello [biblioteca de cliente de almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Hola siguiente ejemplo se muestra cómo toocreate un contenedor:

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>Obtener una firma de acceso compartido para el contenedor de Hola

Después de crear el contenedor de hello, obtener una firma de acceso compartido (SAS) con acceso de escritura toohello contenedor. Una SAS proporciona el contenedor de toohello de acceso delegado. Hola SAS concede acceso con un conjunto especificado de permisos y en un intervalo de tiempo especificado. Hola servicio por lotes debe una SAS con el contenedor de toohello de la salida de tarea de escritura permisos toowrite. Para más información sobre las firmas de acceso compartido, consulte [Uso de firmas de acceso compartido \(SAS\) en Azure Storage](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

Cuando se obtiene una SAS con hello las API de almacenamiento de Azure, Hola API devuelve una cadena de token de SAS. Esta cadena de tokens incluye todos los parámetros de hello SAS, incluidos los permisos de Hola y el intervalo de saludo sobre qué Hola SAS es válido. toouse Hola SAS tooaccess un contenedor de almacenamiento de Azure, deberá tooappend Hola SAS cadena de token toohello URI de recurso. recurso de Hello URI, junto con hello anexa el token de SAS, proporciona acceso autenticado tooAzure almacenamiento.

Hello en el ejemplo siguiente se muestra cómo tooget una SAS de solo escritura símbolo (token) de cadena para el contenedor de Hola y anexa el URI del contenedor de toohello Hola SAS:

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>Especificar archivos de salida para la salida de la tarea

archivos de salida de toospecify para una tarea, crear una colección de [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) objetos y asignar toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) propiedad cuando se crea la tarea hello. 

ejemplo de código de .NET siguiente Hello crea una tarea que escribe números aleatorios tooa archivo denominado `output.txt`. ejemplo de Hola crea un archivo de salida para `output.txt` toobe escrito toohello contenedor. ejemplo de Hola también crea archivos de salida para los archivos de registro que coinciden con el patrón de archivo hello `std*.txt` (_p. ej._, `stdout.txt` y `stderr.txt`). dirección URL del contenedor de Hello requiere Hola SAS que se creó anteriormente para el contenedor de Hola. Hola servicio por lotes utiliza contenedor toohello de hello SAS tooauthenticate acceso: 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a>Especifique un patrón de archivos para buscar coincidencias

Cuando se especifica un archivo de salida, puede usar hello [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) toospecify propiedad un patrón de archivo para hacer coincidir. patrón de archivo Hello puede coincidir con cero archivos, un único archivo o un conjunto de archivos que se crean mediante la tarea hello.

Hola **FilePattern** propiedad admite caracteres comodín de sistema de archivos estándar, como `*` (para que coincida con no recursivo) y `**` (para que coincida con recursivo). Por ejemplo, el ejemplo de código de hello anterior especifica Hola archivo patrón toomatch `std*.txt` de manera no recursiva: 

`filePattern: @"..\std*.txt"`

tooupload un solo archivo, especifique un patrón de archivo con ningún carácter comodín. Por ejemplo, el ejemplo de código de hello anterior especifica Hola archivo patrón toomatch `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>Especificar una condición de carga

Hola [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) propiedad permite cargar condicional de archivos de salida. Un escenario común es tooupload un conjunto de archivos si Hola tarea se ejecuta correctamente y un conjunto diferente de archivos si se produce un error. Por ejemplo, puede que desee archivos de registro detallados tooupload solo cuando se produce un error de tarea hello y finaliza con un código de salida distinto de cero. De forma similar, puede que desee los archivos de resultados tooupload solo si se realiza correctamente la tarea hello, que pueden ser esos archivos falta o está incompleto si se produce un error en la tarea hello.

ejemplo de código anterior Hello establece hello **UploadCondition** propiedad demasiado**TaskCompletion**. Esta configuración especifica que el archivo hello esté toobe cargado al finalizar tareas hello, independientemente del valor Hola de código de salida de hello. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

Para otras configuraciones, vea hello [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) enum.

### <a name="disambiguate-files-with-hello-same-name"></a>Eliminar la ambigüedad de los archivos con hello mismo nombre

tareas de Hello en un trabajo pueden producir archivos que tienen Hola mismo nombre. Por ejemplo, `stdout.txt` y `stderr.txt` se crean para todas las tareas que se ejecutan en un trabajo. Dado que cada tarea se ejecuta en su propio contexto, estos archivos no están en conflicto en el sistema de archivos del nodo de Hola. Sin embargo, al cargar archivos desde varios contenedores compartidos tooa de tareas, deberá toodisambiguate archivos con hello mismo nombre.

Hola [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) propiedad especifica el blob de destino de Hola o el directorio virtual para los archivos de salida. Puede usar hello **ruta de acceso** blob de propiedad tooname Hola o el directorio virtual de tal manera que con el mismo nombre se denominan de forma unívoca en el almacenamiento de Azure de hello archivos de salida. Con el Id. de tarea de hello en ruta de acceso de hello es una buena manera tooensure los nombres únicos e identificar fácilmente los archivos.

Si hello **FilePattern** propiedad se establece la expresión de caracteres comodín tooa, a continuación, todos los archivos que coinciden con el patrón de hello están cargados toohello directorio virtual especificado por hello **ruta de acceso** propiedad. Por ejemplo, si hello contenedor es `mycontainer`, es el Id. de tarea de hello `mytask`, y es el patrón de archivo hello `..\std*.txt`, a continuación, Hola absoluto URI toohello archivos de salida en el almacenamiento de Azure será similares al:

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

Si hello **FilePattern** propiedad es conjunto toomatch un solo nombre de archivo, a continuación, lo que significa que no contiene todos los caracteres comodín, Hola valo hello **ruta de acceso** propiedad especifica el nombre de blob completo Hola . Para evitar conflictos de nomenclatura con un único archivo de varias tareas, a continuación, incluir nombre de hello del directorio virtual de hello como parte de toodisambiguate de nombre de archivo de hello esos archivos. Por ejemplo, un conjunto de hello **ruta de acceso** propiedad tooinclude Id. de tarea hello, carácter de delimitador de hello (normalmente una barra diagonal) y nombre de archivo de hello:

`path: taskId + @"/output.txt"`

Hola absolutos archivos de salida de URI toohello para un conjunto de tareas será similares al:

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Para obtener más información acerca de los directorios virtuales en el almacenamiento de Azure, consulte [enumerar blobs hello en un contenedor](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).


## <a name="diagnose-file-upload-errors"></a>Diagnóstico de errores de carga de archivos

Si carga salida archivos tooAzure almacenamiento se produce un error, tarea hello mueve toohello **completado** hello y estado [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) propiedad está establecida. Examinar hello **FailureInformation** toodetermine propiedad cuál fue el error. Por ejemplo, este es un error que se produce en la carga de archivos si no se encuentra el contenedor de hello: 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

En cada carga de archivos por lotes escribe dos nodos de proceso de toohello de archivos, de registro `fileuploadout.txt` y `fileuploaderr.txt`. Puede examinar estos toolearn de archivos de registro más de un error específico. En casos donde cargar el archivo hello nunca intentó, por ejemplo porque no se pudo ejecutar la tarea hello propio, a continuación, estos archivos de registro no existe.

## <a name="diagnose-file-upload-performance"></a>Diagnóstico del rendimiento de la carga de archivos

Hola `fileuploadout.txt` archivo registra el progreso de la carga. Puede examinar este toolearn de archivo están tardando más información acerca de cuánto tiempo se carga el archivo. Tenga en cuenta que hay muchos factores que contribuyen rendimiento tooupload, incluido el tamaño de hello del nodo de hello, otra actividad en el nodo de hello en tiempo de Hola de carga de hello, si es el contenedor de destino de Hola Hola misma región que el grupo de lote de hello, cuántos nodos son Cargando cuenta de almacenamiento de toohello en hello al mismo tiempo y así sucesivamente.

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>Usa la API del servicio de lote de hello con hello convenciones de archivo por lotes estándar

Al mantener el resultado de la tarea con hello API del servicio de lote, se puede asignar un nombre el contenedor de destino y sin embargo al igual que los blobs. También puede elegir tooname ellas según toohello [estándar convenciones de archivo por lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). estándar de archivo convenciones Hola determina los nombres de hello del contenedor de destino de Hola y de blob en el almacenamiento de Azure para un archivo de salida determinado basándose en los nombres de Hola de hello trabajos y tareas. Si utilizas Hola convenciones de archivo estándar para asignar nombres a archivos de salida, los archivos de salida están disponibles para su visualización en hello [portal de Azure](https://portal.azure.com).

Si está programando en C#, puede utilizar métodos de hello integradas hello [biblioteca convenciones de archivo por lotes para .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files). Esta biblioteca crea Hola correctamente denominado contenedores y las rutas de acceso de blob para usted. Por ejemplo, puede llamar a Hola API tooget Hola correcta nombre hello contenedor, tomando como base el nombre del trabajo de hello:

```csharp
string containerName = job.OutputStorageContainerName();
```

Puede usar hello [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) método tooreturn una dirección URL de firma (SAS) de acceso compartido que es usado toowrite toohello contenedor. A continuación, puede pasar este toohello SAS [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) constructor.

Si está desarrollando en un lenguaje distinto de C#, deberá estándar de tooimplement Hola convenciones archivos usted mismo.

## <a name="code-sample"></a>Código de ejemplo

Hola [PersistOutputs] [ github_persistoutputs] proyecto de ejemplo es uno de hello [ejemplos de código de Azure Batch] [ github_samples] en GitHub. Esta solución de Visual Studio muestra cómo la biblioteca de cliente de toouse Hola por lotes para tareas de .NET toopersist había salida toodurable almacenamiento. Hola toorun de ejemplo, siga estos pasos:

1. Proyecto abierto hello en **Visual Studio 2015 o versiones más recientes**.
2. Agregue el lote y el almacenamiento **las credenciales de cuentas** demasiado**AccountSettings.settings** en proyecto de Microsoft.Azure.Batch.Samples.Common Hola.
3. **Generar** (pero no podrán ejecutar) Hola solución. Si se le solicita, restaure los paquetes NuGet.
4. Hola de uso tooupload portal Azure un [paquete de aplicación](batch-application-packages.md) para **PersistOutputsTask**. Incluir hello `PersistOutputsTask.exe` y sus ensamblados dependientes en paquete de extensión .zip hello, identificador de la aplicación hello conjunto demasiado "PersistOutputsTask" y la aplicación hello empaquetar versión demasiado "1.0".
5. **Iniciar** Hola (ejecutar) **PersistOutputs** proyecto.
6. Cuando escriba toochoose solicitadas Hola persistencia tecnología toouse de ejecución ejemplo hello, **2** ejemplo de Hola a toorun utilizando el resultado de la tarea toopersist Hola API del servicio de lote.
7. Si lo desea, ejemplo de Hola a volver a ejecutar, escribir **3** toopersist salida Hola API del servicio de lote, y también tooname Hola contenedor y blob de ruta de destino según toohello convenciones de archivo estándar.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener más información sobre Guardar resultado de la tarea con la biblioteca de convenciones de archivos de Hola para. NET, vea [conservar trabajos y tareas tooAzure datos almacenamiento con la biblioteca de convenciones de archivo por lotes de Hola para .NET toopersist ](batch-task-output-file-conventions.md).
- Para obtener información sobre otros métodos para almacenar datos de salida en el lote de Azure, consulte [Persist trabajos y tareas de salida tooAzure almacenamiento](batch-task-output.md).

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
