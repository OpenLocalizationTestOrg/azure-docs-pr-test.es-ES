---
title: credenciales aaaCertificate en Azure AD | Documentos de Microsoft
description: "Este artículo describe el registro de hello y el uso de credenciales de certificado para la autenticación de la aplicación"
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="d47c8-103">Credenciales de certificado para la autenticación de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d47c8-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="d47c8-104">Azure Active Directory permite un toouse aplicación sus propias credenciales para la autenticación, por ejemplo, en el flujo de concesión de credenciales de cliente de OAuth 2.0 de Hola y Hola en nombre de flujo.</span><span class="sxs-lookup"><span data-stu-id="d47c8-104">Azure Active Directory allows an application toouse its own credentials for authentication, for example, in hello OAuth 2.0 Client Credentials Grant flow and hello On-Behalf-Of flow.</span></span>
<span data-ttu-id="d47c8-105">Una forma de credencial que se puede utilizar es una aserción de JSON Web Token(JWT) firmada con un certificado que posee la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d47c8-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that hello application owns.</span></span>

## <a name="format-of-hello-assertion"></a><span data-ttu-id="d47c8-106">Formato de aserción de Hola</span><span class="sxs-lookup"><span data-stu-id="d47c8-106">Format of hello assertion</span></span>
<span data-ttu-id="d47c8-107">aserción de hello toocompute, probablemente desee toouse uno Hola muchos [JSON Web Token](https://jwt.io/) bibliotecas en lenguaje de Hola de su elección.</span><span class="sxs-lookup"><span data-stu-id="d47c8-107">toocompute hello assertion, you probably want toouse one of hello many [JSON Web Token](https://jwt.io/) libraries in hello language of your choice.</span></span> <span data-ttu-id="d47c8-108">información de Hello pertenecientes a token hello es:</span><span class="sxs-lookup"><span data-stu-id="d47c8-108">hello information carried by hello token is:</span></span>

#### <a name="header"></a><span data-ttu-id="d47c8-109">Encabezado</span><span class="sxs-lookup"><span data-stu-id="d47c8-109">Header</span></span>

| <span data-ttu-id="d47c8-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d47c8-110">Parameter</span></span> |  <span data-ttu-id="d47c8-111">Comentario</span><span class="sxs-lookup"><span data-stu-id="d47c8-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="d47c8-112">Debe ser **RS256**</span><span class="sxs-lookup"><span data-stu-id="d47c8-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="d47c8-113">Debe ser **JWT**</span><span class="sxs-lookup"><span data-stu-id="d47c8-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="d47c8-114">Debe ser la huella digital de X.509 certificado SHA-1 de Hola</span><span class="sxs-lookup"><span data-stu-id="d47c8-114">Should be hello X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="d47c8-115">Notificaciones (carga útil)</span><span class="sxs-lookup"><span data-stu-id="d47c8-115">Claims (Payload)</span></span>

| <span data-ttu-id="d47c8-116">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d47c8-116">Parameter</span></span> |  <span data-ttu-id="d47c8-117">Comentario</span><span class="sxs-lookup"><span data-stu-id="d47c8-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="d47c8-118">Público: debe ser **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="d47c8-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="d47c8-119">Fecha de expiración: fecha de hello cuando expire el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47c8-119">Expiration date: hello date when hello token expires.</span></span> <span data-ttu-id="d47c8-120">hora de Hola se representa como número de Hola de segundos desde el 1 de enero de 1970 (1970-01-01T0:0:0Z) UTC hasta que expire la validez del token Hola Hola tiempo.</span><span class="sxs-lookup"><span data-stu-id="d47c8-120">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token validity expires.</span></span>|
| `iss` | <span data-ttu-id="d47c8-121">Emisor: debe ser hello client_id (Id. de aplicación de servicio de cliente de hello)</span><span class="sxs-lookup"><span data-stu-id="d47c8-121">Issuer: should be hello client_id (Application Id of hello client service)</span></span> |
| `jti` | <span data-ttu-id="d47c8-122">GUID: Hola Id. de JWT</span><span class="sxs-lookup"><span data-stu-id="d47c8-122">GUID: hello JWT ID</span></span> |
| `nbf` | <span data-ttu-id="d47c8-123">No antes: Hola fecha antes de que hello no se puede usar el símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="d47c8-123">Not Before: hello date before which hello token cannot be used.</span></span> <span data-ttu-id="d47c8-124">hora de Hola se representa como número de Hola de segundos desde el 1 de enero de 1970 (1970-01-01T0:0:0Z) UTC hasta Hola tiempo Hola token haya sido emitido.</span><span class="sxs-lookup"><span data-stu-id="d47c8-124">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token was issued.</span></span> |
| `sub` | <span data-ttu-id="d47c8-125">Asunto: como para `iss`, debe ser hello client_id (Id. de aplicación de servicio de cliente de hello)</span><span class="sxs-lookup"><span data-stu-id="d47c8-125">Subject: As for `iss`, should be hello client_id (Application Id of hello client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="d47c8-126">Firma</span><span class="sxs-lookup"><span data-stu-id="d47c8-126">Signature</span></span>
<span data-ttu-id="d47c8-127">firma de Hola se calcula aplicando certificado Hola tal y como se describe en hello [especificación de JSON Web Token RFC7519](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="d47c8-127">hello signature is computed applying hello certificate as described in hello [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="d47c8-128">Ejemplo de una aserción de JWT descodificada</span><span class="sxs-lookup"><span data-stu-id="d47c8-128">Example of a decoded JWT assertion</span></span>
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="d47c8-129">Ejemplo de una aserción de JWT codificada</span><span class="sxs-lookup"><span data-stu-id="d47c8-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="d47c8-130">Hola después de la cadena es un ejemplo de aserción codificado.</span><span class="sxs-lookup"><span data-stu-id="d47c8-130">hello following string is an example of encoded assertion.</span></span> <span data-ttu-id="d47c8-131">Si observa detenidamente, verá tres secciones separadas por puntos (.).</span><span class="sxs-lookup"><span data-stu-id="d47c8-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="d47c8-132">primera sección de Hello codifica Hola encabezado, Hola segundo Hola carga, y hello en último lugar es signatura de hello calculada por certificados de Hola de contenido de Hola de dos primeras secciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="d47c8-132">hello first section encodes hello header, hello second hello payload, and hello last is hello signature computed with hello certificates from hello content of hello first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="d47c8-133">Registro del certificado con Azure AD</span><span class="sxs-lookup"><span data-stu-id="d47c8-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="d47c8-134">credencial de certificado de hello tooassociate con la aplicación de cliente de hello en Azure AD, deberá manifiesto de aplicación de tooedit Hola.</span><span class="sxs-lookup"><span data-stu-id="d47c8-134">tooassociate hello certificate credential with hello client application in Azure AD, you need tooedit hello application manifest.</span></span>
<span data-ttu-id="d47c8-135">Tiene la suspensión de un certificado, debe toocompute:</span><span class="sxs-lookup"><span data-stu-id="d47c8-135">Having hold of a certificate, you need toocompute:</span></span>
- <span data-ttu-id="d47c8-136">`$base64Thumbprint`, que es Hola codificación base64 del certificado de hello Hash</span><span class="sxs-lookup"><span data-stu-id="d47c8-136">`$base64Thumbprint`, which is hello base64 encoding of hello certificate Hash</span></span>
- <span data-ttu-id="d47c8-137">`$base64Value`, que es Hola codificación base64 de datos sin procesar del certificado Hola</span><span class="sxs-lookup"><span data-stu-id="d47c8-137">`$base64Value`, which is hello base64 encoding of hello certificate raw data</span></span>

<span data-ttu-id="d47c8-138">También necesita una clave de hello tooidentify GUID en el manifiesto de aplicación Hola tooprovide (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="d47c8-138">you also need tooprovide a GUID tooidentify hello key in hello application manifest (`$keyId`)</span></span>

<span data-ttu-id="d47c8-139">En el registro de aplicación de Azure para la aplicación de cliente de Hola Hola, abra el manifiesto de aplicación de Hola y reemplace hello *keyCredentials* propiedad con la información del nuevo certificado con hello después de esquema:</span><span class="sxs-lookup"><span data-stu-id="d47c8-139">In hello Azure app registration for hello client application, open hello application manifest, and replace hello *keyCredentials* property with your new certificate information using hello following schema:</span></span>
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

<span data-ttu-id="d47c8-140">Guardar el manifiesto de aplicación de hello ediciones toohello y cargar tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="d47c8-140">Save hello edits toohello application manifest, and upload tooAzure AD.</span></span> <span data-ttu-id="d47c8-141">propiedad de credenciales de clave de Hello es multivalor, por lo que puede cargar varios certificados para una administración de claves.</span><span class="sxs-lookup"><span data-stu-id="d47c8-141">hello keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
