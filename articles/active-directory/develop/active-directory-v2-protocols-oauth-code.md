---
title: "v2.0 aaaAzure AD flujo de código de autorización de OAuth | Documentos de Microsoft"
description: "Creación de aplicaciones web mediante la implementación de Azure AD hello OAuth 2.0 del protocolo de autenticación."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: dee58f2f5c627fef35cae279349728c3c7bf9421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Protocolos de la versión 2.0: Flujo de código de autorización de OAuth 2.0
concesión de código de autorización de Hello OAuth 2.0 puede utilizarse en aplicaciones que están instaladas en un dispositivo toogain acceder a tooprotected recursos, como las API web.  Mediante la implementación del v2.0 del modelo de aplicación Hola de OAuth 2.0, puede agregar inicio de sesión y API de aplicaciones de escritorio y móviles de tooyour.  Esta guía es independiente del lenguaje y se describe cómo toosend y recibir mensajes HTTP sin usar cualquiera de nuestras bibliotecas de código abierto.

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.  toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

Hola flujo de código de autorización de OAuth 2.0 se describe en [sección 4.1 de especificación de hello OAuth 2.0](http://tools.ietf.org/html/rfc6749).  Es tooperform usa autenticación y autorización en la mayoría de Hola de los tipos de aplicación, incluidos los [aplicaciones web](active-directory-v2-flows.md#web-apps) y [instalado de forma nativa aplicaciones](active-directory-v2-flows.md#mobile-and-native-apps).  Permite que las aplicaciones toosecurely adquirir access_tokens que pueden ser utilizados tooaccess recursos que se protegen mediante el punto de conexión de hello v2.0.  

## Diagrama de protocolo
En un nivel alto, flujo de autenticación en su totalidad de Hola para una aplicación nativa/mobile un poco este aspecto:

![Flujo de código de autenticación de OAuth](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## Solicitud de un código de autorización
flujo de código de autorización de Hello comienza con cliente hello dirigir Hola usuario toohello `/authorize` punto de conexión.  En esta solicitud, cliente hello indica permisos de Hola que necesita tooacquire de usuario de hello:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> Haga clic en vínculo hello tooexecute esta solicitud. Después de iniciar sesión, el explorador se debe redirigir demasiado`https://localhost/myapp/` con un `code` en la barra de direcciones de Hola.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Parámetro |  | Description |
| --- | --- | --- |
| tenant |requerido |Hola `{tenant}` valor de ruta de acceso de saludo de solicitud de hello puede ser usado toocontrol que puede iniciar sesión en la aplicación hello.  Hola valores permitidos son `common`, `organizations`, `consumers`y los identificadores de inquilinos.  Para obtener más información, consulte los [conceptos básicos sobre el protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |requerido |Hola Id. de aplicación ese portal de registro de hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) asignado a la aplicación. |
| response_type |requerido |Debe incluir `code` para el flujo de código de autorización de Hola. |
| redirect_uri |recomendado |Hola redirect_uri de la aplicación, donde las respuestas de autenticación pueden ser enviadas y recibidas por la aplicación.  Debe coincidir exactamente con uno de redirect_uris Hola que registró en el portal de hello, salvo que debe ser la dirección url codificada.  Para las aplicaciones nativas & móviles, debe usar valor predeterminado de Hola de `https://login.microsoftonline.com/common/oauth2/nativeclient`. |
| ámbito |requerido |Una lista separada por espacios de [ámbitos](active-directory-v2-scopes.md) que desea tooconsent de usuario de Hola a. |
| response_mode |recomendado |Especifica el método de Hola que debe ser usado toosend Hola resultante token tooyour back-app.  Puede ser `query` o `form_post`. |
| state |recomendado |Un valor incluido en la solicitud de Hola que también se devolverán en respuesta de token de Hola.  Puede ser una cadena de cualquier contenido que desee.  Normalmente se usa un valor único generado de forma aleatoria para [evitar los ataques de falsificación de solicitudes entre sitios](http://tools.ietf.org/html/rfc6749#section-10.12).  estado de Hello también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido en solicitud de autenticación de hello, como página de Hola o que estaban en la vista. |
| símbolo del sistema |opcional |Indica el tipo de hello de interacción del usuario que es necesario.  Hola solo en este momento los valores válidos son 'login', 'none' y 'da su consentimiento'.  `prompt=login`se fuerza Hola a tooenter usuario sus credenciales en esa solicitud, niega el inicio de sesión único en.  `prompt=none`es Hola opuesto: se asegurará de que el usuario hello no se presenta con cualquier mensaje interactivo ningún tipo..  Si no se puede completar de solicitud Hola a través de inicio de sesión único en modo silencioso, el punto de conexión de hello v2.0 devolverá un error.  `prompt=consent`acepta Hola desencadenador OAuth diálogo después de los signos de usuario de hello, pidiendo permisos toohello aplicación de hello usuario toogrant. |
| login_hint |opcional |Puede ser campo de dirección de nombre de usuario y de correo electrónico usado toopre-relleno Hola del programa Hola a iniciar sesión página de usuario de hello, si conoce su nombre de usuario antes de tiempo.  A menudo las aplicaciones utilizarán este parámetro durante la reautenticación, tener extraído ya el nombre de usuario de Hola desde un inicio de sesión anterior con hello `preferred_username` de notificación. |
| domain_hint |opcional |Puede ser `consumers` o `organizations`.  Si se incluye, se omitirán proceso de detección basada en correo electrónico de Hola que el usuario pasa por de inicio de sesión de hello v2.0 en la página, a la izquierda tooa ligeramente más una mejor experiencia del usuario.  A menudo las aplicaciones utilizarán este parámetro durante la reautenticación, extrayendo hello `tid` desde un inicio de sesión anterior.  Si hello `tid` es el valor de notificación `9188040d-6c67-4c5b-b112-36a304b66dad`, debe usar `domain_hint=consumers`.  De lo contrario, use `domain_hint=organizations`. |

En este punto, el usuario de hello será más frecuentes tooenter sus credenciales y autenticación de hello completa.  Hello v2.0 extremo también garantizarán ese usuario Hola ha dado su consentimiento permisos de toohello indicados en hello `scope` parámetro de consulta.  Si hello no haya consentido tooany de estos permisos, le preguntará Hola usuario tooconsent toohello requerido permisos.  Aquí puede encontrar información detallada sobre los [permisos, el consentimiento y las aplicaciones multiempresa](active-directory-v2-scopes.md).

Una vez que el usuario de Hola se autentica y concede el consentimiento, el punto de conexión de hello v2.0 devolverá una aplicación de tooyour de respuesta en hello indicado `redirect_uri`, mediante el método hello especificado en hello `response_mode` parámetro.

#### Respuesta correcta
Una respuesta correcta al usar `response_mode=query` tiene el siguiente aspecto:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| . | Description |
| --- | --- |
| código |Hola authorization_code que Hola aplicación solicitada. aplicación Hello puede utilizar toorequest de código de autorización de hello un token de acceso para el recurso de destino de Hola.  Los authorization_codes son de muy corta duración, normalmente expiran después de unos 10 minutos. |
| state |Si un parámetro de estado se incluye en la solicitud de hello, Hola debe aparecer el mismo valor en respuesta de Hola. aplicación Hello debe comprobar que los valores de estado de hello en hello solicitud y respuesta son idénticos. |

#### Respuesta de error
Las respuestas de error también se pueden enviar toohello `redirect_uri` por lo que puede controlar aplicación hello correctamente:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
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
| server_error |servidor de Hello detectó un error inesperado. |Vuelva a intentar la solicitud de saludo. Estos errores pueden deberse a condiciones temporales. aplicación de cliente de Hello puede explicar toohello usuario que su respuesta se retrasa debido a un error temporal. |
| temporarily_unavailable |servidor de Hello está temporalmente solicitud de hello toohandle demasiado ocupado. |Vuelva a intentar la solicitud de saludo. aplicación de cliente de Hello puede explicar toohello usuario que su respuesta se retrasa debido a una condición temporal. |
| invalid_resource |recurso de destino de Hello no es válido porque no existe, Azure AD no la encuentra o no está configurado correctamente. |Esto indica recursos hello, si existe, no se configuró en el inquilino de Hola. aplicación Hello puede solicitar a usuario Hola con instrucciones para instalar la aplicación hello y agregar tooAzure AD. |

## Solicitud de un token de acceso
Ahora que ha adquirido un authorization_code y usuario Hola les ha concedido permiso, puede compensar hello `code` para un `access_token` toohello deseado recursos, mediante el envío de un `POST` solicitar toohello `/token` punto de conexión:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> Pruebe a ejecutar esta solicitud en Postman (No olvide hello tooreplace `code`) [ ![ejecutar en Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parámetro |  | Description |
| --- | --- | --- |
| tenant |requerido |Hola `{tenant}` valor de ruta de acceso de saludo de solicitud de hello puede ser usado toocontrol que puede iniciar sesión en la aplicación hello.  Hola valores permitidos son `common`, `organizations`, `consumers`y los identificadores de inquilinos.  Para obtener más información, consulte los [conceptos básicos sobre el protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |requerido |Hola Id. de aplicación ese portal de registro de hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) asignado a la aplicación. |
| grant_type |requerido |Debe ser `authorization_code` para el flujo de código de autorización de Hola. |
| ámbito |requerido |Una lista de ámbitos separada por espacios.  ámbitos de Hola solicitaron en esta bifurcación de la debe ser equivalente tooor un subconjunto de ámbitos de Hola solicitado en el primer segmento de Hola.  Si ámbitos Hola especificados en esta solicitud abarcan varios servidores de recursos, el punto de conexión de hello v2.0 devolverá un token para el recurso de hello especificada en el ámbito primera Hola.  Para obtener una explicación más detallada de ámbitos, consulte demasiado[permisos, ámbitos y consentimiento](active-directory-v2-scopes.md). |
| código |requerido |Hola authorization_code que adquirió en el primer segmento de hello del flujo de Hola. |
| redirect_uri |requerido |Hola el mismo valor de redirect_uri que se usa tooacquire hello authorization_code. |
| client_secret |necesario para las aplicaciones web |secreto de aplicación Hola que creó en el portal de registro de aplicación de hello para la aplicación.  No debería utilizarse en una aplicación nativa, porque los client_secrets no se pueden almacenar de forma confiable en los dispositivos.  Es necesario para las aplicaciones web y las API, que tienen Hola capacidad toostore hello client_secret de forma segura en el lado del servidor de hello web. |

#### Respuesta correcta
Una respuesta de token correcta tendrá un aspecto similar al siguiente:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parámetro | Description |
| --- | --- |
| access_token |símbolo (token) de acceso solicitado Hola. aplicación Hello puede usar este toohello tooauthenticate token protegida recursos, como una API web. |
| token_type |Indica el valor de tipo de token de Hola. solo el tipo que admite Azure AD Hello es portador |
| expires_in |¿Durante cuánto tiempo el token de acceso de hello es válida (en segundos). |
| ámbito |es válido para los ámbitos de Hola Hola access_token. |
| refresh_token |Un token de actualización de OAuth 2.0. Hello aplicación puede usar este token adquirir tokens de acceso adicionales después de que expire el token de acceso actual de Hola.  Refresh_tokens son de larga duración y puede ser usado tooretain acceso tooresources durante largos períodos de tiempo.  Para obtener información más detallada, consulte toohello [referencia del token v2.0](active-directory-v2-tokens.md). |
| ID_token |Un token web JSON (JWT) sin firmar. Hola aplicación can base64Url descodificar segmentos Hola de esta información de token toorequest acerca del usuario de hello inscrita en. puede almacenar en memoria caché los valores de hello y mostrarlos aplicación Hello, pero no debe confiar en ellas para cualquier autorización o los límites de seguridad.  Para obtener más información sobre id_tokens vea hello [v2.0 referencia del token de punto de conexión](active-directory-v2-tokens.md). |

#### Respuesta de error
Las respuestas de error tendrán un aspecto similar al siguiente:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen y puede ser usado tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudar a un desarrollador para identificar la causa de Hola de un error de autenticación. |
| error_codes |Una lista de los códigos de error específicos de STS que pueden ayudar en los diagnósticos. |
| timestamp |hora de Hello en que se produjo el error de Hola. |
| trace_id |Un identificador único para la solicitud de Hola que puede ayudar a diagnósticos. |
| correlation_id |Un identificador único para la solicitud de Hola que puede ayudar a diagnósticos en componentes. |

#### Códigos de error correspondientes a errores de puntos de conexión de token
| Código de error | Description | Acción del cliente |
| --- | --- | --- |
| invalid_request |Error de protocolo, como un parámetro obligatorio que falta. |Corrija y vuelva a enviar solicitud Hola |
| invalid_grant |código de autorización de Hello no es válido o ha expirado. |Intente una nueva toohello solicitud `/authorize` extremo |
| unauthorized_client |Hello cliente autenticado no está autorizado toouse esta autorización el tipo de concesión. |Esto suele ocurrir cuando la aplicación de cliente de hello no está registrado en Azure AD o no se agrega el inquilino de Azure AD del usuario toohello. aplicación Hello puede solicitar a usuario Hola con instrucciones para instalar la aplicación hello y agregar tooAzure AD. |
| invalid_client |Se produjo un error de autenticación de cliente. |las credenciales del cliente Hello no son válidas. toofix, Administrador de la aplicación hello actualiza las credenciales de Hola. |
| unsupported_grant_type |servidor de autorización de Hello no es compatible con el tipo de concesión de autorización de Hola. |Tipo de solicitud de Hola de concesión de Hola de cambio. Este tipo de error solo debe producirse durante el desarrollo y detectarse en las pruebas iniciales. |
| invalid_resource |recurso de destino de Hello no es válido porque no existe, Azure AD no la encuentra o no está configurado correctamente. |Esto indica recursos hello, si existe, no se configuró en el inquilino de Hola. aplicación Hello puede solicitar a usuario Hola con instrucciones para instalar la aplicación hello y agregar tooAzure AD. |
| interaction_required |solicitud de Hello requiere la interacción del usuario. Por ejemplo, hay que realizar un paso de autenticación más. |Vuelva a intentar la solicitud de hello con hello mismo recurso. |
| temporarily_unavailable |servidor de Hello está temporalmente solicitud de hello toohandle demasiado ocupado. |Vuelva a intentar la solicitud de saludo. aplicación de cliente de Hello puede explicar toohello usuario que su respuesta se retrasa debido a una condición temporal. |

## Usar el token de acceso de Hola
Ahora que ha adquirido correctamente una `access_token`, puede usar el token de hello en solicitudes tooWeb API mediante la inclusión en hello `Authorization` encabezado:

> [!TIP]
> Ejecute esta solicitud en Postman (Reemplace hello `Authorization` encabezado primera) [ ![ejecutar en Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## Hola token de acceso de actualización
Access_tokens tienen una duración breve, y debe actualizar después de que expiren toocontinue acceso a los recursos.  Puede hacerlo mediante el envío de otra `POST` solicitar toohello `/token` punto de conexión, este tiempo proporcionan hello `refresh_token` en lugar de Hola `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> Pruebe a ejecutar esta solicitud en Postman (No olvide hello tooreplace `refresh_token`) [ ![ejecutar en Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parámetro |  | Description |
| --- | --- | --- |
| tenant |requerido |Hola `{tenant}` valor de ruta de acceso de saludo de solicitud de hello puede ser usado toocontrol que puede iniciar sesión en la aplicación hello.  Hola valores permitidos son `common`, `organizations`, `consumers`y los identificadores de inquilinos.  Para obtener más información, consulte los [conceptos básicos sobre el protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |requerido |Hola Id. de aplicación ese portal de registro de hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) asignado a la aplicación. |
| grant_type |requerido |Debe ser `refresh_token` para este segmento del flujo de código de autorización de Hola. |
| ámbito |requerido |Una lista de ámbitos separada por espacios.  ámbitos de Hello solicitaron en esta bifurcación de la debe ser equivalente tooor un subconjunto de ámbitos de hello solicitado en hello original authorization_code bifurcación de la solicitud.  Si ámbitos Hola especificados en esta solicitud abarcan varios servidores de recursos, el punto de conexión de hello v2.0 devolverá un token para el recurso de hello especificada en el ámbito primera Hola.  Para obtener una explicación más detallada de ámbitos, consulte demasiado[permisos, ámbitos y consentimiento](active-directory-v2-scopes.md). |
| refresh_token |requerido |Hola refresh_token que adquirió en la bifurcación de la segunda Hola de flujo de Hola. |
| redirect_uri |requerido |Hola el mismo valor de redirect_uri que se usa tooacquire hello authorization_code. |
| client_secret |necesario para las aplicaciones web |secreto de aplicación Hola que creó en el portal de registro de aplicación de hello para la aplicación.  No debería utilizarse en una aplicación nativa, porque los client_secrets no se pueden almacenar de forma confiable en los dispositivos.  Es necesario para las aplicaciones web y las API, que tienen Hola capacidad toostore hello client_secret de forma segura en el lado del servidor de hello web. |

#### Respuesta correcta
Una respuesta de token correcta tendrá un aspecto similar al siguiente:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parámetro | Description |
| --- | --- |
| access_token |símbolo (token) de acceso solicitado Hola. aplicación Hello puede usar este toohello tooauthenticate token protegida recursos, como una API web. |
| token_type |Indica el valor de tipo de token de Hola. solo el tipo que admite Azure AD Hello es portador |
| expires_in |¿Durante cuánto tiempo el token de acceso de hello es válida (en segundos). |
| ámbito |es válido para los ámbitos de Hola Hola access_token. |
| refresh_token |Un nuevo token de actualización de OAuth 2.0. Debe reemplazar la actualización anterior de hello token con esta tooensure de token obtenidos recientemente la actualización de los tokens de actualización siguen siendo válidas mientras sea posible. |
| ID_token |Un token web JSON (JWT) sin firmar. Hola aplicación can base64Url descodificar segmentos Hola de esta información de token toorequest acerca del usuario de hello inscrita en. puede almacenar en memoria caché los valores de hello y mostrarlos aplicación Hello, pero no debe confiar en ellas para cualquier autorización o los límites de seguridad.  Para obtener más información sobre id_tokens vea hello [v2.0 referencia del token de punto de conexión](active-directory-v2-tokens.md). |

#### Respuesta de error
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen y puede ser usado tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudar a un desarrollador para identificar la causa de Hola de un error de autenticación. |
| error_codes |Una lista de los códigos de error específicos de STS que pueden ayudar en los diagnósticos. |
| timestamp |hora de Hello en que se produjo el error de Hola. |
| trace_id |Un identificador único para la solicitud de Hola que puede ayudar a diagnósticos. |
| correlation_id |Un identificador único para la solicitud de Hola que puede ayudar a diagnósticos en componentes. |

Para obtener una descripción de los códigos de error de Hola y Hola acción de cliente recomendada, consulte [códigos de Error para errores de extremo de token](#error-codes-for-token-endpoint-errors).

