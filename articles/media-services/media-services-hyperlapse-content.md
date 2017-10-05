---
title: Archivos multimedia de Hyperlapse con Azure Media Hyperlapse | Microsoft Docs
description: "Azure Media Hyperlapse crea vídeos fluidos con la técnica time-lapse a partir de contenido generado en primera persona o con una cámara de acción. En este tema se muestra cómo usar el Indizador multimedia."
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
ms.openlocfilehash: 02f634c2af04b6b372642ab0e6a17a5d29f16450
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="c8f98-104">Archivos multimedia de Hyperlapse con Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c8f98-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="c8f98-105">Azure Media Hyperlapse es un procesador de multimedia (MP) que crea vídeos fluidos con la técnica time-lapse a partir de contenido generado en primera persona o con una cámara de acción.</span><span class="sxs-lookup"><span data-stu-id="c8f98-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="c8f98-106">Microsoft Hyperlapse para Servicios multimedia de Azure, el correspondiente producto para la nube de [Hyperlapse Pro (para equipos de escritorio) y Hyperlapse Mobile (para móviles) de Microsoft Research](http://aka.ms/hyperlapse), usa la escalación masiva de la plataforma de procesamiento de medios de Servicios multimedia de Azure para escalar horizontalmente y establecer paralelismos en el procesamiento masivo de Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="c8f98-106">The cloud-based sibling to [Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes the massive scale of the Azure Media Services Media Processing platform to horizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8f98-107">Microsoft Hyperlapse está diseñado para funcionar mejor con los contenidos grabados en primera persona con una cámara móvil.</span><span class="sxs-lookup"><span data-stu-id="c8f98-107">Microsoft Hyperlapse is designed to work best on first-person content with a moving camera.</span></span>  <span data-ttu-id="c8f98-108">Aunque la grabación con cámara fija también puede funcionar, no se garantiza el rendimiento y la calidad del procesador multimedia Azure Media Hyperlapse para otros tipos de contenido.</span><span class="sxs-lookup"><span data-stu-id="c8f98-108">Although still-camera footage can still work, the performance and quality of the Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="c8f98-109">Para obtener más información acerca de Microsoft Hyperlapse para Servicios multimedia de Azure y ver algunos vídeos de ejemplo, consulte la [publicación de blog de introducción](http://aka.ms/azurehyperlapseblog) en la vista previa pública.</span><span class="sxs-lookup"><span data-stu-id="c8f98-109">To learn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out the [introductory blog post](http://aka.ms/azurehyperlapseblog) from the public preview.</span></span>
> 
> 

<span data-ttu-id="c8f98-110">Un trabajo de Azure Media Hyperlapse toma como entrada un archivo de recurso en formato MP4, MOV o WMV, junto con un archivo de configuración que especifica a qué fotogramas de vídeo se debe aplicar el time-lapse y a qué velocidad (por ejemplo, los primeros 10.000 fotogramas a 2x).</span><span class="sxs-lookup"><span data-stu-id="c8f98-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and to what speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="c8f98-111">El resultado es una representación estabilizada y en time-lapse del vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="c8f98-111">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

<span data-ttu-id="c8f98-112">Para ver las actualizaciones más recientes de Azure Media Hyperlapse, consulte los [blogs de Servicios multimedia](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="c8f98-112">For the latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="c8f98-113">Aplicar Hyperlapse a un recurso</span><span class="sxs-lookup"><span data-stu-id="c8f98-113">Hyperlapse an asset</span></span>
<span data-ttu-id="c8f98-114">Primero debe cargar el archivo de entrada deseado en Servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8f98-114">First you will need to upload your desired input file to Azure Media Services.</span></span>  <span data-ttu-id="c8f98-115">Para obtener más información acerca de los conceptos relacionados con la carga y la administración de contenido, consulte el [artículo de administración de contenido](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c8f98-115">To learn more about the concepts involved with uploading and managing content, read the [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="c8f98-116"><a id="configuration"></a>Preestablecimiento de configuración para Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c8f98-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="c8f98-117">Una vez que el contenido esté en su cuenta de Servicios multimedia, deberá generar la configuración preestablecida.</span><span class="sxs-lookup"><span data-stu-id="c8f98-117">Once your content is in your Media Services account, you will need to construct your configuration preset.</span></span>  <span data-ttu-id="c8f98-118">En la tabla siguiente se describen los campos especificados por el usuario:</span><span class="sxs-lookup"><span data-stu-id="c8f98-118">The following table explains the user-specified fields:</span></span>

| <span data-ttu-id="c8f98-119">Campo</span><span class="sxs-lookup"><span data-stu-id="c8f98-119">Field</span></span> | <span data-ttu-id="c8f98-120">Description</span><span class="sxs-lookup"><span data-stu-id="c8f98-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8f98-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="c8f98-121">StartFrame</span></span> |<span data-ttu-id="c8f98-122">El fotograma en el que debe comenzar el procesamiento de Microsoft Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="c8f98-122">The frame upon which the Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="c8f98-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="c8f98-123">NumFrames</span></span> |<span data-ttu-id="c8f98-124">El número de fotogramas para procesar.</span><span class="sxs-lookup"><span data-stu-id="c8f98-124">The number of frames to process</span></span> |
| <span data-ttu-id="c8f98-125">Velocidad</span><span class="sxs-lookup"><span data-stu-id="c8f98-125">Speed</span></span> |<span data-ttu-id="c8f98-126">El factor por el que se acelera el vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="c8f98-126">The factor with which to speed up the input video.</span></span> |

<span data-ttu-id="c8f98-127">El siguiente es un ejemplo de un archivo de configuración compatible en JSON y XML:</span><span class="sxs-lookup"><span data-stu-id="c8f98-127">The following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="c8f98-128">**Valor preestablecido XML:**</span><span class="sxs-lookup"><span data-stu-id="c8f98-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="c8f98-129">**Valor preestablecido JSON:**</span><span class="sxs-lookup"><span data-stu-id="c8f98-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="c8f98-130"><a id="sample_code"></a> Microsoft Hyperlapse con el SDK de .NET de AMS</span><span class="sxs-lookup"><span data-stu-id="c8f98-130"><a id="sample_code"></a> Microsoft Hyperlapse with the AMS .NET SDK</span></span>
<span data-ttu-id="c8f98-131">El método siguiente carga un archivo multimedia como un recurso y crea un trabajo con el procesador de multimedia de Azure Media Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="c8f98-131">The following method uploads a media file as an asset and creates a job with the Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="c8f98-132">Ya debe tener un CloudMediaContext con el nombre "context" para que este código funcione.</span><span class="sxs-lookup"><span data-stu-id="c8f98-132">You should already have a CloudMediaContext in scope with the name "context" for this code to work.</span></span>  <span data-ttu-id="c8f98-133">Para obtener más información al respecto, lea el [artículo sobre administración de contenido](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c8f98-133">To learn more about this, read the [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="c8f98-134">El argumento de cadena "hyperConfig" debe ser una configuración preestablecida compatible en JSON o XML, como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c8f98-134">The string argument "hyperConfig" is expected to be a conformant configuration preset in either JSON or XML as described above.</span></span>
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

            // If job state is Error, the event handling
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

### <span data-ttu-id="c8f98-135"><a id="file_types"></a>Tipos de archivo admitidos</span><span class="sxs-lookup"><span data-stu-id="c8f98-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="c8f98-136">MP4</span><span class="sxs-lookup"><span data-stu-id="c8f98-136">MP4</span></span>
* <span data-ttu-id="c8f98-137">MOV</span><span class="sxs-lookup"><span data-stu-id="c8f98-137">MOV</span></span>
* <span data-ttu-id="c8f98-138">WMV</span><span class="sxs-lookup"><span data-stu-id="c8f98-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c8f98-139">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="c8f98-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c8f98-140">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="c8f98-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="c8f98-141">Vínculos relacionados</span><span class="sxs-lookup"><span data-stu-id="c8f98-141">Related links</span></span>
[<span data-ttu-id="c8f98-142">Azure Media Services Analytics Overview (Información general sobre Azure Media Services Analytics)</span><span class="sxs-lookup"><span data-stu-id="c8f98-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="c8f98-143">Demostraciones de Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="c8f98-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

