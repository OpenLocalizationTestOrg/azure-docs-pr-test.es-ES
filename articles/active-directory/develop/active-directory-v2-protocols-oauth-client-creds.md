---
title: "aaaUse Azure AD v2.0 tooaccess proteger los recursos sin interacción del usuario | Documentos de Microsoft"
description: "Compilar aplicaciones web mediante la implementación de Azure AD de Hola Hola OAuth 2.0 del protocolo de autenticación."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 0003ec836d633a5466c48033adedac1108f27203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Fluyen de Azure Active Directory hello y v2.0 OAuth 2.0 credenciales de cliente
Puede usar hello [concesión las credenciales del cliente de OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.4), a veces denominado *OAuth dos segmentos*, tooaccess hospedado en web recursos con el uso de la identidad de una aplicación Hola. Este tipo de concesión normalmente se utiliza para las interacciones de servidor a servidor que se deben ejecutar en segundo plano de hello, sin la intervención inmediata a un usuario. Estos tipos de aplicaciones son a menudo denominado tooas *demonios* o *las cuentas de servicio*.

> [!NOTE]
> el punto de conexión de Hello v2.0 no es compatible con todas las características y escenarios de Azure Active Directory. toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
>
>

Hola más típico *OAuth tres segmentos*, una aplicación cliente es tooaccess permiso concedido un recurso en nombre de un usuario específico. permiso de Hola se delega de aplicación de toohello usuario hello, normalmente durante hello [consentimiento](active-directory-v2-scopes.md) proceso. Sin embargo, en el flujo de credenciales de cliente de hello, se conceden permisos directamente propia aplicación toohello. Cuando la aplicación hello presenta un recurso de token tooa, recursos de hello exige que propia aplicación hello tiene autorización tooperform una acción, y no que el usuario hello tiene autorización.

## Diagrama de protocolo
flujo de credenciales de clientes en su totalidad Hello tiene un aspecto similar toohello siguiente diagrama. Se describe cada uno de los pasos de hello más adelante en este artículo.

![Flujo de credenciales de cliente](../../media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## Obtención de autorización directa
Una aplicación normalmente recibe autorización directa tooaccess un recurso de una de dos maneras: a través de una lista de control de acceso (ACL) en recursos de hello, o a través de la asignación de permisos de aplicación en Azure Active Directory (Azure AD). Estos dos métodos son más comunes en Azure AD hello y recomendamos para los clientes y los recursos que realizan flujo de credenciales de cliente de Hola. Un recurso puede elegir tooauthorize sus clientes de otras maneras, sin embargo. Cada servidor de recursos puede elegir método de Hola que le resulte hello más conveniente para su aplicación.

### Listas de control de acceso
Un proveedor de recursos podría exigir una comprobación de autorización basada en una lista de identificadores de aplicación que conoce y concede un nivel de acceso específico. Cuando recursos Hola reciben un token de punto de conexión de hello v2.0, se puede descodificar el token de Hola y extraer el identificador de la aplicación del cliente de Hola de hello `appid` y `iss` notificaciones. A continuación, compara la aplicación hello en una ACL que mantenga. Hola granularidad de la ACL y método puede variar considerablemente entre los recursos.

Un caso de uso común es toouse un toorun ACL pruebas para una aplicación web o de una API Web. Hola API Web podría conceder a solo un subconjunto de todos los permisos tooa específicos del cliente. pruebas de extremo a extremo toorun Hola API, cree un cliente de prueba que adquiere tokens desde el punto de conexión de hello v2.0 y, a continuación, envía toohello API. Hola API, a continuación, comprobaciones de hello ACL para hello probar Id. de aplicación del cliente para tener acceso total toohello API toda funcionalidad. Si utiliza este tipo de ACL, asegúrese de toovalidate Hola no solo del llamador `appid` valor. También validar ese hello `iss` valor del token de hello es de confianza.

Este tipo de autorización es común que los daemons y cuentas de servicio que necesitan datos tooaccess pertenecen a los usuarios de consumidor con cuentas personales de Microsoft. Para los datos que pertenecen a las organizaciones, se recomienda solicitar autorización necesaria de Hola a través de los permisos de la aplicación.

### Permisos de aplicación
En lugar de utilizar las ACL, puede usar las API tooexpose un conjunto de permisos de aplicación. Un permiso de aplicación se concede tooan aplicación por el Administrador de una organización, y pueden ser usado tooaccess solo datos propiedad dicha organización y sus empleados. Por ejemplo, Microsoft Graph expone varias siguientes de Hola de toodo de permisos de aplicación:

* Leer correo en todos los buzones de correo
* Leer y escribir correo en todos los buzones de correo
* Enviar correo como cualquier usuario
* Leer datos de directorio

Para obtener más información acerca de los permisos de aplicación, vaya demasiado[Microsoft Graph](https://graph.microsoft.io).

permisos de aplicación de toouse en la aplicación Hola pasos se explican en las secciones siguientes se Hola.

#### Solicitar permisos de hello en el portal de registro de aplicación Hola
1. Vaya tooyour aplicación Hola [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o [crear una aplicación](active-directory-v2-app-registration.md), si no lo ha hecho ya. Necesitará toouse al menos un secreto de aplicación cuando se crea la aplicación.
2. Busque hello **permisos directos de aplicación** sección y, a continuación, agregue permisos de Hola que requiere la aplicación.
3. **Guardar** Hola de registro de la aplicación.

#### Recomendado: Usuario de inicio de sesión hello en tooyour aplicación
Normalmente, cuando se compila una aplicación que usa permisos de aplicación, aplicación hello requiere una página o una vista en qué Hola administrador aprueba los permisos de la aplicación hello. Esta página puede formar parte de inicio de sesión de flujo la aplicación hello, parte de la configuración de la aplicación hello, o puede ser dedicado "conectar" flujo. En muchos casos, tiene sentido para hello aplicación tooshow esto "conectar" vista sólo después de que un usuario haya iniciado sesión con un trabajo o escuela cuenta Microsoft.

Si inicia la sesión de usuario de hello en tooyour aplicación, puede identificar la organización de hello pertenece el usuario de Hola de toowhich antes de solicitar permisos de aplicación Hola Hola usuario tooapprove. Aunque no es estrictamente necesario, puede ayudarlo a crear una experiencia más intuitiva para los usuarios. usuario de hello toosign en siguen nuestro [tutoriales de protocolo v2.0](active-directory-v2-protocols.md).

#### Hola solicitar los permisos de un administrador de directorio
Cuando esté listo toorequest permisos de administrador de organización de hello, puede redirigir Hola usuario toohello v2.0 *extremo de consentimiento de administración*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Parámetro | Condición | Descripción |
| --- | --- | --- |
| tenant |Obligatorio |inquilino de directorio de Hola que desee toorequest permiso de. Puede estar en formato de nombre descriptivo o GUID. Si no sabe qué usuario de hello inquilino pertenece tooand desea toolet ellos inicie sesión con todos los inquilinos, use `common`. |
| client_id |Obligatorio |Hola aplicación Id. que hello [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) asignado tooyour aplicación. |
| redirect_uri |Obligatorio |Hola redirigir URI donde desee hello toobe de respuesta enviado para su toohandle de aplicación. Debe coincidir exactamente con uno de redirección de hello URI que se ha registrado en el portal de hello, excepto en que debe ser la dirección URL codificada y puede contener segmentos de ruta de acceso adicional. |
| state |Recomendado |Un valor que se incluye en la solicitud de Hola que también se devuelve en la respuesta de token de Hola. Puede ser una cadena de cualquier contenido que desee. estado de Hello es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido en solicitud de autenticación de hello, como página de Hola o que estaban en la vista. |

En este momento, Azure AD exige que solo un administrador de inquilinos puede iniciar sesión en la solicitud de hello toocomplete. Administrador de Hello pedirá tooapprove que todos Hola permisos directo de aplicaciones que han solicitado para la aplicación de portal de registro de aplicación Hola.

##### Respuesta correcta
Si Hola, administrador aprueba permisos hello para la aplicación, la respuesta es correcta Hola se ve así:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Parámetro | Description |
| --- | --- | --- |
| tenant |inquilino de directorio de Hola que conceden los permisos de aplicación Hola que solicita, en formato GUID. |
| state |Un valor que se incluye en la solicitud de Hola que también se devuelve en la respuesta de token de Hola. Puede ser una cadena de cualquier contenido que desee. estado de Hello es tooencode usa información acerca del estado del usuario de hello en la aplicación hello antes de que se ha producido en solicitud de autenticación de hello, como página de Hola o que estaban en la vista. |
| admin_consent |Establecer demasiado**true**. |

##### Respuesta de error
Si Hola, administrador no puede aprobar los permisos de hello para la aplicación, Hola error respuesta es similar al siguiente:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Parámetro | Description |
| --- | --- | --- |
| error |Una cadena de código de error que se pueden usar tipos de tooclassify de errores y que puede usar tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudarle a identificar la causa de raíz de Hola de un error. |

Una vez que ha recibido una respuesta correcta del extremo de aprovisionamiento de aplicación Hola, la aplicación ha obtenido permisos de la aplicación directa de Hola que solicitó. Ahora puede solicitar un token para recursos de Hola que desee.

## Obtención de un token
Una vez que haya adquirido la autorización necesaria de hello para la aplicación, continúe con la adquisición de tokens de acceso para las API. tooget un token mediante el uso de concesión de credenciales de cliente de hello, envíe un toohello de solicitud POST `/token` v2.0 extremo:

### Primer caso: solicitud de token de acceso con un secreto compartido

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| Parámetro | Condición | Descripción |
| --- | --- | --- |
| client_id |Obligatorio |Hola aplicación Id. que hello [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) asignado tooyour aplicación. |
| ámbito |Obligatorio |pasa el valor de Hola para hello `scope` parámetro en esta solicitud debe ser el identificador hello de recursos (URI de Id. de la aplicación) del recurso de Hola que desee, colocado con hello `.default` sufijo. Por ejemplo, Microsoft Graph hello, valor de hello es `https://graph.microsoft.com/.default`. Este valor le informa de punto de conexión de hello v2.0 que de todos los permisos de aplicación directa Hola que ha configurado para la aplicación, debe emitir un token para hello los asociados con el recurso de Hola que desee toouse. |
| client_secret |Obligatorio |Hola secreto de aplicación que ha generado para la aplicación de portal de registro de aplicación Hola. |
| grant_type |Obligatorio |Debe ser `client_credentials`. |

### Segundo caso: solicitud de token de acceso con un certificado

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

| Parámetro | Condición | Descripción |
| --- | --- | --- |
| client_id |Obligatorio |Hola aplicación Id. que hello [Portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) asignado tooyour aplicación. |
| ámbito |Obligatorio |pasa el valor de Hola para hello `scope` parámetro en esta solicitud debe ser el identificador hello de recursos (URI de Id. de la aplicación) del recurso de Hola que desee, colocado con hello `.default` sufijo. Por ejemplo, Microsoft Graph hello, valor de hello es `https://graph.microsoft.com/.default`. Este valor le informa de punto de conexión de hello v2.0 que de todos los permisos de aplicación directa Hola que ha configurado para la aplicación, debe emitir un token para hello los asociados con el recurso de Hola que desee toouse. |
| client_assertion_type |requerido |debe ser el valor de Hola`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |requerido | Una aserción (un Token Web JSON) que necesita toocreate y el inicio de sesión con hello de certificados se registra como credenciales para la aplicación. Obtenga información sobre [las credenciales del certificado](active-directory-certificate-credentials.md) toolearn cómo tooregister su formato hello y certificado de aserción de Hola.|
| grant_type |Obligatorio |Debe ser `client_credentials`. |

Tenga en cuenta que los parámetros de hello son casi Hola igual que en el caso de saludo de solicitud de Hola por secreto compartido salvo que el parámetro de hello client_secret se sustituye por dos parámetros: una client_assertion_type y client_assertion.

### Respuesta correcta
Una respuesta correcta tiene el siguiente aspecto:

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| Parámetro | Description |
| --- | --- |
| access_token |símbolo (token) de acceso solicitado Hola. aplicación Hello puede usar este toohello tooauthenticate token protegida el recurso, como tooa API Web. |
| token_type |Indica el valor de tipo de token de Hola. Hola solo tipo que admite Azure AD es `bearer`. |
| expires_in |¿Durante cuánto tiempo el token de acceso de hello es válida (en segundos). |

### Respuesta de error
Una respuesta de error tiene el aspecto siguiente:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Una cadena de código de error que se pueden usar tipos de tooclassify de errores que se producen y tooreact tooerrors. |
| error_description |Un mensaje de error específico que puede ayudarle a identificar la causa de raíz de Hola de un error de autenticación. |
| error_codes |Una lista de los códigos de error específicos de STS que podrían ayudar en los diagnósticos. |
| timestamp |hora de Hello en que se produjo el error de Hola. |
| trace_id |Un identificador único para la solicitud de Hola que puede resultar útil en el diagnóstico. |
| correlation_id |Un identificador único para la solicitud de Hola que puede resultar útil en el diagnóstico en componentes. |

## Uso de un token
Ahora que ha adquirido un token, use hello toomake token solicitudes toohello recursos. Cuando expira el token de hello, repita Hola solicitud toohello `/token` extremo tooacquire un token de acceso nuevo.

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try hello following command! (Replace hello token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## Código de ejemplo
toosee muestra un ejemplo de una aplicación que implementa Hola concesión de credenciales de cliente mediante el uso de extremo de consentimiento de administración de hello, consulte nuestro [ejemplo de código de demonio de v2.0](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
