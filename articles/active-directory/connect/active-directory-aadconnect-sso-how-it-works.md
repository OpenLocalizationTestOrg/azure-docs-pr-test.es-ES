---
title: "Azure AD Connect: funcionamiento del inicio de sesión único de conexión directa | Microsoft Docs"
description: "Este artículo describe cómo funciona la característica de Azure Active Directory sin problemas Single Sign-On Hola."
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a>Inicio de sesión único de conexión directa de Azure Active Directory: información técnica detallada

Este artículo proporciona detalles técnicos en cómo funciona la característica de Azure Active Directory sin problemas Single Sign-On (SSO sin problemas) Hola.

>[!IMPORTANT]
>característica de SSO sin problemas de Hello está actualmente en vista previa.

## <a name="how-does-seamless-sso-work"></a>¿Cómo funciona SSO de conexión directa?

En esta sección tiene tooit de dos partes:
1. programa de instalación de Hola de característica de hello SSO sin problemas.
2. Funcionamiento de una transacción de inicio de sesión de usuario único con SSO de conexión directa.

### <a name="how-does-set-up-work"></a>¿Cómo funciona la configuración?

SSO de conexión directa se habilita a través de Azure AD Connect tal como se muestra [aquí](active-directory-aadconnect-sso-quick-start.md). Al habilitar la característica de hello, se produce Hola pasos:
- Una cuenta de equipo denominada `AZUREADSSOACCT` (que representa a Azure AD) se crea en la instancia local de Active Directory (AD).
- clave de descifrado de Kerberos de la cuenta de equipo de Hola se comparte de forma segura con Azure AD.
- Además, los nombres de entidad de seguridad de servicio (SPN) dos de Kerberos se crean toorepresent dos direcciones URL que se usan durante el inicio de sesión en Azure AD.

>[!NOTE]
> cuenta de equipo de Hola y Hola SPN de Kerberos se crean en cada bosque de AD sincronizar tooAzure AD (mediante Azure AD Connect) y para cuyos usuarios desea SSO sin problemas. Mover hello `AZUREADSSOACCT` tooan de cuenta de equipo unidad organizativa (OU) donde otras cuentas de equipo son tooensure almacenado que se administran en Hola misma manera y no se elimina.

>[!IMPORTANT]
>Es muy recomendable que se [clave de descifrado de hello Kerberos se sustituyen](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) de hello `AZUREADSSOACCT` cuenta de equipo al menos cada 30 días.

### <a name="how-does-sign-in-with-seamless-sso-work"></a>¿Cómo funciona el inicio de sesión con SSO de conexión directa?

Una vez completada la instalación de hello, SSO sin problemas funciona Hola mismo modo que con cualquier otra sesión que usa autenticación integrada de Windows (IWA). flujo de Hello es como sigue:

1. usuario de Hello intente tooaccess una aplicación (por ejemplo, Hola Outlook Web App - https://outlook.office365.com/owa/) desde un dispositivo corporativo Unidos a un dominio dentro de su red corporativa.
2. Si el usuario de hello no ha iniciado ya sesión, usuario de hello es página de inicio de sesión de Azure AD de toohello redirigida.

  >[!NOTE]
  >Si una solicitud de inicio de sesión hello Azure AD incluye un `domain_hint` (identificar su inquilino: por ejemplo, contoso.onmicrosoft.com) o `login_hint` (identificación de usuario de hello - por ejemplo, user@contoso.onmicrosoft.com o user@contoso.com) se omite el parámetro y, a continuación, paso 2.

3. tipos de usuario de Hello en su nombre de usuario en la página de inicio de sesión de hello Azure AD.
4. Usar JavaScript en segundo plano de hello, Azure AD desafíos de explorador hello, a través de una respuesta 401 no autorizado, tooprovide un vale de Kerberos.
5. Explorador de Hello, a su vez, solicita un vale desde Active Directory para hello `AZUREADSSOACCT` cuenta de equipo (representado por Azure AD).
6. Active Directory localiza la cuenta de equipo de Hola y devuelve un explorador de toohello de vale de Kerberos cifrado con el secreto de la cuenta de equipo de Hola.
7. Explorador de Hello reenvía el vale de Kerberos de hello obtenido de Active Directory tooAzure AD (en uno de hello [las direcciones URL de Azure AD agregan previamente la configuración de zona de Intranet del explorador toohello](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).
8. Azure AD descifra Hola vale de Kerberos, que incluye Hola identidad de hello usuario inició sesión en el dispositivo corporativo de hello, utilizaba anteriormente Hola clave compartida.
9. Después de la evaluación, Azure AD devuelve una aplicación de símbolo (token) toohello atrás o solicita Hola usuario tooperform pruebas adicionales, como la autenticación multifactor.
10. Si el inicio de sesión de usuario de hello es correcta, usuario de Hola es tooaccess capaz de aplicación de hello.

Hello siguiente diagrama muestra todos los componentes de Hola y pasos Hola.

![Inicio de sesión único de conexión directa](./media/active-directory-aadconnect-sso/sso2.png)

SSO sin problemas es oportunista, lo que significa que si se produce un error, experiencia de inicio de sesión de hello vuelve comportamiento normal tooits: es decir, Hola su toosign de contraseña en el usuario tiene tooenter.

## <a name="next-steps"></a>Pasos siguientes

- [**Inicio rápido**](active-directory-aadconnect-sso-quick-start.md): desarrollo y ejecución de SSO de conexión directa de Azure AD.
- [**Preguntas más frecuentes** ](active-directory-aadconnect-sso-faq.md) -responde toofrequently preguntas más frecuentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para la tramitación de solicitudes de nuevas características.
