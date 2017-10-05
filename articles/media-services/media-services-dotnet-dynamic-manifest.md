---
title: "Creación de filtros con .NET SDK de Servicios multimedia de Azure"
description: "En este tema se describe cómo crear filtros para que su cliente pueda usarlos para el streaming de secciones específicas de una secuencia. Servicios multimedia crea manifiestos dinámicos para lograr este streaming selectivo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 6c43473b86c14679ace558de478bd95f41d476da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="193c6-104">Creación de filtros con .NET SDK de Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="193c6-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="193c6-105">.NET</span><span class="sxs-lookup"><span data-stu-id="193c6-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="193c6-106">REST</span><span class="sxs-lookup"><span data-stu-id="193c6-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="193c6-107">A partir de la versión 2.11, los Servicios multimedia permiten definir filtros para los activos.</span><span class="sxs-lookup"><span data-stu-id="193c6-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="193c6-108">Estos filtros son reglas del lado servidor que permitirán a los clientes elegir realizar acciones como: reproducir solo una sección de un vídeo (en lugar de reproducir el vídeo completo), o especificar solo un subconjunto de las representaciones de audio y vídeo que el dispositivo de su cliente puede controlar (en lugar de todas las copias asociadas al activo).</span><span class="sxs-lookup"><span data-stu-id="193c6-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="193c6-109">Este filtrado de sus activos se logra a través de los **manifiestos dinámicos**que se crean tras la solicitud del cliente para transmitir un vídeo en función de los filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="193c6-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="193c6-110">Para obtener más información detallada relacionada con filtros y manifiesto dinámico, vea [Información general de manifiesto dinámico](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="193c6-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="193c6-111">En este tema se muestra cómo usar el SDK de .NET de Servicios multimedia para crear, actualizar y eliminar filtros.</span><span class="sxs-lookup"><span data-stu-id="193c6-111">This topic shows how to use Media Services .NET SDK to create, update, and delete filters.</span></span> 

<span data-ttu-id="193c6-112">Tenga en cuenta que si actualiza un filtro, se pueden tardar hasta 2 minutos en que el extremo de streaming actualice las reglas.</span><span class="sxs-lookup"><span data-stu-id="193c6-112">Note if you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="193c6-113">Si el contenido se proporcionó con este filtro (y se almacenó en caché en los servidores proxy y cachés de CDN), la actualización de este filtro puede generar errores del reproductor.</span><span class="sxs-lookup"><span data-stu-id="193c6-113">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="193c6-114">Se recomienda borrar la memoria caché después de actualizar el filtro.</span><span class="sxs-lookup"><span data-stu-id="193c6-114">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="193c6-115">Si esta opción no es posible, piense en usar un filtro diferente.</span><span class="sxs-lookup"><span data-stu-id="193c6-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="193c6-116">Tipos usados para crear filtros</span><span class="sxs-lookup"><span data-stu-id="193c6-116">Types used to create filters</span></span>
<span data-ttu-id="193c6-117">Al crear filtros, se usan los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="193c6-117">The following types are used when creating filters:</span></span> 

* <span data-ttu-id="193c6-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="193c6-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="193c6-119">Este tipo está basado en la siguiente API de REST [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="193c6-119">This type is based on the following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="193c6-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="193c6-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="193c6-121">Este tipo está basado en la siguiente API de REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="193c6-121">This type is based on the following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="193c6-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="193c6-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="193c6-123">Este tipo está basado en la siguiente API de REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="193c6-123">This type is based on the following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="193c6-124">**FilterTrackSelectStatement** e **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="193c6-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="193c6-125">Estos tipos se basan en las siguientes API de REST [FilterTrackSelect y FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="193c6-125">These types are based on the following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="193c6-126">Creación/actualización/lectura/eliminación de filtros globales</span><span class="sxs-lookup"><span data-stu-id="193c6-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="193c6-127">El código siguiente muestra cómo usar .NET para crear, actualizar, leer y eliminar filtros de recursos.</span><span class="sxs-lookup"><span data-stu-id="193c6-127">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="193c6-128">Creación/actualización/lectura/eliminación de filtros de recursos</span><span class="sxs-lookup"><span data-stu-id="193c6-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="193c6-129">El código siguiente muestra cómo usar .NET para crear, actualizar, leer y eliminar filtros de recursos.</span><span class="sxs-lookup"><span data-stu-id="193c6-129">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="193c6-130">Generar direcciones URL de streaming que usan filtros</span><span class="sxs-lookup"><span data-stu-id="193c6-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="193c6-131">Para obtener información sobre cómo publicar y entregar los activos, vea [Información general de entrega de contenido a clientes](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="193c6-131">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="193c6-132">En los ejemplos siguientes se muestra cómo agregar filtros a sus URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="193c6-132">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="193c6-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="193c6-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="193c6-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="193c6-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="193c6-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="193c6-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="193c6-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="193c6-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="193c6-137">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="193c6-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="193c6-138">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="193c6-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="193c6-139">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="193c6-139">See Also</span></span>
[<span data-ttu-id="193c6-140">Información general de manifiestos dinámicos</span><span class="sxs-lookup"><span data-stu-id="193c6-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

