---
title: "aaaDetect cara y las emociones con análisis de multimedia de Azure | Documentos de Microsoft"
description: "Este tema muestra cómo se enfrenta a toodetect y emociones con análisis de multimedia de Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a>Detección de caras y emociones con Análisis multimedia de Azure
## <a name="overview"></a>Información general
Hola **Detector de caras de multimedia de Azure** procesador multimedia (MP) le permite toocount, movimientos de seguimiento y participación de la audiencia de medidor incluso y reacción a través de expresiones faciales. Este servicio contiene dos características: 

* **Detección de caras**
  
    La detección de caras busca y realiza el seguimiento de caras humanas dentro de un vídeo. Varias caras pueden detectarse y posteriormente se realiza el seguimiento de medida que se mueven, con metadatos de tiempo y la ubicación de hello devueltos en un archivo JSON. Durante el seguimiento, tratará de toogive un toohello identificador coherente mismo enfrentan mientras está moviendo persona Hola en pantalla, incluso si se puede ver obstruidos o brevemente deje marco Hola.
  
  > [!NOTE]
  > Este servicio no lleva a cabo el reconocimiento facial. Una persona que sale del marco de Hola o deja de estar obstruida para demasiado larga se le asignará un nuevo identificador cuando devuelven.
  > 
  > 
* **Detección de emociones**
  
    Detección de emoción es un componente opcional de hello procesador de multimedia de detección de cara que devuelve el análisis en varios atributos emoción de caras de hello detectados, incluida la satisfacción, tristeza, temor, ira y mucho más. 

Hola **Detector de caras de multimedia de Azure** MP está actualmente en vista previa.

Este tema proporciona detalles acerca de **Detector de caras de multimedia de Azure** y muestra cómo toouse con el SDK de servicios multimedia para. NET.

## <a name="face-detector-input-files"></a>Archivos de entrada de Face Detector (Detector de caras)
Archivos de vídeo. Actualmente, se admite Hola siguientes formatos: MP4, MOV y WMV.

## <a name="face-detector-output-files"></a>Archivos de salida de Face Detector (Detector de caras)
API de detección y seguimiento de cara de Hello proporciona detección de ubicación de cara de alta precisión y el seguimiento que puede detectar una too64 caras humana en un vídeo. Caras frontales proporcionan Hola los mejores resultados, al lado caras y caras pequeños (menor que o igual a too24x24 píxeles) no sea lo más preciso.

Hello caras detectadas y de seguimiento se devuelven con las coordenadas (izquierda, superior, ancho y alto) que indica la ubicación de Hola de caras de imagen de hello en píxeles, así como una cara identificador numérico que indica Hola seguimiento de ese individuo. Números de Id. de cara son propensas a tooreset en circunstancias cuando cara frontal Hola se pierde o superpuesta en el marco de hello, lo que da lugar a algunas personas al asignarse a varios identificadores.

## <a id="output_elements"></a>Elementos Hola JSON del archivo de salida

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

Detector de caras usa técnicas de fragmentación (donde hello metadatos se pueden dividir en fragmentos basados en tiempo y se puede descargar sólo lo que necesita) y la segmentación (donde los eventos de Hola se dividen en caso de aumenten demasiados). Algunos cálculos sencillos pueden ayudarle a transformar datos Hola. Por ejemplo, si un evento se inició en 6300 (tics), con una escala de tiempo de 2997 (tics/segundo) y una velocidad de fotogramas de 29,97 (fotogramas/segundo), entonces:

* Inicio/Escala de tiempo = 2,1 segundos
* Segundos x Framerate = 63 marcos

## <a name="face-detection-input-and-output-example"></a>Ejemplo de entrada y salida de detección de caras
### <a name="input-video"></a>Vídeo de entrada
[Vídeo de entrada](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Configuración de tareas (valor preestablecido)
Al crear una tarea con **Azure Media Face Detector**(Detector de caras multimedia de Azure), debe especificar un valor predeterminado de configuración. Hola siguiente valor preestablecido de configuración es solo para la detección de cara.

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a>Descripciones de atributos
| Nombre del atributo | Description |
| --- | --- |
| Mode |Rápido: procesamiento rápido, pero menos preciso (valor predeterminado).|

### <a name="json-output"></a>Salida de JSON
se truncaron Hola siguiente ejemplo de salida JSON.

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a>Ejemplo de entrada y salida de detección de emociones
### <a name="input-video"></a>Vídeo de entrada
[Vídeo de entrada](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a>Configuración de tareas (valor preestablecido)
Al crear una tarea con **Azure Media Face Detector**(Detector de caras multimedia de Azure), debe especificar un valor predeterminado de configuración. Hola siguiente valor preestablecido de configuración especifica toocreate que JSON en función de detección de hello emociones.

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a>Descripciones de atributos
| Nombre del atributo | Description |
| --- | --- |
| Mode |Faces: solo detección de caras.<br/>PerFaceEmotion: devolver emociones independientemente para cada detección de cara.<br/>AggregateEmotion: Devolver valores de emociones medios para todas las caras del fotograma. |
| AggregateEmotionWindowMs |Utilizar si se selecciona el modo AggregateEmotion. Especifica longitud Hola de vídeo tooproduce utilizado cada resultado agregado, en milisegundos. |
| AggregateEmotionIntervalMs |Utilizar si se selecciona el modo AggregateEmotion. Especifica con qué agregado de tooproduce frecuencia da como resultado. |

#### <a name="aggregate-defaults"></a>Agregar valores predeterminados
A continuación se recomiendan los valores de ventana agregada de Hola y la configuración de intervalos. AggregateEmotionWindowMs debe ser mayor que AggregateEmotionIntervalMs.

|| Valores predeterminados | Mínimos | Máximos |
|--- | --- | --- | --- |
| AggregateEmotionWindowMs |0,5 |2 |0,25|
| AggregateEmotionIntervalMs |0,5 |1 |0,25|

### <a name="json-output"></a>Salida de JSON
Salida de JSON para la emoción agregada (truncada):

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a>Limitaciones
* formatos de vídeo de entrada de Hello compatibles incluyen MP4, MOV y WMV.
* intervalo de tamaño de cara detectables de Hello es too2048x2048 de 24 x 24 píxeles. no se detectarán las caras de Hello fuera de este intervalo.
* Para cada vídeo, número máximo de Hola de caras devuelto es 64.
* Algunas caras podrían no detectarse debido a problemas de tootechnical; Por ejemplo, un gran ángulos de cara (head postura) y oclusión grande. Caras frontales y cerca frontal tienen los mejores resultados Hola.

## <a name="net-sample-code"></a>Código de ejemplo de .NET

siguiente de Hello programa muestra cómo:

1. Crear un activo y cargar un archivo multimedia en activo de Hola.
2. Crear un trabajo con una tarea de detección de la cara basada en un archivo de configuración que contiene Hola siguiente valor preestablecido de json. 
   
        {
            "version": "1.0"
        }
3. Descargar archivos de hello salida JSON. 

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

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

[Demostraciones de Azure Media Analytics](http://amslabs.azurewebsites.net/demos/Analytics.html)

