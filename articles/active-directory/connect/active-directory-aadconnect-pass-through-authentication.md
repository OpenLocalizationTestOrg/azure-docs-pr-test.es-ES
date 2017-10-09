---
title: "Azure AD Connect: Autenticación de paso a través | Microsoft Docs"
description: "En este artículo se describe la autenticación de paso a través de Azure Active Directory (Azure AD) y cómo permite inicios de sesión de Azure AD mediante la validación de las contraseñas de los usuarios en una instancia local de Active Directory."
services: active-directory
keywords: "qué es la autenticación de paso a través de Azure AD Connect, instalar Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a>Inicio de sesión del usuario con la autenticación de paso a través de Azure Active Directory

## <a name="what-is-azure-active-directory-pass-through-authentication"></a>¿Qué es la autenticación de paso a través de Azure Active Directory?

Autenticación de paso a través de Azure Active Directory (Azure AD) permite la toosign usuarios tooboth en local y aplicaciones basadas en la nube mediante Hola mismas contraseñas. Esta característica proporciona a los usuarios una mejor experiencia - uno menos tooremember de contraseña y reduce los costos del departamento de soporte técnico de TI ya que los usuarios son menos probable tooforget cómo toosign en. Cuando los usuarios inician sesión con Azure AD, esta característica valida sus contraseñas directamente con la instancia de Active Directory local.

Esta característica es una alternativa demasiado[sincronización de Hash de contraseña de Azure AD](active-directory-aadconnectsync-implement-password-synchronization.md), lo que proporciona Hola mismo beneficio de tooorganizations de autenticación de nube. Sin embargo, las directivas de seguridad y cumplimiento de ciertas organizaciones no permiten estas organizaciones las contraseñas de los usuarios de toosend, incluso en un formulario con algoritmo hash, fuera de sus límites internos. Este tipo de autenticación es la solución adecuada de hello estas organizaciones.

![Autenticación de paso a través de Azure AD](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

Puede combinar la autenticación de paso a través con hello [perfecta Single Sign-On](active-directory-aadconnect-sso.md) característica. Este modo, cuando los usuarios tienen acceso a las aplicaciones en sus equipos corporativos dentro de la red corporativa, no deben tootype en su toosign contraseñas en.

>[!IMPORTANT]
>La autenticación de paso a través de Azure AD se encuentra actualmente en versión preliminar.

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a>Principales ventajas del uso de la autenticación de paso a través de Azure AD

- *Mejor experiencia del usuario*
  - Los usuarios utilizan Hola mismo toosign contraseñas en local y las aplicaciones basadas en la nube.
  - Los usuarios dedican menos tiempo a hablar toohello soporte técnico de TI para resolver problemas relacionados con la contraseña.
  - Los usuarios pueden completar [administración de contraseñas de autoservicio](../active-directory-passwords-overview.md) tareas en la nube de Hola.
- *Toodeploy fácil & Administrar*
  - No se requieren complejas implementaciones locales ni la configuración de la red.
  - Necesita solo un toobe ligera agente había instalado de forma local.
  - Sin sobrecarga de administración. agente de Hello recibe automáticamente mejoras y correcciones de errores.
- *Protección*
  - Contraseñas locales nunca se almacenan en la nube de Hola en cualquier formato.
  - agente de Hello solo realiza conexiones salientes desde dentro de la red. Por lo tanto, no hay ningún agente de Hola de tooinstall de requisito en una red perimetral, también conocida como una red Perimetral.
  - Protege las cuentas de usuario al trabajar sin problemas con [directivas de acceso condicional de Azure AD](../active-directory-conditional-access-azure-portal.md), incluida Multi-Factor Authentication (MFA), y al [filtrar ataques de contraseña por fuerza bruta](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).
- *Alta disponibilidad*
  - Agentes adicionales se pueden instalar en varios local servidores tooprovide alta disponibilidad de las solicitudes de inicio de sesión.

## <a name="feature-highlights"></a>Características destacadas

- Admite el inicio de sesión de usuario en todas las aplicaciones basadas en explorador web y en las aplicaciones cliente de Microsoft Office que usan la [autenticación moderna](https://aka.ms/modernauthga).
- Nombres de usuario de inicio de sesión pueden ser cualquier nombre de usuario de hello local predeterminado (`userPrincipalName`) o de otro atributo configurado en Azure AD Connect (conocido como `Alternate ID`).
- característica de Hello funciona sin problemas con [acceso condicional](../active-directory-conditional-access.md) características como la autenticación multifactor (MFA) toohelp proteger a los usuarios.
- Se admiten entornos de varios bosques si hay relaciones de confianza de bosque entre los bosques de AD y si el enrutamiento de sufijos de nombre está configurado correctamente.
- Es una característica gratuita y no necesita ninguna edición de pagada de Azure AD toouse lo.
- Puede habilitarse a través de [Azure AD Connect](active-directory-aadconnect.md).
- Utiliza a un agente local ligera que escucha y responde las solicitudes de validación de toopassword.
- La instalación de varios agentes proporciona una alta disponibilidad de las solicitudes de inicio de sesión.
- Se [protege](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) ataques de contraseña en la nube de Hola por fuerza las cuentas local frente a ataques.

## <a name="next-steps"></a>Pasos siguientes

- [**Inicio rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md): desarrollo y ejecución de la autenticación de paso a través de Azure AD.
- [**Limitaciones actuales**](active-directory-aadconnect-pass-through-authentication-current-limitations.md): esta funcionalidad actualmente está en su versión preliminar. Obtenga información sobre los escenarios que se admiten y los que no.
- [**Profundización técnica**](active-directory-aadconnect-pass-through-authentication-how-it-works.md): descripción del funcionamiento de esta característica.
- [**Preguntas más frecuentes** ](active-directory-aadconnect-pass-through-authentication-faq.md) -responde toofrequently preguntas más frecuentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.
- [**SSO de conexión directa de Azure AD**](active-directory-aadconnect-sso.md): obtenga más información sobre esta característica complementaria.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.
