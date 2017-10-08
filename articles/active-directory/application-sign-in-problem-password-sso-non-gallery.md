---
title: "aaaProblems tooan aplicación de galería de Azure AD configurada para la contraseña de inicio de sesión inicio de sesión único | Documentos de Microsoft"
description: "Se describen las áreas problemáticas que proporcionan instrucciones tootroubleshoot emite toosigning relacionado en tooAzure configuradas para inicio de sesión único en la contraseña de aplicaciones de galería de AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a>Problemas para iniciar sesión en tooan configurado para inicio de sesión único en la contraseña de aplicación de galería de Azure AD

Hola Panel de acceso es un portal basado en web que permite un usuario que tiene una empresa o centro educativo Administrador de la cuenta en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que hello Azure AD le haya concedido acceso a. Un usuario que tenga las ediciones de Azure AD también puede utilizar grupos de autoservicio y capacidades de administración de aplicaciones a través de hello Panel de acceso. Hola Panel de acceso es independiente de hello portal de Azure y no requiere que los usuarios toohave una suscripción de Azure.

toouse basada en contraseña inicio de sesión único (SSO) en el Panel de acceso, extensión del Panel de acceso de Hola Hola debe instalarse en el explorador del usuario de Hola. Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Se cumplen los requisitos de explorador para hello Panel de acceso

Hola Panel de acceso requiere un explorador que admita JavaScript y se han habilitado de CSS. toouse basada en contraseña inicio de sesión único (SSO) en el Panel de acceso, extensión del Panel de acceso de Hola Hola debe instalarse en el explorador del usuario de Hola. Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.

Para el SSO basado en contraseña, pueden ser Hola exploradores de los usuarios:

-   Internet Explorer 8, 9, 10, 11 (en Windows 7 o posterior)

-   Chrome (en Windows 7 o posterior y en Mac OS X o posterior)

-   Firefox 26.0 o posterior (en Windows XP SP2 o posterior y en Mac OS X 10.6 o posterior)

>[!NOTE]
>extensión SSO basada en contraseña de Hello están disponibles para los bordes del 10 de Windows cuando se convierten en admite las extensiones del explorador de Edge.
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>¿Cómo tooinstall Hola extensión de explorador del Panel de acceso

Hola tooinstall extensión de explorador del Panel de acceso, siga Hola pasos:

1.  Abra hello [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores compatibles de Hola y de inicio de sesión como un **usuario** en Azure AD.

2.  Haga clic en un **aplicación SSO de contraseña** Hola Panel de acceso.

3.  En hello símbolo del sistema que se pregunta tooinstall Hola software, seleccione **instalar ahora**.

4.  Basado en el explorador es que el vínculo de descarga de toohello dirigida. **Agregar** tooyour Explorador de hello extensión.

5.  Si el explorador solicita, seleccione tooeither **habilitar** o **permitir** Hola extensión.

6.  Una vez instalada, **reinicie** la sesión del explorador.

7.  Inicie sesión en el Panel de acceso de Hola y vea si puede **iniciar** las aplicaciones de SSO de contraseña

También puede descargar extensión Hola para Chrome y Firefox de vínculos directos de Hola a continuación:

-   [Extensión del Panel de acceso para Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensión del Panel de acceso para Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Configuración de una directiva de grupo para Internet Explorer

Puede configurar una directiva de grupo que le permiten tooremotely instalar extensión de Panel de acceso de Hola para Internet Explorer en equipos de los usuarios.

requisitos previos de Hello incluyen:

-   Ha configurado [los servicios de dominio de Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), y se han unido a dominio de tooyour de máquinas de los usuarios.

-   Debe tener Hola "Editar configuración de" permiso tooedit Hola objeto de directiva de grupo (GPO). De forma predeterminada, los miembros del programa Hola a los grupos de seguridad siguientes tienen este permiso: los administradores de dominio, los administradores de organización y propietarios del creador de directivas de grupo. [Más información](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Siga el tutorial de hello [cómo tooDeploy Hola extensión del Panel de acceso para Internet Explorer utilizando la directiva de grupo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) para obtener instrucciones paso a paso acerca de cómo tooconfigure Hola de directiva de grupo e implementarla toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Solucionar problemas de hello Panel de acceso en Internet Explorer

Siga hello [solucionar Hola extensión del Panel de acceso de Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guía para el acceso a una herramienta de diagnóstico y obtener instrucciones paso a paso acerca de cómo configurar la extensión de Hola para Internet Explorer.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación no Galería

una aplicación desde la Galería de Azure AD de hello tooconfigure debe:

-   [Incorporación de una aplicación ajena a la galería](#add-a-non-gallery-application)

-   [Configurar la aplicación hello para el inicio de sesión único en la contraseña](#configure-the-application-for-password-single-sign-on)

-   [Asignar a usuarios de aplicación toohello](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a>Incorporación de una aplicación ajena a la galería

tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:

1.  Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja

6.  Haga clic en **Aplicación situada fuera de la galería**.

7.  Escriba el nombre de saludo de la aplicación Hola **nombre** cuadro de texto. Seleccione **Agregar**.

Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar la aplicación hello para el inicio de sesión único en la contraseña

tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccione la aplicación hello desea tooconfigure inicio de sesión único

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Modo de hello seleccione **sesión basada en contraseña.**

9.  Escriba hello **dirección URL de inicio de sesión**. Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a. Asegúrese de que está visible en la dirección URL de Hola Hola campos inicio de sesión.

10. Asignar a usuarios de aplicación de toohello.

11. Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola. En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.

### <a name="assign-users-toohello-application"></a>Asignar a usuarios de aplicación toohello

tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.

7.  Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.

8.  Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.

9.  Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.

10. Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.

11. Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**. Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.

12. **Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.

13. Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.

14. **Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.

15. Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.

Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Si estos pasos no Hola resolver el problema de Hola

Abra una incidencia de soporte técnico con hello siguiente información si está disponible:

-   Id. de error de correlación

-   UPN (dirección de correo electrónico del usuario)

-   TenantID

-   Tipo de explorador

-   Zona horaria y hora/período de tiempo durante el que se produce el error

-   Seguimientos de Fiddler

## <a name="next-steps"></a>Pasos siguientes
[Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)

