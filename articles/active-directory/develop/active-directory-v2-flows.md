---
title: "tipos de aaaApp para el punto de conexión de hello Azure Active Directory v2.0 | Documentos de Microsoft"
description: "tipos de Hola de aplicaciones y escenarios admitidos por el punto de conexión de hello Azure Active Directory v2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a>Tipos de aplicación para el punto de conexión de hello Azure Active Directory v2.0
Hello extremo de la versión 2.0 de Azure Active Directory (Azure AD) admite la autenticación para una variedad de arquitecturas de aplicaciones modernas, todos ellos se basan en protocolos estándar del sector [OAuth 2.0 o OpenID Connect](active-directory-v2-protocols.md). Este artículo describen los tipos de Hola de las aplicaciones que pueden crear mediante v2.0 de Azure AD, independientemente de su plataforma o el idioma preferido. Hello información contenida en este artículo está diseñado toohelp comprender los escenarios de alto nivel antes de [empezar a trabajar con código de hello](active-directory-appmodel-v2-overview.md#getting-started).

> [!NOTE]
> el punto de conexión de Hello v2.0 no es compatible con todas las características y escenarios de Azure Active Directory. toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

## <a name="hello-basics"></a>conceptos básicos de Hola
Debe registrar cada aplicación que utiliza el punto de conexión de hello v2.0 en hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com). proceso de registro de aplicación Hola recopila y asigna estos valores para la aplicación:

* Un **id. de aplicación** que identifica de forma única su aplicación
* A **URI de redireccionamiento** que puede usar toodirect respuestas atrás tooyour aplicación
* Algunos otros valores específicos de cada escenario.

Para obtener más información, obtenga información acerca de cómo demasiado[registrar una aplicación](active-directory-v2-app-registration.md).

Una vez registrada la aplicación hello, aplicación hello se comunica con Azure AD mediante el envío de solicitudes toohello Azure AD v2.0 extremo. Proporcionamos marcos de código abierto y bibliotecas que administran Hola detalles de estas solicitudes. También tiene lógica de autenticación de hello opción tooimplement Hola usted mismo mediante la creación de las solicitudes de los puntos de conexión de toothese:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a>Aplicaciones web
Para las aplicaciones web (. NET, PHP, Java, Ruby, Python, nodo) que Hola accesos de usuario a través de un explorador, puede usar [OpenID Connect](active-directory-v2-protocols.md) para el inicio de sesión de usuario. En OpenID Connect, aplicación de hello web recibe un identificador de token. Un identificador de token es un token de seguridad que comprueba la identidad del usuario de Hola y proporciona información acerca del usuario de hello en forma de Hola de notificaciones:

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Puede obtener información acerca de todos los tipos de Hola de tokens y notificaciones de aplicación tooan disponible en hello [v2.0 tokens referencia](active-directory-v2-tokens.md).

En las aplicaciones de servidor web, flujo de inicio de sesión autenticación de hello realiza estos pasos de alto nivel:

![Flujo de autenticación de aplicaciones web](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

Puede asegurarse de identidad del usuario de hello mediante la validación de token de Id. de hello con una clave de firma pública que se recibe desde el punto de conexión de hello v2.0. Se establece una cookie de sesión, que puede ser usuario de hello tooidentify utilizados en las solicitudes de las páginas posteriores.

ejemplos de este escenario en acción, pruebe una hello web de inicio de sesión del código de aplicación de toosee en nuestra v2.0 [Introducción](active-directory-appmodel-v2-overview.md#getting-started) sección.

Además toosimple inicio de sesión de, una aplicación de servidor web que tenga tooaccess otro servicio web, como una API de REST. En este caso, aplicación de servidor web de hello se involucra en un flujo de OAuth 2.0 y OpenID Connect combinado, mediante el uso de hello [flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols.md). Para más información sobre este escenario, lea acerca de cómo [comenzar con aplicaciones web y API web](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).

## <a name="web-apis"></a>API web
Puede usar Hola v2.0 extremo toosecure servicios web, por ejemplo, API la aplicación de Web RESTful. En lugar de tokens de identificador y las cookies de sesión, una API Web utiliza un toosecure de token de acceso de OAuth 2.0 sus datos y tooauthenticate las solicitudes entrantes. autor de llamada de Hola de una API Web anexa un token de acceso en el encabezado de autorización de Hola de una solicitud HTTP, similar al siguiente:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hola API Web utiliza información de identidad y tooextract del llamador de hello acceso tooverify token Hola API sobre llamador Hola de notificaciones que se codifican en el token de acceso de Hola. toolearn sobre todos los tipos de Hola de tokens y notificaciones de la aplicación tooan disponibles, vea hello [v2.0 tokens referencia](active-directory-v2-tokens.md).

Puede conceder a los usuarios Hola power tooopt de o rechazar una funcionalidad específica o datos mediante la exposición de permisos, también conocido como una API Web [ámbitos](active-directory-v2-scopes.md). Un llamada aplicación tooacquire ámbito de permisos tooa, usuario de hello debe dar su consentimiento toohello ámbito durante un flujo. el punto de conexión de Hello v2.0 solicita permiso usuario hello y, a continuación, registra los permisos en todos los tokens de acceso ese Hola que API Web recibe. Hola API Web valida los tokens de acceso de hello recibe en cada llamada y realiza comprobaciones de autorización.

Una API web puede recibir tokens de acceso de todos los tipos de aplicaciones, incluidas las aplicaciones de servidor web, aplicaciones móviles y de escritorio, aplicaciones de una página, demonios del lado del servidor e incluso otras API web. flujo de alto nivel de Hola para una API Web tiene el siguiente aspecto:

![Flujo de autenticación de API web](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

toolearn cómo toosecure una API Web mediante el uso de tokens de acceso OAuth2, desprotección Hola código de la API Web de ejemplos en nuestro [Introducción](active-directory-appmodel-v2-overview.md#getting-started) sección.

En muchos casos, las API web también necesitan toomake solicitudes salientes en un nivel inferior tooother web API protegidas por Azure Active Directory.  toodo por lo tanto, las API web puede aprovechar las ventajas de Azure AD **en nombre de** flujo, lo que permite un token de acceso entrante para otro toobe de token de acceso utilizado en las solicitudes salientes de hello web API tooexchange.  Hola v2.0 punto de conexión en nombre de flujo se describe en [detalle aquí](active-directory-v2-protocols-oauth-on-behalf-of.md).

## <a name="mobile-and-native-apps"></a>Aplicaciones móviles y nativas
Aplicaciones de dispositivo instalado, como aplicaciones de escritorio y móviles, suelen necesitan servicios back-end de tooaccess o las API Web que almacenan los datos y realizar acciones en nombre del usuario. Estas aplicaciones pueden agregar servicios de tooback-end de inicio de sesión y la autorización mediante hello [flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

En este flujo, aplicación hello recibe un código de autorización desde el punto de conexión de hello v2.0 cuando Hola usuario inicia sesión. Servicios de back-end de la aplicación de Hello autorización código representa Hola permiso toocall en nombre de usuario de Hola que ha iniciado sesión. aplicación Hello puede intercambiar el código de autorización de hello en segundo plano de Hola para un token de acceso de OAuth 2.0 y un token de actualización. aplicación Hello puede usar Hola acceso token tooauthenticate tooWeb API en las solicitudes HTTP y usar Hola actualización tooget token nuevos tokens de acceso cuando expiran los tokens de acceso anteriores.

![Flujo de autenticación de la aplicación nativa](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a>Aplicaciones de una página (JavaScript)
Muchas aplicaciones modernas tienen un front-end de aplicación de una página escrito principalmente en JavaScript. A menudo, se escribe con un marco como AngularJS, Ember.js o Durandal.js. punto de conexión de v2.0 Hello Azure AD admite estas aplicaciones mediante hello [flujo implícito de OAuth 2.0](active-directory-v2-protocols-implicit.md).

En este flujo de la aplicación hello recibe los tokens directamente de hello v2.0 autorizar el punto de conexión, sin los intercambios de servidor a servidor. Todos los lógica de autenticación y control de la toma de la sesión colocan completamente en el cliente de JavaScript de hello, sin las redirecciones de páginas adicionales.

![Flujo de autenticación implícita](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

toosee este escenario en acción, pruebe uno de los ejemplos de código de aplicación de una sola página de hello en nuestro [Introducción](active-directory-appmodel-v2-overview.md#getting-started) sección.

## <a name="daemons-and-server-side-apps"></a>Demonios y aplicaciones de servidor
Las aplicaciones que tienen procesos de larga duración o que funcionan sin la interacción con un usuario también necesitan un modo tooaccess protege los recursos, como las API Web. Estas aplicaciones pueden autenticar y obtener tokens mediante el uso de la identidad de la aplicación hello, en lugar de un usuario delegado identidad, con flujo de credenciales de cliente hello OAuth 2.0.

En este flujo de la aplicación hello interactúa directamente con hello `/token` puntos de conexión de punto de conexión tooobtain:

![Flujo de autenticación de aplicación de demonio](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

toobuild una aplicación demonio, consulte la documentación de las credenciales del cliente de hello en nuestro [Introducción](active-directory-appmodel-v2-overview.md#getting-started) sección o intente una [aplicación de ejemplo .NET](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
