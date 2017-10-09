---
title: Protocolo de Active Directory v2.0 y Hola OpenID Connect aaaAzure | Documentos de Microsoft
description: "Crear aplicaciones web mediante hello Azure AD v2.0 implementación del protocolo de autenticación de OpenID Connect de Hola."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a4875997-3aac-4e4c-b7fe-2b4b829151ce
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 277bb406dbb24ccefb09e4e4c928f0421755cf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory hello y v2.0 protocolo OpenID Connect
OpenID Connect es un protocolo de autenticación basado en OAuth 2.0 que puede usar el inicio de sesión de toosecurely en una aplicación web de tooa de usuario. Cuando se utiliza la implementación de hello v2.0 del punto de conexión de OpenID Connect, puede agregar el inicio de sesión y las aplicaciones basadas en web de API acceso tooyour. En este artículo, le mostraremos cómo toodo este independiente del idioma. Se describe cómo toosend y recibir mensajes HTTP sin usar las bibliotecas de código abierto de Microsoft.

> [!NOTE]
> el punto de conexión de Hello v2.0 no admite todas las características y escenarios de Azure Active Directory. toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) extiende hello OAuth 2.0 *autorización* toouse de protocolo como un *autenticación* de protocolo, por lo que puede realizar solo mediante OAuth en Inicio de sesión. OpenID Connect introduce el concepto de Hola de un *identificador de token*, que es un token de seguridad que permite que el cliente de hello tooverify Hola identidad de hello usuario. token de Id. de Hello también obtiene información de perfil básico sobre usuario Hola. Puesto que OpenID Connect amplía OAuth 2.0, aplicaciones de forma segura pueden adquirir *tokens de acceso*, lo que puede ser usado tooaccess recursos que están protegidos por un [servidor de autorización](active-directory-v2-protocols.md#the-basics). Se recomienda usar OpenID Connect si compila una [aplicación web](active-directory-v2-flows.md#web-apps) hospedada en un servidor y a la que se obtiene acceso a través de un explorador.

## Diagrama de protocolo: inicio de sesión
Hello flujo de inicio de sesión más básico tiene pasos Hola se muestra en el diagrama siguiente Hola. En este artículo se describe detalladamente cada paso.

![Protocolo OpenID Connect: inicio de sesión](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

## Capturar el documento de metadatos de OpenID Connect de Hola
OpenID Connect describe un documento de metadatos que contiene la mayor parte de información de hello necesaria para un inicio de sesión tooperform de aplicación. Esto incluye información como toouse de direcciones URL de Hola y la ubicación de Hola de las claves de firma pública del servicio de Hola. Para el punto de conexión de hello v2.0, trata de hello OpenID Connect metadatos documento que debe utilizar:

```
https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration
```

Hola `{tenant}` puede tomar uno de cuatro valores:

| Valor | Descripción |
| --- | --- |
| `common` |Los usuarios con una cuenta Microsoft personal y una cuenta profesional o educativa de Azure Active Directory (Azure AD) pueden iniciar sesión en la aplicación toohello. |
| `organizations` |Solo los usuarios con trabajar o cuentas de escuela de Azure AD pueden iniciar sesión en la aplicación toohello. |
| `consumers` |Solo los usuarios con una cuenta Microsoft personal pueden iniciar sesión en la aplicación toohello. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` o `contoso.onmicrosoft.com` |Solo los usuarios con una cuenta profesional o educativa de un anuncio de Azure específica inquilino puede iniciar sesión en aplicaciones de toohello. Nombre de dominio descriptivo de Hola Hola inquilino de Azure AD, o bien puede usarse el identificador GUID del inquilino de Hola. |

metadatos de Hello están un documento de JavaScript Object Notation (JSON) simple. Vea el siguiente fragmento de código para obtener un ejemplo de Hola. Hello contenido del fragmento de código se describe con detalle en hello [especificación OpenID Connect](https://openid.net).

```
{
  "authorization_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/authorize",
  "token_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_post",
    "private_key_jwt"
  ],
  "jwks_uri": "https:\/\/login.microsoftonline.com\/common\/discovery\/v2.0\/keys",

  ...

}
```

Normalmente, usaría este documento de metadatos tooconfigure una biblioteca de OpenID Connect o SDK; biblioteca de Hello utilizaría Hola metadatos toodo su trabajo. Sin embargo, si no usa una biblioteca de OpenID Connect de anterior a la compilación, puede seguir los pasos de hello en el resto de Hola de este artículo tooperform inicio de sesión en una aplicación web usando el punto de conexión de hello v2.0.

## Enviar solicitud de inicio de sesión de Hola
Cuando la aplicación web necesita usuario de hello tooauthenticate, puede dirigir Hola usuario toohello `/authorize` punto de conexión. Esta solicitud es similar toohello primer segmento del hello [flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md), con estas diferencias importantes:

* solicitud de Hello debe incluir hello `openid` ámbito Hola `scope` parámetro.
* Hola `response_type` debe incluir el parámetro `id_token`.
* solicitud de Hello debe incluir hello `nonce` parámetro.

Por ejemplo:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=678910
```

> [!TIP]
> Haga clic en hello siguiendo el vínculo tooexecute esta solicitud. Después de iniciar la sesión, el explorador será redirigido toohttps://localhost/myapp/, con un identificador de token en la barra de direcciones de Hola. Tenga en cuenta que esta solicitud usa `response_mode=query` (solo con fines de demostración). Se recomienda que use `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid&response_mode=query&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Parámetro | Condición | Descripción |
| --- | --- | --- |
| tenant |Obligatorio |Puede usar hello `{tenant}` valor de ruta de acceso de Hola de hello toocontrol de solicitud que puede iniciar sesión en la aplicación toohello. Hola valores permitidos son `common`, `organizations`, `consumers`y los identificadores de inquilinos. Para más información, consulte los [conceptos básicos sobre el protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |Obligatorio |Hola aplicación Id. que hello [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) asignado tooyour aplicación. |
| response_type |Obligatorio |Debe incluir `id_token` para el inicio de sesión en OpenID Connect. También puede incluir otros valores `response_types`, como `code`. |
| redirect_uri |Recomendado |Hola URI de redireccionamiento de la aplicación, donde las respuestas de autenticación pueden ser enviadas y recibidas por la aplicación. Debe coincidir exactamente con uno de redirección de hello URI que registró en el portal de hello, salvo que será la dirección URL codifican. |
| ámbito |Obligatorio |Una lista de ámbitos separada por espacios. Para OpenID Connect, debe incluir el ámbito de hello `openid`, que traduce toohello "Iniciar sesión en" permiso en la IU de consentimiento del saludo. También puede incluir otros ámbitos en esta solicitud para solicitar el consentimiento. |
| valor de seguridad |Obligatorio |Un valor incluido en solicitud de hello, generado por la aplicación hello, que se incluirán en el valor de hello resultante id_token como una notificación. aplicación Hello puede comprobar que los ataques de reproducción de tokens de toomitigate este valor. valor de Hello normalmente es una cadena aleatoria única que puede ser usado tooidentify Hola origen de solicitud de Hola. |
| response_mode |Recomendado |Especifica el método de Hola que debe ser usado toosend Hola resultante autorización código tooyour back-app. Puede ser `query`, `form_post` o `fragment`. Para las aplicaciones web, se recomienda usar `response_mode=form_post`, tooensure Hola transferencia más segura de aplicación de tooyour de símbolos (tokens). |
| state |Recomendado |Un valor incluido en la solicitud de Hola que también se devolverá como respuesta de token de Hola. Puede ser una cadena de cualquier contenido que desee. Un valor único generado aleatoriamente normalmente se utiliza demasiado[evitar los ataques de falsificación de solicitud entre sitios](http://tools.ietf.org/html/rfc6749#section-10.12). estado de Hello también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido la solicitud de autenticación de hello, como usuarios de Hola de página o la vista de Hola se realizó. |
| símbolo del sistema |Opcional |Indica el tipo de hello de interacción del usuario que es necesario. Hello solo los valores válidos en este momento son `login`, `none`, y `consent`. Hola `prompt=login` notificación fuerza Hola tooenter usuario sus credenciales en esa solicitud, lo que niega el inicio de sesión único. Hola `prompt=none` notificación es hello opuesto. Esta notificación se asegura de que el usuario hello no se presenta con cualquier mensaje interactivo ningún tipo.. Si no se puede completar de solicitud de Hola a través de un inicio de sesión único en modo silencioso, el punto de conexión de hello v2.0 devuelve un error. Hola `prompt=consent` notificación desencadenadores Hola cuadro de diálogo de consentimiento de OAuth después Hola usuario inicie sesión. cuadro de diálogo de Hello solicita permisos toohello aplicación de hello usuario toogrant. |
| login_hint |Opcional |Puede utilizar este parámetro toopre relleno Hola nombre de usuario y correo electrónico campo de dirección de página de inicio de sesión de hello para el usuario de hello, si conoce el nombre de usuario de hello antelación. A menudo, las aplicaciones usan este parámetro durante la reautenticación, después de extraer ya el nombre de usuario de Hola desde un inicio de sesión anterior mediante el uso de hello `preferred_username` de notificación. |
| domain_hint |Opcional |Este valor puede ser `consumers` o `organizations`. Si se incluye, omite el proceso de detección basada en correo electrónico de hello ese usuario Hola pasa por de hello v2.0 página de inicio, para una experiencia de usuario ligeramente más sencilla. A menudo, las aplicaciones usan este parámetro durante la reautenticación extrayendo Hola `tid` notificación de token de Id. de Hola. Si hello `tid` es el valor de notificación `9188040d-6c67-4c5b-b112-36a304b66dad`, utilice `domain_hint=consumers`. De lo contrario, use `domain_hint=organizations`. |

En este momento, los usuarios de hello es tooenter solicitada sus credenciales y autenticación de hello completa. Hello v2.0 extremo comprueba dicho usuario Hola ha dado su consentimiento permisos de toohello indicados en hello `scope` parámetro de consulta. Si hello no haya consentido tooany de estos permisos, el punto de conexión de hello v2.0 solicita tooconsent toohello requerido permisos de hello usuario. Puede leer más información sobre los [permisos, el consentimiento y las aplicaciones multiinquilino](active-directory-v2-scopes.md).

Después de usuario de Hola se autentica y concede el consentimiento, Hola v2.0 extremo devuelve indica una aplicación de tooyour de respuesta en hello URI de redireccionamiento mediante método hello especificado en hello `response_mode` parámetro.

### Respuesta correcta
Una respuesta correcta cuando usa `response_mode=form_post` tiene el aspecto siguiente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parámetro | Description |
| --- | --- |
| ID_token |Hello Id. de símbolo (token) que solicita la aplicación hello. Puede usar hello `id_token` parámetro tooverify Hola la identidad del usuario y empezar una sesión de usuario de Hola. Para obtener más información acerca de los tokens de identificador y su contenido, vea hello [v2.0 extremo tokens referencia](active-directory-v2-tokens.md). |
| state |Si un `state` parámetro se incluye en la solicitud de hello, hello mismo valor aparecerán en la respuesta de Hola. aplicación Hello debe comprobar que los valores de estado de hello en hello solicitud y respuesta son idénticos. |

### Respuesta de error
Las respuestas de error podrían también enviar toohello el URI de redireccionamiento para que hello aplicación pueda controlarlos. Una respuesta de error tiene el aspecto siguiente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que se pueden usar tipos de tooclassify de errores que se producen y tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudarle a identificar la causa de raíz de Hola de un error de autenticación. |

### Códigos de error correspondientes a errores de puntos de conexión de autorización
Hello tabla siguiente describen los códigos de error que pueden devolverse en hello `error` parámetro de respuesta de error de hello:

| Código de error | Descripción | Acción del cliente |
| --- | --- | --- |
| invalid_request |Error de protocolo, como un parámetro obligatorio que falta. |Corrija y vuelva a enviar la solicitud de saludo. Se trata de un error de desarrollo que habitualmente se detecta durante las pruebas iniciales. |
| unauthorized_client |aplicación de cliente de Hello no puede solicitar un código de autorización. |Esto suele ocurrir cuando la aplicación de cliente de hello no está registrado en Azure AD o no se agrega el inquilino de Azure AD del usuario toohello. aplicación Hello puede solicitar al usuario Hola con aplicación de instrucciones tooinstall hello y agregar tooAzure AD. |
| access_denied |propietario del recurso de Hello ha denegado el consentimiento. |aplicación de cliente de Hello puede notificar a usuario de Hola que no puede continuar a menos que el consentimiento del usuario de Hola. |
| unsupported_response_type |servidor de autorización de Hola no admite el tipo de respuesta de hello en solicitud de Hola. |Corrija y vuelva a enviar la solicitud de saludo. Se trata de un error de desarrollo que habitualmente se detecta durante las pruebas iniciales. |
| server_error |servidor de Hello detectó un error inesperado. |Vuelva a intentar la solicitud de saludo. Estos errores pueden deberse a condiciones temporales. aplicación de cliente de Hello puede explicar toohello usuario que su respuesta se retrasa debido a error temporal tooa. |
| temporarily_unavailable |servidor de Hello está temporalmente solicitud de hello toohandle demasiado ocupado. |Vuelva a intentar la solicitud de saludo. aplicación de cliente de Hello puede explicar toohello usuario que su respuesta se retrasa debido a tooa de condición temporal. |
| invalid_resource |recurso de destino de Hello no es válido porque no existe, Azure AD no la encuentra o no está configurado correctamente. |Esto indica que el recurso de hello, si existe, no se configuró en el inquilino de Hola. aplicación Hello puede solicitar a usuario Hola con instrucciones para instalar la aplicación hello y agregar tooAzure AD. |

## Validar el token del identificador hello
Recibir un identificador de token no es usuario de hello tooauthenticate suficiente. También debe validar la firma del token de Id. de Hola y Hola notificaciones en el token de hello según los requisitos de la aplicación. Hola v2.0 extremo utiliza [Tokens de Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) y públicos tokens toosign de criptografía de clave y compruebe que son válidos.

Puede elegir token de Id. de toovalidate hello en el código de cliente, pero una práctica común es el servidor back-end tooa símbolo (token) de toosend Hola ID y realizar la validación de hello no existe. Después de comprobar firma Hola de token de Id. de hello, deberá tooverify algunas notificaciones. Para obtener más información, incluida la más sobre [validar los tokens](active-directory-v2-tokens.md#validating-tokens) y [información importante acerca de la sustitución de la clave de firma](active-directory-v2-tokens.md#validating-tokens), vea hello [v2.0 tokens referencia](active-directory-v2-tokens.md). Se recomienda el uso de una biblioteca tooparse y validar los tokens. Hay al menos una de estas bibliotecas disponibles para la mayoría de los lenguajes y plataformas.
<!--TODO: Improve hello information on this-->

También conviene toovalidate notificaciones adicionales, según el escenario. Algunas validaciones comunes incluyen:

* Asegúrese de que el usuario de Hola o la organización ha suscrito para aplicación hello.
* Asegúrese de que ese usuario Hola necesita autorización o privilegios.
* Asegurarse de que se produjo un determinado nivel de autenticación, como la autenticación multifactor.

Para obtener más información sobre notificaciones de hello en un identificador de token, consulte hello [v2.0 extremo tokens referencia](active-directory-v2-tokens.md).

Después de haber validado por completo el token del identificador hello, puede comenzar una sesión por usuario de Hola. Utilizar notificaciones de hello en información de token tooget de Id. de hello acerca del usuario de hello en la aplicación. Puede usar esta información para su visualización, registros, autorizaciones, etc.

## Envío de una solicitud de cierre de sesión
Cuando quiera toosign usuario Hola desde su aplicación, no es suficiente tooclear las cookies de la aplicación o en caso contrario, finalizar la sesión del usuario de Hola. También se debe redirigir Hola usuario toohello v2.0 extremo toosign out. Si no lo hace, usuario Hola vuelve a autentica tooyour aplicación sin escribir sus credenciales de nuevo, porque tienen una válido única inicio de sesión con el punto de conexión de hello v2.0.

Puede redirigir Hola usuario toohello `end_session_endpoint` enumerados en el documento de metadatos de hello OpenID Connect:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
```

| Parámetro | Condición | Descripción |
| ----------------------- | ------------------------------- | ------------ |
| post_logout_redirect_uri | Recomendado | dirección URL de Hola Hola usuario es redirigido tooafter cierre de sesión correctamente. Si no se incluye el parámetro hello, usuario Hola se muestra un mensaje genérico que se genera por el punto de conexión de hello v2.0. Esta dirección URL debe coincidir con uno de redireccionamiento de hello que URI registrado para la aplicación de portal de registro de aplicación Hola.  |

## Cierre de sesión único
Al redirigir Hola usuario toohello `end_session_endpoint`, el punto de conexión de hello v2.0 borra la sesión del usuario de Hola desde el Explorador de Hola. Sin embargo, puede estar firmado todavía usuario hello en aplicaciones de tooother que utilizan cuentas de Microsoft para la autenticación. tooenable esas aplicaciones toosign Hola un usuario al mismo tiempo, el extremo de v2.0 Hola envía una toohello de solicitud HTTP GET registrado `LogoutUrl` de todas las aplicaciones de hello ese usuario Hola actualmente ha iniciado sesión para. Las aplicaciones deben responder toothis solicitud desactivando cualquier sesión que identifica el usuario de Hola y devolver un `200` respuesta.  Si lo desea alejar toosupport inicio de sesión único en la aplicación, debe implementar como una `LogoutUrl` en el código de la aplicación.  Puede establecer hello `LogoutUrl` desde el portal de registro de aplicación Hola.

## Diagrama de protocolo: adquisición de tokens
Muchas aplicaciones web necesitan toonot usuario de Hola de inicio de sesión único en, sino también tooaccess un servicio web en nombre de usuario de hello mediante OAuth. Este escenario combina OpenID Connect para la autenticación de usuario al obtener una autorización de forma simultánea los tokens de código que puede usar el acceso tooget si usa flujo de código de autorización de OAuth de Hola.

Hola completa OpenID Connect sesión y flujo de adquisición de tokens examina el diagrama siguiente de toohello similar. Se describe cada paso en detalle en las siguientes secciones de Hola de artículo Hola.

![Protocolo OpenID Connect: adquisición de tokens](../../media/active-directory-v2-flows/convergence_scenarios_webapp_webapi.png)

## Obtención de tokens de acceso
los tokens de acceso tooacquire, modificar una solicitud de inicio de sesión hello:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application ID
&response_type=id_token%20code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered redirect URI, URL encoded
&response_mode=form_post                              // 'query', 'form_post', or 'fragment'
&scope=openid%20                                      // Include both 'openid' and scopes that your app needs  
offline_access%20                                         
https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

> [!TIP]
> Haga clic en hello siguiendo el vínculo tooexecute esta solicitud. Después de iniciar la sesión, el explorador es redirigido toohttps://localhost/myapp/, con un identificador de token y un código en la barra de direcciones de Hola. Tenga en cuenta que esta solicitud usa `response_mode=query` (solo con fines de demostración). Se recomienda que use `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token%20code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

Mediante la inclusión de ámbitos de permiso de solicitud de Hola y `response_type=id_token code`, el punto de conexión de hello v2.0 garantiza que ese usuario Hola ha dado su consentimiento permisos de toohello indicados en hello `scope` parámetro de consulta. Devuelve una tooexchange de aplicación de tooyour de código de autorización para un token de acceso.

### Respuesta correcta
Una respuesta correcta al usar `response_mode=form_post` tiene el siguiente aspecto:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Parámetro | Description |
| --- | --- |
| ID_token |Hello Id. de símbolo (token) que solicita la aplicación hello. Puede usar identidad de usuario de hello identificador tooverify token hello y empezar una sesión de usuario de Hola. Encontrará más detalles sobre los tokens de identificador y su contenido en hello [v2.0 extremo tokens referencia](active-directory-v2-tokens.md). |
| código |código de autorización de Hola Hola aplicación solicitada. aplicación Hello puede utilizar toorequest de código de autorización de hello un token de acceso para el recurso de destino de Hola. Un código de autorización tiene una duración muy breve. Habitualmente, un código de autorización expira en alrededor de 10 minutos. |
| state |Si un parámetro de estado se incluye en la solicitud de hello, Hola debe aparecer el mismo valor en respuesta de Hola. aplicación Hello debe comprobar que los valores de estado de hello en hello solicitud y respuesta son idénticos. |

### Respuesta de error
Las respuestas de error se podrían también enviar toohello el URI de redireccionamiento para que hello aplicación pueda controlarlos adecuadamente. Una respuesta de error tiene el aspecto siguiente:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que se pueden usar tipos de tooclassify de errores que se producen y tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudarle a identificar la causa de raíz de Hola de un error de autenticación. |

Para una descripción de los posibles códigos de error y las respuestas de cliente recomendadas, consulte [Códigos de error correspondientes a errores de puntos de conexión de autorización](#error-codes-for-authorization-endpoint-errors).

Si tiene un código de autorización y un identificador de token, puede iniciar sesión del usuario hello y obtener tokens de acceso en su nombre. usuario de hello toosign de, debe validar el token del identificador hello [tal y como se describe](#validate-the-id-token). tokens de acceso de tooget, siga los pasos de hello descritos en nuestro [documentación del protocolo OAuth](active-directory-v2-protocols-oauth-code.md#request-an-access-token).
