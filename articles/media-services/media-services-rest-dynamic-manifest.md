---
title: Filtros de aaaCreating con API de REST de servicios multimedia de Azure | Documentos de Microsoft
description: "Este tema describe cómo toocreate filtros para que el cliente pueda usarlas toostream secciones específicas de una secuencia. Servicios multimedia crea manifiestos dinámicos tooachieve este selectivo de transmisión por secuencias."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="20d58-104">Creación de filtros con la API de REST de Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="20d58-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20d58-105">.NET</span><span class="sxs-lookup"><span data-stu-id="20d58-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="20d58-106">REST</span><span class="sxs-lookup"><span data-stu-id="20d58-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="20d58-107">A partir de la versión 2.11, servicios multimedia permite toodefine filtros para los activos.</span><span class="sxs-lookup"><span data-stu-id="20d58-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="20d58-108">Estos filtros son reglas de lado de servidor que permitirán que los clientes toochoose toodo cosas como: reproducción únicamente una sección de un vídeo (en lugar de reproducir Hola completos de vídeo), o especifique solo un subconjunto de copias de audio y vídeo que los dispositivos de su cliente pueden controlar () en lugar de todas las copias de Hola que están asociadas a Hola activo).</span><span class="sxs-lookup"><span data-stu-id="20d58-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="20d58-109">Dicho filtrado de los activos se archiva a través de **manifiesto dinámica**s que se crean al toostream de solicitud de su cliente un vídeo en función de los filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="20d58-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="20d58-110">Para obtener más información consulte toofilters relacionados y el manifiesto dinámico, [dinámicos manifiestos información general sobre](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20d58-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="20d58-111">Este tema muestra cómo toouse toocreate de las API de REST, actualizar y eliminar filtros.</span><span class="sxs-lookup"><span data-stu-id="20d58-111">This topic shows how toouse REST APIs toocreate, update, and delete filters.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="20d58-112">Los tipos utilizan filtros de toocreate</span><span class="sxs-lookup"><span data-stu-id="20d58-112">Types used toocreate filters</span></span>
<span data-ttu-id="20d58-113">Hello tipos siguientes se usan al crear filtros:</span><span class="sxs-lookup"><span data-stu-id="20d58-113">hello following types are used when creating filters:</span></span>  

* [<span data-ttu-id="20d58-114">Filter</span><span class="sxs-lookup"><span data-stu-id="20d58-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="20d58-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="20d58-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="20d58-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="20d58-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="20d58-117">FilterTrackSelect y FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="20d58-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="20d58-118">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="20d58-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="20d58-119">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="20d58-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="20d58-120">Conectar servicios de tooMedia</span><span class="sxs-lookup"><span data-stu-id="20d58-120">Connect tooMedia Services</span></span>

<span data-ttu-id="20d58-121">Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="20d58-121">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="20d58-122">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="20d58-122">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="20d58-123">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="20d58-123">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="20d58-124">Crear filtros</span><span class="sxs-lookup"><span data-stu-id="20d58-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="20d58-125">Crear filtros globales</span><span class="sxs-lookup"><span data-stu-id="20d58-125">Create global Filters</span></span>
<span data-ttu-id="20d58-126">toocreate un filtro global, utilice Hola siguiendo las solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="20d58-126">toocreate a global Filter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="20d58-127">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-127">HTTP Request</span></span>
<span data-ttu-id="20d58-128">Encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="20d58-128">Request Headers</span></span>

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

<span data-ttu-id="20d58-129">Request body</span><span class="sxs-lookup"><span data-stu-id="20d58-129">Request body</span></span> 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a><span data-ttu-id="20d58-130">Respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="20d58-131">Crear AssetFilters locales</span><span class="sxs-lookup"><span data-stu-id="20d58-131">Create local AssetFilters</span></span>
<span data-ttu-id="20d58-132">toocreate un AssetFilter local, use Hola siguiendo las solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="20d58-132">toocreate a local AssetFilter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="20d58-133">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-133">HTTP Request</span></span>
<span data-ttu-id="20d58-134">Encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="20d58-134">Request Headers</span></span>

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

<span data-ttu-id="20d58-135">Request body</span><span class="sxs-lookup"><span data-stu-id="20d58-135">Request body</span></span> 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a><span data-ttu-id="20d58-136">Respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="20d58-137">Enumerar filtros</span><span class="sxs-lookup"><span data-stu-id="20d58-137">List filters</span></span>
### <a name="get-all-global-filters-in-hello-ams-account"></a><span data-ttu-id="20d58-138">Obtener todos los global **filtro**s en la cuenta de hello AMS</span><span class="sxs-lookup"><span data-stu-id="20d58-138">Get all global **Filter**s in hello AMS account</span></span>
<span data-ttu-id="20d58-139">filtros de toolist, usar hello siguiendo las solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="20d58-139">toolist filters, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="20d58-140">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="20d58-141">Obtener **AssetFilter**s asociados a un recurso</span><span class="sxs-lookup"><span data-stu-id="20d58-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="20d58-142">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="20d58-143">Obtener un **AssetFilter** según su id.</span><span class="sxs-lookup"><span data-stu-id="20d58-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="20d58-144">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="20d58-145">Actualizar filtros</span><span class="sxs-lookup"><span data-stu-id="20d58-145">Update filters</span></span>
<span data-ttu-id="20d58-146">Use PATCH, PUT o MERGE tooupdate un filtro con nuevos valores de propiedad.</span><span class="sxs-lookup"><span data-stu-id="20d58-146">Use PATCH, PUT or MERGE tooupdate a filter with new property values.</span></span>  <span data-ttu-id="20d58-147">Para obtener más información acerca de estas operaciones, vea [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="20d58-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="20d58-148">Si actualiza un filtro, puede tardar minutos too2 para reglas de hello toorefresh de extremo de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="20d58-148">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="20d58-149">Si el contenido de Hola se sirvió usando este filtro (y almacena en caché en los servidores proxy y CDN memorias caché), actualización de este filtro puede producir errores en el Reproductor.</span><span class="sxs-lookup"><span data-stu-id="20d58-149">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="20d58-150">Es recomendable caché de hello tooclear después de actualizar el filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="20d58-150">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="20d58-151">Si esta opción no es posible, piense en usar un filtro diferente.</span><span class="sxs-lookup"><span data-stu-id="20d58-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="20d58-152">Actualizar los filtros globales</span><span class="sxs-lookup"><span data-stu-id="20d58-152">Update global Filters</span></span>
<span data-ttu-id="20d58-153">tooupdate un filtro global, utilice Hola siguiendo las solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="20d58-153">tooupdate a global filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="20d58-154">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-154">HTTP Request</span></span>
<span data-ttu-id="20d58-155">Encabezados de solicitud:</span><span class="sxs-lookup"><span data-stu-id="20d58-155">Request headers:</span></span> 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

<span data-ttu-id="20d58-156">Cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="20d58-156">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a><span data-ttu-id="20d58-157">Actualización de AssetFilters locales</span><span class="sxs-lookup"><span data-stu-id="20d58-157">Update local AssetFilters</span></span>
<span data-ttu-id="20d58-158">tooupdate un filtro local, use Hola siguiendo las solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="20d58-158">tooupdate a local filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="20d58-159">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-159">HTTP Request</span></span>
<span data-ttu-id="20d58-160">Encabezados de solicitud:</span><span class="sxs-lookup"><span data-stu-id="20d58-160">Request headers:</span></span> 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

<span data-ttu-id="20d58-161">Cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="20d58-161">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a><span data-ttu-id="20d58-162">Eliminar filtros</span><span class="sxs-lookup"><span data-stu-id="20d58-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="20d58-163">Eliminar filtros globales</span><span class="sxs-lookup"><span data-stu-id="20d58-163">Delete global Filters</span></span>
<span data-ttu-id="20d58-164">toodelete un filtro global, utilice Hola siguiendo las solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="20d58-164">toodelete a global Filter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="20d58-165">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="20d58-166">Eliminar AssetFilters locales</span><span class="sxs-lookup"><span data-stu-id="20d58-166">Delete local AssetFilters</span></span>
<span data-ttu-id="20d58-167">toodelete un AssetFilter local, use Hola siguiendo las solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="20d58-167">toodelete a local AssetFilter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="20d58-168">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="20d58-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="20d58-169">Generar direcciones URL de streaming que usan filtros</span><span class="sxs-lookup"><span data-stu-id="20d58-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="20d58-170">Para obtener información sobre cómo toopublish y ofrecer sus activos, consulte [información general de entrega de contenido tooCustomers](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20d58-170">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="20d58-171">Hello en los ejemplos siguientes muestran cómo tooadd filtros tooyour direcciones URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="20d58-171">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="20d58-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="20d58-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="20d58-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="20d58-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="20d58-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="20d58-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="20d58-175">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="20d58-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="20d58-176">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="20d58-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="20d58-177">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="20d58-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="20d58-178">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="20d58-178">See Also</span></span>
[<span data-ttu-id="20d58-179">Información general de manifiestos dinámicos</span><span class="sxs-lookup"><span data-stu-id="20d58-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

