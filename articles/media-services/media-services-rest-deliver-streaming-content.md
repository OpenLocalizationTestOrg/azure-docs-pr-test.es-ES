---
title: contenido de servicios multimedia de Azure aaaPublish con REST
description: "Obtenga información acerca de cómo toocreate un localizador de toobuild usa una dirección URL de streaming. código de Hello usa API de REST."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: f849e21b3103b9b33bc652e886b2016ea495b19a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="6c178-104">Publicación de contenido de Servicios multimedia de Azure con REST</span><span class="sxs-lookup"><span data-stu-id="6c178-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c178-105">.NET</span><span class="sxs-lookup"><span data-stu-id="6c178-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="6c178-106">REST</span><span class="sxs-lookup"><span data-stu-id="6c178-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="6c178-107">Portal</span><span class="sxs-lookup"><span data-stu-id="6c178-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="6c178-108">Información general</span><span class="sxs-lookup"><span data-stu-id="6c178-108">Overview</span></span>
<span data-ttu-id="6c178-109">Puede transmitir un conjunto de archivos MP4 de velocidad de bits adaptable creando un localizador de streaming a petición y compilando una dirección URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="6c178-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="6c178-110">Hola [codificar un recurso](media-services-rest-encode-asset.md) tema muestra cómo establece tooencode en una velocidad de bits adaptativa MP4.</span><span class="sxs-lookup"><span data-stu-id="6c178-110">hello [encoding an asset](media-services-rest-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="6c178-111">Si el contenido está cifrado, configure la directiva de entrega de recursos (como se describe en [este](media-services-rest-configure-asset-delivery-policy.md) tema) antes de crear un localizador.</span><span class="sxs-lookup"><span data-stu-id="6c178-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="6c178-112">También puede utilizar un localizador toobuild las direcciones URL que los archivos de punto de tooMP4 se pueden descargar progresivamente de transmisión por secuencias a petición.</span><span class="sxs-lookup"><span data-stu-id="6c178-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="6c178-113">Este tema muestra cómo toocreate un localizador de streaming a petición en orden toopublish su activo y compilar un suave, MPEG DASH y HLS direcciones URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="6c178-113">This topic shows how toocreate an OnDemand streaming locator in order toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="6c178-114">También muestra toobuild activa direcciones URL de descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="6c178-114">It also shows hot toobuild progressive download URLs.</span></span>

<span data-ttu-id="6c178-115">Hola [siguiente](#types) sección muestra hello tipos de enumeración cuyos valores se utilizan en las llamadas REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c178-115">hello [following](#types) section shows hello enum types whose values are used in hello REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="6c178-116">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="6c178-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="6c178-117">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="6c178-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="6c178-118">Conectar servicios de tooMedia</span><span class="sxs-lookup"><span data-stu-id="6c178-118">Connect tooMedia Services</span></span>

<span data-ttu-id="6c178-119">Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="6c178-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="6c178-120">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="6c178-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="6c178-121">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="6c178-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="6c178-122">Creación de un localizador de streaming a petición</span><span class="sxs-lookup"><span data-stu-id="6c178-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="6c178-123">toocreate Hola localizador de streaming a petición y obtener las direcciones URL que necesita hello toodo siguientes:</span><span class="sxs-lookup"><span data-stu-id="6c178-123">toocreate hello OnDemand streaming locator and get URLs you need toodo hello following:</span></span>

1. <span data-ttu-id="6c178-124">Si se cifra el contenido de hello, definir una directiva de acceso.</span><span class="sxs-lookup"><span data-stu-id="6c178-124">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="6c178-125">Cree un localizador de streaming a petición.</span><span class="sxs-lookup"><span data-stu-id="6c178-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="6c178-126">Si tiene previsto toostream, obtener Hola transmisión por secuencias de archivo de manifiesto (.ism) en el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c178-126">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="6c178-127">Si tiene previsto tooprogressively descarga, obtener nombres de Hola de archivos MP4 en activos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c178-127">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span> 
4. <span data-ttu-id="6c178-128">Generar archivo de manifiesto de toohello de direcciones URL o archivos MP4.</span><span class="sxs-lookup"><span data-stu-id="6c178-128">Build URLs toohello manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="6c178-129">Tenga en cuenta que no se puede crear un localizador de transmisión mediante una AccessPolicy que incluye permisos de escritura o eliminación.</span><span class="sxs-lookup"><span data-stu-id="6c178-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="6c178-130">Creación de una directiva de acceso</span><span class="sxs-lookup"><span data-stu-id="6c178-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="6c178-131">Hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="6c178-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="6c178-132">Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / acceso permisos, por ejemplo, las directivas para localizadores que son tooremain previsto en su lugar durante mucho tiempo (directivas no carga).</span><span class="sxs-lookup"><span data-stu-id="6c178-132">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="6c178-133">Para obtener más información, consulte [este tema](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="6c178-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="6c178-134">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="6c178-134">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="6c178-135">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="6c178-135">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 311
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https:/media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3A69c80d98-7830-407f-a9af-e25f4b0d3e5f')
    Server: Microsoft-IIS/8.5
    request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:52:09 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AccessPolicies/@Element","Id":"nb:pid:UUID:69c80d98-7830-407f-a9af-e25f4b0d3e5f","Created":"2015-02-18T06:52:09.8862191Z","LastModified":"2015-02-18T06:52:09.8862191Z","Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="6c178-136">Creación de un localizador de streaming a petición</span><span class="sxs-lookup"><span data-stu-id="6c178-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="6c178-137">Crear el localizador de Hola para activos especificado hello y directiva de recursos.</span><span class="sxs-lookup"><span data-stu-id="6c178-137">Create hello locator for hello specified asset and asset policy.</span></span>

<span data-ttu-id="6c178-138">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="6c178-138">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="6c178-139">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="6c178-139">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 637
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Abe245661-2bbd-4fc6-b14f-9cf9a1492e5e')
    Server: Microsoft-IIS/8.5
    request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:58:37 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#Locators/@Element","Id":"nb:lid:UUID:be245661-2bbd-4fc6-b14f-9cf9a1492e5e","ExpirationDateTime":"2015-03-20T06:34:47.267872+00:00","Type":2,"Path":"http://amstest1.streaming.mediaservices.windows.net/be245661-2bbd-4fc6-b14f-9cf9a1492e5e/","BaseUri":"http://amstest1.streaming.mediaservices.windows.net","ContentAccessComponent":"be245661-2bbd-4fc6-b14f-9cf9a1492e5e","AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872+00:00","Name":null}

### <a name="build-streaming-urls"></a><span data-ttu-id="6c178-140">Creación de direcciones URL de streaming</span><span class="sxs-lookup"><span data-stu-id="6c178-140">Build streaming URLs</span></span>
<span data-ttu-id="6c178-141">Hola de uso **ruta de acceso** valor devuelto después de la creación de hello de Hola Hola de toobuild de localizador Smooth, HLS y las direcciones URL de MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="6c178-141">Use hello **Path** value returned after hello creation of hello locator toobuild hello Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="6c178-142">Smooth Streaming: **Path** + nombre del archivo de manifiesto + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="6c178-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="6c178-143">ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6c178-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="6c178-144">HLS: **Path** + nombre del archivo de manifiesto + "/manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="6c178-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="6c178-145">ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6c178-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="6c178-146">DASH: **Path** + nombre del archivo de manifiesto + "/manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="6c178-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="6c178-147">ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6c178-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="6c178-148">Creación de direcciones URL de descarga progresiva</span><span class="sxs-lookup"><span data-stu-id="6c178-148">Build progressive download URLs</span></span>
<span data-ttu-id="6c178-149">Hola de uso **ruta de acceso** valor devuelto después de la creación de hello de dirección URL de la descarga progresiva de hello localizador toobuild Hola.</span><span class="sxs-lookup"><span data-stu-id="6c178-149">Use hello **Path** value returned after hello creation of hello locator toobuild hello progressive download URL.</span></span>   

<span data-ttu-id="6c178-150">URL: **Path** + nombre del archivo mp4 de recursos</span><span class="sxs-lookup"><span data-stu-id="6c178-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="6c178-151">ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6c178-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="6c178-152"><a id="types"></a>Tipos de enumeración</span><span class="sxs-lookup"><span data-stu-id="6c178-152"><a id="types"></a>Enum types</span></span>
    [Flags]
    public enum AccessPermissions
    {
        None = 0,
        Read = 1,
        Write = 2,
        Delete = 4,
        List = 8,
    }

    public enum LocatorType
    {
        None = 0,
        Sas = 1,
        OnDemandOrigin = 2,
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="6c178-153">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="6c178-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6c178-154">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="6c178-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6c178-155">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="6c178-155">See also</span></span>
[<span data-ttu-id="6c178-156">Información general sobre la API de REST de operaciones de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="6c178-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="6c178-157">Configuración de directivas de entrega de activos</span><span class="sxs-lookup"><span data-stu-id="6c178-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

