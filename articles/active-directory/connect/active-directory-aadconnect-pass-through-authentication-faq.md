---
title: "Autenticación de paso a través de Azure AD Connect: Preguntas más frecuentes | Microsoft Docs"
description: "Respuestas toofrequently preguntas más frecuentes sobre la autenticación de paso a través de Azure Active Directory."
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
ms.openlocfilehash: 550e2599177682f8ea971a05485dd5ac12b9b072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-frequently-asked-questions"></a>Autenticación de paso a través de Azure Active Directory: Preguntas más frecuentes

En este artículo se ofrece respuesta a las preguntas más frecuentes acerca de la autenticación de paso a través de Azure Active Directory (Azure AD). Siga comprobando si hay contenido nuevo.

>[!IMPORTANT]
>característica de autenticación de paso a través de Hello está actualmente en vista previa.

## <a name="which-of-hello-azure-ad-sign-in-methods---pass-through-authentication-password-hash-synchronization-and-active-directory-federation-services-ad-fs---should-i-choose"></a>¿Cuál hello Azure AD inicio de sesión de métodos de autenticación de paso a través, sincronización de Hash de contraseña y los servicios de federación de Active Directory (AD FS) - debo elegir?

Depende de su entorno local y de los requisitos organizativos. Revise este artículo para una [Hola de comparación de varios métodos de inicio de sesión en Azure AD](active-directory-aadconnect-user-signin.md).

## <a name="is-pass-through-authentication-a-free-feature"></a>¿Es la autenticación de paso a través una característica gratuita?

Este tipo de autenticación es una característica disponible y no necesita ninguna edición de pagada de Azure AD toouse lo. Permanece disponible cuando la característica de hello alcance la disponibilidad general.

## <a name="is-pass-through-authentication-available-in-microsoft-cloud-germanyhttpwwwmicrosoftdecloud-deutschland-and-microsoft-azure-government-cloudhttpsazuremicrosoftcomfeaturesgov"></a>¿Está disponible la autenticación de paso a través en [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) y en la [nube de Microsoft Azure Government](https://azure.microsoft.com/features/gov/)?

No, la autenticación de paso a través solo está disponible en la instancia de todo el mundo Hola de Azure AD.

## <a name="does-conditional-accessactive-directory-conditional-accessmd-work-with-pass-through-authentication"></a>¿Funciona el [acceso condicional](../active-directory-conditional-access.md) con la autenticación de paso a través?

Sí, todas las funcionalidades de acceso condicional, incluida Azure Multi-Factor Authentication, funcionan con la autenticación de paso a través.

## <a name="does-pass-through-authentication-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>¿Admite la autenticación de paso a través "Id. alternativo" como nombre de usuario de hello, en lugar de "userPrincipalName"?

Sí. Admite la autenticación de paso a través `Alternate ID` como nombre de usuario cuando se configura en Azure AD Connect, tal como se muestra de Hola [aquí](active-directory-aadconnect-get-started-custom.md). No todas las aplicaciones de Office 365 admiten `Alternate ID`. Consulte la documentación de toohello específico de la aplicación para la declaración de soporte técnico de Hola.

## <a name="does-password-hash-synchronization-act-as-a-fallback-toopass-through-authentication"></a>¿Sincronización de Hash de contraseña actúan como tooPass mediante autenticación de reserva?

No, la sincronización de Hash de contraseña no es genérico tooPass mediante autenticación de reserva. Solo actúa como reserva para [escenarios en los que la autenticación de paso a través no se admite en la actualidad](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios). tooavoid inicio de sesión de errores de usuarios, debe configurar la autenticación de paso a través de [alta disponibilidad](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="can-i-install-an-azure-ad-application-proxyactive-directory-application-proxy-get-startedmd-connector-on-hello-same-server-as-a-pass-through-authentication-agent"></a>¿Puedo instalar un [Proxy de aplicación de Azure AD](../active-directory-application-proxy-get-started.md) conector hello en el mismo servidor que un agente de autenticación de paso a través?

Sí, esta configuración es compatible con hello cambiado el nombre de las versiones de agente de autenticación de paso a través de hello (versiones 1.5.193.0 o posterior).

## <a name="what-versions-of-azure-ad-connect-and-pass-through-authentication-agent-do-you-need"></a>¿Qué versiones de Azure AD Connect y del agente de autenticación de paso a través necesita?

Se necesita la versión 1.1.486.0 o posterior para Azure AD Connect y 1.5.58.0 o posterior para hello agente de autenticación de paso a través para esta característica toowork. Todo el software debe instalarse en servidores con Windows Server 2012 R2 o posterior.

## <a name="what-happens-if-my-users-password-has-expired-and-they-try-toosign-in-using-pass-through-authentication"></a>¿Qué ocurre si mi contraseña ha expirado y se intentan toosign con la autenticación de paso a través?

Si ha configurado [escritura diferida de contraseñas](../active-directory-passwords-update-your-own-password.md) para un usuario específico, y si el usuario de hello inicia sesión con autenticación de paso a través, pueden cambiar o restablecer sus contraseñas. las contraseñas de Hola se reescriben tooon local de Active Directory según lo previsto.

Sin embargo, si la escritura diferida de contraseñas no está configurado para un usuario específico o si hello usuario no tiene un anuncio de Azure válido una licencia asignada, usuario de hello no puede actualizar su contraseña en la nube de Hola. El usuario no puede actualizar la contraseña incluso aunque haya expirado. usuario de Hello en su lugar ve este mensaje: "su organización no permite tooupdate la contraseña en este sitio. Actualizar según el método de toohello recomendado por su organización, o pida a su administrador si necesita ayuda." usuario de Hola o un administrador de hello tiene tooreset su contraseña en su Active Directory local.

## <a name="how-does-pass-through-authentication-protect-you-against-brute-force-password-attacks"></a>¿Cómo protege la autenticación de paso a través frente a ataques de contraseña por fuerza bruta?

Lea [este artículo](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) para más información.

## <a name="what-do-pass-through-authentication-agents-communicate-over-ports-80-and-443"></a>¿Qué comunican los agentes de autenticación de paso a través mediante los puertos 80 y 443?

- Hola autenticación agentes realizan las solicitudes HTTPS en el puerto 443 para todas las operaciones de característica.
- Agentes de autenticación de Hello realizar solicitudes HTTP a través del puerto 80 toodownload SSL certificado listas de revocación de.

     >[!NOTE]
     >En las actualizaciones recientes se Hola número reducido de puertos requeridos por la característica de Hola. Si tiene versiones anteriores de Azure AD Connect o hello agente de autenticación, mantener estos puertos abiertos también: 5671, 8080, 9090, 9091, 9350, 9352 y 10100 10120.

## <a name="can-hello-pass-through-authentication-agents-communicate-over-an-outbound-web-proxy-server"></a>¿Puede agentes de autenticación de paso a través de hello comunicarse a través de un servidor de proxy web de salida?

Sí. Si WPAD (Web Proxy Auto-Discovery) está habilitada en su entorno local, los agentes de autenticación automáticamente intente toolocate y usar un servidor proxy web en red de Hola.

## <a name="can-i-install-two-or-more-pass-through-authentication-agents-on-hello-same-server"></a>¿Puedo instalar dos o más agentes de autenticación de paso a través en Hola mismo servidor?

No, solo se puede instalar un agente de autenticación de paso a través en un único servidor. Si desea tooconfigure autenticación de paso a través de alta disponibilidad, siga las instrucciones de hello en este [artículo](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) en su lugar.

## <a name="i-already-use-active-directory-federation-services-ad-fs-for-azure-ad-sign-in-how-do-i-switch-it-toopass-through-authentication"></a>Ya utilizo los servicios de federación de Active Directory (AD FS) para el inicio de sesión de Azure AD. ¿Cómo cambio se tooPass a través de la autenticación?

Si ha configurado AD FS como su método de inicio de sesión mediante el Asistente de hello Azure AD Connect, cambie el método de inicio de sesión de usuario de hello tooPass a través de la autenticación. Este cambio habilita la autenticación de paso a través de inquilino de Hola y convierte _todos los_ los dominios federados en dominios administrado. Todas las solicitudes de inicio de sesión posteriores del inquilino se manejarán mediante la autenticación de paso a través. Actualmente, no hay ninguna manera admitida en Azure AD Connect toouse una combinación de AD FS y la autenticación de paso a través de distintos dominios.

Si AD FS se haya configurado como método de inicio de sesión de hello _fuera_ del Asistente para conectar de hello Azure AD, cambiar el método de inicio de sesión de usuario de hello tooPass a través de la autenticación (de la opción de "No configura" hello). Este cambio permite la autenticación de paso a través en inquilino Hola. Sin embargo, todos los dominios federados continuar toouse AD FS para el inicio de sesión. Usar a PowerShell toomanually convert todos o algunos de estos federado tooManaged dominios. Después de eso, todas las solicitudes de inicio de sesión en dominios administrados (_solo en ellos_) se controlarán mediante la autenticación de paso a través.

>[!IMPORTANT]
>La autenticación de paso a través no admite el inicio de sesión de usuarios de Azure AD solo en la nube.

## <a name="can-i-use-pass-through-authentication-in-a-multi-forest-ad-environment"></a>¿Se puede usar la autenticación de paso a través en un entorno de bosques múltiples de AD?

Sí. Se admiten entornos de varios bosques si hay relaciones de confianza de bosque entre los bosques de AD y si el enrutamiento de sufijos de nombre está configurado correctamente.

## <a name="do-pass-through-authentication-agents-provide-load-balancing-capability"></a>¿Ofrecen los agentes de autenticación de paso a través la funcionalidad de equilibrio de carga?

No, la instalación de varios agentes de autenticación de paso a través solo garantiza una [alta disponibilidad](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability), pero no el equilibrio de carga. Uno o dos agentes de autenticación de Hola terminen control masiva Hola de las solicitudes de inicio de sesión de Hola.

Las solicitudes de validación de contraseña que Hola agentes de autenticación necesario toohandle son ligeras. Por lo tanto, con un total de dos o tres agentes de autenticación se pueden manejar fácilmente las cargas máximas y las cargas medias de trabajo de la mayoría de los clientes.

Se recomienda que instale agentes de autenticación tooyour cerrar controladores de dominio tooimprove inicio de sesión de latencia.

## <a name="can-i-install-hello-first-pass-through-authentication-agent-on-a-server-other-than-hello-one-that-runs-azure-ad-connect"></a>¿Puedo instalar Hola primer agente de autenticación de paso a través en un servidor distinto Hola aquel que se ejecuta Azure AD Connect?

No, este escenario _no_ se admite.

## <a name="how-many-pass-through-authentication-agents-should-i-install"></a>¿Cuántos agentes de autenticación de paso a través se deben instalar?

Es recomendable que:

- Instale dos o tres agentes de autenticación en total. Esta configuración es suficiente para la mayoría de los clientes.
- Instale la latencia de inicio de sesión de tooimprove de agentes de autenticación en los controladores de dominio (o como cerrar toothem como sea posible).
- Asegúrese de que se agregan servidores (donde están instalados los agentes de autenticación) toohello AD mismo bosque como usuarios de hello cuyas contraseñas necesitan toobe validado.

>[!NOTE]
>Hay un límite de sistema de 12 agentes de autenticación por inquilino.

## <a name="how-can-i-disable-pass-through-authentication"></a>¿Se puede deshabilitar la autenticación de paso a través?

Vuelva a ejecutar el Asistente de Azure AD Connect de Hola y cambie el método de inicio de sesión de usuario de Hola de método de autenticación de paso a través de tooanother. Este cambio deshabilita la autenticación de paso a través de inquilino de Hola y desinstala Hola agente de autenticación del servidor de Hola. Tener Hola de toomanually desinstalar agentes de autenticación desde otros servidores.

## <a name="what-happens-when-i-uninstall-a-pass-through-authentication-agent"></a>¿Qué ocurre cuando se desinstala un agente de autenticación de paso a través?

Desinstalar a un agente de autenticación de paso a través de un servidor hace que se toostop aceptando solicitudes de inicio de sesión. Asegúrese de que tiene otro agente de autenticación que se ejecuta antes de realizar esta operación, tooavoid interrumpa usuario iniciar sesión con su inquilino.

## <a name="next-steps"></a>Pasos siguientes
- [**Limitaciones actuales**](active-directory-aadconnect-pass-through-authentication-current-limitations.md): esta funcionalidad actualmente está en su versión preliminar. Obtenga información acerca de qué escenarios se admiten y cuáles no.
- [**Inicio rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md): desarrollo y ejecución de la autenticación de paso a través de Azure AD.
- [**Profundización técnica**](active-directory-aadconnect-pass-through-authentication-how-it-works.md): descripción del funcionamiento de esta característica.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.
- [**SSO de conexión directa de Azure AD**](active-directory-aadconnect-sso.md): obtenga más información sobre esta característica complementaria.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.
