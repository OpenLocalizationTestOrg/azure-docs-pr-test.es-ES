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
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="6f8a1-104">Archivos multimedia de Hyperlapse con Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="6f8a1-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="6f8a1-105">Azure Media Hyperlapse es un procesador de multimedia (MP) que crea vídeos fluidos con la técnica time-lapse a partir de contenido generado en primera persona o con una cámara de acción.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="6f8a1-106">Hola relacionado en la nube demasiado[Microsoft Research desktop Hyperlapse Pro y basada en el teléfono móvil de Hyperlapse](http://aka.ms/hyperlapse), Microsoft Hyperlapse para servicios multimedia de Azure utiliza escala masiva de Hola de hello multimedia de servicios multimedia de Azure Procesamiento toohorizontally plataforma escalar y paralelizar masiva Hyperlapse procesamiento.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-106">hello cloud-based sibling too[Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes hello massive scale of hello Azure Media Services Media Processing platform toohorizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f8a1-107">Microsoft Hyperlapse es toowork diseñada mejor en el contenido de la primera persona con una cámara móvil.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-107">Microsoft Hyperlapse is designed toowork best on first-person content with a moving camera.</span></span>  <span data-ttu-id="6f8a1-108">Aunque todavía pueden funcionar grabaciones de cámara fija, no se puede garantizar Hola rendimiento y la calidad de hello procesador multimedia Azure Media Hyperlapse para otros tipos de contenido.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-108">Although still-camera footage can still work, hello performance and quality of hello Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="6f8a1-109">toolearn más información sobre Microsoft Hyperlapse para servicios multimedia de Azure y ver algunos vídeos de ejemplo, desproteger hello [entrada de blog Introducción](http://aka.ms/azurehyperlapseblog) de versión preliminar pública de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-109">toolearn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out hello [introductory blog post](http://aka.ms/azurehyperlapseblog) from hello public preview.</span></span>
> 
> 

<span data-ttu-id="6f8a1-110">Un Azure Media Hyperlapse trabajo toma como entrada un archivo de recursos MP4, MOV o WMV junto con un archivo de configuración que especifica qué fotogramas de vídeo deben ser el tiempo transcurrido y velocidad de toowhat (por ejemplo, primer 10.000 fotogramas al x 2).</span><span class="sxs-lookup"><span data-stu-id="6f8a1-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and toowhat speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="6f8a1-111">salida de Hello es una copia estabilizar y vencido de tiempo del vídeo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-111">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

<span data-ttu-id="6f8a1-112">Actualizaciones más recientes de Azure Media Hyperlapse de hello, consulte [blogs de servicios multimedia](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="6f8a1-112">For hello latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="6f8a1-113">Aplicar Hyperlapse a un recurso</span><span class="sxs-lookup"><span data-stu-id="6f8a1-113">Hyperlapse an asset</span></span>
<span data-ttu-id="6f8a1-114">En primer lugar deberá tooupload su tooAzure de archivo de entrada deseado servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-114">First you will need tooupload your desired input file tooAzure Media Services.</span></span>  <span data-ttu-id="6f8a1-115">Obtenga más información sobre toolearn Hola conceptos relacionados con la carga y administración de contenido, leer hello [artículo de administración de contenido](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6f8a1-115">toolearn more about hello concepts involved with uploading and managing content, read hello [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="6f8a1-116"><a id="configuration"></a>Preestablecimiento de configuración para Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="6f8a1-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="6f8a1-117">Una vez que el contenido está en su cuenta de servicios multimedia, necesitará tooconstruct preestablece la configuración.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-117">Once your content is in your Media Services account, you will need tooconstruct your configuration preset.</span></span>  <span data-ttu-id="6f8a1-118">Hello en la tabla siguiente explica los campos de hello especificado por el usuario:</span><span class="sxs-lookup"><span data-stu-id="6f8a1-118">hello following table explains hello user-specified fields:</span></span>

| <span data-ttu-id="6f8a1-119">Campo</span><span class="sxs-lookup"><span data-stu-id="6f8a1-119">Field</span></span> | <span data-ttu-id="6f8a1-120">Description</span><span class="sxs-lookup"><span data-stu-id="6f8a1-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6f8a1-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="6f8a1-121">StartFrame</span></span> |<span data-ttu-id="6f8a1-122">marco de Hello en qué Hola Microsoft Hyperlapse debe comenzar el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-122">hello frame upon which hello Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="6f8a1-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="6f8a1-123">NumFrames</span></span> |<span data-ttu-id="6f8a1-124">número de Hola de marcos tooprocess</span><span class="sxs-lookup"><span data-stu-id="6f8a1-124">hello number of frames tooprocess</span></span> |
| <span data-ttu-id="6f8a1-125">Velocidad</span><span class="sxs-lookup"><span data-stu-id="6f8a1-125">Speed</span></span> |<span data-ttu-id="6f8a1-126">factor de Hello con qué toospeed el vídeo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-126">hello factor with which toospeed up hello input video.</span></span> |

<span data-ttu-id="6f8a1-127">Hola te mostramos un ejemplo de un archivo de configuración compatible en JSON y XML:</span><span class="sxs-lookup"><span data-stu-id="6f8a1-127">hello following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="6f8a1-128">**Valor preestablecido XML:**</span><span class="sxs-lookup"><span data-stu-id="6f8a1-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="6f8a1-129">**Valor preestablecido JSON:**</span><span class="sxs-lookup"><span data-stu-id="6f8a1-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="6f8a1-130"><a id="sample_code"></a>Microsoft Hyperlapse con hello AMS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6f8a1-130"><a id="sample_code"></a> Microsoft Hyperlapse with hello AMS .NET SDK</span></span>
<span data-ttu-id="6f8a1-131">Hello método siguiente carga un archivo multimedia como un recurso y crea un trabajo con hello procesador multimedia Azure Media Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-131">hello following method uploads a media file as an asset and creates a job with hello Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="6f8a1-132">Ya debe tener un CloudMediaContext en el ámbito con hello nombre "context" de este toowork de código.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-132">You should already have a CloudMediaContext in scope with hello name "context" for this code toowork.</span></span>  <span data-ttu-id="6f8a1-133">más información acerca de esto, Hola lectura toolearn [artículo de administración de contenido](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6f8a1-133">toolearn more about this, read hello [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="6f8a1-134">argumento de cadena de Hola "hyperConfig" es el esperado toobe una configuración compatible con valor preestablecida en formato JSON o XML como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6f8a1-134">hello string argument "hyperConfig" is expected toobe a conformant configuration preset in either JSON or XML as described above.</span></span>
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

### <span data-ttu-id="6f8a1-135"><a id="file_types"></a>Tipos de archivo admitidos</span><span class="sxs-lookup"><span data-stu-id="6f8a1-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="6f8a1-136">MP4</span><span class="sxs-lookup"><span data-stu-id="6f8a1-136">MP4</span></span>
* <span data-ttu-id="6f8a1-137">MOV</span><span class="sxs-lookup"><span data-stu-id="6f8a1-137">MOV</span></span>
* <span data-ttu-id="6f8a1-138">WMV</span><span class="sxs-lookup"><span data-stu-id="6f8a1-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6f8a1-139">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="6f8a1-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6f8a1-140">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="6f8a1-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="6f8a1-141">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="6f8a1-141">Related links</span></span>
[<span data-ttu-id="6f8a1-142">Azure Media Services Analytics Overview (Información general sobre análisis de Servicios multimedia de Azure)</span><span class="sxs-lookup"><span data-stu-id="6f8a1-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="6f8a1-143">Demostraciones de Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="6f8a1-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

