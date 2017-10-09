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
# <a name="configuring-asset-delivery-policies"></a>Configuración de directivas de entrega de recursos
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

Si tiene previsto toodeliver dinámicamente cifrada activos, uno de hello pasos Hola servicios multimedia de contenido de flujo de trabajo de entrega es la configuración de directivas de entrega de activos. Directiva de entrega del activo de Hello indica los servicios multimedia cómo desea para su toobe asset entregado: en el protocolo de transmisión por secuencias que debe su activo dinámicamente empaquetarse (por ejemplo, MPEG DASH, HLS, Smooth Streaming o todos), si no desea toodynamically cifrar un activo y cómo (sobre o cifrado común).

Este tema se describe cómo y por qué toocreate y configurar directivas de entrega de activos.

>[!NOTE]
>Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado. 
>
>Además, puede toouse toobe el empaquetado dinámico y cifrado dinámico su activo debe contener un conjunto de velocidad de bits adaptativa MP4s o archivos de Smooth Streaming de velocidad de bits adaptativa.

Podría aplicar distintas directivas toohello mismo activo. Por ejemplo, podría aplicar PlayReady cifrado tooSmooth transmisión por secuencias y AES Envelope cifrado tooMPEG DASH y HLS. Todos los protocolos que no estén definidos en una directiva de entrega (por ejemplo, se agrega una directiva única que solo especifica HLS como protocolo de Hola) se bloqueará de transmisión por secuencias. Hola toothis de excepción es si no tiene definida en absoluto ninguna directiva de entrega de activos. A continuación, todos los protocolos se permitirá en hello clara.

Si desea toodeliver un recurso cifrado de almacenamiento, debe configurar la directiva de entrega del activo de Hola. Antes de que se puede transmitir su activo, Hola streaming cifrado de almacenamiento de servidor quita hello y secuencias el contenido con hello especifica directiva de entrega. Por ejemplo, toodeliver su activo cifrado con clave de cifrado de sobre estándar de cifrado avanzado (AES), establezca el tipo de directiva de hello demasiado**DynamicEnvelopeEncryption**. cifrado de almacenamiento de tooremove y los activos de hello secuencia de hello claro, establecer tipo de directiva de hello demasiado**NoDynamicEncryption**. Ejemplos que muestran cómo tooconfigure estos tipos de directiva siguen.

Dependiendo de cómo configurar Directiva de entrega del activo de Hola que podría ser capaz de toodynamically paquete, dinámicamente cifrar y transmitir por hello después de protocolos de transmisión por secuencias: Smooth Streaming, HLS, secuencias de MPEG DASH.

Hola siguiente lista muestra hello da formato a usar toostream Smooth, HLS, guión.

Smooth Streaming:

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{filename}.ism/Manifest

HLS:

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=m3u8-aapl)

MPEG DASH

{nombre de extremo de streaming-nombre de cuenta de servicios multimedia}.streaming.mediaservices.windows.net/{Id. de localizador}/{nombre de archivo}.ism/Manifest(formato=mpd-time-csf)


Para obtener instrucciones sobre cómo toopublish un activo y generar una dirección URL de streaming, vea [generar una dirección URL de streaming](media-services-deliver-streaming-content.md).

## <a name="considerations"></a>Consideraciones
* No puede eliminar una entidad AssetDeliveryPolicy asociada a un activo mientras hay un localizador OnDemand (transmisión) para ese activo. recomendación de Hello es Directiva de hello tooremove de recurso de hello antes de eliminar la directiva de Hola.
* No se puede crear un localizador de transmisión en un activo cifrado de almacenamiento cuando no se establece ninguna directiva de entrega de activos.  Si Hola activo no está cifrado de almacenamiento, sistema de hello le permitirán crear un recurso de hello localizador y secuencias en hello claro sin una directiva de entrega del activo.
* Puede tener varias directivas de entrega de activos asociadas a un único recurso, pero solo se puede especificar una manera de toohandle un AssetDeliveryProtocol determinado.  Lo que significa que si intenta dos directivas de entrega de toolink especificada por el protocolo de AssetDeliveryProtocol.SmoothStreaming Hola que producirá un error porque el sistema de hello no sabe cuál desea tooapply cuando un cliente realiza una solicitud de transmisión por secuencias suave.
* Si tiene un recurso con un localizador de transmisión por secuencias existente, no se puede vincular un nuevo recurso toohello de directiva, desvincular una directiva existente de recurso de Hola o actualizar una directiva de entrega asociada Hola activo.  En primer lugar tiene el localizador de streaming de hello tooremove, ajustar las directivas de hello y, a continuación, volver a crear el localizador de streaming de Hola.  Puede usar Hola mismo locatorId se vuelven a crear Hola streaming localizador pero debe asegurarse de que no causará problemas para los clientes ya que puede almacenarse en caché contenido por origen de Hola o de una CDN siguen en la cadena.

>[!NOTE]

>Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP. Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Conectar servicios de tooMedia

Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia. Debe realizar las llamadas subsiguientes toohello nuevo URI.

## <a name="clear-asset-delivery-policy"></a>Directiva de entrega de recursos sin cifrar
### <a id="create_asset_delivery_policy"></a>Creación de directiva de entrega de recursos
Hello solicitud HTTP siguiente crea una directiva de entrega de activos que especifica toonot aplicar cifrado dinámico y flujo de hello toodeliver en cualquiera de hello siguiendo los protocolos: protocolos MPEG DASH, HLS y Smooth Streaming. 

Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.   

Solicitud:

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

Respuesta:

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

### <a id="link_asset_with_asset_delivery_policy"></a>Vinculación de un recurso con la directiva de entrega de recursos
Hola después Hola de vínculos de solicitud HTTP especifica directiva de entrega de activos toohello activo a.

Solicitud:

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

Respuesta:

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Directiva de entrega de recursos DynamicEnvelopeEncryption
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a>Crear clave de contenido del tipo de EnvelopeEncryption de Hola y vincularlo toohello activo
Al especificar la directiva de entrega DynamicEnvelopeEncryption, deberá toomake seguro toolink la clave de contenido activo tooa de hello EnvelopeEncryption tipo. Para obtener más información, consulte [Creación de una clave de contenido](media-services-rest-create-contentkey.md).

### <a id="get_delivery_url"></a>Obtención de una dirección URL de entrega
Dirección URL de entrega de Get hello para hello especifica método de entrega de clave de contenido de hello creado en el paso anterior de Hola. Un cliente usa Hola devuelve la dirección URL toorequest contenido protegido de una clave de AES o una licencia de PlayReady en hello tooplayback de orden.

Especificar tipo de Hola de hello tooget de dirección URL en el cuerpo de saludo de solicitud HTTP de Hola. Si va a proteger el contenido con PlayReady, solicite una dirección URL de adquisición de licencias de PlayReady de servicios multimedia, con 1 para hello keyDeliveryType: {"keyDeliveryType": 1}. Si va a proteger su contenido con el cifrado de sellado hello, solicite una dirección URL de adquisición de claves especificando 2 para keyDeliveryType: {"keyDeliveryType": 2}.

Solicitud:

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

Respuesta:

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


### <a name="create-asset-delivery-policy"></a>Creación de directiva de entrega de recursos
solicitud HTTP siguiente Hello crea hello **AssetDeliveryPolicy** que es el cifrado de sobre dinámico configurado tooapply (**DynamicEnvelopeEncryption**) toohello **HLS**protocolo (en este ejemplo, otros protocolos se bloqueará de transmisión por secuencias). 

Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.   

Solicitud:

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


Respuesta:

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


### <a name="link-asset-with-asset-delivery-policy"></a>Vinculación de un recurso con la directiva de entrega de recursos
Consulte [Vinculación de un recurso con la directiva de entrega de recursos](#link_asset_with_asset_delivery_policy)

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Directiva de entrega de recursos DynamicCommonEncryption
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a>Crear clave de contenido del tipo de hello CommonEncryption y vincularlo toohello activo
Al especificar la directiva de entrega DynamicCommonEncryption, deberá toomake seguro toolink la clave de contenido activo tooa de hello CommonEncryption tipo. Para obtener más información, consulte [Creación de una clave de contenido](media-services-rest-create-contentkey.md).

### <a name="get-delivery-url"></a>Obtención de una dirección URL de entrega
Obtener dirección URL de entrega de Hola Hola PlayReady método de entrega de clave de contenido de hello creado en el paso anterior de Hola. Un cliente usa Hola devuelve contenido protegida de una licencia de PlayReady en hello tooplayback de orden de toorequest de dirección URL. Para obtener más información, consulte [Obtención de una dirección URL de entrega](#get_delivery_url)

### <a name="create-asset-delivery-policy"></a>Creación de directiva de entrega de recursos
solicitud HTTP siguiente Hello crea hello **AssetDeliveryPolicy** que es configurado tooapply comunes cifrado dinámico (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protocolo (en este ejemplo, otros protocolos se bloqueará de transmisión por secuencias). 

Para obtener información sobre qué valores se puede especificar al crear un AssetDeliveryPolicy, vea hello [tipos que se utilizan al definir AssetDeliveryPolicy](#types) sección.   

Solicitud:

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


Si desea que el contenido con DRM Widevine tooprotect, actualizar hello AssetDeliveryConfiguration valores toouse WidevineLicenseAcquisitionUrl (que tiene el valor de Hola de 7) y especificar dirección URL de Hola de un servicio de entrega de licencia. Puede usar Hola después AMS socios toohelp entregar licencias de Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Por ejemplo: 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> Cuando se cifra con Widevine, sólo sería capaz de toodeliver con guión. Asegúrese de protocolo de entrega de seguro toospecify guión (2) hello en activo.
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a>Vinculación de un recurso con la directiva de entrega de recursos
Consulte [Vinculación de un recurso con la directiva de entrega de recursos](#link_asset_with_asset_delivery_policy)

## <a id="types"></a>Tipos usados al definir AssetDeliveryPolicy

### <a name="assetdeliveryprotocol"></a>AssetDeliveryProtocol

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

### <a name="assetdeliverypolicytype"></a>AssetDeliveryPolicyType

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

### <a name="contentkeydeliverytype"></a>ContentKeyDeliveryType

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


### <a name="assetdeliverypolicyconfigurationkey"></a>AssetDeliveryPolicyConfigurationKey

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

