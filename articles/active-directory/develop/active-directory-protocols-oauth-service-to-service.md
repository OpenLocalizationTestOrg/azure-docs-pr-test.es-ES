---
title: "aaaAzure tooService autenticación de servicio de AD mediante OAuth2.0 | Documentos de Microsoft"
description: "Este artículo describe cómo toouse HTTP mensajes tooimplement service autenticación tooservice con flujo de concesión de credenciales de cliente de hello OAuth2.0."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f4bfd4ea8a7de1929c7dcf7ad65a156edff74f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Servicio tooservice llamadas con credenciales de cliente (secreto compartido o certificado)
Hola flujo de la concesión de credenciales de cliente de OAuth 2.0 permite que un servicio web (*cliente confidencial*) toouse sus propias credenciales en lugar de suplantación de un usuario, tooauthenticate cuando se llama a otro servicio web. En este escenario, el cliente de hello normalmente es un servicio web de nivel intermedio, un servicio demonio o un sitio web. Un mayor grado de confianza, Azure AD también permite Hola una llamada a servicio toouse un certificado (en lugar de un secreto compartido) como una credencial.

## Diagrama de flujo de concesión de credenciales de cliente
Hello diagrama siguiente explica cómo las credenciales del cliente hello concesión flujo funciona en Azure Active Directory (Azure AD).

![Flujo de concesión de credenciales de cliente de OAuth2.0](media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. aplicación de cliente de Hello autentica el extremo de emisión de tokens de Azure AD toohello y solicita un token de acceso.
2. problemas de extremos de emisión de tokens de Hello Azure AD Hola token de acceso.
3. token de acceso de Hello es toohello tooauthenticate usado protegida los recursos.
4. Aplicación web de toohello, se devuelven datos de hello protegida los recursos.

## Registrar servicios hello en Azure AD
Registrar llamar al servicio de Hola y Hola recibir servicio en Azure Active Directory (Azure AD). Para obtener más información, consulte [Integración de aplicaciones con Azure Active Directory](active-directory-integrating-applications.md).

## Solicitar un token de acceso
toorequest un token de acceso, use un punto de conexión de HTTP POST toohello específico del inquilino Azure AD.

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## Solicitud de token de acceso entre servicios
Hay dos casos dependiendo de si la aplicación de cliente de hello elige toobe protegido por un secreto compartido o un certificado.

### Primer caso: solicitud de token de acceso con un secreto compartido
Cuando se usa un secreto compartido, una solicitud de token de acceso del servicio a servicio contiene Hola parámetros siguientes:

| Parámetro |  | Descripción |
| --- | --- | --- |
| grant_type |requerido |Especifica Hola solicitado tipo de concesión. En un flujo de concesión de credenciales de cliente, debe ser el valor de hello **client_credentials**. |
| client_id |requerido |Especifica el identificador de cliente de AD Azure Hola de hello llamar al servicio web. Hola toofind Id. de cliente de la aplicación de llamada en hello [portal de Azure](https://portal.azure.com), haga clic en **Active Directory**, cambie el directorio, haga clic en la aplicación hello. Hola client_id es hello *Id. de aplicación* |
| client_secret |requerido |Escriba una clave registrada para hello llamar a la aplicación de demonio o del servicio web en Azure AD. toocreate una clave, Hola portal de Azure, haga clic en **Active Directory**, cambie el directorio, haga clic en la aplicación hello, haga clic en **configuración**, haga clic en **claves**, y agregar una clave.|
| resource |requerido |Escriba Hola App ID URI de Hola recibir el servicio web. Hola toofind App ID URI, Hola portal de Azure, haga clic en **Active Directory**, cambie el directorio, haga clic en la aplicación de servicio de hello y, a continuación, haga clic en **configuración** y **propiedades** |

#### Ejemplo
Hello siguiente HTTP POST solicita un token de acceso para el servicio web de hello https://service.contoso.com/. Hola `client_id` identifica el servicio web de Hola que solicita un token de acceso de Hola.

```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

### Segundo caso: solicitud de token de acceso con un certificado
Una solicitud de token de acceso al servicio con un certificado contiene Hola parámetros siguientes:

| Parámetro |  | Descripción |
| --- | --- | --- |
| grant_type |requerido |Especifica Hola solicita el tipo de respuesta. En un flujo de concesión de credenciales de cliente, debe ser el valor de hello **client_credentials**. |
| client_id |requerido |Especifica el identificador de cliente de AD Azure Hola de hello llamar al servicio web. Hola toofind Id. de cliente de la aplicación de llamada en hello [portal de Azure](https://portal.azure.com), haga clic en **Active Directory**, cambie el directorio, haga clic en la aplicación hello. Hola client_id es hello *Id. de aplicación* |
| client_assertion_type |requerido |debe ser el valor de Hola`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |requerido | Una aserción (un Token Web JSON) que necesita toocreate y el inicio de sesión con hello de certificados se registra como credenciales para la aplicación. Obtenga información sobre [las credenciales del certificado](active-directory-certificate-credentials.md) toolearn cómo tooregister su formato hello y certificado de aserción de Hola.|
| resource | requerido |Escriba Hola App ID URI de Hola recibir el servicio web. Hola toofind App ID URI, Hola portal de Azure, haga clic en **Active Directory**, haga clic en el directorio de hello, haga clic en la aplicación hello y, a continuación, haga clic en **configurar**. |

Tenga en cuenta que los parámetros de hello son casi Hola igual que en el caso de saludo de solicitud de Hola por secreto compartido salvo que el parámetro de hello client_secret se sustituye por dos parámetros: una client_assertion_type y client_assertion.

#### Ejemplo
Hola siguiente HTTP POST solicita un token de acceso de servicio de web https://service.contoso.com/ Hola con un certificado. Hola `client_id` identifica el servicio web de Hola que solicita un token de acceso de Hola.

```
POST /<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

resource=https%3A%2F%contoso.onmicrosoft.com%2Ffc7664b4-cdd6-43e1-9365-c2e1c4e1b3bf&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

### Respuesta de token de acceso entre servicios

Una respuesta correcta contiene una respuesta JSON OAuth 2.0 con hello parámetros siguientes:

| Parámetro | Description |
| --- | --- |
| access_token |símbolo (token) de acceso solicitado Hola. Hola llamar al servicio web puede usar este toohello tooauthenticate token recibir el servicio web. |
| token_type |Indica el valor de tipo de token de Hola. Hola solo tipo que admite Azure AD es **portador**. Para obtener más información acerca de los tokens de portador, vea hello [marco de autorización de OAuth 2.0: uso del Token del portador (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| expires_in |¿Durante cuánto tiempo el token de acceso de hello es válida (en segundos). |
| expires_on |hora de Hello cuando expire el token de acceso de Hola. fecha de Hola se representa como número de Hola de segundos desde 1970-01-01T0:0:0Z UTC hasta el tiempo de expiración de Hola. Este valor es la duración de hello toodetermine uso de tokens almacenados en caché. |
| not_before |hora de Hola desde qué Hola token de acceso pasa a ser utilizable. fecha de Hola se representa como número de Hola de segundos desde 1970-01-01T0:0:0Z UTC hasta el tiempo de validez para el token de Hola.|
| resource |Hola App ID URI de Hola recibir el servicio web. |

#### Ejemplo de respuesta
Hello en el ejemplo siguiente se muestra una solicitud de tooa de respuesta correcta para un servicio web de tooa de token de acceso.

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## Otras referencias
* [OAuth 2.0 en Azure AD](active-directory-protocols-oauth-code.md)
* [En el ejemplo en C# de hello servicio tooservice llamada con un secreto compartido](https://github.com/Azure-Samples/active-directory-dotnet-daemon) y [en el ejemplo en C# de hello servicio tooservice llamada con un certificado](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)
