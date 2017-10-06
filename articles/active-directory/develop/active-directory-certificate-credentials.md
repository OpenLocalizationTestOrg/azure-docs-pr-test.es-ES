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
# <a name="certificate-credentials-for-application-authentication"></a>Credenciales de certificado para la autenticación de aplicaciones

Azure Active Directory permite un toouse aplicación sus propias credenciales para la autenticación, por ejemplo, en el flujo de concesión de credenciales de cliente de OAuth 2.0 de Hola y Hola en nombre de flujo.
Una forma de credencial que se puede utilizar es una aserción de JSON Web Token(JWT) firmada con un certificado que posee la aplicación hello.

## <a name="format-of-hello-assertion"></a>Formato de aserción de Hola
aserción de hello toocompute, probablemente desee toouse uno Hola muchos [JSON Web Token](https://jwt.io/) bibliotecas en lenguaje de Hola de su elección. información de Hello pertenecientes a token hello es:

#### <a name="header"></a>Encabezado

| Parámetro |  Comentario |
| --- | --- | --- |
| `alg` | Debe ser **RS256** |
| `typ` | Debe ser **JWT** |
| `x5t` | Debe ser la huella digital de X.509 certificado SHA-1 de Hola |

#### <a name="claims-payload"></a>Notificaciones (carga útil)

| Parámetro |  Comentario |
| --- | --- | --- |
| `aud` | Público: debe ser **https://login.microsoftonline.com/*tenant_Id*/oauth2/token** |
| `exp` | Fecha de expiración: fecha de hello cuando expire el token de Hola. hora de Hola se representa como número de Hola de segundos desde el 1 de enero de 1970 (1970-01-01T0:0:0Z) UTC hasta que expire la validez del token Hola Hola tiempo.|
| `iss` | Emisor: debe ser hello client_id (Id. de aplicación de servicio de cliente de hello) |
| `jti` | GUID: Hola Id. de JWT |
| `nbf` | No antes: Hola fecha antes de que hello no se puede usar el símbolo (token). hora de Hola se representa como número de Hola de segundos desde el 1 de enero de 1970 (1970-01-01T0:0:0Z) UTC hasta Hola tiempo Hola token haya sido emitido. |
| `sub` | Asunto: como para `iss`, debe ser hello client_id (Id. de aplicación de servicio de cliente de hello) |

#### <a name="signature"></a>Firma
firma de Hola se calcula aplicando certificado Hola tal y como se describe en hello [especificación de JSON Web Token RFC7519](https://tools.ietf.org/html/rfc7519)

### <a name="example-of-a-decoded-jwt-assertion"></a>Ejemplo de una aserción de JWT descodificada
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

### <a name="example-of-an-encoded-jwt-assertion"></a>Ejemplo de una aserción de JWT codificada
Hola después de la cadena es un ejemplo de aserción codificado. Si observa detenidamente, verá tres secciones separadas por puntos (.).
primera sección de Hello codifica Hola encabezado, Hola segundo Hola carga, y hello en último lugar es signatura de hello calculada por certificados de Hola de contenido de Hola de dos primeras secciones de Hola.
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a>Registro del certificado con Azure AD
credencial de certificado de hello tooassociate con la aplicación de cliente de hello en Azure AD, deberá manifiesto de aplicación de tooedit Hola.
Tiene la suspensión de un certificado, debe toocompute:
- `$base64Thumbprint`, que es Hola codificación base64 del certificado de hello Hash
- `$base64Value`, que es Hola codificación base64 de datos sin procesar del certificado Hola

También necesita una clave de hello tooidentify GUID en el manifiesto de aplicación Hola tooprovide (`$keyId`)

En el registro de aplicación de Azure para la aplicación de cliente de Hola Hola, abra el manifiesto de aplicación de Hola y reemplace hello *keyCredentials* propiedad con la información del nuevo certificado con hello después de esquema:
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

Guardar el manifiesto de aplicación de hello ediciones toohello y cargar tooAzure AD. propiedad de credenciales de clave de Hello es multivalor, por lo que puede cargar varios certificados para una administración de claves.
