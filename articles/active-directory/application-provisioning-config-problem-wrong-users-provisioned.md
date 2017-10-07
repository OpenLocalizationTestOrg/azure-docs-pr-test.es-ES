---
title: "aplicación de la Galería de tooan aprovisionado Azure AD que se aaaWrong conjunto de usuarios | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toofind out ¿por qué se va un conjunto diferente de los usuarios aprovisionados tooan aplicación a los que esperaba"
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
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Un conjunto de usuarios erróneo se están aprovisionados tooan Azure AD Galería aplicación

Qué usuarios son aprovisionados toohello aplicación se basa principalmente en qué usuarios y grupos que han sido **asignado** toohello aplicación.

Usar recursos de hello situados por debajo de toolearn cómo toocheck qué usuarios y grupos se han asignado tooan aplicación en Azure Active Directory.

## <a name="assign-a-user-directly-as-an-administrator"></a>Asignación de un usuario directamente como administrador

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

Si se configura el aprovisionamiento y ya está ejecutando para una aplicación, los nuevos usuarios deben ser aplicación tooan aprovisionado en aproximadamente 10 minutos. Comprobar hello **los registros de auditoría** para obtener más información.

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a>Asignar un grupo directamente tooan aplicación como administrador

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

Si el aprovisionamiento es configurado y ya se está ejecutando para una aplicación, nuevos usuarios incluidos en el grupo de hello deben ser tooan aprovisionado en aproximadamente 10 minutos. Comprobar hello **los registros de auditoría** para obtener más información.

>[!IMPORTANT]
>Aprovisionamiento de Hola nombre del grupo y del grupo de detalles, en los miembros de suma toohello, si admiten para algunas aplicaciones. Puede habilitar o deshabilitar esta funcionalidad habilitando o deshabilitando hello **asignación** para los objetos de grupo se muestra en hello **Provisioning** ficha. 
>
>

Si está habilitado el aprovisionamiento de grupos, asegúrese de tooreview Hola atributo asignaciones tooensure un campo correspondiente se utiliza para saludo "Id. de búsqueda de coincidencias". Esto puede ser el nombre para mostrar hello o correo electrónico alias, como hello grupo y sus miembros no se aprovisionan si ninguna propiedad coincidente con hello está vacía o no rellena para un grupo en Azure AD.

## <a name="next-steps"></a>Pasos siguientes
[Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones con Azure Active Directory](active-directory-saas-app-provisioning.md)
