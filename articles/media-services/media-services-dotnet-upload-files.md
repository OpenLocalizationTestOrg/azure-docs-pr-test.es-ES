---
title: archivos de aaaUpload en una cuenta de servicios multimedia mediante .NET | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooget medios de contenido en los servicios multimedia mediante la creación y carga de activos."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a>Cargar archivos en una cuenta de Servicios multimedia mediante .NET
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

En Media Services, cargará (o especificará) los archivos digitales en un recurso. Hola **Asset** entidad puede contener vídeo, audio, imágenes, colecciones de miniaturas, texto realiza un seguimiento y subtítulos archivos (y Hola metadatos acerca de estos archivos.)  Una vez que se cargan archivos de hello, el contenido está almacenado en forma segura en nube de Hola para su posterior procesamiento y transmisión por secuencias.

se denominan archivos Hello en activos de hello **archivos de recursos**. Hola **AssetFile** instancia y archivo de hello multimedia real son dos objetos diferentes. instancia de AssetFile Hola contiene metadatos sobre archivo multimedia de hello, mientras que el archivo de medios de hello contiene contenido multimedia real de Hola.

> [!NOTE]
> Hola siguientes consideraciones se aplica:
> 
> * Servicios multimedia usa el valor de Hola de hello IAssetFile.Name propiedad al generar direcciones URL para hello transmisión por secuencias contenido (por ejemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esta razón, no se permite la codificación porcentual. Hola valo hello **nombre** propiedad no puede tener cualquiera de los siguientes hello [por ciento reservados a la codificación de caracteres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Además, solo puede haber uno '.' para la extensión de nombre de archivo de Hola.
> * longitud de Hello del nombre de hello no debería ser superior a 260 caracteres.
> * Hay un tamaño de archivo máximo de toohello límite admitido para el procesamiento de los servicios multimedia. Vea [esto](media-services-quotas-and-limitations.md) tema para obtener más información acerca de la limitación de tamaño de archivo de Hola.
> * Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy). Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga). Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .
> 

Al crear activos, puede especificar Hola siguientes opciones de cifrado. 

* **Ninguno** : no se utiliza cifrado. Se trata de un valor predeterminado de Hola. Tenga en cuenta que al utilizar esta opción el contenido no está protegido en tránsito o en reposo en el almacenamiento.
  Si tiene previsto toodeliver un MP4 mediante una descarga progresiva, use esta opción. 
* **CommonEncryption** : utilice esta opción si va a cargar contenido que ya se ha cifrado y protegido con cifrado común o DRM de PlayReady (por ejemplo, Smooth Streaming protegido con DRM de PlayReady).
* **EnvelopeEncrypted** : utilice esta opción si va a cargar HLS cifrado con AES. Tenga en cuenta que deben ha codificado y cifrado con Transform Manager archivos Hola.
* **StorageEncrypted** : cifra el contenido no localmente mediante cifrado AES de 256 bits y, a continuación, cargarlo tooAzure almacenamiento donde se almacena cifrado en reposo. Los recursos protegidos con cifrado de almacenamiento se descifran automáticamente y se colocan en un tooencoding anterior del sistema de archivos cifrados y, opcionalmente, volverá a cifrar toouploading anterior como un recurso de salida nuevo. caso de uso principal de Hello para el cifrado de almacenamiento es cuando se desea toosecure sitúe los archivos multimedia de entrada de gran calidad con cifrado de alta seguridad en disco.
  
    Los Servicios multimedia proporcionan cifrado de almacenamiento en disco para sus recursos, no por cable como el administrador de derechos digitales (DRM).
  
    Si el recurso tiene el almacenamiento cifrado, asegúrese de configurar la directiva de entrega de recursos. Para más información, consulte [Configuración de la directiva de entrega de recursos](media-services-dotnet-configure-asset-delivery-policy.md).

Si se especifica para el toobe activo cifrado con una **CommonEncrypted** opción, o un **EnvelopeEncypted** opción, deberá tooassociate el activo con un **ContentKey**. Para obtener más información, consulte [cómo toocreate una ContentKey](media-services-dotnet-create-contentkey.md). 

Si se especifica para el toobe activo cifrado con una **StorageEncrypted** opción, Hola SDK de servicios multimedia para .NET creará un **StorateEncrypted** **ContentKey** para su activo.

Este tema muestra cómo toouse Media Services .NET SDK, así como archivos de tooupload de extensiones de SDK de .NET de servicios multimedia en un recurso de servicios multimedia.

## <a name="upload-a-single-file-with-media-services-net-sdk"></a>Carga de un solo archivo con el SDK .NET de Servicios multimedia
código de ejemplo de Hola siguiente usa tooupload .NET SDK un único archivo. Hola AccessPolicy y localizador se crean y destruyen por función de carga de Hola. 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a>Carga de varios archivos con el SDK .NET de Servicios multimedia
Hola el siguiente código muestra cómo toocreate un activo y cargar varios archivos.

código de Hello Hola siguientes:

* Crea un recurso vacío con hello CreateEmptyAsset método definido en el paso anterior de Hola.
* Crea un **AccessPolicy** instancia que define los permisos de Hola y la duración del activo de toohello de acceso.
* Crea un **localizador** instancia que proporciona el activo de toohello de acceso.
* Crea una instancia de **BlobTransferClient** . Este tipo representa a un cliente que opera en hello que blobs de Azure. En este ejemplo se utiliza el progreso de la carga de Hola de toomonitor Hola cliente. 
* Enumera los archivos en el directorio especificado hello y crea un **AssetFile** instancia para cada archivo.
* Cargas Hola archivos en servicios multimedia con hello **UploadAsync** método. 

> [!NOTE]
> Utilice hello UploadAsync método tooensure que no se bloquean las llamadas de Hola y Hola archivos se cargan en paralelo.
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



Al cargar un gran número de activos, tenga en cuenta Hola siguiente.

* Cree un nuevo objeto **CloudMediaContext** por subproceso. Hola **CloudMediaContext** clase no es segura para subprocesos.
* Aumentar NumberOfConcurrentTransfers del valor predeterminado de Hola de valor superior del tooa 2, como 5. La configuración de esta propiedad afecta a todas las instancias de **CloudMediaContext**. 
* Mantener ParallelTransferThreadCount en el valor predeterminado de Hola de 10.

## <a id="ingest_in_bulk"></a>Ingesta de activos en bloque con SDK .NET de Servicios multimedia
La carga de archivos de recursos de gran tamaño puede ser un obstáculo durante la creación de recursos. Introducción de activos en bloque o "Ingesta en bloque", implica la separación de creación de recursos de proceso de carga de Hola. toouse un enfoque de ingesta de forma masiva, cree un manifiesto (IngestManifest) que describe el recurso de Hola y sus archivos asociados. Utilizamos el método de carga de Hola de contenedor de blobs de su elección tooupload Hola archivos asociados toohello del manifiesto. Servicios de multimedia de Microsoft Azure observa el contenedor de blob de hello asociado con el manifiesto de Hola. Una vez un archivo contenedor de blobs toohello cargado, servicios de multimedia de Microsoft Azure completa la creación de activos de hello basadas en configuración Hola de activos de hello en el manifiesto de hello (IngestManifestAsset).

toocreate un nuevo IngestManifest llame al método de creación de hello expuesto por hello colección los IngestManifests en hello CloudMediaContext. Este método creará un nuevo IngestManifest con nombre de manifiesto de Hola que proporcione.

    IIngestManifest manifest = context.IngestManifests.Create(name);

Crear los activos de Hola que se asociarán con bulk hello IngestManifest. Configurar opciones de cifrado de hello deseado en activos de hello para la ingesta en bloque.

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

Un IngestManifestAsset permite asociar un recurso con un IngestManifest en masa para la ingesta en masa. También asocia hello AssetFiles que conformarán cada activo. toocreate IngestManifestAsset, usar el método de crear de hello en el contexto del servidor de Hola.

Hello en el ejemplo siguiente se muestra cómo manifiesto de ingesta de agregar los dos IngestManifestAssets nuevas que asocian dos recursos de hello creados previamente toohello masiva. Además, cada IngestManifestAsset asociad un conjunto de archivos que se cargarán para cada recurso durante la ingesta en masa.  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

Puede usar cualquier aplicación de cliente de alta velocidad capaz de cargar el contenedor de almacenamiento de hello asset archivos toohello blob URI proporcionado por hello **IIngestManifest.BlobStorageUriForUpload** propiedad de hello IngestManifest. Un servicio de carga de alta velocidad destacado es [Aspera On Demand para la aplicación de Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6). También puede escribir código en los archivos de activos de hello tooupload tal y como se muestra en el siguiente código de ejemplo de Hola.

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

código de Hello para cargar los archivos de recursos de hello para el ejemplo de Hola utilizado en este tema se muestra en el siguiente código de ejemplo de Hola.

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


Puede determinar el progreso de Hola de Hola la ingesta en bloque para todos los recursos asociados con un **IngestManifest** sondeando la propiedad de las estadísticas de Hola de hello **IngestManifest**. En información de progreso de pedido tooupdate, debe utilizar un nuevo **CloudMediaContext** cada vez que se sondea la propiedad de las estadísticas de Hola.

Hello en el ejemplo siguiente se muestra cómo sondear un IngestManifest por su **identificador**.

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a>Cargar archivos con extensiones del SDK de .NET
ejemplo de Hola siguiente muestra cómo tooupload una única archivo utilizando extensiones del SDK de. NET. En este caso Hola **CreateFromFile** se utiliza el método, pero también está disponible la versión asincrónica de hello (**CreateFromFileAsync**). Hola **CreateFromFile** método le permite especificar el nombre de archivo de hello, opción de cifrado y una devolución de llamada en hello tooreport de orden progreso del archivo de saludo de la carga.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

Hello en el ejemplo siguiente se llama a la función de UploadFile y especifica cifrado de almacenamiento como opción de creación de hello activos.  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a>Pasos siguientes

Ahora puede codificar los recursos cargados. Para más información, consulte [Encode an asset using Media Encoder Standard with the Azure portal](media-services-portal-encode.md)(Codificación de recursos mediante el estándar de codificador multimedia con Azure Portal).

También puede utilizar las funciones de Azure tootrigger un trabajo de codificación basado en un archivo que llegan en el contenedor de hello configurado. Para más información, consulte [este ejemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Paso siguiente
Ahora que ha cargado un activo de servicios de tooMedia, vaya a toohello [cómo tooGet un procesador multimedia] [ How tooGet a Media Processor] tema.

[How tooGet a Media Processor]: media-services-get-media-processor.md

