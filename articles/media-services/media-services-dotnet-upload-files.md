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
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="1ad74-103">Cargar archivos en una cuenta de Servicios multimedia mediante .NET</span><span class="sxs-lookup"><span data-stu-id="1ad74-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ad74-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1ad74-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="1ad74-105">REST</span><span class="sxs-lookup"><span data-stu-id="1ad74-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="1ad74-106">Portal</span><span class="sxs-lookup"><span data-stu-id="1ad74-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="1ad74-107">En Media Services, cargará (o especificará) los archivos digitales en un recurso.</span><span class="sxs-lookup"><span data-stu-id="1ad74-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="1ad74-108">Hola **Asset** entidad puede contener vídeo, audio, imágenes, colecciones de miniaturas, texto realiza un seguimiento y subtítulos archivos (y Hola metadatos acerca de estos archivos.)  Una vez que se cargan archivos de hello, el contenido está almacenado en forma segura en nube de Hola para su posterior procesamiento y transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="1ad74-108">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="1ad74-109">se denominan archivos Hello en activos de hello **archivos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="1ad74-109">hello files in hello asset are called **Asset Files**.</span></span> <span data-ttu-id="1ad74-110">Hola **AssetFile** instancia y archivo de hello multimedia real son dos objetos diferentes.</span><span class="sxs-lookup"><span data-stu-id="1ad74-110">hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="1ad74-111">instancia de AssetFile Hola contiene metadatos sobre archivo multimedia de hello, mientras que el archivo de medios de hello contiene contenido multimedia real de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-111">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="1ad74-112">Hola siguientes consideraciones se aplica:</span><span class="sxs-lookup"><span data-stu-id="1ad74-112">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="1ad74-113">Servicios multimedia usa el valor de Hola de hello IAssetFile.Name propiedad al generar direcciones URL para hello transmisión por secuencias contenido (por ejemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esta razón, no se permite la codificación porcentual.</span><span class="sxs-lookup"><span data-stu-id="1ad74-113">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="1ad74-114">Hola valo hello **nombre** propiedad no puede tener cualquiera de los siguientes hello [por ciento reservados a la codificación de caracteres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="1ad74-114">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="1ad74-115">Además, solo puede haber uno '.' para la extensión de nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-115">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="1ad74-116">longitud de Hello del nombre de hello no debería ser superior a 260 caracteres.</span><span class="sxs-lookup"><span data-stu-id="1ad74-116">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="1ad74-117">Hay un tamaño de archivo máximo de toohello límite admitido para el procesamiento de los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="1ad74-117">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="1ad74-118">Vea [esto](media-services-quotas-and-limitations.md) tema para obtener más información acerca de la limitación de tamaño de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> * <span data-ttu-id="1ad74-119">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="1ad74-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="1ad74-120">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="1ad74-120">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="1ad74-121">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="1ad74-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="1ad74-122">Al crear activos, puede especificar Hola siguientes opciones de cifrado.</span><span class="sxs-lookup"><span data-stu-id="1ad74-122">When you create assets, you can specify hello following encryption options.</span></span> 

* <span data-ttu-id="1ad74-123">**Ninguno** : no se utiliza cifrado.</span><span class="sxs-lookup"><span data-stu-id="1ad74-123">**None** - No encryption is used.</span></span> <span data-ttu-id="1ad74-124">Se trata de un valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-124">This is hello default value.</span></span> <span data-ttu-id="1ad74-125">Tenga en cuenta que al utilizar esta opción el contenido no está protegido en tránsito o en reposo en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1ad74-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="1ad74-126">Si tiene previsto toodeliver un MP4 mediante una descarga progresiva, use esta opción.</span><span class="sxs-lookup"><span data-stu-id="1ad74-126">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="1ad74-127">**CommonEncryption** : utilice esta opción si va a cargar contenido que ya se ha cifrado y protegido con cifrado común o DRM de PlayReady (por ejemplo, Smooth Streaming protegido con DRM de PlayReady).</span><span class="sxs-lookup"><span data-stu-id="1ad74-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="1ad74-128">**EnvelopeEncrypted** : utilice esta opción si va a cargar HLS cifrado con AES.</span><span class="sxs-lookup"><span data-stu-id="1ad74-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="1ad74-129">Tenga en cuenta que deben ha codificado y cifrado con Transform Manager archivos Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-129">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="1ad74-130">**StorageEncrypted** : cifra el contenido no localmente mediante cifrado AES de 256 bits y, a continuación, cargarlo tooAzure almacenamiento donde se almacena cifrado en reposo.</span><span class="sxs-lookup"><span data-stu-id="1ad74-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="1ad74-131">Los recursos protegidos con cifrado de almacenamiento se descifran automáticamente y se colocan en un tooencoding anterior del sistema de archivos cifrados y, opcionalmente, volverá a cifrar toouploading anterior como un recurso de salida nuevo.</span><span class="sxs-lookup"><span data-stu-id="1ad74-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="1ad74-132">caso de uso principal de Hello para el cifrado de almacenamiento es cuando se desea toosecure sitúe los archivos multimedia de entrada de gran calidad con cifrado de alta seguridad en disco.</span><span class="sxs-lookup"><span data-stu-id="1ad74-132">hello primary use case for Storage Encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="1ad74-133">Los Servicios multimedia proporcionan cifrado de almacenamiento en disco para sus recursos, no por cable como el administrador de derechos digitales (DRM).</span><span class="sxs-lookup"><span data-stu-id="1ad74-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="1ad74-134">Si el recurso tiene el almacenamiento cifrado, asegúrese de configurar la directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="1ad74-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="1ad74-135">Para más información, consulte [Configuración de la directiva de entrega de recursos](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="1ad74-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="1ad74-136">Si se especifica para el toobe activo cifrado con una **CommonEncrypted** opción, o un **EnvelopeEncypted** opción, deberá tooassociate el activo con un **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="1ad74-136">If you specify for your asset toobe encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need tooassociate your asset with a **ContentKey**.</span></span> <span data-ttu-id="1ad74-137">Para obtener más información, consulte [cómo toocreate una ContentKey](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="1ad74-137">For more information, see [How toocreate a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="1ad74-138">Si se especifica para el toobe activo cifrado con una **StorageEncrypted** opción, Hola SDK de servicios multimedia para .NET creará un **StorateEncrypted** **ContentKey** para su activo.</span><span class="sxs-lookup"><span data-stu-id="1ad74-138">If you specify for your asset toobe encrypted with a **StorageEncrypted** option, hello Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="1ad74-139">Este tema muestra cómo toouse Media Services .NET SDK, así como archivos de tooupload de extensiones de SDK de .NET de servicios multimedia en un recurso de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="1ad74-139">This topic shows how toouse Media Services .NET SDK as well as Media Services .NET SDK extensions tooupload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="1ad74-140">Carga de un solo archivo con el SDK .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="1ad74-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="1ad74-141">código de ejemplo de Hola siguiente usa tooupload .NET SDK un único archivo.</span><span class="sxs-lookup"><span data-stu-id="1ad74-141">hello sample code below uses .NET SDK tooupload a single file.</span></span> <span data-ttu-id="1ad74-142">Hola AccessPolicy y localizador se crean y destruyen por función de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-142">hello AccessPolicy and Locator are created and destroyed by hello Upload function.</span></span> 


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


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="1ad74-143">Carga de varios archivos con el SDK .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="1ad74-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="1ad74-144">Hola el siguiente código muestra cómo toocreate un activo y cargar varios archivos.</span><span class="sxs-lookup"><span data-stu-id="1ad74-144">hello following code shows how toocreate an asset and upload multiple files.</span></span>

<span data-ttu-id="1ad74-145">código de Hello Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="1ad74-145">hello code does hello following:</span></span>

* <span data-ttu-id="1ad74-146">Crea un recurso vacío con hello CreateEmptyAsset método definido en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-146">Creates an empty asset using hello CreateEmptyAsset method defined in hello previous step.</span></span>
* <span data-ttu-id="1ad74-147">Crea un **AccessPolicy** instancia que define los permisos de Hola y la duración del activo de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="1ad74-147">Creates an **AccessPolicy** instance that defines hello permissions and duration of access toohello asset.</span></span>
* <span data-ttu-id="1ad74-148">Crea un **localizador** instancia que proporciona el activo de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="1ad74-148">Creates a **Locator** instance that provides access toohello asset.</span></span>
* <span data-ttu-id="1ad74-149">Crea una instancia de **BlobTransferClient** .</span><span class="sxs-lookup"><span data-stu-id="1ad74-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="1ad74-150">Este tipo representa a un cliente que opera en hello que blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad74-150">This type represents a client that operates on hello Azure blobs.</span></span> <span data-ttu-id="1ad74-151">En este ejemplo se utiliza el progreso de la carga de Hola de toomonitor Hola cliente.</span><span class="sxs-lookup"><span data-stu-id="1ad74-151">In this example we use hello client toomonitor hello upload progress.</span></span> 
* <span data-ttu-id="1ad74-152">Enumera los archivos en el directorio especificado hello y crea un **AssetFile** instancia para cada archivo.</span><span class="sxs-lookup"><span data-stu-id="1ad74-152">Enumerates through files in hello specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="1ad74-153">Cargas Hola archivos en servicios multimedia con hello **UploadAsync** método.</span><span class="sxs-lookup"><span data-stu-id="1ad74-153">Uploads hello files into Media Services using hello **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="1ad74-154">Utilice hello UploadAsync método tooensure que no se bloquean las llamadas de Hola y Hola archivos se cargan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="1ad74-154">Use hello UploadAsync method tooensure that hello calls are not blocking and hello files are uploaded in parallel.</span></span>
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



<span data-ttu-id="1ad74-155">Al cargar un gran número de activos, tenga en cuenta Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="1ad74-155">When uploading a large number of assets, consider hello following.</span></span>

* <span data-ttu-id="1ad74-156">Cree un nuevo objeto **CloudMediaContext** por subproceso.</span><span class="sxs-lookup"><span data-stu-id="1ad74-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="1ad74-157">Hola **CloudMediaContext** clase no es segura para subprocesos.</span><span class="sxs-lookup"><span data-stu-id="1ad74-157">hello **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="1ad74-158">Aumentar NumberOfConcurrentTransfers del valor predeterminado de Hola de valor superior del tooa 2, como 5.</span><span class="sxs-lookup"><span data-stu-id="1ad74-158">Increase NumberOfConcurrentTransfers from hello default value of 2 tooa higher value like 5.</span></span> <span data-ttu-id="1ad74-159">La configuración de esta propiedad afecta a todas las instancias de **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="1ad74-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="1ad74-160">Mantener ParallelTransferThreadCount en el valor predeterminado de Hola de 10.</span><span class="sxs-lookup"><span data-stu-id="1ad74-160">Keep ParallelTransferThreadCount at hello default value of 10.</span></span>

## <span data-ttu-id="1ad74-161"><a id="ingest_in_bulk"></a>Ingesta de activos en bloque con SDK .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="1ad74-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="1ad74-162">La carga de archivos de recursos de gran tamaño puede ser un obstáculo durante la creación de recursos.</span><span class="sxs-lookup"><span data-stu-id="1ad74-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="1ad74-163">Introducción de activos en bloque o "Ingesta en bloque", implica la separación de creación de recursos de proceso de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from hello upload process.</span></span> <span data-ttu-id="1ad74-164">toouse un enfoque de ingesta de forma masiva, cree un manifiesto (IngestManifest) que describe el recurso de Hola y sus archivos asociados.</span><span class="sxs-lookup"><span data-stu-id="1ad74-164">toouse a bulk ingesting approach, create a manifest (IngestManifest) that describes hello asset and its associated files.</span></span> <span data-ttu-id="1ad74-165">Utilizamos el método de carga de Hola de contenedor de blobs de su elección tooupload Hola archivos asociados toohello del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="1ad74-165">Then use hello upload method of your choice tooupload hello associated files toohello manifest’s blob container.</span></span> <span data-ttu-id="1ad74-166">Servicios de multimedia de Microsoft Azure observa el contenedor de blob de hello asociado con el manifiesto de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-166">Microsoft Azure Media Services watches hello blob container associated with hello manifest.</span></span> <span data-ttu-id="1ad74-167">Una vez un archivo contenedor de blobs toohello cargado, servicios de multimedia de Microsoft Azure completa la creación de activos de hello basadas en configuración Hola de activos de hello en el manifiesto de hello (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="1ad74-167">Once a file is uploaded toohello blob container, Microsoft Azure Media Services completes hello asset creation based on hello configuration of hello asset in hello manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="1ad74-168">toocreate un nuevo IngestManifest llame al método de creación de hello expuesto por hello colección los IngestManifests en hello CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="1ad74-168">toocreate a new IngestManifest call hello Create method exposed by hello IngestManifests collection on hello CloudMediaContext.</span></span> <span data-ttu-id="1ad74-169">Este método creará un nuevo IngestManifest con nombre de manifiesto de Hola que proporcione.</span><span class="sxs-lookup"><span data-stu-id="1ad74-169">This method will create a new IngestManifest with hello manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="1ad74-170">Crear los activos de Hola que se asociarán con bulk hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="1ad74-170">Create hello assets that will be associated with hello bulk IngestManifest.</span></span> <span data-ttu-id="1ad74-171">Configurar opciones de cifrado de hello deseado en activos de hello para la ingesta en bloque.</span><span class="sxs-lookup"><span data-stu-id="1ad74-171">Configure hello desired encryption options on hello asset for bulk ingesting.</span></span>

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="1ad74-172">Un IngestManifestAsset permite asociar un recurso con un IngestManifest en masa para la ingesta en masa.</span><span class="sxs-lookup"><span data-stu-id="1ad74-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="1ad74-173">También asocia hello AssetFiles que conformarán cada activo.</span><span class="sxs-lookup"><span data-stu-id="1ad74-173">It also associates hello AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="1ad74-174">toocreate IngestManifestAsset, usar el método de crear de hello en el contexto del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-174">toocreate an IngestManifestAsset, use hello Create method on hello server context.</span></span>

<span data-ttu-id="1ad74-175">Hello en el ejemplo siguiente se muestra cómo manifiesto de ingesta de agregar los dos IngestManifestAssets nuevas que asocian dos recursos de hello creados previamente toohello masiva.</span><span class="sxs-lookup"><span data-stu-id="1ad74-175">hello following example demonstrates adding two new IngestManifestAssets that associate hello two assets previously created toohello bulk ingest manifest.</span></span> <span data-ttu-id="1ad74-176">Además, cada IngestManifestAsset asociad un conjunto de archivos que se cargarán para cada recurso durante la ingesta en masa.</span><span class="sxs-lookup"><span data-stu-id="1ad74-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="1ad74-177">Puede usar cualquier aplicación de cliente de alta velocidad capaz de cargar el contenedor de almacenamiento de hello asset archivos toohello blob URI proporcionado por hello **IIngestManifest.BlobStorageUriForUpload** propiedad de hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="1ad74-177">You can use any high speed client application capable of uploading hello asset files toohello blob storage container URI provided by hello **IIngestManifest.BlobStorageUriForUpload** property of hello IngestManifest.</span></span> <span data-ttu-id="1ad74-178">Un servicio de carga de alta velocidad destacado es [Aspera On Demand para la aplicación de Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span><span class="sxs-lookup"><span data-stu-id="1ad74-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="1ad74-179">También puede escribir código en los archivos de activos de hello tooupload tal y como se muestra en el siguiente código de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-179">You can also write code tooupload hello assets files as shown in hello following code example.</span></span>

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

<span data-ttu-id="1ad74-180">código de Hello para cargar los archivos de recursos de hello para el ejemplo de Hola utilizado en este tema se muestra en el siguiente código de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-180">hello code for uploading hello asset files for hello sample used in this topic is shown in hello following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="1ad74-181">Puede determinar el progreso de Hola de Hola la ingesta en bloque para todos los recursos asociados con un **IngestManifest** sondeando la propiedad de las estadísticas de Hola de hello **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="1ad74-181">You can determine hello progress of hello bulk ingesting for all assets associated with an **IngestManifest** by polling hello Statistics property of hello **IngestManifest**.</span></span> <span data-ttu-id="1ad74-182">En información de progreso de pedido tooupdate, debe utilizar un nuevo **CloudMediaContext** cada vez que se sondea la propiedad de las estadísticas de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ad74-182">In order tooupdate progress information, you must use a new **CloudMediaContext** each time you poll hello Statistics property.</span></span>

<span data-ttu-id="1ad74-183">Hello en el ejemplo siguiente se muestra cómo sondear un IngestManifest por su **identificador**.</span><span class="sxs-lookup"><span data-stu-id="1ad74-183">hello following example demonstrates polling an IngestManifest by its **Id**.</span></span>

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



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="1ad74-184">Cargar archivos con extensiones del SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="1ad74-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="1ad74-185">ejemplo de Hola siguiente muestra cómo tooupload una única archivo utilizando extensiones del SDK de. NET.</span><span class="sxs-lookup"><span data-stu-id="1ad74-185">hello example below shows how tooupload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="1ad74-186">En este caso Hola **CreateFromFile** se utiliza el método, pero también está disponible la versión asincrónica de hello (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="1ad74-186">In this case hello **CreateFromFile** method is used, but hello asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="1ad74-187">Hola **CreateFromFile** método le permite especificar el nombre de archivo de hello, opción de cifrado y una devolución de llamada en hello tooreport de orden progreso del archivo de saludo de la carga.</span><span class="sxs-lookup"><span data-stu-id="1ad74-187">hello **CreateFromFile** method lets you specify hello file name, encryption option, and a callback in order tooreport hello upload progress of hello file.</span></span>

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

<span data-ttu-id="1ad74-188">Hello en el ejemplo siguiente se llama a la función de UploadFile y especifica cifrado de almacenamiento como opción de creación de hello activos.</span><span class="sxs-lookup"><span data-stu-id="1ad74-188">hello following example calls UploadFile function and specifies storage encryption as hello asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="1ad74-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ad74-189">Next steps</span></span>

<span data-ttu-id="1ad74-190">Ahora puede codificar los recursos cargados.</span><span class="sxs-lookup"><span data-stu-id="1ad74-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="1ad74-191">Para más información, consulte [Encode an asset using Media Encoder Standard with the Azure portal](media-services-portal-encode.md)(Codificación de recursos mediante el estándar de codificador multimedia con Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="1ad74-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="1ad74-192">También puede utilizar las funciones de Azure tootrigger un trabajo de codificación basado en un archivo que llegan en el contenedor de hello configurado.</span><span class="sxs-lookup"><span data-stu-id="1ad74-192">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="1ad74-193">Para más información, consulte [este ejemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="1ad74-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1ad74-194">Rutas de aprendizaje de Media Services</span><span class="sxs-lookup"><span data-stu-id="1ad74-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1ad74-195">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="1ad74-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="1ad74-196">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="1ad74-196">Next step</span></span>
<span data-ttu-id="1ad74-197">Ahora que ha cargado un activo de servicios de tooMedia, vaya a toohello [cómo tooGet un procesador multimedia] [ How tooGet a Media Processor] tema.</span><span class="sxs-lookup"><span data-stu-id="1ad74-197">Now that you have uploaded an asset tooMedia Services, go toohello [How tooGet a Media Processor][How tooGet a Media Processor] topic.</span></span>

[How tooGet a Media Processor]: media-services-get-media-processor.md

