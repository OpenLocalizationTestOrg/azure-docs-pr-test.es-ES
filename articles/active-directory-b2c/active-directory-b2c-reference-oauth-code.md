---
title: "Flujo de código de autorización - Azure AD B2C | Microsoft Docs"
description: "Obtenga información acerca de cómo toobuild aplicaciones web con el protocolo de autenticación de Azure AD B2C y OpenID Connect."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Azure Active Directory B2C: flujo de código de autorización de OAuth 2.0
Puede usar la concesión de código de autorización de hello OAuth 2.0 en aplicaciones instaladas en un dispositivo toogain acceder a tooprotected recursos, como las API web. Mediante el uso de implementación de hello Azure Active Directory B2C (Azure AD B2C) de OAuth 2.0, puede agregar el inicio de sesión, inicio de sesión y otra administración de identidad tareas tooyour aplicaciones de escritorio y móviles. Este artículo es independiente del lenguaje En el artículo de hello, se describe cómo toosend y recibir mensajes HTTP sin usar las bibliotecas de código abierto.

<!-- TODO: Need link toolibraries -->

Hola flujo de código de autorización de OAuth 2.0 se describe en [sección 4.1 de especificación de hello OAuth 2.0](http://tools.ietf.org/html/rfc6749). Puede usarlo para llevar a cabo la autenticación y la autorización en la mayoría de los tipos de aplicación, incluidas las [aplicaciones web](active-directory-b2c-apps.md#web-apps) y las [aplicaciones instaladas de forma nativa](active-directory-b2c-apps.md#mobile-and-native-apps). Puede usar hello adquirir toosecurely de flujo de código de autorización de OAuth 2.0 *tokens de acceso* para las aplicaciones, lo que puede ser usado tooaccess recursos que están protegidos por un [servidor de autorización](active-directory-b2c-reference-protocols.md#the-basics).

En este artículo se centra en hello **clientes públicos** flujo de código de autorización de OAuth 2.0. Un cliente público es cualquier aplicación cliente que no puede ser de confianza toosecurely mantener la integridad de Hola de una contraseña secreta. Esto incluye aplicaciones móviles, aplicaciones de escritorio y básicamente cualquier aplicación que se ejecuta en un dispositivo y necesita tooget los tokens de acceso. 

> [!NOTE]
> aplicación web tooa de administración de identidad de tooadd mediante el uso de Azure AD B2C, use [OpenID Connect](active-directory-b2c-reference-oidc.md) en lugar de OAuth 2.0.

Azure AD B2C amplía estándar Hola que fluye de OAuth 2.0 toodo más de autorización y autenticación simple. Introduce hello [parámetro policy](active-directory-b2c-reference-policies.md). Con las directivas integradas, puede usar OAuth 2.0 tooadd usuario experimenta tooyour aplicación, como inicio de sesión, inicio de sesión y la administración de perfiles. En este artículo, le mostraremos cómo toouse tooimplement de OAuth 2.0 y las directivas de cada una de estas experiencias en sus aplicaciones nativas. También le mostraremos cómo tooget los tokens de acceso para tener acceso a las API de web.

En solicitudes de HTTP de ejemplo de Hola en este artículo, se utiliza el directorio de Azure AD B2C de ejemplo, **fabrikamb2c.onmicrosoft.com**. También se usa nuestra aplicación y nuestras directivas de ejemplo. Puede intentar Hola solicitudes mediante el uso de estos valores o reemplazarlos con sus propios valores.
Obtenga información acerca de cómo demasiado[obtener su propio directorio, aplicaciones y directivas de Azure AD B2C](#use-your-own-azure-ad-b2c-directory).

## <a name="1-get-an-authorization-code"></a>1. Obtener un código de autorización
flujo de código de autorización de Hello comienza con cliente hello dirigir Hola usuario toohello `/authorize` punto de conexión. Esto forma parte interactivo de Hola de flujo de hello, donde usuario Hola realiza la acción. En esta solicitud, el cliente de Hola indica Hola `scope` permisos de Hola de parámetro que necesita tooacquire de usuario de Hola. Hola `p` parámetro, indica Hola directiva tooexecute. Hello tres ejemplos siguientes (con saltos de línea para mejorar la legibilidad) utilizan una directiva diferente.

### <a name="use-a-sign-in-policy"></a>Uso de una directiva de inicio de sesión
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Uso de una directiva de registro
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Uso de una directiva de edición de perfil
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| Parámetro | ¿Necesario? | Description |
| --- | --- | --- |
| client_id |Obligatorio |Identificador de la aplicación Hello asignado tooyour aplicación Hola [portal de Azure](https://portal.azure.com). |
| response_type |Obligatorio |tipo de respuesta de Hello, que debe incluir `code` para el flujo de código de autorización de Hola. |
| redirect_uri |Obligatorio |Hola URI de redireccionamiento de la aplicación, donde se envían y reciben mediante la aplicación de las respuestas de autenticación. Debe coincidir exactamente con uno de redirección de hello URI que se ha registrado en el portal de hello, excepto en que debe ser codificados de dirección URL. |
| ámbito |Obligatorio |Una lista de ámbitos separada por espacios. El valor de un solo ámbito indica tooAzure Active Directory (Azure AD) tanto de los permisos de Hola que se ha solicitado. Mediante identificación como ámbito de hello indica que la aplicación necesita un token de acceso que se puede usar con su propio servicio o la API web, representada por el cliente de Hola Hola mismo identificador de cliente.  Hola `offline_access` ámbito indica que la aplicación necesita un token de actualización para tooresources de acceso de larga duración. También puede usar hello `openid` ámbito toorequest un identificador de token de Azure AD B2C. |
| response_mode |Recomendado |método Hello que usar toosend Hola resultante autorización código tooyour atrás aplicación. Puede ser `query`, `form_post` o `fragment`. |
| state |Recomendado |Un valor incluido en la solicitud de Hola que se devuelve en la respuesta de token de Hola. Puede ser una cadena de contenido que desee toouse. Normalmente, se utiliza un valor único generado aleatoriamente, ataques de falsificación de solicitud entre sitios tooprevent. estado de Hello también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se produjo la solicitud de autenticación de Hola. Por ejemplo, usuario de la página Hola Hola se realizó u Hola directiva que se está ejecutando. |
| p |Obligatorio |Directiva de Hola que se ejecuta. Su Hola nombre de una directiva que se crea en el directorio de Azure AD B2C. valor de nombre de directiva de Hello debe comenzar por **b2c\_1\_**. toolearn más información acerca de las directivas, consulte [directivas integradas de Azure AD B2C](active-directory-b2c-reference-policies.md). |
| símbolo del sistema |Opcional |tipo de Hello de interacción del usuario que es necesario. Actualmente, Hola único valor válido es `login`, que fuerza Hola tooenter usuario sus credenciales en esa solicitud. El inicio de sesión único no surtirá efecto. |

En este momento, usuario Hola se solicita el flujo de trabajo de la directiva de toocomplete Hola. Ello puede significar tener a usuario Hola escribir su nombre de usuario y una contraseña, inicio de sesión con una identidad de redes sociales, registrarse para el directorio de Hola o cualquier otro número de pasos. Las acciones del usuario dependen de cómo se define la directiva de Hola.

Al finalizar usuario Hola directiva hello, Azure AD devuelve una aplicación de tooyour de respuesta al valor de Hola que utilizó para `redirect_uri`. Se utiliza método hello especificado en hello `response_mode` parámetro. respuesta de Hello es exactamente Hola mismo para cada uno de los escenarios de acción de usuario hello, independientemente de la directiva de Hola que se ejecutó.

Una respuesta correcta que usa `response_mode=query` tiene este aspecto:

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| Parámetro | Description |
| --- | --- |
| código |código de autorización de Hola Hola aplicación solicitada. aplicación Hello puede utilizar toorequest de código de autorización de hello un token de acceso para un recurso de destino. Los códigos de autorización tienen una duración muy breve. Normalmente, caducan al cabo de unos 10 minutos. |
| state |Consulte la descripción completa de hello en tabla Hola Hola sección anterior. Si un `state` parámetro se incluye en la solicitud de hello, hello mismo valor aparecerán en la respuesta de Hola. Hello aplicación debe comprobar que hello `state` valores de hello solicitud y respuesta son idénticos. |

Las respuestas de error también se pueden enviar toohello el URI de redireccionamiento para que hello aplicación pueda controlarlos adecuadamente:

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que se pueden usar tipos de hello tooclassify de errores que se producen. También puede usar Hola cadena tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudarle a identificar la causa de raíz de Hola de un error de autenticación. |
| state |Consulte la descripción completa de Hola Hola tabla anterior. Si un `state` parámetro se incluye en la solicitud de hello, hello mismo valor aparecerán en la respuesta de Hola. Hello aplicación debe comprobar que hello `state` valores de hello solicitud y respuesta son idénticos. |

## <a name="2-get-a-token"></a>2. Obtención de un token
Ahora que ha adquirido un código de autorización, puede compensar hello `code` para un toohello símbolo (token) que vayan recursos mediante el envío de un toohello de solicitud POST `/token` punto de conexión. En Azure AD B2C, hello solo los recursos que puede solicitar un token para es la API de web de back-end de la aplicación. convención de Hola que se usa para solicitar un token tooyourself es toouse Id. de cliente de la aplicación como ámbito de hello:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| Parámetro | ¿Necesario? | Description |
| --- | --- | --- |
| p |Obligatorio |Hola directiva de autorización de hello tooacquire usado código. No puede usar una directiva diferente en esta solicitud. Tenga en cuenta que agregar este parámetro toohello *cadena de consulta*, pero no en hello cuerpo POST. |
| client_id |Obligatorio |Identificador de la aplicación Hello asignado tooyour aplicación Hola [portal de Azure](https://portal.azure.com). |
| grant_type |Obligatorio |tipo de Hola de concesión. Para el flujo de código de autorización de hello, debe ser el tipo de concesión de hello `authorization_code`. |
| ámbito |Recomendado |Una lista de ámbitos separada por espacios. Un valor de ámbito único indica tooAzure AD tanto de los permisos de Hola que se ha solicitado. Mediante identificación como ámbito de hello indica que la aplicación necesita un token de acceso que se puede usar con su propio servicio o la API web, representada por el cliente de Hola Hola mismo identificador de cliente.  Hola `offline_access` ámbito indica que la aplicación necesita un token de actualización para tooresources de acceso de larga duración.  También puede usar hello `openid` ámbito toorequest un identificador de token de Azure AD B2C. |
| código |Obligatorio |código de autorización de Hola que adquirió en el primer segmento de hello del flujo de Hola. |
| redirect_uri |Obligatorio |Hola URI de redireccionamiento de aplicación hello que ha recibido código de autorización de Hola. |

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
| token_type |valor de tipo de token de Hola. Hola solo escriba que admite Azure AD es portador. |
| access_token |Hola había firmado JSON Web Token (JWT) que solicitó. |
| ámbito |ámbitos de Hola Hola token es válido para. También puede utilizar tokens de toocache ámbitos para su uso posterior. |
| expires_in |duración de Hola de Hola token es válido (en segundos). |
| refresh_token |Un token de actualización de OAuth 2.0. aplicación Hello puede usar este token tooacquire los tokens adicionales después de que expire el token actual Hola. Los tokens de actualización tienen una duración larga. Puede usarlos tooretain acceso tooresources durante largos períodos de tiempo. Para obtener más información, vea hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md). |

Las respuestas de error tienen un aspecto similar al siguiente:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que se pueden usar tipos de hello tooclassify de errores que se producen. También puede usar Hola cadena tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudarle a identificar la causa de raíz de Hola de un error de autenticación. |

## <a name="3-use-hello-token"></a>3. Usar el token de Hola
Ahora que ha adquirido correctamente un token de acceso, puede usar símbolo (token) de hello en las API de web de back-end de tooyour solicitudes mediante la inclusión en hello `Authorization` encabezado:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4. Hola token de actualización
Los tokens de acceso y los tokens de identificación tienen una corta duración. Después de que expiren, debe actualizarlos toocontinue tooaccess recursos. toodo, enviar otra toohello de solicitud POST `/token` punto de conexión. Este tiempo, proporcionar hello `refresh_token` en lugar de Hola `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| Parámetro | ¿Necesario? | Description |
| --- | --- | --- |
| p |Obligatorio |Directiva de Hola que estaba token tooacquire usado Hola de actualización original. No puede usar una directiva diferente en esta solicitud. Tenga en cuenta que agregar este parámetro toohello *cadena de consulta*, pero no en hello cuerpo POST. |
| client_id |Recomendado |Identificador de la aplicación Hello asignado tooyour aplicación Hola [portal de Azure](https://portal.azure.com). |
| grant_type |Obligatorio |tipo de Hola de concesión. Para este segmento del flujo de código de autorización de hello, debe ser el tipo de concesión de hello `refresh_token`. |
| ámbito |Recomendado |Una lista de ámbitos separada por espacios. Un valor de ámbito único indica tooAzure AD tanto de los permisos de Hola que se ha solicitado. Mediante identificación como ámbito de hello indica que la aplicación necesita un token de acceso que se puede usar con su propio servicio o la API web, representada por el cliente de Hola Hola mismo identificador de cliente.  Hola `offline_access` ámbito indica que la aplicación necesitará un token de actualización para tooresources de acceso de larga duración.  También puede usar hello `openid` ámbito toorequest un identificador de token de Azure AD B2C. |
| redirect_uri |Opcional |Hola URI de redireccionamiento de aplicación hello que ha recibido código de autorización de Hola. |
| refresh_token |Obligatorio |Hola original token de actualización que adquirió en la bifurcación de la segunda Hola de flujo de Hola. |

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
| token_type |valor de tipo de token de Hola. Hola solo escriba que admite Azure AD es portador. |
| access_token |Hola había firmado JWT que solicitó. |
| ámbito |ámbitos de Hola Hola token es válido para. También puede utilizar tokens de hello ámbitos toocache para su uso posterior. |
| expires_in |duración de Hola de Hola token es válido (en segundos). |
| refresh_token |Un token de actualización de OAuth 2.0. aplicación Hello puede usar este token tooacquire los tokens adicionales después de que expire el token actual Hola. Actualizar tokens son de larga duración y puede ser usado tooretain acceso tooresources durante largos períodos de tiempo. Para obtener más información, vea hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md). |

Las respuestas de error tienen un aspecto similar al siguiente:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que se pueden usar tipos de tooclassify de errores que se producen. También puede usar Hola cadena tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudarle a identificar la causa de raíz de Hola de un error de autenticación. |

## <a name="use-your-own-azure-ad-b2c-directory"></a>Usar su propio directorio de Azure AD B2C
tootry estas solicitudes usted mismo, Hola completa siguiendo los pasos. Reemplace los valores de ejemplo de Hola que se usan en este artículo con sus propios valores.

1. [Cree un directorio de Azure AD B2C](active-directory-b2c-get-started.md). Usar el nombre de Hola de su directorio en las solicitudes de Hola.
2. [Crear una aplicación](active-directory-b2c-app-registration.md) tooobtain un identificador de aplicación y un URI de redirección. Incluya un cliente nativo en la aplicación.
3. [Crear las directivas de](active-directory-b2c-reference-policies.md) tooobtain los nombres de directiva.

