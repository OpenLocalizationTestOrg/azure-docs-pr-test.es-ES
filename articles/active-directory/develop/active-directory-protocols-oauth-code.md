---
title: "Hola aaaUnderstand flujo de código de autorización de OAuth 2.0 en Azure AD | Documentos de Microsoft"
description: "Este artículo describe cómo acceder a toouse HTTP mensajes tooauthorize tooweb aplicaciones y las API web en el inquilino con Azure Active Directory y OAuth 2.0."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: de3412cb-5fde-4eca-903a-4e9c74db68f2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4a6fe67d786a5fcb87d1059c2e94ba0c88d26cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Autorizar acceso tooweb aplicaciones mediante OAuth 2.0 y Azure Active Directory
Azure Active Directory (Azure AD) usa OAuth 2.0 tooenable tooauthorize acceso tooweb aplicaciones y las API web de inquilino de Azure AD. Esta guía es independiente del lenguaje y se describe cómo toosend y recibir mensajes HTTP sin usar cualquiera de nuestras bibliotecas de código abierto.

Hola flujo de código de autorización de OAuth 2.0 se describe en [sección 4.1 de especificación de hello OAuth 2.0](https://tools.ietf.org/html/rfc6749#section-4.1). Es tooperform usa autenticación y autorización en la mayoría de los tipos de aplicación, incluidas las aplicaciones web y aplicaciones de forma nativa instaladas.

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## Flujo de autorización de OAuth 2.0
En un nivel alto, flujo de autorización completo de Hola para una aplicación un poco este aspecto:

![Flujo de código de autenticación de OAuth](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## Solicitud de un código de autorización
flujo de código de autorización de Hello comienza con cliente hello dirigir Hola usuario toohello `/authorize` punto de conexión. En esta solicitud, cliente hello indica permisos de Hola que necesita tooacquire de usuario de Hola. Puede obtener los puntos de conexión de hello OAuth 2.0 desde la página de su aplicación de Portal de Azure clásico, en hello **ver extremos** botón en el espacio de hello inferior.

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https%3A%2F%2Fservice.contoso.com%2F
&state=12345
```

| Parámetro |  | Description |
| --- | --- | --- |
| tenant |requerido |Hola `{tenant}` valor de ruta de acceso de saludo de solicitud de hello puede ser usado toocontrol que puede iniciar sesión en la aplicación hello.  Hola valores permitidos son identificadores de inquilino, por ejemplo, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` o `contoso.onmicrosoft.com` o `common` para los tokens de independientes del inquilino |
| client_id |requerido |Hola Id. de aplicación asignado tooyour aplicación cuando se registra con Azure AD. Puede encontrar esto en hello Portal de Azure. Haga clic en **Active Directory**, haga clic en el directorio de hello, elija aplicación hello y haga clic en **configurar** |
| response_type |requerido |Debe incluir `code` para el flujo de código de autorización de Hola. |
| redirect_uri |recomendado |Hola redirect_uri de la aplicación, donde las respuestas de autenticación pueden ser enviadas y recibidas por la aplicación.  Debe coincidir exactamente con uno de redirect_uris Hola que registró en el portal de hello, salvo que debe ser la dirección url codificada.  Para las aplicaciones nativas & móviles, debe usar valor predeterminado de Hola de `urn:ietf:wg:oauth:2.0:oob`. |
| response_mode |recomendado |Especifica el método de Hola que debe ser usado toosend Hola resultante token tooyour back-app.  Puede ser `query` o `form_post`. |
| state |recomendado |Un valor incluido en la solicitud de Hola que también se devuelve como respuesta de token de Hola. Normalmente se usa un valor único generado de forma aleatoria para [evitar los ataques de falsificación de solicitudes entre sitios](http://tools.ietf.org/html/rfc6749#section-10.12).  estado de Hello también es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido en solicitud de autenticación de hello, como página de Hola o que estaban en la vista. |
| resource |opcional |Hola URI de Id. de aplicación de hello web API (recurso seguro). Hola toofind URI de Id. de aplicación de hello web API, Hola Portal de Azure, haga clic en **Active Directory**, haga clic en el directorio de hello, haga clic en la aplicación hello y, a continuación, haga clic en **configurar**. |
| símbolo del sistema |opcional |Indicar el tipo de hello de interacción del usuario que es necesario.<p> Los valores válidos son: <p> *inicio de sesión*: usuario Hola debe ser tooreauthenticate solicitada. <p> *consentimiento*: se ha concedido consentimiento del usuario, pero es necesario toobe actualizado. usuario de Hello debe ser tooconsent solicitada. <p> *admin_consent*: un administrador debe ser tooconsent solicitada en nombre de todos los usuarios de su organización |
| login_hint |opcional |Puede ser el campo de dirección de nombre de usuario y de correo electrónico de relleno de toopre usado Hola de página de inicio de sesión de hello para el usuario de hello, si conoce su nombre de usuario antes de tiempo.  Aplicaciones a menudo usan este parámetro durante la reautenticación, tener extraído ya el nombre de usuario de Hola desde un inicio de sesión anterior con hello `preferred_username` de notificación. |
| domain_hint |opcional |Proporciona una sugerencia sobre el inquilino de Hola o un dominio que Hola usuario debe usar toosign en. valor de Hola de hello domain_hint es un dominio registrado para el inquilino de Hola. Si inquilino hello es directorio local de tooan federado, AAD redirige toohello servidor de federación de inquilino especificado. |

> [!NOTE]
> Si Hola usuario forma parte de una organización, un administrador de organización de hello puede dar su consentimiento o rechazar en nombre de usuario de Hola o permitir Hola usuario tooconsent. se concede al usuario de Hola Hola opción tooconsent sólo cuando Hola administrador lo permite.
>
>

En este punto, el usuario de Hola se solicita tooenter sus credenciales y el consentimiento toohello permisos indican en hello `scope` parámetro de consulta. Una vez que el usuario de Hola se autentica y concede el consentimiento, Azure AD envía una aplicación de tooyour de respuesta en hello `redirect_uri` dirección especificada en la solicitud.

### Respuesta correcta
Una respuesta correcta podría tener el siguiente aspecto:

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| Parámetro | Descripción |
| --- | --- |
| admin_consent |valor de Hello es True si un administrador aceptado tooa solicitud de consentimiento. |
| código |código de autorización de Hola Hola aplicación solicitado. aplicación Hello sirve toorequest de código de autorización de hello un token de acceso para el recurso de destino de Hola. |
| session_state |Un valor único que identifica la sesión del usuario actual Hola. Este valor es un GUID, pero se debe tratar como un valor opaco que se pasa sin analizar. |
| state |Si un parámetro de estado se incluye en la solicitud de hello, Hola debe aparecer el mismo valor en respuesta de Hola. Es una buena práctica para hello tooverify de aplicación que los valores de estado de hello en hello solicitud y respuesta son idénticos antes de usar la respuesta de Hola. Esto ayuda a toodetect [los ataques de falsificación de solicitud entre sitios (CSRF)](https://tools.ietf.org/html/rfc6749#section-10.12) con cliente de Hola. |

### Respuesta de error
Las respuestas de error también se pueden enviar toohello `redirect_uri` para que la aplicación hello puede controlarlos adecuadamente.

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parámetro | Description |
| --- | --- |
| error |Un valor de código de error definido en la sección 5.2 de hello [marco de autorización de OAuth 2.0](http://tools.ietf.org/html/rfc6749). tabla de Hello siguiente describe los códigos de error de Hola que devuelve Azure AD. |
| error_description |Una descripción más detallada del error de Hola. Este mensaje no está pensado toobe el usuario final. |
| state |valor de estado de Hello es un valor no reutilizado generado aleatoriamente que se envía en solicitud de Hola y se devuelve en los ataques de falsificación (CSRF) Hola respuesta tooprevent solicitud entre sitios. |

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

## Usar toorequest de código de autorización de hello un token de acceso
Ahora que ha adquirido un código de autorización y tener concedido permiso al usuario de hello, pueden canjear código de hello para un recurso de token toohello deseado de acceso, mediante el envío de un toohello de solicitud POST `/token` punto de conexión:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code
&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA
&redirect_uri=https%3A%2F%2Flocalhost%2Fmyapp%2F
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=p@ssw0rd

//NOTE: client_secret only required for web apps
```

| Parámetro |  | Description |
| --- | --- | --- |
| tenant |requerido |Hola `{tenant}` valor de ruta de acceso de saludo de solicitud de hello puede ser usado toocontrol que puede iniciar sesión en la aplicación hello.  Hola valores permitidos son identificadores de inquilino, por ejemplo, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` o `contoso.onmicrosoft.com` o `common` para los tokens de independientes del inquilino |
| client_id |requerido |Hola Id. de aplicación asignado tooyour aplicación cuando se registra con Azure AD. Puede encontrar esto en hello Portal clásico de Azure. Haga clic en **Active Directory**, haga clic en el directorio de hello, elija aplicación hello y haga clic en **configurar** |
| grant_type |requerido |Debe ser `authorization_code` para el flujo de código de autorización de Hola. |
| código |requerido |Hola `authorization_code` que adquirió en la sección anterior de Hola |
| redirect_uri |requerido |Hola mismo `redirect_uri` valor de hello tooacquire usado `authorization_code`. |
| client_secret |necesario para las aplicaciones web |secreto de aplicación Hola que creó en el portal de registro de aplicación de hello para la aplicación.  No debería utilizarse en una aplicación nativa, porque los client_secrets no se pueden almacenar de forma confiable en los dispositivos.  Se requiere para las aplicaciones web y las API, que tienen Hola de toostore de capacidad de hello web `client_secret` forma segura en el lado del servidor de Hola. |
| resource |Requerido si se especifica en la solicitud de código de autorización; en caso contrario, es opcional. |Hola URI de Id. de aplicación de hello web API (recurso seguro). |

Hola toofind App ID URI, Hola Portal de administración de Azure, haga clic en **Active Directory**, haga clic en el directorio de hello, haga clic en la aplicación hello y, a continuación, haga clic en **configurar**.

### Respuesta correcta
Azure AD devuelve un token de acceso tras una respuesta correcta. llamadas de red toominimize de aplicación de cliente de Hola y su latencia asociada, aplicación de cliente de hello debe almacenar en caché los tokens de acceso para la duración del token Hola descrito en hello respuesta de OAuth 2.0. duración del token toodetermine hello, usar ambos hello `expires_in` o `expires_on` valores de parámetro.

Si un recurso de la API web devuelve un `invalid_token` código de error, esto podría indicar que determinó recursos Hola ese token Hola ha caducado. Si los tiempos de reloj de cliente y el recurso de hello son diferentes (conocido como "hora sesgo"), recurso de hello podría considerar Hola token toobe finalizó antes de token de Hola se borra de la memoria caché del cliente Hola. Si esto ocurre, borre el token Hola de caché de hello, incluso si está aún dentro de su duración calculada.

Una respuesta correcta podría tener el siguiente aspecto:

```
{
  "access_token": " eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| Parámetro | Description |
| --- | --- |
| access_token |símbolo (token) de acceso solicitado Hola. aplicación Hello puede usar este toohello tooauthenticate token protegida recursos, como una API web. |
| token_type |Indica el valor de tipo de token de Hola. Hola solo escriba que admite Azure AD es portador. Para más información sobre los tokens de portador, consulte [OAuth2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) |
| expires_in |¿Durante cuánto tiempo el token de acceso de hello es válida (en segundos). |
| expires_on |hora de Hello cuando expire el token de acceso de Hola. fecha de Hola se representa como número de Hola de segundos desde 1970-01-01T0:0:0Z UTC hasta el tiempo de expiración de Hola. Este valor es la duración de hello toodetermine uso de tokens almacenados en caché. |
| resource |Hola URI de Id. de aplicación de hello web API (recurso seguro). |
| ámbito |Permisos de suplantación toohello aplicación de cliente. permiso de Hello predeterminado es `user_impersonation`. propietario de Hola de hello protegida recursos puede registrar valores adicionales en Azure AD. |
| refresh_token |Un token de actualización de OAuth 2.0. aplicación Hello puede utilizar los tokens de acceso adicionales de este token tooacquire después de que expire el token de acceso actual de Hola.  Actualizar tokens son de larga duración y puede ser usado tooretain acceso tooresources durante largos períodos de tiempo. |
| ID_token |Un token web JSON (JWT) sin firmar. Hola aplicación can base64Url descodificar segmentos Hola de esta información de token toorequest acerca del usuario de hello inscrita en. puede almacenar en memoria caché los valores de hello y mostrarlos aplicación Hello, pero no debe confiar en ellas para cualquier autorización o los límites de seguridad. |

### Notificaciones de token JWT
token de JWT de Hello en el valor de Hola de hello `id_token` parámetro se puede descodificar en hello siguientes notificaciones:

```
{
 "typ": "JWT",
 "alg": "none"
}.
{
 "aud": "2d4d11a2-f814-46a7-890a-274a72a7309e",
 "iss": "https://sts.windows.net/7fe81447-da57-4385-becb-6de57f21477e/",
 "iat": 1388440863,
 "nbf": 1388440863,
 "exp": 1388444763,
 "ver": "1.0",
 "tid": "7fe81447-da57-4385-becb-6de57f21477e",
 "oid": "68389ae2-62fa-4b18-91fe-53dd109d74f5",
 "upn": "frank@contoso.com",
 "unique_name": "frank@contoso.com",
 "sub": "JWvYdCWPhhlpS1Zsf7yYUxShUwtUm5yzPmw_-jX3fHY",
 "family_name": "Miller",
 "given_name": "Frank"
}.
```

Para obtener más información sobre los tokens web JSON, vea hello [especificación de borrador JWT IETF](http://go.microsoft.com/fwlink/?LinkId=392344). Para obtener más información sobre los tipos de token de Hola y notificaciones, lea [admite tokens y los tipos de notificación](active-directory-token-and-claims.md)

Hola `id_token` parámetro incluye Hola siguientes tipos de notificación:

| Tipo de notificación | Descripción |
| --- | --- |
| aud |Audiencia del token de Hola. Cuando se emite a token de hello tooa aplicación de cliente, audiencia hello es hello `client_id` de cliente de Hola. |
| exp |Se trata de la fecha de expiración. hora de Hello cuando expire el token de Hola. Para toobe token Hola válido, Hola fecha y hora actual debe ser menor o igual toohello `exp` valor. hora de Hola se representa como número de Hola de segundos desde el 1 de enero de 1970 (1970-01-01T0:0:0Z) UTC hasta Hola tiempo Hola token haya sido emitido. |
| family_name |Se trata de los apellidos del usuario. aplicación Hello puede mostrar este valor. |
| given_name |Se trata del nombre del usuario. aplicación Hello puede mostrar este valor. |
| iat |Hora de emisión. hora de Hello cuando se emitió hello JWT. hora de Hola se representa como número de Hola de segundos desde el 1 de enero de 1970 (1970-01-01T0:0:0Z) UTC hasta Hola tiempo Hola token haya sido emitido. |
| iss |Identifica el emisor del token Hola |
| nbf |Significa que el token no se emite antes de la hora. hora de Hello cuando el token de Hola se hace efectiva. Para toobe token Hola válido, Hola fecha y hora actual debe ser toohello igual o mayor que Nbf valor. hora de Hola se representa como número de Hola de segundos desde el 1 de enero de 1970 (1970-01-01T0:0:0Z) UTC hasta Hola tiempo Hola token haya sido emitido. |
| oid |Identificador de objeto (ID) del objeto de usuario de hello en Azure AD. |
| sub |Se trata del identificador de asunto del token. Éste es un identificador persistente e inmutable para usuario Hola Hola token describe. Use este valor en la lógica de caché. |
| tid |Identificador (ID) del inquilino de hello Azure AD que emitió el token de Hola de inquilinos. |
| unique_name |Un identificador único para el puede ser mostrada toohello usuario. Por lo general, suele ser un nombre principal de usuario (UPN). |
| upn |Nombre principal de usuario del usuario de Hola. |
| ver |Se trata de la versión. versión de Hola de token JWT de hello, normalmente 1.0. |

### Respuesta de error
errores de extremo de emisión de tokens de Hello son códigos de error HTTP, porque las llamadas de cliente de Hola Hola extremo de emisión de tokens directamente. Además código de estado HTTP toohello, extremo de emisión de tokens de Azure AD de hello también devuelve un documento JSON con objetos que describen el error Hola.

Una respuesta de error de ejemplo podría tener este aspecto:

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: hello provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
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

#### Códigos de estado HTTP
Hello tabla siguiente enumeran los códigos de estado HTTP de Hola que Hola devuelve de extremo de emisión de tokens. En algunos casos, código de error de hello es la respuesta de hello toodescribe suficiente, pero si hay errores, debe hello tooparse que acompaña a JSON de documentos y examinar el código de error.

| Código HTTP | Descripción |
| --- | --- |
| 400 |Código HTTP predeterminado. Usar en la mayoría de los casos y suele ser debido a tooa de solicitud con formato incorrecto. Corrija y vuelva a enviar la solicitud de saludo. |
| 401 |Error de autenticación. Por ejemplo, solicitud de hello Falta parámetro de client_secret Hola. |
| 403 |Error de autorización. Por ejemplo, usuario hello no tiene el recurso de permiso tooaccess Hola. |
| 500 |Se ha producido un error interno en el servicio de Hola. Vuelva a intentar la solicitud de saludo. |

#### Códigos de error correspondientes a errores de puntos de conexión de token
| Código de error | Description | Acción del cliente |
| --- | --- | --- |
| invalid_request |Error de protocolo, como un parámetro obligatorio que falta. |Corrija y vuelva a enviar solicitud Hola |
| invalid_grant |código de autorización de Hello no es válido o ha expirado. |Intente una nueva toohello solicitud `/authorize` extremo |
| unauthorized_client |Hello cliente autenticado no está autorizado toouse esta autorización el tipo de concesión. |Esto suele ocurrir cuando la aplicación de cliente de hello no está registrado en Azure AD o no se agrega el inquilino de Azure AD del usuario toohello. aplicación Hello puede solicitar a usuario Hola con instrucciones para instalar la aplicación hello y agregar tooAzure AD. |
| invalid_client |Se produjo un error de autenticación de cliente. |las credenciales del cliente Hello no son válidas. toofix, Administrador de la aplicación hello actualiza las credenciales de Hola. |
| unsupported_grant_type |servidor de autorización de Hello no es compatible con el tipo de concesión de autorización de Hola. |Tipo de solicitud de Hola de concesión de Hola de cambio. Este tipo de error solo debe producirse durante el desarrollo y detectarse en las pruebas iniciales. |
| invalid_resource |recurso de destino de Hello no es válido porque no existe, Azure AD no la encuentra o no está configurado correctamente. |Esto indica recursos hello, si existe, no se configuró en el inquilino de Hola. aplicación Hello puede solicitar a usuario Hola con instrucciones para instalar la aplicación hello y agregar tooAzure AD. |
| interaction_required |solicitud de Hello requiere la interacción del usuario. Por ejemplo, hay que realizar un paso de autenticación más. | En lugar de una solicitud no interactivo, vuelva a intentarlo con una solicitud de autorización interactivo para hello mismo recurso. |
| temporarily_unavailable |servidor de Hello está temporalmente solicitud de hello toohandle demasiado ocupado. |Vuelva a intentar la solicitud de saludo. aplicación de cliente de Hello puede explicar toohello usuario que su respuesta se retrasa debido a tooa de condición temporal. |

## Usar Hola acceso tooaccess token Hola recurso
Ahora que ha adquirido correctamente una `access_token`, puede usar el token de hello en solicitudes tooWeb API, mediante la inclusión en hello `Authorization` encabezado. Hola [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt) especificación explica cómo protegen los recursos en tokens de portador de toouse en tooaccess de las solicitudes HTTP.

### Solicitud de ejemplo
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### Respuesta de error
Los recursos protegidos que implementan esta especificación emiten códigos de error HTTP. Si solicitud hello no incluye las credenciales de autenticación o falta respuesta del token, Hola de hello incluye un `WWW-Authenticate` encabezado. Cuando se produce un error en una solicitud, servidor de recursos de hello responde con código de estado HTTP de Hola y un código de error.

Hola aquí te mostramos un ejemplo de una respuesta de error cuando la solicitud de cliente hello no incluye el token de portador de hello:

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="hello access token is missing.",
```

#### Parámetros de error
| Parámetro | Descripción |
| --- | --- |
| authorization_uri |Hola URI (extremo físico) del servidor de autorización de Hola. Este valor también se utiliza como una búsqueda de clave tooget obtener más información sobre el servidor de Hola desde un punto de conexión de detección. <p><p> cliente de Hello debe validar ese Hola servidor de autorización es de confianza. Cuando Hola recurso está protegido por Azure AD, es suficiente tooverify que Hola URL comienza con https://login.microsoftonline.com u otro nombre de host que admita Azure AD. Los recursos específicos del inquilino siempre deben devolver un URI de autorización exclusivo del inquilino. |
| error |Un valor de código de error definido en la sección 5.2 de hello [marco de autorización de OAuth 2.0](http://tools.ietf.org/html/rfc6749). |
| error_description |Una descripción más detallada del error de Hola. Este mensaje no está pensado toobe el usuario final. |
| resource_id |Devuelve Hola identificador único del recurso de Hola. aplicación de cliente de Hello puede usar este identificador como valor de Hola de hello `resource` parámetro cuando se solicita un token para el recurso de Hola. <p><p> Es importante para Hola tooverify de aplicación de cliente de este valor, en caso contrario, un servicio malintencionado podría ser capaz de tooinduce una **elevación de privilegios** ataque <p><p> Hola estrategia recomendada para prevenir los ataques es tooverify que Hola `resource_id` coincidencias Hola base de web Hola URL de la API que está obteniendo acceso. Por ejemplo, si se tiene acceso https://service.contoso.com/data, Hola `resource_id` puede ser htttps://service.contoso.com/. aplicación de cliente de Hello debe rechazar una `resource_id` que no comienza con la dirección URL base de Hola a menos que haya un identificador de hello tooverify alternativa confiable. |

#### Códigos de error del esquema de portador
Hola especificación RFC 6750 define Hola siguientes errores de los recursos que usan el encabezado WWW-Authenticate de Hola y el esquema de portador en respuesta de Hola.

| Código de estado HTTP | Código de error | Description | Acción del cliente |
| --- | --- | --- | --- |
| 400 |invalid_request |solicitud de Hello no está bien formado. Por ejemplo, podría faltar un parámetro o uso Hola mismo parámetro dos veces. |Corrija el error de Hola y vuelva a intentar la solicitud de saludo. Este tipo de error solo debe producirse durante el desarrollo y detectarse en las pruebas iniciales. |
| 401 |invalid_token |token de acceso de Hello es que faltan, no es válido o se ha revocado. valor de Hola de parámetro de hello error_description proporciona detalles adicionales. |Solicitar un nuevo token Hola servidor de autorización. Si se produce un error en el nuevo token de hello, se ha producido un error inesperado. Enviar un usuario toohello de mensaje de error e intente de nuevo después de retrasos aleatorios. |
| 403 |insufficient_scope |token de acceso de Hello no contiene Hola suplantación permisos necesarios tooaccess Hola recursos. |Enviar un nuevo extremo de autorización de toohello de solicitud de autorización. Si respuesta Hola contiene parámetro de ámbito de Hola, utilice el valor de ámbito de Hola en recursos de toohello de solicitud de Hola. |
| 403 |insufficient_access |asunto Hola de token de hello no tiene permisos de Hola que requiere tooaccess Hola recursos. |Hola Prompt usuario toouse una cuenta diferente o toorequest permisos toohello recurso específico. |

## Actualizar los tokens de acceso de Hola
Tokens de acceso son de corta duración y deben actualizarse después de que expiren toocontinue acceso a los recursos. Puede actualizar hello `access_token` mediante el envío de otra `POST` solicitar toohello `/token` punto de conexión, pero esta vez proporcionar hello `refresh_token` en lugar de hello `code`.

Los tokens de actualización no tienen una duración especificada. Por lo general, duraciones de Hola de tokens de actualización son relativamente largas. Sin embargo, en algunos casos, tokens de actualización caducan, se revocan o carecen de privilegios suficientes para la acción de hello deseado. La aplicación necesita tooexpect y controlar errores devueltos por extremo de emisión de tokens de hello correctamente.

Cuando reciba una respuesta con un error de actualización de token, descarte el token de actualización actual de Hola y solicite un nuevo código de autorización o token de acceso. En concreto, cuando utiliza una actualización de token Hola flujo de concesión de código de autorización, si recibe una respuesta con hello `interaction_required` o `invalid_grant` códigos de error, descarte el token de actualización de Hola y solicite un nuevo código de autorización.

Un toohello de solicitud de ejemplo **específico del inquilino** punto de conexión (también puede usar hello **común** extremo) tooget un nuevo token de acceso con un token de actualización tiene el siguiente aspecto:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

### Respuesta correcta
Una respuesta de token correcta tendrá un aspecto similar al siguiente:

```
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1460404526",
  "resource": "https://service.contoso.com/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "refresh_token": "AwABAAAAv YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl PM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfmVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA"
}
```
| Parámetro | Descripción |
| --- | --- |
| token_type |tipo de token Hola. valor de Hello solo admitido es **portador**. |
| expires_in |Hola restante de la duración del token de hello en segundos. Un valor típico es 3600 (una hora). |
| expires_on |Hola fecha y hora en que expira el token de Hola. fecha de Hola se representa como número de Hola de segundos desde 1970-01-01T0:0:0Z UTC hasta el tiempo de expiración de Hola. |
| resource |Identifica Hola protege recursos ese token de acceso de hello puede ser tooaccess usado. |
| ámbito |Suplantación permisos de aplicación de cliente nativo de toohello. permiso de Hello predeterminado es **user_impersonation**. propietario de Hola de recurso de destino de hello puede registrar valores alternativos en Azure AD. |
| access_token |Hola nuevo token de acceso que se solicitó. |
| refresh_token |Nuevo refresh_token de OAuth 2.0 que pueden ser utilizados toorequest nuevos tokens de acceso cuando expira hello en esta respuesta. |

### Respuesta de error
Una respuesta de error de ejemplo podría tener este aspecto:

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: hello application named https://foo.microsoft.com/mail.read was not found in hello tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.  You might have sent your authentication request toohello wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
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
