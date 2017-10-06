---
title: asignaciones de acceso de recursos de Azure aaaView | Documentos de Microsoft
description: Ver y administrar todas las asignaciones de Control de acceso basado en roles de Hola para cualquier usuario o grupo en hello portal de Azure
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a>Ver las asignaciones de acceso para usuarios y grupos en hello portal de Azure
> [!div class="op_single_selector"]
> * [Administración del acceso por usuario o grupo](role-based-access-control-manage-assignments.md)
> * [Administración del acceso por recurso](role-based-access-control-configure.md)

Con control de acceso basado en roles (RBAC) en hello Azure Active Directory (Azure AD), puede administrar el acceso tooyour Azure recursos. 

Acceso asignado con RBAC es específica porque hay dos maneras puede limitar los permisos de hello:

* **Ámbito:** las asignaciones de roles RBAC son suscripción específica de tooa con ámbito, el grupo de recursos o el recurso. Un usuario tiene acceso tooa único recurso no puede tener acceso a otros recursos en hello misma suscripción.
* **Rol:** en el ámbito de Hola de asignación de hello, se restringe el acceso aún más mediante la asignación de un rol. Los roles pueden ser generales, como propietarios, o específicos, como lectores de máquina virtual.

Roles solo pueden asignarse desde dentro de la suscripción de hello, el grupo de recursos o el recurso que es el ámbito de hello para la asignación de Hola. Pero puede ver todas las asignaciones de acceso de Hola para un usuario determinado o un grupo en un único lugar. Puede tener hasta las asignaciones de roles de too2000 en cada suscripción. 

Obtener más información acerca de cómo demasiado[usar recursos de suscripción de Azure de rol asignaciones toomanage acceso tooyour](role-based-access-control-configure.md).

## <a name="view-access-assignments"></a>Visualización de asignaciones de acceso
toolook asignaciones de acceso de Hola para un único usuario o grupo, iniciar en Azure Active Directory en hello [portal de Azure](http://portal.azure.com).

1. Seleccione **Azure Active Directory**. Si esta opción no está visible en la lista de navegación, seleccione **más servicios** y, a continuación, desplácese hacia abajo toofind **Azure Active Directory**.
2. Seleccione **Usuarios y grupos** y luego **Todos los usuarios** o **Todos los grupos**. En este ejemplo, nos centramos en los usuarios individuales.
    ![Captura de pantalla de administración de usuarios y grupos en Azure Active Directory](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)
3. Buscar usuario Hola por nombre o nombre de usuario.
4. Seleccione **recursos de Azure** en la hoja de usuario de Hola. Aparecen todas las asignaciones de acceso de Hola para dicho usuario.

### <a name="read-permissions-tooview-assignments"></a>Asignaciones de tooview de permisos de lectura
Esta página solo muestra las asignaciones de acceso de Hola que dispone de permiso tooread. Por ejemplo, puede tener acceso de lectura toosubscription A y seguir toocheck de hoja de recursos de Azure toohello las asignaciones de usuario. Puede ver sus asignaciones de acceso de la suscripción A, pero no verá que también tiene asignaciones de acceso de la B.

## <a name="delete-access-assignments"></a>Eliminación de asignaciones de acceso
En esta hoja, puede eliminar asignaciones de acceso que se asignaron directamente tooa usuario o grupo. Si la asignación de acceso de Hola se heredó de un grupo primario, es necesario toogo toohello recursos o suscripción y administrar una asignación de hello no existe.

1. En lista de Hola de todas las asignaciones de acceso de Hola para un usuario o grupo, seleccione Hola uno desea toodelete.
2. Seleccione **quitar** y, a continuación, **Sí** tooconfirm.
    ![Captura de pantalla de eliminación de asignación de acceso](./media/role-based-access-control-manage-assignments/delete_assignment.png)

## <a name="next-steps"></a>Pasos siguientes

* Empezar a trabajar con el Control de acceso basado en roles demasiado[usar recursos de rol asignaciones toomanage acceso tooyour suscripción de Azure](role-based-access-control-configure.md)
* Vea hello [funciones integradas de RBAC](role-based-access-built-in-roles.md)

