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
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>Configuración de directivas de entrega de recursos con el SDK de .NET
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>Información general
Si tiene previsto toodelivery cifrado activos, uno de hello pasos Hola servicios multimedia de contenido de flujo de trabajo de entrega es la configuración de directivas de entrega de activos. Directiva de entrega del activo de Hello indica los servicios multimedia cómo desea para su toobe asset entregado: en el protocolo de transmisión por secuencias que debe su activo dinámicamente empaquetarse (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos), si no desea toodynamically cifrar un activo y cómo (sobre o cifrado común).

Este tema se describe cómo y por qué toocreate y configurar directivas de entrega de activos.

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 
>
>Además, puede toouse toobe el empaquetado dinámico y cifrado dinámico su activo debe contener un conjunto de velocidad de bits adaptativa MP4s o archivos de Smooth Streaming de velocidad de bits adaptativa.


Podría aplicar distintas directivas toohello mismo activo. Por ejemplo, podría aplicar PlayReady cifrado tooSmooth transmisión por secuencias y AES Envelope cifrado tooMPEG DASH y HLS. Todos los protocolos que no estén definidos en una directiva de entrega (por ejemplo, se agrega una directiva única que solo especifica HLS como protocolo de Hola) se bloqueará de transmisión por secuencias. Hola toothis de excepción es si no tiene definida en absoluto ninguna directiva de entrega de activos. A continuación, todos los protocolos se permitirá en hello clara.

Si desea toodeliver un recurso cifrado de almacenamiento, debe configurar la directiva de entrega del activo de Hola. Antes de que se puede transmitir su activo, Hola streaming cifrado de almacenamiento de servidor quita hello y secuencias el contenido con hello especifica directiva de entrega. Por ejemplo, toodeliver su activo cifrado con clave de cifrado de sobre estándar de cifrado avanzado (AES), establezca el tipo de directiva de hello demasiado**DynamicEnvelopeEncryption**. cifrado de almacenamiento de tooremove y los activos de hello secuencia de hello claro, establecer tipo de directiva de hello demasiado**NoDynamicEncryption**. Ejemplos que muestran cómo tooconfigure estos tipos de directiva siguen.

Dependiendo de cómo configurar Directiva de entrega del activo de Hola que podría ser capaz de toodynamically paquete, dinámicamente cifrar y transmitir por hello después de protocolos de transmisión por secuencias: secuencias de Smooth Streaming, HLS y MPEG DASH.

Hello lista siguiente muestra los formatos de Hola que usas toostream Smooth, HLS y DASH.

Smooth Streaming:

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{filename}.ism/Manifest

HLS:

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=m3u8-aapl)

MPEG DASH

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=mpd-time-csf)


## <a name="considerations"></a>Consideraciones
* No puede eliminar una entidad AssetDeliveryPolicy asociada a un activo mientras hay un localizador OnDemand (transmisión) para ese activo. recomendación de Hello es Directiva de hello tooremove de recurso de hello antes de eliminar la directiva de Hola.
* No se puede crear un localizador de transmisión en un activo cifrado de almacenamiento cuando no se establece ninguna directiva de entrega de activos.  Si Hola activo no está cifrado de almacenamiento, sistema de hello le permitirán crear un recurso de hello localizador y secuencias en hello claro sin una directiva de entrega del activo.
* Puede tener varias directivas de entrega de activos asociadas a un único recurso, pero solo se puede especificar una manera de toohandle un AssetDeliveryProtocol determinado.  Lo que significa que si intenta dos directivas de entrega de toolink especificada por el protocolo de AssetDeliveryProtocol.SmoothStreaming Hola que producirá un error porque el sistema de hello no sabe cuál desea tooapply cuando un cliente realiza una solicitud de transmisión por secuencias suave.
* Si tiene un recurso con un localizador de transmisión por secuencias existente, no se puede vincular un nuevo recurso de toohello directiva (puede desvincular una directiva existente de recurso de hello, o actualizar una directiva de entrega asociada Hola activo).  En primer lugar tiene el localizador de streaming de hello tooremove, ajustar las directivas de hello y, a continuación, volver a crear el localizador de streaming de Hola.  Puede usar Hola mismo locatorId se vuelven a crear Hola streaming localizador pero debe asegurarse de que no causará problemas para los clientes ya que puede almacenarse en caché contenido por origen de Hola o de una CDN siguen en la cadena.

## <a name="clear-asset-delivery-policy"></a>Directiva de entrega de recursos sin cifrar

siguiente Hello **ConfigureClearAssetDeliveryPolicy** método especifica toonot aplicar cifrado dinámico y flujo de hello toodeliver en cualquiera de hello siguiendo los protocolos: protocolos MPEG DASH, HLS y Smooth Streaming. Puede ser conveniente tooapply este activos de cifrado de almacenamiento de tooyour de directiva.

Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Directiva de entrega de recursos DynamicCommonEncryption

siguiente Hello **CreateAssetDeliveryPolicy** método crea hello **AssetDeliveryPolicy** que es configurado tooapply comunes cifrado dinámico (**DynamicCommonEncryption**) tooa (se bloqueará otros protocolos de transmisión por secuencias) de protocolo de transmisión por secuencias suave. método Hello toma dos parámetros: **Asset** (Hola toowhich asset desea tooapply Hola entrega directiva) y **IContentKey** (clave de contenido de Hola de hello **CommonEncryption**tipo, para obtener más información, consulte: [crear una clave de contenido](media-services-dotnet-create-contentkey.md#common_contentkey)).

Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.

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

Servicios multimedia de Azure también permite tooadd Widevine cifrado. Hello en el ejemplo siguiente se muestra cómo PlayReady y Widevine que se agrega la directiva de entrega del activo de toohello.

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
> Cuando se cifra con Widevine, sólo sería capaz de toodeliver con guión. Asegúrese de toospecify seguro guión en el protocolo de entrega de activos de Hola.
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Directiva de entrega de recursos DynamicEnvelopeEncryption
siguiente Hello **CreateAssetDeliveryPolicy** método crea hello **AssetDeliveryPolicy** que es el cifrado de sobre dinámico configurado tooapply (**DynamicEnvelopeEncryption** ) tooSmooth protocolos de Streaming, HLS y DASH (si decide toonot especificar algunos protocolos, se bloquearán de transmisión por secuencias). método Hello toma dos parámetros: **Asset** (Hola toowhich asset desea tooapply Hola entrega directiva) y **IContentKey** (clave de contenido de Hola de hello **EnvelopeEncryption**tipo, para obtener más información, consulte: [crear una clave de contenido](media-services-dotnet-create-contentkey.md#envelope_contentkey)).

Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.   

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


## <a id="types"></a>Tipos usados al definir AssetDeliveryPolicy

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

Hello enum siguiente describe valores que puede establecer para el protocolo de entrega de activos de Hola.

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

### <a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType

Hello enum siguiente describe valores que puede establecer para el tipo de directiva de entrega de activos de Hola.  

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

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType

Hello enum siguiente describe valores que puede utilizar el método de entrega de hello tooconfigure de cliente de hello toohello de clave de contenido.
    
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

### <a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey

Hola después de la enumeración describe valores que puede establecer las claves usadas tooconfigure tooget configuración concreta para una directiva de entrega del activo.

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

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

