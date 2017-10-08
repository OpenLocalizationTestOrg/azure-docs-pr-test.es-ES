---
title: "Inicio de sesión web con OpenID Connect - Azure AD B2C | Microsoft Docs"
description: "Creación de aplicaciones web mediante el uso de la implementación de Azure Active Directory Hola Hola OpenID Connect del protocolo de autenticación"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 21d420c8-3c10-4319-b681-adf2e89e7ede
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 89e9cfa28e4e5c34304aea355cca2dd0c4b42abc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-web-sign-in-with-openid-connect"></a>Azure Active Directory B2C: inicio de sesión web con OpenID Connect
OpenID Connect es un protocolo de autenticación, que se basa en OAuth 2.0, que pueden ser usuarios de inicio de sesión de toosecurely usado en aplicaciones de tooweb. De forma con hello Azure Active Directory B2C (Azure AD B2C) implementación de OpenID Connect, externalizar la suscripción, inicio de sesión y otra administración de identidad se produce en su tooAzure de aplicaciones web Active Directory (Azure AD). Esta guía le mostrará cómo toodo de una manera independiente del lenguaje. Describe cómo toosend y recibir mensajes HTTP sin usar cualquiera de nuestras bibliotecas de código abierto.

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) extiende hello OAuth 2.0 *autorización* protocolo para su uso como un *autenticación* protocolo. Esto le permite tooperform inicio de sesión único mediante el uso de OAuth. Introduce el concepto de Hola de un *identificador de token*, que es un token de seguridad que permita Hola cliente tooverify Hola la identidad del usuario de Hola y obtenga información del perfil básica acerca del usuario de Hola.

Puesto que amplía OAuth 2.0, también permite que las aplicaciones adquirir toosecurely *tokens de acceso*. Puede usar access_tokens tooaccess recursos que están protegidos por un [servidor de autorización](active-directory-b2c-reference-protocols.md#the-basics). Nosotros recomendamos OpenID Connect si va a crear una aplicación web que esté hospedada en un servidor y a la que se accede mediante un explorador. Si desea tooadd identity management tooyour aplicaciones móviles o escritorio mediante el uso de Azure AD B2C, debe usar [OAuth 2.0](active-directory-b2c-reference-oauth-code.md) en lugar de OpenID Connect.

Azure AD B2C amplía Hola estándar toodo protocolo OpenID Connect más de autorización y autenticación simples. Introduce hello [parámetro policy](active-directory-b2c-reference-policies.md), lo que permite experiencias de usuario de tooadd OpenID Connect toouse--como inicio de sesión, inicio de sesión y la administración de perfiles--tooyour aplicación. En este caso, le mostramos cómo toouse tooimplement de OpenID Connect y las directivas de cada una de estas experiencias en sus aplicaciones web. También le mostraremos cómo tooget los tokens de acceso para tener acceso a las API de web.

las solicitudes de ejemplo HTTP de Hello en la sección siguiente Hola usar nuestro directorio B2C de ejemplo, fabrikamb2c.onmicrosoft.com, así como nuestra aplicación de ejemplo, https://aadb2cplayground.azurewebsites.net y directivas. Tiene la posibilidad de tootry out Hola solicita usted mismo utilizando estos valores o reemplazarlos por los suyos propios.
Obtenga información acerca de cómo demasiado[obtener su propio inquilino B2C, aplicaciones y directivas](#use-your-own-b2c-directory).

## <a name="send-authentication-requests"></a>Envío de solicitudes de autenticación
Cuando la aplicación web necesita el usuario de hello tooauthenticate y ejecutar una directiva, puede dirigir Hola usuario toohello `/authorize` punto de conexión. Es Hola parte interactiva del flujo de Hola donde usuario Hola realiza una acción, dependiendo de la directiva de Hola.

En esta solicitud, cliente hello indica permisos de Hola que necesita tooacquire de usuario de Hola Hola `scope` tooexecute de directiva de hello y parámetro en hello `p` parámetro. Se proporcionan tres ejemplos en hello siguientes secciones (con saltos de línea para mejorar la legibilidad), cada uno utilizan una directiva diferente. tooget una idea de cómo funciona cada solicitud, intente la solicitud de Hola de pegado en un explorador y ejecutarlo.

#### <a name="use-a-sign-in-policy"></a>Uso de una directiva de inicio de sesión
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

#### <a name="use-a-sign-up-policy"></a>Uso de una directiva de registro
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

#### <a name="use-an-edit-profile-policy"></a>Uso de una directiva de edición de perfil
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parámetro | ¿Necesario? | Description |
| --- | --- | --- |
| client_id |Obligatorio |aplicación Hello identificador ese hello [portal de Azure](https://portal.azure.com/) asignado tooyour aplicación. |
| response_type |Obligatorio |tipo de respuesta de Hello, que debe incluir un identificador de token de OpenID Connect. Si su aplicación web también necesita tokens para llamar a una API web, puede usar `code+id_token`, como hemos hecho aquí. |
| redirect_uri |Recomendado |Hola `redirect_uri` parámetro de la aplicación, donde las respuestas de autenticación pueden ser enviadas y recibidas por la aplicación. Debe coincidir exactamente con uno de hello `redirect_uri` parámetros que registró en el portal de hello, excepto en que debe ser la dirección URL codificada. |
| ámbito |Obligatorio |Una lista de ámbitos separada por espacios. Un valor de ámbito único indica tooAzure AD ambos permisos que se ha solicitado. Hola `openid` ámbito indica una toosign permiso en los datos de usuario y get de hello acerca del usuario de hello en forma de Hola de tokens de identificador (toocome más sobre esto más adelante en el artículo de hello). Hola `offline_access` ámbito es opcional para las aplicaciones web. Indica que la aplicación necesitará una *token de actualización* para tooresources de acceso de larga duración. |
| response_mode |Recomendado |método Hello que debe ser usado toosend Hola resultante autorización código tooyour back-app. Puede ser `query`, `form_post` o `fragment`.  Hola `form_post` se recomienda el modo de respuesta para una mayor seguridad. |
| state |Recomendado |Un valor incluido en la solicitud de Hola que también se devuelve como respuesta de token de Hola. Puede ser una cadena de cualquier contenido que desee. Se utiliza normalmente un valor único generado de forma aleatoria para evitar los ataques de falsificación de solicitudes entre sitios. estado de Hello también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de producirse la solicitud de autenticación de hello, como se encontraban en la página de Hola. |
| valor de seguridad |Obligatorio |Un valor incluido en la solicitud de hello (generado por la aplicación hello) que se incluirán en el token de identificador resultante de hello como una notificación. aplicación Hello, a continuación, puede comprobar que los ataques de reproducción de tokens de toomitigate este valor. valor de Hello normalmente es una cadena única aleatoria que puede ser usado tooidentify Hola origen de solicitud de Hola. |
| p |Obligatorio |Directiva de Hola que se va a ejecutar. Se trata Hola nombre de una directiva que se crea en el inquilino B2C. valor de nombre de directiva de Hello debe comenzar por `b2c\_1\_`. Obtener más información acerca de las directivas y hello [marco de directivas extensible](active-directory-b2c-reference-policies.md). |
| símbolo del sistema |Opcional |tipo de Hello de interacción del usuario que es necesario. Hola valor solo es válido en este momento es `login`, que fuerza Hola tooenter usuario sus credenciales en esa solicitud. El inicio de sesión único no surtirá efecto. |

En este momento, usuario Hola se solicita el flujo de trabajo de la directiva de toocomplete Hola. Ello puede significar tener a usuario Hola escribir su nombre de usuario y una contraseña, inicio de sesión con una identidad de redes sociales, registrarse para el directorio de Hola o cualquier otro número de pasos, dependiendo de cómo se define la directiva de Hola.

Al finalizar usuario Hola directiva hello, Azure AD devuelve una aplicación de tooyour de respuesta en hello indicado `redirect_uri` parámetro, utilizando el método hello descrito en hello `response_mode` parámetro. respuesta de Hello es Hola mismo para cada uno de hello delante de los casos, independientemente de la directiva de Hola que se ejecuta.

Una respuesta correcta al usar `response_mode=fragment` tiene el siguiente aspecto:

```
GET https://aadb2cplayground.azurewebsites.net/#
id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parámetro | Description |
| --- | --- |
| ID_token |Hello Id. de símbolo (token) que solicita la aplicación hello. Puede usar identidad de usuario de hello identificador tooverify token hello y empezar una sesión de usuario de Hola. Obtener más detalles sobre los tokens de identificador y su contenido se incluyen en hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md). |
| código |Hello autorización código de esa aplicación hello solicitada, si usó `response_type=code+id_token`. aplicación Hello puede utilizar toorequest de código de autorización de hello un token de acceso para un recurso de destino. Los códigos de autorización tienen una duración muy breve. Normalmente, caducan al cabo de unos 10 minutos. |
| state |Si un `state` parámetro se incluye en la solicitud de hello, hello mismo valor aparecerán en la respuesta de Hola. Hello aplicación debe comprobar que hello `state` valores de hello solicitud y respuesta son idénticos. |

Las respuestas de error también pueden enviarse toohello `redirect_uri` parámetro de forma que pueda controlar esa aplicación hello correctamente:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen y que puede ser usado tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudar a un desarrollador para identificar la causa de Hola de un error de autenticación. |
| state |Consulte la descripción completa de hello en la primera tabla de hello en esta sección. Si un `state` parámetro se incluye en la solicitud de hello, hello mismo valor aparecerán en la respuesta de Hola. Hello aplicación debe comprobar que hello `state` valores de hello solicitud y respuesta son idénticos. |

## <a name="validate-hello-id-token"></a>Validar el token del identificador hello
Simplemente recibe un identificador de token no es suficiente usuario de hello tooauthenticate. Debe validar la firma del token de Id. de Hola y Hola notificaciones en el token de hello según los requisitos de la aplicación. Usa Azure AD B2C [Tokens de Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) y públicos tokens toosign de criptografía de clave y compruebe que son válidos.

Hay muchas bibliotecas de código abierto disponibles para validar los JWT, según el lenguaje de preferencia. Se recomienda explorar esas opciones en lugar de implementar su propia lógica de validación. información de Hello aquí será útil averiguar cómo tooproperly utilizar dichas bibliotecas.

Azure AD B2C tiene un extremo de metadatos OpenID Connect, que permite a una aplicación toofetch obtener información acerca de Azure AD B2C en tiempo de ejecución. En esta información se incluyen los extremos, los contenidos del token y las claves de firma de los token. Hay un documento de metadatos JSON para cada directiva en su inquilino de B2C. Por ejemplo, documento de metadatos de Hola para hello `b2c_1_sign_in` directiva en `fabrikamb2c.onmicrosoft.com` se encuentra en:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Una de las propiedades de Hola de este documento de configuración es `jwks_uri`, cuyo valor de hello sería la misma directiva:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`.

toodetermine directiva que se usó en la firma de un identificador de token (y desde donde toofetch Hola metadatos), tiene dos opciones. En primer lugar, se incluye el nombre de la directiva de Hola Hola `acr` de notificación en el token del identificador hello. Para obtener información sobre cómo tooparse Hola notificaciones desde un identificador de token, consulte hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md). La otra opción es la directiva de hello tooencode en valor de Hola de hello `state` parámetro al emitir la solicitud de Hola y decodificarlo toodetermine directiva que se utilizó. Cualquiera de estos métodos es válido.

Una vez que haya adquirido el documento de metadatos de hello del extremo de metadatos de OpenID Connect de hello, puede usar las claves públicas RSA 256 hello (que se encuentran en este punto de conexión) firma de hello toovalidate del token de Id. de Hola. Podría haber varias claves enumeradas en este punto de conexión en cualquier momento, cada una identificada con una notificación `kid`. Hello encabezado de token de Id. de hello también contiene un `kid` de notificación, que indica cuál de estas claves se usa toosign Hola identificador de token. Para obtener más información, vea hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md) (Hola sección en [validar los tokens](active-directory-b2c-reference-tokens.md#token-validation), en particular).
<!--TODO: Improve hello information on this-->

Una vez haya validado firma Hola de token de Id. de hello, hay varias notificaciones que necesita tooverify. Por ejemplo:

* Debe validar hello `nonce` tooprevent ataques de reproducción de tokens de notificaciones. Su valor debe ser lo que hayas especificado en una solicitud de inicio de sesión Hola.
* Debe validar hello `aud` tooensure que Hola identificador de token haya sido emitido para la aplicación de notificaciones. Su valor debe ser el identificador de la aplicación hello de la aplicación.
* Debe validar hello `iat` y `exp` notificaciones tooensure que Hola identificador de token no ha expirado.

También hay otras validaciones que deberá llevar a cabo. Se describen en detalle en hello [especificación de OpenID conectarse Core](http://openid.net/specs/openid-connect-core-1_0.html).  Puede que le interese toovalidate notificaciones adicionales, según el escenario. Algunas validaciones comunes incluyen:

* Asegurarse de que Hola usuario u organización ha registrado para la aplicación hello.
* Asegurarse de que el usuario hello tiene autorización o los privilegios adecuados.
* Asegurarse de que se haya producido un determinado nivel de autenticación, como Azure Multi-Factor Authentication.

Para obtener más información sobre notificaciones de hello en un identificador de token, consulte hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md).

Una vez que haya validado el token del identificador hello, puede comenzar una sesión por usuario de Hola. Puede usar notificaciones de hello en información de símbolo (token) tooobtain de Id. de hello acerca del usuario de hello en la aplicación. Entre los usos de esta información se incluye la visualización, los registros y la autorización.

## <a name="get-a-token"></a>Obtención de un token
Si necesita la tooonly de aplicación web, ejecutar las directivas, puede omitir Hola siguientes secciones. Estas secciones no son aplicaciones tooweb solo es aplicable que necesitan toomake autenticado llamadas tooa web API y también están protegidas por Azure AD B2C.

Puede canjear código de autorización de Hola que adquirió (mediante el uso de `response_type=code+id_token`) para un token toohello deseado recursos mediante el envío de un `POST` solicitar toohello `/token` punto de conexión. Actualmente, hello solo los recursos que puede solicitar un token para es la API de web de back-end de la aplicación. convención de Hola para solicitar un token tooyourself es toouse Id. de cliente de la aplicación como ámbito de hello:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>

```

| Parámetro | ¿Necesario? | Description |
| --- | --- | --- |
| p |Obligatorio |Hola directiva de autorización de hello tooacquire usado código. No puede usar una directiva diferente en esta solicitud. Tenga en cuenta que agregar esta cadena de consulta de parámetro toohello, no toohello `POST` cuerpo. |
| client_id |Obligatorio |aplicación Hello identificador ese hello [portal de Azure](https://portal.azure.com/) asignado tooyour aplicación. |
| grant_type |Obligatorio |Hola tipo de concesión, que debe ser `authorization_code` para el flujo de código de autorización de Hola. |
| ámbito |Recomendado |Una lista de ámbitos separada por espacios. Un valor de ámbito único indica tooAzure AD ambos permisos que se ha solicitado. Hola `openid` ámbito indica una toosign permiso en los datos de usuario y get de hello acerca del usuario de hello en forma de Hola de id_token parámetros. Puede ser usado tooget tokens tooyour la aplicación web back-end API, que se representa mediante Hola mismo identificador de aplicación como cliente de Hola. Hola `offline_access` ámbito indica que la aplicación necesitará un token de actualización para tooresources de acceso de larga duración. |
| código |Obligatorio |código de autorización de Hola que adquirió en el primer segmento de hello del flujo de Hola. |
| redirect_uri |Obligatorio |Hola `redirect_uri` parámetro de aplicación Hola que ha recibido código de autorización de Hola. |
| client_secret |Obligatorio |secreto de aplicación Hola que generó en hello [portal de Azure](https://portal.azure.com/). El secreto de aplicación es un artefacto de seguridad importante. Debe almacenarlo de forma segura en el servidor. También debe rotar este secreto del cliente de forma periódica. |

Una respuesta correcta del token tiene el siguiente aspecto:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parámetro | Description |
| --- | --- |
| not_before |tiempo de Hello en qué Hola token se considera válida, en tiempo base. |
| token_type |valor de tipo de token de Hola. Hola solo tipo que admite Azure AD es `Bearer`. |
| access_token |Hola firmó token JWT que solicitó. |
| ámbito |ámbitos de Hola para qué hello token es válido. Se pueden usar para almacenar en caché los tokens para su posterior uso. |
| expires_in |Hola longitud de tiempo que Hola token de acceso es válida (en segundos). |
| refresh_token |Un token de actualización de OAuth 2.0. aplicación Hello puede usar este token tooacquire los tokens adicionales después de que expire el token actual Hola. Actualizar tokens son de larga duración y puede ser usado tooretain acceso tooresources durante largos períodos de tiempo. Para obtener más información, consulte toohello [referencia del token B2C](active-directory-b2c-reference-tokens.md). Tenga en cuenta que debe haber utilizado el ámbito de hello `offline_access` en autorización de Hola y el token de las solicitudes en orden tooreceive un token de actualización. |

Las respuestas de error tienen un aspecto similar al siguiente:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen y que puede ser usado tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudar a un desarrollador para identificar la causa de Hola de un error de autenticación. |

## <a name="use-hello-token"></a>Usar el token de Hola
Ahora que ha adquirido correctamente un token de acceso, puede usar símbolo (token) de hello en las API de web de back-end de tooyour solicitudes mediante la inclusión en hello `Authorization` encabezado:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-hello-token"></a>Hola token de actualización
Los tokens de identificador tienen una corta duración. Debe actualizarlos después de que expiren toocontinue que se va a tooaccess capaz de recursos. Puede hacerlo mediante el envío de otra `POST` solicitar toohello `/token` punto de conexión. Este tiempo, proporcionar hello `refresh_token` parámetro en lugar de hello `code` parámetro:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=openid offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>
```

| Parámetro | Obligatorio | Description |
| --- | --- | --- |
| p |Obligatorio |Directiva de Hola que estaba token tooacquire usado Hola de actualización original. No puede usar una directiva diferente en esta solicitud. Tenga en cuenta que agregar esta cadena de consulta de parámetros toohello, toohello el cuerpo de la publicación. |
| client_id |Obligatorio |aplicación Hello identificador ese hello [portal de Azure](https://portal.azure.com/) asignado tooyour aplicación. |
| grant_type |Obligatorio |tipo de Hola de concesión, que debe ser un token de actualización para este segmento del flujo de código de autorización de Hola. |
| ámbito |Recomendado |Una lista de ámbitos separada por espacios. Un valor de ámbito único indica tooAzure AD ambos permisos que se ha solicitado. Hola `openid` ámbito indica una toosign permiso en los datos de usuario y get de hello acerca del usuario de hello en forma de Hola de tokens de identificador. Puede ser usado tooget tokens tooyour la aplicación web back-end API, que se representa mediante Hola mismo identificador de aplicación como cliente de Hola. Hola `offline_access` ámbito indica que la aplicación necesitará un token de actualización para tooresources de acceso de larga duración. |
| redirect_uri |Recomendado |Hola `redirect_uri` parámetro de aplicación Hola que ha recibido código de autorización de Hola. |
| refresh_token |Obligatorio |Hola original token de actualización que adquirió en la bifurcación de la segunda Hola de flujo de Hola. Tenga en cuenta que debe haber utilizado el ámbito de hello `offline_access` en autorización de Hola y el token de las solicitudes en orden tooreceive un token de actualización. |
| client_secret |Obligatorio |secreto de aplicación Hola que generó en hello [portal de Azure](https://portal.azure.com/). El secreto de aplicación es un artefacto de seguridad importante. Debe almacenarlo de forma segura en el servidor. También debe rotar este secreto del cliente de forma periódica. |

Una respuesta correcta del token tiene el siguiente aspecto:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parámetro | Description |
| --- | --- |
| not_before |tiempo de Hello en qué Hola token se considera válida, en tiempo base. |
| token_type |valor de tipo de token de Hola. Hola solo tipo que admite Azure AD es `Bearer`. |
| access_token |Hola firmó token JWT que solicitó. |
| ámbito |ámbito de Hola Hola token es válido, que se puede utilizar para almacenar en caché los tokens para su uso posterior. |
| expires_in |Hola longitud de tiempo que Hola token de acceso es válida (en segundos). |
| refresh_token |Un token de actualización de OAuth 2.0. aplicación Hello puede usar este token tooacquire los tokens adicionales después de que expire el token actual Hola.  Actualizar tokens son de larga duración y puede ser usado tooretain acceso tooresources durante largos períodos de tiempo. Para obtener información más detallada, consulte toohello [referencia del token B2C](active-directory-b2c-reference-tokens.md). |

Las respuestas de error tienen un aspecto similar al siguiente:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen y que puede ser usado tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudar a un desarrollador para identificar la causa de Hola de un error de autenticación. |

## <a name="send-a-sign-out-request"></a>Envío de una solicitud de cierre de sesión
Cuando desee que el usuario de hello toosign fuera de la aplicación hello, es insuficiente tooclear las cookies de la aplicación o en caso contrario, finalizar sesión de hello con usuario Hola. También se debe redirigir Hola usuario tooAzure AD toosign out. Si no toodo por lo tanto, el usuario de hello podría ser capaz de tooreauthenticate tooyour aplicaciones sin escribir sus credenciales de nuevo. Esto se debe a que el usuario tendrá una sesión válida de inicio de sesión único con Azure AD.

Simplemente puede redirigir Hola usuario toohello `end_session` punto de conexión que se muestra en el documento de metadatos de OpenID Connect de hello descrita anteriormente en hello sección "Validar el token de Id. de hello":

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parámetro | ¿Necesario? | Description |
| --- | --- | --- |
| p |Obligatorio |Directiva de Hola que desea que toouse toosign Hola usuario fuera de la aplicación. |
| post_logout_redirect_uri |Recomendado |Hello ese usuario Hola de dirección URL debe ser redirigido tooafter correcta cierre de sesión. Si no se incluye, Azure AD B2C muestra a usuario Hola un mensaje genérico. |

> [!NOTE]
> Aunque dirigir Hola usuario toohello `end_session` extremo borrará algunos Hola del único inicio de sesión de estado del usuario con Azure AD B2C, no firmará usuario Hola fuera de su sesión de proveedor (IDP) de identidades sociales. Si selecciona usuario Hola Hola IDP mismo durante un inicio de sesión posteriores, se puede volver a autenticar, sin proporcionar sus credenciales. Si un usuario desea toosign fuera de la aplicación B2C, no necesariamente significa que deseen toosign fuera de su cuenta de Facebook. Sin embargo, en caso de hello de cuentas locales, sesión de usuario de Hola se finalizará correctamente.
> 
> 

## <a name="use-your-own-b2c-tenant"></a>Uso de un inquilino de B2C propio
Si desea tootry estas solicitudes por sí mismo, debe realizar estos tres pasos y, a continuación, reemplace los valores de ejemplo de Hola descritos por los suyos propios:

1. [Crear un inquilino B2C](active-directory-b2c-get-started.md)y utilice el nombre de Hola de su inquilino en las solicitudes de Hola.
2. [Crear una aplicación](active-directory-b2c-app-registration.md) tooobtain un identificador de aplicación. Incluya una aplicación web o una API web en la aplicación. Opcionalmente puede crear un secreto de aplicación.
3. [Crear las directivas de](active-directory-b2c-reference-policies.md) tooobtain los nombres de directiva.

