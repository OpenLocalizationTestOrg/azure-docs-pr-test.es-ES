---
title: Filtros de aaaCreating con el SDK de .NET de servicios multimedia de Azure
description: "Este tema describe cómo toocreate filtros para que el cliente pueda usarlas toostream secciones específicas de una secuencia. Servicios multimedia crea manifiestos dinámicos tooachieve este selectivo de transmisión por secuencias."
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
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="57e20-104">Creación de filtros con .NET SDK de Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="57e20-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57e20-105">.NET</span><span class="sxs-lookup"><span data-stu-id="57e20-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="57e20-106">REST</span><span class="sxs-lookup"><span data-stu-id="57e20-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="57e20-107">A partir de la versión 2.11, servicios multimedia permite toodefine filtros para los activos.</span><span class="sxs-lookup"><span data-stu-id="57e20-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="57e20-108">Estos filtros son reglas de lado de servidor que permitirán que los clientes toochoose toodo cosas como: reproducción únicamente una sección de un vídeo (en lugar de reproducir Hola completos de vídeo), o especifique solo un subconjunto de copias de audio y vídeo que los dispositivos de su cliente pueden controlar () en lugar de todas las copias de Hola que están asociadas a Hola activo).</span><span class="sxs-lookup"><span data-stu-id="57e20-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="57e20-109">Dicho filtrado de los activos se logra a través de **manifiesto dinámica**s que se crean al toostream de solicitud de su cliente un vídeo en función de los filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="57e20-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="57e20-110">Para obtener más información consulte toofilters relacionados y el manifiesto dinámico, [dinámicos manifiestos información general sobre](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57e20-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="57e20-111">Este tema muestra cómo toouse toocreate del SDK de .NET de servicios multimedia, actualizar y eliminar filtros.</span><span class="sxs-lookup"><span data-stu-id="57e20-111">This topic shows how toouse Media Services .NET SDK toocreate, update, and delete filters.</span></span> 

<span data-ttu-id="57e20-112">Tenga en cuenta que si actualiza un filtro, puede tardar hasta minutos too2 para reglas de hello toorefresh de extremo de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="57e20-112">Note if you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="57e20-113">Si el contenido de Hola se sirvió usando este filtro (y almacena en caché en los servidores proxy y CDN memorias caché), actualización de este filtro puede producir errores en el Reproductor.</span><span class="sxs-lookup"><span data-stu-id="57e20-113">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="57e20-114">Es recomendable caché de hello tooclear después de actualizar el filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="57e20-114">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="57e20-115">Si esta opción no es posible, piense en usar un filtro diferente.</span><span class="sxs-lookup"><span data-stu-id="57e20-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="57e20-116">Los tipos utilizan filtros de toocreate</span><span class="sxs-lookup"><span data-stu-id="57e20-116">Types used toocreate filters</span></span>
<span data-ttu-id="57e20-117">Hello tipos siguientes se usan al crear filtros:</span><span class="sxs-lookup"><span data-stu-id="57e20-117">hello following types are used when creating filters:</span></span> 

* <span data-ttu-id="57e20-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="57e20-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="57e20-119">Este tipo se basa en hello después de la API de REST [filtro](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="57e20-119">This type is based on hello following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="57e20-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="57e20-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="57e20-121">Este tipo se basa en hello después de la API de REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="57e20-121">This type is based on hello following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="57e20-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="57e20-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="57e20-123">Este tipo se basa en hello después de la API de REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="57e20-123">This type is based on hello following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="57e20-124">**FilterTrackSelectStatement** e **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="57e20-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="57e20-125">Estos tipos se basan en hello después de las API de REST [FilterTrackSelect y FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="57e20-125">These types are based on hello following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="57e20-126">Creación/actualización/lectura/eliminación de filtros globales</span><span class="sxs-lookup"><span data-stu-id="57e20-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="57e20-127">Hello código siguiente muestra cómo toouse .NET toocreate, actualizar, leer y eliminar filtros de activos.</span><span class="sxs-lookup"><span data-stu-id="57e20-127">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

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


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="57e20-128">Creación/actualización/lectura/eliminación de filtros de recursos</span><span class="sxs-lookup"><span data-stu-id="57e20-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="57e20-129">Hello código siguiente muestra cómo toouse .NET toocreate, actualizar, leer y eliminar filtros de activos.</span><span class="sxs-lookup"><span data-stu-id="57e20-129">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

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




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="57e20-130">Generar direcciones URL de streaming que usan filtros</span><span class="sxs-lookup"><span data-stu-id="57e20-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="57e20-131">Para obtener información sobre cómo toopublish y ofrecer sus activos, consulte [información general de entrega de contenido tooCustomers](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57e20-131">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="57e20-132">Hello en los ejemplos siguientes muestran cómo tooadd filtros tooyour direcciones URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="57e20-132">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="57e20-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="57e20-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="57e20-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="57e20-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="57e20-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="57e20-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="57e20-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="57e20-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="57e20-137">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="57e20-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="57e20-138">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="57e20-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="57e20-139">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="57e20-139">See Also</span></span>
[<span data-ttu-id="57e20-140">Información general de manifiestos dinámicos</span><span class="sxs-lookup"><span data-stu-id="57e20-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

