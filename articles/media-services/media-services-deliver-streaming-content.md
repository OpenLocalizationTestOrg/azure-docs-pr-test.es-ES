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
# <a name="publish-azure-media-services-content-using-net"></a>Publicación de contenido de Servicios multimedia de Azure con.NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-deliver-streaming-content.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [Portal](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a>Información general
Puede transmitir un conjunto de archivos MP4 de velocidad de bits adaptable creando un localizador de streaming a petición y compilando una dirección URL de streaming. Hola [codificar un recurso](media-services-encode-asset.md) tema muestra cómo establece tooencode en una velocidad de bits adaptativa MP4. 

> [!NOTE]
> Si el contenido está cifrado, configure la directiva de entrega de recursos (como se describe en [este](media-services-dotnet-configure-asset-delivery-policy.md) tema) antes de crear un localizador. 
> 
> 

También puede utilizar un localizador toobuild las direcciones URL que los archivos de punto de tooMP4 se pueden descargar progresivamente de transmisión por secuencias a petición.  

Este tema se muestra cómo toocreate una transmisión por secuencias localizador toopublish los activos y compile un suave, MPEG DASH, HLS direcciones URL de streaming a petición. También muestra toobuild activa direcciones URL de descarga progresiva. 

## <a name="create-an-ondemand-streaming-locator"></a>Creación de un localizador de streaming a petición
toocreate Hola localizador de streaming a petición y obtener las direcciones URL, es necesario hello toodo siguientes cosas:

1. Si se cifra el contenido de hello, definir una directiva de acceso.
2. Cree un localizador de streaming a petición.
3. Si tiene previsto toostream, obtener Hola transmisión por secuencias de archivo de manifiesto (.ism) en el recurso de Hola. 
   
   Si tiene previsto tooprogressively descarga, obtener nombres de Hola de archivos MP4 en activos de Hola.  
4. Generar archivo de manifiesto de toohello de direcciones URL o archivos MP4. 


>[!NOTE]
>Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy). Use Hola mismo Id. de directiva si utilizas siempre Hola mismo días / permisos de acceso. Por ejemplo, las directivas para localizadores que están pensadas tooremain en su lugar durante mucho tiempo (directivas no carga). Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .

### <a name="use-media-services-net-sdk"></a>Uso del SDK de .NET de Servicios multimedia
Generación de direcciones URL de streaming 

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

Hola salidas:

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> También puede transmitir el contenido por una conexión SSL. toodo este enfoque, asegúrese de que la transmisión por secuencias de inicio de las direcciones URL con HTTPS. Actualmente, AMS no admite SSL con dominios personalizados.
> 
> 

Creación de direcciones URL de descarga progresiva 

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

Hola salidas:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a>Uso de Extensiones del SDK .NET de Servicios multimedia
Hello código siguiente llama a métodos de extensiones de SDK de .NET que creación un localizador y generan Hola Smooth Streaming, HLS y MPEG-DASH las direcciones URL para la transmisión por secuencias adaptativa.

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


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Pasos siguientes
* [Descarga de activos](media-services-deliver-asset-download.md)
* [Configuración de directivas de entrega de activos](media-services-dotnet-configure-asset-delivery-policy.md)

