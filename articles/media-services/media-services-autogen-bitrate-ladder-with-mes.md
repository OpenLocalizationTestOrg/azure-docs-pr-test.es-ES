---
title: "aaaUse Azure Media Encoder estándar tooauto-generar una escalera de velocidad de bits | Documentos de Microsoft"
description: "Este tema se muestra cómo toouse medios codificador estándar (MES) tooauto-generar una escalera de velocidad de bits en función de la resolución de entrada de Hola y velocidad de bits. velocidad de bits y la resolución de entrada de hello nunca se puede superar. Por ejemplo, si la entrada de hello es 720p en 3 Mbps, salida will permanecen en el mejor 720p y se iniciará a velocidades inferiores a 3 Mbps."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a><span data-ttu-id="ee343-105">Usar Azure Media Encoder estándar tooauto-generar una escalera de velocidad de bits</span><span class="sxs-lookup"><span data-stu-id="ee343-105">Use Azure Media Encoder Standard tooauto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="ee343-106">Información general</span><span class="sxs-lookup"><span data-stu-id="ee343-106">Overview</span></span>

<span data-ttu-id="ee343-107">Este tema se muestra cómo toouse medios codificador estándar (MES) tooauto-generar una escalera de velocidad de bits (pares de resolución de velocidad de bits) en función de la resolución de entrada de Hola y velocidad de bits.</span><span class="sxs-lookup"><span data-stu-id="ee343-107">This topic shows how toouse Media Encoder Standard (MES) tooauto-generate a bitrate ladder (bitrate-resolution pairs) based on hello input resolution and bitrate.</span></span> <span data-ttu-id="ee343-108">Hello valor preestablecido autogenerada nunca superará velocidad de bits y la resolución de Hola de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee343-108">hello auto-generated preset will never exceed hello input resolution and bitrate.</span></span> <span data-ttu-id="ee343-109">Por ejemplo, si la entrada de hello es 720p en 3 Mbps, salida will permanecen en el mejor 720p y se iniciará a velocidades inferiores a 3 Mbps.</span><span class="sxs-lookup"><span data-stu-id="ee343-109">For example, if hello input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="ee343-110">Codificación solo para streaming</span><span class="sxs-lookup"><span data-stu-id="ee343-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="ee343-111">Si su intención es tooencode el origen de vídeo solo para la transmisión por secuencias, a continuación, se deben usar hello "Transmisión por secuencias adaptativa" preestablecido al crear una tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="ee343-111">If your intent is tooencode your source video only for streaming, then you shoud use hello "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="ee343-112">Cuando se usa hello **transmisión por secuencias adaptativa** predefinidos, codificador MES de hello inteligentemente limitar una escalera de velocidad de bits.</span><span class="sxs-lookup"><span data-stu-id="ee343-112">When using hello **Adaptive Streaming** preset, hello MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="ee343-113">Sin embargo, no será hello toocontrol capaz de codificación de los costes, ya que el servicio Hola determina cuántos toouse de capas y con qué resolución.</span><span class="sxs-lookup"><span data-stu-id="ee343-113">However, you will not be able toocontrol hello encoding costs, since hello service determines how many layers toouse and at what resolution.</span></span> <span data-ttu-id="ee343-114">Puede ver ejemplos de las capas de salida generados por MES como resultado de la codificación con hello **transmisión por secuencias adaptativa** preestablecido final Hola de este tema.</span><span class="sxs-lookup"><span data-stu-id="ee343-114">You can see examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset at hello end of this topic.</span></span> <span data-ttu-id="ee343-115">Hola salida Asset contendrá archivos MP4 donde el audio y vídeo no se intercalan.</span><span class="sxs-lookup"><span data-stu-id="ee343-115">hello output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="ee343-116">Codificación para streaming y descarga progresiva</span><span class="sxs-lookup"><span data-stu-id="ee343-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="ee343-117">Si su intención es tooencode el vídeo de origen para la transmisión por secuencias, así como archivos MP4 de tooproduce para la descarga progresiva, a continuación, se deben usar hello "Contenido adaptable varias velocidades de bits MP4" preestablecido al crear una tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="ee343-117">If your intent is tooencode your source video for streaming as well as tooproduce MP4 files for progressive download, then you shoud use hello "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="ee343-118">Cuando se usa hello **contenido adaptativa MP4 de velocidad de bits múltiples** predefinidos, codificador MES de hello aplicará Hola misma lógica de codificación que anteriormente, pero ahora activo de salida de hello contendrá MP4 archivos donde audio y vídeo son intercalada.</span><span class="sxs-lookup"><span data-stu-id="ee343-118">When using hello **Content Adaptive Multiple Bitrate MP4** preset, hello MES encoder will apply hello same encoding logic as above, but now hello output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="ee343-119">Puede usar uno de estos archivos MP4 (por ejemplo, hello versión más alta velocidad de bits) como un archivo de descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="ee343-119">You can use one of these MP4 files (for example, hello highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="ee343-120"><a id="encoding_with_dotnet"></a>Codificación con el SDK de .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="ee343-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="ee343-121">Hola el ejemplo de código siguiente utiliza Hola de Media Services .NET SDK tooperform siguiente las tareas:</span><span class="sxs-lookup"><span data-stu-id="ee343-121">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="ee343-122">Crear un trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="ee343-122">Create an encoding job.</span></span>
- <span data-ttu-id="ee343-123">Obtiene un Codificador multimedia codificador estándar toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="ee343-123">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="ee343-124">Agregar un trabajo de toohello tarea codificación y especificar hello toouse **transmisión por secuencias adaptativa** preestablecido.</span><span class="sxs-lookup"><span data-stu-id="ee343-124">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="ee343-125">Crear un recurso de salida que contendrá asset Hola codificado.</span><span class="sxs-lookup"><span data-stu-id="ee343-125">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="ee343-126">Agregue un progreso del controlador de eventos toocheck Hola trabajo.</span><span class="sxs-lookup"><span data-stu-id="ee343-126">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="ee343-127">Enviar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee343-127">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ee343-128">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee343-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="ee343-129">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ee343-129">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="ee343-130">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ee343-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
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

## <span data-ttu-id="ee343-131"><a id="output"></a>Salida</span><span class="sxs-lookup"><span data-stu-id="ee343-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="ee343-132">En esta sección se muestra tres ejemplos de niveles de salida generados por MES como resultado de la codificación con hello **transmisión por secuencias adaptativa** preestablecido.</span><span class="sxs-lookup"><span data-stu-id="ee343-132">This section shows three examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="ee343-133">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="ee343-133">Example 1</span></span>
<span data-ttu-id="ee343-134">Un origen con un alto de "1080" y una tasa de fotogramas de "29.970" genera 6 niveles de vídeo:</span><span class="sxs-lookup"><span data-stu-id="ee343-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="ee343-135">Nivel</span><span class="sxs-lookup"><span data-stu-id="ee343-135">Layer</span></span>|<span data-ttu-id="ee343-136">Alto</span><span class="sxs-lookup"><span data-stu-id="ee343-136">Height</span></span>|<span data-ttu-id="ee343-137">Ancho</span><span class="sxs-lookup"><span data-stu-id="ee343-137">Width</span></span>|<span data-ttu-id="ee343-138">Velocidad de bits (kbps)</span><span class="sxs-lookup"><span data-stu-id="ee343-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="ee343-139">1</span><span class="sxs-lookup"><span data-stu-id="ee343-139">1</span></span>|<span data-ttu-id="ee343-140">1080</span><span class="sxs-lookup"><span data-stu-id="ee343-140">1080</span></span>|<span data-ttu-id="ee343-141">1920</span><span class="sxs-lookup"><span data-stu-id="ee343-141">1920</span></span>|<span data-ttu-id="ee343-142">6780</span><span class="sxs-lookup"><span data-stu-id="ee343-142">6780</span></span>|
|<span data-ttu-id="ee343-143">2</span><span class="sxs-lookup"><span data-stu-id="ee343-143">2</span></span>|<span data-ttu-id="ee343-144">720</span><span class="sxs-lookup"><span data-stu-id="ee343-144">720</span></span>|<span data-ttu-id="ee343-145">1280</span><span class="sxs-lookup"><span data-stu-id="ee343-145">1280</span></span>|<span data-ttu-id="ee343-146">3520</span><span class="sxs-lookup"><span data-stu-id="ee343-146">3520</span></span>|
|<span data-ttu-id="ee343-147">3</span><span class="sxs-lookup"><span data-stu-id="ee343-147">3</span></span>|<span data-ttu-id="ee343-148">540</span><span class="sxs-lookup"><span data-stu-id="ee343-148">540</span></span>|<span data-ttu-id="ee343-149">960</span><span class="sxs-lookup"><span data-stu-id="ee343-149">960</span></span>|<span data-ttu-id="ee343-150">2210</span><span class="sxs-lookup"><span data-stu-id="ee343-150">2210</span></span>|
|<span data-ttu-id="ee343-151">4</span><span class="sxs-lookup"><span data-stu-id="ee343-151">4</span></span>|<span data-ttu-id="ee343-152">360</span><span class="sxs-lookup"><span data-stu-id="ee343-152">360</span></span>|<span data-ttu-id="ee343-153">640</span><span class="sxs-lookup"><span data-stu-id="ee343-153">640</span></span>|<span data-ttu-id="ee343-154">1150</span><span class="sxs-lookup"><span data-stu-id="ee343-154">1150</span></span>|
|<span data-ttu-id="ee343-155">5</span><span class="sxs-lookup"><span data-stu-id="ee343-155">5</span></span>|<span data-ttu-id="ee343-156">270</span><span class="sxs-lookup"><span data-stu-id="ee343-156">270</span></span>|<span data-ttu-id="ee343-157">480</span><span class="sxs-lookup"><span data-stu-id="ee343-157">480</span></span>|<span data-ttu-id="ee343-158">720</span><span class="sxs-lookup"><span data-stu-id="ee343-158">720</span></span>|
|<span data-ttu-id="ee343-159">6</span><span class="sxs-lookup"><span data-stu-id="ee343-159">6</span></span>|<span data-ttu-id="ee343-160">180</span><span class="sxs-lookup"><span data-stu-id="ee343-160">180</span></span>|<span data-ttu-id="ee343-161">320</span><span class="sxs-lookup"><span data-stu-id="ee343-161">320</span></span>|<span data-ttu-id="ee343-162">380</span><span class="sxs-lookup"><span data-stu-id="ee343-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="ee343-163">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="ee343-163">Example 2</span></span>
<span data-ttu-id="ee343-164">Un origen con un alto de "720" y una tasa de fotogramas de "23.970" genera 5 niveles de vídeo:</span><span class="sxs-lookup"><span data-stu-id="ee343-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="ee343-165">Nivel</span><span class="sxs-lookup"><span data-stu-id="ee343-165">Layer</span></span>|<span data-ttu-id="ee343-166">Alto</span><span class="sxs-lookup"><span data-stu-id="ee343-166">Height</span></span>|<span data-ttu-id="ee343-167">Ancho</span><span class="sxs-lookup"><span data-stu-id="ee343-167">Width</span></span>|<span data-ttu-id="ee343-168">Velocidad de bits (kbps)</span><span class="sxs-lookup"><span data-stu-id="ee343-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="ee343-169">1</span><span class="sxs-lookup"><span data-stu-id="ee343-169">1</span></span>|<span data-ttu-id="ee343-170">720</span><span class="sxs-lookup"><span data-stu-id="ee343-170">720</span></span>|<span data-ttu-id="ee343-171">1280</span><span class="sxs-lookup"><span data-stu-id="ee343-171">1280</span></span>|<span data-ttu-id="ee343-172">2940</span><span class="sxs-lookup"><span data-stu-id="ee343-172">2940</span></span>|
|<span data-ttu-id="ee343-173">2</span><span class="sxs-lookup"><span data-stu-id="ee343-173">2</span></span>|<span data-ttu-id="ee343-174">540</span><span class="sxs-lookup"><span data-stu-id="ee343-174">540</span></span>|<span data-ttu-id="ee343-175">960</span><span class="sxs-lookup"><span data-stu-id="ee343-175">960</span></span>|<span data-ttu-id="ee343-176">1850</span><span class="sxs-lookup"><span data-stu-id="ee343-176">1850</span></span>|
|<span data-ttu-id="ee343-177">3</span><span class="sxs-lookup"><span data-stu-id="ee343-177">3</span></span>|<span data-ttu-id="ee343-178">360</span><span class="sxs-lookup"><span data-stu-id="ee343-178">360</span></span>|<span data-ttu-id="ee343-179">640</span><span class="sxs-lookup"><span data-stu-id="ee343-179">640</span></span>|<span data-ttu-id="ee343-180">960</span><span class="sxs-lookup"><span data-stu-id="ee343-180">960</span></span>|
|<span data-ttu-id="ee343-181">4</span><span class="sxs-lookup"><span data-stu-id="ee343-181">4</span></span>|<span data-ttu-id="ee343-182">270</span><span class="sxs-lookup"><span data-stu-id="ee343-182">270</span></span>|<span data-ttu-id="ee343-183">480</span><span class="sxs-lookup"><span data-stu-id="ee343-183">480</span></span>|<span data-ttu-id="ee343-184">600</span><span class="sxs-lookup"><span data-stu-id="ee343-184">600</span></span>|
|<span data-ttu-id="ee343-185">5</span><span class="sxs-lookup"><span data-stu-id="ee343-185">5</span></span>|<span data-ttu-id="ee343-186">180</span><span class="sxs-lookup"><span data-stu-id="ee343-186">180</span></span>|<span data-ttu-id="ee343-187">320</span><span class="sxs-lookup"><span data-stu-id="ee343-187">320</span></span>|<span data-ttu-id="ee343-188">320</span><span class="sxs-lookup"><span data-stu-id="ee343-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="ee343-189">Ejemplo 3</span><span class="sxs-lookup"><span data-stu-id="ee343-189">Example 3</span></span>
<span data-ttu-id="ee343-190">Un origen con un alto de "360" y una tasa de fotogramas de "29.970" genera 3 niveles de vídeo:</span><span class="sxs-lookup"><span data-stu-id="ee343-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="ee343-191">Nivel</span><span class="sxs-lookup"><span data-stu-id="ee343-191">Layer</span></span>|<span data-ttu-id="ee343-192">Alto</span><span class="sxs-lookup"><span data-stu-id="ee343-192">Height</span></span>|<span data-ttu-id="ee343-193">Ancho</span><span class="sxs-lookup"><span data-stu-id="ee343-193">Width</span></span>|<span data-ttu-id="ee343-194">Velocidad de bits (kbps)</span><span class="sxs-lookup"><span data-stu-id="ee343-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="ee343-195">1</span><span class="sxs-lookup"><span data-stu-id="ee343-195">1</span></span>|<span data-ttu-id="ee343-196">360</span><span class="sxs-lookup"><span data-stu-id="ee343-196">360</span></span>|<span data-ttu-id="ee343-197">640</span><span class="sxs-lookup"><span data-stu-id="ee343-197">640</span></span>|<span data-ttu-id="ee343-198">700</span><span class="sxs-lookup"><span data-stu-id="ee343-198">700</span></span>|
|<span data-ttu-id="ee343-199">2</span><span class="sxs-lookup"><span data-stu-id="ee343-199">2</span></span>|<span data-ttu-id="ee343-200">270</span><span class="sxs-lookup"><span data-stu-id="ee343-200">270</span></span>|<span data-ttu-id="ee343-201">480</span><span class="sxs-lookup"><span data-stu-id="ee343-201">480</span></span>|<span data-ttu-id="ee343-202">440</span><span class="sxs-lookup"><span data-stu-id="ee343-202">440</span></span>|
|<span data-ttu-id="ee343-203">3</span><span class="sxs-lookup"><span data-stu-id="ee343-203">3</span></span>|<span data-ttu-id="ee343-204">180</span><span class="sxs-lookup"><span data-stu-id="ee343-204">180</span></span>|<span data-ttu-id="ee343-205">320</span><span class="sxs-lookup"><span data-stu-id="ee343-205">320</span></span>|<span data-ttu-id="ee343-206">230</span><span class="sxs-lookup"><span data-stu-id="ee343-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="ee343-207">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="ee343-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ee343-208">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="ee343-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="ee343-209">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ee343-209">See Also</span></span>
[<span data-ttu-id="ee343-210">Información general sobre la codificación de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="ee343-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

