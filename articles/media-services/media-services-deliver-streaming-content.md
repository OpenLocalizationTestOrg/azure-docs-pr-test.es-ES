---
title: aaaPublish contenido de servicios multimedia de Azure mediante .NET | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un localizador de toobuild usa una dirección URL de streaming. Ejemplos de código están escritos en C# y usar hello SDK de servicios multimedia para. NET."
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
ms.openlocfilehash: c941cd93c252a96e66546cce2793bb426afac059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="24225-104">Publicación de contenido de Servicios multimedia de Azure con.NET</span><span class="sxs-lookup"><span data-stu-id="24225-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="24225-105">REST</span><span class="sxs-lookup"><span data-stu-id="24225-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="24225-106">.NET</span><span class="sxs-lookup"><span data-stu-id="24225-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="24225-107">Portal</span><span class="sxs-lookup"><span data-stu-id="24225-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="24225-108">Información general</span><span class="sxs-lookup"><span data-stu-id="24225-108">Overview</span></span>
<span data-ttu-id="24225-109">Puede transmitir un conjunto de archivos MP4 de velocidad de bits adaptable creando un localizador de streaming a petición y compilando una dirección URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="24225-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="24225-110">Hola [codificar un recurso](media-services-encode-asset.md) tema muestra cómo establece tooencode en una velocidad de bits adaptativa MP4.</span><span class="sxs-lookup"><span data-stu-id="24225-110">hello [encoding an asset](media-services-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="24225-111">Si el contenido está cifrado, configure la directiva de entrega de recursos (como se describe en [este](media-services-dotnet-configure-asset-delivery-policy.md) tema) antes de crear un localizador.</span><span class="sxs-lookup"><span data-stu-id="24225-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="24225-112">También puede utilizar un localizador toobuild las direcciones URL que los archivos de punto de tooMP4 se pueden descargar progresivamente de transmisión por secuencias a petición.</span><span class="sxs-lookup"><span data-stu-id="24225-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="24225-113">Este tema se muestra cómo toocreate una transmisión por secuencias localizador toopublish los activos y compile un suave, MPEG DASH, HLS direcciones URL de streaming a petición.</span><span class="sxs-lookup"><span data-stu-id="24225-113">This topic shows how toocreate an OnDemand streaming locator toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="24225-114">También muestra toobuild activa direcciones URL de descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="24225-114">It also shows hot toobuild progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="24225-115">Creación de un localizador de streaming a petición</span><span class="sxs-lookup"><span data-stu-id="24225-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="24225-116">toocreate Hola localizador de streaming a petición y obtener las direcciones URL, es necesario hello toodo siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="24225-116">toocreate hello OnDemand streaming locator and get URLs, you need toodo hello following things:</span></span>

1. <span data-ttu-id="24225-117">Si se cifra el contenido de hello, definir una directiva de acceso.</span><span class="sxs-lookup"><span data-stu-id="24225-117">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="24225-118">Cree un localizador de streaming a petición.</span><span class="sxs-lookup"><span data-stu-id="24225-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="24225-119">Si tiene previsto toostream, obtener Hola transmisión por secuencias de archivo de manifiesto (.ism) en el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="24225-119">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="24225-120">Si tiene previsto tooprogressively descarga, obtener nombres de Hola de archivos MP4 en activos de Hola.</span><span class="sxs-lookup"><span data-stu-id="24225-120">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span>  
4. <span data-ttu-id="24225-121">Generar archivo de manifiesto de toohello de direcciones URL o archivos MP4.</span><span class="sxs-lookup"><span data-stu-id="24225-121">Build URLs toohello manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="24225-122">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="24225-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="24225-123">Use Hola mismo Id. de directiva si utilizas siempre Hola mismo días / permisos de acceso.</span><span class="sxs-lookup"><span data-stu-id="24225-123">Use hello same policy ID if you are always using hello same days / access permissions.</span></span> <span data-ttu-id="24225-124">Por ejemplo, las directivas para localizadores que están pensadas tooremain en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="24225-124">For example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="24225-125">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="24225-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="24225-126">Uso del SDK de .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="24225-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="24225-127">Generación de direcciones URL de streaming</span><span class="sxs-lookup"><span data-stu-id="24225-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL toomanifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL toomanifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL toomanifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="24225-128">Hola salidas:</span><span class="sxs-lookup"><span data-stu-id="24225-128">hello outputs:</span></span>

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="24225-129">También puede transmitir el contenido por una conexión SSL.</span><span class="sxs-lookup"><span data-stu-id="24225-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="24225-130">toodo este enfoque, asegúrese de que la transmisión por secuencias de inicio de las direcciones URL con HTTPS.</span><span class="sxs-lookup"><span data-stu-id="24225-130">toodo this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="24225-131">Actualmente, AMS no admite SSL con dominios personalizados.</span><span class="sxs-lookup"><span data-stu-id="24225-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="24225-132">Creación de direcciones URL de descarga progresiva</span><span class="sxs-lookup"><span data-stu-id="24225-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator toohello asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL toohello MP4 files. Use this tooprogressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="24225-133">Hola salidas:</span><span class="sxs-lookup"><span data-stu-id="24225-133">hello outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="24225-134">Uso de Extensiones del SDK .NET de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="24225-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="24225-135">Hello código siguiente llama a métodos de extensiones de SDK de .NET que creación un localizador y generan Hola Smooth Streaming, HLS y MPEG-DASH las direcciones URL para la transmisión por secuencias adaptativa.</span><span class="sxs-lookup"><span data-stu-id="24225-135">hello following code calls .NET SDK extensions methods that create a locator and generate hello Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get hello streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="24225-136">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="24225-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="24225-137">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="24225-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="24225-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24225-138">Next steps</span></span>
* [<span data-ttu-id="24225-139">Descarga de activos</span><span class="sxs-lookup"><span data-stu-id="24225-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="24225-140">Configuración de directivas de entrega de activos</span><span class="sxs-lookup"><span data-stu-id="24225-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

