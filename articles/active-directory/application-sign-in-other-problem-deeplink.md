---
title: "iniciar sesión en la aplicación de tooan mediante un vínculo profundo de aaaProblems | Documentos de Microsoft"
description: "Cómo problemas tootroubleshoot obtiene acceso a una aplicación desde una dirección URL de vínculo profundo con Azure AD"
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a>Problemas para iniciar sesión en la aplicación tooan mediante un vínculo profundo

Hola Panel de acceso es un portal basado en web que permite a los usuarios con un trabajo o cuenta educativa en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que Hola Administrador de Azure AD le haya concedido acceso a. 

Estas aplicaciones se configuran en nombre de usuario de hello en el portal de Azure AD Hola. aplicación Hello debe configurarse correctamente y asignado toohello usuario o un grupo de usuario de hello es miembro de la aplicación de hello toosee Hola Panel de acceso.

Acceso de usuario o vínculos profundos las direcciones URL son vínculos que los usuarios pueden usar tooaccess sus aplicaciones de SSO de contraseña directamente desde su dirección URL de exploradores barras. Desplazándose toothis vínculo, los usuarios pueden automáticamente sesión en la aplicación hello sin tener primero toogo toohello Panel de acceso. Se trata de hello mismo vínculo que los usuarios utilicen tooaccess estas aplicaciones desde el iniciador de la aplicación hello Office 365.

## <a name="general-issues-toocheck-first"></a>General emite toocheck primero

-   Asegúrese de que el uso de un **explorador** que cumple los requisitos mínimos de Hola para hello Panel de acceso.

-   Asegúrese de explorador del usuario de hello agregada URL Hola de hello aplicación tooits **sitios de confianza**.

-   Asegúrese de que es de aplicación de hello toocheck **configurado** correctamente.

-   Asegúrese de que es la cuenta de usuario de hello **habilitado** para inicios de sesión.

-   Asegúrese de que es la cuenta de usuario de hello **no está bloqueada.**

-   Asegúrese de que usuario hello **contraseña no se ha caducado o se olvida.**

-   Que **Multi-Factor Authentication** no bloquea el acceso del usuario.

-   Que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquea el acceso del usuario.

-   Asegúrese de que un usuario **información de contacto de autenticación** es hacia arriba toodate tooallow la autenticación multifactor o acceso condicional directivas toobe aplicada.

-   Asegúrese de tooalso seguro intente borrar las cookies del explorador y vuelva a probar toosign en.

## <a name="checking-hello-deeplink"></a>Comprobando vínculo profundo de Hola

toocheck si dispone de vínculo profundo correcto de hello, siga Hola pasos:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

7.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

8.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

9.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

10. Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

11. Seleccionar aplicación de Hola Hola vínculo profundo de Hola de comprobación para la que desea.

12. Buscar etiqueta hello **dirección URL de acceso de usuario**. El vínculo profundo debe coincidir con esta dirección URL.

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

-   [Extensión del panel de acceso para Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación de la Galería de Azure AD

una aplicación desde la Galería de Azure AD de hello tooconfigure debe:

-   [Agregar una aplicación de la Galería de Azure AD Hola](#add-an-application-from-the-Azure-AD-gallery)

-   [Configurar la aplicación hello para el inicio de sesión único en la contraseña](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Agregar una aplicación de la Galería de Azure AD Hola

tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:

1.  Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**.

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.

6.  Hola **escriba un nombre** cuadro de texto de hello **agregar a partir de la Galería de hello** sección, escriba un nombre de aplicación hello como Hola.

7.  Seleccionar aplicación hello tooconfigure que desee para el inicio de sesión único.

8.  Antes de agregar la aplicación hello, puede cambiar su nombre de hello **nombre** cuadro de texto.

9.  Haga clic en **agregar** button, aplicación de hello tooadd.

Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar la aplicación hello para el inicio de sesión único en la contraseña

tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Modo de hello seleccione **sesión basada en contraseña.**

9.  [Asignar usuarios de aplicación de toohello](#how-to-assign-a-user-to-an-application-directly).

10. Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola. En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación no Galería

una aplicación desde la Galería de Azure AD de hello tooconfigure debe:

-   [Incorporación de una aplicación ajena a la galería](#add-a-non-gallery-application)

-   [Configurar la aplicación hello para el inicio de sesión único en la contraseña](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>Incorporación de una aplicación ajena a la galería

tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:

1.  Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**.

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.

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

    1.  Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Modo de hello seleccione **sesión basada en contraseña.**

9.  Escriba hello **dirección URL de inicio de sesión**. Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a. Asegúrese de que está visible en la dirección URL de Hola Hola campos inicio de sesión.

10. Asignar a usuarios de aplicación de toohello.

11. Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola. En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.

## <a name="how-tooassign-a-user-tooan-application-directly"></a>¿Cómo tooassign directamente una aplicación de tooan de usuario

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

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Si estos pasos no Hola resuelva el problema de Hola. 

Abra una incidencia de soporte técnico con hello siguiente información si está disponible:

-   Id. de error de correlación

-   UPN (dirección de correo electrónico del usuario)

-   TenantID

-   Tipo de explorador

-   Zona horaria y hora/período de tiempo durante el que se produce el error

-   Seguimientos de Fiddler

## <a name="next-steps"></a>Pasos siguientes
[Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)
