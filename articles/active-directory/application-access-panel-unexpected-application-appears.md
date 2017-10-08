---
title: las aplicaciones aaaHow aparecen en el panel de acceso de hello | Documentos de Microsoft
description: "Solucionar problemas de por qué aparece una aplicación Hola Panel de acceso"
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>Cómo aparecen las aplicaciones en el panel de acceso de Hola

Hola Panel de acceso es un portal basado en web que permite a los usuarios con un trabajo o cuenta educativa en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que Hola Administrador de Azure AD le haya concedido acceso a. Estas aplicaciones se configuran en nombre de usuario de hello en el portal de Azure AD Hola. Hola, administrador puede aprovisionar directamente usuario de toohello la aplicación Hola o un grupo de tooa que un usuario forma parte de lo que en la aplicación hello que aparecen en el Panel de acceso del usuario de Hola.

## <a name="general-issues-toocheck-first"></a>General emite toocheck primero

-   Si se acaba de quitar una aplicación de un usuario o grupo Hola usuario es miembro de, toosign de entrada y salida vuelva a intentarlo en el Panel de acceso del usuario de hello después de unos toosee minutos si se quita la aplicación hello.

-   Si se acaba de quitar una licencia a un usuario o grupo de usuario de hello es que un miembro de este puede tardar mucho tiempo, según el tamaño de Hola y la complejidad del grupo de Hola para toobe cambios realizado. Permitir un tiempo adicional antes de iniciar sesión en el Panel de acceso de Hola.

## <a name="problems-related-tooassigning-applications-toousers"></a>Problemas relacionados tooassigning aplicaciones toousers

Un usuario puede estar viendo una aplicación en su Panel de acceso porque le asignase previamente tooit. A continuación se muestran algunas maneras toocheck:

-   [Comprobar si un usuario se ha asignado toohello aplicación](#check-if-a-user-is-assigned-to-the-application)

-   [Comprobar si un usuario está sometido a una licencia relacionados con la aplicación toohello](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a>Comprobar si un usuario se ha asignado toohello aplicación

toocheck si se asigna a un usuario toohello aplicación, siga Hola pasos siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

6.  **Búsqueda** como nombre de Hola de aplicación hello en cuestión.

7.  Haga clic en **Usuarios y grupos**.

8.  Compruebe toosee si el usuario se le asigna la aplicación toohello.

  * Si desea que tooremove Hola usuario de la aplicación hello, **haga clic en la fila de hello** del usuario de Hola y seleccione **eliminar**.

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Comprobar si un usuario está sometido a una licencia relacionados con la aplicación toohello

toocheck un usuario había asignado licencias, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.

   * Si se asigna la licencia de Office tooan Esto activar tooappear de las aplicaciones de Office de primera entidad de usuario de Hola Hola Panel de acceso del usuario.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Problemas relacionados tooassigning aplicaciones toogroups

Un usuario puede estar viendo una aplicación en su Panel de acceso ya que forman parte de un grupo que se ha asignado la aplicación hello. A continuación se muestran algunas maneras toocheck:

-   [Comprobar la pertenencia a grupos de un usuario](#check-a-users-group-memberships)

-   [Comprobar si un usuario es miembro de un grupo asignado tooa licencia](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>Comprobar la pertenencia a grupos de un usuario

toocheck pertenencia de un grupo, siga los pasos de Hola a continuación:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **Grupos**.

8.  Compruebe toosee si el usuario es parte de una aplicación de toohello de grupo asignado.

   * Si desea que tooremove Hola usuario del grupo de hello, **haga clic en la fila de hello** del grupo de Hola y seleccione Eliminar.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>Comprobar si un usuario es miembro de un grupo asignado tooa licencia

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **usuarios y grupos** en el menú de navegación de Hola.

5.  Haga clic en **Todos los usuarios**.

6.  **Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.

7.  Haga clic en **Grupos**.

8.  Haga clic en la fila de Hola de un grupo específico.

9.  Haga clic en **licencias** toosee qué grupo de licencias Hola asignó tooit.

  * Si se asigna el grupo de hello licencia de Office tooan en que esto, puede habilitar determinada tooappear de las aplicaciones de Office de primera entidad Hola Panel de acceso del usuario.


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Si estos pasos no Hola resolver el problema de Hola

Abra una incidencia de soporte técnico con hello siguiente información si está disponible:

-   Id. de error de correlación

-   UPN (dirección de correo electrónico del usuario)

-   Id. de inquilino

-   Tipo de explorador

-   Zona horaria y hora/período de tiempo durante el que se produce el error

-   Seguimientos de Fiddler

## <a name="next-steps"></a>Pasos siguientes
[Administración de aplicaciones con Azure Active Directory](active-directory-enable-sso-scenario.md)
