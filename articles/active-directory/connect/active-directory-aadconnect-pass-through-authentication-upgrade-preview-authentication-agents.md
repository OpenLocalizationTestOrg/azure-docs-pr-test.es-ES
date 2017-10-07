---
title: "Azure AD Connect: Autenticación de paso a través (actualización de la versión preliminar de los agentes de autenticación) | Microsoft Docs"
description: "Este artículo se describe cómo tooupgrade la configuración de autenticación de paso a través de Azure Active Directory (Azure AD)."
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
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 1695326b182278944e9f1584da72b18862b6ef27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a>Autenticación de paso a través de Azure Active Directory: actualización de la versión preliminar de los agentes de autenticación

## <a name="overview"></a>Información general

Este artículo está dirigido a los clientes que usan la Autenticación de paso a través de Azure AD en versión preliminar. Se Hola recientemente actualizada (y nueva) el software de agente de autenticación. Necesita too_manually_ actualización preview agentes de autenticación instalados en los servidores locales. Esta actualización manual requiere una única acción. Todas las actualizaciones futuras tooAuthentication agentes son automáticos. Hola motivos tooupgrade son los siguientes:

- las versiones preliminares de Hola de agentes de autenticación no recibirá ningún más seguridad o correcciones de errores.
-   las versiones preliminares de Hola de agentes de autenticación no se puede instalar en otros servidores, para lograr alta disponibilidad.

## <a name="check-versions-of-your-authentication-agents"></a>Comprobación de las versiones de los agentes de autenticación

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a>Paso 1: Comprobar si los agentes de autenticación están instalados

Siga estos pasos toocheck donde están instalados los agentes de autenticación:

1. Inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con credenciales de administrador Global de hello para el inquilino.
2. Seleccione **Azure Active Directory** en el panel de navegación izquierdo Hola.
3. Seleccione **Azure AD Connect**. 
4. Seleccione **Autenticación de paso a través**. Esta hoja enumera los servidores de Hola donde están instalados los agentes de autenticación.

![Centro de administración de Azure Active Directory: hoja de Autenticación de paso a través](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-hello-versions-of-your-authentication-agents"></a>Paso 2: Comprobar las versiones de Hola de los agentes de autenticación

versiones de hello toocheck de los agentes de autenticación, en cada servidor identificado en hello anterior paso, sigan estas instrucciones:

1. Vaya demasiado**el Panel de Control -> Programas -> programas y características** en el servidor local de Hola.
2. Si no hay una entrada para "**autenticación de agente de Microsoft Azure AD Connect**", no es necesario tootake ninguna acción en este servidor.
3. Si no hay una entrada para "**conector del Proxy de aplicación de Microsoft Azure AD**", versiones 1.5.132.0 o versiones anteriores, necesitará toomanually actualización en este servidor.

![Versión preliminar del agente de autenticación](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-toofollow-before-starting-hello-upgrade"></a>Prácticas recomendadas toofollow antes de iniciar la actualización de Hola

Antes de actualizar, asegúrese de que tiene Hola siguientes elementos en su lugar:

1. **Crear cuenta de administrador Global solo en la nube**: no realiza la actualización sin necesidad de un toouse de cuenta de administrador Global solo en la nube en situaciones de emergencia donde los agentes de autenticación de paso a través no funcionen correctamente. Información acerca de la [incorporación de una cuenta de administrador global que está solo en la nube](../active-directory-users-create-azure-portal.md). Este paso es esencial y se asegura de no quedar bloqueado fuera de su inquilino.
2.  **Asegurar la alta disponibilidad**: si no se ha completado previamente, instalar un segundo independiente tooprovide alta disponibilidad de agente de autenticación para solicitudes de inicio de sesión, uso de estas [instrucciones](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="upgrading-hello-authentication-agent-on-your-azure-ad-connect-server"></a>Actualizar Hola agente de autenticación en el servidor de Azure AD Connect

Necesita actualizar Azure AD Connect antes de actualizar Hola agente de autenticación en hello mismo servidor. Siga estos pasos tanto en el servidor principal como en el servidor provisional de Azure AD Connect:

1. **Actualizar Azure AD Connect**: siga este [artículo](./active-directory-aadconnect-upgrade-previous-version.md) y actualizar la versión de toohello más reciente AD Azure Connect.
2. **Desinstalar la versión de vista previa de Hola de hello Authentication Agent**: descargar [esta secuencia de comandos de PowerShell](https://aka.ms/rmpreviewagent) y ejecutar como administrador en el servidor de Hola.
3. **Descargar Hola la versión más reciente del agente de autenticación de hello (versiones 1.5.193.0 o una versión posterior)**: inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con credenciales de administrador Global de su inquilino. Seleccione **Azure Active Directory -> Azure AD Connect -> Autenticación de paso a través -> Descargar agente**. Acepto los términos de hello del servicio y descargar Hola la versión más reciente del programa Hola a agente de autenticación.
4. **Instale Hola la versión más reciente del agente de autenticación de Hola**: Hola de ejecución ejecutable descargado en el paso 3. Proporcione las credenciales de administrador global de su inquilino cuando se le solicite.
5. **Compruebe que se ha instalado esa versión más reciente de hello**: como se mostró anteriormente, vaya demasiado**el Panel de Control -> Programas -> programas y características** y compruebe que hay una entrada para "**Microsoft Azure AD Connect Agente de autenticación**".

>[!NOTE]
>Si activa la hoja de la autenticación de paso a través de hello en hello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) después de completar los pasos anteriores de hello, verá dos entradas de agente de autenticación por servidor: una entrada que muestra hello Agente de autenticación como **Active** y otro como Hola **inactivo**. Se _espera_ que esto sea así. Hola **inactivo** entrada se quita automáticamente después de unos días.

## <a name="upgrading-hello-authentication-agent-on-other-servers"></a>Actualizar Hola agente de autenticación en otros servidores

Siga estos tooupgrade pasos agentes de autenticación en otros servidores (donde no se instala Azure AD Connect):

1. **Desinstalar la versión de vista previa de Hola de hello Authentication Agent**: descargar [esta secuencia de comandos de PowerShell](https://aka.ms/rmpreviewagent) y ejecutar como administrador en el servidor de Hola.
2. **Descargar Hola la versión más reciente del agente de autenticación de hello (versiones 1.5.193.0 o una versión posterior)**: inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con credenciales de administrador Global de su inquilino. Seleccione **Azure Active Directory -> Azure AD Connect -> Autenticación de paso a través -> Descargar agente**. Acepto los términos de hello del servicio y descargar la versión más reciente de Hola.
3. **Instale Hola la versión más reciente del agente de autenticación de Hola**: Hola de ejecución ejecutable descargado en el paso 2. Proporcione las credenciales de administrador global de su inquilino cuando se le solicite.
4. **Compruebe que se ha instalado esa versión más reciente de hello**: como se mostró anteriormente, vaya demasiado**el Panel de Control -> Programas -> programas y características** y compruebe que hay una entrada denominada **Microsoft Azure AD Connect Agente de autenticación**.

>[!NOTE]
>Si activa la hoja de la autenticación de paso a través de hello en hello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) después de completar los pasos anteriores de hello, verá dos entradas de agente de autenticación por servidor: una entrada que muestra hello Agente de autenticación como **Active** y otro como Hola **inactivo**. Se _espera_ que esto sea así. Hola **inactivo** entrada se quita automáticamente después de unos días.

## <a name="next-steps"></a>Pasos siguientes
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.
