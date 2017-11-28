---
title: "Uso de Azure Media Encoder Standard para generar automáticamente una escalera de velocidad de bits | Microsoft Docs"
description: "En este tema se muestra cómo usar Media Encoder Standard (MES) para generar automáticamente una escalera de velocidad de bits en función de la resolución de entrada y la velocidad de bits. La resolución de entrada y la velocidad de bits nunca se superarán. Por ejemplo, si la entrada es 720p a 3 Mbps, la salida permanecerá en 720p en el mejor de los casos y se iniciará a velocidades inferiores a 3 Mbps."
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
ms.openlocfilehash: b5616aa9f8b15ab576d914fbae89a56f64c27f4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
#  <a name="use-azure-media-encoder-standard-to-auto-generate-a-bitrate-ladder"></a><span data-ttu-id="7a886-105">Uso de Azure Media Encoder Standard para generar automáticamente una escalera de velocidad de bits</span><span class="sxs-lookup"><span data-stu-id="7a886-105">Use Azure Media Encoder Standard to auto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="7a886-106">Información general</span><span class="sxs-lookup"><span data-stu-id="7a886-106">Overview</span></span>

<span data-ttu-id="7a886-107">En este tema se muestra cómo usar Media Encoder Standard (MES) para generar automáticamente una escalera de velocidad de bits (pares de velocidad de bits-resolución) en función de la velocidad de bits y la resolución de entrada.</span><span class="sxs-lookup"><span data-stu-id="7a886-107">This topic shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span></span> <span data-ttu-id="7a886-108">El valor preestablecido generado automáticamente nunca superará la velocidad de bits y la resolución de entrada.</span><span class="sxs-lookup"><span data-stu-id="7a886-108">The auto-generated preset will never exceed the input resolution and bitrate.</span></span> <span data-ttu-id="7a886-109">Por ejemplo, si la entrada es 720p a 3 Mbps, la salida permanecerá en 720p en el mejor de los casos y se iniciará a velocidades inferiores a 3 Mbps.</span><span class="sxs-lookup"><span data-stu-id="7a886-109">For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="7a886-110">Codificación solo para streaming</span><span class="sxs-lookup"><span data-stu-id="7a886-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="7a886-111">Si su intención es codificar el vídeo de origen solo para streaming, deberá usar el valor preestablecido "Adaptive Streaming" al crear una tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="7a886-111">If your intent is to encode your source video only for streaming, then you shoud use the "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="7a886-112">Cuando se usa el valor preestablecido **Adaptive Streaming**, el codificador MES limitará inteligentemente una escalera de velocidad de bits.</span><span class="sxs-lookup"><span data-stu-id="7a886-112">When using the **Adaptive Streaming** preset, the MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="7a886-113">Sin embargo, no será capaz de controlar los costos de codificación, ya que el servicio determina cuántos niveles usar y con qué resolución.</span><span class="sxs-lookup"><span data-stu-id="7a886-113">However, you will not be able to control the encoding costs, since the service determines how many layers to use and at what resolution.</span></span> <span data-ttu-id="7a886-114">Puede ver ejemplos de los niveles de salida generados por MES como resultado de la codificación con el valor preestablecido **Adaptive Streaming** al final de este tema.</span><span class="sxs-lookup"><span data-stu-id="7a886-114">You can see examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset at the end of this topic.</span></span> <span data-ttu-id="7a886-115">El recurso de salida contendrá archivos MP4 en los que el audio y el vídeo no están intercalados.</span><span class="sxs-lookup"><span data-stu-id="7a886-115">The output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="7a886-116">Codificación para streaming y descarga progresiva</span><span class="sxs-lookup"><span data-stu-id="7a886-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="7a886-117">Si su intención es codificar el vídeo de origen para streaming, así como generar archivos MP4 para la descarga progresiva, deberá usar el valor preestablecido "Content Adaptive Multiple Bitrate MP4" al crear una tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="7a886-117">If your intent is to encode your source video for streaming as well as to produce MP4 files for progressive download, then you shoud use the "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="7a886-118">Cuando se usa el valor preestablecido **Content Adaptive Multiple Bitrate MP4**, el codificador MES aplicará la misma lógica de codificación que la mostrada anteriormente, pero el recurso de salida contendrá los archivos MP4 en los que el audio y el vídeo están intercalados.</span><span class="sxs-lookup"><span data-stu-id="7a886-118">When using the **Content Adaptive Multiple Bitrate MP4** preset, the MES encoder will apply the same encoding logic as above, but now the output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="7a886-119">Puede usar uno de estos archivos MP4 (por ejemplo, la versión de velocidad de bits más alta) como un archivo de descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="7a886-119">You can use one of these MP4 files (for example, the highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="7a886-120"><a id="encoding_with_dotnet"></a>Codificación con el SDK de .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="7a886-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="7a886-121">En el ejemplo de código siguiente se usa el último SDK para .NET de Servicios multimedia para realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="7a886-121">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="7a886-122">Crear un trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="7a886-122">Create an encoding job.</span></span>
- <span data-ttu-id="7a886-123">Obtener una referencia al codificador Codificador multimedia estándar.</span><span class="sxs-lookup"><span data-stu-id="7a886-123">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="7a886-124">Agregue una tarea de codificación al trabajo y especifique que se utilice el valor preestablecido **Adaptive Streaming**.</span><span class="sxs-lookup"><span data-stu-id="7a886-124">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="7a886-125">Crear un recurso de salida que contendrá el recurso codificado.</span><span class="sxs-lookup"><span data-stu-id="7a886-125">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="7a886-126">Agregar un controlador de eventos para comprobar el progreso del trabajo.</span><span class="sxs-lookup"><span data-stu-id="7a886-126">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="7a886-127">Envíe el trabajo.</span><span class="sxs-lookup"><span data-stu-id="7a886-127">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="7a886-128">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a886-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="7a886-129">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="7a886-129">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="7a886-130">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="7a886-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
    {
        class Program
        {
        // Read values from the App.config file.
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

            // Encode and generate the output using the "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

## <span data-ttu-id="7a886-131"><a id="output"></a>Salida</span><span class="sxs-lookup"><span data-stu-id="7a886-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="7a886-132">Esta sección muestra tres niveles de salida generados por MES como resultado de la codificación con el valor preestablecido **Adaptive Streaming**.</span><span class="sxs-lookup"><span data-stu-id="7a886-132">This section shows three examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="7a886-133">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="7a886-133">Example 1</span></span>
<span data-ttu-id="7a886-134">Un origen con un alto de "1080" y una tasa de fotogramas de "29.970" genera 6 niveles de vídeo:</span><span class="sxs-lookup"><span data-stu-id="7a886-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="7a886-135">Nivel</span><span class="sxs-lookup"><span data-stu-id="7a886-135">Layer</span></span>|<span data-ttu-id="7a886-136">Alto</span><span class="sxs-lookup"><span data-stu-id="7a886-136">Height</span></span>|<span data-ttu-id="7a886-137">Ancho</span><span class="sxs-lookup"><span data-stu-id="7a886-137">Width</span></span>|<span data-ttu-id="7a886-138">Velocidad de bits (kbps)</span><span class="sxs-lookup"><span data-stu-id="7a886-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="7a886-139">1</span><span class="sxs-lookup"><span data-stu-id="7a886-139">1</span></span>|<span data-ttu-id="7a886-140">1080</span><span class="sxs-lookup"><span data-stu-id="7a886-140">1080</span></span>|<span data-ttu-id="7a886-141">1920</span><span class="sxs-lookup"><span data-stu-id="7a886-141">1920</span></span>|<span data-ttu-id="7a886-142">6780</span><span class="sxs-lookup"><span data-stu-id="7a886-142">6780</span></span>|
|<span data-ttu-id="7a886-143">2</span><span class="sxs-lookup"><span data-stu-id="7a886-143">2</span></span>|<span data-ttu-id="7a886-144">720</span><span class="sxs-lookup"><span data-stu-id="7a886-144">720</span></span>|<span data-ttu-id="7a886-145">1280</span><span class="sxs-lookup"><span data-stu-id="7a886-145">1280</span></span>|<span data-ttu-id="7a886-146">3520</span><span class="sxs-lookup"><span data-stu-id="7a886-146">3520</span></span>|
|<span data-ttu-id="7a886-147">3</span><span class="sxs-lookup"><span data-stu-id="7a886-147">3</span></span>|<span data-ttu-id="7a886-148">540</span><span class="sxs-lookup"><span data-stu-id="7a886-148">540</span></span>|<span data-ttu-id="7a886-149">960</span><span class="sxs-lookup"><span data-stu-id="7a886-149">960</span></span>|<span data-ttu-id="7a886-150">2210</span><span class="sxs-lookup"><span data-stu-id="7a886-150">2210</span></span>|
|<span data-ttu-id="7a886-151">4</span><span class="sxs-lookup"><span data-stu-id="7a886-151">4</span></span>|<span data-ttu-id="7a886-152">360</span><span class="sxs-lookup"><span data-stu-id="7a886-152">360</span></span>|<span data-ttu-id="7a886-153">640</span><span class="sxs-lookup"><span data-stu-id="7a886-153">640</span></span>|<span data-ttu-id="7a886-154">1150</span><span class="sxs-lookup"><span data-stu-id="7a886-154">1150</span></span>|
|<span data-ttu-id="7a886-155">5</span><span class="sxs-lookup"><span data-stu-id="7a886-155">5</span></span>|<span data-ttu-id="7a886-156">270</span><span class="sxs-lookup"><span data-stu-id="7a886-156">270</span></span>|<span data-ttu-id="7a886-157">480</span><span class="sxs-lookup"><span data-stu-id="7a886-157">480</span></span>|<span data-ttu-id="7a886-158">720</span><span class="sxs-lookup"><span data-stu-id="7a886-158">720</span></span>|
|<span data-ttu-id="7a886-159">6</span><span class="sxs-lookup"><span data-stu-id="7a886-159">6</span></span>|<span data-ttu-id="7a886-160">180</span><span class="sxs-lookup"><span data-stu-id="7a886-160">180</span></span>|<span data-ttu-id="7a886-161">320</span><span class="sxs-lookup"><span data-stu-id="7a886-161">320</span></span>|<span data-ttu-id="7a886-162">380</span><span class="sxs-lookup"><span data-stu-id="7a886-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="7a886-163">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="7a886-163">Example 2</span></span>
<span data-ttu-id="7a886-164">Un origen con un alto de "720" y una tasa de fotogramas de "23.970" genera 5 niveles de vídeo:</span><span class="sxs-lookup"><span data-stu-id="7a886-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="7a886-165">Nivel</span><span class="sxs-lookup"><span data-stu-id="7a886-165">Layer</span></span>|<span data-ttu-id="7a886-166">Alto</span><span class="sxs-lookup"><span data-stu-id="7a886-166">Height</span></span>|<span data-ttu-id="7a886-167">Ancho</span><span class="sxs-lookup"><span data-stu-id="7a886-167">Width</span></span>|<span data-ttu-id="7a886-168">Velocidad de bits (kbps)</span><span class="sxs-lookup"><span data-stu-id="7a886-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="7a886-169">1</span><span class="sxs-lookup"><span data-stu-id="7a886-169">1</span></span>|<span data-ttu-id="7a886-170">720</span><span class="sxs-lookup"><span data-stu-id="7a886-170">720</span></span>|<span data-ttu-id="7a886-171">1280</span><span class="sxs-lookup"><span data-stu-id="7a886-171">1280</span></span>|<span data-ttu-id="7a886-172">2940</span><span class="sxs-lookup"><span data-stu-id="7a886-172">2940</span></span>|
|<span data-ttu-id="7a886-173">2</span><span class="sxs-lookup"><span data-stu-id="7a886-173">2</span></span>|<span data-ttu-id="7a886-174">540</span><span class="sxs-lookup"><span data-stu-id="7a886-174">540</span></span>|<span data-ttu-id="7a886-175">960</span><span class="sxs-lookup"><span data-stu-id="7a886-175">960</span></span>|<span data-ttu-id="7a886-176">1850</span><span class="sxs-lookup"><span data-stu-id="7a886-176">1850</span></span>|
|<span data-ttu-id="7a886-177">3</span><span class="sxs-lookup"><span data-stu-id="7a886-177">3</span></span>|<span data-ttu-id="7a886-178">360</span><span class="sxs-lookup"><span data-stu-id="7a886-178">360</span></span>|<span data-ttu-id="7a886-179">640</span><span class="sxs-lookup"><span data-stu-id="7a886-179">640</span></span>|<span data-ttu-id="7a886-180">960</span><span class="sxs-lookup"><span data-stu-id="7a886-180">960</span></span>|
|<span data-ttu-id="7a886-181">4</span><span class="sxs-lookup"><span data-stu-id="7a886-181">4</span></span>|<span data-ttu-id="7a886-182">270</span><span class="sxs-lookup"><span data-stu-id="7a886-182">270</span></span>|<span data-ttu-id="7a886-183">480</span><span class="sxs-lookup"><span data-stu-id="7a886-183">480</span></span>|<span data-ttu-id="7a886-184">600</span><span class="sxs-lookup"><span data-stu-id="7a886-184">600</span></span>|
|<span data-ttu-id="7a886-185">5</span><span class="sxs-lookup"><span data-stu-id="7a886-185">5</span></span>|<span data-ttu-id="7a886-186">180</span><span class="sxs-lookup"><span data-stu-id="7a886-186">180</span></span>|<span data-ttu-id="7a886-187">320</span><span class="sxs-lookup"><span data-stu-id="7a886-187">320</span></span>|<span data-ttu-id="7a886-188">320</span><span class="sxs-lookup"><span data-stu-id="7a886-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="7a886-189">Ejemplo 3</span><span class="sxs-lookup"><span data-stu-id="7a886-189">Example 3</span></span>
<span data-ttu-id="7a886-190">Un origen con un alto de "360" y una tasa de fotogramas de "29.970" genera 3 niveles de vídeo:</span><span class="sxs-lookup"><span data-stu-id="7a886-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="7a886-191">Nivel</span><span class="sxs-lookup"><span data-stu-id="7a886-191">Layer</span></span>|<span data-ttu-id="7a886-192">Alto</span><span class="sxs-lookup"><span data-stu-id="7a886-192">Height</span></span>|<span data-ttu-id="7a886-193">Ancho</span><span class="sxs-lookup"><span data-stu-id="7a886-193">Width</span></span>|<span data-ttu-id="7a886-194">Velocidad de bits (kbps)</span><span class="sxs-lookup"><span data-stu-id="7a886-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="7a886-195">1</span><span class="sxs-lookup"><span data-stu-id="7a886-195">1</span></span>|<span data-ttu-id="7a886-196">360</span><span class="sxs-lookup"><span data-stu-id="7a886-196">360</span></span>|<span data-ttu-id="7a886-197">640</span><span class="sxs-lookup"><span data-stu-id="7a886-197">640</span></span>|<span data-ttu-id="7a886-198">700</span><span class="sxs-lookup"><span data-stu-id="7a886-198">700</span></span>|
|<span data-ttu-id="7a886-199">2</span><span class="sxs-lookup"><span data-stu-id="7a886-199">2</span></span>|<span data-ttu-id="7a886-200">270</span><span class="sxs-lookup"><span data-stu-id="7a886-200">270</span></span>|<span data-ttu-id="7a886-201">480</span><span class="sxs-lookup"><span data-stu-id="7a886-201">480</span></span>|<span data-ttu-id="7a886-202">440</span><span class="sxs-lookup"><span data-stu-id="7a886-202">440</span></span>|
|<span data-ttu-id="7a886-203">3</span><span class="sxs-lookup"><span data-stu-id="7a886-203">3</span></span>|<span data-ttu-id="7a886-204">180</span><span class="sxs-lookup"><span data-stu-id="7a886-204">180</span></span>|<span data-ttu-id="7a886-205">320</span><span class="sxs-lookup"><span data-stu-id="7a886-205">320</span></span>|<span data-ttu-id="7a886-206">230</span><span class="sxs-lookup"><span data-stu-id="7a886-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="7a886-207">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="7a886-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7a886-208">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="7a886-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="7a886-209">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="7a886-209">See Also</span></span>
[<span data-ttu-id="7a886-210">Información general sobre la codificación de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="7a886-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

