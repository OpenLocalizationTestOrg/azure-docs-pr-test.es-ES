---
title: aaaHow tooadd o quitar un rol de usuario | Documentos de Microsoft
description: "Obtenga información acerca de cómo las identidades de tooadd roles tooprivileged con Hola aplicación de Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a>AD Privileged Identity Management de Azure: ¿Cómo tooadd o quitar un rol de usuario
Con Azure Active Directory (AD), un administrador global (o el Administrador de la compañía) puede actualizar los usuarios **permanentemente** asignado tooroles en Azure AD. Para ello, se usan cmdlets de PowerShell, como `Add-MsolRoleMember` y `Remove-MsolRoleMember`. O pueden utilizar Hola portal de Azure clásico como se describe en [asignar roles de administrador en Azure Active Directory](active-directory-assign-admin-roles.md).

Hola aplicación de Azure AD Privileged Identity Management permite a los administradores de roles con privilegios las asignaciones de roles permanente de toomake, también. Además, los administradores de rol con privilegios pueden hacer que los usuarios sean **aptos** para roles de administrador. Un administrador elegible puede activar el rol de hello cuando lo necesitan y, a continuación, sus permisos expiran una vez que haya terminado.

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a>Administrar los roles con PIM en hello portal de Azure
En su organización, puede asignar roles administrativos de toodifferent de usuarios en Azure AD, aplicaciones y servicios de Microsoft Office 365 y otros.  Encontrará más detalles sobre los roles disponibles de hello en [Roles en Azure AD PIM](active-directory-privileged-identity-management-roles.md).

tooadd o quitar un usuario de una función utilizando la administración de identidad con privilegios, Mostrar panel PIM Hola. A continuación, haga clic en hello **los usuarios de Roles de administrador** botón, o seleccione un rol específico (por ejemplo, un administrador Global) de tabla de funciones de Hola.

> [!NOTE]
> Si aún no ha habilitado PIM Hola portal de Azure, vaya demasiado[empezar a trabajar con Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) para obtener más información.

Si desea toogive otro tooPIM de acceso de usuario propio, roles de Hola que PIM requiere hello toohave de usuario se describen con mayor detalle en [cómo toogive a tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="add-a-user-tooa-role"></a>Agregar un rol de usuario tooa
1. Hola [portal de Azure](https://portal.azure.com/), seleccione hello **Azure AD Privileged Identity Management** icono Panel de Hola.
2. Seleccione **Administrar roles con privilegios**.
3. Hola **resumen de funciones** tabla, seleccione Hola un rol que desee toomanage.
4. En la hoja de rol de hello, seleccione **agregar**.
5. Haga clic en **Seleccionar usuarios** y búsqueda para los usuarios Hola Hola **Seleccionar usuarios** hoja.  
6. Seleccione el usuario de Hola de lista de resultados de búsqueda de Hola y haga clic en **realiza**.
7. Haga clic en **Aceptar** toosave la selección. usuario de Hola que ha seleccionado se mostrará en lista de hello como aptos para su rol de Hola.

> [!NOTE]
> Nuevos usuarios en un rol solo son aptos para la función hello de forma predeterminada. Si quiere que toomake Hola rol permanente, haga clic en usuario de hello en lista de Hola. información del usuario de Hello aparecerá en una nueva hoja. Seleccione **Asegúrese perm** en el menú de información de usuario de Hola.  
> Si un usuario no se puede registrar para Azure Multi-factor Authentication (MFA), o está usando una cuenta de Microsoft (normalmente @outlook.com), deberá toomake ellos permanentes en todas sus funciones. Los administradores pueden se piden tooregister MFA durante la activación.

Ahora que hello usuario es apto para un rol, hágales saber que pueden activar, según las instrucciones de toohello en [cómo tooactivate o desactivar un rol](active-directory-privileged-identity-management-how-to-activate-role.md).

## <a name="remove-a-user-from-a-role"></a>Eliminación de un usuario de un rol
Puede quitar a los usuarios de las asignaciones de rol apto, pero asegúrese de que siempre haya al menos un usuario que sea un administrador global permanente.

Siga estos tooremove pasos un usuario específico de un rol:

1. Navegue toohello rol en la lista de funciones de hello seleccionando un rol en el panel de PIM de Azure AD de Hola o haciendo clic en hello **a los usuarios en Roles de administrador** botón.
2. Haga clic en usuario de hello en la lista de usuarios de Hola.
3. Haga clic en **Quitar**. Un mensaje le preguntará si tooconfirm.
4. Haga clic en **Sí** rol de hello tooremove de usuario de Hola.

Si no está seguro de qué usuarios sigue necesitan sus asignaciones de roles, también puede [iniciar una revisión de acceso para el rol de hello](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

