---
title: "aplicaciones de una página de aaaSecure mediante flujo implícito de hello Azure AD v2.0 | Documentos de Microsoft"
description: "Creación de aplicaciones web con implementación de v2.0 de Azure AD de flujo implícitos de Hola para aplicaciones de la misma página."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# V2.0 protocolos - SPAs mediante flujo implícito Hola
Con el punto de conexión de hello v2.0, puede iniciar sesión a los usuarios en sus aplicaciones de página única con cuentas personales y de trabajo o educativa de Microsoft.  Página única y otras aplicaciones de JavaScript que se ejecutan principalmente en una cara de explorador interesantes algunos desafíos cuando se incluye tooauthentication:

* características de seguridad de Hola de estas aplicaciones son significativamente diferentes de aplicaciones web de servidor tradicional basado.
* Muchos proveedores de identidades y servidores de autorización no admiten solicitudes CORS.
* Página completa explorador redirecciones fuera de la aplicación hello se convierten en toohello especialmente invasiva experiencia del usuario.

Para estas aplicaciones (pensar: AngularJS, Ember.js, React.js, etcetera), Azure AD admite el flujo de concesión implícita OAuth 2.0 Hola.  flujo implícito Hola se describe en hello [especificación de OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.2).  La principal ventaja es que permite tokens de tooget aplicación Hola de Azure AD sin tener que realizar un intercambio de credenciales de servidor back-end.  Esto permite toosign de aplicación hello en usuario hello, mantener la sesión y obtener tokens tooother web API todo dentro de código de JavaScript de cliente de Hola.  Hay unos tootake de consideraciones de seguridad importantes en cuenta cuando se usa específicamente alrededor de flujo implícitos de hello - [cliente](http://tools.ietf.org/html/rfc6749#section-10.3) y [suplantación de usuario](http://tools.ietf.org/html/rfc6749#section-10.3).

Si desea flujo implícito de toouse hello y aplicación de Azure AD tooadd autenticación tooyour JavaScript, se recomienda utilizar nuestra biblioteca de JavaScript de código abierto, [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js).  Hay muy pocos tutoriales de AngularJS [aquí](active-directory-appmodel-v2-overview.md#getting-started) toohelp empezar a trabajar.  

Sin embargo, si prefiere no toouse una biblioteca en los mensajes de protocolo de aplicación y envío de página única usted mismo, siga Hola general pasos.

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.  toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

## Diagrama de protocolo
Hello todo inicio de sesión implícito en el flujo es algo parecido a esto, cada uno de los pasos de Hola se describen en detalle a continuación.

![Calles OpenId Connect](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## Enviar solicitud de inicio de sesión de Hola
inicio de sesión de tooinitially hello usuario en la aplicación, puede enviar un [OpenID Connect](active-directory-v2-protocols-oidc.md) solicitud de autorización y obtener un `id_token` desde el punto de conexión de hello v2.0:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> Haga clic en vínculo hello tooexecute esta solicitud. Después de iniciar sesión, el explorador se debe redirigir demasiado`https://localhost/myapp/` con un `id_token` en la barra de direcciones de Hola.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Parámetro |  | Description |
| --- | --- | --- |
| tenant |requerido |Hola `{tenant}` valor de ruta de acceso de saludo de solicitud de hello puede ser usado toocontrol que puede iniciar sesión en la aplicación hello.  Hola valores permitidos son `common`, `organizations`, `consumers`y los identificadores de inquilinos.  Para obtener más información, consulte los [conceptos básicos sobre el protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |requerido |Hola Id. de aplicación ese portal de registro de hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) asignado a la aplicación. |
| response_type |requerido |Debe incluir `id_token` para el inicio de sesión en OpenID Connect.  También puede incluir hello response_type `token`. Usar `token` aquí le permitirá la tooreceive de aplicación un token de acceso inmediatamente Hola extremo authorize sin necesidad de toomake autorizar a un segundo toohello solicitud extremo.  Si usas hello `token` response_type, hello `scope` parámetro debe contener un ámbito que indica qué token de recurso tooissue Hola para. |
| redirect_uri |recomendado |Hola redirect_uri de la aplicación, donde las respuestas de autenticación pueden ser enviadas y recibidas por la aplicación.  Debe coincidir exactamente con uno de redirect_uris Hola que registró en el portal de hello, salvo que debe ser la dirección url codificada. |
| ámbito |requerido |Una lista de ámbitos separada por espacios.  Para OpenID Connect, debe incluir el ámbito de hello `openid`, que traduce toohello "Iniciar sesión en" permiso en la IU de consentimiento del saludo.  Opcionalmente, puede que también desee hello tooinclude `email` o `profile` [ámbitos](active-directory-v2-scopes.md) para obtener acceso a datos de usuario de tooadditional.  También puede incluir otros ámbitos en esta solicitud para solicitar el consentimiento toovarious recursos. |
| response_mode |recomendado |Especifica el método de Hola que debe ser usado toosend Hola resultante token tooyour back-app.  Debe ser `fragment` para flujo implícito Hola. |
| state |recomendado |Un valor incluido en la solicitud de Hola que también se devolverán en respuesta de token de Hola.  Puede ser una cadena de cualquier contenido que desee.  Normalmente se usa un valor único generado de forma aleatoria para [evitar los ataques de falsificación de solicitudes entre sitios](http://tools.ietf.org/html/rfc6749#section-10.12).  estado de Hello también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido en solicitud de autenticación de hello, como página de Hola o que estaban en la vista. |
| valor de seguridad |requerido |Un valor incluido en solicitud de hello, generado por la aplicación hello, que se incluirán en hello id_token resultante como una notificación.  aplicación Hello, a continuación, puede comprobar que los ataques de reproducción de tokens de toomitigate este valor.  valor de Hello suele ser una cadena aleatoria única que puede ser usado tooidentify Hola origen de solicitud de Hola. |
| símbolo del sistema |opcional |Indica el tipo de hello de interacción del usuario que es necesario.  Hola solo en este momento los valores válidos son 'login', 'none' y 'da su consentimiento'.  `prompt=login`se fuerza Hola a tooenter usuario sus credenciales en esa solicitud, niega el inicio de sesión único en.  `prompt=none`es Hola opuesto: se asegurará de que el usuario hello no se presenta con cualquier mensaje interactivo ningún tipo..  Si no se puede completar de solicitud Hola a través de inicio de sesión único en modo silencioso, el punto de conexión de hello v2.0 devolverá un error.  `prompt=consent`acepta Hola desencadenador OAuth diálogo después de los signos de usuario de hello, pidiendo permisos toohello aplicación de hello usuario toogrant. |
| login_hint |opcional |Puede ser campo de dirección de nombre de usuario y de correo electrónico usado toopre-relleno Hola del programa Hola a iniciar sesión página de usuario de hello, si conoce su nombre de usuario antes de tiempo.  A menudo las aplicaciones utilizarán este parámetro durante la reautenticación, tener extraído ya el nombre de usuario de Hola desde un inicio de sesión anterior con hello `preferred_username` de notificación. |
| domain_hint |opcional |Puede ser `consumers` o `organizations`.  Si se incluye, se omitirán proceso de detección basada en correo electrónico de Hola que el usuario pasa por de inicio de sesión de hello v2.0 en la página, a la izquierda tooa ligeramente más una mejor experiencia del usuario.  A menudo las aplicaciones utilizarán este parámetro durante la reautenticación, extrayendo hello `tid` notificación de hello id_token.  Si hello `tid` es el valor de notificación `9188040d-6c67-4c5b-b112-36a304b66dad`, debe usar `domain_hint=consumers`.  De lo contrario, use `domain_hint=organizations`. |

En este punto, el usuario de hello será más frecuentes tooenter sus credenciales y autenticación de hello completa.  Hello v2.0 extremo también garantizarán ese usuario Hola ha dado su consentimiento permisos de toohello indicados en hello `scope` parámetro de consulta.  Si hello no haya consentido tooany de estos permisos, le preguntará Hola usuario tooconsent toohello requerido permisos.  Aquí puede encontrar información detallada sobre los [permisos, el consentimiento y las aplicaciones multiempresa](active-directory-v2-scopes.md).

Una vez que el usuario de Hola se autentica y concede el consentimiento, el punto de conexión de hello v2.0 devolverá una aplicación de tooyour de respuesta en hello indicado `redirect_uri`, mediante el método hello especificado en hello `response_mode` parámetro.

#### Respuesta correcta
Una respuesta correcta mediante `response_mode=fragment` y `response_type=id_token+token` siguiente hello, saltos de línea por legibilidad aspecto:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| Parámetro | Description |
| --- | --- |
| access_token |Incluido si `response_type` incluye `token`. token de acceso de Hola Hola de aplicación solicitado, en este caso para Hola Microsoft Graph.  token de acceso de Hello no se debe descodificar o inspeccionar en caso contrario, se puede tratar como una cadena opaca. |
| token_type |Incluido si `response_type` incluye `token`.  Siempre será `Bearer`. |
| expires_in |Incluido si `response_type` incluye `token`.  Indica el número de Hola de token de hello es válido, para almacenar en caché con fines de segundos. |
| ámbito |Incluido si `response_type` incluye `token`.  Indica los ámbitos de Hola para qué hello access_token será válido. |
| ID_token |Hola id_token que Hola aplicación solicitada. Puede usar la identidad del usuario de hello id_token tooverify hello y empezar una sesión de usuario de Hola.  Obtener más detalles sobre id_tokens y su contenido se incluye en hello [v2.0 referencia del token de punto de conexión](active-directory-v2-tokens.md). |
| state |Si un parámetro de estado se incluye en la solicitud de hello, Hola debe aparecer el mismo valor en respuesta de Hola. aplicación Hello debe comprobar que los valores de estado de hello en hello solicitud y respuesta son idénticos. |

#### Respuesta de error
Las respuestas de error también se pueden enviar toohello `redirect_uri` por lo que puede controlar aplicación hello correctamente:

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen y puede ser usado tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudar a un desarrollador para identificar la causa de Hola de un error de autenticación. |

## Validar hello id_token
Simplemente recibe un id_token no es suficiente tooauthenticate Hola usuario debe validar la firma del id_token hello y comprobar notificaciones de Hola de token de hello según los requisitos de la aplicación.  Hola v2.0 extremo utiliza [Tokens de Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) y públicos tokens toosign de criptografía de clave y compruebe que son válidos.

Puede elegir hello toovalidate `id_token` en el código de cliente, pero una práctica común es hello toosend `id_token` tooa servidor de back-end y realizar la validación de hello no existe.  Una vez que haya validado firma Hola de hello id_token, hay algunas notificaciones que será necesario tooverify.  Vea hello [referencia del token v2.0](active-directory-v2-tokens.md) para obtener más información, incluidos los [validar Tokens](active-directory-v2-tokens.md#validating-tokens) y [importante información sobre la firma de sustitución de clave](active-directory-v2-tokens.md#validating-tokens).  Hay al menos una disponible para la mayoría de los lenguajes y las plataformas.
<!--TODO: Improve hello information on this-->

También puede llamar toovalidate demandas adicionales según el escenario.  Algunas validaciones comunes incluyen:

* Garantizar Hola usuario u organización ha registrado para la aplicación hello.
* Usuario de hello asegurar que tiene autorización o los privilegios adecuados
* Asegurarse de que se haya producido un determinado nivel de autenticación, como la autenticación multifactor.

Para obtener más información sobre notificaciones de hello en un id_token, vea hello [v2.0 referencia del token de punto de conexión](active-directory-v2-tokens.md).

Una vez que haya validado completamente id_token hello, puede empezar una sesión de usuario de Hola y utilizar notificaciones de hello en hello id_token tooobtain saber usuario hello en la aplicación.  Esta información puede utilizarse para su visualización, registros, autorizaciones, etc.

## Obtención de tokens de acceso
Ahora que ha firmado usuario hello en su aplicación de una página, puede obtener tokens de acceso web que realiza la llamada API protegidas por Azure AD, como hello [Microsoft Graph](https://graph.microsoft.io).  Incluso si ya recibió un token con hello `token` response_type, se pueden utilizar este método tooacquire tokens tooadditional los recursos sin tener tooredirect Hola usuario toosign nuevo.

En el flujo OpenID Connect y OAuth normal hello, para hacerlo realizando un v2.0 de toohello solicitud `/token` punto de conexión.  Sin embargo, el punto de conexión de hello v2.0 no compatibilidad con CORS las solicitudes, para realizar AJAX llamadas tooget y tokens de actualización está fuera del pregunta Hola.  En su lugar, puede usar flujo implícito de hello en un iframe oculto tooget nuevos tokens para otras API web: 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> Intente copiar & Pegar Hola por debajo de la solicitud en una pestaña del explorador. (No olvide hello tooreplace `domain_hint` hello y `login_hint` valores con hello corrigen valores para el usuario)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| Parámetro |  | Description |
| --- | --- | --- |
| tenant |requerido |Hola `{tenant}` valor de ruta de acceso de saludo de solicitud de hello puede ser usado toocontrol que puede iniciar sesión en la aplicación hello.  Hola valores permitidos son `common`, `organizations`, `consumers`y los identificadores de inquilinos.  Para obtener más información, consulte los [conceptos básicos sobre el protocolo](active-directory-v2-protocols.md#endpoints). |
| client_id |requerido |Hola Id. de aplicación ese portal de registro de hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) asignado a la aplicación. |
| response_type |requerido |Debe incluir `id_token` para el inicio de sesión en OpenID Connect.  También puede incluir otros elementos response_type como `code`. |
| redirect_uri |recomendado |Hola redirect_uri de la aplicación, donde las respuestas de autenticación pueden ser enviadas y recibidas por la aplicación.  Debe coincidir exactamente con uno de redirect_uris Hola que registró en el portal de hello, salvo que debe ser la dirección url codificada. |
| ámbito |requerido |Una lista de ámbitos separada por espacios.  Para obtener los tokens, incluir todos los [ámbitos](active-directory-v2-scopes.md) requieren para el recurso de Hola de interés. |
| response_mode |recomendado |Especifica el método de Hola que debe ser usado toosend Hola resultante token tooyour back-app.  Puede ser `query`, `form_post` o `fragment`. |
| state |recomendado |Un valor incluido en la solicitud de Hola que también se devolverán en respuesta de token de Hola.  Puede ser una cadena de cualquier contenido que desee.  Se utiliza normalmente un valor único generado de forma aleatoria para evitar los ataques de falsificación de solicitudes entre sitios.  estado de Hello también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido en solicitud de autenticación de hello, como página de Hola o que estaban en la vista. |
| valor de seguridad |requerido |Un valor incluido en solicitud de hello, generado por la aplicación hello, que se incluirán en hello id_token resultante como una notificación.  aplicación Hello, a continuación, puede comprobar que los ataques de reproducción de tokens de toomitigate este valor.  valor de Hello suele ser una cadena aleatoria única que puede ser usado tooidentify Hola origen de solicitud de Hola. |
| símbolo del sistema |requerido |Para actualizar y obtener tokens en un iframe oculto, debe usar `prompt=none` tooensure que Hola iframe no responder al inicio de sesión de hello v2.0 en la página y se devuelve inmediatamente. |
| login_hint |requerido |Para actualizar y obtener tokens en un iframe oculto, debe incluir Hola nombre del usuario con hello en esta sugerencia en orden toodistinguish entre varias sesiones de usuario de hello puede tener en un momento dado en el tiempo. Puede extraer el nombre de usuario de Hola desde un inicio de sesión anterior con hello `preferred_username` de notificación. |
| domain_hint |requerido |Puede ser `consumers` o `organizations`.  Para actualizar y obtener tokens en un iframe oculto, debe incluir domain_hint hello en solicitud de Hola.  Debe extraer hello `tid` qué toouse valor de notificación de hello id_token de un toodetermine de inicio de sesión anterior.  Si hello `tid` es el valor de notificación `9188040d-6c67-4c5b-b112-36a304b66dad`, debe usar `domain_hint=consumers`.  De lo contrario, use `domain_hint=organizations`. |

Gracias toohello `prompt=none` parámetro, esta solicitud ya sea correctamente o produce un error inmediato y devolver la aplicación de tooyour.  Se enviará a una respuesta correcta aplicación tooyour en hello indicado `redirect_uri`, mediante el método hello especificado en hello `response_mode` parámetro.

#### Respuesta correcta
Una respuesta correcta al usar `response_mode=fragment` tiene el siguiente aspecto:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| . | Description |
| --- | --- |
| access_token |Hola símbolo (token) de esa aplicación hello solicitada. |
| token_type |Siempre será `Bearer`. |
| state |Si un parámetro de estado se incluye en la solicitud de hello, Hola debe aparecer el mismo valor en respuesta de Hola. aplicación Hello debe comprobar que los valores de estado de hello en hello solicitud y respuesta son idénticos. |
| expires_in |¿Durante cuánto tiempo el token de acceso de hello es válida (en segundos). |
| ámbito |ámbitos de Hola Hola token de acceso es válida para. |

#### Respuesta de error
Las respuestas de error también se pueden enviar toohello `redirect_uri` por lo que la aplicación hello puede controlarlos adecuadamente.  En caso de hello de `prompt=none`, será un error inesperado:

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parámetro | Description |
| --- | --- |
| error |Una cadena de código de error que puede ser utilizados tooclassify tipos de errores que se producen y puede ser usado tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudar a un desarrollador para identificar la causa de Hola de un error de autenticación. |

Si recibe este error en la solicitud de iframe de hello, Hola usuario debe iniciar interactivamente en nuevo tooretrieve un nuevo token.  Puede elegir toohandle este caso en la forma que tenga sentido para la aplicación.

## Actualización de tokens
Ambos `id_token`s y `access_token`s expirará tras un breve período de tiempo, por lo que la aplicación debe estar preparada toorefresh estos tokens periódicamente.  toorefresh escriba de símbolo (token), puede realizar Hola misma solicitud iframe oculto desde encima utilizar hello `prompt=none` parámetro comportamiento toocontrol de Azure AD.  Si desea que tooreceive un nuevo `id_token`, ser seguro toouse `response_type=id_token` y `scope=openid`, así como un `nonce` parámetro.

## Envío de una solicitud de cierre de sesión
Hola OpenIdConnect `end_session_endpoint` permite que su aplicación toosend un tooend de punto de conexión de solicitud toohello v2.0 sesión y borrar cookies de un usuario establecen el punto de conexión de hello v2.0.  toofully inicie sesión un usuario de una aplicación web, la aplicación debe finalizar su propia sesión de usuario de hello (normalmente al borrar una caché de tokens o quitar las cookies) y, a continuación, redirigir el Explorador de Hola a:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| Parámetro |  | Description |
| --- | --- | --- |
| tenant |requerido |Hola `{tenant}` valor de ruta de acceso de saludo de solicitud de hello puede ser usado toocontrol que puede iniciar sesión en la aplicación hello.  Hola valores permitidos son `common`, `organizations`, `consumers`y los identificadores de inquilinos.  Para obtener más información, consulte los [conceptos básicos sobre el protocolo](active-directory-v2-protocols.md#endpoints). |
| post_logout_redirect_uri | recomendado | dirección URL de Hola que Hola usuario se debe devolver tooafter cierre de sesión se completa. Este valor debe coincidir con uno de redirección de hello que URI registrado para la aplicación hello. Si no se incluye usuario Hola se mostrará un mensaje genérico por el punto de conexión de hello v2.0. |
