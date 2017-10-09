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
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Creación de filtros con .NET SDK de Servicios multimedia de Azure
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

A partir de la versión 2.11, servicios multimedia permite toodefine filtros para los activos. Estos filtros son reglas de lado de servidor que permitirán que los clientes toochoose toodo cosas como: reproducción únicamente una sección de un vídeo (en lugar de reproducir Hola completos de vídeo), o especifique solo un subconjunto de copias de audio y vídeo que los dispositivos de su cliente pueden controlar () en lugar de todas las copias de Hola que están asociadas a Hola activo). Dicho filtrado de los activos se logra a través de **manifiesto dinámica**s que se crean al toostream de solicitud de su cliente un vídeo en función de los filtros especificados.

Para obtener más información consulte toofilters relacionados y el manifiesto dinámico, [dinámicos manifiestos información general sobre](media-services-dynamic-manifest-overview.md).

Este tema muestra cómo toouse toocreate del SDK de .NET de servicios multimedia, actualizar y eliminar filtros. 

Tenga en cuenta que si actualiza un filtro, puede tardar hasta minutos too2 para reglas de hello toorefresh de extremo de transmisión por secuencias. Si el contenido de Hola se sirvió usando este filtro (y almacena en caché en los servidores proxy y CDN memorias caché), actualización de este filtro puede producir errores en el Reproductor. Es recomendable caché de hello tooclear después de actualizar el filtro de Hola. Si esta opción no es posible, piense en usar un filtro diferente. 

## <a name="types-used-toocreate-filters"></a>Los tipos utilizan filtros de toocreate
Hello tipos siguientes se usan al crear filtros: 

* **IStreamingFilter**.  Este tipo se basa en hello después de la API de REST [filtro](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. Este tipo se basa en hello después de la API de REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. Este tipo se basa en hello después de la API de REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** e **IFilterTrackPropertyCondition**. Estos tipos se basan en hello después de las API de REST [FilterTrackSelect y FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>Creación/actualización/lectura/eliminación de filtros globales
Hello código siguiente muestra cómo toouse .NET toocreate, actualizar, leer y eliminar filtros de activos.

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


## <a name="createupdatereaddelete-asset-filters"></a>Creación/actualización/lectura/eliminación de filtros de recursos
Hello código siguiente muestra cómo toouse .NET toocreate, actualizar, leer y eliminar filtros de activos.

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




## <a name="build-streaming-urls-that-use-filters"></a>Generar direcciones URL de streaming que usan filtros
Para obtener información sobre cómo toopublish y ofrecer sus activos, consulte [información general de entrega de contenido tooCustomers](media-services-deliver-content-overview.md).

Hello en los ejemplos siguientes muestran cómo tooadd filtros tooyour direcciones URL de streaming.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Smooth Streaming**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Otras referencias
[Información general de manifiestos dinámicos](media-services-dynamic-manifest-overview.md)

