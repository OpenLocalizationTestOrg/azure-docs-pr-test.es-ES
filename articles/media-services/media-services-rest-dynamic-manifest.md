---
title: "Creación de filtros con la API de REST de Azure Media Services | Microsoft Docs"
description: "En este tema se describe cómo crear filtros para que su cliente pueda usarlos para el streaming de secciones específicas de una transmisión. Servicios multimedia crea manifiestos dinámicos para lograr este streaming selectivo."
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
ms.openlocfilehash: 76d2721138668d9f0a908af3fa42840309b068ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="34e31-104">Creación de filtros con la API de REST de Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="34e31-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34e31-105">.NET</span><span class="sxs-lookup"><span data-stu-id="34e31-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="34e31-106">REST</span><span class="sxs-lookup"><span data-stu-id="34e31-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="34e31-107">A partir de la versión 2.11, los Servicios multimedia permiten definir filtros para los activos.</span><span class="sxs-lookup"><span data-stu-id="34e31-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="34e31-108">Estos filtros son reglas del lado servidor que permitirán a los clientes elegir realizar acciones como: reproducir solo una sección de un vídeo (en lugar de reproducir el vídeo completo), o especificar solo un subconjunto de las representaciones de audio y vídeo que el dispositivo de su cliente puede controlar (en lugar de todas las copias asociadas al activo).</span><span class="sxs-lookup"><span data-stu-id="34e31-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="34e31-109">Este filtrado de sus activos se archiva a través de los **manifiestos dinámicos**que se crean tras la solicitud del cliente para transmitir un vídeo en función de los filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="34e31-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="34e31-110">Para obtener más información detallada relacionada con filtros y manifiesto dinámico, vea [Información general de manifiesto dinámico](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34e31-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="34e31-111">En este tema se muestra cómo usar las API de REST para crear, actualizar y eliminar filtros.</span><span class="sxs-lookup"><span data-stu-id="34e31-111">This topic shows how to use REST APIs to create, update, and delete filters.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="34e31-112">Tipos usados para crear filtros</span><span class="sxs-lookup"><span data-stu-id="34e31-112">Types used to create filters</span></span>
<span data-ttu-id="34e31-113">Al crear filtros, se usan los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="34e31-113">The following types are used when creating filters:</span></span>  

* [<span data-ttu-id="34e31-114">Filter</span><span class="sxs-lookup"><span data-stu-id="34e31-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="34e31-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="34e31-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="34e31-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="34e31-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="34e31-117">FilterTrackSelect y FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="34e31-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="34e31-118">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="34e31-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="34e31-119">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="34e31-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="34e31-120">Conexión con Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="34e31-120">Connect to Media Services</span></span>

<span data-ttu-id="34e31-121">Para obtener más información sobre cómo conectarse a la API de Azure Media Services, consulte [Acceso a la API de Azure Media Services con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="34e31-121">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="34e31-122">Después de conectarse correctamente a https://media.windows.net, recibirá una redirección 301 que especifica otro URI de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="34e31-122">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="34e31-123">Debe realizar las llamadas posteriores al nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="34e31-123">You must make subsequent calls to the new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="34e31-124">Crear filtros</span><span class="sxs-lookup"><span data-stu-id="34e31-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="34e31-125">Crear filtros globales</span><span class="sxs-lookup"><span data-stu-id="34e31-125">Create global Filters</span></span>
<span data-ttu-id="34e31-126">Para crear un filtro global, use las siguientes solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="34e31-126">To create a global Filter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="34e31-127">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-127">HTTP Request</span></span>
<span data-ttu-id="34e31-128">Encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="34e31-128">Request Headers</span></span>

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

<span data-ttu-id="34e31-129">Request body</span><span class="sxs-lookup"><span data-stu-id="34e31-129">Request body</span></span> 

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




#### <a name="http-response"></a><span data-ttu-id="34e31-130">Respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="34e31-131">Crear AssetFilters locales</span><span class="sxs-lookup"><span data-stu-id="34e31-131">Create local AssetFilters</span></span>
<span data-ttu-id="34e31-132">Para crear un AssetFilter local, use las siguientes solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="34e31-132">To create a local AssetFilter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="34e31-133">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-133">HTTP Request</span></span>
<span data-ttu-id="34e31-134">Encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="34e31-134">Request Headers</span></span>

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

<span data-ttu-id="34e31-135">Request body</span><span class="sxs-lookup"><span data-stu-id="34e31-135">Request body</span></span> 

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

#### <a name="http-response"></a><span data-ttu-id="34e31-136">Respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="34e31-137">Enumerar filtros</span><span class="sxs-lookup"><span data-stu-id="34e31-137">List filters</span></span>
### <a name="get-all-global-filters-in-the-ams-account"></a><span data-ttu-id="34e31-138">Obtener todos los **filtro**s globales en la cuenta de AMS</span><span class="sxs-lookup"><span data-stu-id="34e31-138">Get all global **Filter**s in the AMS account</span></span>
<span data-ttu-id="34e31-139">Para enumerar filtros, use las siguientes solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="34e31-139">To list filters, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="34e31-140">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="34e31-141">Obtener **AssetFilter**s asociados a un recurso</span><span class="sxs-lookup"><span data-stu-id="34e31-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="34e31-142">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="34e31-143">Obtener un **AssetFilter** según su id.</span><span class="sxs-lookup"><span data-stu-id="34e31-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="34e31-144">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="34e31-145">Actualizar filtros</span><span class="sxs-lookup"><span data-stu-id="34e31-145">Update filters</span></span>
<span data-ttu-id="34e31-146">Use PATCH, PUT o MERGE para actualizar un filtro con nuevos valores de propiedad.</span><span class="sxs-lookup"><span data-stu-id="34e31-146">Use PATCH, PUT or MERGE to update a filter with new property values.</span></span>  <span data-ttu-id="34e31-147">Para obtener más información acerca de estas operaciones, vea [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="34e31-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="34e31-148">Si actualiza un filtro, se pueden tardar hasta 2 minutos en que el extremo de streaming actualice las reglas.</span><span class="sxs-lookup"><span data-stu-id="34e31-148">If you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="34e31-149">Si el contenido se proporcionó con este filtro (y se almacenó en caché en los servidores proxy y cachés de CDN), la actualización de este filtro puede generar errores del reproductor.</span><span class="sxs-lookup"><span data-stu-id="34e31-149">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="34e31-150">Se recomienda borrar la memoria caché después de actualizar el filtro.</span><span class="sxs-lookup"><span data-stu-id="34e31-150">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="34e31-151">Si esta opción no es posible, piense en usar un filtro diferente.</span><span class="sxs-lookup"><span data-stu-id="34e31-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="34e31-152">Actualizar los filtros globales</span><span class="sxs-lookup"><span data-stu-id="34e31-152">Update global Filters</span></span>
<span data-ttu-id="34e31-153">Para actualizar un filtro global, use las siguientes solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="34e31-153">To update a global filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="34e31-154">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-154">HTTP Request</span></span>
<span data-ttu-id="34e31-155">Encabezados de solicitud:</span><span class="sxs-lookup"><span data-stu-id="34e31-155">Request headers:</span></span> 

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

<span data-ttu-id="34e31-156">Cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="34e31-156">Request body:</span></span> 

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

### <a name="update-local-assetfilters"></a><span data-ttu-id="34e31-157">Actualización de AssetFilters locales</span><span class="sxs-lookup"><span data-stu-id="34e31-157">Update local AssetFilters</span></span>
<span data-ttu-id="34e31-158">Para actualizar un filtro local, use las siguientes solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="34e31-158">To update a local filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="34e31-159">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-159">HTTP Request</span></span>
<span data-ttu-id="34e31-160">Encabezados de solicitud:</span><span class="sxs-lookup"><span data-stu-id="34e31-160">Request headers:</span></span> 

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

<span data-ttu-id="34e31-161">Cuerpo de la solicitud:</span><span class="sxs-lookup"><span data-stu-id="34e31-161">Request body:</span></span> 

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


## <a name="delete-filters"></a><span data-ttu-id="34e31-162">Eliminar filtros</span><span class="sxs-lookup"><span data-stu-id="34e31-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="34e31-163">Eliminar filtros globales</span><span class="sxs-lookup"><span data-stu-id="34e31-163">Delete global Filters</span></span>
<span data-ttu-id="34e31-164">Para eliminar un filtro local, use las siguientes solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="34e31-164">To delete a global Filter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="34e31-165">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="34e31-166">Eliminar AssetFilters locales</span><span class="sxs-lookup"><span data-stu-id="34e31-166">Delete local AssetFilters</span></span>
<span data-ttu-id="34e31-167">Para eliminar un AssetFilter local, use las siguientes solicitudes HTTP:</span><span class="sxs-lookup"><span data-stu-id="34e31-167">To delete a local AssetFilter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="34e31-168">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="34e31-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="34e31-169">Generar direcciones URL de streaming que usan filtros</span><span class="sxs-lookup"><span data-stu-id="34e31-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="34e31-170">Para obtener información sobre cómo publicar y entregar los activos, vea [Información general de entrega de contenido a clientes](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34e31-170">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="34e31-171">En los ejemplos siguientes se muestra cómo agregar filtros a sus URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="34e31-171">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="34e31-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="34e31-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="34e31-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="34e31-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="34e31-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="34e31-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="34e31-175">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="34e31-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="34e31-176">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="34e31-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="34e31-177">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="34e31-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="34e31-178">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="34e31-178">See Also</span></span>
[<span data-ttu-id="34e31-179">Información general de manifiestos dinámicos</span><span class="sxs-lookup"><span data-stu-id="34e31-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)
