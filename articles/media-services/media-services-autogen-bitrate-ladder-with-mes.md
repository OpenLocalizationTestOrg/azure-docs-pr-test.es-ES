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
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a>Usar Azure Media Encoder estándar tooauto-generar una escalera de velocidad de bits

## <a name="overview"></a>Información general

Este tema se muestra cómo toouse medios codificador estándar (MES) tooauto-generar una escalera de velocidad de bits (pares de resolución de velocidad de bits) en función de la resolución de entrada de Hola y velocidad de bits. Hello valor preestablecido autogenerada nunca superará velocidad de bits y la resolución de Hola de entrada. Por ejemplo, si la entrada de hello es 720p en 3 Mbps, salida will permanecen en el mejor 720p y se iniciará a velocidades inferiores a 3 Mbps.

### <a name="encoding-for-streaming-only"></a>Codificación solo para streaming

Si su intención es tooencode el origen de vídeo solo para la transmisión por secuencias, a continuación, se deben usar hello "Transmisión por secuencias adaptativa" preestablecido al crear una tarea de codificación. Cuando se usa hello **transmisión por secuencias adaptativa** predefinidos, codificador MES de hello inteligentemente limitar una escalera de velocidad de bits. Sin embargo, no será hello toocontrol capaz de codificación de los costes, ya que el servicio Hola determina cuántos toouse de capas y con qué resolución. Puede ver ejemplos de las capas de salida generados por MES como resultado de la codificación con hello **transmisión por secuencias adaptativa** preestablecido final Hola de este tema. Hola salida Asset contendrá archivos MP4 donde el audio y vídeo no se intercalan.

### <a name="encoding-for-streaming-and-progressive-download"></a>Codificación para streaming y descarga progresiva

Si su intención es tooencode el vídeo de origen para la transmisión por secuencias, así como archivos MP4 de tooproduce para la descarga progresiva, a continuación, se deben usar hello "Contenido adaptable varias velocidades de bits MP4" preestablecido al crear una tarea de codificación. Cuando se usa hello **contenido adaptativa MP4 de velocidad de bits múltiples** predefinidos, codificador MES de hello aplicará Hola misma lógica de codificación que anteriormente, pero ahora activo de salida de hello contendrá MP4 archivos donde audio y vídeo son intercalada. Puede usar uno de estos archivos MP4 (por ejemplo, hello versión más alta velocidad de bits) como un archivo de descarga progresiva.

## <a id="encoding_with_dotnet"></a>Codificación con el SDK de .NET de Servicios multimedia

Hola el ejemplo de código siguiente utiliza Hola de Media Services .NET SDK tooperform siguiente las tareas:

- Crear un trabajo de codificación.
- Obtiene un Codificador multimedia codificador estándar toohello de referencia.
- Agregar un trabajo de toohello tarea codificación y especificar hello toouse **transmisión por secuencias adaptativa** preestablecido. 
- Crear un recurso de salida que contendrá asset Hola codificado.
- Agregue un progreso del controlador de eventos toocheck Hola trabajo.
- Enviar el trabajo de Hola.

#### <a name="create-and-configure-a-visual-studio-project"></a>Creación y configuración de un proyecto de Visual Studio

Configurar el entorno de desarrollo y rellenar el archivo app.config de hello con información de conexión, como se describe en [desarrollo de servicios multimedia con .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Ejemplo

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

## <a id="output"></a>Salida

En esta sección se muestra tres ejemplos de niveles de salida generados por MES como resultado de la codificación con hello **transmisión por secuencias adaptativa** preestablecido. 

### <a name="example-1"></a>Ejemplo 1
Un origen con un alto de "1080" y una tasa de fotogramas de "29.970" genera 6 niveles de vídeo:

|Nivel|Alto|Ancho|Velocidad de bits (kbps)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1280|3520|
|3|540|960|2210|
|4|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>Ejemplo 2
Un origen con un alto de "720" y una tasa de fotogramas de "23.970" genera 5 niveles de vídeo:

|Nivel|Alto|Ancho|Velocidad de bits (kbps)|
|---|---|---|---|
|1|720|1280|2940|
|2|540|960|1850|
|3|360|640|960|
|4|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>Ejemplo 3
Un origen con un alto de "360" y una tasa de fotogramas de "29.970" genera 3 niveles de vídeo:

|Nivel|Alto|Ancho|Velocidad de bits (kbps)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|
## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[Información general sobre la codificación de Servicios multimedia](media-services-encode-asset.md)

