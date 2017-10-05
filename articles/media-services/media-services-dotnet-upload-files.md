---
title: Carga de archivos en una cuenta de Media Services mediante .NET | Microsoft Docs
description: "Aprenda a obtener contenido multimedia en Servicios multimedia mediante la creación y carga de recursos."
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
ms.openlocfilehash: ec8c1da633374ba684f6a0a895c542ee76ef73b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="802a7-103">Cargar archivos en una cuenta de Servicios multimedia mediante .NET</span><span class="sxs-lookup"><span data-stu-id="802a7-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="802a7-104">.NET</span><span class="sxs-lookup"><span data-stu-id="802a7-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="802a7-105">REST</span><span class="sxs-lookup"><span data-stu-id="802a7-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="802a7-106">Portal</span><span class="sxs-lookup"><span data-stu-id="802a7-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="802a7-107">En Servicios multimedia, cargará (o introducirá) los archivos digitales en un recurso.</span><span class="sxs-lookup"><span data-stu-id="802a7-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="802a7-108">La entidad **Asset** puede contener archivos de vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y subtítulos (y los metadatos sobre estos archivos).  Una vez cargados los archivos, el contenido se almacena de forma segura en la nube para un posterior procesamiento y streaming.</span><span class="sxs-lookup"><span data-stu-id="802a7-108">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="802a7-109">Los archivos del recurso se denominan **archivos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="802a7-109">The files in the asset are called **Asset Files**.</span></span> <span data-ttu-id="802a7-110">La instancia de **AssetFile** y el archivo multimedia real son dos objetos distintos.</span><span class="sxs-lookup"><span data-stu-id="802a7-110">The **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="802a7-111">La instancia de AssetFile contiene metadatos sobre el archivo multimedia, mientras que el archivo multimedia contiene el contenido multimedia real.</span><span class="sxs-lookup"><span data-stu-id="802a7-111">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="802a7-112">Se aplican las siguientes consideraciones:</span><span class="sxs-lookup"><span data-stu-id="802a7-112">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="802a7-113">Los Servicios multimedia usan el valor de la propiedad IAssetFile.Name al generar direcciones URL para el contenido de streaming (por ejemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esta razón, no se permite la codificación porcentual.</span><span class="sxs-lookup"><span data-stu-id="802a7-113">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="802a7-114">El valor de la propiedad **Name**no puede tener ninguno de los siguientes [caracteres reservados para la codificación porcentual](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):!*'();:@&=+$,/?%#[]" </span><span class="sxs-lookup"><span data-stu-id="802a7-114">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="802a7-115">Además, solo puede haber un '.' para la extensión del nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="802a7-115">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="802a7-116">La longitud del nombre no debe ser superior a 260 caracteres.</span><span class="sxs-lookup"><span data-stu-id="802a7-116">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="802a7-117">Existe un límite máximo de tamaño de archivo admitido para el procesamiento en Media Services.</span><span class="sxs-lookup"><span data-stu-id="802a7-117">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="802a7-118">Consulte [este](media-services-quotas-and-limitations.md) tema para obtener información más detallada acerca de la limitación de tamaño de archivo.</span><span class="sxs-lookup"><span data-stu-id="802a7-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> * <span data-ttu-id="802a7-119">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="802a7-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="802a7-120">Debe usar el mismo identificador de directiva si siempre usa los mismos permisos de acceso y días, por ejemplo, directivas para localizadores que vayan a aplicarse durante mucho tiempo (directivas distintas a carga).</span><span class="sxs-lookup"><span data-stu-id="802a7-120">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="802a7-121">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="802a7-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="802a7-122">Al crear recursos, puede especificar las siguientes opciones de cifrado.</span><span class="sxs-lookup"><span data-stu-id="802a7-122">When you create assets, you can specify the following encryption options.</span></span> 

* <span data-ttu-id="802a7-123">**Ninguno** : no se utiliza cifrado.</span><span class="sxs-lookup"><span data-stu-id="802a7-123">**None** - No encryption is used.</span></span> <span data-ttu-id="802a7-124">Este es el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="802a7-124">This is the default value.</span></span> <span data-ttu-id="802a7-125">Tenga en cuenta que al utilizar esta opción el contenido no está protegido en tránsito o en reposo en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="802a7-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="802a7-126">Si tiene previsto entregar un MP4 mediante una descarga progresiva, utilice esta opción.</span><span class="sxs-lookup"><span data-stu-id="802a7-126">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="802a7-127">**CommonEncryption** : utilice esta opción si va a cargar contenido que ya se ha cifrado y protegido con cifrado común o DRM de PlayReady (por ejemplo, Smooth Streaming protegido con DRM de PlayReady).</span><span class="sxs-lookup"><span data-stu-id="802a7-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="802a7-128">**EnvelopeEncrypted** : utilice esta opción si va a cargar HLS cifrado con AES.</span><span class="sxs-lookup"><span data-stu-id="802a7-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="802a7-129">Tenga en cuenta que los archivos deben haberse codificado y cifrado con Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="802a7-129">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="802a7-130">**StorageEncrypted** : cifra el contenido no cifrado localmente mediante el cifrado AES de 256 bits y, a continuación, lo carga en el almacenamiento de Azure donde se almacena cifrado en reposo.</span><span class="sxs-lookup"><span data-stu-id="802a7-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="802a7-131">Los recursos protegidos con el cifrado de almacenamiento se descifran automáticamente y se colocan en un sistema de archivos cifrados antes de la codificación y, opcionalmente, se vuelven a cifrar antes de volver a cargarlos como un nuevo recurso de salida.</span><span class="sxs-lookup"><span data-stu-id="802a7-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="802a7-132">El caso de uso principal para el cifrado de almacenamiento es cuando desea proteger los archivos multimedia de entrada de alta calidad con un sólido cifrado en reposo en disco.</span><span class="sxs-lookup"><span data-stu-id="802a7-132">The primary use case for Storage Encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="802a7-133">Los Servicios multimedia proporcionan cifrado de almacenamiento en disco para sus recursos, no por cable como el administrador de derechos digitales (DRM).</span><span class="sxs-lookup"><span data-stu-id="802a7-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="802a7-134">Si el recurso tiene el almacenamiento cifrado, asegúrese de configurar la directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="802a7-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="802a7-135">Para más información, consulte [Configuración de la directiva de entrega de recursos](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="802a7-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="802a7-136">Si especifica que el recurso se cifre con una opción **CommonEncrypted** o una opción **EnvelopeEncypted**, deberá asociar el recurso a un elemento **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="802a7-136">If you specify for your asset to be encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need to associate your asset with a **ContentKey**.</span></span> <span data-ttu-id="802a7-137">Para obtener más información, consulte [Creación de una ContentKey](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="802a7-137">For more information, see [How to create a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="802a7-138">Si especifica que el recurso se cifre con una opción **StorageEncrypted**, el SDK de Media Services para .NET creará un elemento **ContentKey** de **StorageEncrypted** para el recurso.</span><span class="sxs-lookup"><span data-stu-id="802a7-138">If you specify for your asset to be encrypted with a **StorageEncrypted** option, the Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="802a7-139">En este tema se muestra cómo usar el SDK de Servicios multimedia para .NET, así como las extensiones del SDK de Servicios multimedia para .NET para cargar archivos en un recurso de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="802a7-139">This topic shows how to use Media Services .NET SDK as well as Media Services .NET SDK extensions to upload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="802a7-140">Carga de un solo archivo con el SDK .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="802a7-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="802a7-141">El código de ejemplo siguiente usa el SDK de .NET para cargar un único archivo.</span><span class="sxs-lookup"><span data-stu-id="802a7-141">The sample code below uses .NET SDK to upload a single file.</span></span> <span data-ttu-id="802a7-142">Se crean y se destruyen las instancias AccessPolicy y Locator mediante la función Upload.</span><span class="sxs-lookup"><span data-stu-id="802a7-142">The AccessPolicy and Locator are created and destroyed by the Upload function.</span></span> 


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


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="802a7-143">Carga de varios archivos con el SDK .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="802a7-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="802a7-144">El código siguiente muestra cómo crear un recurso y cargar varios archivos.</span><span class="sxs-lookup"><span data-stu-id="802a7-144">The following code shows how to create an asset and upload multiple files.</span></span>

<span data-ttu-id="802a7-145">El código hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="802a7-145">The code does the following:</span></span>

* <span data-ttu-id="802a7-146">Crea un recurso vacío mediante el método CreateEmptyAsset definido en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="802a7-146">Creates an empty asset using the CreateEmptyAsset method defined in the previous step.</span></span>
* <span data-ttu-id="802a7-147">Crea una instancia de **AccessPolicy** que define los permisos y la duración del acceso al recurso.</span><span class="sxs-lookup"><span data-stu-id="802a7-147">Creates an **AccessPolicy** instance that defines the permissions and duration of access to the asset.</span></span>
* <span data-ttu-id="802a7-148">Crea una instancia de **Locator** que proporciona acceso al recurso.</span><span class="sxs-lookup"><span data-stu-id="802a7-148">Creates a **Locator** instance that provides access to the asset.</span></span>
* <span data-ttu-id="802a7-149">Crea una instancia de **BlobTransferClient** .</span><span class="sxs-lookup"><span data-stu-id="802a7-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="802a7-150">Este tipo representa a un cliente que funciona en los blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="802a7-150">This type represents a client that operates on the Azure blobs.</span></span> <span data-ttu-id="802a7-151">En este ejemplo, usamos al cliente para supervisar el progreso de carga.</span><span class="sxs-lookup"><span data-stu-id="802a7-151">In this example we use the client to monitor the upload progress.</span></span> 
* <span data-ttu-id="802a7-152">Enumera los archivos en el directorio especificado y crea una instancia de **AssetFile** para cada archivo.</span><span class="sxs-lookup"><span data-stu-id="802a7-152">Enumerates through files in the specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="802a7-153">Carga los archivos en los Servicios multimedia con el método **UploadAsync** .</span><span class="sxs-lookup"><span data-stu-id="802a7-153">Uploads the files into Media Services using the **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="802a7-154">Use el método UploadAsync para asegurarse de que las llamadas no provocan un bloqueo y los archivos se cargan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="802a7-154">Use the UploadAsync method to ensure that the calls are not blocking and the files are uploaded in parallel.</span></span>
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

                // It is recommended to validate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading the files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as the upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="802a7-155">Al cargar un número elevado de recursos, tenga en cuenta lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="802a7-155">When uploading a large number of assets, consider the following.</span></span>

* <span data-ttu-id="802a7-156">Cree un nuevo objeto **CloudMediaContext** por subproceso.</span><span class="sxs-lookup"><span data-stu-id="802a7-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="802a7-157">La clase **CloudMediaContext** no es segura para subprocesos.</span><span class="sxs-lookup"><span data-stu-id="802a7-157">The **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="802a7-158">Aumente NumberOfConcurrentTransfers desde el valor predeterminado de 2 a un valor superior como 5.</span><span class="sxs-lookup"><span data-stu-id="802a7-158">Increase NumberOfConcurrentTransfers from the default value of 2 to a higher value like 5.</span></span> <span data-ttu-id="802a7-159">La configuración de esta propiedad afecta a todas las instancias de **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="802a7-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="802a7-160">Mantenga ParallelTransferThreadCount en el valor predeterminado de 10.</span><span class="sxs-lookup"><span data-stu-id="802a7-160">Keep ParallelTransferThreadCount at the default value of 10.</span></span>

## <span data-ttu-id="802a7-161"><a id="ingest_in_bulk"></a>Ingesta de activos en bloque con SDK .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="802a7-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="802a7-162">La carga de archivos de recursos de gran tamaño puede ser un obstáculo durante la creación de recursos.</span><span class="sxs-lookup"><span data-stu-id="802a7-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="802a7-163">La ingesta de recursos en masa o "Ingesta en masa" implica la separación de la creación de recursos del proceso de carga.</span><span class="sxs-lookup"><span data-stu-id="802a7-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from the upload process.</span></span> <span data-ttu-id="802a7-164">Para adoptar un enfoque de ingesta en masa, cree un manifiesto (IngestManifest) que describa el recurso y sus archivos asociados.</span><span class="sxs-lookup"><span data-stu-id="802a7-164">To use a bulk ingesting approach, create a manifest (IngestManifest) that describes the asset and its associated files.</span></span> <span data-ttu-id="802a7-165">A continuación, use el método de carga que prefiera para cargar los archivos asociados al contenedor de blobs del manifiesto.</span><span class="sxs-lookup"><span data-stu-id="802a7-165">Then use the upload method of your choice to upload the associated files to the manifest’s blob container.</span></span> <span data-ttu-id="802a7-166">Los Servicios multimedia de Microsoft Azure ven el contenedor de blobs asociado al manifesto.</span><span class="sxs-lookup"><span data-stu-id="802a7-166">Microsoft Azure Media Services watches the blob container associated with the manifest.</span></span> <span data-ttu-id="802a7-167">Una vez que se carga un archivo en el contenedor de blobs, los Servicios multimedia de Microsoft Azure completan la creación de recursos según la configuración del recurso en el manifiesto (IngestManifestAsset).</span><span class="sxs-lookup"><span data-stu-id="802a7-167">Once a file is uploaded to the blob container, Microsoft Azure Media Services completes the asset creation based on the configuration of the asset in the manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="802a7-168">Para crear un nuevo IngestManifest, llame al método Create expuesto por la colección de IngestManifests en CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="802a7-168">To create a new IngestManifest call the Create method exposed by the IngestManifests collection on the CloudMediaContext.</span></span> <span data-ttu-id="802a7-169">Este método creará un nuevo IngestManifest con el nombre de manifesto proporcionado.</span><span class="sxs-lookup"><span data-stu-id="802a7-169">This method will create a new IngestManifest with the manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="802a7-170">Cree los recursos que se asociarán con el IngestManifest en masa.</span><span class="sxs-lookup"><span data-stu-id="802a7-170">Create the assets that will be associated with the bulk IngestManifest.</span></span> <span data-ttu-id="802a7-171">Configure las opciones de cifrado deseadas en el recurso para la ingesta en masa.</span><span class="sxs-lookup"><span data-stu-id="802a7-171">Configure the desired encryption options on the asset for bulk ingesting.</span></span>

    // Create the assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="802a7-172">Un IngestManifestAsset permite asociar un recurso con un IngestManifest en masa para la ingesta en masa.</span><span class="sxs-lookup"><span data-stu-id="802a7-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="802a7-173">También asocia los AssetFiles que conformarán cada recurso.</span><span class="sxs-lookup"><span data-stu-id="802a7-173">It also associates the AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="802a7-174">Para crear un IngestManifestAsset, use el método Create en el contexto del servidor.</span><span class="sxs-lookup"><span data-stu-id="802a7-174">To create an IngestManifestAsset, use the Create method on the server context.</span></span>

<span data-ttu-id="802a7-175">En el ejemplo siguiente se agregan dos nuevos IngestManifestAssets que asocian los dos recursos creados anteriormente al manifesto de ingesta en masa.</span><span class="sxs-lookup"><span data-stu-id="802a7-175">The following example demonstrates adding two new IngestManifestAssets that associate the two assets previously created to the bulk ingest manifest.</span></span> <span data-ttu-id="802a7-176">Además, cada IngestManifestAsset asociad un conjunto de archivos que se cargarán para cada recurso durante la ingesta en masa.</span><span class="sxs-lookup"><span data-stu-id="802a7-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="802a7-177">Puede usar cualquier aplicación cliente de alta velocidad capaz de cargar los archivos de recursos en el URI del contenedor de almacenamiento de blobs proporcionado por la propiedad **IIngestManifest.BlobStorageUriForUpload** de IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="802a7-177">You can use any high speed client application capable of uploading the asset files to the blob storage container URI provided by the **IIngestManifest.BlobStorageUriForUpload** property of the IngestManifest.</span></span> <span data-ttu-id="802a7-178">Un servicio de carga de alta velocidad destacado es [Aspera On Demand para la aplicación de Azure](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span><span class="sxs-lookup"><span data-stu-id="802a7-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="802a7-179">También puede escribir código para cargar los archivos de recursos como se muestra en el ejemplo de código siguiente.</span><span class="sxs-lookup"><span data-stu-id="802a7-179">You can also write code to upload the assets files as shown in the following code example.</span></span>

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

<span data-ttu-id="802a7-180">El código para cargar los archivos de recursos para el ejemplo usado en este tema se muestra en el ejemplo de código siguiente.</span><span class="sxs-lookup"><span data-stu-id="802a7-180">The code for uploading the asset files for the sample used in this topic is shown in the following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="802a7-181">Puede determinar el progreso de la ingesta en bloque de todos los recursos asociados con un manifiesto **IngestManifest** mediante el sondeo de la propiedad Statistics de **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="802a7-181">You can determine the progress of the bulk ingesting for all assets associated with an **IngestManifest** by polling the Statistics property of the **IngestManifest**.</span></span> <span data-ttu-id="802a7-182">Para actualizar la información de progreso, debe usar un **CloudMediaContext** nuevo cada vez que sondee la propiedad Statistics.</span><span class="sxs-lookup"><span data-stu-id="802a7-182">In order to update progress information, you must use a new **CloudMediaContext** each time you poll the Statistics property.</span></span>

<span data-ttu-id="802a7-183">En el ejemplo siguiente se muestra cómo sondear un **IngestManifest**por su Id.</span><span class="sxs-lookup"><span data-stu-id="802a7-183">The following example demonstrates polling an IngestManifest by its **Id**.</span></span>

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



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="802a7-184">Cargar archivos con extensiones del SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="802a7-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="802a7-185">En el ejemplo siguiente se muestra cómo cargar un solo archivo con extensiones del SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="802a7-185">The example below shows how to upload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="802a7-186">En este caso, se usa el método **CreateFromFile**, pero también está disponible la versión asincrónica (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="802a7-186">In this case the **CreateFromFile** method is used, but the asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="802a7-187">El método **CreateFromFile** le permite especificar el nombre de archivo, la opción de cifrado y una devolución de llamada para notificar el progreso de carga del archivo.</span><span class="sxs-lookup"><span data-stu-id="802a7-187">The **CreateFromFile** method lets you specify the file name, encryption option, and a callback in order to report the upload progress of the file.</span></span>

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

<span data-ttu-id="802a7-188">En el ejemplo siguiente se llama a la función UploadFile y se especifica el cifrado de almacenamiento como la opción de creación de recursos.</span><span class="sxs-lookup"><span data-stu-id="802a7-188">The following example calls UploadFile function and specifies storage encryption as the asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="802a7-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="802a7-189">Next steps</span></span>

<span data-ttu-id="802a7-190">Ahora puede codificar los recursos cargados.</span><span class="sxs-lookup"><span data-stu-id="802a7-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="802a7-191">Para más información, consulte [Encode an asset using Media Encoder Standard with the Azure portal](media-services-portal-encode.md)(Codificación de recursos mediante el estándar de codificador multimedia con Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="802a7-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="802a7-192">También puede usar Azure Functions para desencadenar un trabajo de codificación basado en un archivo que llega al contenedor configurado.</span><span class="sxs-lookup"><span data-stu-id="802a7-192">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="802a7-193">Para más información, consulte [este ejemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="802a7-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="802a7-194">Rutas de aprendizaje de Media Services</span><span class="sxs-lookup"><span data-stu-id="802a7-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="802a7-195">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="802a7-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="802a7-196">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="802a7-196">Next step</span></span>
<span data-ttu-id="802a7-197">Ahora que ha cargado un recurso en Media Services, vaya al tema [Obtención de un procesador multimedia][How to Get a Media Processor].</span><span class="sxs-lookup"><span data-stu-id="802a7-197">Now that you have uploaded an asset to Media Services, go to the [How to Get a Media Processor][How to Get a Media Processor] topic.</span></span>

[How to Get a Media Processor]: media-services-get-media-processor.md

