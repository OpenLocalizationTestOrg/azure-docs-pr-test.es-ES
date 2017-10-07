---
title: "aaaHow tooconfigure contraseña inicio de sesión único para una aplicación de la Galería de Azure AD | Documentos de Microsoft"
description: "Cómo tooconfigure una aplicación para proteger basada en contraseña de inicio de sesión único cuando ya se incluye en hello Galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación de la Galería de Azure AD

Cuando se agrega una aplicación de hello [Galería de aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), tiene la opción de Hola de cómo desea que su toosign a los usuarios de aplicación de toothat. Puede configurar esta opción en cualquier momento seleccionando hello **Single Sign-on** elemento de navegación en una aplicación empresarial de hello [Portal de Azure](https://portal.azure.com/).

Uno de tooyou disponible de métodos de inicio de sesión único de hello es hello [basado en contraseña Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opción. Se trata de una excelente manera de tooget a integrar aplicaciones en Azure AD rápidamente y le permite:

-   Habilitar **inicio de sesión único para los usuarios** por almacenar de forma segura y reproducir los nombres de usuario y contraseñas de aplicación hello ha integrado con Azure AD

-   **Compatibilidad con aplicaciones que requieren varios campos de inicio de sesión** para aplicaciones que requieren algo más que simplemente username y password campos toosign en

-   **Personalizar las etiquetas de hello** Hola username y password de campos de entrada, los usuarios verán en hello [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) cuando escriban sus credenciales

-   Permitir la **usuarios** tooprovide sus propios nombres de usuario y contraseñas para cuentas de aplicación existente que está escribiendo en manualmente en hello [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   Permitir que un **miembro del grupo de negocios de hello** contraseñas y nombres de usuario de hello toospecify asignan tooa usuario mediante hello [autoservicio acceso a la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) característica

-   Permitir que un **administrador** toospecify Hola nombres y contraseñas asignadas tooa usuario mediante las credenciales de actualización de hello característica cuando [asignar una aplicación de usuario tooan](#assign-a-user-to-an-application-directly)

-   Permitir que un **administrador** toospecify Hola compartido username o la contraseña utilizada por un grupo de personas mediante las credenciales de actualización de hello característica cuando [asignar una aplicación de tooan de grupo](#assign-an-application-to-a-group-directly)

A continuación se describe cómo habilitar [basado en contraseña Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan aplicación que ya está en hello [Galería de aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

## <a name="overview-of-steps-required"></a>Introducción a los pasos necesarios
una aplicación desde la Galería de Azure AD de hello tooconfigure debe:

-   [Agregar una aplicación de la Galería de Azure AD Hola](#add-an-application-from-the-azure-ad-gallery)

-   [Configurar la aplicación hello para el inicio de sesión único en la contraseña](#configure-the-application-for-password-single-sign-on)

-   [Asignar Hola aplicación tooa usuario o un grupo](#assign-the-application-to-a-user-or-a-group)

    -   [Asignar una aplicación de usuario tooan directamente](#assign-a-user-to-an-application-directly)

    -   [Asignar a un grupo de tooa aplicación directamente](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Agregar una aplicación de la Galería de Azure AD Hola

tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:

1.  Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja

6.  Hola **escriba un nombre** cuadro de texto de hello **agregar a partir de la Galería de hello** sección, escriba un nombre Hola de aplicación hello

7.  Seleccionar aplicación hello tooconfigure que desee para el inicio de sesión único

8.  Antes de agregar la aplicación hello, puede cambiar su nombre de hello **nombre** cuadro de texto.

9.  Haga clic en **agregar** button, aplicación de hello tooadd.

Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.

## <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar la aplicación hello para el inicio de sesión único en la contraseña

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

9.  [Asignar usuarios de aplicación de toohello](#assign-a-user-to-an-application-directly).

10. Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola. En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.

## <a name="assign-a-user-tooan-application-directly"></a>Asignar una aplicación de usuario tooan directamente

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

## <a name="assign-an-application-tooa-group-directly"></a>Asignar a un grupo de tooa aplicación directamente

tooassign uno o más grupos de aplicación de tooan directamente, siga los pasos de Hola a continuación:

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

10. Tipo de hello **nombre de grupo completa** del grupo de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.

11. Mantenga el mouse sobre hello **grupo** en hello lista tooreveal una **casilla**. Haga clic en tooadd de foto o el logotipo de perfil de hello casilla siguiente toohello del grupo su usuario toohello **seleccionados** lista.

12. **Opcional:** si lo desea demasiado**agregar más de un grupo**, tipo de otro **nombre de grupo completa** en hello **buscar por nombre o dirección de correo** cuadro de búsqueda, y haga clic en hello casilla tooadd este grupo toohello **seleccionados** lista.

13. Cuando haya terminado la selección de grupos, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.

14. **Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** grupos hoja tooselect una toohello tooassign de rol que ha seleccionado.

15. Haga clic en hello **asignar** botón tooassign Hola aplicación toohello grupos seleccionados.

Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.

## <a name="next-steps"></a>Pasos siguientes
[Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)
