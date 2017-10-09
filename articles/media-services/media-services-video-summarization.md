---
title: "aaaUse miniaturas de vídeo de multimedia de Azure tooCreate un resumen de vídeo | Documentos de Microsoft"
description: "Resumen de vídeo puede ayudar a crear resúmenes de los vídeos largos seleccionando automáticamente interesantes fragmentos de vídeo de origen de Hola. Esto es útil cuando se desea una introducción rápida de qué tooexpect en un vídeo largo tooprovide."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 0a8f0bba6c12a948b940114fe4937e675688a8c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a><span data-ttu-id="e1e9e-104">Usar vistas en miniatura de Azure Media Video tooCreate un resumen de vídeo</span><span class="sxs-lookup"><span data-stu-id="e1e9e-104">Use Azure Media Video Thumbnails tooCreate a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="e1e9e-105">Información general</span><span class="sxs-lookup"><span data-stu-id="e1e9e-105">Overview</span></span>
<span data-ttu-id="e1e9e-106">Hola **las miniaturas de vídeo de multimedia de Azure** procesador multimedia (MP) le permite toocreate un resumen de un vídeo que sea útil toocustomers que solo desea toopreview un resumen de un vídeo largo.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-106">hello **Azure Media Video Thumbnails** media processor (MP) enables you toocreate a summary of a video that is useful toocustomers who just want toopreview a summary of a long video.</span></span> <span data-ttu-id="e1e9e-107">Por ejemplo, los clientes podrían desear toosee un breve "resumen vídeo" cuando mantenga el mouse sobre una vista en miniatura.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-107">For example, customers might want toosee a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="e1e9e-108">Ajustando los parámetros de Hola de **miniaturas de vídeo de multimedia de Azure** a través de un valor preestablecido de configuración, puede utilizar la detección de capturas eficaz Hola del módulo de administración y concatenación tecnología tooalgorithmically generar un subclip descriptivo.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-108">By tweaking hello parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use hello MP's powerful shot detection and concatenation technology tooalgorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="e1e9e-109">Hola **miniatura de vídeo de multimedia de Azure** MP está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-109">hello **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="e1e9e-110">Este tema proporciona detalles acerca de **miniatura de vídeo de multimedia de Azure** y muestra cómo toouse con el SDK de servicios multimedia para. NET.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="e1e9e-111">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="e1e9e-111">Limitations</span></span>

<span data-ttu-id="e1e9e-112">En algunos casos, si el vídeo no está formado por diferentes escenas, salida de hello solo será una captura única.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-112">In some cases, if your video is not comprised of different scenes, hello output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="e1e9e-113">Ejemplo de resumen de vídeo</span><span class="sxs-lookup"><span data-stu-id="e1e9e-113">Video summary example</span></span>
<span data-ttu-id="e1e9e-114">Estos son algunos ejemplos de qué procesador multimedia Azure Media Video miniaturas Hola puede hacer:</span><span class="sxs-lookup"><span data-stu-id="e1e9e-114">Here are some examples of what hello Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="e1e9e-115">Vídeo original</span><span class="sxs-lookup"><span data-stu-id="e1e9e-115">Original video</span></span>
[<span data-ttu-id="e1e9e-116">Vídeo original</span><span class="sxs-lookup"><span data-stu-id="e1e9e-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="e1e9e-117">Resultado de miniaturas de vídeo</span><span class="sxs-lookup"><span data-stu-id="e1e9e-117">Video thumbnail result</span></span>
[<span data-ttu-id="e1e9e-118">Resultado de miniaturas de vídeo</span><span class="sxs-lookup"><span data-stu-id="e1e9e-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="e1e9e-119">Configuración de tareas (valor preestablecido)</span><span class="sxs-lookup"><span data-stu-id="e1e9e-119">Task configuration (preset)</span></span>
<span data-ttu-id="e1e9e-120">Al crear una tarea de miniatura de vídeo con **Miniaturas de vídeo multimedia de Azure**, debe especificar un valor predeterminado de configuración.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="e1e9e-121">Hola en miniatura ejemplo anterior se creó con hello después de la configuración básica de JSON:</span><span class="sxs-lookup"><span data-stu-id="e1e9e-121">hello above thumbnail sample was created with hello following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="e1e9e-122">Actualmente, puede cambiar Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="e1e9e-122">Currently, you can change hello following parameters:</span></span>

| <span data-ttu-id="e1e9e-123">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e1e9e-123">Param</span></span> | <span data-ttu-id="e1e9e-124">Description</span><span class="sxs-lookup"><span data-stu-id="e1e9e-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e1e9e-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="e1e9e-125">outputAudio</span></span> |<span data-ttu-id="e1e9e-126">Especifica si se permite o no vídeo resultante de hello contiene audio.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-126">Specifies whether or not hello resultant video contains any audio.</span></span> <br/><span data-ttu-id="e1e9e-127">Los valores permitidos son: True o False.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-127">Allowed values are: True or False.</span></span> <span data-ttu-id="e1e9e-128">El valor predeterminado es True.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-128">Default is True.</span></span> |
| <span data-ttu-id="e1e9e-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="e1e9e-129">fadeInFadeOut</span></span> |<span data-ttu-id="e1e9e-130">Especifica si no realiza la transición atenuación utilizados entre las miniaturas de movimiento independientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-130">Specifies whether or not fade transitions are used between hello separate motion thumbnails.</span></span>  <br/><span data-ttu-id="e1e9e-131">Los valores permitidos son: True o False.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="e1e9e-132">El valor predeterminado es True.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-132">Default is True.</span></span> |
| <span data-ttu-id="e1e9e-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="e1e9e-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="e1e9e-134">Entero que especifica cuánto tiempo Hola todo resultante vídeo será.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-134">Integer that specifies how long hello entire resultant video shall be.</span></span>  <span data-ttu-id="e1e9e-135">El valor predeterminado depende de la duración del vídeo original.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="e1e9e-136">Hello tabla siguiente describen duración predeterminada de hello, cuando **maxMotionThumbnailInSecs** no se utiliza.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-136">hello following table describes hello default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e1e9e-137">Duración del vídeo</span><span class="sxs-lookup"><span data-stu-id="e1e9e-137">Video duration</span></span> |<span data-ttu-id="e1e9e-138">d < 3 min</span><span class="sxs-lookup"><span data-stu-id="e1e9e-138">d < 3 min</span></span> |<span data-ttu-id="e1e9e-139">3 min < d < 15 min</span><span class="sxs-lookup"><span data-stu-id="e1e9e-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="e1e9e-140">Duración de la miniatura</span><span class="sxs-lookup"><span data-stu-id="e1e9e-140">Thumbnail duration</span></span> |<span data-ttu-id="e1e9e-141">15 s (2-3 escenas)</span><span class="sxs-lookup"><span data-stu-id="e1e9e-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="e1e9e-142">30 s (3-5 escenas)</span><span class="sxs-lookup"><span data-stu-id="e1e9e-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="e1e9e-143">Hello JSON siguiente establece los parámetros disponibles.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-143">hello following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="e1e9e-144">Código de ejemplo de .NET</span><span class="sxs-lookup"><span data-stu-id="e1e9e-144">.NET sample code</span></span>

<span data-ttu-id="e1e9e-145">siguiente de Hello programa muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="e1e9e-145">hello following program shows how to:</span></span>

1. <span data-ttu-id="e1e9e-146">Crear un activo y cargar un archivo multimedia en activo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-146">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="e1e9e-147">Crea un trabajo con una tarea de miniatura vídeo basada en un archivo de configuración que contiene Hola siguiente valor preestablecido de json.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-147">Creates a job with a video thumbnail task based on a configuration file that contains hello following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="e1e9e-148">Descarga los archivos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="e1e9e-148">Downloads hello output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e1e9e-149">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e1e9e-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="e1e9e-150">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="e1e9e-150">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="e1e9e-151">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e1e9e-151">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
    {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);


                // Run hello thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference tooAzure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
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
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

### <a name="video-thumbnail-output"></a><span data-ttu-id="e1e9e-152">Resultado de miniaturas de vídeo</span><span class="sxs-lookup"><span data-stu-id="e1e9e-152">Video thumbnail output</span></span>
[<span data-ttu-id="e1e9e-153">Resultado de miniaturas de vídeo</span><span class="sxs-lookup"><span data-stu-id="e1e9e-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="e1e9e-154">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="e1e9e-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e1e9e-155">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="e1e9e-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="e1e9e-156">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="e1e9e-156">Related links</span></span>
[<span data-ttu-id="e1e9e-157">Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)</span><span class="sxs-lookup"><span data-stu-id="e1e9e-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="e1e9e-158">Demostraciones de Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="e1e9e-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

