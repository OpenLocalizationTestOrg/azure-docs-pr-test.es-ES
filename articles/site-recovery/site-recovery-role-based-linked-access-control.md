---
title: aaaUsing Role-Based Access Control toomanage Azure Site Recovery | Documentos de Microsoft
description: "Este artículo describe cómo tooapply y usar Control de acceso basado en roles (RBAC) toomanage las implementaciones de Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>Usar implementaciones de Azure Site Recovery toomanage de Control de acceso basado en roles

El control de acceso basado en roles (RBAC) de Azure permite realizar una administración detallada del acceso para Azure. Usar RBAC, puede separar las responsabilidades en el equipo y conceder solo toousers de permisos de acceso específico como trabajos específicos tooperform necesarios.

Azure Site Recovery proporciona 3 funciones integradas de las operaciones de administración de Site Recovery toocontrol. Más información sobre [roles integrados del control de acceso basado en rol de Azure](../active-directory/role-based-access-built-in-roles.md)

* [Colaborador de recuperación del sitio](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) -este rol tiene todas las operaciones de Azure Site Recovery de toomanage requiere permisos en un almacén de servicios de recuperación. Un usuario con este rol, sin embargo, no se puede crear o eliminar un almacén de servicios de recuperación o asignar el acceso a los usuarios de derechos tooother. Este rol es ideal para los administradores de recuperación ante desastres que pueden habilitar y administrar la recuperación ante desastres para las aplicaciones u organizaciones completas, como puede ser el caso de hello.
* [Operador de recuperación del sitio](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) -este rol tiene las operaciones de conmutación por error y conmutación por recuperación de tooexecute y el Administrador de permisos. Un usuario con este rol no se puede habilitar o deshabilitar la replicación, crear o eliminar almacenes, registrar la nueva infraestructura o asignar a usuarios de tooother de derechos de acceso. Este rol es ideal para un operador de recuperación ante desastres que puede conmutar por error desde máquinas virtuales o aplicaciones cuando se lo indican los propietarios de las aplicaciones y los administradores de TI en una situación desastrosa real o simulada, como un simulacro de recuperación ante desastres. POST resolución de desastre hello, operador de hello DR puede volver a proteger y conmutación por recuperación Hola máquinas virtuales.
* [Lector de recuperación del sitio](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) -este rol tiene permisos tooview todas las operaciones de administración de Site Recovery. Esta función es ideal para un ejecutivo de supervisión de TI que puede supervisar el estado actual de Hola de protección y provocar incidencias de soporte técnico si es necesario.

Si está pensando toodefine sus propios roles para tener un mayor control, vea cómo demasiado[crear roles personalizados](../active-directory/role-based-access-control-custom-roles.md) en Azure.

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>Permisos necesarios tooEnable replicación para nuevas máquinas virtuales
Cuando una máquina Virtual nueva es tooAzure replicado mediante Azure Site Recovery, niveles de acceso del usuario de hello asociado son tooensure validado que Hola usuario Hola necesario permisos toouse Hola recursos de Azure proporciona tooSite recuperación.

tooenable la replicación para una nueva máquina virtual, debe tener un usuario:
* Permiso toocreate una máquina virtual en el grupo de recursos seleccionado Hola
* Permiso toocreate una máquina virtual en la red virtual seleccionada de Hola
* Permiso toowrite toohello seleccionado cuenta de almacenamiento

Un usuario necesita Hola después de la replicación de toocomplete de permisos de una nueva máquina virtual.

> [!IMPORTANT]
>Asegúrese de que los permisos relevantes se agregan por modelo de implementación de hello (Administrador de recursos / clásico) utilizado para la implementación de recursos.

| **Tipo de recurso** | **Modelo de implementación** | **Permiso** |
| --- | --- | --- |
| Proceso | Resource Manager | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | Clásico | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| Red | Resource Manager | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | Clásico | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| Almacenamiento | Resource Manager | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | Clásico | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| Grupo de recursos | Resource Manager | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

Considere el uso de hello 'Colaborador de la máquina Virtual' y 'Colaborador clásico de máquina Virtual' [roles integrados](../active-directory/role-based-access-built-in-roles.md) para la implementación del Administrador de recursos y clásico modela respectivamente.

## <a name="next-steps"></a>Pasos siguientes
* [Control de acceso basado en roles](../active-directory/role-based-access-control-configure.md): comience a usar RBAC en hello portal de Azure.
* Obtenga información acerca de cómo tener acceso toomanage con:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [CLI de Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [API DE REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Solución de problemas del control de acceso basado en roles](../active-directory/role-based-access-control-troubleshooting.md): sugerencias para resolver problemas frecuentes.
