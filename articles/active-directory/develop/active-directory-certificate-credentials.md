---
title: Credenciales de certificado en Azure AD | Microsoft Docs
description: "Este artículo describe el registro y el uso de credenciales de certificados para la autenticación de aplicaciones"
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
ms.openlocfilehash: 08bb5140bb35bbd120aaa506afeab8ad247f81e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="55970-103">Credenciales de certificado para la autenticación de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="55970-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="55970-104">Azure Active Directory permite que una aplicación use sus propias credenciales para la autenticación, por ejemplo, en el flujo de concesión de credenciales de cliente de OAuth 2.0 y el flujo en nombre de otro.</span><span class="sxs-lookup"><span data-stu-id="55970-104">Azure Active Directory allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow and the On-Behalf-Of flow.</span></span>
<span data-ttu-id="55970-105">Un formato de credencial que se puede utilizar es una aserción de JSON Web Token (JWT) firmada con un certificado que la aplicación posea.</span><span class="sxs-lookup"><span data-stu-id="55970-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span></span>

## <a name="format-of-the-assertion"></a><span data-ttu-id="55970-106">Formato de la aserción</span><span class="sxs-lookup"><span data-stu-id="55970-106">Format of the assertion</span></span>
<span data-ttu-id="55970-107">Para calcular la aserción, es posible que desee utilizar una de las muchas bibliotecas de [JSON Web Token](https://jwt.io/) en el idioma que prefiera.</span><span class="sxs-lookup"><span data-stu-id="55970-107">To compute the assertion, you probably want to use one of the many [JSON Web Token](https://jwt.io/) libraries in the language of your choice.</span></span> <span data-ttu-id="55970-108">La información que lleva el token es:</span><span class="sxs-lookup"><span data-stu-id="55970-108">The information carried by the token is:</span></span>

#### <a name="header"></a><span data-ttu-id="55970-109">Encabezado</span><span class="sxs-lookup"><span data-stu-id="55970-109">Header</span></span>

| <span data-ttu-id="55970-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="55970-110">Parameter</span></span> |  <span data-ttu-id="55970-111">Comentario</span><span class="sxs-lookup"><span data-stu-id="55970-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="55970-112">Debe ser **RS256**</span><span class="sxs-lookup"><span data-stu-id="55970-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="55970-113">Debe ser **JWT**</span><span class="sxs-lookup"><span data-stu-id="55970-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="55970-114">Debe ser la huella digital SHA-1 del certificado X.509</span><span class="sxs-lookup"><span data-stu-id="55970-114">Should be the X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="55970-115">Notificaciones (carga útil)</span><span class="sxs-lookup"><span data-stu-id="55970-115">Claims (Payload)</span></span>

| <span data-ttu-id="55970-116">Parámetro</span><span class="sxs-lookup"><span data-stu-id="55970-116">Parameter</span></span> |  <span data-ttu-id="55970-117">Comentario</span><span class="sxs-lookup"><span data-stu-id="55970-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="55970-118">Público: debe ser **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="55970-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="55970-119">Fecha de expiración: la fecha en que el token expira.</span><span class="sxs-lookup"><span data-stu-id="55970-119">Expiration date: the date when the token expires.</span></span> <span data-ttu-id="55970-120">La hora se representa como el número de segundos desde el 1 de enero de 1970 (1970-01-01T0:0:0Z) UTC hasta el momento en que la validez del token expira.</span><span class="sxs-lookup"><span data-stu-id="55970-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span></span>|
| `iss` | <span data-ttu-id="55970-121">Emisor: debe ser el identificador client_id (identificador de la aplicación del servicio de cliente)</span><span class="sxs-lookup"><span data-stu-id="55970-121">Issuer: should be the client_id (Application Id of the client service)</span></span> |
| `jti` | <span data-ttu-id="55970-122">GUID: el identificador de JWT</span><span class="sxs-lookup"><span data-stu-id="55970-122">GUID: the JWT ID</span></span> |
| `nbf` | <span data-ttu-id="55970-123">No antes de: fecha antes de la cual el token no se puede usar.</span><span class="sxs-lookup"><span data-stu-id="55970-123">Not Before: the date before which the token cannot be used.</span></span> <span data-ttu-id="55970-124">La hora se representa como el número de segundos desde el 1 de enero de 1970 (1970-01-01T0:0:0Z) UTC hasta el momento en que se emitió el token.</span><span class="sxs-lookup"><span data-stu-id="55970-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span></span> |
| `sub` | <span data-ttu-id="55970-125">Asunto: al igual que para `iss`, debe ser el identificador client_id (identificador de la aplicación del servicio de cliente)</span><span class="sxs-lookup"><span data-stu-id="55970-125">Subject: As for `iss`, should be the client_id (Application Id of the client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="55970-126">Firma</span><span class="sxs-lookup"><span data-stu-id="55970-126">Signature</span></span>
<span data-ttu-id="55970-127">La firma se calcula aplicando el certificado como se describe en la [especificación RFC7519 de JSON Web Token](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="55970-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="55970-128">Ejemplo de una aserción de JWT descodificada</span><span class="sxs-lookup"><span data-stu-id="55970-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="55970-129">Ejemplo de una aserción de JWT codificada</span><span class="sxs-lookup"><span data-stu-id="55970-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="55970-130">La cadena siguiente es un ejemplo de aserción codificada.</span><span class="sxs-lookup"><span data-stu-id="55970-130">The following string is an example of encoded assertion.</span></span> <span data-ttu-id="55970-131">Si observa detenidamente, verá tres secciones separadas por puntos (.).</span><span class="sxs-lookup"><span data-stu-id="55970-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="55970-132">La primera sección codifica el encabezado, la segunda la carga útil y la última es la firma calculada con los certificados a partir del contenido de las primeras dos secciones.</span><span class="sxs-lookup"><span data-stu-id="55970-132">The first section encodes the header, the second the payload, and the last is the signature computed with the certificates from the content of the first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="55970-133">Registro del certificado con Azure AD</span><span class="sxs-lookup"><span data-stu-id="55970-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="55970-134">Para asociar las credenciales del certificado con la aplicación de cliente en Azure AD, debe editar el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="55970-134">To associate the certificate credential with the client application in Azure AD, you need to edit the application manifest.</span></span>
<span data-ttu-id="55970-135">Si tiene un certificado, debe calcular:</span><span class="sxs-lookup"><span data-stu-id="55970-135">Having hold of a certificate, you need to compute:</span></span>
- <span data-ttu-id="55970-136">`$base64Thumbprint`, que es la codificación base64 del hash del certificado</span><span class="sxs-lookup"><span data-stu-id="55970-136">`$base64Thumbprint`, which is the base64 encoding of the certificate Hash</span></span>
- <span data-ttu-id="55970-137">`$base64Value`, que es la codificación base64 de los datos sin procesar del certificado</span><span class="sxs-lookup"><span data-stu-id="55970-137">`$base64Value`, which is the base64 encoding of the certificate raw data</span></span>

<span data-ttu-id="55970-138">También deberá proporcionar un GUID para identificar la clave en el manifiesto de la aplicación (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="55970-138">you also need to provide a GUID to identify the key in the application manifest (`$keyId`)</span></span>

<span data-ttu-id="55970-139">En el registro de aplicación de Azure para la aplicación cliente, abra el manifiesto de aplicación y reemplace la propiedad *keyCredentials* con la información del nuevo certificado usando el siguiente esquema:</span><span class="sxs-lookup"><span data-stu-id="55970-139">In the Azure app registration for the client application, open the application manifest, and replace the *keyCredentials* property with your new certificate information using the following schema:</span></span>
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

<span data-ttu-id="55970-140">Guarde las modificaciones en el manifiesto de aplicación y cárguelo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55970-140">Save the edits to the application manifest, and upload to Azure AD.</span></span> <span data-ttu-id="55970-141">La propiedad keyCredentials es multivalor, por lo que puede cargar varios certificados para una administración de claves más eficaz.</span><span class="sxs-lookup"><span data-stu-id="55970-141">The keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
