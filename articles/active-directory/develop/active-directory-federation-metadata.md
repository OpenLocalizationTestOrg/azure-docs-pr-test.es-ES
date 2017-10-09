---
title: "aaaAzure AD metadatos de federación | Documentos de Microsoft"
description: "Este artículo describe el documento de metadatos de federación de hello Azure Active Directory publica para los servicios que aceptan tokens de Azure Active Directory."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a>Metadatos de federación
Azure Active Directory (Azure AD) publica un documento de metadatos de federación para servicios que es configuran tokens de seguridad de hello tooaccept que emite Azure AD. formato de documento de metadatos de federación Hello se describe una Hola [lenguaje de federación de servicios Web (WS-Federation) versión 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), que extiende [metadatos de lenguaje de marcado de aserción de seguridad (SAML) de OASIS Hola V2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a>Puntos de conexión de metadatos específicos e independientes del inquilino
Azure AD publica los extremos específicos del inquilino e independientes del inquilino.

Los extremos específicos del inquilino están diseñados para un inquilino determinado. metadatos de federación específicos del inquilino de Hello incluyen información sobre el inquilino de hello, incluyendo emisor específico del inquilino y la información de punto de conexión. Las aplicaciones que restringen el inquilino único de acceso tooa utilizar extremos específicos del inquilino.

Extremos independientes del inquilino proporcionan información que es común inquilinos de Azure AD tooall. Esta información aplica tootenants hospedado en *login.microsoftonline.com* y se comparte entre los inquilinos. Los extremos independientes del inquilino se recomiendan para aplicaciones de varios inquilinos, ya que no están asociados a ningún inquilino en particular.

## <a name="federation-metadata-endpoints"></a>Puntos de conexión de metadatos de federación
Azure AD publica los metadatos de federación en `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.

Para **extremos específicos del inquilino**, hello `TenantDomainName` puede ser uno de los siguientes tipos de hello:

* Un nombre de dominio registrado de un inquilino de Azure AD, como `contoso.onmicrosoft.com`.
* Hola inmutable inquilino Id. del dominio de hello, como `72f988bf-86f1-41af-91ab-2d7cd011db45`.

Para **extremos independientes del inquilino**, hello `TenantDomainName` es `common`. Este documento enumera únicamente elementos de metadatos de federación de Hola que son inquilinos de Azure AD tooall comunes que se hospedan en login.microsoftonline.com.

Por ejemplo, un punto de conexión específico del inquilino podría ser `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`. es el extremo independiente del inquilino de Hello [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml). Puede ver el documento de metadatos de federación de hello escribiendo esta dirección URL en un explorador.

## <a name="contents-of-federation-metadata"></a>Contenido de los metadatos de federación
Hello siguiente sección proporciona información necesaria para los servicios que consumen los tokens de hello emitidos por Azure AD.

### <a name="entity-id"></a>El identificador de entidad
Hola `EntityDescriptor` elemento contiene un `EntityID` atributo. Hola valo hello `EntityID` atributo representa el emisor de hello, es decir, Hola del token de seguridad (STS) de servicio ese token emitido Hola. Es importante toovalidate emisor de hello cuando reciba un token.

Hello metadatos siguientes muestran un ejemplo específico del inquilino `EntityDescriptor` elemento con un `EntityID` elemento.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
Puede reemplazar Id. de inquilino Hola extremo independiente del inquilino de hello con su toocreate de Id. de inquilino específico de inquilino `EntityID` valor. se Hola valor resultante de Hello igual Hola emisor del token. Hola estrategia permite que un emisor de hello toovalidate de aplicación de varios inquilinos para un inquilino determinado.

Hello metadatos siguientes muestran un ejemplo independientes del inquilino `EntityID` elemento. Tenga en cuenta que hello `{tenant}` es un literal, no un marcador de posición.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a>Certificados de firma de tokens
Cuando un servicio recibe un token emitido por un inquilino de Azure AD, hello firma de token de hello debe validarse con una clave de firma que se publica en el documento de metadatos de federación de Hola. los metadatos de federación de Hello incluyen parte pública de Hola de certificados de Hola que usan los inquilinos de Hola para firmar los tokens. bytes sin procesar del certificado Hola aparecen en hello `KeyDescriptor` elemento. certificado de firma de token de Hello es válido para solo firma Hola al valor de hello `use` atributo es `signing`.

Un documento de metadatos de federación publicado por Azure AD puede tener varias claves de firmas, como cuando Azure AD está preparando hello tooupdate certificado de firma. Cuando un documento de metadatos de federación incluye más de un certificado, un servicio que se está validando los tokens de hello debe admitir todos los certificados en el documento de Hola.

Hello metadatos siguientes muestran un ejemplo `KeyDescriptor` elemento con una clave de firma.

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

Hola `KeyDescriptor` elemento aparece en dos lugares en el documento de metadatos de federación de hello; en la sección específica de WS-Federation de Hola y Hola específica de SAML. certificados de Hello publicados en ambas secciones se se Hola mismo.

En la sección Hola específica de WS-Federation, un lector de metadatos de WS-Federation leería los certificados de Hola de un `RoleDescriptor` elemento con hello `SecurityTokenServiceType` tipo.

Hello metadatos siguientes muestran un ejemplo `RoleDescriptor` elemento.

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

En la sección Hola específica de SAML, un lector de metadatos de WS-Federation leería los certificados de Hola de un `IDPSSODescriptor` elemento.

Hello metadatos siguientes muestran un ejemplo `IDPSSODescriptor` elemento.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
No hay ninguna diferencia en formato de Hola de certificados específicos del inquilino e independientes del inquilino.

### <a name="ws-federation-endpoint-url"></a>Dirección URL del punto de conexión de WS-Federation
metadatos de federación de Hello incluyen hello dirección URL que es Azure AD usa para el inicio de sesión único y cierre de sesión de protocolo WS-Federation único. Este punto de conexión aparece en hello `PassiveRequestorEndpoint` elemento.

Hello metadatos siguientes muestran un ejemplo `PassiveRequestorEndpoint` elemento para un extremo específico del inquilino.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
Para el extremo independiente del inquilino de hello, Hola URL de WS-Federation aparece en extremo Hola WS-Federation, tal y como se muestra en el siguiente ejemplo de Hola.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a>Dirección URL del punto de conexión de protocolo SAML
metadatos de federación de Hello incluyen dirección URL de Hola que Azure AD usa para el inicio de sesión único y cierre de sesión en el protocolo SAML 2.0 único. Estos extremos aparecen en hello `IDPSSODescriptor` elemento.

Hola, inicio de sesión y cierre de sesión, direcciones URL aparecen en hello `SingleSignOnService` y `SingleLogoutService` elementos.

Hello metadatos siguientes muestran un ejemplo `PassiveResistorEndpoint` para un extremo específico del inquilino.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

De igual forma extremos de Hola para puntos de conexión de protocolo de SAML 2.0 comunes de Hola se publican en los metadatos de federación independientes del inquilino de hello, tal y como se muestra en el siguiente ejemplo de Hola.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
