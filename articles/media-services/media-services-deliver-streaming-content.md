---
title: "Publicación de contenido de Azure Media Services mediante .NET | Microsoft Docs"
description: "Aprenda a crear un localizador que se usa para generar una dirección URL de streaming. Los ejemplos de código están escritos en C# y utilizan el SDK de Servicios multimedia para .NET."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 2bcb012eef84faa7c1e13ed22e88e45e4300ed54
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="9ead4-104">Publicación de contenido de Servicios multimedia de Azure con.NET</span><span class="sxs-lookup"><span data-stu-id="9ead4-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ead4-105">REST</span><span class="sxs-lookup"><span data-stu-id="9ead4-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="9ead4-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9ead4-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="9ead4-107">Portal</span><span class="sxs-lookup"><span data-stu-id="9ead4-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9ead4-108">Información general</span><span class="sxs-lookup"><span data-stu-id="9ead4-108">Overview</span></span>
<span data-ttu-id="9ead4-109">Puede transmitir un conjunto de archivos MP4 de velocidad de bits adaptable creando un localizador de streaming a petición y compilando una dirección URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="9ead4-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="9ead4-110">El tema [Codificación de un recurso](media-services-encode-asset.md) muestra cómo codificar en un conjunto de MP4 de velocidad de bits adaptable.</span><span class="sxs-lookup"><span data-stu-id="9ead4-110">The [encoding an asset](media-services-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="9ead4-111">Si el contenido está cifrado, configure la directiva de entrega de recursos (como se describe en [este](media-services-dotnet-configure-asset-delivery-policy.md) tema) antes de crear un localizador.</span><span class="sxs-lookup"><span data-stu-id="9ead4-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="9ead4-112">También puede utilizar un localizador de streaming a petición para generar direcciones URL que señalen a archivos MP4 que se pueden descargar progresivamente.</span><span class="sxs-lookup"><span data-stu-id="9ead4-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="9ead4-113">En este tema se muestra cómo crear un localizador de streaming a petición para publicar el recurso y crear direcciones URL de streaming Smooth, MPEG DASH y HLS.</span><span class="sxs-lookup"><span data-stu-id="9ead4-113">This topic shows how to create an OnDemand streaming locator to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="9ead4-114">También se muestra cómo generar direcciones URL de descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="9ead4-114">It also shows hot to build progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="9ead4-115">Creación de un localizador de streaming a petición</span><span class="sxs-lookup"><span data-stu-id="9ead4-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="9ead4-116">Para crear el localizador de streaming a petición y obtener las direcciones URL, deberá hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9ead4-116">To create the OnDemand streaming locator and get URLs, you need to do the following things:</span></span>

1. <span data-ttu-id="9ead4-117">Si se cifra el contenido, defina una directiva de acceso.</span><span class="sxs-lookup"><span data-stu-id="9ead4-117">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="9ead4-118">Cree un localizador de streaming a petición.</span><span class="sxs-lookup"><span data-stu-id="9ead4-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="9ead4-119">Si planea transmitir, obtenga el archivo de manifiesto de streaming (.ism) del recurso.</span><span class="sxs-lookup"><span data-stu-id="9ead4-119">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="9ead4-120">Si planea la descarga progresiva, obtenga los nombres de los archivos MP4 del recurso.</span><span class="sxs-lookup"><span data-stu-id="9ead4-120">If you plan to progressively download, get the names of MP4 files in the asset.</span></span>  
4. <span data-ttu-id="9ead4-121">Genere direcciones URL para el archivo de manifiesto o archivos MP4.</span><span class="sxs-lookup"><span data-stu-id="9ead4-121">Build URLs to the manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="9ead4-122">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="9ead4-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="9ead4-123">Utilice el mismo identificador de directiva si siempre usa los mismos días o permisos de acceso.</span><span class="sxs-lookup"><span data-stu-id="9ead4-123">Use the same policy ID if you are always using the same days / access permissions.</span></span> <span data-ttu-id="9ead4-124">Por ejemplo, directivas para localizadores que van a permanecer durante mucho tiempo (directivas no de carga).</span><span class="sxs-lookup"><span data-stu-id="9ead4-124">For example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="9ead4-125">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="9ead4-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="9ead4-126">Uso del SDK de .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="9ead4-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="9ead4-127">Generación de direcciones URL de streaming</span><span class="sxs-lookup"><span data-stu-id="9ead4-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator to the streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on the locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference to the streaming manifest file from the  
        // collection of files in the asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL to the manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL to manifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL to manifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL to manifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="9ead4-128">Las salidas:</span><span class="sxs-lookup"><span data-stu-id="9ead4-128">The outputs:</span></span>

    URL to manifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL to manifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL to manifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="9ead4-129">También puede transmitir el contenido por una conexión SSL.</span><span class="sxs-lookup"><span data-stu-id="9ead4-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="9ead4-130">Para llevar a cabo este enfoque, asegúrese de que las direcciones URL de streaming comienzan por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9ead4-130">To do this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="9ead4-131">Actualmente, AMS no admite SSL con dominios personalizados.</span><span class="sxs-lookup"><span data-stu-id="9ead4-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="9ead4-132">Creación de direcciones URL de descarga progresiva</span><span class="sxs-lookup"><span data-stu-id="9ead4-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator to the asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on the locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL to the MP4 files. Use this to progressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="9ead4-133">Las salidas:</span><span class="sxs-lookup"><span data-stu-id="9ead4-133">The outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="9ead4-134">Uso de Extensiones del SDK .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="9ead4-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="9ead4-135">El código siguiente llama a los métodos de extensiones del SDK de .NET que crean un localizador y generan las direcciones URL de Smooth Streaming, HLS y MPEG-DASH para el streaming adaptable.</span><span class="sxs-lookup"><span data-stu-id="9ead4-135">The following code calls .NET SDK extensions methods that create a locator and generate the Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get the streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="9ead4-136">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="9ead4-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9ead4-137">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="9ead4-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="9ead4-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9ead4-138">Next steps</span></span>
* [<span data-ttu-id="9ead4-139">Descarga de activos</span><span class="sxs-lookup"><span data-stu-id="9ead4-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="9ead4-140">Configuración de directivas de entrega de activos</span><span class="sxs-lookup"><span data-stu-id="9ead4-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

