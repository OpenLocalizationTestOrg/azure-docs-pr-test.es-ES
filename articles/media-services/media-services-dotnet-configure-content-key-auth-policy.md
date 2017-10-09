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
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a>Cifrado dinámico: configuración de la directiva de autorización de claves de contenido
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Información general
Servicios de multimedia de Microsoft Azure le permite toodeliver MPEG-DASH, Smooth Streaming y secuencias de HTTP-Live-Streaming (HLS) protegidas con Advanced Encryption Standard (AES) (con claves de cifrado de 128 bits) o [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS también permite toodeliver guión streams cifrado con Widevine DRM. PlayReady y Widevine se cifran por hello especificación de cifrado común (ISO/IEC 23001-7 CENC).

Servicios multimedia también ofrecen una **servicio de entrega de clave/licencia** de que los clientes pueden obtener claves de AES o tooplay de licencias de PlayReady/Widevine Hola contenido cifrado.

Si desea para los servicios multimedia tooencrypt un activo, que tooassociate una clave de cifrado (**CommonEncryption** o **EnvelopeEncryption**) a activo hello (tal como se describe [aquí](media-services-dotnet-create-contentkey.md)) y también configurar directivas de autorización para la clave de hello (como se describe en este artículo).

Cuando un Reproductor solicita una secuencia, los servicios multimedia usa Hola especificado toodynamically clave cifrar el contenido con cifrado de AES o DRM. secuencia de hello toodecrypt, Hola Reproductor solicitará clave Hola del servicio de entrega de claves de Hola. toodecide si es usuario de hello autorizado tooget clave de hello, servicio de hello evalúa las directivas de autorización de Hola que especificó para la clave de Hola.

Servicios multimedia admite varias formas de autenticar a los usuarios que realizan solicitudes de clave. Hello directiva de autorización de clave de contenido podría tener una o más restricciones de autorización: **abrir** o **token** restricción. directiva restringida de tokens de Hello debe ir acompañada de un token emitido por un Token seguro servicio (STS). Servicios multimedia admite tokens en hello **Tokens Web simples** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato y **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) formato.

Los Servicios multimedia no proporcionan Servicios de tokens seguros. Puede crear a un STS personalizado o aprovechar símbolos (tokens) de Microsoft Azure ACS tooissue. Hola STS debe estar configurado toocreate un token firmado con la clave especificada de Hola y emiten notificaciones que especificó en la configuración de restricción de token de hello (como se describe en este artículo). Hello servicio de entrega de claves de servicios multimedia devolverá a cliente de toohello clave de cifrado de hello si Hola token es válido y hello notificaciones de token de hello coinciden con los configurados para la clave de contenido de Hola.

Para obtener más información, consulte

[Autenticación de token JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Integración de la aplicación OWIN basada en MVC de Servicios multimedia de Azure con Azure Active Directory y restricción de la entrega de claves de contenido basada en notificaciones de JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Usar tokens de ACS de Azure tooissue](http://mingfeiy.com/acs-with-key-services).

### <a name="some-considerations-apply"></a>Se aplican algunas consideraciones:
* Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado. toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, el extremo de streaming tiene toobe en hello **ejecutando** estado. 
* El recurso debe contener un conjunto de archivos MP4 de velocidad de bits adaptable o archivos Smooth Streaming de velocidad de bits adaptable. Para obtener más información, consulte [Codificación de un recurso](media-services-encode-asset.md).
* Cargue y codifique sus recursos con la opción **AssetCreationOptions.StorageEncrypted** .
* Si tiene previsto toohave varias claves de contenido que requieran Hola misma configuración de directiva, es muy recomendable toocreate una directiva de autorización única y volver a usarla con varias claves de contenido.
* Hola servicio de entrega de claves almacena en caché ContentKeyAuthorizationPolicy y sus objetos relacionados (opciones de directivas y restricciones) durante 15 minutos.  Si una contentkeyauthorizationpolicy y especificar una restricción de "Token", toouse, a continuación, probarlo y, a continuación, actualizar la directiva de Hola "Abierto" demasiado restricción, se tardará aproximadamente 15 minutos antes de hello conmutadores toohello "Abierta" versión de la directiva de directiva de Hola.
* Si agrega o actualiza la directiva de entrega de recursos, debe eliminar un localizador existente (si hay) y crear uno nuevo.
* En este momento no se pueden cifrar las descargas progresivas.

## <a name="aes-128-dynamic-encryption"></a>Cifrado dinámico AES-128
### <a name="open-restriction"></a>Restricción open
Restricción abierta significa sistema Hola ofrecerá hello tooanyone clave que realiza una solicitud de clave. Esta restricción puede ser útil para realizar pruebas.

Hola de ejemplo siguiente crea una directiva de autorización abierta y agrega toohello clave de contenido.

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


### <a name="token-restriction"></a>Restricción de token
Esta sección describe cómo toocreate un contenido directiva de autorización de clave y lo asocia con la clave de contenido de Hola. Directiva de autorización de Hello describe los requisitos de autorización deben ser toodetermine cumpla si usuario hello es clave de hello tooreceive autorizados (por ejemplo, lista de "clave de verificación" hello contienen clave Hola ese token Hola se firmó con).

opción de restricción de token de hello tooconfigure, deberá toouse un documento XML requisitos de autorización del token de toodescribe Hola. XML de configuración de restricción de token de Hello debe ajustarse toohello después de esquema XML.

#### <a id="schema"></a>Esquema de restricción de token
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

Al configurar hello **token** restringe la directiva, debe especificar Hola principal ** comprobación clave **, **emisor** y **audiencia** parámetros. Hola ** clave de verificación principal ** contiene clave Hola Hola token se firmó con, **emisor** es servicio de token seguro Hola ese token de Hola de problemas. Hola **audiencia** (a veces denominado **ámbito**) describe la intención de Hola de token de Hola o recurso de hello token Hola autoriza el acceso a. Hola servicio de entrega de claves de servicios multimedia valida que estos valores de símbolo (token) de hello coinciden con los valores de hello en plantilla Hola. 

Cuando se usa **SDK de servicios multimedia para .NET**, puede usar hello **TokenRestrictionTemplate** token de restricción de clase toogenerate Hola.
Hola de ejemplo siguiente crea una directiva de autorización con una restricción de token. En este ejemplo, cliente hello tiene toopresent un token que contenga: firma de clave (VerificationKey), un emisor de tokens y notificaciones requeridas.

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

#### <a id="test"></a>Token de prueba
tooget un token de prueba basado en restricción de token de Hola que se usó para la directiva de autorización de claves de hello, Hola después.

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


## <a name="playready-dynamic-encryption"></a>Cifrado dinámico PlayReady.
Servicios multimedia permite derechos de hello tooconfigure y restricciones donde desea que hello tooenforce en tiempo de ejecución de DRM de PlayReady cuando un usuario trate de tooplay volver el contenido protegido. 

Al proteger el contenido con PlayReady, una de estas cosas Hola deberá toospecify en la directiva de autorización es una cadena XML que define hello [plantilla de licencia de PlayReady](media-services-playready-license-template-overview.md). En el SDK de servicios multimedia para. NET, Hola **PlayReadyLicenseResponseTemplate** y **PlayReadyLicenseTemplate** clases le ayudará a definir Hola plantilla de licencia de PlayReady.

[En este tema](media-services-protect-with-drm.md) muestra cómo tooencrypt su contenido con **PlayReady** y **Widevine**.

### <a name="open-restriction"></a>Restricción open
Restricción abierta significa sistema Hola ofrecerá hello tooanyone clave que realiza una solicitud de clave. Esta restricción puede ser útil para realizar pruebas.

Hola de ejemplo siguiente crea una directiva de autorización abierta y agrega toohello clave de contenido.

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

### <a name="token-restriction"></a>Restricción de token
opción de restricción de token de hello tooconfigure, deberá toouse un documento XML requisitos de autorización del token de toodescribe Hola. configuración de restricción de token de Hello XML debe ajustarse toohello esquema XML se muestra en [esto](#schema) sección.

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


tooget un token de prueba basado en la restricción de token de Hola que se usó para vea de directiva de autorización de claves de hello [esto](#test) sección. 

## <a id="types"></a>Tipos usados al definir ContentKeyAuthorizationPolicy
### <a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <a id="TokenType"></a>TokenType
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Paso siguiente
Ahora que ha configurado la directiva de autorización de la clave de contenido, vaya toohello [la directiva de entrega del activo de tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) tema.

