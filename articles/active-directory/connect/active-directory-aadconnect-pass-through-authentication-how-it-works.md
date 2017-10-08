---
title: "Azure AD Connect: funcionamiento de la autenticación de paso a través | Microsoft Docs"
description: "En este artículo se describe el funcionamiento de la autenticación de paso a través de Azure Active Directory."
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
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Autenticación de paso a través de Azure Active Directory: información técnica detallada

>[!IMPORTANT]
>La autenticación de paso a través de Azure AD se encuentra actualmente en versión preliminar. 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Funcionamiento de la autenticación de paso a través de Azure Active Directory

Cuando un usuario intenta toosign en una aplicación protegida por Azure Active Directory (Azure AD) y si está habilitada la autenticación de paso a través en el inquilino de hello, Hola se producen los pasos siguientes:

1. usuario de Hello intente tooaccess una aplicación (por ejemplo, Hola Outlook Web App - https://outlook.office365.com/owa/).
2. Si el usuario de hello no ha iniciado ya sesión, usuario de hello es página de inicio de sesión de Azure AD de toohello redirigida.
3. usuario de Hello entra en su nombre de usuario y contraseña en la página de inicio de sesión de Azure AD de Hola y hace clic en el botón de "Iniciar sesión" Hola.
4. Azure AD, al recibir la solicitud de inicio de sesión hello, coloca Hola nombre de usuario y contraseña (cifrada con una clave pública) en una cola.
5. Un agente de autenticación de paso a través de local hace que una cola de toohello llamada saliente y recupera el nombre de usuario de hello y una contraseña cifrada.
6. agente de Hello descifra contraseña Hola usando su clave privada.
7. agente de Hello, a continuación, valida Hola username y password con Active Directory mediante la API estándar de Windows (un toowhat mecanismo similar es utilizado por los servicios de federación de Active Directory). Hello nombre de usuario puede ser cualquier nombre de usuario de hello local predeterminado (normalmente `userPrincipalName`) o de otro atributo configurado en Azure AD Connect (conocido como `Alternate ID`).
8. Hola controlador de dominio de Active Directory (DC) local, a continuación, evalúa la solicitud de Hola y devuelve Hola respuesta adecuada (correcto, error, contraseña expirada o usuario bloqueado) toohello agente.
9. agente de Hello, a su vez, devuelve este tooAzure de espera de respuesta AD.
10. Azure AD se evalúa como respuesta de Hola y responde toohello usuario según corresponda; por ejemplo, inicia el usuario de hello inmediatamente o las solicitudes para la autenticación multifactor (MFA).
11. Si el inicio de sesión de usuario de hello es correcta, usuario de Hola es tooaccess capaz de aplicación de hello.

Hello siguiente diagrama muestra todos los componentes de Hola y pasos Hola.

![Autenticación de paso a través](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>Pasos siguientes
- [**Limitaciones actuales**](active-directory-aadconnect-pass-through-authentication-current-limitations.md): esta funcionalidad actualmente está en su versión preliminar. Obtenga información acerca de qué escenarios se admiten y cuáles no.
- [**Inicio rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md): desarrollo y ejecución de la autenticación de paso a través de Azure AD.
- [**Preguntas más frecuentes** ](active-directory-aadconnect-pass-through-authentication-faq.md) -responde toofrequently preguntas más frecuentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.
- [**SSO de conexión directa de Azure AD**](active-directory-aadconnect-sso.md): obtenga más información sobre esta característica complementaria.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.
