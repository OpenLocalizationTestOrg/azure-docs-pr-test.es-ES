---
title: directivas de entrega de activos aaaConfiguring mediante API de REST de servicios multimedia | Documentos de Microsoft
description: "Este tema se muestra cómo las directivas de entrega de activos distintas tooconfigure mediante la API de REST de servicios multimedia."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="a2c38-103">Configuración de directivas de entrega de recursos</span><span class="sxs-lookup"><span data-stu-id="a2c38-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="a2c38-104">Si tiene previsto toodeliver dinámicamente cifrada activos, uno de hello pasos Hola servicios multimedia de contenido de flujo de trabajo de entrega es la configuración de directivas de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="a2c38-104">If you plan toodeliver dynamically encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="a2c38-105">Directiva de entrega del activo de Hello indica los servicios multimedia cómo desea para su toobe asset entregado: en el protocolo de transmisión por secuencias que debe su activo dinámicamente empaquetarse (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos), si no desea toodynamically cifrar un activo y cómo (sobre o cifrado común).</span><span class="sxs-lookup"><span data-stu-id="a2c38-105">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="a2c38-106">Este tema se describe cómo y por qué toocreate y configurar directivas de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="a2c38-106">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="a2c38-107">Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado.</span><span class="sxs-lookup"><span data-stu-id="a2c38-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="a2c38-108">toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="a2c38-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="a2c38-109">Además, puede toouse toobe el empaquetado dinámico y cifrado dinámico su activo debe contener un conjunto de velocidad de bits adaptativa MP4s o archivos de Smooth Streaming de velocidad de bits adaptativa.</span><span class="sxs-lookup"><span data-stu-id="a2c38-109">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="a2c38-110">Podría aplicar distintas directivas toohello mismo activo.</span><span class="sxs-lookup"><span data-stu-id="a2c38-110">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="a2c38-111">Por ejemplo, podría aplicar PlayReady cifrado tooSmooth transmisión por secuencias y AES Envelope cifrado tooMPEG DASH y HLS.</span><span class="sxs-lookup"><span data-stu-id="a2c38-111">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="a2c38-112">Todos los protocolos que no estén definidos en una directiva de entrega (por ejemplo, se agrega una directiva única que solo especifica HLS como protocolo de Hola) se bloqueará de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="a2c38-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="a2c38-113">Hola toothis de excepción es si no tiene definida en absoluto ninguna directiva de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="a2c38-113">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="a2c38-114">A continuación, todos los protocolos se permitirá en hello clara.</span><span class="sxs-lookup"><span data-stu-id="a2c38-114">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="a2c38-115">Si desea toodeliver un recurso cifrado de almacenamiento, debe configurar la directiva de entrega del activo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2c38-115">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="a2c38-116">Antes de que se puede transmitir su activo, Hola streaming cifrado de almacenamiento de servidor quita hello y secuencias el contenido con hello especifica directiva de entrega.</span><span class="sxs-lookup"><span data-stu-id="a2c38-116">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="a2c38-117">Por ejemplo, toodeliver su activo cifrado con clave de cifrado de sobre estándar de cifrado avanzado (AES), establezca el tipo de directiva de hello demasiado**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="a2c38-117">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="a2c38-118">cifrado de almacenamiento de tooremove y los activos de hello secuencia de hello claro, establecer tipo de directiva de hello demasiado**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="a2c38-118">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="a2c38-119">Ejemplos que muestran cómo tooconfigure estos tipos de directiva siguen.</span><span class="sxs-lookup"><span data-stu-id="a2c38-119">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="a2c38-120">Dependiendo de cómo configurar Directiva de entrega del activo de Hola que podría ser capaz de toodynamically paquete, dinámicamente cifrar y transmitir por hello después de protocolos de transmisión por secuencias: Smooth Streaming, HLS, secuencias de MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="a2c38-120">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="a2c38-121">Hola siguiente lista muestra hello da formato a usar toostream Smooth, HLS, guión.</span><span class="sxs-lookup"><span data-stu-id="a2c38-121">hello following list shows hello formats that you use toostream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="a2c38-122">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="a2c38-122">Smooth Streaming:</span></span>

<span data-ttu-id="a2c38-123">{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{filename}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="a2c38-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="a2c38-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="a2c38-124">HLS:</span></span>

<span data-ttu-id="a2c38-125">{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="a2c38-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="a2c38-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="a2c38-126">MPEG DASH</span></span>

<span data-ttu-id="a2c38-127">{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="a2c38-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="a2c38-128">Para obtener instrucciones sobre cómo toopublish un activo y generar una dirección URL de streaming, vea [generar una dirección URL de streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="a2c38-128">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="a2c38-129">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="a2c38-129">Considerations</span></span>
* <span data-ttu-id="a2c38-130">No puede eliminar una entidad AssetDeliveryPolicy asociada a un activo mientras hay un localizador OnDemand (transmisión) para ese activo.</span><span class="sxs-lookup"><span data-stu-id="a2c38-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="a2c38-131">recomendación de Hello es Directiva de hello tooremove de recurso de hello antes de eliminar la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2c38-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="a2c38-132">No se puede crear un localizador de transmisión en un activo cifrado de almacenamiento cuando no se establece ninguna directiva de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="a2c38-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="a2c38-133">Si Hola activo no está cifrado de almacenamiento, sistema de hello le permitirán crear un recurso de hello localizador y secuencias en hello claro sin una directiva de entrega del activo.</span><span class="sxs-lookup"><span data-stu-id="a2c38-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="a2c38-134">Puede tener varias directivas de entrega de activos asociadas a un único recurso, pero solo se puede especificar una manera de toohandle un AssetDeliveryProtocol determinado.</span><span class="sxs-lookup"><span data-stu-id="a2c38-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="a2c38-135">Lo que significa que si intenta dos directivas de entrega de toolink especificada por el protocolo de AssetDeliveryProtocol.SmoothStreaming Hola que producirá un error porque el sistema de hello no sabe cuál desea tooapply cuando un cliente realiza una solicitud de transmisión por secuencias suave.</span><span class="sxs-lookup"><span data-stu-id="a2c38-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="a2c38-136">Si tiene un recurso con un localizador de transmisión por secuencias existente, no se puede vincular un nuevo recurso toohello de directiva, desvincular una directiva existente de recurso de Hola o actualizar una directiva de entrega asociada Hola activo.</span><span class="sxs-lookup"><span data-stu-id="a2c38-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset, unlink an existing policy from hello asset, or update a delivery policy associated with hello asset.</span></span>  <span data-ttu-id="a2c38-137">En primer lugar tiene el localizador de streaming de hello tooremove, ajustar las directivas de hello y, a continuación, volver a crear el localizador de streaming de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2c38-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="a2c38-138">Puede usar Hola mismo locatorId se vuelven a crear Hola streaming localizador pero debe asegurarse de que no causará problemas para los clientes ya que puede almacenarse en caché contenido por origen de Hola o de una CDN siguen en la cadena.</span><span class="sxs-lookup"><span data-stu-id="a2c38-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="a2c38-139">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="a2c38-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a2c38-140">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a2c38-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="a2c38-141">Conectar servicios de tooMedia</span><span class="sxs-lookup"><span data-stu-id="a2c38-141">Connect tooMedia Services</span></span>

<span data-ttu-id="a2c38-142">Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a2c38-142">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="a2c38-143">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="a2c38-143">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a2c38-144">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="a2c38-144">You must make subsequent calls toohello new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="a2c38-145">Directiva de entrega de recursos sin cifrar</span><span class="sxs-lookup"><span data-stu-id="a2c38-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="a2c38-146"><a id="create_asset_delivery_policy"></a>Creación de directiva de entrega de recursos</span><span class="sxs-lookup"><span data-stu-id="a2c38-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="a2c38-147">Hello solicitud HTTP siguiente crea una directiva de entrega de activos que especifica toonot aplicar cifrado dinámico y flujo de hello toodeliver en cualquiera de hello siguiendo los protocolos: protocolos MPEG DASH, HLS y Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="a2c38-147">hello following HTTP request creates an asset delivery policy that specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="a2c38-148">Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.</span><span class="sxs-lookup"><span data-stu-id="a2c38-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="a2c38-149">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="a2c38-149">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

<span data-ttu-id="a2c38-150">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="a2c38-150">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <span data-ttu-id="a2c38-151"><a id="link_asset_with_asset_delivery_policy"></a>Vinculación de un recurso con la directiva de entrega de recursos</span><span class="sxs-lookup"><span data-stu-id="a2c38-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="a2c38-152">Hola después Hola de vínculos de solicitud HTTP especifica directiva de entrega de activos toohello activo a.</span><span class="sxs-lookup"><span data-stu-id="a2c38-152">hello following HTTP request links hello specified asset toohello asset delivery policy to.</span></span>

<span data-ttu-id="a2c38-153">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="a2c38-153">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

<span data-ttu-id="a2c38-154">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="a2c38-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="a2c38-155">Directiva de entrega de recursos DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="a2c38-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="a2c38-156">Crear clave de contenido del tipo de EnvelopeEncryption de Hola y vincularlo toohello activo</span><span class="sxs-lookup"><span data-stu-id="a2c38-156">Create content key of hello EnvelopeEncryption type and link it toohello asset</span></span>
<span data-ttu-id="a2c38-157">Al especificar la directiva de entrega DynamicEnvelopeEncryption, deberá toomake seguro toolink la clave de contenido activo tooa de hello EnvelopeEncryption tipo.</span><span class="sxs-lookup"><span data-stu-id="a2c38-157">When specifying DynamicEnvelopeEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello EnvelopeEncryption type.</span></span> <span data-ttu-id="a2c38-158">Para obtener más información, consulte [Creación de una clave de contenido](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="a2c38-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="a2c38-159"><a id="get_delivery_url"></a>Obtención de una dirección URL de entrega</span><span class="sxs-lookup"><span data-stu-id="a2c38-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="a2c38-160">Dirección URL de entrega de Get hello para hello especifica método de entrega de clave de contenido de hello creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2c38-160">Get hello delivery URL for hello specified delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="a2c38-161">Un cliente usa Hola devuelve la dirección URL toorequest contenido protegido de una clave de AES o una licencia de PlayReady en hello tooplayback de orden.</span><span class="sxs-lookup"><span data-stu-id="a2c38-161">A client uses hello returned URL toorequest an AES key or a PlayReady license in order tooplayback hello protected content.</span></span>

<span data-ttu-id="a2c38-162">Especificar tipo de Hola de hello tooget de dirección URL en el cuerpo de saludo de solicitud HTTP de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2c38-162">Specify hello type of hello URL tooget in hello body of hello HTTP request.</span></span> <span data-ttu-id="a2c38-163">Si va a proteger el contenido con PlayReady, solicite una dirección URL de adquisición de licencias de PlayReady de servicios multimedia, con 1 para hello keyDeliveryType: {"keyDeliveryType": 1}.</span><span class="sxs-lookup"><span data-stu-id="a2c38-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for hello keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="a2c38-164">Si va a proteger su contenido con el cifrado de sellado hello, solicite una dirección URL de adquisición de claves especificando 2 para keyDeliveryType: {"keyDeliveryType": 2}.</span><span class="sxs-lookup"><span data-stu-id="a2c38-164">If you are protecting your content with hello envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="a2c38-165">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="a2c38-165">Request:</span></span>

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

<span data-ttu-id="a2c38-166">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="a2c38-166">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="a2c38-167">Creación de directiva de entrega de recursos</span><span class="sxs-lookup"><span data-stu-id="a2c38-167">Create asset delivery policy</span></span>
<span data-ttu-id="a2c38-168">solicitud HTTP siguiente Hello crea hello **AssetDeliveryPolicy** que es el cifrado de sobre dinámico configurado tooapply (**DynamicEnvelopeEncryption**) toohello **HLS**protocolo (en este ejemplo, otros protocolos se bloqueará de transmisión por secuencias).</span><span class="sxs-lookup"><span data-stu-id="a2c38-168">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) toohello **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="a2c38-169">Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.</span><span class="sxs-lookup"><span data-stu-id="a2c38-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="a2c38-170">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="a2c38-170">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


<span data-ttu-id="a2c38-171">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="a2c38-171">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="a2c38-172">Vinculación de un recurso con la directiva de entrega de recursos</span><span class="sxs-lookup"><span data-stu-id="a2c38-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="a2c38-173">Consulte [Vinculación de un recurso con la directiva de entrega de recursos](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="a2c38-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="a2c38-174">Directiva de entrega de recursos DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="a2c38-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="a2c38-175">Crear clave de contenido del tipo de hello CommonEncryption y vincularlo toohello activo</span><span class="sxs-lookup"><span data-stu-id="a2c38-175">Create content key of hello CommonEncryption type and link it toohello asset</span></span>
<span data-ttu-id="a2c38-176">Al especificar la directiva de entrega DynamicCommonEncryption, deberá toomake seguro toolink la clave de contenido activo tooa de hello CommonEncryption tipo.</span><span class="sxs-lookup"><span data-stu-id="a2c38-176">When specifying DynamicCommonEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello CommonEncryption type.</span></span> <span data-ttu-id="a2c38-177">Para obtener más información, consulte [Creación de una clave de contenido](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="a2c38-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="a2c38-178">Obtención de una dirección URL de entrega</span><span class="sxs-lookup"><span data-stu-id="a2c38-178">Get Delivery URL</span></span>
<span data-ttu-id="a2c38-179">Obtener dirección URL de entrega de Hola Hola PlayReady método de entrega de clave de contenido de hello creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2c38-179">Get hello delivery URL for hello PlayReady delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="a2c38-180">Un cliente usa Hola devuelve contenido protegida de una licencia de PlayReady en hello tooplayback de orden de toorequest de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="a2c38-180">A client uses hello returned URL toorequest a PlayReady license in order tooplayback hello protected content.</span></span> <span data-ttu-id="a2c38-181">Para obtener más información, consulte [Obtención de una dirección URL de entrega](#get_delivery_url)</span><span class="sxs-lookup"><span data-stu-id="a2c38-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="a2c38-182">Creación de directiva de entrega de recursos</span><span class="sxs-lookup"><span data-stu-id="a2c38-182">Create asset delivery policy</span></span>
<span data-ttu-id="a2c38-183">solicitud HTTP siguiente Hello crea hello **AssetDeliveryPolicy** que es configurado tooapply comunes cifrado dinámico (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protocolo (en este ejemplo, otros protocolos se bloqueará de transmisión por secuencias).</span><span class="sxs-lookup"><span data-stu-id="a2c38-183">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="a2c38-184">Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.</span><span class="sxs-lookup"><span data-stu-id="a2c38-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="a2c38-185">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="a2c38-185">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


<span data-ttu-id="a2c38-186">Si desea que el contenido con DRM Widevine tooprotect, actualizar hello AssetDeliveryConfiguration valores toouse WidevineLicenseAcquisitionUrl (que tiene el valor de Hola de 7) y especificar dirección URL de Hola de un servicio de entrega de licencia.</span><span class="sxs-lookup"><span data-stu-id="a2c38-186">If you want tooprotect your content using Widevine DRM, update hello AssetDeliveryConfiguration values toouse WidevineLicenseAcquisitionUrl (which has hello value of 7) and specify hello URL of a license delivery service.</span></span> <span data-ttu-id="a2c38-187">Puede usar Hola después AMS socios toohelp entregar licencias de Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="a2c38-187">You can use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="a2c38-188">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a2c38-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="a2c38-189">Cuando se cifra con Widevine, sólo sería capaz de toodeliver con guión.</span><span class="sxs-lookup"><span data-stu-id="a2c38-189">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="a2c38-190">Asegúrese de protocolo de entrega de seguro toospecify guión (2) hello en activo.</span><span class="sxs-lookup"><span data-stu-id="a2c38-190">Make sure toospecify DASH (2) in hello asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="a2c38-191">Vinculación de un recurso con la directiva de entrega de recursos</span><span class="sxs-lookup"><span data-stu-id="a2c38-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="a2c38-192">Consulte [Vinculación de un recurso con la directiva de entrega de recursos](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="a2c38-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="a2c38-193"><a id="types"></a>Tipos usados al definir AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="a2c38-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="a2c38-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="a2c38-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="a2c38-195">Hello enum siguiente describe valores que puede establecer para el protocolo de entrega de activos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2c38-195">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="a2c38-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="a2c38-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="a2c38-197">Hello enum siguiente describe valores que puede establecer para el tipo de directiva de entrega de activos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2c38-197">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a><span data-ttu-id="a2c38-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="a2c38-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="a2c38-199">Hello enum siguiente describe valores que puede utilizar el método de entrega de hello tooconfigure de cliente de hello toohello de clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="a2c38-199">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="a2c38-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="a2c38-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="a2c38-201">Hola después de la enumeración describe valores que puede establecer las claves usadas tooconfigure tooget configuración concreta para una directiva de entrega del activo.</span><span class="sxs-lookup"><span data-stu-id="a2c38-201">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="a2c38-202">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="a2c38-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a2c38-203">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="a2c38-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

