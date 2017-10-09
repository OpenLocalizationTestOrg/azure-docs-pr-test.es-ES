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
# <a name="federation-metadata"></a><span data-ttu-id="2cdd3-103">Metadatos de federación</span><span class="sxs-lookup"><span data-stu-id="2cdd3-103">Federation metadata</span></span>
<span data-ttu-id="2cdd3-104">Azure Active Directory (Azure AD) publica un documento de metadatos de federación para servicios que es configuran tokens de seguridad de hello tooaccept que emite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="2cdd3-105">formato de documento de metadatos de federación Hello se describe una Hola [lenguaje de federación de servicios Web (WS-Federation) versión 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), que extiende [metadatos de lenguaje de marcado de aserción de seguridad (SAML) de OASIS Hola V2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="2cdd3-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="2cdd3-106">Puntos de conexión de metadatos específicos e independientes del inquilino</span><span class="sxs-lookup"><span data-stu-id="2cdd3-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="2cdd3-107">Azure AD publica los extremos específicos del inquilino e independientes del inquilino.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="2cdd3-108">Los extremos específicos del inquilino están diseñados para un inquilino determinado.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="2cdd3-109">metadatos de federación específicos del inquilino de Hello incluyen información sobre el inquilino de hello, incluyendo emisor específico del inquilino y la información de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="2cdd3-110">Las aplicaciones que restringen el inquilino único de acceso tooa utilizar extremos específicos del inquilino.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="2cdd3-111">Extremos independientes del inquilino proporcionan información que es común inquilinos de Azure AD tooall.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="2cdd3-112">Esta información aplica tootenants hospedado en *login.microsoftonline.com* y se comparte entre los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="2cdd3-113">Los extremos independientes del inquilino se recomiendan para aplicaciones de varios inquilinos, ya que no están asociados a ningún inquilino en particular.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="2cdd3-114">Puntos de conexión de metadatos de federación</span><span class="sxs-lookup"><span data-stu-id="2cdd3-114">Federation metadata endpoints</span></span>
<span data-ttu-id="2cdd3-115">Azure AD publica los metadatos de federación en `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="2cdd3-116">Para **extremos específicos del inquilino**, hello `TenantDomainName` puede ser uno de los siguientes tipos de hello:</span><span class="sxs-lookup"><span data-stu-id="2cdd3-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="2cdd3-117">Un nombre de dominio registrado de un inquilino de Azure AD, como `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="2cdd3-118">Hola inmutable inquilino Id. del dominio de hello, como `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="2cdd3-119">Para **extremos independientes del inquilino**, hello `TenantDomainName` es `common`.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="2cdd3-120">Este documento enumera únicamente elementos de metadatos de federación de Hola que son inquilinos de Azure AD tooall comunes que se hospedan en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="2cdd3-121">Por ejemplo, un punto de conexión específico del inquilino podría ser `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="2cdd3-122">es el extremo independiente del inquilino de Hello [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="2cdd3-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="2cdd3-123">Puede ver el documento de metadatos de federación de hello escribiendo esta dirección URL en un explorador.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="2cdd3-124">Contenido de los metadatos de federación</span><span class="sxs-lookup"><span data-stu-id="2cdd3-124">Contents of federation Metadata</span></span>
<span data-ttu-id="2cdd3-125">Hello siguiente sección proporciona información necesaria para los servicios que consumen los tokens de hello emitidos por Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="2cdd3-126">El identificador de entidad</span><span class="sxs-lookup"><span data-stu-id="2cdd3-126">Entity ID</span></span>
<span data-ttu-id="2cdd3-127">Hola `EntityDescriptor` elemento contiene un `EntityID` atributo.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="2cdd3-128">Hola valo hello `EntityID` atributo representa el emisor de hello, es decir, Hola del token de seguridad (STS) de servicio ese token emitido Hola.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="2cdd3-129">Es importante toovalidate emisor de hello cuando reciba un token.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="2cdd3-130">Hello metadatos siguientes muestran un ejemplo específico del inquilino `EntityDescriptor` elemento con un `EntityID` elemento.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="2cdd3-131">Puede reemplazar Id. de inquilino Hola extremo independiente del inquilino de hello con su toocreate de Id. de inquilino específico de inquilino `EntityID` valor.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="2cdd3-132">se Hola valor resultante de Hello igual Hola emisor del token.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="2cdd3-133">Hola estrategia permite que un emisor de hello toovalidate de aplicación de varios inquilinos para un inquilino determinado.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="2cdd3-134">Hello metadatos siguientes muestran un ejemplo independientes del inquilino `EntityID` elemento.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="2cdd3-135">Tenga en cuenta que hello `{tenant}` es un literal, no un marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="2cdd3-136">Certificados de firma de tokens</span><span class="sxs-lookup"><span data-stu-id="2cdd3-136">Token signing certificates</span></span>
<span data-ttu-id="2cdd3-137">Cuando un servicio recibe un token emitido por un inquilino de Azure AD, hello firma de token de hello debe validarse con una clave de firma que se publica en el documento de metadatos de federación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="2cdd3-138">los metadatos de federación de Hello incluyen parte pública de Hola de certificados de Hola que usan los inquilinos de Hola para firmar los tokens.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="2cdd3-139">bytes sin procesar del certificado Hola aparecen en hello `KeyDescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="2cdd3-140">certificado de firma de token de Hello es válido para solo firma Hola al valor de hello `use` atributo es `signing`.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="2cdd3-141">Un documento de metadatos de federación publicado por Azure AD puede tener varias claves de firmas, como cuando Azure AD está preparando hello tooupdate certificado de firma.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="2cdd3-142">Cuando un documento de metadatos de federación incluye más de un certificado, un servicio que se está validando los tokens de hello debe admitir todos los certificados en el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="2cdd3-143">Hello metadatos siguientes muestran un ejemplo `KeyDescriptor` elemento con una clave de firma.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="2cdd3-144">Hola `KeyDescriptor` elemento aparece en dos lugares en el documento de metadatos de federación de hello; en la sección específica de WS-Federation de Hola y Hola específica de SAML.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="2cdd3-145">certificados de Hello publicados en ambas secciones se se Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="2cdd3-146">En la sección Hola específica de WS-Federation, un lector de metadatos de WS-Federation leería los certificados de Hola de un `RoleDescriptor` elemento con hello `SecurityTokenServiceType` tipo.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="2cdd3-147">Hello metadatos siguientes muestran un ejemplo `RoleDescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="2cdd3-148">En la sección Hola específica de SAML, un lector de metadatos de WS-Federation leería los certificados de Hola de un `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="2cdd3-149">Hello metadatos siguientes muestran un ejemplo `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="2cdd3-150">No hay ninguna diferencia en formato de Hola de certificados específicos del inquilino e independientes del inquilino.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="2cdd3-151">Dirección URL del punto de conexión de WS-Federation</span><span class="sxs-lookup"><span data-stu-id="2cdd3-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="2cdd3-152">metadatos de federación de Hello incluyen hello dirección URL que es Azure AD usa para el inicio de sesión único y cierre de sesión de protocolo WS-Federation único.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="2cdd3-153">Este punto de conexión aparece en hello `PassiveRequestorEndpoint` elemento.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="2cdd3-154">Hello metadatos siguientes muestran un ejemplo `PassiveRequestorEndpoint` elemento para un extremo específico del inquilino.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="2cdd3-155">Para el extremo independiente del inquilino de hello, Hola URL de WS-Federation aparece en extremo Hola WS-Federation, tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="2cdd3-156">Dirección URL del punto de conexión de protocolo SAML</span><span class="sxs-lookup"><span data-stu-id="2cdd3-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="2cdd3-157">metadatos de federación de Hello incluyen dirección URL de Hola que Azure AD usa para el inicio de sesión único y cierre de sesión en el protocolo SAML 2.0 único.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="2cdd3-158">Estos extremos aparecen en hello `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="2cdd3-159">Hola, inicio de sesión y cierre de sesión, direcciones URL aparecen en hello `SingleSignOnService` y `SingleLogoutService` elementos.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="2cdd3-160">Hello metadatos siguientes muestran un ejemplo `PassiveResistorEndpoint` para un extremo específico del inquilino.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="2cdd3-161">De igual forma extremos de Hola para puntos de conexión de protocolo de SAML 2.0 comunes de Hola se publican en los metadatos de federación independientes del inquilino de hello, tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2cdd3-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
