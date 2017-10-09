---
title: directivas de entrega de activos aaaConfigure con .NET SDK | Documentos de Microsoft
description: "Este tema se muestra cómo tooconfigure las directivas de entrega de activos distintas con el SDK de .NET de servicios multimedia de Azure."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="4a9e0-103">Configuración de directivas de entrega de recursos con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="4a9e0-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="4a9e0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4a9e0-104">Overview</span></span>
<span data-ttu-id="4a9e0-105">Si tiene previsto toodelivery cifrado activos, uno de hello pasos Hola servicios multimedia de contenido de flujo de trabajo de entrega es la configuración de directivas de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-105">If you plan toodelivery encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="4a9e0-106">Directiva de entrega del activo de Hello indica los servicios multimedia cómo desea para su toobe asset entregado: en el protocolo de transmisión por secuencias que debe su activo dinámicamente empaquetarse (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos), si no desea toodynamically cifrar un activo y cómo (sobre o cifrado común).</span><span class="sxs-lookup"><span data-stu-id="4a9e0-106">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="4a9e0-107">Este tema se describe cómo y por qué toocreate y configurar directivas de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-107">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="4a9e0-108">Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-108">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="4a9e0-109">toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-109">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="4a9e0-110">Además, puede toouse toobe el empaquetado dinámico y cifrado dinámico su activo debe contener un conjunto de velocidad de bits adaptativa MP4s o archivos de Smooth Streaming de velocidad de bits adaptativa.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-110">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="4a9e0-111">Podría aplicar distintas directivas toohello mismo activo.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-111">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="4a9e0-112">Por ejemplo, podría aplicar PlayReady cifrado tooSmooth transmisión por secuencias y AES Envelope cifrado tooMPEG DASH y HLS.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-112">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="4a9e0-113">Todos los protocolos que no estén definidos en una directiva de entrega (por ejemplo, se agrega una directiva única que solo especifica HLS como protocolo de Hola) se bloqueará de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="4a9e0-114">Hola toothis de excepción es si no tiene definida en absoluto ninguna directiva de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-114">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="4a9e0-115">A continuación, todos los protocolos se permitirá en hello clara.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-115">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="4a9e0-116">Si desea toodeliver un recurso cifrado de almacenamiento, debe configurar la directiva de entrega del activo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-116">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="4a9e0-117">Antes de que se puede transmitir su activo, Hola streaming cifrado de almacenamiento de servidor quita hello y secuencias el contenido con hello especifica directiva de entrega.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-117">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="4a9e0-118">Por ejemplo, toodeliver su activo cifrado con clave de cifrado de sobre estándar de cifrado avanzado (AES), establezca el tipo de directiva de hello demasiado**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-118">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="4a9e0-119">cifrado de almacenamiento de tooremove y los activos de hello secuencia de hello claro, establecer tipo de directiva de hello demasiado**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-119">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="4a9e0-120">Ejemplos que muestran cómo tooconfigure estos tipos de directiva siguen.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-120">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="4a9e0-121">Dependiendo de cómo configurar Directiva de entrega del activo de Hola que podría ser capaz de toodynamically paquete, dinámicamente cifrar y transmitir por hello después de protocolos de transmisión por secuencias: secuencias de Smooth Streaming, HLS y MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-121">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="4a9e0-122">Hello lista siguiente muestra los formatos de Hola que usas toostream Smooth, HLS y DASH.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-122">hello following list shows hello formats that you use toostream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="4a9e0-123">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="4a9e0-123">Smooth Streaming:</span></span>

<span data-ttu-id="4a9e0-124">{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{filename}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="4a9e0-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="4a9e0-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="4a9e0-125">HLS:</span></span>

<span data-ttu-id="4a9e0-126">{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="4a9e0-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="4a9e0-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="4a9e0-127">MPEG DASH</span></span>

<span data-ttu-id="4a9e0-128">{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="4a9e0-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="4a9e0-129">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="4a9e0-129">Considerations</span></span>
* <span data-ttu-id="4a9e0-130">No puede eliminar una entidad AssetDeliveryPolicy asociada a un activo mientras hay un localizador OnDemand (transmisión) para ese activo.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="4a9e0-131">recomendación de Hello es Directiva de hello tooremove de recurso de hello antes de eliminar la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="4a9e0-132">No se puede crear un localizador de transmisión en un activo cifrado de almacenamiento cuando no se establece ninguna directiva de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="4a9e0-133">Si Hola activo no está cifrado de almacenamiento, sistema de hello le permitirán crear un recurso de hello localizador y secuencias en hello claro sin una directiva de entrega del activo.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="4a9e0-134">Puede tener varias directivas de entrega de activos asociadas a un único recurso, pero solo se puede especificar una manera de toohandle un AssetDeliveryProtocol determinado.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="4a9e0-135">Lo que significa que si intenta dos directivas de entrega de toolink especificada por el protocolo de AssetDeliveryProtocol.SmoothStreaming Hola que producirá un error porque el sistema de hello no sabe cuál desea tooapply cuando un cliente realiza una solicitud de transmisión por secuencias suave.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="4a9e0-136">Si tiene un recurso con un localizador de transmisión por secuencias existente, no se puede vincular un nuevo recurso de toohello directiva (puede desvincular una directiva existente de recurso de hello, o actualizar una directiva de entrega asociada Hola activo).</span><span class="sxs-lookup"><span data-stu-id="4a9e0-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset (you can either unlink an existing policy from hello asset, or update a delivery policy associated with hello asset).</span></span>  <span data-ttu-id="4a9e0-137">En primer lugar tiene el localizador de streaming de hello tooremove, ajustar las directivas de hello y, a continuación, volver a crear el localizador de streaming de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="4a9e0-138">Puede usar Hola mismo locatorId se vuelven a crear Hola streaming localizador pero debe asegurarse de que no causará problemas para los clientes ya que puede almacenarse en caché contenido por origen de Hola o de una CDN siguen en la cadena.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="4a9e0-139">Directiva de entrega de recursos sin cifrar</span><span class="sxs-lookup"><span data-stu-id="4a9e0-139">Clear asset delivery policy</span></span>

<span data-ttu-id="4a9e0-140">siguiente Hello **ConfigureClearAssetDeliveryPolicy** método especifica toonot aplicar cifrado dinámico y flujo de hello toodeliver en cualquiera de hello siguiendo los protocolos: protocolos MPEG DASH, HLS y Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-140">hello following **ConfigureClearAssetDeliveryPolicy** method specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="4a9e0-141">Puede ser conveniente tooapply este activos de cifrado de almacenamiento de tooyour de directiva.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-141">You might want tooapply this policy tooyour storage encrypted assets.</span></span>

<span data-ttu-id="4a9e0-142">Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="4a9e0-143">Directiva de entrega de recursos DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="4a9e0-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="4a9e0-144">siguiente Hello **CreateAssetDeliveryPolicy** método crea hello **AssetDeliveryPolicy** que es configurado tooapply comunes cifrado dinámico (**DynamicCommonEncryption**) tooa (se bloqueará otros protocolos de transmisión por secuencias) de protocolo de transmisión por secuencias suave.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-144">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="4a9e0-145">método Hello toma dos parámetros: **Asset** (Hola toowhich asset desea tooapply Hola entrega directiva) y **IContentKey** (clave de contenido de Hola de hello **CommonEncryption**tipo, para obtener más información, consulte: [crear una clave de contenido](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="4a9e0-145">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="4a9e0-146">Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="4a9e0-147">Servicios multimedia de Azure también permite tooadd Widevine cifrado.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-147">Azure Media Services also enables you tooadd Widevine encryption.</span></span> <span data-ttu-id="4a9e0-148">Hello en el ejemplo siguiente se muestra cómo PlayReady y Widevine que se agrega la directiva de entrega del activo de toohello.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-148">hello following example demonstrates both PlayReady and Widevine being added toohello asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get hello PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

        Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
        UriBuilder uriBuilder = new UriBuilder(widevineUrl);
        uriBuilder.Query = String.Empty;
        widevineUrl = uriBuilder.Uri;

        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
        {
            {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="4a9e0-149">Cuando se cifra con Widevine, sólo sería capaz de toodeliver con guión.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-149">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="4a9e0-150">Asegúrese de toospecify seguro guión en el protocolo de entrega de activos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-150">Make sure toospecify DASH in hello asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="4a9e0-151">Directiva de entrega de recursos DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="4a9e0-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="4a9e0-152">siguiente Hello **CreateAssetDeliveryPolicy** método crea hello **AssetDeliveryPolicy** que es el cifrado de sobre dinámico configurado tooapply (**DynamicEnvelopeEncryption** ) tooSmooth protocolos de Streaming, HLS y DASH (si decide toonot especificar algunos protocolos, se bloquearán de transmisión por secuencias).</span><span class="sxs-lookup"><span data-stu-id="4a9e0-152">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) tooSmooth Streaming, HLS, and DASH protocols (if you decide toonot specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="4a9e0-153">método Hello toma dos parámetros: **Asset** (Hola toowhich asset desea tooapply Hola entrega directiva) y **IContentKey** (clave de contenido de Hola de hello **EnvelopeEncryption**tipo, para obtener más información, consulte: [crear una clave de contenido](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="4a9e0-153">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="4a9e0-154">Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
        };

        IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                        "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                        AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);

        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="4a9e0-155"><a id="types"></a>Tipos usados al definir AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="4a9e0-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="4a9e0-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="4a9e0-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="4a9e0-157">Hello enum siguiente describe valores que puede establecer para el protocolo de entrega de activos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-157">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <span data-ttu-id="4a9e0-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="4a9e0-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="4a9e0-159">Hello enum siguiente describe valores que puede establecer para el tipo de directiva de entrega de activos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-159">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <span data-ttu-id="4a9e0-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="4a9e0-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="4a9e0-161">Hello enum siguiente describe valores que puede utilizar el método de entrega de hello tooconfigure de cliente de hello toohello de clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-161">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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

### <span data-ttu-id="4a9e0-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="4a9e0-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="4a9e0-163">Hola después de la enumeración describe valores que puede establecer las claves usadas tooconfigure tooget configuración concreta para una directiva de entrega del activo.</span><span class="sxs-lookup"><span data-stu-id="4a9e0-163">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="4a9e0-164">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="4a9e0-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4a9e0-165">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="4a9e0-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

