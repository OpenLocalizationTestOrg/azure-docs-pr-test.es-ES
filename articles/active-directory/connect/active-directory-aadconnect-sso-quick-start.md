---
title: "Inicio de sesión único de conexión directa de Azure AD Connect: Quía de inicio rápido | Microsoft Docs"
description: "Este artículo describe cómo se inicia tooget con Azure Active Directory sin problemas Single Sign-On."
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Inicio de sesión único de conexión directa de Azure Active Directory: Guía de inicio rápido

## <a name="how-toodeploy-seamless-sso"></a>¿Cómo toodeploy SSO sin problemas

Azure Active Directory sin problemas Single Sign-On (SSO sin problemas de Azure AD), inicia automáticamente los usuarios cuando se encuentran en su red corporativa de los escritorios corporativos tooyour conectado. Proporciona a los usuarios un acceso fácil tooyour basada en la nube aplicaciones sin necesidad de todos los componentes locales adicionales.

>[!IMPORTANT]
>característica de SSO sin problemas de Hello está actualmente en vista previa.

toodeploy SSO sin problemas, necesita toofollow estos pasos:

## <a name="step-1-check-prerequisites"></a>Paso 1: Comprobación de los requisitos previos

Asegúrese de que Hola siguiendo los requisitos previos están en su lugar:

1. El servidor de Azure AD Connect está configurado: si usa la [autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md) como método de inicio de sesión, no es necesaria realizar ninguna otra acción. Si va a usar la [sincronización de hash de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) como método de inicio de sesión y hay un firewall entre Azure AD Connect y Azure AD, asegúrese de que:
- Está usando la versión 1.1.484.0 de Azure AD Connect o una posterior.
- Azure AD Connect puede comunicarse con las direcciones URL de `*.msappproxy.net` y a través del puerto 443. Este requisito previo solo es aplicable cuando se habilita la característica de hello, no para los inicios de sesión de usuario real.
- Azure AD Connect hacer direct IP conexiones toohello [intervalos IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653). Una vez más, este requisito previo solo es aplicable cuando se habilita la característica de Hola.
2. Necesita credenciales de administrador de dominio para cada bosque de AD que sincronizar tooAzure AD (mediante Azure AD Connect) y para cuyos usuarios desea tooenable SSO sin problemas.

## <a name="step-2-enable-hello-feature"></a>Paso 2: Habilitar la característica de Hola

SSO de conexión directa se puede habilitar a través de [Azure AD Connect](active-directory-aadconnect.md).

Si está realizando una instalación nueva de Azure AD Connect, elija hello [ruta de acceso de instalación personalizada](active-directory-aadconnect-get-started-custom.md). En la página de Hola "Inicio de sesión de usuario", active la opción de "Habilitar inicio de sesión único" de Hola.

![Azure AD Connect: Inicio de sesión de usuario](./media/active-directory-aadconnect-sso/sso8.png)

Si ya tiene una instalación de Azure AD Connect, elija "Change user sign-in page" (Cambiar página de inicio de sesión del usuario) en Azure AD Connect y haga clic en "Siguiente". A continuación, compruebe la opción "Habilitar inicio de sesión único" de Hola.

![Azure AD Connect: Change user sign-in page (Cambiar página de inicio de sesión del usuario)](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Continúe con el Asistente de hello hasta obtener la página de "Habilitar inicio de sesión único" de toohello. Proporcione las credenciales de administrador de dominio para cada bosque de AD que sincronizar tooAzure AD (mediante Azure AD Connect) y para cuyos usuarios desea tooenable SSO sin problemas. 

Tras la finalización del Asistente para hello, SSO sin problemas está habilitado en el inquilino.

>[!NOTE]
> las credenciales de administrador de dominio de Hello no se almacenan en Azure AD Connect o en Azure AD, pero son solo la característica de hello tooenable usado.

Siga estos tooverify de instrucciones que se ha habilitado correctamente SSO sin problemas:

1. Inicie sesión en toohello [centro de administración de Azure Active Directory](https://aad.portal.azure.com) con credenciales de administrador Global de hello para el inquilino.
2. Seleccione **Azure Active Directory** en el panel de navegación izquierdo Hola.
3. Seleccione **Azure AD Connect**.
4. Compruebe que hello **perfecta Single Sign-On** característica se muestra como **habilitado**.

![Azure Portal: hoja Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a>Paso 3: Implementar características de Hola

tooroll los usuarios de hello característica tooyour, necesita configuración de zona de Intranet de toousers del Azure direcciones URL de AD (https://autologon.microsoftazuread-sso.com y https://aadg.windows.net.nsatc.net) de dos tooadd a través de la directiva de grupo en Active Directory.

>[!NOTE]
> Hola siguiendo las instrucciones sólo funcionan para Internet Explorer y Google Chrome en Windows (si el conjunto de direcciones URL de sitios de confianza comparte con Internet Explorer). Lea las secciones siguiente Hola para instrucciones tooset Mozilla Firefox y Google Chrome en Mac.

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a>¿Por qué necesita la configuración de zona de Intranet de los usuarios de toomodify?

De forma predeterminada, el Explorador de hello calcula automáticamente zona derecha de hello (Internet o Intranet) desde una dirección URL. Por ejemplo, http://contoso/ es toohello asignada la zona de Intranet, mientras que http://intranet.contoso.com/ es zona de Internet asignada toohello (porque la dirección URL de hello contiene un punto). Exploradores no envían el extremo de nube de tooa de vales de Kerberos - como Hola dos Azure AD direcciones URL - a menos que su dirección URL se agrega explícitamente a la zona de Intranet del explorador de toohello.

### <a name="detailed-steps"></a>Pasos detallados

1. Abra la herramienta de administración de directivas de grupo de Hola.
2. Editar directiva de grupo aplicado toosome o todos los usuarios de Hola. En este ejemplo, utilizamos hello **Default Domain Policy**.
3. Navegue demasiado**usuario Configuración del equipo\Plantillas administrativas\Componentes de Windows\Internet Internet Control Internet\página** y seleccione **tooZone lista de asignación de sitio**.
![Inicio de sesión único](./media/active-directory-aadconnect-sso/sso6.png)  
4. Habilitar directiva de Hola y escriba Hola después de valores (Azure AD direcciones URL donde se reenvían los vales de Kerberos) y los datos (*1* indica la zona de Intranet) en el cuadro de diálogo de Hola.

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Si desea toodisallow algunos usuarios utilizasen SSO sin problemas: por ejemplo, si estos usuarios inician sesión en quioscos compartidos - establezca Hola valores iniciales demasiado*4*. Esta acción agrega hello las direcciones URL de Azure AD toohello zona Sitios restringidos y se produce un error SSO sin problemas todo el tiempo de Hola.

5. Haga clic en **Aceptar** y en **Aceptar** de nuevo.

![Inicio de sesión único](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>Consideraciones sobre el explorador

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox no realiza automáticamente la autenticación Kerberos. Cada usuario tiene toomanually agregar configuraciones de Firefox hello Azure AD direcciones URL tootheir con hello pasos:
1. Ejecute Firefox y escriba `about:config` en la barra de direcciones de Hola. Descarte las notificaciones que vea.
2. Busque hello **network.negotiate-auth.trusted-URI** preferencias. Esta preferencia enumera los sitios de confianza de Firefox para la autenticación Kerberos.
3. Haga clic con el botón derecho y seleccione "Modificar".
4. Escriba "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" en el campo de Hola.
5. Haga clic en "Aceptar" y vuelva a abrir el Explorador de Hola.

#### <a name="safari-on-mac-os"></a>Safari en Mac OS

Asegúrese de que Hola equipo ejecuta Mac OS tooAD combinada. Consulte las instrucciones sobre cómo toodo que [aquí](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).

#### <a name="google-chrome-on-mac-os"></a>Google Chrome en Mac OS

Para Google Chrome en Mac OS y otras plataformas distintas de Windows, consulte demasiado[este artículo](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) para obtener información sobre cómo toowhitelist Hola direcciones URL de Azure AD para la autenticación integrada.

Mediante la directiva de grupo de aplicaciones de terceros Active Directory extensiones tooroll tooFirefox de hello las direcciones URL de Azure AD y Google Chrome en los usuarios de Mac está fuera del ámbito de este artículo.

#### <a name="known-limitations"></a>Limitaciones conocidas

SSO de conexión directa no funciona en modo de exploración privada en los navegadores Firefox y Edge. También no funciona en Internet Explorer si Hola explorador se ejecuta en modo de protección mejorado.

>[!IMPORTANT]
>Se recientemente revierten compatibilidad con borde tooinvestigate problemas detectados por el cliente.

## <a name="step-4-test-hello-feature"></a>Paso 4: Probar la característica de Hola

característica de hello tootest para un usuario específico, asegúrese de que _todos los_ Hola condiciones siguientes está en su lugar:
  - usuario de Hello es iniciar sesión en un dispositivo de la empresa.
  - dispositivo de Hello ha sido tooyour previamente Unidos a un dominio de Active Directory (AD).
  - dispositivo de Hello tiene un controlador de dominio (DC), ya sea en la red corporativa con cable o inalámbrica de Hola o mediante una conexión de acceso remoto, como una conexión VPN tooyour de conexión directa.
  - Tiene [implantado característica hello](##step-3-roll-out-the-feature) usuario toothis mediante Directiva de grupo.

escenario de hello tootest donde entra en usuario Hola solo nombre de usuario de hello, pero una contraseña no sea hello:
- Inicie sesión en *https://myapps.microsoft.com/* en una nueva sesión privada del explorador.

escenario de hello tootest donde el usuario de hello no tiene la contraseña de nombre de usuario u Hola Hola tooenter: 
- Inicie sesión en *https://myapps.microsoft.com/contoso.onmicrosoft.com* en una nueva sesión privada del explorador. Reemplace "*contoso*" con el nombre de su inquilino.
- O bien, inicie sesión en *https://myapps.microsoft.com/contoso.com* en una nueva sesión privada del explorador. Reemplace "*contoso.com*" con un dominio comprobado (no un dominio federado) en el inquilino.

## <a name="step-5-roll-over-keys"></a>Paso 5: Sustitución de claves

En el paso 2, Azure AD Connect crea cuentas de equipo (que representa a Azure AD) en todos los bosques de AD de hello en el que ha habilitado SSO sin problemas. Obtenga información más detallada [aquí](active-directory-aadconnect-sso-how-it-works.md). Para mejorar la seguridad, se recomienda que con frecuencia se sustituyen las claves de descifrado de hello Kerberos de estas cuentas de equipo.

>[!IMPORTANT]
>No es necesario toodo este paso _inmediatamente_ después de haber habilitado la característica de Hola. Se sustituyen las claves de descifrado de Kerberos de hello al menos cada 30 días.

## <a name="next-steps"></a>Pasos siguientes

- [**Profundización técnica**](active-directory-aadconnect-sso-how-it-works.md): descripción del funcionamiento de esta característica.
- [**Preguntas más frecuentes** ](active-directory-aadconnect-sso-faq.md) -responde toofrequently preguntas más frecuentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Obtenga información acerca de cómo emite tooresolve común con la característica de Hola.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para la tramitación de solicitudes de nuevas características.
