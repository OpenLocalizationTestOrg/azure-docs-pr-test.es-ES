---
title: "Azure Active Directory B2C: configuración de tokens, sesión e inicio de sesión único | Microsoft Docs"
description: "Configuración de token, sesión e inicio de sesión único en Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a>Azure Active Directory B2C: configuración de tokens, sesión e inicio de sesión único
Esta característica ofrece un control más preciso, [por directivas](active-directory-b2c-reference-policies.md), de:

1. La vigencia de los tokens de seguridad emitidos por Azure Active Directory (Azure AD) B2C.
2. La duración de las sesiones de aplicación web administradas por Azure AD B2C.
3. Formatos de notificaciones importantes hello en tokens de seguridad emitidos por Azure AD B2C.
4. El comportamiento de inicio de sesión único (SSO) entre varias aplicaciones y directivas en el inquilino B2C.

Puede utilizar esta característica en el inquilino B2C como sigue:

1. Siga estos pasos demasiado[navegue hoja de características toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) en hello portal de Azure.
2. Haga clic en **Directivas de inicio de sesión**. *Nota: Esta característica se puede usar en cualquier tipo de directiva, no solo en **directivas de inicio de sesión***.
3. Abra una directiva haciendo clic en ella. Por ejemplo, haga clic en **B2C_1_SiIn**.
4. Haga clic en **editar** princip Hola de hoja de Hola.
5. Haga clic en **Token, session & single sign-on config** (Configuración de tokens, sesión e inicio de sesión único).
6. Realice los cambios deseados. Obtenga información acerca de las propiedades disponibles en las secciones siguientes.
7. Haga clic en **Aceptar**.
8. Haga clic en **guardar** en la parte superior de Hola de hoja de Hola.

## <a name="token-lifetimes-configuration"></a>Configuración de la vigencia de los tokens
B2C de Azure AD admite hello [protocolo de autorización de OAuth 2.0](active-directory-b2c-reference-protocols.md) para habilitar el acceso seguro tooprotected recursos. tooimplement esta compatibilidad, Azure AD B2C emite varios [tokens de seguridad](active-directory-b2c-reference-tokens.md). Se trata de propiedades de Hola que puede utilizar toomanage duraciones de tokens de seguridad emitidos por Azure AD B2C:

* **Duración (minutos) de token de acceso & identificador**: duración de Hola de hello OAuth 2.0 portador token toogain usa acceso tooa al recurso protegido. Azure AD B2C solo emite tokens de identificador en este momento. Este valor se aplicaría tooaccess tokens así, cuando se agrega compatibilidad para ellos.
  * Valor predeterminado: 60 minutos.
  * Mínimo (incluido) = 5 minutos.
  * Máximo (incluido) = 1440 minutos.
* **Duración del token de actualización (días)**: Hola período máximo de tiempo antes de que un token de actualización puede ser tooacquire usa un nuevo acceso o identificador de token (y opcionalmente, un nuevo token de actualización, si la aplicación se hubiesen garantizada hello `offline_access` ámbito).
  * Valor predeterminado = 14 días.
  * Mínimo (incluido) = 1 día.
  * Máximo (incluido) = 90 días.
* **Actualizar token duración de ventana deslizante (días)**: después de este usuario de tiempo transcurrido hello toore forzada-autenticar, independientemente del período de validez de Hola de token de actualización más reciente de hello adquirido por la aplicación hello. Solo pueden concederse si se ha establecido el modificador de hello demasiado**Bounded**. Necesita toobe mayor que o igual toohello **duración del token de actualización (días)** valor. Si se ha establecido el modificador de hello demasiado**Unbounded**, no puede proporcionar un valor específico.
  * Valor predeterminado = 90 días.
  * Mínimo (incluido) = 1 día.
  * Máximo (incluido) = 365 días.

Aquí puede ver un par de casos de uso que puede habilitar mediante el uso de estas propiedades:

* Permitir que un toostay de usuario que ha iniciado sesión en una aplicación móvil de forma indefinida, mientras que está continuamente activo en la aplicación hello. Para ello, establecer hello **duración de ventana deslizante token actualización (días)** cambiar demasiado**Unbounded** en la directiva de inicio de sesión.
* Cumplir los requisitos de seguridad y cumplimiento de la industria al establecer vigencias de token de acceso adecuado de Hola.

    > [!NOTE]
    > Estas opciones no están disponibles para las directivas de restablecimiento de contraseña.
    > 
    > 

## <a name="token-compatibility-settings"></a>Configuración de compatibilidad de tokens
Hemos realizado formato cambios tooimportant notificaciones en tokens de seguridad emitidos por Azure AD B2C. Esto ha sido realiza tooimprove la compatibilidad del protocolo estándar y para mejorar la interoperabilidad con las bibliotecas de identidad de otro fabricante. Sin embargo, tooavoid separación de las aplicaciones existentes, hemos creado Hola después de los clientes de tooallow propiedades tooopt de según sea necesario:

* **Notificación de emisor (iss)**: Esto identifica el inquilino de Azure AD B2C Hola que emitió el token de Hola.
  * `https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: Esto es el valor predeterminado de Hola.
  * `https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: Este valor incluye identificadores de inquilino de hello B2C y directiva de hello usada en la solicitud de token de Hola. Si su aplicación o biblioteca necesita Azure AD B2C toobe compatible con hello [especificación OpenID Connect 1.0 de detección](http://openid.net/specs/openid-connect-discovery-1_0.html), use este valor.
* **Notificación de asunto (sub)**: Esto identifica la entidad de hello, es decir, usuario de hello, para qué hello token valida información.
  * **ObjectID**: se trata de valor predeterminado de Hola. Rellena Hola Id. de objeto de usuario de hello en el directorio de hello en hello `sub` de notificación en el token de Hola.
  * **No admite**: sólo se proporciona por compatibilidad con versiones anteriores, y se recomienda cambiar demasiado**ObjectID** tan pronto como pueda.
* **Que representa el Id. de directiva de notificación**: Esto identifica el tipo de notificación de hello en qué Hola se rellena el Id. de directiva que se usa en la solicitud de token de Hola.
  * **TFTP**: se trata de valor predeterminado de Hola.
  * **Acr**: sólo se proporciona por compatibilidad con versiones anteriores, y se recomienda cambiar demasiado`tfp` tan pronto como pueda.

## <a name="session-behavior"></a>Comportamiento de la sesión
B2C de Azure AD admite hello [protocolo de autenticación OpenID Connect](active-directory-b2c-reference-oidc.md) para permitir que las aplicaciones de tooweb de inicio de sesión segura. Se trata de propiedades de Hola que puede utilizar sesiones de aplicación web de toomanage:

* **Aplicación Web de duración de la sesión (minutos)**: duración de Hola de cookie de sesión de Azure AD B2C almacenada en el explorador del usuario de hello tras una autenticación correcta.
  * Valor predeterminado: 1440 minutos.
  * Mínimo (incluido) = 15 minutos.
  * Máximo (incluido) = 1440 minutos.
* **Tiempo de espera de sesión de aplicación de Web**: si este modificador se establece demasiado**absoluta**, usuario de hello es forzada toore-autenticar después Hola período de tiempo especificado por **aplicación Web de duración de la sesión (minutos)** transcurre. Si este modificador se establece demasiado**graduales** (hello la configuración predeterminada), usuario de Hola permanece con sesión iniciada como usuario de hello está continuamente activo en la aplicación web.

Aquí puede ver un par de casos de uso que puede habilitar mediante el uso de estas propiedades:

* Cumplir los requisitos de seguridad y cumplimiento de la industria mediante el establecimiento de la sesión de la aplicación web adecuada Hola duraciones.
* Obligación de volver a autenticar después de un período de tiempo establecido durante la interacción del usuario con una zona de alta seguridad de la aplicación web. 

    > [!NOTE]
    > Estas opciones no están disponibles para las directivas de restablecimiento de contraseña.
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a>Configuración de inicio de sesión único (SSO)
Si tiene varias aplicaciones y directivas en el inquilino B2C, puede administrar las interacciones del usuario a través de ellos con hello **configuración de inicio de sesión único** propiedad. Puede establecer Hola propiedad tooone de hello después de configuración:

* **Inquilino**: ésta es configuración predeterminada de Hola. Con esta configuración permite que varias aplicaciones y directivas en el inquilino B2C tooshare Hola misma sesión de usuario. Por ejemplo, una vez que un usuario inicia sesión en una aplicación llamada Contoso Shopping, puede también iniciar sesión perfectamente en otra llamada Contoso Pharmacy simplemente con acceder a ella.
* **Aplicación**: Esto permite toomaintain una sesión de usuario exclusivamente para una aplicación, independientemente de otras aplicaciones. Por ejemplo, si desea toosign de usuario de hello en tooContoso farmacia (con hello mismas credenciales), incluso si ya ha iniciado sesión en Contoso la compra, otra aplicación en hello mismo inquilino B2C. 
* **Directiva**: Esto permite toomaintain una sesión de usuario exclusivamente para una directiva, independiente de las aplicaciones de hello usarlo. Por ejemplo, si el usuario Hola ya ha iniciado sesión y completar un paso de multi factor authentication (MFA), que puede indicarse partes de toohigher relacionadas con la seguridad de acceso de varias aplicaciones como Hola sesión vinculada toohello directiva no expire.
* **Deshabilitado**: Esto fuerza hello toorun de usuario a través de viaje de usuario completo de hello en cada ejecución de la directiva de Hola. Por ejemplo, esto le permitirá toosign varios de los usuarios de aplicación de tooyour (en un escenario de escritorio compartido) incluso mientras un usuario permanece con sesión iniciada durante el tiempo completo de Hola.

    > [!NOTE]
    > Estas opciones no están disponibles para las directivas de restablecimiento de contraseña.
    > 
    > 

