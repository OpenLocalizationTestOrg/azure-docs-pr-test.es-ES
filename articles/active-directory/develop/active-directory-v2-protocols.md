---
title: "aaaLearn acerca de los protocolos de autorización de hello compatibles con Azure AD v2.0 | Documentos de Microsoft"
description: "Tooprotocols de guía que admite el punto de conexión de hello Azure AD v2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f90511b1880ff223f725c1f79df9f79bddccc7bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Protocolos de v2.0: OAuth 2.0 y OpenID Connect
el punto de conexión de Hello v2.0 puede usar Azure AD para identidad-as-a-service con protocolos estándar del sector, OpenID Connect y OAuth 2.0.  Mientras el servicio de hello es compatible con los estándares, puede haber diferencias sutiles entre las dos implementaciones de estos protocolos.  información de Hello aquí será útil si decide toowrite el código mediante el envío directo & controlar las solicitudes HTTP o use un 3rd entidad Abrir biblioteca de origen, en lugar de mediante una de nuestras bibliotecas de código abierto.
<!-- TODO: Need link toolibraries above -->

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión de hello v2.0.  toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
>
>

## Hola conceptos básicos
En casi todos los flujos de OAuth y OpenID Connect, hay cuatro partes en exchange hello:

![Funciones de OAuth 2.0](../../media/active-directory-v2-flows/protocols_roles.png)

* Hola **servidor de autorización** es el punto de conexión de hello v2.0.  Es responsable de garantizar la identidad del usuario de Hola, conceder y revocar el acceso tooresources y emitir tokens.  También se denomina es proveedor de identidades de hello: segura controla nada toodo con del usuario de hello información acceso y sus relaciones de confianza de hello entre entidades en un flujo.
* Hola **propietario del recurso** es normalmente por el usuario final de Hola.  Es parte de Hola que posee datos hello y tiene Hola power tooallow terceros tooaccess esos datos o recurso.
* Hola **cliente OAuth** es la aplicación, identificada por su identificador de aplicación.  Normalmente es parte de Hola que por el usuario final de hello interactúa con, y solicita tokens Hola servidor de autorización.  cliente de Hello debe concederse permiso tooaccess Hola recursos por el propietario del recurso de Hola.
* Hola **servidor de recursos** es donde residen el recurso de Hola o datos.  Se confía Hola servidor de autorización toosecurely autenticar y autorizar Hola cliente OAuth y usa portador tooensure access_tokens que tienen acceso a recursos de tooa puede concederse.

## Registro de aplicaciones
Cada aplicación que utiliza el punto de conexión de hello v2.0 necesitará toobe registrado en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) para que puedan interactuar con OAuth u OpenID Connect.  proceso de registro de aplicación Hola se recopile y asignar unos valores tooyour aplicación:

* Un **Id. de aplicación** que identifica de forma única su aplicación
* A **URI de redireccionamiento** o **identificador de paquete** que pueden ser utilizados toodirect respuestas tooyour atrás aplicación
* Algunos otros valores específicos de cada escenario.

Para obtener más detalles, obtenga información acerca de cómo demasiado[registrar una aplicación](active-directory-v2-app-registration.md).

## Puntos de conexión
Una vez registrado, aplicación hello se comunica con Azure AD mediante el envío de solicitudes toohello v2.0 extremo:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Hola donde `{tenant}` puede tomar uno de cuatro valores diferentes:

| Valor | Descripción |
| --- | --- |
| `common` |Permite a los usuarios con cuentas Microsoft personales y cuentas de trabajo o escuela de toosign de Azure Active Directory en la aplicación hello. |
| `organizations` |Permite a solo los usuarios con cuentas de trabajo o escuela de toosign de Azure Active Directory en la aplicación hello. |
| `consumers` |Permite a solo los usuarios con personal toosign de cuentas de (MSA) de Microsoft en la aplicación hello. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` o `contoso.onmicrosoft.com` |Permite a solo los usuarios con cuentas de trabajo o escuela de un determinado toosign de inquilino de Azure Active Directory en la aplicación hello.  Nombre de dominio descriptivo de Hola Hola inquilino de Azure AD, o bien puede usarse el identificador guid del inquilino de Hola. |

Para obtener más información acerca de cómo toointeract con estos puntos de conexión, elija un tipo de aplicación determinada a continuación.

## Tokens
implementación de la versión 2.0 de Hola de OAuth 2.0 y OpenID Connect realizar un amplio uso de tokens de portador, incluidos los tokens portadores representados como Jwt. Un token de portador es un token de seguridad ligero que concede Hola tooa de "portador" acceso al recurso protegido. En este sentido, Hola "portador" es cualquier persona que puede presentar el token de Hola. Aunque una entidad debe autenticarse primero con el token de acceso de Azure AD tooreceive hello, si es necesario de hello no se toman medidas toosecure Hola símbolo (token) de transmisión y el almacenamiento, puede interceptar y utilizado por una entidad no deseada. Mientras que algunos tokens de seguridad disponen de un mecanismo integrado para evitar ser usados por partes no autorizadas, los tokens portadores no tienen este mecanismo y deben transportarse en un canal seguro como, por ejemplo, la seguridad de la capa de transporte (HTTPS). Si se transmite un token de portador en hello claro, un ataque de intermedio de hello man en puede usarse en un token de usuario malintencionado tooacquire hello y usarlo para un recurso de tooa protegido del acceso no autorizado. Hola mismos principios de seguridad que se aplican al almacenamiento o almacenamiento en caché de tokens portadores para su uso posterior. Asegúrese siempre de que la aplicación transmite y almacena los tokens de portador de manera segura. Para otras consideraciones sobre la seguridad de los tokens portadores, consulte la [Sección 5 de RFC 6750](http://tools.ietf.org/html/rfc6750).

Obtener más detalles de diferentes tipos de tokens que se usan en el punto de conexión de hello v2.0 está disponible en [Hola v2.0 referencia del token de punto de conexión](active-directory-v2-tokens.md).

## Protocolos
Si está listo toosee solicita algunos ejemplos, empezar a trabajar con uno de Hola por debajo de los tutoriales.  Cada uno de ellos corresponde tooa escenario de autenticación determinado.  Si necesita ayuda para determinar cuál es el flujo de derecho de Hola para usted, consulte [Hola tipos de aplicaciones puede crear con hello v2.0](active-directory-v2-flows.md).

* [Creación de aplicaciones móviles y nativas con OAuth 2.0](active-directory-v2-protocols-oauth-code.md)
* [Creación de aplicaciones web con OpenID Connect](active-directory-v2-protocols-oidc.md)
* [Compilar aplicaciones de página única con hello flujo implícito de OAuth 2.0](active-directory-v2-protocols-implicit.md)
* [Compilar demonios o procesos del lado servidor con hello flujo de credenciales de cliente de OAuth 2.0](active-directory-v2-protocols-oauth-client-creds.md)
* [Obtener tokens en una API Web con hello OAuth 2.0 en nombre de flujo](active-directory-v2-protocols-oauth-on-behalf-of.md)
