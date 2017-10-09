---
title: 'aaaTutorial: utilizar la biblioteca cliente en hello Azure Batch para .NET | Documentos de Microsoft'
description: "Obtenga información acerca de los conceptos básicos de Azure Batch hello y generar una solución simple con. NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a>Empezar a crear soluciones a la biblioteca de cliente de hello Batch para .NET

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Obtenga información acerca de los conceptos básicos de Hola de [Azure Batch] [ azure_batch] hello y [.NET de lotes] [ net_api] biblioteca en este artículo tal y como se describe un paso de la aplicación de ejemplo en C# por paso. Veremos cómo aprovecha la aplicación de ejemplo de Hola Hola lote servicio tooprocess una carga de trabajo paralelo en la nube de Hola y cómo interactúa con [el almacenamiento de Azure](../storage/common/storage-introduction.md) para almacenamiento provisional de archivo y la recuperación. Podrá Obtenga información acerca de un flujo de trabajo de aplicación común de lote y obtener una descripción de base de componentes principales Hola de lote como trabajos, tareas, grupos y nodos de ejecución.

![Flujo de trabajo de soluciones de Batch (básico)][11]<br/>

## <a name="prerequisites"></a>Requisitos previos
En este artículo se asume que tiene conocimientos prácticos de C# y Visual Studio. También se da por supuesto que es capaz de toosatisfy Hola creación requisitos de las cuentas que se especifican a continuación para Azure y Hola por lotes y los servicios de almacenamiento.

### <a name="accounts"></a>Cuentas
* **Cuenta de Azure**: si aún no tiene ninguna suscripción a Azure, [cree una cuenta gratuita de Azure][azure_free_account].
* **Cuenta de Batch**: una vez que tenga una suscripción a Azure, [cree una cuenta de Azure Batch](batch-account-create-portal.md).
* **Cuenta de almacenamiento**: consulte la sección [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) del artículo [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).

> [!IMPORTANT]
> Procesar por lotes admite actualmente *sólo* hello **general** tipo de cuenta de almacenamiento, tal como se describe en el paso 5 de # [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) en [acerca de Azure las cuentas de almacenamiento](../storage/common/storage-create-storage-account.md).
>
>

### <a name="visual-studio"></a>Visual Studio
Debe tener **Visual Studio 2015 o versiones más recientes** toobuild proyecto de ejemplo de Hola. Puede encontrar versiones gratuitas y de prueba de Visual Studio en hello [información general de productos de Visual Studio][visual_studio].

### <a name="dotnettutorial-code-sample"></a>*DotNetTutorial*
Hola [DotNetTutorial] [ github_dotnettutorial] ejemplo es uno de los muchos ejemplos de código de proceso por lotes que se encuentran en Hola de hello [ejemplos de lote de azure] [ github_samples] repositorio en GitHub. Puede descargar todos los ejemplos de hello haciendo clic en **clon o una descarga > Download ZIP** en página de inicio del repositorio de hello, o haciendo clic en hello [azure-lote-ejemplos-master.zip] [ github_samples_zip]vínculo de descarga directa. Una vez que haya extraído contenido Hola del archivo ZIP de hello, puede encontrar soluciones Hola Hola después de la carpeta:

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a>Explorador de Azure Batch (opcional)
Hola [Explorador de lote de Azure] [ github_batchexplorer] es una utilidad gratuita que se incluye en hello [ejemplos de lote de azure] [ github_samples] repositorio en GitHub. Mientras no se requiere toocomplete este tutorial, puede ser útil al desarrollar y depurar las soluciones de lote.

## <a name="dotnettutorial-sample-project-overview"></a>Información general del proyecto de ejemplo DotNetTutorial
Hola *DotNetTutorial* ejemplo de código es una solución de Visual Studio que consta de dos proyectos: **DotNetTutorial** y **TaskApplication**.

* **DotNetTutorial** es aplicación de cliente de Hola que interactúa con tooexecute de servicios de almacenamiento y por lotes Hola una carga de trabajo paralelo en nodos de proceso (máquinas virtuales). DotNetTutorial se ejecuta en la estación de trabajo local.
* **TaskApplication** es programa Hola que se ejecuta en nodos de proceso de trabajo real de Azure tooperform Hola. En el ejemplo de Hola, `TaskApplication.exe` analiza Hola texto en un archivo descargado desde el almacenamiento de Azure (archivo de entrada de hello). A continuación, genera un archivo de texto (archivo de salida de Hola) que contiene una lista de palabras de tres primeras Hola que aparecen en el archivo de entrada de Hola. Después de crear el archivo de salida de hello, TaskApplication carga Hola archivo tooAzure almacenamiento. Esto facilita la aplicación de cliente de toohello disponibles para su descarga. TaskApplication se ejecuta en paralelo en varios nodos de proceso de hello servicio por lotes.

Hello siguiente diagrama muestra operaciones principales de hello realizadas por la aplicación de cliente de hello, *DotNetTutorial*y la aplicación hello que ejecuta tareas de hello, *TaskApplication*. Este flujo de trabajo básico es típico de muchas soluciones de proceso que se crean con Batch. Mientras no muestran todas las características disponibles en hello servicio por lotes, casi cada escenario de lote incluye algunas partes de este flujo de trabajo.

![Flujo de trabajo de ejemplo de Batch][8]<br/>

[**Paso 1.**](#step-1-create-storage-containers) Crear **contenedores** en Azure Blob Storage.<br/>
[**Paso 2.**](#step-2-upload-task-application-and-data-files) Archivos de aplicación de tarea de carga y toocontainers de archivos de entrada.<br/>
[**Paso 3.**](#step-3-create-batch-pool) Cree un **grupo** de Batch.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Hola grupo **StartTask** descargas Hola toonodes de archivos binarios (TaskApplication) de tarea cuando se unen a grupo Hola.<br/>
[**Paso 4.**](#step-4-create-batch-job) Cree un **trabajo** de Batch.<br/>
[**Paso 5.**](#step-5-add-tasks-to-job) Agregar **tareas** toohello trabajo.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** las tareas de Hello son tooexecute programada en nodos.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Cada tarea descarga sus datos de entrada de Azure Storage y comienza la ejecución.<br/>
[**Paso 6.**](#step-6-monitor-tasks) Supervisar las tareas.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Tal y como se completan tareas, cargan su tooAzure de datos de salida almacenamiento.<br/>
[**Paso 7.**](#step-7-download-task-output) Descargar el resultado de la tarea de Storage

Tal y como se ha mencionado, no todas las soluciones lote realiza estos pasos exactos y pueden incluir muchos más, pero Hola *DotNetTutorial* aplicación de ejemplo muestra procesos comunes que se encuentra en una solución de lote.

## <a name="build-hello-dotnettutorial-sample-project"></a>Compilar hello *DotNetTutorial* proyecto de ejemplo
Antes de poder ejecutar correctamente el ejemplo de Hola, debe especificar las credenciales de cuenta de lote y el almacenamiento en hello *DotNetTutorial* del proyecto `Program.cs` archivo. Si aún no lo ha hecho, abra la solución de hello en Visual Studio haciendo doble clic en hello `DotNetTutorial.sln` archivo de solución. O ábralo desde dentro de Visual Studio mediante el uso de hello **archivo > Abrir > proyecto/solución** menú.

Abra `Program.cs` en hello *DotNetTutorial* proyecto. A continuación, agregue las credenciales tal como se especifica en parte superior de Hola de archivo hello:

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> Como se mencionó anteriormente, actualmente debe especificar credenciales de Hola para un **general** cuenta de almacenamiento en el almacenamiento de Azure. Las aplicaciones de lote usan almacenamiento blob de hello **general** cuenta de almacenamiento. No se especifican credenciales de Hola para una cuenta de almacenamiento que se creó mediante la selección de hello *almacenamiento de blobs* tipo de cuenta.
>
>

Puede encontrar sus credenciales de cuenta de lote y el almacenamiento en la hoja de la cuenta de hello de cada servicio en hello [portal de Azure][azure_portal]:

![Procesar por lotes las credenciales en el portal de hello][9]
![credenciales de almacenamiento en el portal de Hola][10]<br/>

Ahora que ha actualizado el proyecto de hello con sus credenciales, haga clic en solución de hello en el Explorador de soluciones y haga clic en **generar solución**. Confirmar restauración de Hola de los paquetes de NuGet, si se le pide.

> [!TIP]
> Si no se restauran automáticamente paquetes de NuGet hello, o si ve errores sobre un paquetes de saludo de toorestore de error, asegúrese de que tiene hello [Administrador de paquetes de NuGet] [ nuget_packagemgr] instalado. A continuación, habilitar la descarga de Hola de paquetes que faltan. Vea [habilitar paquete restaurar durante la compilación] [ nuget_restore] tooenable descarga del paquete.
>
>

En las secciones siguientes de hello, se divide hacia abajo de la aplicación de ejemplo de Hola en pasos Hola que realiza tooprocess una carga de trabajo en hello servicio por lotes y se explican estos pasos detalladamente. Le recomendamos que toorefer toohello solución abierta en Visual Studio mientras trabaja su camino a través de rest de Hola de este artículo, ya que no todas las líneas de código de ejemplo de Hola se explica.

Desplazarse arriba toohello de hello `MainAsync` método Hola *DotNetTutorial* del proyecto `Program.cs` archivo toostart con el paso 1. Cada paso a continuación, a continuación, aproximadamente sigue Hola progresión del método se llama `MainAsync`.

## <a name="step-1-create-storage-containers"></a>Paso 1: Crear contenedores de Storage
![Crear contenedores en Azure Storage][1]
<br/>

Batch incluye compatibilidad integrada para interactuar con Azure Storage. Contenedores en su cuenta de almacenamiento proporcionará los archivos de hello necesarios para las tareas de Hola que se ejecutan en su cuenta de lote. los contenedores de Hello también proporcionan un colocar toostore Hola salida los datos que producen las tareas de Hola. lo primero que Hola Hola *DotNetTutorial* aplicación de cliente hace es crear tres contenedores en [almacenamiento de blobs de Azure](../storage/common/storage-introduction.md):

* **aplicación**: este contenedor almacenará aplicación hello ejecutar tareas de hello, así como cualquiera de sus dependencias, como archivos DLL.
* **entrada**: tareas descargará tooprocess de archivos de datos de Hola de hello *entrada* contenedor.
* **salida**: cuando completen de tareas de procesamiento del archivo de entrada, cargará Hola resultados toohello *salida* contenedor.

En orden toointeract con un almacenamiento de información de la cuenta y crear contenedores, usamos hello [biblioteca de cliente de almacenamiento de Azure para .NET][net_api_storage]. Creamos una cuenta de toohello de referencia con [CloudStorageAccount][net_cloudstorageaccount]y desde el que crear un [CloudBlobClient][net_cloudblobclient]:

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

Usamos hello `blobClient` hacen referencia a lo largo de la aplicación hello y pasarla como un parámetro tooseveral métodos. Un ejemplo de esto es en bloque de código de hello que sigue inmediatamente a Hola anterior, donde se llamó a `CreateContainerIfNotExistAsync` tooactually crear contenedores de Hola.

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

Una vez que se han creado los contenedores de hello, aplicación hello ahora puede cargar archivos de Hola que se usará en las tareas de Hola.

> [!TIP]
> [¿Cómo toouse almacenamiento de blobs en .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) proporciona una buena información general sobre cómo trabajar con contenedores de almacenamiento de Azure y los blobs. Debe ser cerca de la parte superior de saludo de la lista de lectura como comienza a trabajar con el lote.
>
>

## <a name="step-2-upload-task-application-and-data-files"></a>Paso 2: Cargar la aplicación de tarea y los archivos de datos
![Toocontainers de archivos de la tarea de carga de aplicación y entrada (datos)][2]
<br/>

En el archivo hello cargar el operación, *DotNetTutorial* define en primer lugar las colecciones de **aplicación** y **entrada** las rutas de acceso de archivo tal como aparecen en la máquina local Hola. A continuación, se cargan estos contenedores de toohello de archivos que creó en el paso anterior de Hola.

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

Hay dos métodos de `Program.cs` que intervienen en el proceso de carga de hello:

* `UploadFilesToContainerAsync`: Este método devuelve una colección de [ResourceFile] [ net_resourcefile] objetos (descritos a continuación) e internamente llama `UploadFileToContainerAsync` tooupload cada archivo que es pasa hello *filePaths* parámetro.
* `UploadFileToContainerAsync`: Se trata de método hello que realmente realiza la carga de archivos de Hola y crea hello [ResourceFile] [ net_resourcefile] objetos. Después de cargar el archivo hello, obtiene una firma de acceso compartido (SAS) para el archivo hello y devuelve un objeto ResourceFile que lo representa. A continuación también se tratan las firmas de acceso compartido.

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a>ResourceFiles
A [ResourceFile] [ net_resourcefile] proporciona el nodo de ejecución de tareas en el lote con el archivo de tooa de dirección URL de hello en el almacenamiento de Azure que está tooa descargado antes de que se ejecuta dicha tarea. Hola [ResourceFile.BlobSource] [ net_resourcefile_blobsource] propiedad especifica Hola de dirección URL completa del archivo hello tal como existe en el almacenamiento de Azure. dirección URL de Hello también puede incluir una firma de acceso compartido (SAS) que proporciona un acceso seguro toohello archivo. La mayoría de los tipos de tareas de .NET de Batch contienen una propiedad *ResourceFiles*, que incluye:

* [CloudTask][net_task]
* [StartTask][net_pool_starttask]
* [JobPreparationTask][net_jobpreptask]
* [JobReleaseTask][net_jobreltask]

Hola DotNetTutorial aplicación de ejemplo no utiliza Hola JobPreparationTask o tipos de tareas de JobReleaseTask, pero puede obtener más información acerca de esto en [nodos de ejecución de las tareas de preparación y finalización del trabajo de ejecución en Azure Batch](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Firma de acceso compartido (SAS)
Acceso compartido firmas son cadenas que, cuando se incluye como parte de una dirección URL: proporcionar un acceso seguro toocontainers y blobs en almacenamiento de Azure. Hola DotNetTutorial aplicación usa ambos blob y contenedor comparten las URL de firma de acceso y muestra cómo tooobtain estos compartidos tener acceso a las cadenas de firmas de hello servicio de almacenamiento.

* **Firmas de acceso compartido de BLOB**: StartTask del grupo de hello en DotNetTutorial usa firmas de acceso compartido de blob cuando descarga los archivos binarios de aplicación de Hola y archivos de datos de entrada de almacenamiento (vea el paso 3 siguiente). Hola `UploadFileToContainerAsync` método del DotNetTutorial `Program.cs` contiene código de hello que obtiene la firma de acceso compartido de cada blob. Para ello, llama a [CloudBlob.GetSharedAccessSignature][net_sas_blob].
* **Contenedor de firmas de acceso compartido**: a medida que cada tarea finaliza su trabajo en el nodo de proceso de hello, que se carga su toohello del archivo de salida *salida* contenedor en el almacenamiento de Azure. toodo por lo tanto, TaskApplication utiliza una firma de acceso compartido de contenedor que proporciona acceso de escritura toohello contenedor como parte de la ruta de acceso de hello cuando carga el archivo hello. Firma de acceso compartido de obtención Hola contenedor se realiza de forma similar, como cuando obtención blob Hola firma de acceso compartido. En DotNetTutorial, encontrará que hello `GetContainerSasUrl` llamadas al método auxiliar [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo para. Podrá leer más acerca de cómo TaskApplication usa contenedor Hola compartido firma de acceso en "paso 6: las tareas de supervisión."

> [!TIP]
> Desprotección serie de dos partes de hello en firmas de acceso compartido, [parte 1: Hola descripción compartido modelo de firma (SAS) de acceso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) y [parte 2: crear y utilizar una firma de acceso compartido (SAS) con el almacenamiento de blobs](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn más acerca de cómo proporcionar un acceso seguro toodata en su cuenta de almacenamiento.
>
>

## <a name="step-3-create-batch-pool"></a>Paso 3: Crear el grupo de Batch
![Crear un grupo de Batch][3]
<br/>

Un **grupo** de Batch es una colección de nodos de proceso (máquinas virtuales) en los que Batch ejecuta tareas de un trabajo.

Después de cargar la aplicación hello y toohello de archivos de datos cuenta de almacenamiento con la API de almacenamiento de Azure, *DotNetTutorial* comienza a realizar el servicio por lotes de llamadas a toohello con las API proporcionadas por la biblioteca de .NET de lotes de Hola. Hello código crea primero un [BatchClient][net_batchclient]:

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

A continuación, ejemplo de Hola a crea un grupo de nodos de proceso en la cuenta de lote de hello con una llamada demasiado`CreatePoolIfNotExistsAsync`. `CreatePoolIfNotExistsAsync`hello usa [BatchClient.PoolOperations.CreatePool] [ net_pool_create] método toocreate un nuevo grupo en hello servicio por lotes:

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

Cuando se crea un grupo con [CreatePool][net_pool_create], especifique varios parámetros como el número de Hola de nodos de proceso, hello [tamaño de los nodos de hello](../cloud-services/cloud-services-sizes-specs.md), y Hola operativo nodos sistema. En *DotNetTutorial*, usamos [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 desde [servicios en la nube](../cloud-services/cloud-services-guestos-update-matrix.md). 

También puede crear grupos de nodos de proceso que son máquinas virtuales (VM) de Azure mediante la especificación de hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] para el grupo. Puede crear un grupo de nodos de proceso de máquinas virtuales a partir de imágenes de Windows o [Linux](batch-linux-nodes.md). origen de Hola para las imágenes de máquina virtual puede ser:

- Hola [máquinas virtuales de Azure Marketplace][vm_marketplace], lo que proporciona imágenes de Windows y Linux que están listos para usar. 
- Una imagen personalizada preparada y proporcionada por el usuario. Para más información acerca de las imágenes personalizadas, consulte [Desarrollo de soluciones de procesos paralelos a gran escala con Batch](batch-api-basics.md#pool).

> [!IMPORTANT]
> Se cobrará por recursos de proceso en Batch. los costos de toominimize, puede reducir `targetDedicatedComputeNodes` too1 antes de ejecutar el ejemplo hello.
>
>

Junto con estas propiedades de nodo físico, también puede especificar un [StartTask] [ net_pool_starttask] para el grupo de Hola. Hola StartTask se ejecuta en cada nodo según ese nodo une a grupo de Hola y cada vez que se reinicie un nodo. Hola StartTask resulta especialmente útil para instalar aplicaciones en ejecución de toohello anteriores de nodos de proceso de tareas. Por ejemplo, si las tareas para procesar datos mediante el uso de scripts de Python, podría utilizar un tooinstall StartTask Python en nodos de proceso de Hola.

En esta aplicación de ejemplo Hola StartTask copia los archivos de Hola que descarga desde el almacenamiento (que se especifican mediante hello [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] propiedad) del directorio compartido toohello del directorio de trabajo de hello StartTask que *todos los* pueden tener acceso tareas que se ejecutan en el nodo de Hola. Básicamente, se copian `TaskApplication.exe` y su dependencias toohello directorio compartido en cada nodo como nodo de Hola une a grupo de hello, para que las tareas que se ejecutan en el nodo de hello pueden tener acceso a él.

> [!TIP]
> Hola **paquetes de aplicación** característica de lote de Azure proporciona tooget de otra manera su aplicación en los nodos de proceso de hello en un grupo. Vea [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md) para obtener más información.
>
>

También importantes en el fragmento de código de hello anterior es el uso de Hola de dos variables de entorno de hello *CommandLine* propiedad de hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` y `%AZ_BATCH_NODE_SHARED_DIR%`. Cada nodo de ejecución dentro de un grupo de proceso por lotes se configura automáticamente con varias variables de entorno que están tooBatch específico. Cualquier proceso que se ejecuta una tarea tiene acceso a variables de entorno de toothese.

> [!TIP]
> toofind más información sobre las variables de entorno de Hola que están disponibles en los nodos de proceso en un grupo de lote e información de directorios de trabajo de tarea, vea hello [configuración del entorno para tareas](batch-api-basics.md#environment-settings-for-tasks) y [archivos y directorios ](batch-api-basics.md#files-and-directories) secciones de hello [Introducción a la característica por lotes para los desarrolladores](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Paso 4: Crear el trabajo de Batch
![Crear un trabajo de Batch][4]<br/>

Un **trabajo** de Batch es una colección de tareas y está asociado a un grupo de nodos de proceso. las tareas de Hello en un trabajo que se ejecutan en nodos de proceso del grupo de hello asociado.

Puede usar un trabajo no solo para organizar y seguimiento de las tareas en las cargas de trabajo relacionados, sino también para imponer ciertas restricciones, como el tiempo de ejecución máximo de hello para el trabajo de hello (y por extensión, sus tareas), así como la prioridad del trabajo en los trabajos de relación tooother Hola por lotes cuenta. Sin embargo, en este ejemplo, el trabajo de Hola se asocia únicamente a grupo Hola que creó en el paso 3 de #. No hay propiedades adicionales configuradas.

Todos los trabajos de Batch están asociados a un grupo específico. Esta asociación indica qué nodos se ejecutarán las tareas del trabajo de hello en. Especifique este mediante el uso de hello [CloudJob.PoolInformation] [ net_job_poolinfo] propiedad, como se muestra en el siguiente fragmento de código de hello.

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

Ahora que se ha creado un trabajo, las tareas se agregan trabajo de hello tooperform.

## <a name="step-5-add-tasks-toojob"></a>Paso 5: Agregar toojob de tareas
![Agregar tareas toojob][5]<br/>
*(1) tareas se agregan toohello trabajo, tareas de hello (2) son toorun programada en nodos y tareas (3) Hola descargar tooprocess de archivos de datos de Hola*

Lote **tareas** son nodos de proceso de hello unidades de trabajo que se ejecutan en Hola. Una tarea tiene una línea de comandos y ejecuta scripts de Hola o archivos ejecutables que especifique en esa línea de comandos.

tooactually realizar el trabajo, se deben agregar tareas tooa trabajo. Cada [CloudTask] [ net_task] se configura con una propiedad de línea de comandos y [ResourceFiles] [ net_task_resourcefiles] (al igual que con StartTask del grupo de Hola) que tarea Hello descarga toohello nodo antes de su línea de comandos se ejecuta automáticamente. Hola *DotNetTutorial* proyecto de ejemplo, cada tarea procesa un solo archivo. Por lo tanto, su colección ResourceFiles contiene un único elemento.

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> Cuando tengan acceso a las variables de entorno como `%AZ_BATCH_NODE_SHARED_DIR%` o ejecutar una aplicación no se encuentra en el nodo de hello `PATH`, líneas de comandos de tarea deben ir precedidas de `cmd /c`. Esto explícitamente ejecutará el intérprete de comandos de Hola e indicar a tooterminate después de llevar a cabo el comando. Este requisito no es necesario si las tareas ejecutan una aplicación en el nodo de hello `PATH` (como *robocopy.exe* o *powershell.exe*) y no se usa ninguna variable de entorno.
>
>

Dentro de hello `foreach` bucle en el fragmento de código de hello anterior, puede ver que se construye la línea de comandos de hello para la tarea hello, que se pasan tres argumentos de línea de comandos demasiado*TaskApplication.exe*:

1. Hola **primer argumento** es ruta Hola Hola archivo tooprocess. Este es el archivo de toohello de ruta de acceso local de hello tal como existe en el nodo de Hola. Hola al objeto ResourceFile en `UploadFileToContainerAsync` creó por primera vez los casos anteriores, el nombre del archivo de Hola se usó para esta propiedad (como un constructor al parámetro toohello ResourceFile). Esto indica que ese archivo hello puede encontrarse en hello mismo directorio como *TaskApplication.exe*.
2. Hola **el segundo argumento** especifica ese Hola hacia arriba *N* palabras deberían escribir el archivo de salida de toohello. En el ejemplo de Hola, esto está codificado de forma rígida para que superior tres palabras de Hola se escriben toohello archivo de salida.
3. Hola **tercer argumento** es la firma de acceso compartido (SAS) de Hola que proporciona acceso de escritura toohello **salida** contenedor en el almacenamiento de Azure. *TaskApplication.exe* utiliza este recurso compartido acceso URL de firma cuando se carga de tooAzure de archivo de salida de hello almacenamiento. Puede encontrar código de hello para esto en hello `UploadFileToContainer` método en hello TaskApplication proyecto `Program.cs` archivo:

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a>Paso 6: Supervisar tareas
![Supervisar tareas][6]<br/>
*monitores (1) aplicación de cliente de Hola Hola tareas de finalización y el estado de correcto y (2) Hola tooAzure de datos de resultado de carga de tareas almacenamiento*

Cuando las tareas se agregan trabajo tooa, están en cola y programadas para ejecutarse en nodos de ejecución dentro del bloque de hello asociado al trabajo de Hola automáticamente. En función de la configuración de Hola que especifique, por lotes controla Queue de todas las tareas, programación, Reintentar y otras tareas de administración de la tarea de.

Existen muchos enfoques de ejecución de la tarea de toomonitoring. DotNetTutorial muestra un ejemplo sencillo que informa únicamente sobre la finalización y los estados de error y de realización correcta de la tarea. Dentro de hello `MonitorTasks` método del DotNetTutorial `Program.cs`, hay tres conceptos de .NET de lotes que justifican una explicación. Dichos conceptos se enumeran a continuación en su orden de aparición:

1. **ODATADetailLevel**: es esencial especificar [ODATADetailLevel][net_odatadetaillevel] en las operaciones de lista (por ejemplo, obtener una lista de las tareas de un trabajo) para garantizar el rendimiento de una aplicación de Batch. Agregar [consultar el servicio de Azure Batch Hola eficazmente](batch-efficient-list-queries.md) tooyour leer lista si planea realizar algún tipo de supervisión de estado en las aplicaciones de lote.
2. **TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] proporciona a aplicaciones de .NET de Batch utilidades auxiliares para la supervisión de los estados de las tareas. En `MonitorTasks`, *DotNetTutorial* espera a que todos los tooreach de tareas [TaskState.Completed] [ net_taskstate] dentro de un límite de tiempo. A continuación, finaliza el trabajo de Hola.
3. **TerminateJobAsync**: finalizar un trabajo con [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (u Hola bloqueando JobOperations.TerminateJob) marca ese trabajo como completado. Resulta esencial toodo por lo que si la solución de lote usa un [JobReleaseTask][net_jobreltask]. Se trata de un tipo de tarea especial, que se describe en [areas de preparación y finalización de trabajos](batch-job-prep-release.md).

Hola `MonitorTasks` método de *DotNetTutorial*del `Program.cs` aparece a continuación:

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a>Paso 7: Descargar el resultado de la tarea
![Descargar el resultado de la tarea de Storage][7]<br/>

Ahora que hello trabajo se completa, resultado de hello de las tareas de hello puede descargarse desde el almacenamiento de Azure. Esto se realiza con una llamada demasiado`DownloadBlobsFromContainerAsync` en *DotNetTutorial*del `Program.cs`:

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> Hola llamada demasiado`DownloadBlobsFromContainerAsync` en hello *DotNetTutorial* aplicación especifica que los archivos de hello deben ser descargado tooyour `%TEMP%` carpeta. Cree toomodify libre esta ubicación de salida.
>
>

## <a name="step-8-delete-containers"></a>Paso 8: Eliminar contenedores
Dado que se le cobrará por datos que residen en el almacenamiento de Azure, siempre es una buena idea tooremove los blobs que ya no son necesarios para los trabajos por lotes. Del DotNetTutorial `Program.cs`, esto se realiza con el método de aplicación auxiliar de tres llamadas toohello `DeleteContainerAsync`:

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

el propio método Hello simplemente obtiene un contenedor de toohello de referencia y, a continuación, se llama [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Paso 9: Eliminar trabajo hello y grupo de Hola
En el paso final de hello, le toodelete solicitadas Hola hello y trabajo de grupo creados por la aplicación de hello DotNetTutorial. Aunque no se cobran los trabajos y las tareas, *sí* se cobran los nodos de proceso. Por consiguiente, se recomienda asignar solo los nodos necesarios. La eliminación de los grupos que no se usen puede formar parte del proceso de mantenimiento.

Hola BatchClient [JobOperations] [ net_joboperations] y [PoolOperations] [ net_pooloperations] tienen métodos de eliminación correspondientes, que se denominan si usuario de Hello confirma la eliminación:

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> Tenga en cuenta que los recursos de proceso se cobran; la eliminación de grupos sin usar reducirá el costo. Además, tenga en cuenta que al eliminar un grupo eliminan todos los nodos de proceso dentro de ese grupo y que todos los datos de los nodos de hello serán irrecuperables después de elimina el grupo de Hola.
>
>

## <a name="run-hello-dotnettutorial-sample"></a>Ejecute hello *DotNetTutorial* ejemplo
Cuando se ejecuta la aplicación de ejemplo de Hola, resultado de la consola de hello será similar siguiente toohello. Durante la ejecución, experimentarán una pausa en `Awaiting task completion, timeout in 00:30:00...` mientras se inician los nodos de proceso del grupo de Hola. Hola de uso [portal de Azure] [ azure_portal] toomonitor su grupo, nodos de proceso, trabajo y las tareas durante y después de la ejecución. Hola de uso [portal de Azure] [ azure_portal] o hello [Azure Storage Explorer] [ storage_explorers] tooview Hola recursos de almacenamiento (contenedores y blobs) que están Creando aplicación hello.

Tiempo de ejecución típica es **aproximadamente 5 minutos** al ejecutar la aplicación hello en su configuración predeterminada.

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Pasos siguientes
Cree cambios toomake libre demasiado*DotNetTutorial* y *TaskApplication* tooexperiment con diferentes escenarios de proceso. Por ejemplo, intente agregar un retraso de ejecución demasiado*TaskApplication*, por ejemplo, al igual que con [Thread.Sleep][net_thread_sleep], toosimulate larga ejecución tareas y supervisarlos en el portal de Hola. Intente agregar más tareas o ajustar Hola número de nodos de cálculo. Agregar lógica toocheck para y permitir el uso de Hola de tiempo de ejecución existente grupo toospeed (*sugerencia*: extraer del repositorio `ArticleHelpers.cs` en hello [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] proyecto [ejemplos de lote de azure][github_samples]).

Ahora que está familiarizado con un flujo de trabajo básico de Hola de una solución de lote, es hora toodig en toohello características adicionales de hello servicio por lotes.

* Hola de revisión [características de información general de Azure Batch](batch-api-basics.md) artículo, que se recomienda si dispone de un nuevo servicio de toohello.
* Inicio de Hola otros artículos de desarrollo de lote en **desarrollo detallada** en hello [ruta de acceso de aprendizaje por lotes][batch_learning_path].
* Extraer del repositorio una implementación diferente de procesamiento de cargas de trabajo de Hola "top N palabras" mediante el proceso por lotes en hello [TopNWords] [ github_topnwords] ejemplo.
* Hola revisión .NET de lotes [notas de la versión](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) de cambios más recientes de hello en la biblioteca de Hola.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Crear contenedores en Azure Storage"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Toocontainers de archivos de la tarea de carga de aplicación y entrada (datos)"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Crear el grupo de Batch"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Crear trabajo de Batch"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Agregar tareas toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Supervisar tareas"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Descargar el resultado de la tarea de Storage"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Flujo de trabajo de soluciones de Batch (diagrama completo)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Credenciales de Batch en el portal"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Credenciales de Storage en el portal"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Flujo de trabajo de soluciones de Batch (diagrama mínimo)"
