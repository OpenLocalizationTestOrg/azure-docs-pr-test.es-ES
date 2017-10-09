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
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a>Usar vistas en miniatura de Azure Media Video tooCreate un resumen de vídeo
## <a name="overview"></a>Información general
Hola **las miniaturas de vídeo de multimedia de Azure** procesador multimedia (MP) le permite toocreate un resumen de un vídeo que sea útil toocustomers que solo desea toopreview un resumen de un vídeo largo. Por ejemplo, los clientes podrían desear toosee un breve "resumen vídeo" cuando mantenga el mouse sobre una vista en miniatura. Ajustando los parámetros de Hola de **miniaturas de vídeo de multimedia de Azure** a través de un valor preestablecido de configuración, puede utilizar la detección de capturas eficaz Hola del módulo de administración y concatenación tecnología tooalgorithmically generar un subclip descriptivo.  

Hola **miniatura de vídeo de multimedia de Azure** MP está actualmente en vista previa.

Este tema proporciona detalles acerca de **miniatura de vídeo de multimedia de Azure** y muestra cómo toouse con el SDK de servicios multimedia para. NET.

## <a name="limitations"></a>Limitaciones

En algunos casos, si el vídeo no está formado por diferentes escenas, salida de hello solo será una captura única.

## <a name="video-summary-example"></a>Ejemplo de resumen de vídeo
Estos son algunos ejemplos de qué procesador multimedia Azure Media Video miniaturas Hola puede hacer:

### <a name="original-video"></a>Vídeo original
[Vídeo original](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a>Resultado de miniaturas de vídeo
[Resultado de miniaturas de vídeo](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a>Configuración de tareas (valor preestablecido)
Al crear una tarea de miniatura de vídeo con **Miniaturas de vídeo multimedia de Azure**, debe especificar un valor predeterminado de configuración. Hola en miniatura ejemplo anterior se creó con hello después de la configuración básica de JSON:

    {"version":"1.0"}

Actualmente, puede cambiar Hola parámetros siguientes:

| Parámetro | Description |
| --- | --- |
| outputAudio |Especifica si se permite o no vídeo resultante de hello contiene audio. <br/>Los valores permitidos son: True o False. El valor predeterminado es True. |
| fadeInFadeOut |Especifica si no realiza la transición atenuación utilizados entre las miniaturas de movimiento independientes de Hola.  <br/>Los valores permitidos son: True o False.  El valor predeterminado es True. |
| maxMotionThumbnailDurationInSecs |Entero que especifica cuánto tiempo Hola todo resultante vídeo será.  El valor predeterminado depende de la duración del vídeo original. |

Hello tabla siguiente describen duración predeterminada de hello, cuando **maxMotionThumbnailInSecs** no se utiliza.

|  |  |  |
| --- | --- | --- | --- | --- |
| Duración del vídeo |d < 3 min |3 min < d < 15 min |
| Duración de la miniatura |15 s (2-3 escenas) |30 s (3-5 escenas) |

Hello JSON siguiente establece los parámetros disponibles.

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a>Código de ejemplo de .NET

siguiente de Hello programa muestra cómo:

1. Crear un activo y cargar un archivo multimedia en activo de Hola.
2. Crea un trabajo con una tarea de miniatura vídeo basada en un archivo de configuración que contiene Hola siguiente valor preestablecido de json. 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. Descarga los archivos de salida de hello. 

#### <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio

Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Ejemplo

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

### <a name="video-thumbnail-output"></a>Resultado de miniaturas de vídeo
[Resultado de miniaturas de vídeo](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Vínculos relacionados
[Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)](media-services-analytics-overview.md)

[Demostraciones de Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

