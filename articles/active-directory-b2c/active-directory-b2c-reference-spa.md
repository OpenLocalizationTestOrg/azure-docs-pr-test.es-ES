---
title: "Azure Active Directory B2C: aplicaciones de una página con el flujo implícito | Microsoft Docs"
description: "Obtenga información acerca de cómo toobuild página aplicaciones directamente mediante el uso de OAuth 2.0 implícita fluyen con Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: a45cc74c-a37e-453f-b08b-af75855e0792
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: parakhj
ms.openlocfilehash: 5e52abc18fe545f0f6d1745cdb2ea42c5b2698cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-single-page-app-sign-in-by-using-oauth-20-implicit-flow"></a>Azure AD B2C: inicio de sesión de aplicaciones de una página con el flujo implícito de OAuth 2.0

> [!NOTE]
> Esta característica se encuentra en su versión preliminar.
> 

Muchas aplicaciones modernas tienen un front-end de aplicación de una página escrito principalmente en JavaScript. A menudo, la aplicación hello se escribe con el marco como AngularJS, Ember.js o Durandal. Las aplicaciones de una sola página y otras aplicaciones JavaScript que se ejecutan principalmente en un explorador tienen algunos retos adicionales para la autenticación:

* características de seguridad de Hola de estas aplicaciones son significativamente diferentes de las aplicaciones web tradicionales basados en servidor.
* Muchos proveedores de identidades y servidores de autorización no admiten solicitudes de uso compartido de recursos entre orígenes (CORS).
* Las redirecciones de página completa explorador fuera de la aplicación hello pueden ser toohello invasiva considerablemente la experiencia del usuario.

toosupport estas aplicaciones, Azure Active Directory B2C (Azure AD B2C) usa flujo implícito hello OAuth 2.0. se describe el flujo de concesión implícita de autorización de Hello OAuth 2.0 en [sección 4.2 de especificación de hello OAuth 2.0](http://tools.ietf.org/html/rfc6749). En el flujo implícito, aplicación hello recibe los tokens directamente de hello Azure Active Directory (Azure AD) autorizar el punto de conexión, sin ningún servidor a servidor exchange. Todos los lógica de autenticación y control de la toma de la sesión colocan completamente en el cliente de JavaScript de hello, sin las redirecciones de páginas adicionales.

Azure AD B2C amplía hello toomore de flujo implícitos de OAuth 2.0 estándar de autorización y autenticación simples. Azure AD B2C presenta hello [parámetro policy](active-directory-b2c-reference-policies.md). Con el parámetro de directiva de hello, puede usar OAuth 2.0 tooadd usuario experimenta tooyour aplicación, como inicio de sesión, inicio de sesión y la administración de perfiles. En este artículo, le mostraremos cómo toouse Hola flujo implícito y Azure AD tooimplement cada de estas experiencias en las aplicaciones de la página. toohelp comenzar, eche un vistazo a nuestro [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi) y [Microsoft .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi) ejemplos.

En solicitudes de HTTP de ejemplo de Hola en este artículo, se utiliza el directorio de Azure AD B2C de ejemplo, **fabrikamb2c.onmicrosoft.com**. También se usa nuestra propia aplicación y nuestras directivas de ejemplo. Puede intentar Hola solicitudes mediante el uso de estos valores o reemplazarlos con sus propios valores.
Obtenga información acerca de cómo demasiado[obtener su propio directorio, aplicaciones y directivas de Azure AD B2C](#use-your-own-b2c-tenant).


## <a name="protocol-diagram"></a>Diagrama de protocolo

el flujo de inicio de sesión implícito de Hello es algo parecido a Hola figura siguiente. Cada paso se describe en detalle más adelante en el artículo de Hola.

![Calles OpenID Connect](../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## <a name="send-authentication-requests"></a>Envío de solicitudes de autenticación
Cuando la aplicación web necesita el usuario de hello tooauthenticate y ejecutar una directiva, dirige Hola usuario toohello `/authorize` punto de conexión. Es Hola parte interactiva del flujo de Hola donde usuario Hola realiza una acción, dependiendo de la directiva de Hola. usuario de Hola Obtiene un identificador de token Hola extremo de Azure AD.

En esta solicitud, el cliente de Hola indica Hola `scope` permisos de Hola de parámetro que necesita tooacquire de usuario de Hola. Hola `p` parámetro, indica Hola directiva tooexecute. Hello tres ejemplos siguientes (con saltos de línea para mejorar la legibilidad) utilizan una directiva diferente. tooget una idea de cómo funciona cada solicitud, intente la solicitud de Hola de pegado en un explorador y ejecutarlo.

### <a name="use-a-sign-in-policy"></a>Uso de una directiva de inicio de sesión
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Uso de una directiva de registro
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Uso de una directiva de edición de perfil
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parámetro | ¿Necesario? | Description |
| --- | --- | --- |
| client_id |Obligatorio |Identificador de la aplicación Hello asignado tooyour aplicación Hola [portal de Azure](https://portal.azure.com). |
| response_type |Obligatorio |Debe incluir `id_token` para el inicio de sesión en OpenID Connect. También puede incluir el tipo de respuesta de hello `token`. Si usa `token`, la aplicación puede recibir inmediatamente un token de acceso de hello autorizar el punto de conexión, sin realizar una segunda toohello solicitud extremo authorize.  Si usas hello `token` tipo de respuesta, hello `scope` parámetro debe contener un ámbito que indica qué token de recurso tooissue Hola para. |
| redirect_uri |Recomendado |Hola URI de redireccionamiento de la aplicación, donde las respuestas de autenticación pueden ser enviadas y recibidas por la aplicación. Debe coincidir exactamente con uno de redirección de hello URI que se ha registrado en el portal de hello, excepto en que debe ser codificados de dirección URL. |
| response_mode |Recomendado |Especifica el método toouse toosend Hola resultante token tooyour atrás aplicación hello.  Para los flujos implícitos, use `fragment`. |
| ámbito |Obligatorio |Una lista de ámbitos separada por espacios. Un valor de ámbito único indica tooAzure AD tanto de los permisos de Hola que se ha solicitado. Hola `openid` ámbito indica una toosign permiso en los datos de usuario y get de hello acerca del usuario de hello en forma de Hola de tokens de identificador. (Hablaremos sobre esto más adelante en el artículo de Hola.) Hola `offline_access` ámbito es opcional para las aplicaciones web. Indica que la aplicación necesita un token de actualización para tooresources de acceso de larga duración. |
| state |Recomendado |Un valor incluido en la solicitud de Hola que también se devuelve en la respuesta de token de Hola. Puede ser una cadena de contenido que desee toouse. Por lo general, se usa un valor único, generado de forma aleatoria, ataques de falsificación de solicitud entre sitios tooprevent. Hello estado también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido la solicitud de autenticación de hello, al igual que la página de hello estuvieran en. |
| valor de seguridad |Obligatorio |Un valor incluido en la solicitud de hello (generado por la aplicación hello) que se incluye en el token de identificador resultante de hello como una notificación. aplicación Hello, a continuación, puede comprobar que los ataques de reproducción de tokens de toomitigate este valor. Por lo general, el valor de hello es una cadena aleatoria, única que puede ser utilizados tooidentify Hola origen de solicitud de Hola. |
| p |Obligatorio |Hola tooexecute de directiva. Su Hola nombre de una directiva que se crea en el inquilino de Azure AD B2C. valor de nombre de directiva de Hello debe comenzar por **b2c\_1\_**. Para obtener más información, vea [Directivas integradas de Azure AD B2C](active-directory-b2c-reference-policies.md). |
| símbolo del sistema |Opcional |tipo de Hello de interacción del usuario que se necesita. Actualmente, Hola único valor válido es `login`. Esto obliga a Hola usuario tooenter sus credenciales en esa solicitud. El inicio de sesión único no surtirá efecto. |

En este momento, usuario Hola se solicita el flujo de trabajo de la directiva de toocomplete Hola. Ello puede significar tener a usuario Hola escribir su nombre de usuario y una contraseña, inicio de sesión con una identidad de redes sociales, registrarse para el directorio de Hola o cualquier otro número de pasos. Las acciones del usuario dependen de cómo se define la directiva de Hola.

Al finalizar usuario Hola directiva hello, Azure AD devuelve una aplicación de tooyour de respuesta al valor de Hola que utilizó para `redirect_uri`. Se utiliza método hello especificado en hello `response_mode` parámetro. respuesta de Hello es exactamente Hola mismo para cada uno de los escenarios de acción de usuario hello, independientemente de la directiva de Hola que se ejecutó.

### <a name="successful-response"></a>Respuesta correcta
Una respuesta correcta que utiliza `response_mode=fragment` y `response_type=id_token+token` siguiente hello, saltos de línea por legibilidad aspecto:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
```

| Parámetro | Description |
| --- | --- |
| access_token |token de acceso de Hola que Hola aplicación solicitada.  token de acceso de Hello no se debe descodificar o inspeccionar en caso contrario. Puede tratarse como una cadena opaca. |
| token_type |valor de tipo de token de Hola. Hola solo escriba que admite Azure AD es portador. |
| expires_in |Hola longitud de tiempo que Hola token de acceso es válida (en segundos). |
| ámbito |ámbitos de Hola Hola token es válido para. También puede utilizar tokens de toocache ámbitos para su uso posterior. |
| ID_token |Hello Id. de símbolo (token) que solicita la aplicación hello. Puede usar identidad de usuario de hello identificador tooverify token hello y empezar una sesión de usuario de Hola. Para obtener más información sobre los tokens de identificador y su contenido, vea hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md). |
| state |Si un `state` parámetro se incluye en la solicitud de hello, hello mismo valor aparecerán en la respuesta de Hola. Hello aplicación debe comprobar que hello `state` valores de hello solicitud y respuesta son idénticos. |

### <a name="error-response"></a>Respuesta de error
Las respuestas de error también se pueden enviar toohello el URI de redireccionamiento para que hello aplicación pueda controlarlos adecuadamente:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error usa tooclassify tipos de errores que se producen. También puede utilizar el código de error de hello para el control de errores. |
| error_description |Un mensaje de error específico que puede ayudarle a identificar la causa de raíz de Hola de un error de autenticación. |
| state |Consulte la descripción completa de Hola Hola tabla anterior. Si un `state` parámetro se incluye en la solicitud de hello, hello mismo valor aparecerán en la respuesta de Hola. Hello aplicación debe comprobar que hello `state` valores de hello solicitud y respuesta son idénticos.|

## <a name="validate-hello-id-token"></a>Validar el token del identificador hello
Recibir un identificador de token no es suficiente usuario de hello tooauthenticate. Debe validar la firma del token de Id. de Hola y comprobar las notificaciones de Hola de token de hello según los requisitos de la aplicación. Usa Azure AD B2C [Tokens de Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) y públicos tokens toosign de criptografía de clave y compruebe que son válidos.

Existen muchas bibliotecas de código abierto para validar los Jwt, según el lenguaje de hello prefiere toouse. Considere la posibilidad de explorar las bibliotecas de código abierto disponibles, en lugar de implementar su propia lógica de validación. Puede utilizar información de hello en toohelp de este artículo aprenderá cómo tooproperly utilizar dichas bibliotecas.

Azure AD B2C tiene un punto de conexión de metadatos OpenID Connect. Una aplicación puede utilizar la información de toofetch de punto de conexión de hello sobre Azure AD B2C en tiempo de ejecución. En esta información se incluyen los extremos, los contenidos del token y las claves de firma de los token. Hay un documento de metadatos JSON para cada directiva en su inquilino de Azure AD B2C. Por ejemplo, el documento de metadatos de hello para la directiva de b2c_1_sign_in hello en el inquilino de hello fabrikamb2c.onmicrosoft.com se encuentra en:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Una de las propiedades de Hola de este documento de configuración es hello `jwks_uri`. valor de Hola para hello sería la misma directiva:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

toodetermine qué directiva era toosign usa un identificador de token (y donde toofetch Hola metadatos de), tiene dos opciones. En primer lugar, se incluye el nombre de la directiva de Hola Hola `acr` de notificación en `id_token`. Para obtener información acerca de cómo tooparse Hola notificaciones desde un identificador de token, consulte hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md). La otra opción es la directiva de hello tooencode en valor de Hola de hello `state` parámetro cuando se emite la solicitud de saludo. A continuación, descodificar hello `state` toodetermine parámetro directiva que se utilizó. Cualquiera de estos métodos es válido.

Una vez que haya adquirido el documento de metadatos de hello del extremo de metadatos de OpenID Connect de hello, puede usar Hola RSA-256 claves públicas (que se encuentra en este extremo) toovalidate Hola firma de token de Id. de Hola. Podría haber varias claves enumeradas en este punto de conexión en cualquier momento, cada una identificada con una `kid`. encabezado de Hola de `id_token` también contiene un `kid` de notificación. Indica cuál de estas claves era el token del identificador hello toosign usado. Para obtener más información, aprender a [validar los tokens](active-directory-b2c-reference-tokens.md#token-validation), vea hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md).
<!--TODO: Improve hello information on this-->

Después de validar la firma de Hola de token de Id. de hello, varias notificaciones requieran comprobación. Por ejemplo:

* Validar hello `nonce` tooprevent ataques de reproducción de tokens de notificaciones. Su valor debe ser lo que hayas especificado en una solicitud de inicio de sesión Hola.
* Validar hello `aud` tooensure que Hola identificador de token haya sido emitido para la aplicación de notificaciones. Su valor debe ser el identificador de la aplicación hello de la aplicación.
* Validar hello `iat` y `exp` notificaciones tooensure que Hola identificador de token no ha expirado.

Varias validaciones más que se deben realizar se describen en detalle en hello [especificación de OpenID conectarse Core](http://openid.net/specs/openid-connect-core-1_0.html). Puede que le interese toovalidate notificaciones adicionales, según el escenario. Algunas validaciones comunes incluyen:

* Garantizar ese usuario de Hola o la organización ha registrado para la aplicación hello.
* Asegurarse de que el usuario hello tiene la autorización adecuada y privilegios.
* Asegurarse de que se haya producido un determinado nivel de autenticación, como al usar Azure Multi-Factor Authentication.

Para obtener más información sobre notificaciones de hello en un identificador de token, consulte hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md).

Después de haber validado por completo el token del identificador hello, puede comenzar una sesión por usuario de Hola. En la aplicación, utilizar notificaciones de hello en información de símbolo (token) tooobtain de Id. de hello acerca del usuario de Hola. Esta información puede usarse para su visualización, registros, autorizaciones, etc.

## <a name="get-access-tokens"></a>Obtención de tokens de acceso
Si lo único que hello es su toodo de necesidades de las aplicaciones web ejecuta las directivas, puede omitir Hola siguientes secciones. información de Hello en hello siguientes secciones es aplicable solo tooweb las aplicaciones que necesitan toomake autenticado llamadas tooa web API, y que están protegidos por Azure AD B2C.

Ahora que has iniciado la sesión de usuario hello en tooyour página aplicación, puede obtener tokens de acceso web que realiza la llamada API que están protegidas por Azure AD. Incluso si ya ha recibido un token mediante el uso de hello `token` tipo de respuesta, puede utilizar los tokens de tooacquire de este método para obtener recursos adicionales sin redirigir toosign de usuario de Hola de nuevo.

En un flujo de aplicación web típica, podría hacer esto mediante la realización de una solicitud toohello `/token` punto de conexión.  Sin embargo, el punto de conexión de hello no compatibilidad con CORS las solicitudes, para realizar AJAX llamadas tooget y tokens de actualización no es una opción. En su lugar, puede usar flujo implícito de hello en un oculto HTML iframe elemento tooget nuevos tokens para otras API web. Aquí se muestra un ejemplo, con saltos de línea por motivos de legibilidad:

```

https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
&response_mode=fragment
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
&p=b2c_1_sign_in
```

| Parámetro | ¿Necesario? | Description |
| --- | --- | --- |
| client_id |Obligatorio |Identificador de la aplicación Hello asignado tooyour aplicación Hola [portal de Azure](https://portal.azure.com). |
| response_type |Obligatorio |Debe incluir `id_token` para el inicio de sesión en OpenID Connect.  También puede incluir el tipo de respuesta de hello `token`. Si utiliza `token` en este caso, la aplicación inmediatamente puede recibir un token de acceso de hello autorizar el punto de conexión, sin realizar una segunda toohello solicitud extremo authorize. Si usas hello `token` tipo de respuesta, hello `scope` parámetro debe contener un ámbito que indica qué token de recurso tooissue Hola para. |
| redirect_uri |Recomendado |Hola URI de redireccionamiento de la aplicación, donde las respuestas de autenticación pueden ser enviadas y recibidas por la aplicación. Debe coincidir exactamente con uno de redirección de hello URI que registró en el portal de hello, excepto en que debe ser codificados de dirección URL. |
| ámbito |Obligatorio |Una lista de ámbitos separada por espacios.  Para obtener los tokens, incluir todos los ámbitos que necesite para el recurso de hello prevista. |
| response_mode |Recomendado |Especifica el método de Hola que es usado toosend Hola resultante token tooyour atrás aplicación.  Puede ser `query`, `form_post` o `fragment`. |
| state |Recomendado |Un valor incluido en la solicitud de Hola que se devuelve en la respuesta de token de Hola.  Puede ser una cadena de contenido que desee toouse.  Por lo general, se usa un valor único, generado de forma aleatoria, ataques de falsificación de solicitud entre sitios tooprevent.  estado de Hello también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se produjo la solicitud de autenticación de Hola. Por ejemplo, el usuario de Hola de página o la vista de Hola estaba en. |
| valor de seguridad |Obligatorio |Un valor incluido en solicitud de hello, generado por la aplicación hello, que se incluye en el token de identificador resultante de hello como una notificación.  aplicación Hello, a continuación, puede comprobar que los ataques de reproducción de tokens de toomitigate este valor. Por lo general, valor de hello es una cadena aleatoria única que identifica el origen de saludo de solicitud de saludo. |
| símbolo del sistema |Obligatorio |usar tokens toorefresh y get en un iframe oculto, `prompt=none` tooensure que Hola iframe no atascar en página de inicio de sesión de Hola y vuelve inmediatamente. |
| login_hint |Obligatorio |los tokens de toorefresh y get en un iframe oculto, incluyen hello nombre del usuario con hello en este toodistinguish sugerencia entre varias sesiones de usuario de hello podría tener en un momento dado. Puede extraer el nombre de usuario de Hola desde un inicio de sesión anterior mediante hello `preferred_username` de notificación. |
| domain_hint |Obligatorio |Puede ser `consumers` o `organizations`.  Para actualizar y obtener tokens en un iframe oculto, debe incluir hello `domain_hint` valor de solicitud de saludo.  Extraer hello `tid` notificación de token de Id. de Hola de una anterior de inicio de sesión toodetermine qué toouse de valor.  Si hello `tid` es el valor de notificación `9188040d-6c67-4c5b-b112-36a304b66dad`, utilice `domain_hint=consumers`.  De lo contrario, use `domain_hint=organizations`. |

Al establecer hello `prompt=none` parámetro, esta solicitud ya sea correctamente o se produce un error inmediatamente y se devuelva tooyour aplicación.  Se envía una respuesta correcta tooyour aplicación Hola indicado en el URI de redirección de, utilizando el método hello especificado en hello `response_mode` parámetro.

### <a name="successful-response"></a>Respuesta correcta
Una respuesta correcta al usar `response_mode=fragment` tiene el siguiente aspecto:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
```

| Parámetro | Description |
| --- | --- |
| access_token |Hola símbolo (token) de esa aplicación hello solicitada. |
| token_type |el tipo de token Hola siempre será portador. |
| state |Si un `state` parámetro se incluye en la solicitud de hello, hello mismo valor aparecerán en la respuesta de Hola. Hello aplicación debe comprobar que hello `state` valores de hello solicitud y respuesta son idénticos. |
| expires_in |¿Durante cuánto tiempo el token de acceso de hello es válida (en segundos). |
| ámbito |ámbitos de Hola Hola token de acceso es válida para. |

### <a name="error-response"></a>Respuesta de error
Las respuestas de error también pueden enviarse toohello el URI de redireccionamiento para que hello aplicación pueda controlarlos adecuadamente.  Para `prompt=none`, un error esperado tiene este aspecto:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen. También puede usar Hola cadena tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudarle a identificar la causa de raíz de Hola de un error de autenticación. |

Si recibe este error en la solicitud de iframe de hello, Hola usuario debe iniciar interactivamente en nuevo tooretrieve un nuevo token. Puede controlar esto de manera que tenga sentido para su aplicación.

## <a name="refresh-tokens"></a>Tokens de actualización
Los tokens de identificador y los tokens de acceso expiran tras un breve período de tiempo. La aplicación debe estar preparada toorefresh estos tokens periódicamente.  realizar cualquier tipo de símbolo (token), de toorefresh Hola misma solicitud iframe oculto que hemos usado en un ejemplo anterior, mediante el uso de hello `prompt=none` pasos toocontrol Azure AD de parámetro.  tooreceive un nuevo `id_token` valor, ser seguro toouse `response_type=id_token` y `scope=openid`y un `nonce` parámetro.

## <a name="send-a-sign-out-request"></a>Envío de una solicitud de cierre de sesión
Si desea que el usuario de hello toosign fuera de la aplicación hello, redirigir Hola usuario tooAzure AD toosign out. Si no lo hace, el usuario de hello podría ser capaz de tooreauthenticate tooyour aplicaciones sin escribir sus credenciales de nuevo. Esto se debe a que el usuario tendrá una sesión válida de inicio de sesión único con Azure AD.

Simplemente puede redirigir Hola usuario toohello `end_session_endpoint` decir enumerado en hello mismo documento de metadatos de OpenID Connect se describe en [validar el token del identificador hello](#validate-the-id-token). Por ejemplo:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parámetro | ¿Necesario? | Description |
| --- | --- | --- |
| p |Obligatorio |Hola directiva toouse toosign Hola el usuario de la aplicación. |
| post_logout_redirect_uri |Recomendado |Hello ese usuario Hola de dirección URL debe ser redirigido tooafter correcta cierre de sesión. Si no se incluye, Azure AD B2C muestra un usuario de toohello mensaje genérico. |

> [!NOTE]
> Dirigir Hola usuario toohello `end_session_endpoint` borra algunos Hola del único inicio de sesión de estado del usuario con Azure AD B2C. Sin embargo, no inicie sesión usuario Hola fuera de sesión del usuario de hello del proveedor de identidades sociales. Si el usuario de hello selecciona Hola mismo identificar proveedor durante un inicio de sesión posteriores, se vuelve a autenticar el usuario de hello, sin proporcionar sus credenciales. Si un usuario desea toosign fuera de la aplicación de Azure AD B2C, no necesariamente significa que desean toocompletely cerrado su sesión en su cuenta de Facebook, por ejemplo. Sin embargo, para las cuentas locales, sesión de usuario de Hola se finalizará correctamente.
> 
> 

## <a name="use-your-own-azure-ad-b2c-tenant"></a>Usar su propio inquilino de Azure AD B2C
tootry estas solicitudes usted mismo, completar Hola siga tres pasos. Reemplace los valores de ejemplo de Hola que se usan en este artículo con sus propios valores:

1. [Crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md). Usar el nombre de hello del inquilino en las solicitudes de Hola.
2. [Crear una aplicación](active-directory-b2c-app-registration.md) tooobtain un identificador de aplicación y un `redirect_uri` valor. Incluya una aplicación web o una API web en la aplicación. Opcionalmente, puede crear un secreto de aplicación.
3. [Crear las directivas de](active-directory-b2c-reference-policies.md) tooobtain los nombres de directiva.

## <a name="samples"></a>Muestras

* [Creación de una aplicación de una página mediante Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi)
* [Creación de una aplicación de una página mediante .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi)

