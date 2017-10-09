---
title: "Directiva de autorización de clave de contenido aaaConfigure usando el SDK de .NET de servicios multimedia | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure una directiva de autorización para una clave de contenido mediante el SDK de .NET de servicios multimedia."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: cfcbc5da9819bcec8b163fef183988a8beff9ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="9dcf5-103">Cifrado dinámico: configuración de la directiva de autorización de claves de contenido</span><span class="sxs-lookup"><span data-stu-id="9dcf5-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="9dcf5-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9dcf5-104">Overview</span></span>
<span data-ttu-id="9dcf5-105">Servicios de multimedia de Microsoft Azure le permite toodeliver MPEG-DASH, Smooth Streaming y secuencias de HTTP-Live-Streaming (HLS) protegidas con Advanced Encryption Standard (AES) (con claves de cifrado de 128 bits) o [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="9dcf5-105">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="9dcf5-106">AMS también permite toodeliver guión streams cifrado con Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-106">AMS also enables you toodeliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="9dcf5-107">PlayReady y Widevine se cifran por hello especificación de cifrado común (ISO/IEC 23001-7 CENC).</span><span class="sxs-lookup"><span data-stu-id="9dcf5-107">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="9dcf5-108">Servicios multimedia también ofrecen una **servicio de entrega de clave/licencia** de que los clientes pueden obtener claves de AES o tooplay de licencias de PlayReady/Widevine Hola contenido cifrado.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses tooplay hello encrypted content.</span></span>

<span data-ttu-id="9dcf5-109">Si desea para los servicios multimedia tooencrypt un activo, que tooassociate una clave de cifrado (**CommonEncryption** o **EnvelopeEncryption**) a activo hello (tal como se describe [aquí](media-services-dotnet-create-contentkey.md)) y también configurar directivas de autorización para la clave de hello (como se describe en este artículo).</span><span class="sxs-lookup"><span data-stu-id="9dcf5-109">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="9dcf5-110">Cuando un Reproductor solicita una secuencia, los servicios multimedia usa Hola especificado toodynamically clave cifrar el contenido con cifrado de AES o DRM.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-110">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="9dcf5-111">secuencia de hello toodecrypt, Hola Reproductor solicitará clave Hola del servicio de entrega de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-111">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="9dcf5-112">toodecide si es usuario de hello autorizado tooget clave de hello, servicio de hello evalúa las directivas de autorización de Hola que especificó para la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-112">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="9dcf5-113">Servicios multimedia admite varias formas de autenticar a los usuarios que realizan solicitudes de clave.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="9dcf5-114">Hello directiva de autorización de clave de contenido podría tener una o más restricciones de autorización: **abrir** o **token** restricción.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-114">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="9dcf5-115">directiva restringida de tokens de Hello debe ir acompañada de un token emitido por un Token seguro servicio (STS).</span><span class="sxs-lookup"><span data-stu-id="9dcf5-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="9dcf5-116">Servicios multimedia admite tokens en hello **Tokens Web simples** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato y **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) formato.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-116">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="9dcf5-117">Los Servicios multimedia no proporcionan Servicios de tokens seguros.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="9dcf5-118">Puede crear a un STS personalizado o aprovechar símbolos (tokens) de Microsoft Azure ACS tooissue.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-118">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="9dcf5-119">Hola STS debe estar configurado toocreate un token firmado con la clave especificada de Hola y emiten notificaciones que especificó en la configuración de restricción de token de hello (como se describe en este artículo).</span><span class="sxs-lookup"><span data-stu-id="9dcf5-119">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="9dcf5-120">Hello servicio de entrega de claves de servicios multimedia devolverá a cliente de toohello clave de cifrado de hello si Hola token es válido y hello notificaciones de token de hello coinciden con los configurados para la clave de contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-120">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="9dcf5-121">Para obtener más información, consulte</span><span class="sxs-lookup"><span data-stu-id="9dcf5-121">For more information, see</span></span>

[<span data-ttu-id="9dcf5-122">Autenticación de token JWT</span><span class="sxs-lookup"><span data-stu-id="9dcf5-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="9dcf5-123">[Integración de la aplicación OWIN basada en MVC de Servicios multimedia de Azure con Azure Active Directory y restricción de la entrega de claves de contenido basada en notificaciones de JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="9dcf5-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="9dcf5-124">[Usar tokens de ACS de Azure tooissue](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="9dcf5-124">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="9dcf5-125">Se aplican algunas consideraciones:</span><span class="sxs-lookup"><span data-stu-id="9dcf5-125">Some considerations apply:</span></span>
* <span data-ttu-id="9dcf5-126">Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-126">When your AMS account is created a **default** streaming endpoint is added  tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="9dcf5-127">toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, el extremo de streaming tiene toobe en hello **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-127">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has toobe in hello **Running** state.</span></span> 
* <span data-ttu-id="9dcf5-128">El recurso debe contener un conjunto de archivos MP4 de velocidad de bits adaptable o archivos Smooth Streaming de velocidad de bits adaptable.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="9dcf5-129">Para obtener más información, consulte [Codificación de un recurso](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="9dcf5-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="9dcf5-130">Cargue y codifique sus recursos con la opción **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="9dcf5-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="9dcf5-131">Si tiene previsto toohave varias claves de contenido que requieran Hola misma configuración de directiva, es muy recomendable toocreate una directiva de autorización única y volver a usarla con varias claves de contenido.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-131">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="9dcf5-132">Hola servicio de entrega de claves almacena en caché ContentKeyAuthorizationPolicy y sus objetos relacionados (opciones de directivas y restricciones) durante 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-132">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="9dcf5-133">Si una contentkeyauthorizationpolicy y especificar una restricción de "Token", toouse, a continuación, probarlo y, a continuación, actualizar la directiva de Hola "Abierto" demasiado restricción, se tardará aproximadamente 15 minutos antes de hello conmutadores toohello "Abierta" versión de la directiva de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-133">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="9dcf5-134">Si agrega o actualiza la directiva de entrega de recursos, debe eliminar un localizador existente (si hay) y crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="9dcf5-135">En este momento no se pueden cifrar las descargas progresivas.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="9dcf5-136">Cifrado dinámico AES-128</span><span class="sxs-lookup"><span data-stu-id="9dcf5-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="9dcf5-137">Restricción open</span><span class="sxs-lookup"><span data-stu-id="9dcf5-137">Open Restriction</span></span>
<span data-ttu-id="9dcf5-138">Restricción abierta significa sistema Hola ofrecerá hello tooanyone clave que realiza una solicitud de clave.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-138">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="9dcf5-139">Esta restricción puede ser útil para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="9dcf5-140">Hola de ejemplo siguiente crea una directiva de autorización abierta y agrega toohello clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-140">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="9dcf5-141">Restricción de token</span><span class="sxs-lookup"><span data-stu-id="9dcf5-141">Token Restriction</span></span>
<span data-ttu-id="9dcf5-142">Esta sección describe cómo toocreate un contenido directiva de autorización de clave y lo asocia con la clave de contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-142">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="9dcf5-143">Directiva de autorización de Hello describe los requisitos de autorización deben ser toodetermine cumpla si usuario hello es clave de hello tooreceive autorizados (por ejemplo, lista de "clave de verificación" hello contienen clave Hola ese token Hola se firmó con).</span><span class="sxs-lookup"><span data-stu-id="9dcf5-143">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="9dcf5-144">opción de restricción de token de hello tooconfigure, deberá toouse un documento XML requisitos de autorización del token de toodescribe Hola.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-144">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="9dcf5-145">XML de configuración de restricción de token de Hello debe ajustarse toohello después de esquema XML.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-145">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="9dcf5-146"><a id="schema"></a>Esquema de restricción de token</span><span class="sxs-lookup"><span data-stu-id="9dcf5-146"><a id="schema"></a>Token restriction schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

<span data-ttu-id="9dcf5-147">Al configurar hello **token** restringe la directiva, debe especificar Hola principal ** comprobación clave **, **emisor** y **audiencia** parámetros.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-147">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="9dcf5-148">Hola ** clave de verificación principal ** contiene clave Hola Hola token se firmó con, **emisor** es servicio de token seguro Hola ese token de Hola de problemas.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-148">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="9dcf5-149">Hola **audiencia** (a veces denominado **ámbito**) describe la intención de Hola de token de Hola o recurso de hello token Hola autoriza el acceso a.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-149">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="9dcf5-150">Hola servicio de entrega de claves de servicios multimedia valida que estos valores de símbolo (token) de hello coinciden con los valores de hello en plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="9dcf5-151">Cuando se usa **SDK de servicios multimedia para .NET**, puede usar hello **TokenRestrictionTemplate** token de restricción de clase toogenerate Hola.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-151">When using **Media Services SDK for .NET**, you can use hello **TokenRestrictionTemplate** class toogenerate hello restriction token.</span></span>
<span data-ttu-id="9dcf5-152">Hola de ejemplo siguiente crea una directiva de autorización con una restricción de token.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-152">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="9dcf5-153">En este ejemplo, cliente hello tiene toopresent un token que contenga: firma de clave (VerificationKey), un emisor de tokens y notificaciones requeridas.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-153">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {
        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    }

#### <span data-ttu-id="9dcf5-154"><a id="test"></a>Token de prueba</span><span class="sxs-lookup"><span data-stu-id="9dcf5-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="9dcf5-155">tooget un token de prueba basado en restricción de token de Hola que se usó para la directiva de autorización de claves de hello, Hola después.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-155">tooget a test token based on hello token restriction that was used for hello key authorization policy, do hello following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
    // Note, you need toopass hello key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="9dcf5-156">Cifrado dinámico PlayReady.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="9dcf5-157">Servicios multimedia permite derechos de hello tooconfigure y restricciones donde desea que hello tooenforce en tiempo de ejecución de DRM de PlayReady cuando un usuario trate de tooplay volver el contenido protegido.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-157">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="9dcf5-158">Al proteger el contenido con PlayReady, una de estas cosas Hola deberá toospecify en la directiva de autorización es una cadena XML que define hello [plantilla de licencia de PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9dcf5-158">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="9dcf5-159">En el SDK de servicios multimedia para. NET, Hola **PlayReadyLicenseResponseTemplate** y **PlayReadyLicenseTemplate** clases le ayudará a definir Hola plantilla de licencia de PlayReady.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-159">In Media Services SDK for .NET, hello **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define hello PlayReady License Template.</span></span>

<span data-ttu-id="9dcf5-160">[En este tema](media-services-protect-with-drm.md) muestra cómo tooencrypt su contenido con **PlayReady** y **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-160">[This topic](media-services-protect-with-drm.md) shows how tooencrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="9dcf5-161">Restricción open</span><span class="sxs-lookup"><span data-stu-id="9dcf5-161">Open Restriction</span></span>
<span data-ttu-id="9dcf5-162">Restricción abierta significa sistema Hola ofrecerá hello tooanyone clave que realiza una solicitud de clave.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-162">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="9dcf5-163">Esta restricción puede ser útil para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="9dcf5-164">Hola de ejemplo siguiente crea una directiva de autorización abierta y agrega toohello clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-164">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="9dcf5-165">Restricción de token</span><span class="sxs-lookup"><span data-stu-id="9dcf5-165">Token Restriction</span></span>
<span data-ttu-id="9dcf5-166">opción de restricción de token de hello tooconfigure, deberá toouse un documento XML requisitos de autorización del token de toodescribe Hola.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-166">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="9dcf5-167">configuración de restricción de token de Hello XML debe ajustarse toohello esquema XML se muestra en [esto](#schema) sección.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-167">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {

        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();


        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    } 

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // hello following code configures PlayReady License Template using .NET classes
        // and returns hello XML string.

        //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user. 
        //It contains a field for a custom data string between hello license server and hello application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // toobe returned toohello end users. 
        //It contains hello data on hello content key in hello license and any rights or restrictions toobe 
        //enforced by hello PlayReady DRM runtime when using hello content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether hello license is persistent (saved in persistent storage on hello client) 
        //or non-persistent (only held in memory while hello player is using hello license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use hello license or not.  
        // If true, hello MinimumSecurityLevel property of hello license
        // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class. 
        // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions 
        // configured in hello license and on hello PlayRight itself (for playback specific policy). 
        // Much of hello policy on hello PlayRight has toodo with output restrictions 
        // which control hello types of outputs that hello content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if hello DigitalVideoOnlyContentRestriction is enabled, 
        //then hello DRM runtime will only allow hello video toobe displayed over digital outputs 
        //(analog video outputs won’t be allowed toopass hello content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience. 
        // If hello output protections are configured too restrictive, 
        // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="9dcf5-168">tooget un token de prueba basado en la restricción de token de Hola que se usó para vea de directiva de autorización de claves de hello [esto](#test) sección.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-168">tooget a test token based on hello token restriction that was used for hello key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="9dcf5-169"><a id="types"></a>Tipos usados al definir ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="9dcf5-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="9dcf5-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="9dcf5-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="9dcf5-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="9dcf5-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="9dcf5-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="9dcf5-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="9dcf5-173">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="9dcf5-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9dcf5-174">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="9dcf5-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="9dcf5-175">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="9dcf5-175">Next step</span></span>
<span data-ttu-id="9dcf5-176">Ahora que ha configurado la directiva de autorización de la clave de contenido, vaya toohello [la directiva de entrega del activo de tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) tema.</span><span class="sxs-lookup"><span data-stu-id="9dcf5-176">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

