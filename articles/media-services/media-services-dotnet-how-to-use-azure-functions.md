---
title: aaaDevelop funciones de Azure con servicios multimedia
description: "Este tema muestra cómo desarrollar las funciones de Azure con el uso de servicios multimedia de toostart Hola portal de Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a>Desarrollo de Azure Functions con Media Services

Este tema muestra cómo tooget se inicia con la creación de funciones de Azure que usan los servicios multimedia. Hola definido en este tema de función de Azure supervisa un contenedor de la cuenta de almacenamiento denominado **entrada** para los nuevos archivos MP4. Una vez que un archivo se coloca en el contenedor de almacenamiento de hello, desencadenador de blob de Hola ejecutará la función hello.

Si desea tooexplore e implementa las funciones de Azure existentes que usan los servicios multimedia de Azure, visite [funciones de Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Este repositorio incluye ejemplos que utilizan los servicios multimedia tooshow flujos de trabajo relacionado tooingesting contenido directamente desde el almacenamiento de blobs, codificación y escribir el contenido nuevo tooblob almacenamiento. También incluye ejemplos de cómo toomonitor trabajo notificaciones a través de las colas de Azure y Webhook. También puede desarrollar sus funciones basadas en los ejemplos de hello en hello [funciones de Azure Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repositorio. funciones de hello toodeploy, presione hello **implementar tooAzure** botón.

## <a name="prerequisites"></a>Requisitos previos

- Antes de crear la primera función, deberá toohave una cuenta activa de Azure. Si aún no tiene una cuenta de Azure, [tiene a su disposición la creación de una cuenta gratis](https://azure.microsoft.com/free/).
- Si va toocreate Azure funciones que realizan acciones en su cuenta de servicios de multimedia de Azure (AMS) o escuchar tooevents enviados por los servicios multimedia, debe crear una cuenta de AMS, tal como se describe [aquí](media-services-portal-create-account.md).
- Descripción de [cómo toouse Azure funciones](../azure-functions/functions-overview.md). Además, revise lo siguiente:
    - [Enlaces HTTP y webhook en Azure Functions](../azure-functions/functions-triggers-bindings.md)
    - [¿Cómo tooconfigure configuración de la aplicación de Azure (función)](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Consideraciones

-  Las funciones de Azure ejecutando bajo el plan de consumo de hello tengan tiempo de espera de 5 minutos limitar.

## <a name="create-a-function-app"></a>Creación de una aplicación de función

1. Vaya toohello [portal de Azure](http://portal.azure.com) e inicie sesión con su cuenta de Azure.
2. Cree una aplicación de función como se describe [aquí](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Una cuenta de almacenamiento que especifique en hello **StorageConnection** (vea el paso siguiente de hello) debe ser la variable de entorno en hello misma región que la aplicación.

## <a name="configure-function-app-settings"></a>Configuración de la aplicación de función

Cuando desarrolle las funciones de servicios multimedia, resulta práctica tooadd variables de entorno que se utilizará a lo largo de las funciones. tooconfigure configuración de la aplicación, haga clic en el vínculo de configuración de aplicación Hola. Para obtener más información, consulte [la configuración de la aplicación Azure función tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

Por ejemplo:

![Settings](./media/media-services-azure-functions/media-services-azure-functions001.png)

función Hello, definida en este artículo, se supone que tiene Hola después de las variables de entorno en la configuración de aplicación:

**AMSAccount**: *nombre de la cuenta de AMS* (p. ej., testams)

**AMSKey**: *clave de la cuenta de AMS* (p. ej., IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)

**MediaServicesStorageAccountName**: *nombre de la cuenta de almacenamiento* (p. ej., testamsstorage)

**MediaServicesStorageAccountKey**: *clave de cuenta de almacenamiento* (p. ej., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)

**StorageConnection**: *conexión de almacenamiento* (p. ej., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)

## <a name="create-a-function"></a>Creación de una función

Una vez implementada su instancia de Function App, puede encontrarla entre Azure Functions de **App Services**.

1. Seleccione la aplicación de función y haga clic en **Nueva función**.
2. Elija hello **C#** lenguaje y **procesamiento de datos** escenario.
3. Elija la plantilla **BlobTrigger**. Esta función se desencadenará cada vez que se carga un blob en hello **entrada** contenedor. Hola **entrada** nombre se especifica en hello **ruta de acceso**, en el paso siguiente de saludo.

    ![files](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. Una vez que seleccione **BlobTrigger**, algunos controles más aparecerá en la página de Hola.

    ![files](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. Haga clic en **Crear**. 


## <a name="files"></a>Archivos

La función de Azure está asociada a archivos de código y otros archivos que se describen en esta sección. De forma predeterminada, una función está asociada con los archivos **function.json** y **run.csx** (C#). Deberá tooadd un **project.json** archivo. resto de Hola de esta sección muestra las definiciones de Hola para estos archivos.

![files](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>function.json

archivo de Hello function.json define los enlaces de función hello y otras opciones de configuración. Hola en tiempo de ejecución utiliza este toomonitor de eventos de archivo toodetermine hello y toopass y devolución de datos de funcionamiento de ejecución. Para obtener más información, consulte [Enlaces HTTP y webhook en Azure Functions](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Conjunto hello **deshabilitado** propiedad demasiado**true** función de hello tooprevent desde que se está ejecutando. 


Este es un ejemplo de archivo **function.json**.

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a>project.json

archivo project.json de Hello contiene dependencias. Este es un ejemplo de **project.json** archivo que incluye servicios de multimedia de Azure de hello requerido .NET paquetes de Nuget. Tenga en cuenta que los números de versión de Hola cambiará con las últimas actualizaciones toohello paquetes, por lo que debe confirmar versiones más recientes de Hola. 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a>run.csx

Se trata de código C# hello para la función.  función Hello define a continuación de monitores de un contenedor de la cuenta de almacenamiento denominado **entrada** (que es lo que se especificó en la ruta de acceso de hello) para los nuevos archivos MP4. Una vez que un archivo se coloca en el contenedor de almacenamiento de hello, desencadenador de blob de Hola ejecutará la función hello.
    
ejemplo de Hola definido en esta sección se muestra 

1. la cuenta de tooingest un activo en los servicios multimedia (a copiar un blob en un recurso de AMS) y 
2. ¿Cómo toosubmit un trabajo de codificación que usa "Transmisión por secuencias adaptativa" Media Encoder estándar preestablecido.

En el escenario de uso real de hello, lo más probable es que desee tootrack progreso del trabajo y, a continuación, publica el activo codificado. Para obtener más información, consulte [notificaciones de trabajo de servicios multimedia de uso Azure WebHooks toomonitor](media-services-dotnet-check-job-progress-with-webhooks.md). Para obtener más ejemplos, consulte [Azure Functions de Media Services](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

Una vez que haya terminado de definir la función, haga clic en **Guardar y ejecutar**.

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get hello destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of hello destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a>Probar la función

tootest la función, deberá tooupload un archivo MP4 en hello **entrada** contenedor de cuenta de almacenamiento de Hola que especificó en la cadena de conexión de Hola.  

## <a name="next-step"></a>Paso siguiente

En este punto, está listo toostart desarrollar una aplicación de servicios multimedia. 
 
Para obtener más detalles y ejemplos/soluciones completas del uso de funciones de Azure y las aplicaciones lógicas con flujos de trabajo de creación de contenido personalizado de toocreate de servicios multimedia de Azure, vea hello [ejemplo de integración de Media Services .NET funciones en GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Consulte también [notificaciones con .NET de trabajo de servicios multimedia de uso Azure WebHooks toomonitor](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

