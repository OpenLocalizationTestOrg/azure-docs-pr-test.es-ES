---
title: "aaaProblem iniciar sesión en el sitio Web de panel de acceso toohello | Documentos de Microsoft"
description: Problemas de tootroubleshoot de instrucciones que pueden surgir al intentar toosign en toouse Hola Panel de acceso
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
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a>Problema al iniciar sesión en el sitio Web de panel de acceso toohello

Hola Panel de acceso es un portal basado en web que permite un usuario que tiene una empresa o centro educativo Administrador de la cuenta en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que hello Azure AD le haya concedido acceso a. Un usuario que tenga las ediciones de Azure AD también puede utilizar grupos de autoservicio y capacidades de administración de aplicaciones a través de hello Panel de acceso. Hola Panel de acceso es independiente de hello portal de Azure y no requiere que los usuarios toohave una suscripción de Azure.

Los usuarios puedan iniciar sesión en toohello Panel de acceso si tienen una cuenta profesional o educativa en Azure AD.

-   Los usuarios se pueden autenticar directamente mediante Azure AD.

-   Los usuarios se pueden autenticar mediante los Servicios de federación de Active Directory (AD FS).

-   Los usuarios se pueden autenticar mediante Windows Server Active Directory.

Si un usuario tiene una suscripción para Azure u Office 365 y ha estado usando Hola portal de Azure o una aplicación de Office 365, será capaz de toouse Hola Panel de acceso sin problemas sin necesidad de toosign de nuevo. Los usuarios autenticados no sea toosign solicitada en mediante Hola username y password para su cuenta de Azure AD. Si la organización de hello ha configurado federación, escriba el nombre de usuario de Hola es suficiente.

## <a name="general-issues-toocheck-first"></a>General emite toocheck primero 

-   Asegúrese de que el usuario de hello es iniciar sesión en toohello **corríjala**: <https://myapps.microsoft.com>

-   Asegúrese de que el explorador del usuario de hello agregada tooits de dirección URL de Hola **sitios de confianza**

-   Asegúrese de que es la cuenta de usuario de hello **habilitado** para inicios de sesión.

-   Asegúrese de que es la cuenta de usuario de hello **no está bloqueada.**

-   Asegúrese de que usuario hello **contraseña no se ha caducado o se olvida.**

-   Que **Multi-Factor Authentication** no bloquea el acceso del usuario.

-   Que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquea el acceso del usuario.

-   Asegúrese de que un usuario **información de contacto de autenticación** es hacia arriba toodate tooallow la autenticación multifactor o acceso condicional directivas toobe aplicada.

-   Asegúrese de tooalso seguro intente borrar las cookies del explorador y vuelva a probar toosign en.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Se cumplen los requisitos de explorador para hello Panel de acceso

Hola Panel de acceso requiere un explorador que admita JavaScript y se han habilitado de CSS. toouse basada en contraseña inicio de sesión único (SSO) en el Panel de acceso, extensión del Panel de acceso de Hola Hola debe instalarse en el explorador del usuario de Hola. Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.

Para el SSO basado en contraseña, pueden ser Hola exploradores de los usuarios:

-   Internet Explorer 8, 9, 10, 11 (en Windows 7 o posterior)

-   Edge en Windows 10 Anniversary Edition o posterior 

-   Chrome (en Windows 7 o posterior y en Mac OS X o posterior)

-   Firefox 26.0 o posterior (en Windows XP SP2 o posterior y en Mac OS X 10.6 o posterior)


## <a name="problems-with-hello-users-account"></a>Problemas con la cuenta de usuario de Hola

Acceso toohello Panel de acceso se puede bloquear debido tooa problema con la cuenta de usuario de Hola. A continuación se muestran algunas maneras de solucionar problemas con los usuarios y la configuración de sus cuentas:

-   [Comprobar si existe una cuenta de usuario en Azure Active Directory](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Comprobar el estado de la cuenta de un usuario](#check-a-users-account-status)

-   [Restablecer la contraseña de un usuario](#reset-a-users-password)

-   [Habilitar el autoservicio de restablecimiento de contraseña](#enable-self-service-password-reset)

-   [Comprobar el estado de la autenticación multifactor de un usuario](#check-a-users-multi-factor-authentication-status)

-   [Comprobar la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info)

-   [Comprobar la pertenencia a grupos de un usuario](#check-a-users-group-memberships)

-   [Comprobar las licencias asignadas de un usuario](#check-a-users-assigned-licenses)

-   [Asignar una licencia a un usuario](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Comprobar si existe una cuenta de usuario en Azure Active Directory

toocheck si está presente, una cuenta de usuario siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Compruebe las propiedades de Hola de hello usuario objeto toobe seguro de que se muestran como esperaba y no existe ningún dato.

### <a name="check-a-users-account-status"></a>Comprobar el estado de la cuenta de un usuario

toocheck un usuario de estado de la cuenta, siga los pasos de hello siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **Perfil**.

8.  En **configuración** Asegúrese de que **bloque iniciar sesión en** se establece demasiado**No**.

### <a name="reset-a-users-password"></a>Restablecer la contraseña de un usuario

tooreset contraseña de un usuario, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en hello **de restablecimiento de contraseña** situado en la parte superior de Hola de hoja de usuario de Hola.

8.  Haga clic en hello **de restablecimiento de contraseña** botón en hello **de restablecimiento de contraseña** hoja que aparece.

9.  Hola copia **contraseña temporal** o **escriba una contraseña nueva** para el usuario de Hola.

10. Este nuevo usuario toohello de contraseña se comunican, requiere toochange esta contraseña durante su próximo iniciar sesión en tooAzure Active Directory.

### <a name="enable-self-service-password-reset"></a>Habilitar el autoservicio de restablecimiento de contraseña

contraseña de autoservicio de tooenable restablecer, siga los pasos de implementación de hello siguientes:

-   [Habilitar usuarios tooreset sus contraseñas de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Habilitar usuarios tooreset o cambiar sus contraseñas locales de Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Comprobar el estado de la autenticación multifactor de un usuario

toocheck un usuario de multifactor estado de autenticación, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  Haga clic en hello **la autenticación multifactor** situado en la parte superior de Hola de hoja de Hola.

7.  Una vez Hola **Portal de administración de Multi-factor Authentication** cargas, asegúrese de que esté en hello **usuarios** ficha.

8.  Busque el usuario de hello en lista de Hola de usuarios por búsqueda, el filtrado u ordenación.

9.  Usuario seleccione Hola Hola usuarios de lista y **habilitar**, **deshabilitar**, o **aplicar** la autenticación multifactor según sea necesario.

   >[!NOTE]
   >Si un usuario pertenece a un **forzado** estado, puede establecerlos demasiado**deshabilitado** temporalmente toolet volverlos a su cuenta. Una vez que estén en, a continuación, puede cambiar su estado demasiado**habilitado** nuevo toorequire les toore su información de contacto durante su próximo iniciar sesión en el registro. Como alternativa, puede seguir los pasos de Hola Hola [Compruebe la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info) tooverify o establecer estos datos para ellos.
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>Comprobar la información de contacto de autenticación de un usuario

toocheck autenticación de un usuario, póngase en contacto con información usada para la autenticación multifactor, acceso condicional, protección de identidad y de restablecimiento de contraseña, siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **Perfil**.

8.  Desplácese hacia abajo demasiado**información de contacto de autenticación**.

9.  **Revisión** datos Hola registrado para el usuario de Hola y actualizar según sea necesario.

### <a name="check-a-users-group-memberships"></a>Comprobar la pertenencia a grupos de un usuario

toocheck un usuario de pertenencia a grupos, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **grupos** toosee que agrupa usuario hello es un miembro de.

### <a name="check-a-users-assigned-licenses"></a>Comprobar las licencias asignadas de un usuario

toocheck un usuario había asignado licencias, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.

### <a name="assign-a-user-a-license"></a>Asignar una licencia a un usuario 

tooassign un usuario tooa de licencias, siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.

8.  Haga clic en hello **asignar** botón.

9.  Seleccione **uno o más productos** en lista de Hola de productos disponibles.

10. **Opcional** haga clic en hello **opciones de asignación** elemento toogranularly asignar productos. Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.

11. Haga clic en hello **asignar** botón tooassign estos usuario toothis de licencias.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Si estos pasos no resuelven el problema de Hola

Abra una incidencia de soporte técnico con hello siguiente información si está disponible:

-   Id. de error de correlación

-   UPN (dirección de correo electrónico del usuario)

-   Id. de inquilino

-   Tipo de explorador

-   Zona horaria y hora/período de tiempo durante el que se produce el error

-   Seguimientos de Fiddler

## <a name="next-steps"></a>Pasos siguientes
[Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)
