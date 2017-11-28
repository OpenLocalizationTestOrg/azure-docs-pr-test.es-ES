---
title: "aaaAzure AD servicio tooservice autenticación mediante OAuth2.0 especificación de borrador en nombre de otra persona | Documentos de Microsoft"
description: "Este artículo describe cómo toouse HTTP mensajes tooimplement autenticación de servicios tooservice con Hola OAuth2.0 en nombre de flujo."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 55b7fcfe6c0223bddedd8d8fa2defcb5769b43c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Servicio tooservice llama a usar la identidad de usuario delegado en hello en nombre de flujo
Hola flujo de OAuth 2.0 On-Behalf-Of sirve de caso de uso de Hola donde una aplicación invoca un servicio web o API, que a su vez debe toocall otro servicio o web API. idea Hello es toopropagate Hola delega permisos a través de la cadena de solicitud de Hola e identidad de usuario. Para hello servicio de nivel intermedio toomake autentica las solicitudes toohello servicio de nivel inferior, debe toosecure un token de acceso de Azure Active Directory (Azure AD), en nombre de usuario de Hola.

## Diagrama del flujo de On-Behalf-Of
Suponga ese usuario Hola se ha autenticado en una aplicación con hello [flujo de concesión de código de autorización de OAuth 2.0](active-directory-protocols-oauth-code.md). En este momento, aplicación hello tiene un token de acceso (un símbolo (token)) con notificaciones de usuario de Hola y web de nivel intermedio de consentimiento tooaccess Hola API (API de A). Ahora, la API A debe toomake una API web de nivel inferior de toohello de solicitud autenticada (API B).

pasos de Hola que seguir constituyen hello en nombre de flujo y se explican con ayuda de Hola de hello siguiente diagrama.

![Flujo en nombre de OAuth 2.0](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. aplicación de cliente de Hello realiza una tooAPI de solicitud con a hello símbolo (token).
2. API A autentica el extremo de emisión de tokens de Azure AD toohello y solicita un token tooaccess API B.
3. extremo de emisión de tokens de Azure AD Hola valida las credenciales de la API A con un símbolo (token) y problemas Hola token de acceso de API B (token B).
4. token Hola B se establece en el encabezado de autorización de Hola de hello solicitud tooAPI B.
5. Devuelve datos de hello protegida recursos API B.

## Registrar aplicación Hola y el servicio en Azure AD
Registrar aplicación de cliente de hello y servicio de nivel intermedio de hello en Azure AD.
### Registrar el servicio de nivel intermedio de Hola
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta y en hello **Directory** lista, elija el inquilino de Active Directory de Hola que le gustaría tooregister la aplicación.
3. Haga clic en **más servicios** en Hola nav izquierda y elija **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y elija **Nuevo registro de aplicaciones**.
5. Escriba un nombre descriptivo para la aplicación hello y seleccione el tipo de aplicación Hola. Se basa en el tipo de aplicación Hola conjunto Hola inicio de sesión de dirección URL o dirección URL de redireccionamiento URL toohello base. Haga clic en **crear** aplicación de hello toocreate.
6. Mientras sigue en hello portal de Azure, elija la aplicación y haga clic en **configuración**. En el menú de configuración de hello, elija **claves** y agregar una clave: seleccione una duración de clave del año 1 o 2 años. Al guardar esta página, valor de clave de Hola se mostrará, copiar y guardar el valor de hello en una ubicación segura; lo necesitará esta clave posteriores tooconfigure Hola configuración de la aplicación en su implementación - este valor de clave no será nuevo mostrado, ni puede recuperar por cualquiera otra manera, por lo que les registro, tan pronto como es visible desde Hola Portal de Azure.

### Registrar aplicación de cliente hello
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta y en hello **Directory** lista, elija el inquilino de Active Directory de Hola que le gustaría tooregister la aplicación.
3. Haga clic en **más servicios** en Hola nav izquierda y elija **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y elija **Nuevo registro de aplicaciones**.
5. Escriba un nombre descriptivo para la aplicación hello y seleccione el tipo de aplicación Hola. Se basa en el tipo de aplicación Hola conjunto Hola inicio de sesión de dirección URL o dirección URL de redireccionamiento URL toohello base. Haga clic en **crear** aplicación de hello toocreate.
6. Configurar los permisos para la aplicación - en el menú de configuración de hello, elija hello **los permisos necesarios** sección, haga clic en **agregar**, a continuación, **seleccionar una API**, tipo hello y nombre del servicio de nivel intermedio de hello en el cuadro de texto de Hola. Después, haga clic en **Seleccionar permisos** y seleccione "Acceder a *nombre del servicio*".

### Configuración de aplicaciones cliente conocidas
En este escenario, servicio de nivel intermedio de hello no dispone de ningún usuario interacción tooobtain Hola del usuario API de nivel inferior de hello tooaccess de consentimiento. Por lo tanto, Hola opción toogrant acceso toohello debe contar con API de nivel inferior por adelantado como parte del paso de consentimiento de Hola durante la autenticación.
tooachieve, siga los pasos a continuación el registro de la aplicación de cliente de tooexplicitly enlace hello en Azure AD con el registro de hello de servicio de nivel intermedio de hello, que combina requerido por el cliente de Hola y de nivel intermedio en un único cuadro de diálogo de consentimiento de Hola Hola.
1. Navegar por el registro del servicio de nivel intermedio de toohello y haga clic en **manifiesto** editor de manifiestos de hello tooopen.
2. En el manifiesto de hello, busque hello `knownClientApplications` propiedad de matriz y agregar Id. de cliente de aplicación de cliente de Hola Hola como un elemento.
3. Guarde el manifiesto de hello haciendo clic en hello botón Guardar.

## Solicitud de token de acceso de tooservice de servicio
toorequest un token de acceso, asegúrese de un punto de conexión de HTTP POST toohello específico del inquilino Azure AD con hello parámetros siguientes.

```
https://login.microsoftonline.com/<tenant>/oauth2/token
```
Hay dos casos dependiendo de si la aplicación de cliente de hello elige toobe protegido por un secreto compartido o un certificado.

### Primer caso: solicitud de token de acceso con un secreto compartido
Cuando se usa un secreto compartido, una solicitud de token de acceso del servicio a servicio contiene Hola parámetros siguientes:

| Parámetro |  | Descripción |
| --- | --- | --- |
| grant_type |requerido | tipo de saludo de solicitud de token de Hola. Para una solicitud con un JWT, el valor de hello debe ser **urn: ietf:params:oauth:grant-tipo: jwt-portador**. |
| Aserción |requerido | valor de Hola de hello token que se utiliza en la solicitud de saludo. |
| client_id |requerido | Hello Id. de aplicación había asignado toohello llamada servicio durante el registro con Azure AD. Id. de aplicación del toofind Hola Hola Portal de administración de Azure, haga clic en **Active Directory**, haga clic en el directorio de hello y, a continuación, haga clic en nombre de la aplicación hello. |
| client_secret |requerido | clave de Hello registrado para hello llamar al servicio de Azure AD. Este valor debe se han anotado en tiempo de presentación del registro. |
| resource |requerido | Hola App ID URI de Hola recibir servicio (recurso seguro). Hola toofind App ID URI, Hola Portal de administración de Azure, haga clic en **Active Directory**, haga clic en el directorio de hello, haga clic en el nombre de la aplicación hello, haga clic en **toda la configuración de** y, a continuación, haga clic en **propiedades** . |
| requested_token_use |requerido | Especifica cómo se debe procesar la solicitud de saludo. Hola en nombre de flujo, el valor de hello debe ser **on_behalf_of**. |
| ámbito |requerido | Lista de ámbitos para solicitud de token de hello separada de un espacio. Para OpenID Connect, Hola ámbito **openid** debe especificarse.|

#### Ejemplo
Hello siguiente HTTP POST solicita un token de acceso de API de web de hello https://graph.windows.net. Hola `client_id` identifica el servicio de Hola que solicita un token de acceso de Hola.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_secret=0Y1W%2BY3yYb3d9N8vSjvm8WrGzVZaAaHbHHcGbcgG%2BoI%3D
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

### Segundo caso: solicitud de token de acceso con un certificado
Una solicitud de token de acceso al servicio con un certificado contiene Hola parámetros siguientes:

| Parámetro |  | Descripción |
| --- | --- | --- |
| grant_type |requerido | tipo de saludo de solicitud de token de Hola. Para una solicitud con un JWT, el valor de hello debe ser **urn: ietf:params:oauth:grant-tipo: jwt-portador**. |
| Aserción |requerido | valor de Hola de hello token que se utiliza en la solicitud de saludo. |
| client_id |requerido | Hello Id. de aplicación había asignado toohello llamada servicio durante el registro con Azure AD. Id. de aplicación del toofind Hola Hola Portal de administración de Azure, haga clic en **Active Directory**, haga clic en el directorio de hello y, a continuación, haga clic en nombre de la aplicación hello. |
| client_assertion_type |requerido |debe ser el valor de Hola`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |requerido | Una aserción (un Token Web JSON) que necesita toocreate y el inicio de sesión con hello de certificados se registra como credenciales para la aplicación.  Obtenga información sobre [las credenciales del certificado](active-directory-certificate-credentials.md) toolearn cómo tooregister su formato hello y certificado de aserción de Hola.|
| resource |requerido | Hola App ID URI de Hola recibir servicio (recurso seguro). Hola toofind App ID URI, Hola Portal de administración de Azure, haga clic en **Active Directory**, haga clic en el directorio de hello, haga clic en el nombre de la aplicación hello, haga clic en **toda la configuración de** y, a continuación, haga clic en **propiedades** . |
| requested_token_use |requerido | Especifica cómo se debe procesar la solicitud de saludo. Hola en nombre de flujo, el valor de hello debe ser **on_behalf_of**. |
| ámbito |requerido | Lista de ámbitos para solicitud de token de hello separada de un espacio. Para OpenID Connect, Hola ámbito **openid** debe especificarse.|

Tenga en cuenta que los parámetros de hello son casi Hola igual que en el caso de saludo de solicitud de Hola por secreto compartido salvo que el parámetro de hello client_secret se sustituye por dos parámetros: una client_assertion_type y client_assertion.

#### Ejemplo
Hola siguiente HTTP POST solicita un token de acceso para hello https://graph.windows.net API web con un certificado. Hola `client_id` identifica el servicio de Hola que solicita un token de acceso de Hola.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

## Respuesta de token de acceso de tooservice de servicio
Una respuesta correcta es una respuesta JSON OAuth 2.0 con hello parámetros siguientes.

| Parámetro | Descripción |
| --- | --- |
| token_type |Indica el valor de tipo de token de Hola. Hola solo tipo que admite Azure AD es **portador**. Para obtener más información acerca de los tokens de portador, vea hello [marco de autorización de OAuth 2.0: uso del Token del portador (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| ámbito |ámbito de Hola de acceso concedido en token Hola. |
| expires_in |longitud de Hola de token de acceso de Hola de tiempo es válida (en segundos). |
| expires_on |hora de Hello cuando expire el token de acceso de Hola. fecha de Hola se representa como número de Hola de segundos desde 1970-01-01T0:0:0Z UTC hasta el tiempo de expiración de Hola. Este valor es la duración de hello toodetermine uso de tokens almacenados en caché. |
| resource |Hola App ID URI de Hola recibir servicio (recurso seguro). |
| access_token |símbolo (token) de acceso solicitado Hola. Hola llamar al servicio puede usar este servicio de recepción de toohello tooauthenticate símbolo (token). |
| ID_token |token de Id. solicitado Hola. Hola llamar al servicio puede utilizar la identidad del usuario tooverify hello y empezar una sesión de usuario de Hola. |
| refresh_token |token de actualización de Hello para el token de acceso solicitado Hola. Hola llamar al servicio puede utilizar este token toorequest otro token de acceso después de que expire el token de acceso actual de Hola. |

### Ejemplo de respuesta correcta
Hello en el ejemplo siguiente se muestra una solicitud de tooa de respuesta correcta para un token de acceso de API de web de hello https://graph.windows.net.

```
{
    "token_type":"Bearer",
    "scope":"User.Read",
    "expires_in":"43482",
    "ext_expires_in":"302683",
    "expires_on":"1493466951",
    "not_before":"1493423168",
    "resource":"https://graph.windows.net",
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ",
    "refresh_token":"AQABAAAAAABnfiG-mA6NTae7CdWW7QfdjKGu9-t1scy_TDEmLi4eLQMjJGt_nAoVu6A4oSu1KsRiz8XyQIPKQxSGfbf2FoSK-hm2K8TYzbJuswYusQpJaHUQnSqEvdaCeFuqXHBv84wjFhuanzF9dQZB_Ng5za9xKlUENrNtlq9XuLNVKzxEyeUM7JyxzdY7JiEphWImwgOYf6II316d0Z6-H3oYsFezf4Xsjz-MOBYEov0P64UaB5nJMvDyApV-NWpgklLASfNoSPGb67Bc02aFRZrm4kLk-xTl6eKE6hSo0XU2z2t70stFJDxvNQobnvNHrAmBaHWPAcC3FGwFnBOojpZB2tzG1gLEbmdROVDp8kHEYAwnRK947Py12fJNKExUdN0njmXrKxNZ_fEM33LHW1Tf4kMX_GvNmbWHtBnIyG0w5emb-b54ef5AwV5_tGUeivTCCysgucEc-S7G8Cz0xNJ_BOiM_4bAv9iFmrm9STkltpz0-Tftg8WKmaJiC0xXj6uTf4ZkX79mJJIuuM7XP4ARIcLpkktyg2Iym9jcZqymRkGH2Rm9sxBwC4eeZXM7M5a7TJ-5CqOdfuE3sBPq40RdEWMFLcrAzFvP0VDR8NKHIrPR1AcUruat9DETmTNJukdlJN3O41nWdZOVoJM-uKN3uz2wQ2Ld1z0Mb9_6YfMox9KTJNzRzcL52r4V_y3kB6ekaOZ9wQ3HxGBQ4zFt-2U0mSszIAA",
    "id_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IvIiwiaWF0IjoxNDkzNDIzMTY4LCJuYmYiOjE0OTM0MjMxNjgsImV4cCI6MTQ5MzQ2Njk1MSwiYW1yIjpbInB3ZCJdLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXRpIjoieEN3ZnpoYS1QMFdKUU9MeENHZ0tBQSIsInZlciI6IjEuMCJ9."
}
```

### Ejemplo de respuesta de error
Una respuesta de error se devuelve por extremo de token de Azure AD al intentar tooacquire un token de acceso de API de nivel inferior de hello, si la API de nivel inferior de hello tiene una directiva de acceso condicional, como la autenticación multifactor establecido en él. servicio de nivel intermedio de Hello debe expuesta en esta aplicación de cliente de toohello de error para que la aplicación de cliente de hello puede proporcionar la directiva de acceso condicional de hello usuario interacción toosatisfy Hola.

```
{
    "error":"interaction_required",
    "error_description":"AADSTS50079: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must enroll in multi-factor authentication tooaccess 'bf8d80f9-9098-4972-b203-500f535113b1'.\r\nTrace ID: b72a68c3-0926-4b8e-bc35-3150069c2800\r\nCorrelation ID: 73d656cf-54b1-4eb2-b429-26d8165a52d7\r\nTimestamp: 2017-05-01 22:43:20Z",
    "error_codes":[50079],
    "timestamp":"2017-05-01 22:43:20Z",
    "trace_id":"b72a68c3-0926-4b8e-bc35-3150069c2800",
    "correlation_id":"73d656cf-54b1-4eb2-b429-26d8165a52d7",
    "claims":"{\"access_token\":{\"polids\":{\"essential\":true,\"values\":[\"9ab03e19-ed42-4168-b6b7-7001fb3e933a\"]}}}"
}
```

## Usar Hola Hola de tooaccess símbolo (token) de acceso protegido recursos
Ahora servicio de nivel intermedio de hello puede utilizar en un nivel inferior Hola token toomake adquiridos anteriormente autenticado las solicitudes toohello web API, establecer el token de Hola Hola `Authorization` encabezado.

### Ejemplo
```
GET /me?api-version=2013-11-08 HTTP/1.1
Host: graph.windows.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ
```

## Pasos siguientes
Más información sobre otra manera tooperform servicio tooservice autenticación utilizando las credenciales del cliente y el protocolo hello OAuth 2.0.
* [Autenticación de tooservice de servicio mediante la concesión de credenciales de cliente de OAuth 2.0 en Azure AD](active-directory-protocols-oauth-service-to-service.md)
* [OAuth 2.0 en Azure AD](active-directory-protocols-oauth-code.md)
