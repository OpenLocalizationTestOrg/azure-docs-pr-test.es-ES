---
title: "Azure Active Directory B2C: protocolos de autenticación | Microsoft Docs"
description: "¿Cómo toobuild aplicaciones directamente con Hola protocolos que son compatibles con Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5e407d0a-73a2-4d74-ac81-3aa6c31ddcee
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8fa4cbebe711841d410b3ae43b78f893c06d9b63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Azure AD B2C: protocolos de autenticación
Azure Active Directory B2C (Azure AD B2C) proporciona identidad como servicio para sus aplicaciones gracias a la compatibilidad con dos protocolos estándar del sector: OpenID Connect y OAuth 2.0. servicio de Hello es compatible con los estándares, pero las dos implementaciones de estos protocolos pueden tener diferencias sutiles. 

información de Hello en esta guía es útil si se escribe el código directamente enviando y controlar las solicitudes HTTP, en lugar de utilizar una biblioteca de código abierto. Se recomienda que lea esta página antes de profundizar en los detalles de Hola de cada protocolo específico. Pero si ya está familiarizado con Azure AD B2C, puede ir directamente demasiado[Hola guías de referencia de protocolo](#protocols).

<!-- TODO: Need link toolibraries above -->

## conceptos básicos de Hola
Todas las aplicaciones que usa Azure AD B2C necesita toobe registrada en su directorio B2C Hola [portal de Azure](https://portal.azure.com). proceso de registro de aplicación Hola recopila y asigna unos valores tooyour aplicación:

* Un **identificador de la aplicación** que identifica la aplicación de forma única.
* A **URI de redireccionamiento** o **identificador de paquete** que pueden ser utilizados toodirect respuestas tooyour back-app.
* Algunos otros valores específicos de cada escenario. Para obtener más información, consulte [cómo tooregister la aplicación](active-directory-b2c-app-registration.md).

Después de registrar la aplicación, se comunica con Azure Active Directory (Azure AD) mediante el envío de solicitudes toohello extremo:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

En casi todos los flujos de OAuth y OpenID Connect, están implicadas en exchange Hola cuatro partes:

![Funciones de OAuth 2.0](./media/active-directory-b2c-reference-protocols/protocols_roles.png)

* Hola **servidor de autorización** es el punto de conexión de hello Azure AD. Forma segura controla información toouser nada relacionadas y acceso. También administra las relaciones de confianza de hello entre partes de hello en un flujo. Es responsable de comprobar la identidad del usuario de hello, conceder y revocar el acceso tooresources y emisión de tokens. También se denomina es proveedor de identidades de Hola.

* Hola **propietario del recurso** es normalmente el usuario final de Hola. Es parte de Hola que posee datos hello y tiene Hola power tooallow terceros tooaccess esos datos o recurso.

* Hola **cliente OAuth** es la aplicación. Se identifica mediante su identificador de aplicación. Normalmente es parte de Hola que los usuarios finales interactúan con. Asimismo, solicita tokens Hola servidor de autorización. debe conceder el propietario del recurso de Hola Hola cliente permiso tooaccess Hola recursos.

* Hola **servidor de recursos** es donde residen el recurso de Hola o datos. Confianzas de autorización de hello toosecurely servidor autenticar y autorizar el cliente de OAuth de Hola. También se utiliza acceso de portador tooensure de símbolos (tokens) que tienen acceso a recursos de tooa puede concederse.

## Directivas
Sin duda, las directivas de Azure AD B2C son características más importantes de hello del servicio de Hola. Azure AD B2C amplía protocolos estándar de OAuth 2.0 y OpenID Connect Hola introduciendo las directivas. Estos permiten tooperform de Azure AD B2C mucho más sencillo de autenticación y autorización. 

Las directivas describen por completo las experiencias de identidad del consumidor como el registro, el inicio de sesión y la edición de perfil. Las directivas se pueden definir en una interfaz de usuario administrativa. Se pueden ejecutar mediante un parámetro de consulta especial en solicitudes de autenticación de HTTP. 

Las directivas no son características estándares de OAuth 2.0 y OpenID Connect, por lo que debe tomar Hola tiempo toounderstand ellos. Para obtener más información, vea hello [Guía de referencia de directiva de Azure AD B2C](active-directory-b2c-reference-policies.md).

## Tokens
implementación de Azure AD B2C Hola de OAuth 2.0 y OpenID Connect hace uso masivo de tokens portadores, incluidos tokens de portador que se representan como tokens de web JSON (Jwt). Un token de portador es un token de seguridad ligero que concede Hola tooa de "portador" acceso al recurso protegido.

portador de Hello es cualquier entidad que puede presentar el token de Hola. Para que una parte pueda recibir un token de portador, es necesario que Azure AD la autentique previamente. Pero si Hola necesario no se toman medidas toosecure Hola símbolo (token) de transmisión y el almacenamiento, se puede interceptar y utilizado por una entidad no deseada.

Algunos tokens de seguridad tienen mecanismos integrados que impiden que partes no autorizadas puedan usarlos, pero los tokens de portador no disponen de este mecanismo. Deberán ser transportados en un canal seguro, como la seguridad de la capa de transporte (HTTPS). 

Si se transmite un token de portador fuera de un canal seguro, un usuario malintencionado puede usar un token de ataque de man-in-the-middle tooacquire hello y usar recursos de tooa protegido del acceso de toogain no autorizado. Hola mismos principios de seguridad que se aplican cuando se almacena tokens de portador o se almacena en caché para su uso posterior. Asegúrate siempre de que la aplicación transmite y almacena los tokens de portador de manera segura.

Para ver más consideraciones de seguridad relativas a los tokens de portador, consulte la [sección 5 de RFC 6750](http://tools.ietf.org/html/rfc6750).

Para obtener más información acerca de los tipos diferentes de hello de tokens que se usan en Azure AD B2C están disponibles en [Hola referencia del token de Azure AD](active-directory-b2c-reference-tokens.md).

## Protocolos
Cuando esté listo tooreview algunos ejemplos solicita, puede empezar con uno de los tutoriales de Hola. Cada uno de ellos corresponde tooa escenario de autenticación determinado. Si necesita ayuda para determinar qué flujo es adecuado para usted, visite [Hola tipos de aplicaciones puede crear mediante el uso de Azure AD B2C](active-directory-b2c-apps.md).

* [Creación de aplicaciones móviles nativas mediante OAuth 2.0](active-directory-b2c-reference-oauth-code.md)
* [Creación de aplicaciones web mediante OpenID Connect](active-directory-b2c-reference-oidc.md)
* [Crear aplicaciones de página con flujo implícito hello OAuth 2.0](active-directory-b2c-reference-spa.md)

