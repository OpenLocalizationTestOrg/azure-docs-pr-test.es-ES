---
title: "valores preestablecidos de Media Encoder estándar aaaCustomizing | Documentos de Microsoft"
description: "Este tema muestra cómo tooperform avanzado de codificación mediante la personalización de Media Encoder estándar de valores preestablecidos de tarea. Hola tema muestra cómo toocreate del SDK de .NET de servicios multimedia de toouse una codificación de tareas y de trabajo. También muestra cómo toosupply personalizado presintonías de trabajo de codificación toohello."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec95392f-d34a-4c22-a6df-5274eaac445b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: fa8c3bef63b0c1ecc88a6b8874ecbff3a8028a57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-media-encoder-standard-presets"></a><span data-ttu-id="06d7b-105">Personalización de valores preestablecidos de Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="06d7b-105">Customizing Media Encoder Standard presets</span></span>

## <a name="overview"></a><span data-ttu-id="06d7b-106">Información general</span><span class="sxs-lookup"><span data-stu-id="06d7b-106">Overview</span></span>

<span data-ttu-id="06d7b-107">Este tema muestra cómo tooperform avanzado de codificación con medios codificador estándar (MES) usando un comparador preestablecido.</span><span class="sxs-lookup"><span data-stu-id="06d7b-107">This topic shows how tooperform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span></span> <span data-ttu-id="06d7b-108">tema de Hello usa .NET toocreate una tarea de codificación y un trabajo que se ejecuta esta tarea.</span><span class="sxs-lookup"><span data-stu-id="06d7b-108">hello topic uses .NET toocreate an encoding task and a job that executes this task.</span></span>  

<span data-ttu-id="06d7b-109">En este tema verá cómo toocustomize un valor preestablecido tomando Hola [H264 varias velocidades de bits 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) número Hola preestablecidas y reducir de capas.</span><span class="sxs-lookup"><span data-stu-id="06d7b-109">In this topic you will see how toocustomize a preset by taking hello [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing hello number of layers.</span></span> <span data-ttu-id="06d7b-110">Hola [presintonías personalizar estándar del Codificador multimedia](media-services-advanced-encoding-with-mes.md) tema muestra valores preestablecidos personalizados que pueden ser utilizado tooperform avanzada tareas de codificación.</span><span class="sxs-lookup"><span data-stu-id="06d7b-110">hello [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) topic demonstrates custom presets that can be used tooperform advanced encoding tasks.</span></span>

## <span data-ttu-id="06d7b-111"><a id="customizing_presets"></a> Personalización de un valor preestablecido de MES</span><span class="sxs-lookup"><span data-stu-id="06d7b-111"><a id="customizing_presets"></a> Customizing a MES preset</span></span>

### <a name="original-preset"></a><span data-ttu-id="06d7b-112">Valor preestablecido original</span><span class="sxs-lookup"><span data-stu-id="06d7b-112">Original preset</span></span>

<span data-ttu-id="06d7b-113">Hola guardar JSON definido en hello [H264 varias velocidades de bits 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tema en un archivo con extensión .json.</span><span class="sxs-lookup"><span data-stu-id="06d7b-113">Save hello JSON defined in hello [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) topic in some file with .json extension.</span></span> <span data-ttu-id="06d7b-114">Por ejemplo, **CustomPreset_JSON.json**.</span><span class="sxs-lookup"><span data-stu-id="06d7b-114">For example, **CustomPreset_JSON.json**.</span></span>

### <a name="customized-preset"></a><span data-ttu-id="06d7b-115">Valor preestablecido personalizado</span><span class="sxs-lookup"><span data-stu-id="06d7b-115">Customized preset</span></span>

<span data-ttu-id="06d7b-116">Abra hello **CustomPreset_JSON.json** de archivos y quitar en primer lugar tres capas de **H264Layers** por lo que el archivo tiene el siguiente aspecto.</span><span class="sxs-lookup"><span data-stu-id="06d7b-116">Open hello **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span></span>

    
    {  
      "Version": 1.0,  
      "Codecs": [  
        {  
          "KeyFrameInterval": "00:00:02",  
          "H264Layers": [  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 1000,  
              "MaxBitrate": 1000,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 650,  
              "MaxBitrate": 650,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 400,  
              "MaxBitrate": 400,  
              "BufferWindow": "00:00:05",  
              "Width": 320,  
              "Height": 180,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            }  
          ],  
          "Type": "H264Video"  
        },  
        {  
          "Profile": "AACLC",  
          "Channels": 2,  
          "SamplingRate": 48000,  
          "Bitrate": 128,  
          "Type": "AACAudio"  
        }  
      ],  
      "Outputs": [  
        {  
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
          "Format": {  
            "Type": "MP4Format"  
          }  
        }  
      ]  
    }  
    

## <span data-ttu-id="06d7b-117"><a id="encoding_with_dotnet"></a>Codificación con el SDK de .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="06d7b-117"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="06d7b-118">Hola el ejemplo de código siguiente utiliza Hola de Media Services .NET SDK tooperform siguiente las tareas:</span><span class="sxs-lookup"><span data-stu-id="06d7b-118">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="06d7b-119">Crear un trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="06d7b-119">Create an encoding job.</span></span>
- <span data-ttu-id="06d7b-120">Obtiene un Codificador multimedia codificador estándar toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="06d7b-120">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="06d7b-121">Cargar Hola que valor preestablecido de JSON personalizada que creó en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="06d7b-121">Load hello custom JSON preset that you created in hello previous section.</span></span> 
  
        // Load hello JSON from hello local file.
        string configuration = File.ReadAllText(fileName);  

- <span data-ttu-id="06d7b-122">Agregar un trabajo de toohello tarea codificación.</span><span class="sxs-lookup"><span data-stu-id="06d7b-122">Add an encoding task toohello job.</span></span> 
- <span data-ttu-id="06d7b-123">Especificar la entrada de hello toobe activo codificado.</span><span class="sxs-lookup"><span data-stu-id="06d7b-123">Specify hello input asset toobe encoded.</span></span>
- <span data-ttu-id="06d7b-124">Crear un recurso de salida que contendrá asset Hola codificado.</span><span class="sxs-lookup"><span data-stu-id="06d7b-124">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="06d7b-125">Agregue un progreso del controlador de eventos toocheck Hola trabajo.</span><span class="sxs-lookup"><span data-stu-id="06d7b-125">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="06d7b-126">Enviar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="06d7b-126">Submit hello job.</span></span>
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="06d7b-127">Creación y configuración de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="06d7b-127">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="06d7b-128">Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="06d7b-128">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="06d7b-129">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="06d7b-129">Example</span></span>   

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace CustomizeMESPresests
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using custom presets.
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

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("CustomPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="06d7b-130">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="06d7b-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="06d7b-131">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="06d7b-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="06d7b-132">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="06d7b-132">See Also</span></span>
[<span data-ttu-id="06d7b-133">Información general sobre la codificación de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="06d7b-133">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

