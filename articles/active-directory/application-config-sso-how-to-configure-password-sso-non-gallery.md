---
title: "aaaHow tooconfigure contraseña inicio de sesión único para una galería no applicationn | Documentos de Microsoft"
description: "Cómo tooconfigure una aplicación no galería personalizada para proteger basada en contraseña de inicio de sesión único cuando no se encuentra en hello Galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación no Galería

Además opciones toohello encuentra Galería de aplicaciones de hello Azure AD, también tiene Hola opción tooadd una **aplicación no gallery** cuando aplicación Hola que desea no aparece. Con esta capacidad, puede agregar todas las aplicaciones que ya existe en su organización, o cualquier aplicación de terceros que puedan usar desde un proveedor que ya no forma parte del programa Hola a [Galería de aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

Una vez que agregue una aplicación no galería, puede configurar solo inicio de sesión método hello esta aplicación utiliza seleccionando hello **Single Sign-on** elemento de navegación en una aplicación empresarial de hello [Portal de Azure ](https://portal.azure.com/).

Uno de hello Single Sign-on métodos disponible tooyou es hello [basado en contraseña Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opción. Con hello **agregar una aplicación de la Galería no** experiencia, puede integrar cualquier aplicación que representa un nombre de usuario basado en HTML y la contraseña de entrada de campo, incluso si no está en nuestro conjunto de aplicaciones previamente integradas.

Esto funciona de manera de Hello es una página de barrido de tecnología que forma parte del programa Hola a extensión del Panel de acceso que nos permite tooauto-se detectan los campos de entrada de nombre de usuario y contraseña, almacene de forma segura para la instancia de la aplicación específica. A continuación, reproduzca de forma segura nombres de usuario y campos de toothose las contraseñas cuando un usuario navega toothat aplicación en el panel de acceso de aplicación Hola.

Se trata de una excelente manera de tooget a integrar rápidamente cualquier tipo de aplicación en Azure AD y le permite:

-   Integrar **cualquier aplicación de Hola a todos** con el inquilino de Azure AD, siempre y cuando se representa un campo de entrada de usuario y la contraseña HTML

-   Habilitar **inicio de sesión único para los usuarios** por almacenar de forma segura y reproducir los nombres de usuario y contraseñas de aplicación hello ha integrado con Azure AD

-   **La detección automática de entrada** campos para cualquier aplicación y le permiten toomanually detectar esos campos mediante Hola extensión de explorador del Panel de acceso, en caso de que la detección automática no encontrarlos

-   **Compatibilidad con aplicaciones que requieren varios campos de inicio de sesión** para aplicaciones que requieren algo más que simplemente username y password campos toosign en

-   **Personalizar las etiquetas de hello** Hola username y password de campos de entrada, los usuarios verán en hello [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) cuando escriban sus credenciales

-   Permitir la **usuarios** tooprovide sus propios nombres de usuario y contraseñas para cuentas de aplicación existente que está escribiendo en manualmente en hello [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   Permitir que un **miembro del grupo de negocios de hello** contraseñas y nombres de usuario de hello toospecify asignan tooa usuario mediante hello [autoservicio acceso a la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) característica

-   Permitir que un **administrador** toospecify Hola nombres y contraseñas asignadas tooa usuario mediante las credenciales de actualización de hello característica cuando [asignar una aplicación de usuario tooan](#_How_to_configure_1)

-   Permitir que un **administrador** toospecify Hola compartido username o la contraseña utilizada por un grupo de personas mediante las credenciales de actualización de hello característica cuando [asignar una aplicación de tooan de grupo](#assign-an-application-to-a-group-directly)

A continuación se describe cómo habilitar [basado en contraseña Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) aplicación tooany agregar utilizando hello **agregar una aplicación de la Galería no** experimentar.

## <a name="overview-of-steps-required"></a>Introducción a los pasos necesarios

una aplicación desde la Galería de Azure AD de hello tooconfigure debe:

-   [Incorporación de una aplicación ajena a la galería](#add-a-non-gallery-application)

-   [Configurar la aplicación hello para el inicio de sesión único en la contraseña](#configure-the-application-for-password-single-sign-on)

-   [Asignar Hola aplicación tooa usuario o un grupo](#assign-the-application-to-a-user-or-a-group)

    -   [Asignar una aplicación de usuario tooan directamente](#assign-a-user-to-an-application-directly)

    -   [Asignar a un grupo de tooa aplicación directamente](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a>Incorporación de una aplicación ajena a la galería

tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:

1.  Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja

6.  Haga clic en **Aplicación situada fuera de la galería**.

7.  Escriba el nombre de saludo de la aplicación Hola **nombre** cuadro de texto. Seleccione **Agregar**.

Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.

## <a name="configure-hello-application-for-password-single-sign-on"></a>Configurar la aplicación hello para el inicio de sesión único en la contraseña

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

9.  Escriba hello **dirección URL de inicio de sesión**. Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a. Asegúrese de que está visible en la dirección URL de Hola Hola campos inicio de sesión.

10. Asignar a usuarios de aplicación de toohello.

11. Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola. En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.

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
