---
title: "Hola aaaUnderstand flujo del código de autenticación de OpenID Connect de Azure AD | Documentos de Microsoft"
description: "Este artículo describe cómo acceder a toouse HTTP mensajes tooauthorize tooweb aplicaciones y las API web en el inquilino con Azure Active Directory y OpenID Connect."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 29142f7e-d862-4076-9a1a-ecae5bcd9d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: fafd8ab906ee576c584fec2ef1e9de83ddb1f6e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Autorizar acceso tooweb aplicaciones con Azure Active Directory y OpenID Connect
[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) es una capa de identidad sencilla creada por encima de protocolo de hello OAuth 2.0. OAuth 2.0 define mecanismos tooobtain y uso **tokens de acceso** tooaccess los recursos protegidos, pero no definen información de identidad de tooprovide métodos estándar. OpenID Connect, la autenticación se implementa como un proceso de autorización de OAuth 2.0 toohello de extensión. Proporciona información sobre el usuario final de hello en forma de Hola de un `id_token` que comprueba la identidad de saludo del usuario de Hola y proporciona información de perfil básico sobre usuario Hola.

Nosotros recomendamos OpenID Connect si va a crear una aplicación web que está hospedada en un servidor y a la que se accede mediante un explorador.


[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)] 

## Flujo de autenticación con OpenID Connect
el flujo de inicio de sesión más sencilla de Hello contiene Hola pasos: cada uno de ellos se describe en detalle más adelante.

![Flujo de autenticación de OpenID Connect](media/active-directory-protocols-openid-connect-code/active-directory-oauth-code-flow-web-app.png)

## Documento de metadatos de OpenID Connect

OpenID Connect describe un documento de metadatos que contiene la mayor parte de información de hello necesaria para un inicio de sesión tooperform de aplicación. Esto incluye información como toouse de direcciones URL de Hola y la ubicación de Hola de las claves de firma pública del servicio de Hola. documento de metadatos de Hello OpenID Connect se puede encontrar en:

```
https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration
```
metadatos de Hello están un documento de JavaScript Object Notation (JSON) simple. Vea el siguiente fragmento de código para obtener un ejemplo de Hola. Hello contenido del fragmento de código se describe con detalle en hello [especificación OpenID Connect](https://openid.net).

```
{
    "authorization_endpoint": "https://login.microsoftonline.com/common/oauth2/authorize",
    "token_endpoint": "https://login.microsoftonline.com/common/oauth2/token",
    "token_endpoint_auth_methods_supported":
    [
        "client_secret_post",
        "private_key_jwt"
    ],
    "jwks_uri": "https://login.microsoftonline.com/common/discovery/keys"
    
    ...
}
```

## Enviar solicitud de inicio de sesión de Hola
Cuando la aplicación web necesita usuario de hello tooauthenticate, deben dirigir el Hola usuario toohello `/authorize` punto de conexión. Esta solicitud es similar toohello primer segmento del hello [flujo de código de autorización de OAuth 2.0](active-directory-protocols-oauth-code.md), con algunas diferencias importantes:

* solicitud de Hello debe incluir el ámbito de hello `openid` en hello `scope` parámetro.
* Hola `response_type` debe incluir el parámetro `id_token`.
* solicitud de Hello debe incluir hello `nonce` parámetro.

Por tanto, una solicitud de muestra tendría el siguiente aspecto:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=7362CAEA-9CA5-4B43-9BA3-34D7C303EBA7
```

| Parámetro |  | Description |
| --- | --- | --- |
| tenant |requerido |Hola `{tenant}` valor de ruta de acceso de saludo de solicitud de hello puede ser usado toocontrol que puede iniciar sesión en la aplicación hello.  Hola valores permitidos son identificadores de inquilino, por ejemplo, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` o `contoso.onmicrosoft.com` o `common` para los tokens de independientes del inquilino |
| client_id |requerido |Hola Id. de aplicación asignado tooyour aplicación cuando se registra con Azure AD. Puede encontrar esto en hello Portal de Azure. Haga clic en **Azure Active Directory**, haga clic en **registros de aplicación**, elija aplicación hello y busque Hola Id. de aplicación en la página de aplicación Hola. |
| response_type |requerido |Debe incluir `id_token` para el inicio de sesión en OpenID Connect.  También puede incluir otros elementos response_type como `code`. |
| ámbito |requerido |Una lista de ámbitos separada por espacios.  Para OpenID Connect, debe incluir el ámbito de hello `openid`, que traduce toohello "Iniciar sesión en" permiso en la IU de consentimiento del saludo.  También puede incluir otros ámbitos en esta solicitud para solicitar el consentimiento. |
| valor de seguridad |requerido |Un valor incluido en solicitud de hello, generado por la aplicación hello, que se incluye en hello resultante `id_token` como una notificación.  aplicación Hello, a continuación, puede comprobar que los ataques de reproducción de tokens de toomitigate este valor.  valor de Hello suele ser una cadena aleatorio, único o un GUID que puede ser utilizados tooidentify Hola origen de solicitud de Hola. |
| redirect_uri |recomendado |Hola redirect_uri de la aplicación, donde las respuestas de autenticación pueden ser enviadas y recibidas por la aplicación.  Debe coincidir exactamente con uno de redirect_uris Hola que registró en el portal de hello, salvo que debe ser la dirección url codificada. |
| response_mode |recomendado |Especifica el método de Hola que debe ser usado toosend Hola resultante authorization_code tooyour back-app.  Los valores admitidos son `form_post` para *envíos de formulario HTTP* o `fragment` para *fragmentos de dirección URL*.  Para las aplicaciones web, se recomienda usar `response_mode=form_post` tooensure Hola transferencia más segura de aplicación de tooyour de símbolos (tokens). |
| state |recomendado |Un valor incluido en la solicitud de Hola que se devuelve en la respuesta de token de Hola.  Puede ser una cadena de cualquier contenido que desee.  Normalmente se usa un valor único generado de forma aleatoria para [evitar los ataques de falsificación de solicitudes entre sitios](http://tools.ietf.org/html/rfc6749#section-10.12).  estado de Hello también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido en solicitud de autenticación de hello, como página de Hola o que estaban en la vista. |
| símbolo del sistema |opcional |Indica el tipo de hello de interacción del usuario que es necesario.  Hola actualmente, solo los valores válidos son 'login', 'none' y 'da su consentimiento'.  `prompt=login`fuerza Hola usuario tooenter sus credenciales en esa solicitud, niega inicio de sesión único.  `prompt=none`es Hola opuesto: garantiza que ese usuario hello no se presenta con cualquier interactivo solicitar ningún tipo.  Si no se puede completar de solicitud Hola a través de inicio de sesión único en modo silencioso, el punto de conexión de hello devuelve un error.  `prompt=consent`diálogo de consentimiento de OAuth de hello después de los signos de usuario de hello, pidiendo permisos toohello aplicación de hello usuario toogrant se desencadena. |
| login_hint |opcional |Puede ser el campo de dirección de nombre de usuario y de correo electrónico de relleno de toopre usado Hola de página de inicio de sesión de hello para el usuario de hello, si conoce su nombre de usuario antes de tiempo.  Aplicaciones a menudo usan este parámetro durante la reautenticación, tener extraído ya el nombre de usuario de Hola desde un inicio de sesión anterior con hello `preferred_username` de notificación. |

En este punto, es el usuario de hello más frecuentes tooenter sus credenciales y autenticación de hello completa.

### Respuesta de muestra
Una respuesta de ejemplo, una vez autenticado el usuario de hello, podría ser similar al siguiente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parámetro | Description |
| --- | --- |
| ID_token |Hola `id_token` esa aplicación hello solicitada. Puede usar hello `id_token` tooverify Hola la identidad del usuario e iniciar una sesión de usuario de Hola. |
| state |Un valor incluido en la solicitud de Hola que también se devuelve como respuesta de token de Hola. Normalmente se usa un valor único generado de forma aleatoria para [evitar los ataques de falsificación de solicitudes entre sitios](http://tools.ietf.org/html/rfc6749#section-10.12).  estado de Hello también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido en solicitud de autenticación de hello, como página de Hola o que estaban en la vista. |

### Respuesta de error
Las respuestas de error también se pueden enviar toohello `redirect_uri` por lo que puede controlar aplicación hello correctamente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen y puede ser usado tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudar a un desarrollador para identificar la causa de Hola de un error de autenticación. |

#### Códigos de error correspondientes a errores de puntos de conexión de autorización
Hello tabla siguiente describen Hola varios códigos de error que pueden devolverse en hello `error` parámetro de respuesta de error de Hola.

| Código de error | Description | Acción del cliente |
| --- | --- | --- |
| invalid_request |Error de protocolo, como un parámetro obligatorio que falta. |Corrija y vuelva a enviar la solicitud de saludo. Se trata de un error de desarrollo que suele detectarse durante las pruebas iniciales. |
| unauthorized_client |Hello aplicación cliente no está permitido toorequest un código de autorización. |Esto suele ocurrir cuando la aplicación de cliente de hello no está registrado en Azure AD o no se agrega el inquilino de Azure AD del usuario toohello. aplicación Hello puede solicitar a usuario Hola con instrucciones para instalar la aplicación hello y agregar tooAzure AD. |
| access_denied |El propietario del recurso ha denegado el consentimiento. |aplicación de cliente de Hello puede notificar a usuario de Hola que no puede continuar a menos que el consentimiento del usuario de Hola. |
| unsupported_response_type |servidor de autorización de Hola no admite el tipo de respuesta de hello en solicitud de Hola. |Corrija y vuelva a enviar la solicitud de saludo. Se trata de un error de desarrollo que suele detectarse durante las pruebas iniciales. |
| server_error |servidor de Hello detectó un error inesperado. |Vuelva a intentar la solicitud de saludo. Estos errores pueden deberse a condiciones temporales. aplicación de cliente de Hello puede explicar toohello usuario que su respuesta se retrasa debido a error temporal tooa. |
| temporarily_unavailable |servidor de Hello está temporalmente solicitud de hello toohandle demasiado ocupado. |Vuelva a intentar la solicitud de saludo. aplicación de cliente de Hello puede explicar toohello usuario que su respuesta se retrasa debido a tooa de condición temporal. |
| invalid_resource |recurso de destino de Hello no es válido porque no existe, Azure AD no la encuentra o no está configurado correctamente. |Esto indica recursos hello, si existe, no se configuró en el inquilino de Hola. aplicación Hello puede solicitar a usuario Hola con instrucciones para instalar la aplicación hello y agregar tooAzure AD. |

## Validar hello id_token
Acaba de recibir un `id_token` no es suficiente tooauthenticate Hola usuario debe validar la firma de Hola y notificaciones de Hola Hola `id_token` según los requisitos de la aplicación. extremo de Azure AD de Hello usa Tokens de Web JSON (Jwt) y símbolos (tokens) de criptografía de clave pública toosign y verificar que son válidos.

Puede elegir hello toovalidate `id_token` en el código de cliente, pero una práctica común es hello toosend `id_token` tooa servidor de back-end y realizar la validación de hello no existe. Una vez que haya validado firma Hola de hello `id_token`, hay algunas notificaciones están tooverify necesario.

También puede llamar toovalidate demandas adicionales según el escenario. Algunas validaciones comunes incluyen:

* Garantizar Hola usuario u organización ha registrado para la aplicación hello.
* Usuario de hello asegurar que tiene autorización o los privilegios adecuados
* Asegurarse de que se haya producido un determinado nivel de autenticación, como la autenticación multifactor.

Una vez que valide hello `id_token`, puede empezar una sesión de usuario de Hola y usar notificaciones de Hola Hola `id_token` tooobtain información acerca del usuario de hello en la aplicación. Esta información puede utilizarse para su visualización, registros, autorizaciones, etc. Para obtener más información sobre los tipos de token de Hola y notificaciones, lea [admite tokens y los tipos de notificación](active-directory-token-and-claims.md).

## Envío de una solicitud de cierre de sesión
Cuando se desea que el usuario de hello toosign fuera de la aplicación hello, es tooclear no son suficiente las cookies de la aplicación o en caso contrario, finalizar sesión de hello con usuario Hola.  También se debe redirigir Hola usuario toohello `end_session_endpoint` de cierre de sesión.  Si no toodo por lo tanto, el usuario de hello será capaz de tooreauthenticate tooyour aplicaciones sin escribir sus credenciales de nuevo, porque tienen una única inicio de sesión sesión válida con el punto de conexión de hello Azure AD.

Simplemente puede redirigir Hola usuario toohello `end_session_endpoint` enumerados en el documento de metadatos de hello OpenID Connect:

```
GET https://login.microsoftonline.com/common/oauth2/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F

```

| Parámetro |  | Descripción |
| --- | --- | --- |
| post_logout_redirect_uri |recomendado |dirección URL de Hola que Hola usuario debe ser redirigido tooafter cierre de sesión correcto.  Si no se incluye usuario Hola se muestra un mensaje genérico. |

## Cierre de sesión único
Al redirigir Hola usuario toohello `end_session_endpoint`, Azure AD borra la sesión del usuario de Hola desde el Explorador de Hola. Sin embargo, puede estar firmado todavía usuario hello en aplicaciones de tooother que usan Azure AD para la autenticación. tooenable esos toosign aplicaciones Hola de un usuario al mismo tiempo, Azure AD envía una toohello de solicitud HTTP GET registrado `LogoutUrl` de todas las aplicaciones de hello ese usuario Hola actualmente ha iniciado sesión para. Las aplicaciones deben responder toothis solicitud desactivando cualquier sesión que identifica el usuario de Hola y devolver un `200` respuesta.  Si lo desea alejar toosupport inicio de sesión único en la aplicación, debe implementar como una `LogoutUrl` en el código de la aplicación.  Puede establecer hello `LogoutUrl` de hello portal de Azure:

1. Navegue toohello [Portal de Azure](https://portal.azure.com).
2. Elija su Active Directory, haga clic en su cuenta en hello superior derecho de la página de Hola.
3. Desde el panel de navegación izquierdo de hello, elija **Azure Active Directory**, a continuación, elija **registros de aplicación** y seleccione la aplicación.
4. Haga clic en **propiedades** y buscar hello **Logout URL** cuadro de texto. 

## Obtención de tokens
Muchas aplicaciones web necesitan toonot usuario de Hola de inicio de sesión único en, pero también tener acceso a un servicio web en nombre del usuario con OAuth. Este escenario combina OpenID Connect para la autenticación de usuario al adquirir simultáneamente una `authorization_code` que puede ser usado tooget `access_tokens` utilizando Hola flujo de código de autorización de OAuth.

## Obtención de tokens de acceso
los tokens de acceso tooacquire, necesita toomodify Hola inicio de sesión de solicitud desde arriba:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application Id
&response_type=id_token+code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered Redirect Uri, url encoded
&response_mode=form_post                              // form_post', or 'fragment'
&scope=openid
&resource=https%3A%2F%2Fservice.contoso.com%2F                                     
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

Incluidos los ámbitos de permiso en la solicitud de Hola y usando `response_type=code+id_token`, hello `authorize` extremo garantiza que ese usuario Hola ha dado su consentimiento permisos de toohello indicados en hello `scope` parámetro de consulta y devolver un código de autorización de la aplicación tooexchange para un token de acceso.

### Respuesta correcta
Una respuesta correcta al usar `response_mode=form_post` tiene el siguiente aspecto:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| . | Description |
| --- | --- |
| ID_token |Hola `id_token` esa aplicación hello solicitada. Puede usar hello `id_token` tooverify Hola la identidad del usuario e iniciar una sesión de usuario de Hola. |
| código |Hola authorization_code que Hola aplicación solicitada. aplicación Hello puede utilizar toorequest de código de autorización de hello un token de acceso para el recurso de destino de Hola. Los authorization_codes son de corta duración y normalmente expiran después de unos 10 minutos. |
| state |Si un parámetro de estado se incluye en la solicitud de hello, Hola debe aparecer el mismo valor en respuesta de Hola. aplicación Hello debe comprobar que los valores de estado de hello en hello solicitud y respuesta son idénticos. |

### Respuesta de error
Las respuestas de error también se pueden enviar toohello `redirect_uri` por lo que puede controlar aplicación hello correctamente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen y puede ser usado tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudar a un desarrollador para identificar la causa de Hola de un error de autenticación. |

Para obtener una descripción de los códigos de error posibles hello y su acción de cliente recomendada, consulte [códigos de Error para errores de autorización de punto de conexión](#error-codes-for-authorization-endpoint-errors).

Una vez que ha llegado una autorización `code` y `id_token`, puede iniciar sesión del usuario hello y obtener tokens de acceso en su nombre.  usuario de hello toosign de, debe validar hello `id_token` tal y como se ha descrito anteriormente. tokens de acceso de tooget, puede seguir los pasos de Hola se describe en la sección "Usar toorequest de código de autorización de hello un token de acceso" de Hola de nuestro [documentación del protocolo OAuth](active-directory-protocols-oauth-code.md).
