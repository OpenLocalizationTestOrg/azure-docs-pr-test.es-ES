---
title: "Administración de copias de seguridad con el control de acceso basado en roles de Azure | Microsoft Docs"
description: "Usar operaciones de administración de Control de acceso basado en roles toomanage acceso toobackup en el almacén de servicios de recuperación."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 3bd46b97-4b29-47a5-b5ac-ac174dd36760
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: trinadhk;markgal
ms.openlocfilehash: 26d034d152f9b77fc6d5b2ffd5ef2648b1797f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a>Usar puntos de recuperación de copia de seguridad de Azure de toomanage de Control de acceso basado en roles
El control de acceso basado en roles (RBAC) de Azure permite realizar una administración detallada del acceso para Azure. Usar RBAC, puede separar los derechos en el equipo y conceder solo Hola mucha toousers de acceso que necesitan tooperform sus trabajos.

> [!IMPORTANT]
> Roles proporcionados por la copia de seguridad de Azure son tooactions limitado que se pueden realizar en el portal de Azure o cmdlets de PowerShell del almacén de servicios de recuperación. Las acciones realizadas en la IU del cliente del agente de Azure Backup, en la IU de System Center Data Protection Manager o en la IU del Azure Backup Server están fuera del control de estos roles.

Copia de seguridad de Azure proporciona 3 funciones integradas de operaciones de copia de seguridad de administración de toocontrol. Más información sobre [roles integrados del control de acceso basado en rol de Azure](../active-directory/role-based-access-built-in-roles.md)

* [Colaborador de copia de seguridad](../active-directory/role-based-access-built-in-roles.md#backup-contributor) -este rol tiene toocreate de todos los permisos y administrar copias de seguridad excepto crear almacén de servicios de recuperación y que proporciona acceso tooothers. Imagine este rol como administrador de copias de seguridad que puede realizar todas las operaciones de administración de copia de seguridad.
* [Operador de copia de seguridad](../active-directory/role-based-access-built-in-roles.md#backup-operator) -este rol tiene tooeverything permisos excepto un colaborador de eliminación de directivas de copia de seguridad de copia de seguridad y administración. Esta función es equivalente toocontributor salvo que no se puede realizar operaciones destructivas como detener copia de seguridad con datos de eliminación o quitar el registro de recursos locales.
* [Lector de copia de seguridad](../active-directory/role-based-access-built-in-roles.md#backup-reader) -este rol tiene permisos tooview todas las operaciones de copia de seguridad de administración. Imagine este toobe rol una persona de supervisión.

Si está pensando toodefine sus propios roles para tener un mayor control, vea cómo demasiado[crear roles personalizados](../active-directory/role-based-access-control-custom-roles.md) en RBAC de Azure.



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a>Asignación de acciones de administración de toobackup de funciones integradas de copia de seguridad
Hello en la tabla siguiente captura acciones de administración de copia de seguridad de Hola y correspondiente rol RBAC mínimo necesario tooperform esa operación.

| Operación de administración | Rol RBAC mínimo necesario |
| --- | --- |
| Crear almacén de Recovery Services | Colaborador en el grupo de recursos del almacén |
| Habilitar la copia de seguridad de VM de Azure | Operador de copia de seguridad en el almacén, colaborador de máquina virtual en VM |
| Copia de seguridad a petición de VM | Operador de copia de seguridad |
| Restaurar VM | Operador de copia de seguridad, colaborador de grupo de recursos en el que VM y redes virtuales van tooget implementado |
| Restaurar discos y archivos individuales a partir de la copia de seguridad de VM | Operador de copia de seguridad |
| Crear directiva de copia de seguridad para copia de seguridad de VM de Azure | Colaborador de copia de seguridad |
| Modificar directiva de copia de seguridad de copia de seguridad de VM de Azure | Colaborador de copia de seguridad |
| Eliminar directiva de copia de seguridad de copia de seguridad de VM de Azure | Colaborador de copia de seguridad |
| Detener copia de seguridad (con retención de datos o eliminación de datos) en copia de seguridad de VM | Colaborador de copia de seguridad |
| Registrar Windows Server, cliente o SCDPM local o Azure Backup Server | Operador de copia de seguridad |
| Eliminar Windows Server, cliente o SCDPM local registrado o Azure Backup Server | Colaborador de copia de seguridad |

## <a name="next-steps"></a>Pasos siguientes
* [Control de acceso basado en roles](../active-directory/role-based-access-control-configure.md): comience a usar RBAC en hello portal de Azure.
* Obtenga información acerca de cómo tener acceso toomanage con:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [CLI de Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [API DE REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Solución de problemas del control de acceso basado en roles](../active-directory/role-based-access-control-troubleshooting.md): sugerencias para resolver problemas frecuentes.
