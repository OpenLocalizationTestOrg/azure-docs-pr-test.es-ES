---
title: "Autenticación de paso a través de Azure AD: limitaciones actuales | Microsoft Docs"
description: "Este artículo describen las limitaciones actuales de Hola de autenticación de paso a través de Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Autenticación de paso a través de Azure AD Connect, instalación de Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Autenticación de paso a través de Azure Active Directory: limitaciones actuales

>[!IMPORTANT]
>La autenticación de paso a través de Azure AD se encuentra actualmente en versión preliminar. Es una característica gratuita y no necesita ninguna edición de pagada de Azure AD toouse lo. Autenticación de paso a través solo está disponible en la instancia de todo el mundo Hola de Azure AD y no se encuentra en [Alemania Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) y [nube de Microsoft Azure Government](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Escenarios admitidos

Hola los escenarios siguientes se admite por completo durante la vista previa:

- Inicios de sesión de usuario en todas las aplicaciones basadas en explorador web.
- Inicios de sesión de usuario en las aplicaciones cliente de Office 365 que admitan la [autenticación moderna](https://aka.ms/modernauthga).
- Azure AD Join para dispositivos con Windows 10.
- Compatibilidad con Exchange ActiveSync.

## <a name="unsupported-scenarios"></a>Escenarios no admitidos

Hello siguientes escenarios son _no_ admiten durante la vista previa:

- Inicios de sesión de usuarios en aplicaciones cliente de Office heredadas (Office 2013 o versiones anteriores). Las organizaciones están tooswitch recomienda toomodern autenticación, si es posible. La autenticación moderna permite la compatibilidad de la autenticación de paso a través, pero también le ayuda a proteger sus cuentas de usuario mediante características de [acceso condicional](../active-directory-conditional-access.md) como Multi-Factor Authentication (MFA).
- Inicios de sesión de usuarios en aplicaciones cliente de Skype Empresarial, incluido Skype Empresarial 2016.
- Inicios de sesión de usuario en PowerShell v1.0. Se recomienda que use PowerShell v2.0 en su lugar.

>[!IMPORTANT]
>Como solución alternativa para escenarios no admitidos, habilitar la sincronización de Hash de contraseña en hello [características opcionales](active-directory-aadconnect-get-started-custom.md#optional-features) página del Asistente para conectar de hello Azure AD. Sincronización de Hash de contraseñas actúa como una acción de reserva para hello anteriores escenarios _sólo_ (y _no_ como genérico tooPass mediante autenticación de reserva). Si no necesita estos escenarios, desactive la sincronización hash de contraseñas.

## <a name="next-steps"></a>Pasos siguientes
- [**Inicio rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md): desarrollo y ejecución de la autenticación de paso a través de Azure AD.
- [**Profundización técnica**](active-directory-aadconnect-pass-through-authentication-how-it-works.md): descripción del funcionamiento de esta característica.
- [**Preguntas más frecuentes** ](active-directory-aadconnect-pass-through-authentication-faq.md) -responde toofrequently preguntas más frecuentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.
- [**SSO de conexión directa de Azure AD**](active-directory-aadconnect-sso.md): obtenga más información sobre esta característica complementaria.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.
