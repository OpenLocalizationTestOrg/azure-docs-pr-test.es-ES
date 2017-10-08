---
title: "Azure AD Connect: inicio de sesión único de conexión directa | Microsoft Docs"
description: "Este tema describe Azure Active Directory (Azure AD) sin problemas Single Sign-On y cómo permite tooprovide true inicio de sesión único para los usuarios de escritorio corporativos dentro de la red corporativa."
services: active-directory
keywords: "qué es Azure AD Connect, instalar Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a>Inicio de sesión único de conexión directa de Azure Active Directory

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>¿Qué es el inicio de sesión único de conexión directa de Azure Active Directory?

Azure Active Directory sin problemas Single Sign-On (SSO sin problemas de Azure AD), inicia automáticamente los usuarios cuando se encuentran en su red corporativa de dispositivos corporativos tooyour conectado. Cuando se habilita, los usuarios no necesita tootype en su toosign contraseñas en tooAzure AD y, por lo general, escriba incluso en sus nombres de usuario. Esta característica proporciona a los usuarios un acceso fácil tooyour basada en la nube aplicaciones sin necesidad de todos los componentes locales adicionales.

SSO sin problemas puede combinarse con cualquier hello [sincronización de Hash de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) o [autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md) métodos de inicio de sesión.

![Inicio de sesión único de conexión directa](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
>SSO de conexión directa está actualmente en versión preliminar. Esta característica está _no_ aplicable tooActive Directory Federation Services (ADFS).

## <a name="key-benefits"></a>Ventajas principales

- *Mejor experiencia del usuario*
  - Los usuarios inician sesión automáticamente tanto en las aplicaciones basadas en la nube como en las locales.
  - Los usuarios no tengan tooenter sus contraseñas varias veces.
- *Toodeploy fácil & Administrar*
  - No necesitan componentes adicionales local toomake este trabajo.
  - Funciona con cualquier método de autenticación en la nube, ya sea [sincronización de hash de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) o [autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md).
  - Se pueden poner toosome o todos los usuarios mediante la directiva de grupo.
  - Registrar dispositivos no sean Windows 10 con Azure AD sin necesidad de Hola de cualquier infraestructura de AD FS. Esta funcionalidad debe toouse versión 2.1 o posterior de hello [cliente del área de trabajo](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="feature-highlights"></a>Características destacadas

- Nombre de inicio de sesión de usuario puede ser cualquier nombre de usuario de hello local predeterminado (`userPrincipalName`) o de otro atributo configurado en Azure AD Connect (`Alternate ID`). Ambos usan trabajo de casos porque SSO sin problemas utiliza Hola `securityIdentifier` notificación en toolook de vale de Kerberos de hello seguridad del objeto de usuario correspondiente de hello en Azure AD.
- SSO de conexión directa es una característica oportunista. Si se produce un error por algún motivo, experiencia de inicio de sesión del usuario de hello vuelve comportamiento normal tooits: es decir, Hola usuario necesita tooenter su contraseña en la página de inicio de sesión de Hola.
- Si una aplicación envía una `domain_hint` (OpenID Connect) o `whr` parámetro (SAML) - identificar su inquilino, o `login_hint` parámetro - identificación de usuario de hello, en su solicitud de inicio de sesión en Azure AD, los usuarios inician sesión automáticamente sin ellos especificar nombres de usuario o contraseñas.
- Puede habilitarse a través de Azure AD Connect.
- Es una característica gratuita y no necesita ninguna edición de pagada de Azure AD toouse lo.
- Se admite en clientes basados en el explorador web y en clientes de Office que admiten la [autenticación moderna](https://aka.ms/modernauthga) en plataformas con la funcionalidad de autenticación de Kerberos:

| SO\Explorador |Internet Explorer|perimetral|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|Sí|No|Sí|Sí\*|N/D
|Windows 8.1|Sí|N/D|Sí|Sí\*|N/D
|Windows 8|Sí|N/D|Sí|Sí\*|N/D
|Windows 7|Sí|N/D|Sí|Sí\*|N/D
|Mac OS X|N/D|N/D|Sí\*|Sí\*|Sí\*

\*Requiere [configuración adicional](active-directory-aadconnect-sso-quick-start.md#browser-considerations)

>[!IMPORTANT]
>Se recientemente revierten compatibilidad con borde tooinvestigate problemas detectados por el cliente.

>[!NOTE]
>Para Windows 10, recomendación de hello es toouse [Azure AD Join](../active-directory-azureadjoin-overview.md) para hello único inicio de sesión en una experiencia óptima con Azure AD.

## <a name="next-steps"></a>Pasos siguientes

- [**Inicio rápido**](active-directory-aadconnect-sso-quick-start.md): desarrollo y ejecución de SSO de conexión directa de Azure AD.
- [**Profundización técnica**](active-directory-aadconnect-sso-how-it-works.md): descripción del funcionamiento de esta característica.
- [**Preguntas más frecuentes** ](active-directory-aadconnect-sso-faq.md) -responde toofrequently preguntas más frecuentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para la tramitación de solicitudes de nuevas características.
