---
title: "Introducción a la entrega de contenido a petición mediante .NET | Microsoft Docs"
description: "Este tutorial le guiará por los pasos necesarios para implementar una aplicación de entrega de contenido a petición con Azure Media Services mediante la API de REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f0be787ba1ccee067fb1d7e6a6554be32f886089
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="66f66-103">Introducción a la entrega de contenido a petición mediante .NET SDK</span><span class="sxs-lookup"><span data-stu-id="66f66-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="66f66-104">Este tutorial le guiará por los pasos necesarios para implementar un servicio básico de entrega de contenido de vídeo bajo demanda (VoD) con la aplicación de Azure Media Services (AMS) mediante el SDK de .NET para Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="66f66-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66f66-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="66f66-105">Prerequisites</span></span>

<span data-ttu-id="66f66-106">Estos son los requisitos previos para completar el tutorial.</span><span class="sxs-lookup"><span data-stu-id="66f66-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="66f66-107">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="66f66-107">An Azure account.</span></span> <span data-ttu-id="66f66-108">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66f66-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="66f66-109">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="66f66-109">A Media Services account.</span></span> <span data-ttu-id="66f66-110">Para crear una cuenta de Media Services, consulte el tema [Creación de una cuenta de Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="66f66-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="66f66-111">.NET Framework 4.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="66f66-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="66f66-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66f66-112">Visual Studio.</span></span>

<span data-ttu-id="66f66-113">Este tutorial incluye las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="66f66-113">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="66f66-114">Inicio de punto de conexión de streaming (mediante Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="66f66-114">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="66f66-115">Creación y configuración de un proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66f66-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="66f66-116">Conexión a la cuenta de Media Services</span><span class="sxs-lookup"><span data-stu-id="66f66-116">Connect to the Media Services account.</span></span>
2. <span data-ttu-id="66f66-117">Carga de un archivo de vídeo.</span><span class="sxs-lookup"><span data-stu-id="66f66-117">Upload a video file.</span></span>
3. <span data-ttu-id="66f66-118">Codificación del archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptativa</span><span class="sxs-lookup"><span data-stu-id="66f66-118">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="66f66-119">Publicación del recurso y obtención de direcciones URL de descarga progresiva y streaming.</span><span class="sxs-lookup"><span data-stu-id="66f66-119">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="66f66-120">Reproduzca el contenido.</span><span class="sxs-lookup"><span data-stu-id="66f66-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="66f66-121">Información general</span><span class="sxs-lookup"><span data-stu-id="66f66-121">Overview</span></span>
<span data-ttu-id="66f66-122">Este tutorial le guiará por los pasos necesarios para implementar una aplicación de entrega de contenido de vídeo a petición (VoD) con el SDK de Azure Media Services (AMS) para .NET.</span><span class="sxs-lookup"><span data-stu-id="66f66-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="66f66-123">Presenta el flujo de trabajo básico de Media Services y la mayoría de los objetos y tareas de programación más comunes necesarios para el desarrollo de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="66f66-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="66f66-124">Al término del tutorial, podrá transmitir o cargar progresivamente un archivo multimedia de ejemplo que cargó, codificó y descargó.</span><span class="sxs-lookup"><span data-stu-id="66f66-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="66f66-125">Modelo AMS</span><span class="sxs-lookup"><span data-stu-id="66f66-125">AMS model</span></span>

<span data-ttu-id="66f66-126">En la ilustración siguiente se muestran algunos de los objetos que se utilizan con más frecuencia al desarrollar aplicaciones de VoD con el modelo OData de Media Services.</span><span class="sxs-lookup"><span data-stu-id="66f66-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="66f66-127">Haga clic en la imagen para verla a tamaño completo.</span><span class="sxs-lookup"><span data-stu-id="66f66-127">Click the image to view it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="66f66-128">Puede ver el modelo completo [aquí](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="66f66-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="66f66-129">Inicio de los puntos de conexión de streaming con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="66f66-129">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="66f66-130">Cuando se trabaja con Azure Media Services, uno de los escenarios más comunes es entregar contenido de vídeo a los clientes mediante streaming con velocidad de bits adaptable.</span><span class="sxs-lookup"><span data-stu-id="66f66-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="66f66-131">Media Services proporciona empaquetado dinámico que permite entregar contenido codificado MP4 con velocidad de bits adaptable en formatos de streaming admitidos por Media Services (MPEG DASH, HLS, Smooth Streaming) justo a tiempo, sin tener que almacenar versiones previamente empaquetadas de cada uno de estos formatos.</span><span class="sxs-lookup"><span data-stu-id="66f66-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="66f66-132">Cuando se crea la cuenta de AMS, se agrega un punto de conexión de streaming **predeterminado** a la cuenta en estado **Stopped** (Detenido).</span><span class="sxs-lookup"><span data-stu-id="66f66-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="66f66-133">Para iniciar la transmisión del contenido y aprovechar el empaquetado dinámico y el cifrado dinámico, el punto de conexión de streaming desde el que va a transmitir el contenido debe estar en estado **Running** (En ejecución).</span><span class="sxs-lookup"><span data-stu-id="66f66-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="66f66-134">Para iniciar el punto de conexión de streaming, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="66f66-134">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="66f66-135">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="66f66-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="66f66-136">En la ventana Settings (Configuración), haga clic en Streaming endpoints (Puntos de conexión de streaming).</span><span class="sxs-lookup"><span data-stu-id="66f66-136">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="66f66-137">Haga clic en el punto de conexión de streaming predeterminado.</span><span class="sxs-lookup"><span data-stu-id="66f66-137">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="66f66-138">Aparecerá la ventana de detalles del punto de conexión de streaming predeterminado.</span><span class="sxs-lookup"><span data-stu-id="66f66-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="66f66-139">Haga clic en el icono de inicio.</span><span class="sxs-lookup"><span data-stu-id="66f66-139">Click the Start icon.</span></span>
5. <span data-ttu-id="66f66-140">Haga clic en el botón Save (Guardar) para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="66f66-140">Click the Save button to save your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="66f66-141">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66f66-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="66f66-142">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="66f66-142">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="66f66-143">Cree una carpeta nueva (la carpeta puede estar en cualquier lugar del disco duro) y copie el archivo .mp4 o .wmv que desea codificar para reproducirlo en streaming o descargarlo progresivamente.</span><span class="sxs-lookup"><span data-stu-id="66f66-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="66f66-144">En este ejemplo, se usa la ruta de acceso "C:\VideoFiles".</span><span class="sxs-lookup"><span data-stu-id="66f66-144">In this example, the "C:\VideoFiles" path is used.</span></span>

## <a name="connect-to-the-media-services-account"></a><span data-ttu-id="66f66-145">Conexión a la cuenta de Media Services</span><span class="sxs-lookup"><span data-stu-id="66f66-145">Connect to the Media Services account</span></span>

<span data-ttu-id="66f66-146">Cuando se usa Media Services con .NET, debe usar la clase **CloudMediaContext** para la mayoría de las tareas de programación de Media Services: conexión a la cuenta de Media Services; creación, actualización, acceso y eliminación de los siguientes objetos: activos, archivos de activos, trabajos, directivas de acceso, localizadores, etc.</span><span class="sxs-lookup"><span data-stu-id="66f66-146">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="66f66-147">Sobrescriba la clase de programa predeterminada con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="66f66-147">Overwrite the default Program class with the following code.</span></span> <span data-ttu-id="66f66-148">El código muestra cómo leer los valores de conexión del archivo App.config y cómo crear el objeto **CloudMediaContext** para conectarse a Media Services.</span><span class="sxs-lookup"><span data-stu-id="66f66-148">The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span></span> <span data-ttu-id="66f66-149">Para más información, consulte [Conexión a la API de Media Services](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="66f66-149">For more information, see [connecting to the Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="66f66-150">No olvide actualizar el nombre de archivo y la ruta de acceso con la ubicación del archivo multimedia.</span><span class="sxs-lookup"><span data-stu-id="66f66-150">Make sure to update the file name and path to where you have your media file.</span></span>

<span data-ttu-id="66f66-151">La función **Main** llama a métodos que se definirán más adelante en esta sección.</span><span class="sxs-lookup"><span data-stu-id="66f66-151">The **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="66f66-152">Recibirá errores de compilación hasta que agregue las definiciones para todas las funciones.</span><span class="sxs-lookup"><span data-stu-id="66f66-152">You will be getting compilation errors until you add definitions for all the functions.</span></span>

    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls to methods defined in this section.
            // Make sure to update the file name and path to where you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse the XML error message in the Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="66f66-153">Creación de un nuevo recurso y carga de un archivo de vídeo</span><span class="sxs-lookup"><span data-stu-id="66f66-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="66f66-154">En Media Services, cargará (o especificará) los archivos digitales en un recurso.</span><span class="sxs-lookup"><span data-stu-id="66f66-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="66f66-155">La entidad **Recurso** puede contener archivos de vídeo, audio, imágenes, colecciones de miniaturas, pistas de texto y subtítulos (y los metadatos acerca de estos archivos).  Una vez cargados los archivos, el contenido se almacena de forma segura en la nube para un posterior procesamiento y streaming.</span><span class="sxs-lookup"><span data-stu-id="66f66-155">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> <span data-ttu-id="66f66-156">Los archivos del recurso se denominan **archivos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="66f66-156">The files in the asset are called **Asset Files**.</span></span>

<span data-ttu-id="66f66-157">El método **UploadFile** definido a continuación llama a **CreateFromFile** (definido en las extensiones del SDK para .NET).</span><span class="sxs-lookup"><span data-stu-id="66f66-157">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="66f66-158">**CreateFromFile** crea un nuevo recurso en el que se carga el archivo de origen especificado.</span><span class="sxs-lookup"><span data-stu-id="66f66-158">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span></span>

<span data-ttu-id="66f66-159">El método **CreateFromFile** toma **AssetCreationOptions**, que permite especificar una de las siguientes opciones de creación de recursos:</span><span class="sxs-lookup"><span data-stu-id="66f66-159">The **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of the following asset creation options:</span></span>

* <span data-ttu-id="66f66-160">**Ninguno** : no se utiliza cifrado.</span><span class="sxs-lookup"><span data-stu-id="66f66-160">**None** - No encryption is used.</span></span> <span data-ttu-id="66f66-161">Este es el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="66f66-161">This is the default value.</span></span> <span data-ttu-id="66f66-162">Tenga en cuenta que al usar esta opción el contenido no está protegido en tránsito o en reposo en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="66f66-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="66f66-163">Si tiene previsto entregar un MP4 mediante una descarga progresiva, utilice esta opción.</span><span class="sxs-lookup"><span data-stu-id="66f66-163">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="66f66-164">**StorageEncrypted**: use esta opción para cifrar el contenido no cifrado de manera local mediante el cifrado Estándar de cifrado avanzado (AES) de 256 bits y luego cargarlo en Azure Storage, donde se almacena cifrado en reposo.</span><span class="sxs-lookup"><span data-stu-id="66f66-164">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="66f66-165">Los recursos protegidos con el cifrado de almacenamiento se descifran automáticamente y se colocan en un sistema de archivos cifrados antes de la codificación y, opcionalmente, se vuelven a cifrar antes de volver a cargarlos como un nuevo recurso de salida.</span><span class="sxs-lookup"><span data-stu-id="66f66-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="66f66-166">El caso de uso principal para el cifrado de almacenamiento es cuando desea proteger los archivos multimedia de entrada de alta calidad con un sólido cifrado en reposo en disco.</span><span class="sxs-lookup"><span data-stu-id="66f66-166">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="66f66-167">**CommonEncryptionProtected** : use esta opción si va a cargar contenido que ya se cifró y protegió con cifrado común o DRM de PlayReady (por ejemplo, Smooth Streaming protegido con DRM de PlayReady).</span><span class="sxs-lookup"><span data-stu-id="66f66-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="66f66-168">**EnvelopeEncryptionProtected** : use esta opción si va a cargar HLS cifrado con AES.</span><span class="sxs-lookup"><span data-stu-id="66f66-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="66f66-169">Tenga en cuenta que los archivos deben haberse codificado y cifrado con Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="66f66-169">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="66f66-170">El método **CreateFromFile** también permite especificar una devolución de llamada para notificar el progreso de carga del archivo.</span><span class="sxs-lookup"><span data-stu-id="66f66-170">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span></span>

<span data-ttu-id="66f66-171">En el siguiente ejemplo especificamos **Ninguno** para las opciones del activo.</span><span class="sxs-lookup"><span data-stu-id="66f66-171">In the following example, we specify **None** for the asset options.</span></span>

<span data-ttu-id="66f66-172">Agregue el método siguiente a la clase Program</span><span class="sxs-lookup"><span data-stu-id="66f66-172">Add the following method to the Program class.</span></span>

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


## <a name="encode-the-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="66f66-173">Codificación del archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptativa</span><span class="sxs-lookup"><span data-stu-id="66f66-173">Encode the source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="66f66-174">Después de especificar los recursos en Media Services, los elementos multimedia se pueden codificar, transmultiplexar, agregar una marca de agua, entre otras opciones, antes de entregarse a los clientes.</span><span class="sxs-lookup"><span data-stu-id="66f66-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="66f66-175">Estas actividades se programan y se ejecutan en varias instancias de rol en segundo plano para garantizar la disponibilidad y alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="66f66-175">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="66f66-176">Estas actividades se denominan trabajos y cada trabajo está compuesto de tareas atómicas que realizan el trabajo real en el archivo del recurso.</span><span class="sxs-lookup"><span data-stu-id="66f66-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span></span>

<span data-ttu-id="66f66-177">Como se ha indicado antes, cuando se trabaja con Azure Media Services, uno de los escenarios más comunes es ofrecer streaming con velocidad de bits adaptable a los clientes.</span><span class="sxs-lookup"><span data-stu-id="66f66-177">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="66f66-178">Media Services puede empaquetar de manera dinámica un conjunto de archivos MP4 de velocidad de bits adaptable en uno de los siguientes formatos: HTTP Live Streaming (HLS), Smooth Streaming y MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="66f66-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="66f66-179">Para aprovechar el empaquetado dinámico, tiene que modificar o transcodificar el archivo intermedio (origen) en un conjunto de archivos MP4 de velocidad de bits adaptable o de Smooth Streaming de velocidad de bits adaptable.</span><span class="sxs-lookup"><span data-stu-id="66f66-179">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="66f66-180">El código siguiente muestra cómo enviar un trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="66f66-180">The following code shows how to submit an encoding job.</span></span> <span data-ttu-id="66f66-181">El trabajo contiene una tarea que especifica la transcodificación del archivo intermedio en un conjunto de MP4 de velocidades de bits adaptables con el **Estándar de Codificador multimedia**.</span><span class="sxs-lookup"><span data-stu-id="66f66-181">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="66f66-182">El código envía el trabajo y espera hasta que se complete.</span><span class="sxs-lookup"><span data-stu-id="66f66-182">The code submits the job and waits until it is completed.</span></span>

<span data-ttu-id="66f66-183">Una vez completado el trabajo, debería poder transmitir el recurso o descargar progresivamente archivos MP4 creados como resultado de la transcodificación.</span><span class="sxs-lookup"><span data-stu-id="66f66-183">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="66f66-184">Agregue el método siguiente a la clase Program</span><span class="sxs-lookup"><span data-stu-id="66f66-184">Add the following method to the Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task to transcode the specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit the job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-the-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="66f66-185">Publicación del recurso y obtención de direcciones URL para streaming y descarga progresiva</span><span class="sxs-lookup"><span data-stu-id="66f66-185">Publish the asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="66f66-186">Para transmitir o descargar un recurso, necesita "publicarlo" mediante la creación de un localizador.</span><span class="sxs-lookup"><span data-stu-id="66f66-186">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="66f66-187">Los localizadores proporcionan acceso a los archivos contenidos en el recurso.</span><span class="sxs-lookup"><span data-stu-id="66f66-187">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="66f66-188">Media Services admite dos tipos de localizadores: OnDemandOrigin, que se usan para transmitir contenido multimedia (por ejemplo, MPEG DASH, HLS o Smooth Streaming) y localizadores de firma de acceso (SAS), que se usan para descargar archivos multimedia (para más información sobre los localizadores SAS, lea [este](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span><span class="sxs-lookup"><span data-stu-id="66f66-188">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="66f66-189">Algunos detalles sobre los formatos de direcciones URL</span><span class="sxs-lookup"><span data-stu-id="66f66-189">Some details about URL formats</span></span>

<span data-ttu-id="66f66-190">Una vez creados los localizadores, puede generar las direcciones URL que se van a utilizar para reproducir los archivos en streaming o descargarlos.</span><span class="sxs-lookup"><span data-stu-id="66f66-190">After you create the locators, you can build the URLs that would be used to stream or download your files.</span></span> <span data-ttu-id="66f66-191">En el ejemplo de este tutorial, la salida mostrará direcciones URL, que puede pegar en los exploradores correspondientes.</span><span class="sxs-lookup"><span data-stu-id="66f66-191">The sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="66f66-192">En esta sección se incluyen breves ejemplos del aspecto de los diferentes formatos.</span><span class="sxs-lookup"><span data-stu-id="66f66-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-the-following-format"></a><span data-ttu-id="66f66-193">Una dirección URL de streaming de MPEG DASH tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="66f66-193">A streaming URL for MPEG DASH has the following format:</span></span>

<span data-ttu-id="66f66-194">{nombre del punto de conexión de streaming-nombre de la cuenta de media services}.streaming.mediaservices.windows.net/{id. de localizador}/{nombre del archivo}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="66f66-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-the-following-format"></a><span data-ttu-id="66f66-195">Una dirección URL de streaming de HLS tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="66f66-195">A streaming URL for HLS has the following format:</span></span>

<span data-ttu-id="66f66-196">{nombre del punto de conexión de streaming-nombre de la cuenta de media services}.streaming.mediaservices.windows.net/{id. de localizador}/{nombre del archivo}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="66f66-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-the-following-format"></a><span data-ttu-id="66f66-197">Una dirección URL de streaming de Smooth Streaming tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="66f66-197">A streaming URL for Smooth Streaming has the following format:</span></span>

<span data-ttu-id="66f66-198">{nombre de punto de conexión de streaming-nombre de cuenta de Media Services}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="66f66-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-to-download-files-has-the-following-format"></a><span data-ttu-id="66f66-199">Una dirección URL de SAS utilizada para descargar archivos tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="66f66-199">A SAS URL used to download files has the following format:</span></span>

<span data-ttu-id="66f66-200">{nombre del contenedor de blobs}/{nombre del recurso}/{nombre del archivo}/{firma de SAS}</span><span class="sxs-lookup"><span data-stu-id="66f66-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="66f66-201">Las extensiones de SDK de Media Services para .NET ofrecen útiles métodos auxiliares que devuelven direcciones URL con formato para el recurso publicado.</span><span class="sxs-lookup"><span data-stu-id="66f66-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span></span>

<span data-ttu-id="66f66-202">El código siguiente usa extensiones del SDK de .NET para crear localizadores y obtener las direcciones URL de streaming y descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="66f66-202">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span></span> <span data-ttu-id="66f66-203">El código también muestra cómo descargar los archivos en una carpeta local.</span><span class="sxs-lookup"><span data-stu-id="66f66-203">The code also shows how to download files to a local folder.</span></span>

<span data-ttu-id="66f66-204">Agregue el método siguiente a la clase Program</span><span class="sxs-lookup"><span data-stu-id="66f66-204">Add the following method to the Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish the output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and the Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get the URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  the streaming URLs.
        Console.WriteLine("Use the following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display the URLs for progressive download.
        Console.WriteLine("Use the following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download the output asset to a local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files to a local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="66f66-205">Prueba mediante la reproducción de contenido</span><span class="sxs-lookup"><span data-stu-id="66f66-205">Test by playing your content</span></span>

<span data-ttu-id="66f66-206">Una vez ejecutado el programa definido en la sección anterior, se mostrarán las direcciones URL similares a la siguiente en la ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="66f66-206">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span></span>

<span data-ttu-id="66f66-207">Direcciones URL de streaming adaptable:</span><span class="sxs-lookup"><span data-stu-id="66f66-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="66f66-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="66f66-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="66f66-209">HLS</span><span class="sxs-lookup"><span data-stu-id="66f66-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="66f66-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="66f66-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="66f66-211">Direcciones URL de descarga progresiva (audio y vídeo).</span><span class="sxs-lookup"><span data-stu-id="66f66-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="66f66-212">Para transmitir el vídeo, copie la dirección URL en el cuadro de texto URL de [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="66f66-212">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="66f66-213">Para probar la descarga progresiva, pegue una dirección URL en un explorador (por ejemplo, Internet Explorer, Chrome o Safari).</span><span class="sxs-lookup"><span data-stu-id="66f66-213">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="66f66-214">Para obtener más información, consulte los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="66f66-214">For more information, see the following topics:</span></span>

- [<span data-ttu-id="66f66-215">Reproducir contenido con reproductores existentes</span><span class="sxs-lookup"><span data-stu-id="66f66-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="66f66-216">Desarrollo de aplicaciones para reproductor de vídeo</span><span class="sxs-lookup"><span data-stu-id="66f66-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="66f66-217">Incrustación de un vídeo de transmisión por secuencias adaptativa MPEG-DASH en una aplicación HTML5 con DASH.js</span><span class="sxs-lookup"><span data-stu-id="66f66-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="66f66-218">Descarga de un ejemplo</span><span class="sxs-lookup"><span data-stu-id="66f66-218">Download sample</span></span>
<span data-ttu-id="66f66-219">El ejemplo siguiente contiene el código que creó en este tutorial: [ejemplo](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="66f66-219">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="66f66-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66f66-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="66f66-221">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="66f66-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
