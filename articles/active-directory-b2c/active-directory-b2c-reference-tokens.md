---
title: 'Azure Active Directory B2C: referencia de tokens | Microsoft Docs'
description: tipos de Hola de tokens emitidos en Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/17/2017
ms.author: dastrock
ms.openlocfilehash: 776bc88cc0308875ac6e576f19ac9edf50319d08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-token-reference"></a>Azure AD B2C: referencia de tokens
Azure Active Directory B2C (Azure AD B2C) emite varios tipos de tokens de seguridad a medida que procesa cada [flujo de autenticación](active-directory-b2c-apps.md). Este documento describe el formato de hello, características de seguridad y el contenido de cada tipo de símbolo (token).

## <a name="types-of-tokens"></a>Tipos de tokens
B2C de Azure AD admite hello [protocolo de autorización de OAuth 2.0](active-directory-b2c-reference-protocols.md), que hace uso de los tokens de acceso y tokens de actualización. También admite la autenticación e inicio de sesión a través de [OpenID Connect](active-directory-b2c-reference-protocols.md), que presenta un tercer tipo de símbolo (token): identificador de token de Hola. Todos estos tokens se representan como un token de portador.

Un token de portador es un token de seguridad ligero que concede Hola tooa de "portador" acceso al recurso protegido. portador de Hello es cualquier entidad que puede presentar el token de Hola. Para que una parte pueda recibir un token de portador, es necesario que Azure AD la autentique previamente. Pero si Hola necesario no se toman medidas toosecure Hola símbolo (token) de transmisión y el almacenamiento, se puede interceptar y utilizado por una entidad no deseada. Algunos tokens de seguridad disponen de un mecanismo integrado para evitar que usuarios no autorizados puedan usarlos, pero los tokens de portador no tienen este mecanismo. Deberán ser transportados en un canal seguro, como Seguridad de la capa de transporte (HTTPS).

Si se transmite un token de portador fuera de un canal seguro, un usuario malintencionado puede usar un token de ataque de man-in-the-middle tooacquire hello y usar recursos de tooa protegido del acceso de toogain no autorizado. Hola mismos principios de seguridad que se aplican cuando se almacena tokens de portador o se almacena en caché para su uso posterior. Asegúrate siempre de que la aplicación transmite y almacena los tokens de portador de manera segura.

Para ver más consideraciones de seguridad relativas a los tokens de portador, consulte la [sección 5 de RFC 6750](http://tools.ietf.org/html/rfc6750).

Muchos de los tokens de Hola que emite Azure AD B2C se implementan como tokens de web JSON (Jwt). Un JWT es un medio compacto y seguro de la dirección URL para transferir información entre dos partes. Los JWT contienen información conocida como notificaciones. Se trata de aserciones de información sobre el portador de Hola y Hola del asunto del token de Hola. notificaciones de Hola de Jwt son objetos JSON que se codifican y se serializan para la transmisión. Porque hello Jwt emitidos por Azure AD B2C está firmado pero no cifrado, fácilmente puede inspeccionar el contenido de Hola de un toodebug JWT se. Hay varias herramientas para hacerlo, entre ellas [calebb.net](http://calebb.net). Para obtener más información acerca de Jwt, consulte demasiado[especificaciones de JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Tokens de identificador
Un identificador de token es una forma de token de seguridad que recibe de la aplicación de Azure AD B2C hello `authorize` y `token` los puntos de conexión. Tokens de identificador se representan como [JWTs](#types-of-tokens), y contienen notificaciones que puede usar tooidentify a los usuarios de la aplicación. Cuando se adquieren los tokens de Id. de hello `authorize` punto de conexión, suelen ser toosign usado en aplicaciones de tooweb de los usuarios. Cuando se adquieren los tokens de Id. de hello `token` punto de conexión, se pueden enviar en solicitudes HTTP durante la comunicación entre dos componentes de hello misma aplicación o servicio. Puede usar notificaciones de hello en un identificador de token como considere oportuno. Únicamente son utilizadas toodisplay cuenta información o toomake decisiones control de acceso en una aplicación.  

Los tokens de identificador están firmados, pero actualmente no están cifrados. Cuando su aplicación o API recibe un identificador de token, debe [validar la firma de hello](#token-validation) tooprove que Hola token es auténtico. Su aplicación o la API también debe validar algunas notificaciones de hello tooprove símbolo (token) que es válido. Según los requisitos de escenario de hello, pueden variar notificaciones Hola validados por una aplicación, pero la aplicación debe realizar algunas [validaciones de notificación comunes](#token-validation) en cada escenario.

#### <a name="sample-id-token"></a>Token de identificador de ejemplo
```
// Line breaks for display purposes only

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IklkVG9rZW5TaWduaW5nS2V5Q29udGFpbmVyIn0.
eyJleHAiOjE0NDIzNjAwMzQsIm5iZiI6MTQ0MjM1NjQzNCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9s
b2dpbi5taWNyb3NvZnRvbmxpbmUuY29tLzc3NTUyN2ZmLTlhMzctNDMwNy04YjNkLWNjMzExZjU4ZDkyNS92
Mi4wLyIsImFjciI6ImIyY18xX3NpZ25faW5fc3RvY2siLCJzdWIiOiJOb3Qgc3VwcG9ydGVkIGN1cnJlbnRs
eS4gVXNlIG9pZCBjbGFpbS4iLCJhdWQiOiI5MGMwZmU2My1iY2YyLTQ0ZDUtOGZiNy1iOGJiYzBiMjlkYzYi
LCJpYXQiOjE0NDIzNTY0MzQsImF1dGhfdGltZSI6MTQ0MjM1NjQzNCwiaWRwIjoiZmFjZWJvb2suY29tIn0.
h-uiKcrT882pSKUtWCpj-_3b3vPs3bOWsESAhPMrL-iIIacKc6_uZrWxaWvIYkLra5czBcGKWrYwrAC8ZvQe
DJWZ50WXQrZYODEW1OUwzaD_I1f1HE0c2uvaWdGXBpDEVdsD3ExKaFlKGjFR2V7F-fPThkVDdKmkUDQX3bVc
yyj2V2nlCQ9jd7aGnokTPfLfpOjuIrTsAdPcGpe5hfSEuwYDmqOJjGs9Jp1f-eSNEiCDQOaTBSvr479L5ptP
XWeQZyX2SypN05Rjr05bjZh3j70ZUimiocfJzjibeoDCaQTz907yAg91WYuFOrQxb-5BaUoR7K-O7vxr2M-_
CQhoFA

```

### <a name="access-tokens"></a>Tokens de acceso
Un token de acceso también es una forma de token de seguridad que recibe de la aplicación de Azure AD B2C hello `authorize` y `token` los puntos de conexión. Tokens de acceso también se representan como [JWTs](#types-of-tokens), y contienen notificaciones que se puede usar hello tooidentify concedido permisos tooyour API. Los tokens de acceso están firmados, pero actualmente no están cifrados. Tokens de acceso deben ser servidores de tooAPIs y recursos de acceso de tooprovide usado. Más información acerca de cómo demasiado[usar tokens de acceso](active-directory-b2c-access-tokens.md). 

Cuando su API recibe un token de acceso, debe [validar la firma de hello](#token-validation) tooprove que Hola token es auténtico. La API también debe validar algunas notificaciones de hello tooprove símbolo (token) que es válido. Según los requisitos de escenario de hello, pueden variar notificaciones Hola validados por una aplicación, pero la aplicación debe realizar algunas [validaciones de notificación comunes](#token-validation) en cada escenario.

### <a name="claims-in-id-and-access-tokens"></a>Notificaciones en los tokens de identificador y de acceso
Cuando se usa Azure AD B2C, tendrá un control específico sobre el contenido de Hola de sus tokens. Puede configurar [directivas](active-directory-b2c-reference-policies.md) toosend cierto conjuntos de datos de usuario en las notificaciones que requiere la aplicación para sus operaciones. Estas notificaciones pueden incluir propiedades estándar como del usuario de hello `displayName` y `emailAddress`. También pueden incluir [atributos de usuario personalizados](active-directory-b2c-reference-custom-attr.md) que se pueden definir en el directorio de B2C. Todos los tokens de identificador y de acceso que reciba contienen un conjunto concreto de notificaciones relacionadas con la seguridad. Las aplicaciones pueden usar estas notificaciones toosecurely autenticar usuarios y solicitudes.

Tenga en cuenta que no se devuelven notificaciones de hello en tokens de identificador en ningún orden concreto. Además, se pueden agregar nuevas notificaciones en tokens de identificador en cualquier momento. No se debe interrumpir la aplicación cuando se agreguen nuevas notificaciones. Estos son Hola de notificaciones que se espera tooexist de acceso y el Id. de tokens emitidos por Azure AD B2C. Las directivas determinan otras notificaciones adicionales. Para practicar, intente inspeccionar notificaciones de hello en el token de Id. de ejemplo de Hola pegándolos en [calebb.net](http://calebb.net). Encontrará más detalles en hello [especificación OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html).

| Nombre | Notificación | Valor de ejemplo | Descripción |
| --- | --- | --- | --- |
| Público |`aud` |`90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6` |Una notificación de audiencia identifica a destinatario Hola prevista del token de Hola. Para Azure AD B2C, Hola está dirigido Id. de aplicación de la aplicación, como aplicación de tooyour asignado en el portal de registro de aplicación Hola. La aplicación debe validar este valor y rechazar el token de hello si no coincide. |
| Emisor |`iss` |`https://login.microsoftonline.com/775527ff-9a37-4307-8b3d-cc311f58d925/v2.0/` |Esta notificación identifica Hola símbolo (token) servicio de seguridad (STS) que construye y devuelve el símbolo (token) de Hola. También identifica el directorio de Azure AD de hello en qué Hola se ha autenticado el usuario. La aplicación debe validar la notificación de emisor de hello tooensure que Hola token procede de extremo v2.0 de hello Azure Active Directory. |
| Emitido a las |`iat` |`1438535543` |Esta notificación es el momento de Hola a qué Hola se emitió el token, representado en tiempo base. |
| Fecha de expiración |`exp` |`1438539443` |Hola notificación de tiempo de expiración es hora de hello en qué Hola símbolo (token) se vuelve no válido, se representan en tiempo. La aplicación debe utilizar este validez de hello tooverify de notificación de duración del token Hola. |
| No antes de |`nbf` |`1438535543` |Esta notificación es el momento de hello en qué Hola símbolo (token) se convierte en válido, se representan en tiempo base. Esto se suele Hola a mismo como Hola tiempo Hola token haya sido emitido. La aplicación debe utilizar este validez de hello tooverify de notificación de duración del token Hola. |
| Versión |`ver` |`1.0` |Esta es la versión de Hola de token de Id. de hello, tal como se define por Azure AD. |
| Código hash |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Un hash de código se incluye en un identificador de token solo cuando se emite el token de hello junto con un código de autorización de OAuth 2.0. Un hash de código puede ser usado toovalidate Hola autenticidad de un código de autorización. Para obtener más información acerca de cómo tooperform esta validación, vea hello [especificación OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html).  |
| Hash de token de acceso |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Un hash de token de acceso se incluye en un identificador de token solo cuando se emite el token de hello junto con un token de acceso de OAuth 2.0. Un hash de token de acceso puede ser usado toovalidate Hola autenticidad de un token de acceso. Para obtener más información acerca de cómo tooperform esta validación, vea hello [especificación OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html)  |
| Valor de seguridad |`nonce` |`12345` |Un nonce es que usa una estrategia mediante ataques de reproducción de tokens de toomitigate. La aplicación puede especificar un valor nonce en una solicitud de autorización mediante hello `nonce` parámetro de consulta. valor de Hola que proporcione en solicitud de saludo se emitirá sin modificar en hello `nonce` de notificación de un identificador de token solo. Esto permite que el valor de aplicación tooverify Hola con valor de hello que lo especificado en la solicitud de hello, que asocia la sesión de la aplicación hello con un determinado identificador de token. La aplicación debe realizar esta validación durante el proceso de validación del token de Id. de Hola. |
| Asunto |`sub` |`884408e1-2918-4cz0-b12d-3aa027d7563b` |Se trata de entidad de seguridad de hello sobre qué Hola token valida información, como el usuario de una aplicación Hola. Este valor es inmutable y no se puede reasignar ni volver a usar. Puede ser usado tooperform las comprobaciones de autorización de forma segura, como cuando el token de Hola se tooaccess usa un recurso. De forma predeterminada, notificación de asunto Hola se rellena con hello Id. de objeto de usuario de hello en el directorio de Hola. más información, consulte toolearn [Azure Active Directory B2C: símbolo (token), la sesión y la configuración de inicio de sesión único](active-directory-b2c-token-session-sso.md). |
| Referencia de clase de contexto de autenticación |`acr` |No aplicable |No se usa actualmente, excepto en el caso de hello de directivas anteriores. más información, consulte toolearn [Azure Active Directory B2C: símbolo (token), la sesión y la configuración de inicio de sesión único](active-directory-b2c-token-session-sso.md). |
| Directiva de marco de confianza |`tfp` |`b2c_1_sign_in` |Este es el nombre de Hola de directiva de Hola que era el token del identificador hello tooacquire usado. |
| Hora de autenticación |`auth_time` |`1438535543` |Esta notificación es el momento de hello en el que un último especificado credenciales de usuario se representan en tiempo base. |

### <a name="refresh-tokens"></a>Tokens de actualización
Actualizar los tokens son tokens de seguridad que la aplicación puede usar tooacquire nuevos tokens de identificador y tokens de acceso en un flujo de OAuth 2.0. Proporcionan la aplicación tooresources de acceso a largo plazo en nombre de los usuarios sin necesidad de interacción con los usuarios.

tooreceive un token de actualización en una respuesta de token, la aplicación debe solicitar hello `offline_acesss` ámbito. más información acerca de hello toolearn `offline_access` ámbito, consulte toohello [referencia del protocolo de Azure AD B2C](active-directory-b2c-reference-protocols.md).

Tokens de actualización son y siempre será, aplicación tooyour completamente opaco. Los emite Azure AD y solo Azure AD los puede inspeccionar e interpretar. Son de larga duración, pero la aplicación no debe escribirse con la expectativa de Hola que un token de actualización durarán durante un período de tiempo específico. Los tokens de actualización pueden invalidarse en cualquier momento por varios motivos. Hola solo tooattempt tooredeem de forma para su tooknow de aplicación si un token de actualización es válido, realizando una tooAzure de solicitud de token AD.

Al canjear un token de actualización para un nuevo token (y si la aplicación se ha concedido hello `offline_access` ámbito), recibirá un nuevo token de actualización en la respuesta de token de Hola. Debe guardar el token de actualización de hello recién emitido. Debe reemplazar el token de actualización de Hola que había utilizado previamente en la solicitud de saludo. Esto ayuda a garantizar que los tokens de actualización sigan siendo válidos mientras sea posible.

## <a name="token-validation"></a>Validación de tokens
toovalidate un token, la aplicación debe comprobar firma hello y notificaciones del token de Hola.

Hay muchas bibliotecas de código abierto disponibles para validar los JWT según su lenguaje preferido. Se recomienda explorar esas opciones en lugar de implementar su propia lógica de validación. información de Hello en esta guía puede ayudarle a aprender cómo tooproperly utilizar dichas bibliotecas.

### <a name="validate-hello-signature"></a>Validar la firma de Hola
Un JWT contiene tres segmentos, separados por hello `.` caracteres. primer segmento de Hello es hello *encabezado*, hello en segundo lugar es hello *cuerpo*, y el tercero, hello es hello *firma*. segmento de firma de Hello puede ser usado toovalidate Hola autenticidad del token de Hola para que lo puede ser de confianza para la aplicación.

Los tokens de Azure AD B2C se firman con algoritmos de cifrado asimétrico estándar del sector, como RSA 256. encabezado de Hello del token de hello contiene información acerca de la clave de Hola y método de cifrado usa el token de Hola toosign:

```
{
        "typ": "JWT",
        "alg": "RS256",
        "kid": "GvnPApfWMdLRi8PDmisFn7bprKg"
}
```

Hola `alg` notificación indica el algoritmo de Hola que era el token de hello toosign usado. Hola `kid` notificación indica la clave pública determinada Hola que era el token de hello toosign usado.

En cualquier momento, Azure AD puede firmar un token mediante cualquiera de un determinado conjunto de pares de claves pública y privada. Azure AD gira posible conjunto de claves de hello periódicamente, por lo que la aplicación debe escribirse toohandle esos clave cambia automáticamente. Un toocheck frecuencia razonable para claves públicas de las actualizaciones toohello usa Azure AD es cada 24 horas.

Azure AD B2C tiene un punto de conexión de metadatos OpenID Connect. Esto permite a las aplicaciones toofetch información acerca de Azure AD B2C en tiempo de ejecución. En esta información se incluyen los extremos, los contenidos del token y las claves de firma de los token. Su directorio B2C contiene un documento de metadatos JSON para cada directiva. Por ejemplo, documento de metadatos de Hola para hello `b2c_1_sign_in` directiva en `fabrikamb2c.onmicrosoft.com` se encuentra en:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in
```

`fabrikamb2c.onmicrosoft.com`es usuario de hello tooauthenticate, que usa directory Hola B2C y `b2c_1_sign_in` es Directiva hello usa el token de hello tooacquire. toodetermine qué directiva era toosign usa un token (y donde toogo toofetch Hola metadatos), tiene dos opciones. En primer lugar, se incluye el nombre de la directiva de Hola Hola `acr` de notificación en el token de Hola. Puede analizar notificaciones del cuerpo de Hola de hello JWT por cuerpo Hola descodificación de Base64 y deserializar Hola que da como resultado de cadena de JSON. Hola `acr` notificación estará formado por nombre de Hola de directiva de Hola que era el token de hello tooissue usado.  La otra opción es la directiva de hello tooencode en valor de Hola de hello `state` parámetro al emitir la solicitud de Hola y decodificarlo toodetermine directiva que se utilizó. Cualquiera de estos métodos es válido.

documento de metadatos de Hello es un objeto JSON que contiene varias piezas útiles de información. Estos incluyen la ubicación de Hola de hello extremos requiere tooperform autenticación OpenID Connect. También incluyen `jwks_uri`, que proporciona la ubicación de Hola de conjunto de Hola de claves públicas que son tokens de toosign usado. Aquí se proporciona esa ubicación, pero es mejor ubicación de hello toofetch dinámicamente mediante el documento de metadatos de Hola y analizar `jwks_uri`:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in
```

documento JSON de Hello ubicado en esta dirección URL contiene todos los Hola información de clave pública en uso en un momento determinado. Puede usar su aplicación Hola `kid` de notificación en hello JWT encabezado tooselect Hola clave pública de documento JSON de hello es toosign usa un símbolo concreto. A continuación, puede realizar la validación de firma mediante una clave pública correcta Hola y Hola indicado algoritmo.

Una descripción de cómo validar la firma tooperform es exterior Hola alcance de este documento. Muchas bibliotecas de código abierto son toohelp disponible con este si se necesita.

### <a name="validate-hello-claims"></a>Validar las reclamaciones de Hola
Cuando su aplicación o API recibe un identificador de token, también debe realizar varias comprobaciones frente a las notificaciones de hello en el token del identificador hello. Estas incluyen, pero no se limitan a:

* Hola **audiencia** de notificación: este modo se comprueba ese token de Id. de hello estaba previsto toobe dado tooyour aplicación.
* Hola **no antes** y **tiempo de expiración** notificaciones: estos comprobar ese token de Id. de hello no ha expirado.
* Hola **emisor** de notificación: este modo se comprueba ese token Hola emitió tooyour aplicación Azure AD.
* Hola **nonce**: se trata de una estrategia de mitigación de ataques de reproducción de tokens.

Para obtener una lista completa de las validaciones que se debe realizar la aplicación, consulte toohello [especificación OpenID Connect](https://openid.net). Detalles de los valores esperados de Hola para estas notificaciones se incluyen en hello anterior [token sección](#types-of-tokens).  

## <a name="token-lifetimes"></a>Vigencia de los tokens
Hola siguiendo la vigencia de los tokens es proporciona toofurther su conocimiento. Pueden ayudarle a desarrollar y depurar aplicaciones. Tenga en cuenta que las aplicaciones no deben estar escrito tooexpect cualquiera de estos constante de tooremain duraciones. Pueden cambiar y lo harán. Obtener más información acerca de hello [personalización de la duración de token de](active-directory-b2c-token-session-sso.md) en Azure AD B2C.

| SWT | Vigencia | Descripción |
| --- | --- | --- |
| Tokens de identificador |Una hora |Los tokens de identificador normalmente son válidos durante una hora. La aplicación web puede usar este toomaintain duración sus propias sesiones con los usuarios (recomendados). También puede elegir una vigencia de sesión diferente. Si la aplicación necesita tooget un nuevo token de identificador, simplemente debe toomake un nuevo tooAzure de solicitud de inicio de sesión de AD. Si un usuario tiene una sesión de explorador válidas con Azure AD, ese usuario podría no ser necesario tooenter credenciales nuevo. |
| Tokens de actualización |Los días de too14 |Un token de actualización solo es válido durante un máximo de 14 días. Pero un token de actualización puede dejar de ser válido en cualquier momento por una serie de motivos. La aplicación debe continuar tootry toouse un token de actualización hasta que se produce un error en la solicitud de hello, o hasta que la aplicación reemplaza el token de actualización de hello con uno nuevo. Un token de actualización también puede volverse no válido si han pasado 90 días desde que el último elemento usuario Hola introducido credenciales. |
| Códigos de autorización |Cinco minutos |Los códigos de autorización son de corta duración intencionadamente. Deben canjearse inmediatamente por tokens de acceso, tokens de identificador o tokens de actualización cuando se reciben. |

