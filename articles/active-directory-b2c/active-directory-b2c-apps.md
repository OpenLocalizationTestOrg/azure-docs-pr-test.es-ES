---
title: aaaAzure AD B2C | Documentos de Microsoft
description: tipos de Hola de aplicaciones que puede crear en hello Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a>Azure Active Directory B2C: Tipos de aplicaciones
Azure Active Directory (Azure AD) B2C admite la autenticación para una diversas arquitecturas de aplicaciones modernas. Todos ellos se basan en protocolos estándar del sector de hello [OAuth 2.0](active-directory-b2c-reference-protocols.md) o [OpenID Connect](active-directory-b2c-reference-protocols.md). Este documento describe brevemente los tipos de Hola de aplicaciones que se pueden compilar, independiente del idioma de Hola o plataforma que prefiera. También le ayuda a comprender los escenarios de alto nivel de hello antes de [empezar a crear aplicaciones](active-directory-b2c-overview.md#get-started).

## <a name="hello-basics"></a>conceptos básicos de Hola
Todas las aplicaciones que usa Azure AD B2C deben estar registrada en su [directory B2C](active-directory-b2c-get-started.md) a través de hello [Portal de Azure](https://portal.azure.com/). proceso de registro de aplicación Hola recopila y asigna unos valores tooyour aplicación:

* Un **identificador de la aplicación** que identifica la aplicación de forma única.
* A **URI de redireccionamiento** que pueden ser utilizados toodirect respuestas tooyour back-app.
* Cualquier otro valor específico de cada escenario. Para obtener más detalles, obtenga información acerca de cómo demasiado[registrar una aplicación](active-directory-b2c-app-registration.md).

Una vez registrada la aplicación hello, se comunica con Azure AD mediante el envío de solicitudes toohello Azure AD v2.0 extremo:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

Cada solicitud que se envía tooAzure AD B2C especifica un **directiva**. Una directiva controla el comportamiento de Hola de Azure AD. También puede utilizar estos toocreate un conjunto muy personalizable de experiencias de usuario de puntos de conexión. Algunas directivas comunes son las de registro, las de inicio de sesión y las de edición de perfiles. Si no está familiarizado con las directivas, debe leer acerca de hello Azure AD B2C [marco de directivas extensible](active-directory-b2c-reference-policies.md) antes de continuar.

interacción de Hola de todas las aplicaciones con un punto de conexión de v2.0 sigue un patrón similar de alto nivel:

1. aplicación Hello dirige Hola usuario toohello v2.0 extremo tooexecute una [directiva](active-directory-b2c-reference-policies.md).
2. usuario de Hello completa directiva Hola según la definición de la directiva de toohello.
3. aplicación Hello recibe algún tipo de token de seguridad desde el punto de conexión de hello v2.0.
4. aplicación Hello usa información de token tooaccess protegido de seguridad de Hola o un recurso protegido.
5. servidor de recursos de Hello valida Hola seguridad tooverify símbolo (token) que se pueden conceder acceso.
6. aplicación Hello actualiza periódicamente el token de seguridad de Hola.

<!-- TODO: Need a page for libraries toolink too-->
Estos pasos pueden diferir ligeramente en función de tipo hello de aplicación que se va a compilar. Bibliotecas de código abierto pueden incluir detalles de Hola para usted.

## <a name="web-apps"></a>Aplicaciones web
Para las aplicaciones web (incluidas .NET, PHP, Java, Ruby, Python y Node.js) que se hospedan en un servidor y a las que se tiene acceso a través de un explorador, Azure AD B2C admite [OpenID Connect](active-directory-b2c-reference-protocols.md) para todas las experiencias de usuario. Esto incluye el inicio de sesión, el registro y la administración de perfiles. En la implementación de Azure AD B2C Hola de OpenID Connect, la aplicación web inicia estas experiencias de usuario mediante la emisión de solicitudes de autenticación tooAzure AD. resultado de Hello de solicitud de hello es un `id_token`. Este token de seguridad representa la identidad del usuario de Hola. También proporciona información acerca del usuario de hello en forma de Hola de notificaciones:

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Más información acerca de los tipos de Hola de tokens y notificaciones aplicación tooan disponible en hello [referencia del token B2C](active-directory-b2c-reference-tokens.md).

En una aplicación web, cada ejecución de una [directiva](active-directory-b2c-reference-policies.md) realiza estos pasos generales:

![Imagen de las calles de la aplicación web](./media/active-directory-b2c-apps/webapp.png)

Validación de hello `id_token` mediante el uso de una clave de firma pública que se recibe de Azure AD es suficiente identidad de hello tooverify del usuario de Hola. Esto también establece una cookie de sesión que puede ser usuario de hello tooidentify utilizados en las solicitudes de las páginas posteriores.

toosee este escenario en acción, pruebe uno de los ejemplos de código de inicio de sesión de aplicación hello web en nuestros [Introducción a la sección](active-directory-b2c-overview.md#get-started).

En suma toofacilitating simple inicio de sesión, una aplicación de servidor web también podría necesitar tooaccess un servicio web back-end. En este caso, la aplicación web de hello puede realizar ligeramente diferente [flujo OpenID Connect](active-directory-b2c-reference-oidc.md) y adquirir tokens mediante el uso de códigos de autorización y tokens de actualización. Este escenario se muestra en la siguiente hello [sección de las API Web](#web-apis).

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a>API web
Puede usar los servicios web de Azure AD B2C toosecure como API de REST web de la aplicación. Las API Web puede usar OAuth 2.0 toosecure sus datos, mediante la autenticación de las solicitudes HTTP entrantes mediante tokens. autor de llamada de Hola de una API web anexa un token en el encabezado de autorización de Hola de una solicitud HTTP:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hello web API, a continuación, puede utilizar la información de identidad y tooextract del llamador de hello tooverify token Hola API sobre llamador Hola de notificaciones que se codifican en el token de Hola. Más información acerca de los tipos de Hola de tokens y notificaciones aplicación tooan disponible en hello [referencia del token de Azure AD B2C](active-directory-b2c-reference-tokens.md).

> [!NOTE]
> Azure AD B2C actualmente solo admite API web a las que acceden sus propios clientes conocidos. Por ejemplo, la aplicación completa puede incluir una aplicación iOS, una aplicación Android y una API web back-end. Esta arquitectura es totalmente compatible. Permitir que a un cliente de socios comerciales, como otra aplicación de iOS, tooaccess Hola mismo web que API no se admite actualmente. Todos los componentes de saludo de la aplicación completa de deben compartir un identificador de aplicación único.
>
>

Una API web puede recibir tokens de muchos tipos de clientes, incluidas aplicaciones web, aplicaciones móviles y de escritorio, aplicaciones de una página, demonios del lado del servidor e incluso otras API web. Este es un ejemplo de Hola flujo completa para una aplicación web que llama a una API web de:

![Imagen de las calles de la API web de la aplicación web](./media/active-directory-b2c-apps/webapi.png)

toolearn más información acerca de los códigos de autorización, los tokens de actualización y los pasos de Hola para obtención de tokens, que conozca hello [protocolo OAuth 2.0](active-directory-b2c-reference-oauth-code.md).

toolearn cómo toosecure una API web mediante el uso de Azure AD B2C, consulte hello web tutoriales de API en nuestro [Introducción a la sección](active-directory-b2c-overview.md#get-started).

## <a name="mobile-and-native-apps"></a>Aplicaciones móviles y nativas
Aplicaciones que están instaladas en los dispositivos, como aplicaciones de escritorio y móviles, suelen necesitan servicios back-end de tooaccess o las API web en nombre de los usuarios. Puede agregar aplicaciones nativas de identidad personalizada administración experiencias tooyour y llamar de forma segura servicios back-end mediante hello y Azure AD B2C [flujo de código de autorización de OAuth 2.0](active-directory-b2c-reference-oauth-code.md).  

En este flujo, se ejecuta la aplicación hello [directivas](active-directory-b2c-reference-policies.md) y recibe un `authorization_code` de Azure AD usuario Hola finalizar directiva Hola. Hola `authorization_code` representa Hola servicios de back-end de la aplicación permiso toocall en nombre de usuario de Hola que actualmente ha iniciado sesión. aplicación Hello, a continuación, puede intercambiar hello `authorization_code` en segundo plano de Hola para un `id_token` y `refresh_token`.  aplicación Hello puede usar hello `id_token` tooauthenticate tooa back-end API web en las solicitudes HTTP. También puede utilizar hello `refresh_token` tooget un nuevo `id_token` cuando expira una más antigua.

> [!NOTE]
> B2C de Azure AD admite actualmente solo los tokens que son tooaccess usa un servicio web back-end de la aplicación. Por ejemplo, la aplicación completa puede incluir una aplicación iOS, una aplicación Android y una API web back-end. Esta arquitectura es totalmente compatible. Lo que permite su tooaccess de aplicación de iOS una API web de socios comerciales mediante el uso de tokens de acceso de OAuth 2.0 no se admite actualmente. Todos los componentes de saludo de la aplicación completa de deben compartir un identificador de aplicación único.
>
>

![Imagen de las calles de la aplicación nativa](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a>Limitaciones actuales
Azure AD B2C no admite actualmente la Hola siguientes tipos de aplicaciones, pero se encuentran en la guía básica de Hola. 

### <a name="daemonsserver-side-apps"></a>Demonios o aplicaciones del lado del servidor
Aplicaciones que contienen los procesos de larga duración o que funcionan sin la presencia de Hola de un usuario también necesitan un modo tooaccess proteger recursos como las API web. Estas aplicaciones pueden autenticar y obtener tokens mediante la identidad de la aplicación hello (en lugar de una identidad de usuario delegado) y mediante el uso de flujo de credenciales de cliente hello OAuth 2.0.

Actualmente, este flujo no es compatible con Azure AD B2C. Estas aplicaciones pueden obtener tokens solo después de que se haya producido un flujo de usuario interactivo.

### <a name="web-api-chains-on-behalf-of-flow"></a>Cadenas de la API web (flujo en nombre de)
Muchas arquitecturas incluyen una API que necesita toocall web otra API web descendente, donde ambos están protegidos por Azure AD B2C. Este escenario es habitual en los clientes nativos que tienen una API web back-end. Esto, a continuación, llama a un servicio en línea de Microsoft como Hola API de Azure AD Graph.

Este escenario encadenadas web API puede ser compatibles con concesión de credenciales portador Hola JWT de OAuth 2.0, también conocido como hello en nombre de flujo.  Sin embargo, hello en nombre de flujo no está implementada actualmente en hello Azure AD B2C.
