---
title: Control de acceso basado en aaaRole Hola portal de Azure | Documentos de Microsoft
description: "Introducción a administración de acceso con Control de acceso basado en roles en hello Portal de Azure. Usar los recursos de rol asignaciones tooassign permisos tooyour."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a>Usar recursos de suscripción de Azure de Role-Based Access Control toomanage acceso tooyour
> [!div class="op_single_selector"]
> * [Administración del acceso por usuario o grupo](role-based-access-control-manage-assignments.md)
> * [Administrar el acceso por recurso](role-based-access-control-configure.md)

El control de acceso basado en roles (RBAC) de Azure permite realizar una administración detallada del acceso para Azure. Usar RBAC, puede conceder únicamente cantidad de Hola de acceso que los usuarios necesitan tooperform sus trabajos. En este artículo le ayuda a ponerse en marcha con RBAC en hello portal de Azure. Si desea más detalles sobre cómo RBAC ayuda a administrar el acceso, consulte [¿Qué es el control de acceso basado en rol?](role-based-access-control-what-is.md)

Dentro de cada suscripción, puede conceder too2000 asignaciones de rol. 

## <a name="view-access"></a>Vista de acceso
Puede ver quién tiene acceso tooa recursos, grupo de recursos o suscripción de su hoja principal en hello [portal de Azure](https://portal.azure.com). Por ejemplo, queremos toosee que tenga acceso tooone nuestro de grupos de recursos:

1. Seleccione **grupos de recursos** en barra de navegación de Hola Hola izquierda.  
    ![Grupos de recursos - icono](./media/role-based-access-control-configure/resourcegroups_icon.png)
2. Nombre seleccione Hola Hola del grupo de recursos de hello **grupos de recursos** hoja.
3. Seleccione **(de índices IAM) de control de acceso** desde el menú de la izquierda Hola.  
4. hoja de control de acceso de Hello enumera todos los usuarios, grupos y las aplicaciones que se han concedido el grupo de recursos de toohello de acceso.  
   
    ![Hoja de usuarios: acceso heredado frente a asignado (captura de pantalla)](./media/role-based-access-control-configure/view-access.png)

Tenga en cuenta que algunos roles tienen como ámbito demasiado**este recurso** mientras que otras son **Inherited** desde otro ámbito. Acceso se asigna a específicamente el grupo de recursos toohello o se hereda de una suscripción de asignación toohello primario.

> [!NOTE]
> Los administradores de suscripciones clásico y coadministradores se consideran los propietarios de suscripción de hello en el nuevo modelo de RBAC Hola.

## <a name="add-access"></a>Agregación de acceso
Conceder acceso desde dentro de recurso de hello, grupo de recursos o suscripción de ámbito de Hola Hola de asignación de roles.

1. Seleccione **agregar** en el módulo de control de acceso de Hola.  
2. Rol de hello SELECT que desea tooassign de hello **seleccione un rol** hoja.
3. Seleccione usuario hello, grupo o aplicación en el directorio que desee toogrant acceso a. Puede buscar directorio de hello con nombres para mostrar, direcciones de correo electrónico y los identificadores de objeto.  
   
    ![Hoja Agregar usuarios: búsqueda (captura de pantalla)](./media/role-based-access-control-configure/grant-access2.png)
4. Seleccione **Aceptar** asignación de hello toocreate. Hola **Agregar usuario** emergente realiza un seguimiento de progreso de Hola.  
    ![Barra de progreso Agregando usuario: captura de pantalla](./media/role-based-access-control-configure/addinguser_popup.png)

Después de agregar correctamente una asignación de roles, que aparecerá en hello **usuarios** hoja.

## <a name="remove-access"></a>Eliminación de acceso
1. Mantenga el cursor sobre el nombre de asignación de Hola que desea tooremove Hola. Nombre de toohello siguiente aparece una casilla.
2. Usar Hola casillas tooselect uno o más asignaciones de roles.
2. Seleccione **Quitar**.  
3. Seleccione **Sí** eliminación de hello tooconfirm.

Las asignaciones heredadas no se pueden quitar. Si necesita tooremove una asignación heredada, deberá toodo en hello ámbito donde se creó la asignación de roles de Hola. Hola **ámbito** columna, junto demasiado**Inherited** hay un vínculo que le guíe toohello recursos que se asignó este rol. Vaya a la lista de recursos de toohello asignación de roles de tooremove Hola.

![Hoja de usuario: acceso heredado deshabilita el botón de eliminación (captura de pantalla)](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a>Acceso a toomanage de otra herramientas
Puede asignar roles y administrar el acceso con comandos de RBAC de Azure en herramientas distintas Hola portal de Azure.  Siga Hola vínculos toolearn más información acerca de los requisitos previos de Hola y empezar a trabajar con comandos de hello RBAC de Azure.

* [Azure PowerShell](role-based-access-control-manage-access-powershell.md)
* [Interfaz de la línea de comandos de Azure](role-based-access-control-manage-access-azure-cli.md)
* [API DE REST](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a>Pasos siguientes
* [Creación de un informe del historial de cambios de acceso](role-based-access-control-access-change-history-report.md)
* Vea hello [funciones integradas de RBAC](role-based-access-built-in-roles.md)
* Defina sus propios [Custom Roles in Azure RBAC](role-based-access-control-custom-roles.md)

