---
title: aaaHyperlapse archivos multimedia con Azure Media Hyperlapse | Documentos de Microsoft
description: "Azure Media Hyperlapse crea vídeos fluidos con la técnica time-lapse a partir de contenido generado en primera persona o con una cámara de acción. Este tema se muestra cómo toouse Media Indexer."
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a>Archivos multimedia de Hyperlapse con Azure Media Hyperlapse
Azure Media Hyperlapse es un procesador de multimedia (MP) que crea vídeos fluidos con la técnica time-lapse a partir de contenido generado en primera persona o con una cámara de acción.  Hola relacionado en la nube demasiado[Microsoft Research desktop Hyperlapse Pro y basada en el teléfono móvil de Hyperlapse](http://aka.ms/hyperlapse), Microsoft Hyperlapse para servicios multimedia de Azure utiliza escala masiva de Hola de hello multimedia de servicios multimedia de Azure Procesamiento toohorizontally plataforma escalar y paralelizar masiva Hyperlapse procesamiento.

> [!IMPORTANT]
> Microsoft Hyperlapse es toowork diseñada mejor en el contenido de la primera persona con una cámara móvil.  Aunque todavía pueden funcionar grabaciones de cámara fija, no se puede garantizar Hola rendimiento y la calidad de hello procesador multimedia Azure Media Hyperlapse para otros tipos de contenido.  toolearn más información sobre Microsoft Hyperlapse para servicios multimedia de Azure y ver algunos vídeos de ejemplo, desproteger hello [entrada de blog Introducción](http://aka.ms/azurehyperlapseblog) de versión preliminar pública de Hola.
> 
> 

Un Azure Media Hyperlapse trabajo toma como entrada un archivo de recursos MP4, MOV o WMV junto con un archivo de configuración que especifica qué fotogramas de vídeo deben ser el tiempo transcurrido y velocidad de toowhat (por ejemplo, primer 10.000 fotogramas al x 2).  salida de Hello es una copia estabilizar y vencido de tiempo del vídeo de entrada de Hola.

Actualizaciones más recientes de Azure Media Hyperlapse de hello, consulte [blogs de servicios multimedia](https://azure.microsoft.com/blog/topics/media-services/).

## <a name="hyperlapse-an-asset"></a>Aplicar Hyperlapse a un recurso
En primer lugar deberá tooupload su tooAzure de archivo de entrada deseado servicios multimedia.  Obtenga más información sobre toolearn Hola conceptos relacionados con la carga y administración de contenido, leer hello [artículo de administración de contenido](media-services-portal-vod-get-started.md).

### <a id="configuration"></a>Preestablecimiento de configuración para Hyperlapse
Una vez que el contenido está en su cuenta de servicios multimedia, necesitará tooconstruct preestablece la configuración.  Hello en la tabla siguiente explica los campos de hello especificado por el usuario:

| Campo | Description |
| --- | --- |
| StartFrame |marco de Hello en qué Hola Microsoft Hyperlapse debe comenzar el procesamiento. |
| NumFrames |número de Hola de marcos tooprocess |
| Velocidad |factor de Hello con qué toospeed el vídeo de entrada de Hola. |

Hola te mostramos un ejemplo de un archivo de configuración compatible en JSON y XML:

**Valor preestablecido XML:**

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

**Valor preestablecido JSON:**

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <a id="sample_code"></a>Microsoft Hyperlapse con hello AMS .NET SDK
Hello método siguiente carga un archivo multimedia como un recurso y crea un trabajo con hello procesador multimedia Azure Media Hyperlapse.

> [!NOTE]
> Ya debe tener un CloudMediaContext en el ámbito con hello nombre "context" de este toowork de código.  más información acerca de esto, Hola lectura toolearn [artículo de administración de contenido](media-services-dotnet-get-started.md).
> 
> [!NOTE]
> argumento de cadena de Hola "hyperConfig" es el esperado toobe una configuración compatible con valor preestablecida en formato JSON o XML como se describió anteriormente.
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
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
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <a id="file_types"></a>Tipos de archivo admitidos
* MP4
* MOV
* WMV

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Vínculos relacionados
[Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)](media-services-analytics-overview.md)

[Demostraciones de Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

