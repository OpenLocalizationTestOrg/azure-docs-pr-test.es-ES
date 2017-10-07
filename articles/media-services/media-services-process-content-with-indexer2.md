---
title: aaaIndexing archivos multimedia con vista previa de Azure Media Indexer 2 | Documentos de Microsoft
description: "Azure Media Indexer le permite toomake contenido de los archivos multimedia que permite realizar búsquedos y toogenerate una transcripción de texto completo para palabras clave y subtítulos. En este tema se muestra cómo obtener una vista previa en toouse Media Indexer 2."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: f83fa0db58b828ffa29933d68ce108b4906dcd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a>Indización de archivos multimedia con Azure Media Indexer 2 Preview
## <a name="overview"></a>Información general
Hola **vista previa de Azure Media Indexer 2** procesador multimedia (MP) le permite toomake los archivos multimedia y contenido para la búsqueda, así como generar pistas de subtítulos. Toohello en comparación con la versión anterior de [Azure Media Indexer](media-services-index-content.md), **vista previa de Azure Media Indexer 2** realiza una indización más rápida y ofrece mayor compatibilidad de idioma. Los idiomas admitidos son inglés, español, francés, alemán, italiano, chino (simplificado y mandarín), portugués, árabe y japonés.

Hola **vista previa de Azure Media Indexer 2** MP está actualmente en vista previa.

Este tema muestra cómo los trabajos de indización toocreate con **vista previa de Azure Media Indexer 2**.

> [!NOTE]
> Hola siguientes consideraciones se aplica:
> 
> Indexer 2 no es compatible con Azure China y Azure Government.
> 
> Al realizar la indización de contenido, asegúrese de toouse seguro de archivos multimedia que tienen muy claro (sin música de fondo, ruido, efectos o audio del micrófono). Algunos ejemplos de contenido adecuado son: reuniones, conferencias o presentaciones grabadas. Hello siguiente contenido podría no ser adecuado para la indización: películas, programas de TV, cualquier cosa con audio mixto y efectos de sonido, contenido mal graban con fondo ruido de fondo.
> 
> 

Este tema proporciona detalles acerca de **vista previa de Azure Media Indexer 2** y muestra cómo toouse con el SDK de servicios multimedia para .NET

## <a name="input-and-output-files"></a>Archivos de entrada y salida
### <a name="input-files"></a>Archivos de entrada
Archivos de audio o vídeo

### <a name="output-files"></a>Archivos de salida
Un trabajo de indización puede generar archivos de subtítulos de hello siguientes formatos:  

* **SAMI**
* **TTML**
* **WebVTT**

Archivos cerrados de subtítulos (CC) en estos formatos pueden ser usado toomake audio y archivos de vídeo toopeople accesible con discapacidades auditivas.

## <a name="task-configuration-preset"></a>Configuración de tareas (valor preestablecido)
Al crear una tarea de indexación con **Azure Media Indexer 2 Preview**, debe especificar un valor predeterminado de configuración.

Hello JSON siguiente establece los parámetros disponibles.

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a>Idiomas admitidos
Azure Media Indexer 2 Preview admite texto a voz para hello siguientes idiomas (cuando se especifica el nombre de idioma de hello en configuración de la tarea de hello, usar el código de 4 caracteres entre corchetes tal y como se muestra a continuación):

* Inglés [EnUs]
* Español [EsEs]
* Chino (mandarín, simplificado) [ZhCn]
* Francés [FrFr]
* Alemán [DeDe]
* Italiano [ItIt]
* Portugués [PtBr]
* Árabe (egipcio) [ArEg]
* Japonés [JaJp]
* Ruso [RuRu]
* Inglés británico [EnGb]
* Español de México [EsMx] 

## <a name="supported-file-types"></a>Tipos de archivo admitidos

Para obtener información acerca de los tipos de archivos compatibles, vea hello [códecs y formatos compatibles](media-services-media-encoder-standard-formats.md#input-containerfile-formats) sección.

## <a name="net-sample-code"></a>Código de ejemplo de .NET

siguiente de Hello programa muestra cómo:

1. Crear un activo y cargar un archivo multimedia en activo de Hola.
2. Crear un trabajo con una tarea de indización basándose en un archivo de configuración que contiene Hola siguiente valor preestablecido de json.
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
        }
3. Descargar archivos de salida de hello. 
   
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

    namespace IndexContent
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

                // Run indexing job.
                var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                            @"C:\supportFiles\Indexer\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
            }

            static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Indexing Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Indexing Job");

                // Get a reference tooAzure Media Indexer 2 Preview.
                string MediaProcessorName = "Azure Media Indexer 2 Preview";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Indexing Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset toobe indexed.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Vínculos relacionados
[Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)](media-services-analytics-overview.md)

[Demostraciones de Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

