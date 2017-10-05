---
title: "Codificación avanzada con el flujo de trabajo de Media Encoder premium | Microsoft Docs"
description: "Aprenda a codificar con el flujo de trabajo del Codificador multimedia Premium. Los ejemplos de código están escritos en C# y utilizan el SDK de Servicios multimedia para .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 2b03853bf07e05c07fd730d5e8a8563963887921
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="0101a-104">Codificación avanzada con el flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="0101a-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="0101a-105">El procesador multimedia del flujo de trabajo premium de Media Encoder del que se habla en este tema no está disponible en China.</span><span class="sxs-lookup"><span data-stu-id="0101a-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="0101a-106">Si tiene preguntas sobre el codificador premium, envíe un correo a mepd en Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="0101a-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="0101a-107">Información general</span><span class="sxs-lookup"><span data-stu-id="0101a-107">Overview</span></span>
<span data-ttu-id="0101a-108">Servicios multimedia de Microsoft Azure presenta el procesador multimedia de **Flujo de trabajo del Codificador multimedia Premium** .</span><span class="sxs-lookup"><span data-stu-id="0101a-108">Microsoft Azure Media Services is introducing the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="0101a-109">Este procesador ofrece funciones de codificación avanzadas para sus flujos de trabajo de Premium a petición.</span><span class="sxs-lookup"><span data-stu-id="0101a-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="0101a-110">Los siguientes temas describen los detalles relacionados con el **flujo de trabajo premium de Media Encoder**:</span><span class="sxs-lookup"><span data-stu-id="0101a-110">The following topics outline details related to **Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="0101a-111">[Formatos que admite el flujo de trabajo del Codificador multimedia Premium](media-services-premium-workflow-encoder-formats.md) : trata los formatos de archivo y los códecs que admite el **flujo de trabajo del Codificador multimedia Premium**.</span><span class="sxs-lookup"><span data-stu-id="0101a-111">[Formats Supported by the Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses the file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="0101a-112">En [Información general y comparación de codificadores multimedia a petición de Azure](media-services-encode-asset.md) se comparan las funcionalidades de codificación de **Flujo de trabajo del Codificador multimedia** y **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="0101a-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares the encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="0101a-113">En este tema se muestra cómo codificar con el **flujo de trabajo premium de Media Encoder** con .NET.</span><span class="sxs-lookup"><span data-stu-id="0101a-113">This topic demonstrates how to encode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="0101a-114">Las tareas de codificación del **flujo de trabajo del Codificador multimedia Premium** requieren un archivo de configuración independiente, denominado archivo de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0101a-114">Encoding tasks for the **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="0101a-115">Estos archivos tienen una extensión .workflow y se crean con la herramienta [Diseñador de flujo de trabajo](media-services-workflow-designer.md) .</span><span class="sxs-lookup"><span data-stu-id="0101a-115">These files have a .workflow extension and are created using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="0101a-116">Los archivos de flujo de trabajo predeterminados también se pueden obtener [aquí](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="0101a-116">You can also get the default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="0101a-117">La carpeta también contiene la descripción de estos archivos.</span><span class="sxs-lookup"><span data-stu-id="0101a-117">The folder also contains the description of these files.</span></span>

<span data-ttu-id="0101a-118">Los archivos de flujo de trabajo deben cargarse en su cuenta de Servicios multimedia como un recurso, y el recurso se debe transferir a la tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="0101a-118">The workflow files need to be uploaded to your Media Services account as an Asset, and this Asset should be passed in to the encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0101a-119">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0101a-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="0101a-120">Configure el entorno de desarrollo y rellene el archivo app.config con la información de la conexión, como se describe en [Desarrollo de Media Services con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0101a-120">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="0101a-121">Ejemplo de codificación</span><span class="sxs-lookup"><span data-stu-id="0101a-121">Encoding example</span></span>

<span data-ttu-id="0101a-122">En el ejemplo siguiente se muestra cómo codificar con el **flujo de trabajo del Codificador multimedia Premium**.</span><span class="sxs-lookup"><span data-stu-id="0101a-122">The following example demonstrates how to encode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="0101a-123">Hay que seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0101a-123">The following steps are performed:</span></span>

1. <span data-ttu-id="0101a-124">Crear un recurso y cargar un archivo de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0101a-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="0101a-125">Crear un recurso y cargar un archivo multimedia de origen.</span><span class="sxs-lookup"><span data-stu-id="0101a-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="0101a-126">Obtenga el procesador multimedia "Media Encoder Premium Workflow".</span><span class="sxs-lookup"><span data-stu-id="0101a-126">Get the "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="0101a-127">Crear un trabajo y una tarea.</span><span class="sxs-lookup"><span data-stu-id="0101a-127">Create a job and a task.</span></span>

    <span data-ttu-id="0101a-128">En la mayoría de los casos, la cadena de configuración de la tarea está vacía (como en el ejemplo siguiente).</span><span class="sxs-lookup"><span data-stu-id="0101a-128">In most cases, the configuration string for the task is empty (like in the following example).</span></span> <span data-ttu-id="0101a-129">Hay algunos escenarios avanzados (que requieren que establezca propiedades de tiempo de ejecución dinámicamente) en los que debería proporcionar una cadena XML para la tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="0101a-129">There are some advanced scenarios (that require you to to set runtime properties dynamically) in which case you would provide an XML string to the encoding task.</span></span> <span data-ttu-id="0101a-130">Ejemplos de estos escenarios son la creación de una superposición, la unión paralela o secuencial multimedia y el subtitulado.</span><span class="sxs-lookup"><span data-stu-id="0101a-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="0101a-131">Agregar dos recursos de entrada a la tarea.</span><span class="sxs-lookup"><span data-stu-id="0101a-131">Add two input assets to the task.</span></span>

    1. <span data-ttu-id="0101a-132">1.º: el recurso de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0101a-132">1st – the workflow asset.</span></span>
    2. <span data-ttu-id="0101a-133">2.º: el recurso de vídeo.</span><span class="sxs-lookup"><span data-stu-id="0101a-133">2nd – the video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="0101a-134">El recurso de flujo de trabajo debe agregarse a la tarea antes que el recurso multimedia.</span><span class="sxs-lookup"><span data-stu-id="0101a-134">The workflow asset must be added to the task before the media asset.</span></span>
   <span data-ttu-id="0101a-135">La cadena de configuración para esta tarea debe estar vacía.</span><span class="sxs-lookup"><span data-stu-id="0101a-135">The configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="0101a-136">Envíe el trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="0101a-136">Submit the encoding job.</span></span>

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
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

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass to it the name of the
                    // processor to use for the specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify the input asset to be encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset to contain the results of the job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means the output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use the following event handler to check job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch the job.
                    job.Submit();

                    // Check job execution and wait for job to finish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error the event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due to job error.");
                    }

                    return job.OutputMediaAssets[0];
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

<span data-ttu-id="0101a-137">Si tiene preguntas sobre el codificador premium, envíe un correo a mepd en Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="0101a-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="0101a-138">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="0101a-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0101a-139">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="0101a-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
