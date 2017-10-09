---
title: "aaaLearn sobre Hola distintos tokens y los tipos compatibles con Azure AD de notificación | Documentos de Microsoft"
description: "Una guía para entender y evaluar las notificaciones de hello en hello SAML 2.0 y tokens de Tokens de Web JSON (JWT) emitidos por Azure Active Directory (AAD)"
documentationcenter: na
author: dstrockis
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 166aa18e-1746-4c5e-b382-68338af921e2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: c512894476613e94d86a994c32a8459d6cf00fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-token-reference"></a>Referencia de tokens de Azure AD
Azure Active Directory (Azure AD) emite varios tipos de tokens de seguridad en el procesamiento de Hola de cada flujo de autenticación. Este documento describe el formato de hello, características de seguridad y el contenido de cada tipo de símbolo (token).

## <a name="types-of-tokens"></a>Tipos de tokens
Azure AD admite hello [protocolo de autorización de OAuth 2.0](active-directory-protocols-oauth-code.md), que hace uso de access_tokens y refresh_tokens.  También admite la autenticación e inicio de sesión a través de [OpenID Connect](active-directory-protocols-openid-connect-code.md), que presenta un tercer tipo de token, id_token Hola.  Todos estos tokens se representan como un "token de portador".

Un token de portador es un token de seguridad ligero que concede Hola tooa de "portador" acceso al recurso protegido. En este sentido, Hola "portador" es cualquier persona que puede presentar el token de Hola. Si se requiere la autenticación con Azure AD en orden tooreceive un token de portador, se deben realizar pasos interceptación toosecure Hola de token, tooprevent por una de las partes no deseada. Porque tokens portadores no tienen un partes de tooprevent no autorizado mecanismo integrado de su uso, deberán ser transportados en un canal seguro, como la seguridad de la capa de transporte (HTTPS). Si se transmite un token de portador en hello claro, un ataque intermedio Hola man en puede ser usado tooacquire Hola token y obtener recursos de tooa protegido del acceso no autorizado. Hola mismos principios de seguridad que se aplican al almacenamiento o almacenamiento en caché de tokens portadores para su uso posterior. Asegúrate siempre de que la aplicación transmite y almacena los tokens de portador de manera segura. Para otras consideraciones sobre la seguridad de los tokens portadores, consulte la [Sección 5 de RFC 6750](http://tools.ietf.org/html/rfc6750).

Muchos de los tokens de hello emitidos por Azure AD se implementan como Tokens Web JSON o Jwt.  Un JWT es un medio compacto y seguro de la dirección URL para transferir información entre dos partes.  información de Hello contenida en los Jwt se conocen como "notificaciones", o aserciones de información acerca de portador de Hola y el asunto del token de Hola.  notificaciones de Hola de Jwt son objetos JSON codificar y serializar para su transmisión.  Puesto que los Jwt de hello emitidos por Azure AD están firmados, pero no cifra, puede inspeccionar fácilmente contenido Hola de un JWT para fines de depuración.  Hay varias herramientas disponibles para hacerlo, como [jwt.calebb.net](http://jwt.calebb.net). Para obtener más información sobre los Jwt, puede hacer referencia a toohello [especificación JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

## <a name="idtokens"></a>Id_Tokens
Los id_tokens son una forma de token de seguridad de inicio de sesión que recibe la aplicación cuando la autenticación se realiza mediante [OpenID Connect](active-directory-protocols-openid-connect-code.md).  Se representan como [JWTs](#types-of-tokens)y contienen notificaciones que puede usar para iniciar la sesión de usuario hello en la aplicación.  Puede usar notificaciones de hello en un id_token como considere oportuno: normalmente se usan para mostrar información de la cuenta o para tomar decisiones de control de acceso en una aplicación.

En ese momento los id_tokens están firmados, pero no cifrados.  Cuando la aplicación recibe un id_token, debe [validar la firma de hello](#validating-tokens) tooprove Hola autenticidad del token y validar las reclamaciones unos en hello token tooprove su validez.  Hello validados por una aplicación de notificaciones varían dependiendo de los requisitos de escenario, pero hay algunos [validaciones de notificación comunes](#validating-tokens) que la aplicación debe realizar en cada escenario.

Vea la siguiente sección para obtener información de notificaciones de id_tokens, así como un id_token de ejemplo de Hola.  Tenga en cuenta que no se devuelven notificaciones de hello en id_tokens en ningún orden concreto.  Además, se pueden introducir nuevas notificaciones en los id_tokens en cualquier momento y no se debe interrumpir la aplicación cuando se introducen nuevas notificaciones.  Hello siguiente lista incluye las notificaciones de Hola que la aplicación puede interpretar de forma confiable en tiempo de Hola de redactar este artículo.  Si es necesario, incluso más detalle puede encontrarse en hello [especificación OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-idtoken"></a>Ejemplo de id_token
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ.
```

> [!TIP]
> Para practicar, intente inspeccionar notificaciones de hello en id_token de ejemplo de Hola pegándolos en [calebb.net](http://jwt.calebb.net).
> 
> 

#### <a name="claims-in-idtokens"></a>Notificaciones en los id_tokens
> [!div class="mx-codeBreakAll"]
| Notificación de JWT | Nombre | Description |
| --- | --- | --- |
| `appid` |Identificador de aplicación |Identifica la aplicación hello que está usando Hola token tooaccess un recurso. aplicación Hello puede actuar por sí misma o en nombre del usuario. Identificador de la aplicación Hello normalmente representa un objeto de aplicación, pero también puede representar un objeto de entidad de seguridad de servicio en Azure AD. <br><br> **Valor de JWT de ejemplo**: <br> `"appid":"15CB020F-3984-482A-864D-1D92265E8268"` |
| `aud` |Público |Hola destinatario del token de Hola. aplicación Hello que recibe el token de hello debe comprobar que el valor de audiencia de hello es correcto y rechazar los tokens destinados a una audiencia diferente. <br><br> **Valor de SAML de ejemplo**: <br> `<AudienceRestriction>`<br>`<Audience>`<br>`https://contoso.com`<br>`</Audience>`<br>`</AudienceRestriction>` <br><br> **Valor de JWT de ejemplo**: <br> `"aud":"https://contoso.com"` |
| `appidacr` |Referencia de clase de contexto de autenticación de aplicación |Indica cómo se autenticó el cliente de Hola. Para un cliente público, el valor de hello es 0. Si se usan los Id. de cliente y el secreto del cliente, el valor de hello es 1. <br><br> **Valor de JWT de ejemplo**: <br> `"appidacr": "0"` |
| `acr` |Referencia de clase de contexto de autenticación |Indica cómo se autenticó el sujeto de hello, como cliente de toohello lugar en la notificación de referencia de clase de contexto de autenticación de aplicación Hola. Un valor de "0" indica la autenticación de usuario final de hello no cumplía los requisitos de Hola de ISO/IEC 29115. <br><br> **Valor de JWT de ejemplo**: <br> `"acr": "0"` |
| Instante de autenticación |Registros Hola fecha y hora en que se realizó la autenticación. <br><br> **Valor de SAML de ejemplo**: <br> `<AuthnStatement AuthnInstant="2011-12-29T05:35:22.000Z">` | |
| `amr` |Método de autenticación |Identifica cómo se autenticó Hola sujeto del token de Hola. <br><br> **Valor de SAML de ejemplo**: <br> `<AuthnContextClassRef>`<br>`http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod/password`<br>`</AuthnContextClassRef>` <br><br> **Valor de JWT de ejemplo**: `“amr”: ["pwd"]` |
| `given_name` |Nombre |Proporciona Hola primero o "el nombre de usuario de hello, especificado" como está establecido en el objeto de usuario de hello Azure AD. <br><br> **Valor de SAML de ejemplo**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname”>`<br>`<AttributeValue>Frank<AttributeValue>` <br><br> **Valor de JWT de ejemplo**: <br> `"given_name": "Frank"` |
| `groups` |Grupos |Proporciona identificadores de objetos que representan la pertenencia a grupos del sujeto Hola. Estos valores son únicos (consulte el Id. de objeto) y se pueden usar para administrar el acceso, como exigir la autorización tooaccess un recurso. grupos de Hello incluidos en la notificación de grupos de Hola se configuran de forma según la aplicación, a través de la propiedad "groupMembershipClaims" de Hola Hola del manifiesto de aplicación. Un valor null excluirá todos los grupos, un valor de "SecurityGroup" incluirá únicamente la pertenencia a grupos de seguridad de Active Directory y un valor de "All" incluirá grupos de seguridad y listas de distribución de Office 365. <br><br> **Valor de SAML de ejemplo**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">`<br>`<AttributeValue>07dd8a60-bf6d-4e17-8844-230b77145381</AttributeValue>` <br><br> **Valor de JWT de ejemplo**: <br> `“groups”: ["0e129f5b-6b0a-4944-982d-f776045632af", … ]` |
| `idp` |Proveedor de identidades |Registros Hola proveedor de identidades que autenticó Hola sujeto del token de Hola. Este valor es valor toohello idénticos de hello emisor de notificaciones a menos que la cuenta de usuario de hello está en un inquilino diferente emisor Hola. <br><br> **Valor de SAML de ejemplo**: <br> `<Attribute Name=” http://schemas.microsoft.com/identity/claims/identityprovider”>`<br>`<AttributeValue>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/<AttributeValue>` <br><br> **Valor de JWT de ejemplo**: <br> `"idp":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `iat` |IssuedAt |Almacena la hora de hello en qué Hola token haya sido emitido. A menudo resulta toomeasure usado actualización del token. <br><br> **Valor de SAML de ejemplo**: <br> `<Assertion ID="_d5ec7a9b-8d8f-4b44-8c94-9812612142be" IssueInstant="2014-01-06T20:20:23.085Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">` <br><br> **Valor de JWT de ejemplo**: <br> `"iat": 1390234181` |
| `iss` |Emisor |Identifica Hola símbolo (token) servicio de seguridad (STS) que construye y devuelve el símbolo (token) de Hola. En los tokens de Hola que devuelve Azure AD, emisor de hello es sts.windows.net. Hello GUID en el valor de notificación de emisor de hello es Hola Id. de inquilino de directorio de Azure AD Hola. Id. de inquilino de Hello es un identificador inmutable y confiable del directorio de Hola. <br><br> **Valor de SAML de ejemplo**: <br> `<Issuer>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/</Issuer>` <br><br> **Valor de JWT de ejemplo**: <br>  `"iss":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `family_name` |Apellido |Proporciona apellido hello, apellido o apellidos del usuario de hello tal como se define en el objeto de usuario de hello Azure AD. <br><br> **Valor de SAML de ejemplo**: <br> `<Attribute Name=” http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname”>`<br>`<AttributeValue>Miller<AttributeValue>` <br><br> **Valor de JWT de ejemplo**: <br> `"family_name": "Miller"` |
| `unique_name` |Nombre |Proporciona un valor legible que identifica a Hola sujeto del token de Hola. Este valor no está garantizado toobe único dentro de un inquilino y está diseñada toobe utilizada solo con fines de visualización. <br><br> **Valor de SAML de ejemplo**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name”>`<br>`<AttributeValue>frankm@contoso.com<AttributeValue>` <br><br> **Valor de JWT de ejemplo**: <br> `"unique_name": "frankm@contoso.com"` |
| `oid` |Id. de objeto |Contiene un identificador único de un objeto en Azure AD. Este valor es inmutable y no se puede reasignar ni volver a usar. Use tooidentify de Id. de objeto de hello un objeto de tooAzure de las consultas AD. <br><br> **Valor de SAML de ejemplo**: <br> `<Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">`<br>`<AttributeValue>528b2ac2-aa9c-45e1-88d4-959b53bc7dd0<AttributeValue>` <br><br> **Valor de JWT de ejemplo**: <br> `"oid":"528b2ac2-aa9c-45e1-88d4-959b53bc7dd0"` |
| `roles` |Roles |Control de acceso representa todos los roles de aplicación Hola asunto se ha concedido directa e indirectamente a través de la pertenencia a grupos y puede ser usado tooenforce basada en roles. Roles de aplicación se definen de forma según la aplicación, a través de hello `appRoles` propiedad Hola del manifiesto de aplicación. Hola `value` propiedad de cada rol de aplicación es el valor de Hola que aparece en la notificación de roles de Hola. <br><br> **Valor de SAML de ejemplo**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">`<br>`<AttributeValue>Admin</AttributeValue>` <br><br> **Valor de JWT de ejemplo**: <br> `“roles”: ["Admin", … ]` |
| `scp` |Scope |Indica la aplicación de cliente de hello suplantación permisos concedidos toohello. permiso de Hello predeterminado es `user_impersonation`. propietario de Hola de hello protegida recursos puede registrar valores adicionales en Azure AD. <br><br> **Valor de JWT de ejemplo**: <br> `"scp": "user_impersonation"` |
| `sub` |Asunto |Identifica la entidad de seguridad de hello sobre qué Hola token valida información, como usuario de Hola de una aplicación. Este valor es inmutable y no se pueden reasignar o volver a usar, por lo que puede ser usado tooperform las comprobaciones de autorización sin ningún riesgo. Porque siempre está presente en el asunto de Hola Hola tokens emite Azure AD de hello, se recomienda usar este valor en un sistema de autorización de uso general. <br> `SubjectConfirmation` no es una notificación. Describe cómo se comprueba el sujeto de Hola de token de Hola. `Bearer`indica que los firmantes de Hola se ha confirmado por medio de su posesión del token de Hola. <br><br> **Valor de SAML de ejemplo**: <br> `<Subject>`<br>`<NameID>S40rgb3XjhFTv6EQTETkEzcgVmToHKRkZUIsJlmLdVc</NameID>`<br>`<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />`<br>`</Subject>` <br><br> **Valor de JWT de ejemplo**: <br> `"sub":"92d0312b-26b9-4887-a338-7b00fb3c5eab"` |
| `tid` |Id. de inquilino |Un identificador inmutable y no reutilizable que identifica el inquilino de directorio de Hola que emitió el token de Hola. Puede utilizar este recurso de directorio específico del inquilino de tooaccess de valor en una aplicación de varios inquilinos. Por ejemplo, puede usar a este inquilino de hello tooidentify de valor en un toohello de llamada de API Graph. <br><br> **Valor de SAML de ejemplo**: <br> `<Attribute Name=”http://schemas.microsoft.com/identity/claims/tenantid”>`<br>`<AttributeValue>cbb1a5ac-f33b-45fa-9bf5-f37db0fed422<AttributeValue>` <br><br> **Valor de JWT de ejemplo**: <br> `"tid":"cbb1a5ac-f33b-45fa-9bf5-f37db0fed422"` |
| `nbf`, `exp` |Vigencia del token |Define el intervalo de tiempo de hello dentro del cual un token es válido. servicio Hola que valida el token de Hola debe comprobar que hello fecha actual está dentro de hello duración del token, else debe rechazar el token de Hola. Hello servicio podría permitir la toofive minutos más allá de tooaccount de intervalo de duración del token de Hola de las diferencias en el tiempo de reloj ("sesgo horario") entre Azure AD y el servicio de Hola. <br><br> **Valor de SAML de ejemplo**: <br> `<Conditions`<br>`NotBefore="2013-03-18T21:32:51.261Z"`<br>`NotOnOrAfter="2013-03-18T22:32:51.261Z"`<br>`>` <br><br> **Valor de JWT de ejemplo**: <br> `"nbf":1363289634, "exp":1363293234` |
| `upn` |Nombre principal de usuario |Nombre de usuario principal de usuario de Hola Hola a almacenes.<br><br> **Valor de JWT de ejemplo**: <br> `"upn": frankm@contoso.com` |
| `ver` |Versión |Almacena el número de versión de Hola de token de Hola. <br><br> **Valor de JWT de ejemplo**: <br> `"ver": "1.0"` |

## <a name="access-tokens"></a>Tokens de acceso
Tras una autenticación correcta, Azure AD devuelve un token de acceso, que puede ser usado tooaccess protegido recursos. token de acceso de Hello es una base 64 con codificación JSON Web Token (JWT) y se puede inspeccionar su contenido mediante la ejecución a través de un descodificador.

Si la aplicación solo *utiliza* tooget acceso tooAPIs los tokens de acceso, se puede (y debe) trata los tokens de acceso como completamente opaco; son simplemente cadenas que su aplicación pasa tooresources en las solicitudes HTTP.

Cuando se solicita un token de acceso, Azure AD también devuelve algunos metadatos sobre el token de acceso de hello para el consumo de la aplicación.  Esta información incluye la hora de expiración Hola de token de acceso de Hola y ámbitos de hello para el que es válido.  Esto permite que su aplicación tooperform inteligente de almacenamiento en caché de tokens de acceso sin necesidad de abrir el token de acceso de hello propio tooparse.

Si la aplicación es una API protegida con Azure AD que espera tokens de acceso en las solicitudes HTTP, debe realizar validación e inspección de tokens de hello que recibirá. La aplicación debe realizar la validación de token de acceso de hello antes de usar recursos de tooaccess. Para obtener más información sobre la validación, consulte [Validación de los tokens](#validating-tokens).  
Para obtener más información sobre cómo toodo esto con. NET, vea [proteger una API Web mediante tokens de portador de Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

## <a name="refresh-tokens"></a>Tokens de actualización

Actualizar tokens son tokens de seguridad, que puede usar su aplicación tooacquire nuevos tokens de acceso en un flujo de OAuth 2.0.  Permite el tooresources de acceso a largo plazo de aplicación tooachieve en nombre del usuario sin requerir la interacción del usuario de Hola.

Los tokens de actualización tienen varios recursos.  Que es toosay que recibe un token de actualización durante una solicitud de token para un recurso se puede canjear para tooa completamente diferentes recursos de tokens de acceso. toodo, Hola conjunto `resource` parámetro hello solicitud toohello recurso de destino.

Tokens de actualización son completamente opacos tooyour aplicación. Son de larga duración, pero la aplicación no debe escribirse tooexpect que un token de actualización durarán durante cualquier período de tiempo.  Los tokens de actualización pueden ser invalidados en cualquier momento por varios motivos.  Hola solo manera para que su tooknow de aplicación si un token de actualización es válido es tooattempt tooredeem, mediante la realización de un extremo de token de solicitud de token tooAzure AD.

Al canjear un token de actualización para un nuevo token de acceso, recibirá un nuevo token de actualización en la respuesta de token de Hola.  Debe guardar símbolo (token) de la actualización de hello recién emitido, reemplazando Hola que usó en la solicitud de saludo.  Esto garantizará que los tokens de actualización sigan siendo válidos mientras sea posible.

## <a name="validating-tokens"></a>Validación de los tokens

En orden toovalidate una id_token o una access_token, la aplicación debe validar notificaciones de hello y firma del token de ambos Hola. En los tokens de acceso de toovalidate de orden, la aplicación también debe validar emisor hello, audiencia de Hola y Hola firmar los tokens. Es necesario toobe valida con respecto a valores de hello en el documento de descubrimiento de hello OpenID. Por ejemplo, se encuentra en la versión independiente de inquilino de Hola de documento de hello [https://login.microsoftonline.com/common/.well-known/openid-configuration](https://login.microsoftonline.com/common/.well-known/openid-configuration). Middleware de Azure AD tiene capacidades integradas para validar los tokens de acceso, y puede examinar a través de nuestro [ejemplos](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-code-samples) toofind en lenguaje de Hola de su elección. Para obtener más información sobre cómo tooexplicitly validar un token JWT, vea hello [manual ejemplo de validación de JWT](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation).  

Se proporcionan las bibliotecas y ejemplos de código que muestran cómo tooeasily administran la validación de token - hello debajo de información simplemente se proporciona para quienes desea hello toounderstand subyacente proceso.  También hay varias bibliotecas de código abierto de terceros para la validación de JWT; hay al menos una opción para casi cualquier plataforma e idioma. Para más información acerca de los ejemplos de código y las bibliotecas de autenticación de Azure AD, consulte [Bibliotecas de autenticación de Azure Active Directory](active-directory-authentication-libraries.md).

#### <a name="validating-hello-signature"></a>Validar la firma de Hola

Un JWT contiene tres segmentos, que están separados por hello `.` caracteres.  primer segmento de Hola se conoce como hello **encabezado**, hello en segundo lugar como hello **cuerpo**, hello en tercer lugar como hello y **firma**.  segmento de firma de Hello puede ser usado toovalidate Hola autenticidad del token de Hola para que lo puede ser de confianza para la aplicación.

Los tokens emitidos por Azure AD se firman con algoritmos de cifrado asimétrico estándar del sector, como RSA 256. encabezado de Hola de hello JWT contiene información acerca de la clave de Hola y método de cifrado usa el token de Hola toosign:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "kriMPdmBvx68skT8-mPAB3BseeA"
}
```

Hola `alg` notificación indica el algoritmo de Hola que era el token de hello toosign utilizados, mientras se realizaba hello `x5t` notificación indica la clave pública determinada Hola que era el token de hello toosign usado.

En cualquier momento, Azure AD puede firmar un id_token mediante cualquiera de un determinado conjunto de pares de claves pública y privada. Azure AD gira el conjunto posibles Hola de claves de forma periódica, por lo que la aplicación debe escribirse toohandle esos clave cambia automáticamente.  Un toocheck frecuencia razonable para claves públicas de las actualizaciones toohello usa Azure AD es cada 24 horas.

Puede adquirir Hola firmar firma de datos de la clave toovalidate necesarios hello mediante el uso de hello OpenID Connect metadatos documento que se encuentra en:

```
https://login.microsoftonline.com/common/.well-known/openid-configuration
```

> [!TIP]
> Pruebe esta dirección URL en un explorador.
> 
> 

Este documento de metadatos es un objeto JSON que contiene varias piezas útiles de información, como la ubicación de Hola de hello varios extremos necesarios para realizar la autenticación de OpenID Connect.  

También incluye un `jwks_uri`, que proporciona la ubicación de Hola de hello del conjunto de claves públicas utiliza toosign símbolos (tokens).  documento JSON de Hello situada hello `jwks_uri` contiene toda la información de clave pública de hello en uso en ese momento determinado.  Puede usar su aplicación Hola `kid` de notificación en hello JWT encabezado tooselect qué clave pública en este documento ha sido toosign usa un símbolo concreto.  A continuación, puede realizar la validación de firma mediante una clave pública correcta Hola y Hola un algoritmo indicado.

Realizar la validación de firma es ámbito de hello fuera de este documento, hay muchas bibliotecas de código abierto disponible para ayudarle a hacerlo si es necesario.

#### <a name="validating-hello-claims"></a>Validación de notificaciones de Hola

Cuando la aplicación recibe un token (una id_token al inicio de sesión de usuario o un token de acceso como un token de portador en la solicitud HTTP de hello) también debe realizar algunas comprobaciones frente a las notificaciones de hello en el token de Hola.  Estas incluyen, pero no se limitan a:

* Hola **audiencia** notificación - tooverify que Hola token estaba previsto toobe dado tooyour aplicación.
* Hola **no antes** y **tiempo de expiración** notificaciones - tooverify que Hola token no ha expirado.
* Hola **emisor** notificación - tooverify que Hola token se emite realmente tooyour aplicación Azure AD.
* Hola **Nonce** -toomitigate un ataque de reproducción de tokens.
* y mucho más...

Para obtener una lista completa de la aplicación debe realizar para los Tokens de Id. de validaciones de notificación, consulte toohello [especificación OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). Detalles de los valores esperados de Hola para estas notificaciones se incluyen en hello anterior [id_token sección](#id-tokens) sección.

## <a name="sample-tokens"></a>Tokens de ejemplo

Esta sección muestra ejemplos de tokens SAML y JWT que Azure AD devuelve. Estos ejemplos le permiten ver notificaciones de hello en contexto.

### <a name="saml-token"></a>Token SAML

Este es un ejemplo de token SAML típico.

    <?xml version="1.0" encoding="UTF-8"?>
    <t:RequestSecurityTokenResponse xmlns:t="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <t:Lifetime>
        <wsu:Created xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T05:15:47.060Z</wsu:Created>
        <wsu:Expires xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T06:15:47.060Z</wsu:Expires>
      </t:Lifetime>
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
          <Address>https://contoso.onmicrosoft.com/MyWebApp</Address>
        </EndpointReference>
      </wsp:AppliesTo>
      <t:RequestedSecurityToken>
        <Assertion xmlns="urn:oasis:names:tc:SAML:2.0:assertion" ID="_3ef08993-846b-41de-99df-b7f3ff77671b" IssueInstant="2014-12-24T05:20:47.060Z" Version="2.0">
          <Issuer>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</Issuer>
          <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
              <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
              <ds:Reference URI="#_3ef08993-846b-41de-99df-b7f3ff77671b">
                <ds:Transforms>
                  <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
                <ds:DigestValue>cV1J580U1pD24hEyGuAxrbtgROVyghCqI32UkER/nDY=</ds:DigestValue>
              </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>j+zPf6mti8Rq4Kyw2NU2nnu0pbJU1z5bR/zDaKaO7FCTdmjUzAvIVfF8pspVR6CbzcYM3HOAmLhuWmBkAAk6qQUBmKsw+XlmF/pB/ivJFdgZSLrtlBs1P/WBV3t04x6fRW4FcIDzh8KhctzJZfS5wGCfYw95er7WJxJi0nU41d7j5HRDidBoXgP755jQu2ZER7wOYZr6ff+ha+/Aj3UMw+8ZtC+WCJC3yyENHDAnp2RfgdElJal68enn668fk8pBDjKDGzbNBO6qBgFPaBT65YvE/tkEmrUxdWkmUKv3y7JWzUYNMD9oUlut93UTyTAIGOs5fvP9ZfK2vNeMVJW7Xg==</ds:SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <X509Data>
                <X509Certificate>MIIDPjCCAabcAwIBAgIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTQwMTAxMDcwMDAwWhcNMTYwMTAxMDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSCWg6q9iYxvJE2NIhSyOiKvqoWCO2GFipgH0sTSAs5FalHQosk9ZNTztX0ywS/AHsBeQPqYygfYVJL6/EgzVuwRk5txr9e3n1uml94fLyq/AXbwo9yAduf4dCHTP8CWR1dnDR+Qnz/4PYlWVEuuHHONOw/blbfdMjhY+C/BYM2E3pRxbohBb3x//CfueV7ddz2LYiH3wjz0QS/7kjPiNCsXcNyKQEOTkbHFi3mu0u13SQwNddhcynd/GTgWN8A+6SN1r4hzpjFKFLbZnBt77ACSiYx+IHK4Mp+NaVEi5wQtSsjQtI++XsokxRDqYLwus1I1SihgbV/STTg5enufuwIDAQABo2IwYDBeBgNVHQEEVzBVgBDLebM6bK3BjWGqIBrBNFeNoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAA4IBAQCJ4JApryF77EKC4zF5bUaBLQHQ1PNtA1uMDbdNVGKCmSp8M65b8h0NwlIjGGGy/unK8P6jWFdm5IlZ0YPTOgzcRZguXDPj7ajyvlVEQ2K2ICvTYiRQqrOhEhZMSSZsTKXFVwNfW6ADDkN3bvVOVbtpty+nBY5UqnI7xbcoHLZ4wYD251uj5+lo13YLnsVrmQ16NCBYq2nQFNPuNJw6t3XUbwBHXpF46aLT1/eGf/7Xx6iy8yPJX4DyrpFTutDz882RWofGEO5t4Cw+zZg70dJ/hH/ODYRMorfXEW+8uKmXMKmX2wyxMKvfiPbTy5LmAU8Jvjs2tLg4rOBcXWLAIarZ</X509Certificate>
              </X509Data>
            </KeyInfo>
          </ds:Signature>
          <Subject>
            <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">m_H3naDei2LNxUmEcWd0BZlNi_jVET1pMLR6iQSuYmo</NameID>
            <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
          </Subject>
          <Conditions NotBefore="2014-12-24T05:15:47.060Z" NotOnOrAfter="2014-12-24T06:15:47.060Z">
            <AudienceRestriction>
              <Audience>https://contoso.onmicrosoft.com/MyWebApp</Audience>
            </AudienceRestriction>
          </Conditions>
          <AttributeStatement>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
              <AttributeValue>a1addde8-e4f9-4571-ad93-3059e3750d23</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/tenantid">
              <AttributeValue>b9411234-09af-49c2-b0c3-653adc1f376e</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
              <AttributeValue>sample.admin@contoso.onmicrosoft.com</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname">
              <AttributeValue>Admin</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname">
              <AttributeValue>Sample</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">
              <AttributeValue>5581e43f-6096-41d4-8ffa-04e560bab39d</AttributeValue>
              <AttributeValue>07dd8a89-bf6d-4e81-8844-230b77145381</AttributeValue>
              <AttributeValue>0e129f4g-6b0a-4944-982d-f776000632af</AttributeValue>
              <AttributeValue>3ee07328-52ef-4739-a89b-109708c22fb5</AttributeValue>
              <AttributeValue>329k14b3-1851-4b94-947f-9a4dacb595f4</AttributeValue>
              <AttributeValue>6e32c650-9b0a-4491-b429-6c60d2ca9a42</AttributeValue>
              <AttributeValue>f3a169a7-9a58-4e8f-9d47-b70029v07424</AttributeValue>
              <AttributeValue>8e2c86b2-b1ad-476d-9574-544d155aa6ff</AttributeValue>
              <AttributeValue>1bf80264-ff24-4866-b22c-6212e5b9a847</AttributeValue>
              <AttributeValue>4075f9c3-072d-4c32-b542-03e6bc678f3e</AttributeValue>
              <AttributeValue>76f80527-f2cd-46f4-8c52-8jvd8bc749b1</AttributeValue>
              <AttributeValue>0ba31460-44d0-42b5-b90c-47b3fcc48e35</AttributeValue>
              <AttributeValue>edd41703-8652-4948-94a7-2d917bba7667</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/identityprovider">
              <AttributeValue>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</AttributeValue>
            </Attribute>
          </AttributeStatement>
          <AuthnStatement AuthnInstant="2014-12-23T18:51:11.000Z">
            <AuthnContext>
              <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
            </AuthnContext>
          </AuthnStatement>
        </Assertion>
      </t:RequestedSecurityToken>
      <t:RequestedAttachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedAttachedReference>
      <t:RequestedUnattachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedUnattachedReference>
      <t:TokenType>http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0</t:TokenType>
      <t:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</t:RequestType>
      <t:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</t:KeyType>
    </t:RequestSecurityTokenResponse>

### <a name="jwt-token---user-impersonation"></a>Token JWT: suplantación de usuario
A continuación se muestra un ejemplo de token web JSON (JWT) típico que se usa en un flujo de concesión de códigos de autorización.
En suma tooclaims, token de hello incluye un número de versión en **ver** y **appidacr**, Hola autenticación contexto referencia de clase, que indica cómo se autenticó el cliente de Hola. Para un cliente público, el valor de hello es 0. Si se usó un Id. de cliente o el secreto del cliente, el valor de hello es 1.

    {
     typ: "JWT",
     alg: "RS256",
     x5t: "kriMPdmBvx68skT8-mPAB3BseeA"
    }.
    {
     aud: "https://contoso.onmicrosoft.com/scratchservice",
     iss: "https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/",
     iat: 1416968588,
     nbf: 1416968588,
     exp: 1416972488,
     ver: "1.0",
     tid: "b9411234-09af-49c2-b0c3-653adc1f376e",
     amr: [
      "pwd"
     ],
     roles: [
      "Admin"
     ],
     oid: "6526e123-0ff9-4fec-ae64-a8d5a77cf287",
     upn: "sample.user@contoso.onmicrosoft.com",
     unique_name: "sample.user@contoso.onmicrosoft.com",
     sub: "yf8C5e_VRkR1egGxJSDt5_olDFay6L5ilBA81hZhQEI",
     family_name: "User",
     given_name: "Sample",
     groups: [
      "0e129f6b-6b0a-4944-982d-f776000632af",
      "323b13b3-1851-4b94-947f-9a4dacb595f4",
      "6e32c250-9b0a-4491-b429-6c60d2ca9a42",
      "f3a161a7-9a58-4e8f-9d47-b70022a07424",
      "8d4c81b2-b1ad-476d-9574-544d155aa6ff",
      "1bf80164-ff24-4866-b19c-6212e5b9a847",
      "76f80127-f2cd-46f4-8c52-8edd8bc749b1",
      "0ba27160-44d0-42b5-b90c-47b3fcc48e35"
     ],
     appid: "b075ddef-0efa-123b-997b-de1337c29185",
     appidacr: "1",
     scp: "user_impersonation",
     acr: "1"
    }.

## <a name="related-content"></a>Contenido relacionado
* Vea hello Azure AD Graph [operaciones de directiva](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) hello y [entidad directiva](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity), toolearn más acerca de cómo administrar la directiva de duración del token a través de hello Azure AD Graph API.
* Para más información y ejemplos acerca de cómo administrar las directivas a través de los cmdlets de PowerShell, incluidos ejemplos, consulte [Configurable Token Lifetimes in Azure Active Directory](../active-directory-configurable-token-lifetimes.md) (Vigencias de tokens configurables en Azure Active Directory). 
