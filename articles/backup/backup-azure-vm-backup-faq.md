---
title: "Preguntas más frecuentes de copia de seguridad de máquina virtual aaaAzure | Documentos de Microsoft"
description: "Responde a las preguntas de toocommon sobre: cómo funciona de copia de seguridad de máquina virtual de Azure, limitaciones y qué ocurre cuando se producen cambios toopolicy"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "copia de seguridad de máquinas virtuales de azure, restauración de máquinas virtuales de azure, directiva de copia de seguridad"
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a>Preguntas sobre Hola servicio de copia de seguridad de máquina virtual de Azure
Este artículo tiene respuestas toocommon preguntas toohelp rápidamente entender los componentes de copia de seguridad de Azure VM Hola. En algunas de las respuestas de hello, hay artículos de toohello vínculos que tienen información completa. También puede publicar preguntas sobre Hola servicio de copia de seguridad de Azure en hello [foro de discusión](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Configuración de la copia de seguridad
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>¿Admiten los almacenes de Servicios de recuperación máquinas virtuales implementadas con el modelo clásico o máquinas virtuales implementadas con Resource Manager? <br/>
Los almacenes de Servicios de recuperación admiten ambos modelos.  Puede realizar copias de seguridad de una máquina virtual clásica (creado en el portal clásico de hello) o un tooa VM Administrador de recursos (creado en el portal de Azure hello) del almacén de servicios de recuperación.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a>¿Qué configuraciones no se admiten en la copia de seguridad de máquinas virtuales de Azure?
Consulte los [sistemas operativos admitidos](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) y las [limitaciones de la copia de seguridad de máquinas virtuales](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm).

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>¿Por qué no aparece mi máquina virtual en el Asistente para configuración de la copia de seguridad?
En el Asistente para configuración de la copia de seguridad, Azure Backup solo muestra máquinas virtuales con los siguientes criterios:
* Aún no están protegidos, puede comprobar estado de copia de seguridad de Hola de una máquina virtual va tooVM hoja y comprobando en estado de copia de seguridad desde el menú de configuración de la hoja de Hola. Más información acerca de cómo demasiado[comprobar el estado de copia de seguridad de una máquina virtual](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)
* Pertenece toosame región como máquina virtual

## <a name="backup"></a>Backup
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>¿Seguirá el trabajo de copia de seguridad a petición la misma programación de retención que las copias de seguridad programadas?
No. Duración de retención de hello toospecify es necesario para un trabajo de copia de seguridad a petición. De forma predeterminada, se conservará durante 30 días cuando se active desde el portal. 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a>Recientemente habilité Azure Disk Encryption en algunas máquinas virtuales. ¿Mis copias de seguridad continuará toowork?
Necesitará permisos de toogive para tooaccess de servicio de copia de seguridad de Azure el almacén de claves. Puede proporcionar estos permisos en PowerShell mediante los pasos que se indican en la sección sobre *cómo habilitar Backup* de la documentación de [PowerShell](backup-azure-vms-automation.md).

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a>Migran los discos de los discos de toomanaged de una máquina virtual. ¿Mis copias de seguridad continuará toowork?
Sí, las copias de seguridad funcionan a la perfección y sin necesidad de toore-Configurar copia de seguridad. 

## <a name="restore"></a>Restauración
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>¿Cómo decido entre la restauración de discos frente a restauración completa de máquinas virtuales?
Considere la restauración completa de máquinas virtuales de Azure como una opción rápida de creación para máquinas virtuales restauradas. Restaure VM opción cambiará nombres Hola de discos, contenedores utilizan discos, direcciones IP públicas, interfaz de red nombres para la unicidad de los recursos obtener creados como parte de la creación de la máquina virtual. También agregará no Hola VM tooavailability conjunto. 

Use discos de restauración para:
* Personalizar Hola máquina virtual que se crea desde el punto en la configuración de tiempo como cambiar el tamaño de Hola de configuración de copia de seguridad
* Agregar configuraciones que no están presentes en tiempo de Hola de copia de seguridad 
* Convención de nomenclatura de Hola de control de recursos obtener creados
* Agregar conjunto de tooavailability de máquina virtual.
* Tiene una configuración que solo se puede lograr mediante PowerShell o una definición de plantilla declarativa

## <a name="manage-vm-backups"></a>Administrar copias de seguridad de máquina virtual
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>¿Qué ocurre cuando se cambia una directiva de copia de seguridad en las máquinas virtuales?
Cuando se aplica una nueva directiva de máquinas virtuales, se seguirá la retención de nueva directiva de Hola y programación. Si se amplía la retención, puntos de recuperación existentes se marcarán tookeep ellas según la directiva de nuevo. Si se reduce la retención, que están marcados para ser eliminados en el siguiente trabajo de limpieza de Hola y se eliminará. 
