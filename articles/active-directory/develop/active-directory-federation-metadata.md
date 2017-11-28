---
title: "Metadatos de federación de Azure AD | Microsoft Docs"
description: "En este artículo se describe el documento de metadatos de federación que Azure Active Directory publica para los servicios que aceptan tokens de este directorio."
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
ms.openlocfilehash: ecafb02a6ac13d1c3cd1fe77ef710cd8525e32b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="998ff-103">Metadatos de federación</span><span class="sxs-lookup"><span data-stu-id="998ff-103">Federation metadata</span></span>
<span data-ttu-id="998ff-104">Azure Active Directory (Azure AD) publica un documento de metadatos de federación para los servicios que están configurados para aceptar los tokens de seguridad que emite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="998ff-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured to accept the security tokens that Azure AD issues.</span></span> <span data-ttu-id="998ff-105">El formato del documento de metadatos de federación se describe en la [versión 1.2 del lenguaje de federación de servicios web (WS-Federation)](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), que amplía los [metadatos del lenguaje de marcado de aserción de seguridad (SAML) de la versión 2.0 de OASIS](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="998ff-105">The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="998ff-106">Puntos de conexión de metadatos específicos e independientes del inquilino</span><span class="sxs-lookup"><span data-stu-id="998ff-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="998ff-107">Azure AD publica los extremos específicos del inquilino e independientes del inquilino.</span><span class="sxs-lookup"><span data-stu-id="998ff-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="998ff-108">Los extremos específicos del inquilino están diseñados para un inquilino determinado.</span><span class="sxs-lookup"><span data-stu-id="998ff-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="998ff-109">Los metadatos de federación específicos del inquilino incluyen información sobre el inquilino, incluida la información sobre el emisor y el extremo específica del inquilino.</span><span class="sxs-lookup"><span data-stu-id="998ff-109">The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="998ff-110">Las aplicaciones que restringen el acceso a un solo inquilino utilizan extremos específicos del inquilino.</span><span class="sxs-lookup"><span data-stu-id="998ff-110">Applications that restrict access to a single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="998ff-111">Los extremos independientes del inquilino proporcionan información que es común a todos los inquilinos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="998ff-111">Tenant-independent endpoints provide information that is common to all Azure AD tenants.</span></span> <span data-ttu-id="998ff-112">Esta información se aplica a los inquilinos hospedados en *login.windows.net* y se comparte entre ellos.</span><span class="sxs-lookup"><span data-stu-id="998ff-112">This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="998ff-113">Los extremos independientes del inquilino se recomiendan para aplicaciones de varios inquilinos, ya que no están asociados a ningún inquilino en particular.</span><span class="sxs-lookup"><span data-stu-id="998ff-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="998ff-114">Puntos de conexión de metadatos de federación</span><span class="sxs-lookup"><span data-stu-id="998ff-114">Federation metadata endpoints</span></span>
<span data-ttu-id="998ff-115">Azure AD publica los metadatos de federación en `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="998ff-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="998ff-116">En el caso de los **puntos de conexión específicos del inquilino**, el `TenantDomainName` puede ser uno de los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="998ff-116">For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:</span></span>

* <span data-ttu-id="998ff-117">Un nombre de dominio registrado de un inquilino de Azure AD, como `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="998ff-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="998ff-118">El identificador de inquilino inmutable, como `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="998ff-118">The immutable tenant ID of the domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="998ff-119">En el caso de los **puntos de conexión independientes del inquilino**, `TenantDomainName` es `common`.</span><span class="sxs-lookup"><span data-stu-id="998ff-119">For **tenant-independent endpoints**, the `TenantDomainName` is `common`.</span></span> <span data-ttu-id="998ff-120">En este documento se indica que los elementos de metadatos de federación que son comunes a todos los inquilinos de Azure AD son los únicos que se hospedan en login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="998ff-120">This document lists only the Federation Metadata elements that are common to all Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="998ff-121">Por ejemplo, un punto de conexión específico del inquilino podría ser `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="998ff-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="998ff-122">El punto de conexión independiente del inquilino es [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="998ff-122">The tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="998ff-123">Puede ver el documento de metadatos de federación al escribir esta dirección URL en un explorador.</span><span class="sxs-lookup"><span data-stu-id="998ff-123">You can view the federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="998ff-124">Contenido de los metadatos de federación</span><span class="sxs-lookup"><span data-stu-id="998ff-124">Contents of federation Metadata</span></span>
<span data-ttu-id="998ff-125">La siguiente sección proporciona la información necesaria para los servicios que consumen los tokens emitidos por Azure AD.</span><span class="sxs-lookup"><span data-stu-id="998ff-125">The following section provides information needed by services that consume the tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="998ff-126">El identificador de entidad</span><span class="sxs-lookup"><span data-stu-id="998ff-126">Entity ID</span></span>
<span data-ttu-id="998ff-127">El elemento `EntityDescriptor` contiene un atributo `EntityID`.</span><span class="sxs-lookup"><span data-stu-id="998ff-127">The `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="998ff-128">El valor del atributo `EntityID` representa al emisor; es decir, al servicio de token de seguridad (STS) que emitió el token.</span><span class="sxs-lookup"><span data-stu-id="998ff-128">The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token.</span></span> <span data-ttu-id="998ff-129">Es importante validar al emisor cuando reciba un token.</span><span class="sxs-lookup"><span data-stu-id="998ff-129">It is important to validate the issuer when you receive a token.</span></span>

<span data-ttu-id="998ff-130">Los metadatos siguientes muestran un ejemplo de un elemento `EntityDescriptor` específico del inquilino con un elemento `EntityID`.</span><span class="sxs-lookup"><span data-stu-id="998ff-130">The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="998ff-131">Puede reemplazar el identificador de inquilino del punto de conexión independiente del inquilino por el suyo para crear un valor `EntityID` específico del cliente.</span><span class="sxs-lookup"><span data-stu-id="998ff-131">You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="998ff-132">El valor resultante será el mismo que el emisor del token.</span><span class="sxs-lookup"><span data-stu-id="998ff-132">The resulting value will be the same as the token issuer.</span></span> <span data-ttu-id="998ff-133">Esta estrategia permite a una aplicación de varios inquilinos validar al emisor de un inquilino determinado.</span><span class="sxs-lookup"><span data-stu-id="998ff-133">The strategy allows a multi-tenant application to validate the issuer for a given tenant.</span></span>

<span data-ttu-id="998ff-134">Los metadatos siguientes muestran un ejemplo de un elemento `EntityID` independiente del inquilino.</span><span class="sxs-lookup"><span data-stu-id="998ff-134">The following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="998ff-135">Tenga en cuenta que `{tenant}` es un literal, no un marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="998ff-135">Please note, that the `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="998ff-136">Certificados de firma de tokens</span><span class="sxs-lookup"><span data-stu-id="998ff-136">Token signing certificates</span></span>
<span data-ttu-id="998ff-137">Cuando un servicio recibe un token emitido por un inquilino de Azure AD, la firma del token debe validarse con una clave de firma que se publica en el documento de metadatos de federación.</span><span class="sxs-lookup"><span data-stu-id="998ff-137">When a service receives a token that is issued by a Azure AD tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document.</span></span> <span data-ttu-id="998ff-138">Los metadatos de federación incluyen la parte pública de los certificados que utilizan los inquilinos para la firma de tokens.</span><span class="sxs-lookup"><span data-stu-id="998ff-138">The federation metadata includes the public portion of the certificates that the tenants use for token signing.</span></span> <span data-ttu-id="998ff-139">Los bytes sin formato del certificado aparecen en el elemento `KeyDescriptor` .</span><span class="sxs-lookup"><span data-stu-id="998ff-139">The certificate raw bytes appear in the `KeyDescriptor` element.</span></span> <span data-ttu-id="998ff-140">El certificado de la firma del token es válido para la firma solo cuando el valor del atributo `use` es `signing`.</span><span class="sxs-lookup"><span data-stu-id="998ff-140">The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.</span></span>

<span data-ttu-id="998ff-141">Un documento de metadatos de federación que haya publicado Azure AD puede tener varias claves de firma, como en aquellos casos en que Azure AD se está preparando para actualizar el certificado de firma.</span><span class="sxs-lookup"><span data-stu-id="998ff-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing to update the signing certificate.</span></span> <span data-ttu-id="998ff-142">Cuando un documento de metadatos de federación incluye más de un certificado, un servicio que está validando los tokens debe admitir todos los certificados del documento.</span><span class="sxs-lookup"><span data-stu-id="998ff-142">When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.</span></span>

<span data-ttu-id="998ff-143">Los metadatos siguientes muestran un ejemplo del elemento `KeyDescriptor` con una clave de firma.</span><span class="sxs-lookup"><span data-stu-id="998ff-143">The following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="998ff-144">El elemento `KeyDescriptor` aparece en dos lugares en el documento de metadatos de federación: en la sección específica de WS-Federation y de SAML.</span><span class="sxs-lookup"><span data-stu-id="998ff-144">The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section.</span></span> <span data-ttu-id="998ff-145">Los certificados publicados en ambas secciones serán el mismo.</span><span class="sxs-lookup"><span data-stu-id="998ff-145">The certificates published in both sections will be the same.</span></span>

<span data-ttu-id="998ff-146">En la sección específica de WS-Federation, un lector de metadatos de WS-Federation leería los certificados de un elemento `RoleDescriptor` con el tipo `SecurityTokenServiceType`.</span><span class="sxs-lookup"><span data-stu-id="998ff-146">In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="998ff-147">Los metadatos siguientes muestran un ejemplo del elemento `RoleDescriptor` .</span><span class="sxs-lookup"><span data-stu-id="998ff-147">The following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="998ff-148">En la sección específica de SAML, un lector de metadatos de WS-Federation leería los certificados de un elemento `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="998ff-148">In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="998ff-149">Los metadatos siguientes muestran un ejemplo del elemento `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="998ff-149">The following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="998ff-150">No existen diferencias en el formato de los certificados específicos del inquilino e independientes del inquilino.</span><span class="sxs-lookup"><span data-stu-id="998ff-150">There are no differences in the format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="998ff-151">Dirección URL del punto de conexión de WS-Federation</span><span class="sxs-lookup"><span data-stu-id="998ff-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="998ff-152">Los metadatos de federación incluyen la dirección URL que utiliza Azure AD para el inicio de sesión único y el cierre de sesión único en el protocolo WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="998ff-152">The federation metadata includes the URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="998ff-153">Este punto de conexión aparece en el elemento `PassiveRequestorEndpoint` .</span><span class="sxs-lookup"><span data-stu-id="998ff-153">This endpoint appears in the `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="998ff-154">Los metadatos siguientes muestran un ejemplo del elemento `PassiveRequestorEndpoint` de un punto de conexión específico del inquilino.</span><span class="sxs-lookup"><span data-stu-id="998ff-154">The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="998ff-155">Para el extremo independiente del inquilino, la dirección URL de WS-Federation aparece en el extremo de WS-Federation, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="998ff-155">For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="998ff-156">Dirección URL del punto de conexión de protocolo SAML</span><span class="sxs-lookup"><span data-stu-id="998ff-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="998ff-157">Los metadatos de federación incluyen la dirección URL que utiliza Azure AD para el inicio de sesión único y el cierre de sesión único en el protocolo SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="998ff-157">The federation metadata includes the URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="998ff-158">Estos puntos de conexión aparecen en el elemento `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="998ff-158">These endpoints appear in the `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="998ff-159">Las direcciones URL de inicio y cierre de sesión se muestran en los elementos `SingleSignOnService` y `SingleLogoutService`.</span><span class="sxs-lookup"><span data-stu-id="998ff-159">The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="998ff-160">Los metadatos siguientes muestran un ejemplo de `PassiveResistorEndpoint` para un punto de conexión específico del inquilino.</span><span class="sxs-lookup"><span data-stu-id="998ff-160">The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="998ff-161">Del mismo modo, los extremos comunes del protocolo SAML 2.0 se publican en los metadatos de federación independientes del inquilino, tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="998ff-161">Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
