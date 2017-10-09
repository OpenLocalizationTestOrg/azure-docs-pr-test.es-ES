---
title: "aaaRedact caras con análisis de multimedia de Azure | Documentos de Microsoft"
description: "Este tema muestra cómo se enfrenta a tooredact con análisis de multimedia de Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a>Censura de rostros con Azure Media Analytics
## <a name="overview"></a>Información general
**Redactor de Azure Media** es un [análisis de multimedia de Azure](media-services-analytics-overview.md) procesador multimedia (MP) que ofrece la redacción de cara escalable en la nube de Hola. Redacción de cara permite toomodify el vídeo en caras de tooblur de orden de los usuarios seleccionados. Puede desear toouse Hola el servicio de redacción de cara en escenarios de seguridad y medios de noticias públicos. Unos pocos minutos después de material de archivo que contiene varios tipos pueden tardar horas tooredact manualmente, pero con esta imagen de hello servicio proceso de redacción requiere unos pocos pasos sencillos. Para más información, consulte [este blog](https://azure.microsoft.com/blog/azure-media-redactor/).

Este tema proporciona detalles acerca de **Redactor de multimedia de Azure** y muestra cómo toouse con el SDK de servicios multimedia para. NET.

Hola **Redactor de multimedia de Azure** MP está actualmente en vista previa. Está disponible en todas las regiones de Azure públicas, así como en los centros de datos de China y el gobierno de Estados Unidos. Actualmente, esta versión preliminar es gratuita. 

## <a name="face-redaction-modes"></a>Modos de censura de rostros
Redacción facial funciona mediante la detección de caras en cada fotograma de vídeo y seguimiento cara Hola objeto tanto hacia delante y hacia atrás en el tiempo, para que hello misma persona puede ser borrosa desde otros ángulos así. Hola proceso automatizado de redacción es muy compleja y no genera siempre el 100% del resultado deseado, por este motivo que análisis multimedia proporciona con un par de formas de obtener el resultado final hello toomodify.

En suma tooa totalmente el modo automático, hay un flujo de trabajo de dos pasos que permite Hola selección/desinstalación-selection de caras se encuentra a través de una lista de identificadores. Además, toomake arbitrario por Hola de ajustes de marco MP usa un archivo de metadatos en formato JSON. Este flujo de trabajo se divide en los modos **Analyze** (Analizar) y **Redact** (Censurar). Puede combinar los dos modos de hello en un único paso que ejecuta dos tareas en un trabajo; este modo se denomina **Combined**.

### <a name="combined-mode"></a>Modo combinado
Se generará un mp4 censurado automáticamente sin necesidad de intervención manual.

| Fase | Nombre de archivo | Notas |
| --- | --- | --- |
| Recurso de entrada |foo.bar |Vídeo en formato WMV, MOV o MP4 |
| Configuración de entrada |Configuración predeterminada de trabajo |{'version':'1.0', 'options': {'mode':'combined'}} |
| Recurso de salida |foo_redacted.mp4 |Vídeo con difuminado aplicado |

#### <a name="input-example"></a>Ejemplo de entrada:
[Vea este vídeo](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a>Ejemplo de salida:
[Vea este vídeo](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a>Modo Analyze (Análisis)
Hola **analizar** paso del flujo de trabajo de dos pasos Hola toma una entrada de vídeo y genera un archivo JSON de ubicaciones de cara y jpg imágenes de cada detectan cara.

| Fase | Nombre de archivo | Notas |
| --- | --- | --- |
| Recurso de entrada |foo.bar |Vídeo en formato WMV, MOV o MP4 |
| Configuración de entrada |Configuración predeterminada de trabajo |{'version':'1.0', 'options': {'mode':'analyze'}} |
| Recurso de salida |foo_annotations.JSON |Datos de anotación de ubicaciones de rostros en formato JSON. Esto se puede editar mediante Hola usuario toomodify Hola de desenfoque cuadros de límite. Vea el ejemplo a continuación. |
| Recurso de salida |foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg] |Un jpg recortado de cada detectado cara, donde el número de hello indica labelId Hola de cara de Hola |

#### <a name="output-example"></a>Ejemplo de salida:

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a>Modo Redact (Censurar)
segundo pase de Hola de flujo de trabajo de hello tiene un mayor número de entradas que deben combinarse en un solo activo.

Esto incluye una lista de identificadores de tooblur, vídeo original de Hola y anotaciones Hola JSON. Este modo utiliza Hola anotaciones tooapply desenfoque en vídeo de entrada de Hola.

salida de paso de analizar Hola Hello no incluye la vídeo original de Hola. Hola vídeo debe toobe cargado en el recurso de entrada de hello para la tarea de modo de hello Redact y seleccionado como archivo principal de Hola.

| Fase | Nombre de archivo | Notas |
| --- | --- | --- |
| Recurso de entrada |foo.bar |Vídeo en formato WMV, MOV o MP4. El mismo vídeo que en el paso 1. |
| Recurso de entrada |foo_annotations.JSON |archivo de metadatos de anotaciones de la fase uno, con modificaciones opcionales. |
| Recurso de entrada |foo_IDList.txt (opcional) |Nueva línea opcional lista separada de cara tooredact de identificadores. Si se deja en blanco, se difuminarán todas las caras. |
| Configuración de entrada |Configuración predeterminada de trabajo |{'version':'1.0', 'options': {'mode':'analyze'}} |
| Recurso de salida |foo_redacted.mp4 |Vídeo con difuminado aplicado en base a las anotaciones |

#### <a name="example-output"></a>Salida de ejemplo
Este es el resultado de hello desde un Lista_id con un Id. de seleccionado.

[Vea este vídeo](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

foo_IDList.txt de ejemplo
 
     1
     2
     3

## <a name="blur-types"></a>Tipos de desenfoque

Hola **Combined** o **Redact** modo, hay 5 modos desenfoque diferentes posibles a través de la configuración de entrada de JSON de hello: **bajo**, **Med**, **Alta**, **depurar**, y **negro**. Se usa **Medio** de forma predeterminada.

Puede encontrar ejemplos de hello desenfoque tipos siguiente.

### <a name="example-json"></a>Ejemplo de JSON:

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a>Bajo

![Bajo](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a>Medio

![Medio](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a>Alto

![Alto](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a>Depurar

![Depurar](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a>Negro

![Negro](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a>Elementos Hola JSON del archivo de salida

Hola MP de redacción proporciona detección de ubicación de cara de alta precisión y el seguimiento que puede detectar una too64 caras humana en un fotograma de vídeo. Caras frontales proporcionan Hola los mejores resultados, mientras caras laterales y caras pequeñas (menor que o igual a too24x24 píxeles) son un desafío.

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a>Código de ejemplo de .NET

siguiente de Hello programa muestra cómo:

1. Crear un activo y cargar un archivo multimedia en activo de Hola.
2. Crear un trabajo con una tarea de redacción de cara basada en un archivo de configuración que contiene el siguiente valor preestablecido de json de Hola. 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
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

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Vínculos relacionados
[Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)](media-services-analytics-overview.md)

[Demostraciones de Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

