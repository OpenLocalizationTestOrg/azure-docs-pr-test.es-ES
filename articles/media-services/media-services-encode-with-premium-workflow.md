---
title: "aaaAdvanced codificación con el flujo de trabajo de Media Encoder Premium | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooencode con flujo de trabajo de Premium de codificación de medios. Ejemplos de código están escritos en C# y usar hello SDK de servicios multimedia para. NET."
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
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="3dbc9-104">Codificación avanzada con el flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="3dbc9-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="3dbc9-105">El procesador multimedia del flujo de trabajo premium de Media Encoder del que se habla en este tema no está disponible en China.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="3dbc9-106">Si tiene preguntas sobre el codificador premium, envíe un correo a mepd en Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="3dbc9-107">Información general</span><span class="sxs-lookup"><span data-stu-id="3dbc9-107">Overview</span></span>
<span data-ttu-id="3dbc9-108">Servicios de multimedia de Microsoft Azure está presentando hello **flujo de trabajo de Premium de codificación de medios** procesador multimedia.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-108">Microsoft Azure Media Services is introducing hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="3dbc9-109">Este procesador ofrece funciones de codificación avanzadas para sus flujos de trabajo de Premium a petición.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="3dbc9-110">Hello en los temas siguientes describen detalles relacionados con demasiado**flujo de trabajo de Premium de codificación de medios**:</span><span class="sxs-lookup"><span data-stu-id="3dbc9-110">hello following topics outline details related too**Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="3dbc9-111">[Formatos admitidos al Hola flujo de trabajo de Premium de codificación de medios](media-services-premium-workflow-encoder-formats.md) : describe los formatos de archivo de Hola y códecs admitidos por **flujo de trabajo de Premium de codificación de medios**.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-111">[Formats Supported by hello Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses hello file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="3dbc9-112">[Información general y la comparación de Azure en codificadores de medios de petición](media-services-encode-asset.md) compara Hola capacidades de codificación de **flujo de trabajo de Premium de codificación de medios** y **Media Encoder estándar**.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares hello encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="3dbc9-113">Este tema se muestra cómo tooencode con **flujo de trabajo de Premium de codificación de medios** con. NET.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-113">This topic demonstrates how tooencode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="3dbc9-114">Codificación de tareas para hello **flujo de trabajo de Premium de codificación de medios** requieren un archivo de configuración independiente, denominado archivo de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-114">Encoding tasks for hello **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="3dbc9-115">Estos archivos tienen una extensión de longitud y se crean mediante hello [Workflow Designer](media-services-workflow-designer.md) herramienta.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-115">These files have a .workflow extension and are created using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="3dbc9-116">También puede obtener predeterminado de hello archivos de flujo de trabajo [aquí](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="3dbc9-116">You can also get hello default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="3dbc9-117">carpeta de Hello también contiene la descripción de Hola de estos archivos.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-117">hello folder also contains hello description of these files.</span></span>

<span data-ttu-id="3dbc9-118">archivos de flujo de trabajo de Hello necesitan la cuenta de servicios multimedia de tooyour toobe cargado como un recurso y se debe pasar este recurso toohello tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-118">hello workflow files need toobe uploaded tooyour Media Services account as an Asset, and this Asset should be passed in toohello encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3dbc9-119">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3dbc9-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="3dbc9-120">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3dbc9-120">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="3dbc9-121">Ejemplo de codificación</span><span class="sxs-lookup"><span data-stu-id="3dbc9-121">Encoding example</span></span>

<span data-ttu-id="3dbc9-122">Hello ejemplo siguiente se muestra cómo tooencode con **flujo de trabajo de Premium de codificación de medios**.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-122">hello following example demonstrates how tooencode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="3dbc9-123">Hola pasos se realiza:</span><span class="sxs-lookup"><span data-stu-id="3dbc9-123">hello following steps are performed:</span></span>

1. <span data-ttu-id="3dbc9-124">Crear un recurso y cargar un archivo de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="3dbc9-125">Crear un recurso y cargar un archivo multimedia de origen.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="3dbc9-126">Obtener procesador multimedia de Hola "Flujo de trabajo del Premium de codificación de medios".</span><span class="sxs-lookup"><span data-stu-id="3dbc9-126">Get hello "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="3dbc9-127">Crear un trabajo y una tarea.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-127">Create a job and a task.</span></span>

    <span data-ttu-id="3dbc9-128">En la mayoría de los casos, la cadena de configuración de hello para la tarea hello está vacío (como en el siguiente ejemplo de Hola).</span><span class="sxs-lookup"><span data-stu-id="3dbc9-128">In most cases, hello configuration string for hello task is empty (like in hello following example).</span></span> <span data-ttu-id="3dbc9-129">Hay algunos escenarios avanzados (que requieran tootooset en tiempo de ejecución propiedades dinámicamente) en cuyo caso deberá proporcionar una tarea de codificación de toohello de cadena XML.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-129">There are some advanced scenarios (that require you tootooset runtime properties dynamically) in which case you would provide an XML string toohello encoding task.</span></span> <span data-ttu-id="3dbc9-130">Ejemplos de estos escenarios son la creación de una superposición, la unión paralela o secuencial multimedia y el subtitulado.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="3dbc9-131">Agregue dos tareas de toohello de activos de entrada.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-131">Add two input assets toohello task.</span></span>

    1. <span data-ttu-id="3dbc9-132">1 – activos de flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-132">1st – hello workflow asset.</span></span>
    2. <span data-ttu-id="3dbc9-133">2 º – recurso de vídeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-133">2nd – hello video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3dbc9-134">activos de flujo de trabajo de Hello deben agregarse toohello tarea antes de activo multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-134">hello workflow asset must be added toohello task before hello media asset.</span></span>
   <span data-ttu-id="3dbc9-135">cadena de configuración de Hola para esta tarea debe estar vacío.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-135">hello configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="3dbc9-136">Enviar el trabajo de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-136">Submit hello encoding job.</span></span>

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
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
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

<span data-ttu-id="3dbc9-137">Si tiene preguntas sobre el codificador premium, envíe un correo a mepd en Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="3dbc9-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3dbc9-138">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="3dbc9-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3dbc9-139">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="3dbc9-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
