---
title: "Azure AD Connect: preguntas más frecuentes sobre el inicio de sesión único de conexión directa | Microsoft Docs"
description: "Respuestas toofrequently preguntas más frecuentes sobre Azure Active Directory sin problemas Single Sign-On."
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
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Preguntas más frecuentes sobre el inicio de sesión único de conexión directa de Azure Active Directory

En este artículo se ofrece respuesta a las preguntas más frecuentes sobre el inicio de sesión único de conexión directa (SSO de conexión directa) de Azure Active Directory. Siga comprobando si hay contenido nuevo.

>[!IMPORTANT]
>característica de SSO sin problemas de Hello está actualmente en vista previa.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>¿Con qué métodos de inicio de sesión funciona el SSO de conexión directa?

SSO sin problemas puede combinarse con cualquier hello [sincronización de Hash de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) o [autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md) métodos de inicio de sesión. Pero esta característica no se puede usar con los Servicios de federación de Active Directory (AD FS).

## <a name="is-seamless-sso-a-free-feature"></a>¿SSO de conexión directa es una característica gratuita?

SSO sin problemas es una característica gratuita y no necesita ninguna edición de pagada de Azure AD toouse lo. Permanece disponible cuando la característica de hello alcance la disponibilidad general.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>¿Qué aplicaciones aprovechan la funcionalidad de parámetro `domain_hint` o `login_hint` de SSO de conexión directa?

Estamos en proceso de Hola de compilando lista de Hola de las aplicaciones que envían estos hello y parámetros que no. Si tiene aplicaciones que están interesadas, comuníquenoslo en la sección de comentarios de Hola.

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>¿Es compatible con el SSO sin problemas `Alternate ID` como Hola nombre de usuario, en lugar de `userPrincipalName`?

Sí. Es compatible con SSO sin problemas `Alternate ID` como nombre de usuario cuando se configura en Azure AD Connect, tal como se muestra de Hola [aquí](active-directory-aadconnect-get-started-custom.md). No todas las aplicaciones de Office 365 admiten `Alternate ID`. Consulte la documentación de toohello específico de la aplicación para la declaración de soporte técnico de Hola.

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>Deseo tooregister distinta de Windows 10 dispositivos con Azure AD, sin usar AD FS. ¿Puedo usar SSO de conexión directa en su lugar?

Sí, este escenario necesita la versión 2.1 o posterior de hello [cliente del área de trabajo](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>¿Cómo puedo poner a través de la clave de descifrado de Kerberos de Hola de hello `AZUREADSSOACCT` cuenta de equipo?

Es importante toofrequently escribirse clave de descifrado de Kerberos de Hola de hello `AZUREADSSOACCT` cuenta de equipo (representado por Azure AD) creado en sus instalaciones en el bosque de AD.

>[!IMPORTANT]
>Se recomienda encarecidamente implementar a través de la clave de descifrado de hello Kerberos al menos cada 30 días.

Siga estos pasos en el servidor local de Hola donde se ejecuta Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Paso 1. Obtención de la lista de bosques de AD en los que se habilitó SSO de conexión directa

1. En primer lugar, descargar e instalar hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).
2. A continuación, descargue e instale hello [módulo de Azure Active Directory de 64 bits para Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navegue toohello `%programfiles%\Microsoft Azure Active Directory Connect` carpeta.
4. Módulo de PowerShell de SSO sin problemas de importación Hola con este comando: `Import-Module .\AzureADSSO.psd1`.
5. Ejecute PowerShell como administrador. En PowerShell, llame a `New-AzureADSSOAuthenticationContext`. Este comando debe darle un tooenter emergente credenciales de administrador Global de su inquilino.
6. Llame a `Get-AzureADSSOStatus`. Este comando proporciona que Hola lista de los bosques de AD (vistazo a la lista de dominios"hello") en que se ha habilitado esta característica.

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>Paso 2: Actualizar la clave de descifrado de Kerberos de hello en cada bosque de AD que se ha configurado, en

1. Llame a `$creds = Get-Credential`. Cuando se le solicite, escriba las credenciales de administrador de dominio de hello para el bosque de AD que vayan Hola.
2. Llame a `Update-AzureADSSOForest -OnPremCredentials $creds`. Este comando actualizaciones Hola clave de descifrado de Kerberos para hello `AZUREADSSOACCT` cuenta de equipo en este bosque de AD específico y se actualiza en Azure AD.
3. Repita Hola pasos para cada bosque de AD que haya configurado la característica de hello en anteriores.

>[!IMPORTANT]
>Asegúrese de que _no_ ejecute hello `Update-AzureADSSOForest` comando más de una vez. En caso contrario, la característica de hello deja de funcionar hasta el tiempo de hello vales de Kerberos de los usuarios expiren y se vuelve a emitir su Active Directory local.

## <a name="how-can-i-disable-seamless-sso"></a>¿Cómo se deshabilita SSO de conexión directa?

SSO de conexión directa se puede deshabilitar con Azure AD Connect.

Ejecute Azure AD Connect, elija "Change user sign-in page" (Cambiar página de inicio de sesión de usuario) y haga clic en "Siguiente". A continuación, desactive la opción "Habilitar inicio de sesión único" de Hola. Continúe con el Asistente de Hola. Tras la finalización del Asistente para hello, SSO sin problemas está deshabilitado en el inquilino.

Sin embargo, verá un mensaje en pantalla en el que se anuncia lo siguiente:

"Inicio de sesión único ahora está deshabilitada, pero hay pasos manuales adicionales tooperform en orden toocomplete limpieza. Más información".

toocomplete Hola proceso, siga estos pasos manuales en el servidor local de Hola donde se ejecuta Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Paso 1. Obtención de la lista de bosques de AD en los que se habilitó SSO de conexión directa

1. En primer lugar, descargar e instalar hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).
2. A continuación, descargue e instale hello [módulo de Azure Active Directory de 64 bits para Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navegue toohello `%programfiles%\Microsoft Azure Active Directory Connect` carpeta.
4. Módulo de PowerShell de SSO sin problemas de importación Hola con este comando: `Import-Module .\AzureADSSO.psd1`.
5. Ejecute PowerShell como administrador. En PowerShell, llame a `New-AzureADSSOAuthenticationContext`. Este comando debe darle un tooenter emergente credenciales de administrador Global de su inquilino.
6. Llame a `Get-AzureADSSOStatus`. Este comando proporciona que Hola lista de los bosques de AD (vistazo a la lista de dominios"hello") en que se ha habilitado esta característica.

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>Paso 2: Elimine manualmente hello `AZUREADSSOACCT` cuenta de equipo en cada bosque de AD que se ve.

## <a name="next-steps"></a>Pasos siguientes

- [**Inicio rápido**](active-directory-aadconnect-sso-quick-start.md): desarrollo y ejecución de SSO de conexión directa de Azure AD.
- [**Profundización técnica**](active-directory-aadconnect-sso-how-it-works.md): descripción del funcionamiento de esta característica.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para la tramitación de solicitudes de nuevas características.
