---
title: "un activo con Media Encoder estándar mediante .NET aaaEncode | Documentos de Microsoft"
description: "Este tema se muestra cómo toouse .NET tooencode un activo mediante el estándar de codificador multimedia."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="c157f-103">Codificación de un recurso mediante Estándar de codificador multimedia</span><span class="sxs-lookup"><span data-stu-id="c157f-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="c157f-104">Trabajos de codificación son una de las operaciones de procesamiento más habituales de hello en los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="c157f-104">Encoding jobs are one of hello most common processing operations in Media Services.</span></span> <span data-ttu-id="c157f-105">Crear archivos multimedia de codificación trabajos tooconvert desde una tooanother de codificación.</span><span class="sxs-lookup"><span data-stu-id="c157f-105">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="c157f-106">Al codificar, puede usar Hola Codificador multimedia integrado de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="c157f-106">When you encode, you can use hello Media Services built-in Media Encoder.</span></span> <span data-ttu-id="c157f-107">También puede utilizar un codificador proporcionado por un socio de servicios multimedia; codificadores de terceros están disponibles a través de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c157f-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through hello Azure Marketplace.</span></span> 

<span data-ttu-id="c157f-108">Este tema se muestra cómo toouse .NET tooencode sus activos con medios codificador estándar (MES).</span><span class="sxs-lookup"><span data-stu-id="c157f-108">This topic shows how toouse .NET tooencode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="c157f-109">Media Encoder estándar se configura mediante uno de los valores predefinidos del codificador Hola descritos [aquí](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="c157f-109">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="c157f-110">Se recomienda tooalways codificar los archivos de origen en un conjunto de MP4 de velocidad de bits adaptativa y, a continuación, convertir mediante Hola Hola conjunto toohello deseado formato [empaquetado dinámico](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c157f-110">It is recommended tooalways encode your source files into an adaptive bitrate MP4 set and then convert hello set toohello desired format using hello [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="c157f-111">Si el recurso de salida tiene el almacenamiento cifrado, asegúrese de configurar la directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="c157f-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="c157f-112">Para más información, consulte [Configuración de la directiva de entrega de recursos](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="c157f-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c157f-113">Genera MES con un nombre que contiene un archivo de salida Hola 32 primeros caracteres de Hola nombre de archivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="c157f-113">MES produces an output file with a name that contains hello first 32 characters of hello input file name.</span></span> <span data-ttu-id="c157f-114">nombre de Hola se basa en lo que se especifique en el archivo de valores preestablecidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c157f-114">hello name is based on what is specified in hello preset file.</span></span> <span data-ttu-id="c157f-115">Por ejemplo, "FileName": "{nombreBase}_{índice}{extensión}".</span><span class="sxs-lookup"><span data-stu-id="c157f-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="c157f-116">{Basename} se reemplaza por hello 32 primeros caracteres del nombre de archivo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c157f-116">{Basename} is replaced by hello first 32 characters of hello input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="c157f-117">Formatos de MES</span><span class="sxs-lookup"><span data-stu-id="c157f-117">MES Formats</span></span>
[<span data-ttu-id="c157f-118">Códecs y formatos</span><span class="sxs-lookup"><span data-stu-id="c157f-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="c157f-119">Valores preestablecidos de MES</span><span class="sxs-lookup"><span data-stu-id="c157f-119">MES Presets</span></span>
<span data-ttu-id="c157f-120">Media Encoder estándar se configura mediante uno de los valores predefinidos del codificador Hola descritos [aquí](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="c157f-120">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="c157f-121">Metadatos de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="c157f-121">Input and output metadata</span></span>
<span data-ttu-id="c157f-122">Al codificar un activo de entrada (o activos) el uso de MES, obtendrá un recurso de salida en hello finalización correcta de los que codificar la tarea.</span><span class="sxs-lookup"><span data-stu-id="c157f-122">When you encode an input asset (or assets) using MES, you get an output asset at hello successful completion of that encode task.</span></span> <span data-ttu-id="c157f-123">Hola activo de salida contiene vídeo, audio, miniaturas, manifiesto, etc., basado en el valor predeterminado de codificación de hello que usa.</span><span class="sxs-lookup"><span data-stu-id="c157f-123">hello output asset contains video, audio, thumbnails, manifest, etc. based on hello encoding preset you use.</span></span>

<span data-ttu-id="c157f-124">recurso de salida de Hello también contiene un archivo con metadatos sobre el recurso de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c157f-124">hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="c157f-125">nombre del archivo XML de metadatos de hello Hello tiene Hola siguiendo el formato: < asset_id > _metadata.xml (por ejemplo, 41114ad3-eb5e - 4c 57-8d 92-5354e2b7d4a4_metadata.xml), donde < id_recurso > es valor de AssetId Hola de recurso de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c157f-125">hello name of hello metadata XML file has hello following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is hello AssetId value of hello input asset.</span></span> <span data-ttu-id="c157f-126">Hello esquema de esta entrado metadatos XML se describe [aquí](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c157f-126">hello schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="c157f-127">recurso de salida de Hello también contiene un archivo con metadatos sobre el recurso de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="c157f-127">hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="c157f-128">nombre del archivo XML de metadatos de hello Hello tiene Hola siguiendo el formato: < nombre_archivo_origen > _manifest.xml (por ejemplo, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="c157f-128">hello name of hello metadata XML file has hello following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="c157f-129">esquema de Hola de estos metadatos de salida XML se describe [aquí](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c157f-129">hello schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="c157f-130">Si desea tooexamine cualquiera de los archivos de metadatos de hello dos, puede crear un localizador SAS y descargar el equipo local de hello archivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="c157f-130">If you want tooexamine either of hello two metadata files, you can create a SAS locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="c157f-131">Puede encontrar un ejemplo sobre cómo toocreate un localizador SAS y descargar un archivo mediante hello de servicios multimedia extensiones del SDK de. NET.</span><span class="sxs-lookup"><span data-stu-id="c157f-131">You can find an example on how toocreate a SAS locator and download a file Using hello Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="c157f-132">Descarga de un ejemplo</span><span class="sxs-lookup"><span data-stu-id="c157f-132">Download sample</span></span>
<span data-ttu-id="c157f-133">Puede obtener y ejecutar un ejemplo que muestra cómo tooencode con el MES de [aquí](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="c157f-133">You can get and run a sample that shows how tooencode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="c157f-134">Código de ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="c157f-134">.NET sample code</span></span>

<span data-ttu-id="c157f-135">Hola el ejemplo de código siguiente utiliza Hola de Media Services .NET SDK tooperform siguiente las tareas:</span><span class="sxs-lookup"><span data-stu-id="c157f-135">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="c157f-136">Crear un trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="c157f-136">Create an encoding job.</span></span>
* <span data-ttu-id="c157f-137">Obtiene un Codificador multimedia codificador estándar toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="c157f-137">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="c157f-138">Especificar hello toouse [transmisión por secuencias adaptativa](media-services-autogen-bitrate-ladder-with-mes.md) preestablecido.</span><span class="sxs-lookup"><span data-stu-id="c157f-138">Specify toouse hello [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="c157f-139">Agregar un único trabajo de codificación tarea toohello.</span><span class="sxs-lookup"><span data-stu-id="c157f-139">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="c157f-140">Especificar la entrada de hello toobe activo codificado.</span><span class="sxs-lookup"><span data-stu-id="c157f-140">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="c157f-141">Crear un recurso de salida que contendrá asset Hola codificado.</span><span class="sxs-lookup"><span data-stu-id="c157f-141">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="c157f-142">Agregue un progreso del controlador de eventos toocheck Hola trabajo.</span><span class="sxs-lookup"><span data-stu-id="c157f-142">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="c157f-143">Enviar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c157f-143">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c157f-144">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c157f-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="c157f-145">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c157f-145">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="c157f-146">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c157f-146">Example</span></span> 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    // Get an uploaded asset.
                    var asset = _context.Assets.FirstOrDefault();

                    // Encode and generate hello output using hello "Adaptive Streaming" preset.
                    EncodeToAdaptiveBitrateMP4Set(asset);

                    Console.ReadLine();
                }

                static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Media Encoder Standard Job");
                    // Get a media processor reference, and pass tooit hello name of hello 
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
                        processor,
                        "Adaptive Streaming",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(asset);
                    // Add an output asset toocontain hello results of hello job. 
                    // This output is specified as AssetCreationOptions.None, which 
                    // means hello output asset is not encrypted. 
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
                    job.Submit();
                    job.GetExecutionProgressTask(CancellationToken.None).Wait();

                    return job.OutputMediaAssets[0];
                }

                private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
                {
                    Console.WriteLine("Job state changed event:");
                    Console.WriteLine("  Previous state: " + e.PreviousState);
                    Console.WriteLine("  Current state: " + e.CurrentState);
                    switch (e.CurrentState)
                    {
                        case JobState.Finished:
                            Console.WriteLine();
                            Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
                            break;
                        case JobState.Canceling:
                        case JobState.Queued:
                        case JobState.Scheduled:
                        case JobState.Processing:
                            Console.WriteLine("Please wait...\n");
                            break;
                        case JobState.Canceled:
                        case JobState.Error:

                            // Cast sender as a job.
                            IJob job = (IJob)sender;

                            // Display or log error details as needed.
                            break;
                        default:
                            break;
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
            }
        }

## <a name="media-services-learning-paths"></a><span data-ttu-id="c157f-147">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="c157f-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c157f-148">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="c157f-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c157f-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c157f-149">Next steps</span></span>
<span data-ttu-id="c157f-150">[Cómo miniatura toogenerate con Media Encoder estándar .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[codificación Introducción a servicios multimedia](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="c157f-150">[How toogenerate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

