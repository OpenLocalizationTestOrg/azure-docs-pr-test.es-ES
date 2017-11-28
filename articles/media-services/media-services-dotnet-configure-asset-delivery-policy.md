---
title: "Configuración de directivas de entrega de recursos con el SDK de .NET | Microsoft Docs"
description: "En este tema se muestra cómo configurar distintas directivas de entrega de recursos con .NET SDK de Servicios multimedia de Azure."
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
ms.openlocfilehash: 282fd9e24dc147e31613469926128894d48366f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="bf5f6-103">Configuración de directivas de entrega de recursos con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bf5f6-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="bf5f6-104">Información general</span><span class="sxs-lookup"><span data-stu-id="bf5f6-104">Overview</span></span>
<span data-ttu-id="bf5f6-105">Si tiene pensado entregar activos cifrados, uno de los pasos del flujo de trabajo de entrega de contenido de Servicios multimedia consiste en configurar directivas de entrega para los activos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-105">If you plan to delivery encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="bf5f6-106">La directiva de entrega de recursos indica a los Servicios multimedia cómo desea usted que se entregue el recurso: en qué protocolo de streaming se debe empaquetar de forma dinámica el recurso (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos) o si desea o no cifrar de forma dinámica el recurso y de qué manera (cifrado de sobre o común).</span><span class="sxs-lookup"><span data-stu-id="bf5f6-106">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="bf5f6-107">En este tema se explica por qué y cómo crear y configurar directivas de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-107">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="bf5f6-108">Cuando se crea la cuenta de AMS, se agrega un punto de conexión de streaming **predeterminado** a la cuenta en estado **Stopped** (Detenido).</span><span class="sxs-lookup"><span data-stu-id="bf5f6-108">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="bf5f6-109">Para iniciar la transmisión del contenido y aprovechar el empaquetado dinámico y el cifrado dinámico, el punto de conexión de streaming desde el que va a transmitir el contenido debe estar en estado **Running** (En ejecución).</span><span class="sxs-lookup"><span data-stu-id="bf5f6-109">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="bf5f6-110">Además, para poder usar el empaquetado dinámico y el cifrado dinámico, el recurso debe contener un conjunto de archivos MP4 de velocidad de bits adaptable o archivos Smooth Streaming de velocidad de bits adaptable.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-110">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="bf5f6-111">Puede aplicar diferentes directivas al mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-111">You could apply different policies to the same asset.</span></span> <span data-ttu-id="bf5f6-112">Por ejemplo, puede aplicar cifrado PlayReady a Smooth Streaming y cifrado de sobre AES a MPEG DASH y HLS.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-112">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="bf5f6-113">Se bloqueará la transmisión para todos los protocolos que no estén definidos en una directiva de entrega (por ejemplo, si agrega una sola directiva que solo especifica HLS como el protocolo).</span><span class="sxs-lookup"><span data-stu-id="bf5f6-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="bf5f6-114">La excepción a esta regla se produce en el caso de que no haya definido ninguna directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-114">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="bf5f6-115">En tal caso, todos los protocolos estarán habilitados sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-115">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="bf5f6-116">Si desea entregar un recurso de almacenamiento cifrado, debe configurar la directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-116">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="bf5f6-117">Antes de poder transmitir el recurso, el servidor de streaming quita el cifrado de almacenamiento y transmite el contenido usando la directiva de entrega especificada.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-117">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="bf5f6-118">Por ejemplo, para entregar el recurso cifrado con la clave de cifrado de sobre de Estándar de cifrado avanzado (AES), establezca el tipo de directiva en **DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-118">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="bf5f6-119">Para quitar el cifrado de almacenamiento y transmitir el recurso sin cifrar, establezca el tipo de directiva en **NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-119">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="bf5f6-120">A continuación se muestran ejemplos de configuración de estos tipos de directiva.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-120">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="bf5f6-121">Según cómo configure la directiva de entrega de recursos podrá realizar el empaquetamiento de forma dinámica, cifrar de forma dinámica y hacer streaming de los protocolos de streaming siguientes: secuencias Smooth Streaming, HLS y MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-121">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="bf5f6-122">En la lista siguiente se muestran los formatos usados para transmitir Smooth Streaming, HLS y DASH.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-122">The following list shows the formats that you use to stream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="bf5f6-123">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="bf5f6-123">Smooth Streaming:</span></span>

<span data-ttu-id="bf5f6-124">{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{filename}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="bf5f6-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="bf5f6-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="bf5f6-125">HLS:</span></span>

<span data-ttu-id="bf5f6-126">{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="bf5f6-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="bf5f6-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="bf5f6-127">MPEG DASH</span></span>

<span data-ttu-id="bf5f6-128">{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="bf5f6-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="bf5f6-129">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="bf5f6-129">Considerations</span></span>
* <span data-ttu-id="bf5f6-130">No puede eliminar una entidad AssetDeliveryPolicy asociada a un activo mientras hay un localizador OnDemand (transmisión) para ese activo.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="bf5f6-131">Se recomienda quitar la directiva del activo antes de eliminar la directiva.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="bf5f6-132">No se puede crear un localizador de transmisión en un activo cifrado de almacenamiento cuando no se establece ninguna directiva de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="bf5f6-133">Si el activo no está cifrado para almacenamiento, el sistema le permitirá crear un localizador y transmitir el activo sin cifrar, sin una directiva de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="bf5f6-134">Puede tener varias directivas de entrega de activos asociadas a un único activo, pero solo se puede especificar una forma de controlar un AssetDeliveryProtocol determinado,</span><span class="sxs-lookup"><span data-stu-id="bf5f6-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="bf5f6-135">es decir, si intenta vincular dos directivas de entrega que especifican el protocolo AssetDeliveryProtocol.SmoothStreaming que producirá un error porque el sistema no sabe cuál quiere que aplique cuando un cliente realiza una solicitud de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="bf5f6-136">Si tiene un activo con un localizador de transmisión existente, no puede vincular una nueva directiva al activo (puede desvincular una directiva existente del activo o actualizar una directiva de entrega asociada al activo).</span><span class="sxs-lookup"><span data-stu-id="bf5f6-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset (you can either unlink an existing policy from the asset, or update a delivery policy associated with the asset).</span></span>  <span data-ttu-id="bf5f6-137">Primero debe quitar el localizador de transmisión, ajustar las directivas y volver a crear el localizador de transmisión.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="bf5f6-138">Puede usar el mismo locatorId al volver a crear el localizador de transmisión, pero debe asegurarse de que no causará problemas para los clientes ya que se puede almacenar en caché el contenido por el origen o una red CDN de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="bf5f6-139">Directiva de entrega de recursos sin cifrar</span><span class="sxs-lookup"><span data-stu-id="bf5f6-139">Clear asset delivery policy</span></span>

<span data-ttu-id="bf5f6-140">El método **ConfigureClearAssetDeliveryPolicy** siguiente especifica que no se aplique el cifrado dinámico y se entregue la transmisión en cualquiera de los siguientes protocolos: MPEG DASH, HLS y Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-140">The following **ConfigureClearAssetDeliveryPolicy** method specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="bf5f6-141">Querrá aplicar esta directiva a los activos cifrados de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-141">You might want to apply this policy to your storage encrypted assets.</span></span>

<span data-ttu-id="bf5f6-142">Para obtener información sobre los valores que puede especificar al crear una entidad AssetDeliveryPolicy, consulte la sección [Tipos usados al definir AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="bf5f6-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="bf5f6-143">Directiva de entrega de recursos DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="bf5f6-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="bf5f6-144">El método siguiente **CreateAssetDeliveryPolicy** crea la entidad **AssetDeliveryPolicy** que se configura para aplicar el cifrado común dinámico (**DynamicCommonEncryption**) a un protocolo de streaming con velocidad de transmisión adaptable (se bloqueará el streaming para otros protocolos).</span><span class="sxs-lookup"><span data-stu-id="bf5f6-144">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to a smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="bf5f6-145">El método toma dos parámetros: **Asset** (el recurso al que desea aplicar la directiva de entrega) e **IContentKey** (la clave de contenido de tipo **CommonEncryption**. Para más información, consulte [Creación de una clave de contenido](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="bf5f6-145">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="bf5f6-146">Para obtener información sobre los valores que puede especificar al crear una entidad AssetDeliveryPolicy, consulte la sección [Tipos usados al definir AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="bf5f6-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

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
    
            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="bf5f6-147">Los Servicios multimedia de Azure también permiten agregar el cifrado de Widevine.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-147">Azure Media Services also enables you to add Widevine encryption.</span></span> <span data-ttu-id="bf5f6-148">En el ejemplo siguiente se muestra cómo se agrega tanto PlayReady como Widevine a la directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-148">The following example demonstrates both PlayReady and Widevine being added to the asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get the PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // to append /? KID =< keyId > to the end of the url when creating the manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

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


        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="bf5f6-149">Al cifrar con Widevine, solo podría entregar con DASH.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-149">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="bf5f6-150">Asegúrese de especificar DASH en el protocolo de entrega de activos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-150">Make sure to specify DASH in the asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="bf5f6-151">Directiva de entrega de recursos DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="bf5f6-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="bf5f6-152">El método **CreateAssetDeliveryPolicy** siguiente crea la entidad **AssetDeliveryPolicy** que se configura para aplicar el cifrado de sobre dinámico (**DynamicEnvelopeEncryption**) para los protocolos Smooth Streaming, HLS y DASH (si decide no especificar algunos protocolos, se bloqueará el streaming en ellos).</span><span class="sxs-lookup"><span data-stu-id="bf5f6-152">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to Smooth Streaming, HLS, and DASH protocols (if you decide to not specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="bf5f6-153">El método toma dos parámetros: **Asset** (el recurso al que desea aplicar la directiva de entrega) e **IContentKey** (la clave de contenido de tipo **EnvelopeEncryption**. Para más información, consulte [Creación de una clave de contenido](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="bf5f6-153">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="bf5f6-154">Para obtener información sobre los valores que puede especificar al crear una entidad AssetDeliveryPolicy, consulte la sección [Tipos usados al definir AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="bf5f6-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get the Key Delivery Base Url by removing the Query parameter.  The Dynamic Encryption service will
        //  automatically add the correct key identifier to the url when it generates the Envelope encrypted content
        //  manifest.  Omitting the IV will also cause the Dynamice Encryption service to generate a deterministic
        //  IV for the content automatically.  By using the EnvelopeBaseKeyAcquisitionUrl and omitting the IV, this
        //  allows the AssetDelivery policy to be reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // The following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended to the envelope and
        //   the Initialization Vector (IV) to use for the envelope encryption.
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

        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="bf5f6-155"><a id="types"></a>Tipos usados al definir AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="bf5f6-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="bf5f6-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="bf5f6-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="bf5f6-157">La enumeración siguiente describe los valores que puede establecer para el protocolo de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-157">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <span data-ttu-id="bf5f6-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="bf5f6-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="bf5f6-159">La enumeración siguiente describe los valores que puede establecer para el tipo de directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-159">The following enum describes values you can set for the asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// The Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption to the asset.
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

### <span data-ttu-id="bf5f6-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="bf5f6-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="bf5f6-161">La enumeración siguiente describe los valores que puede utilizar para configurar el método de entrega de la clave de contenido al cliente.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-161">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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

### <span data-ttu-id="bf5f6-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="bf5f6-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="bf5f6-163">La enumeración siguiente describe los valores que puede establecer para configurar las claves usadas para obtener la configuración específica para una directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf5f6-163">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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
        /// The initialization vector to use for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// The PlayReady License Acquisition Url to use for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// The PlayReady Custom Attributes to add to the PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// The initialization vector to use for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="bf5f6-164">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="bf5f6-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bf5f6-165">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="bf5f6-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

