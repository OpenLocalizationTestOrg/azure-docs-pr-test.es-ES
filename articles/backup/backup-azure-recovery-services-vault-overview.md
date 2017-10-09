---
title: "aaaOverview de almacenes de servicios de recuperación | Documentos de Microsoft"
description: "Información general y comparación entre los almacenes de Recovery Services y los de Azure Backup."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.assetid: 38d4078b-ebc8-41ff-9bc8-47acf256dc80
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/15/2017
ms.author: markgal;arunak
ms.openlocfilehash: 77dd9ece7fe86429cc6f9a47a68b5150a1f4af71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vaults-overview"></a>Introducción a los almacenes de Recovery Services

Este artículo describen características de Hola de un almacén de servicios de recuperación. Un almacén de Recovery Services es una entidad de almacenamiento de Azure que aloja datos. datos de Hello son ser copias de datos, o la información de configuración de máquinas virtuales (VM), las cargas de trabajo, los servidores o estaciones de trabajo. Un almacén de servicios de recuperación es la versión del Administrador de recursos de Hola de un almacén de copia de seguridad. Microsoft recomienda a los almacenes de servicios de recuperación de toouse y tooconvert tooRecovery almacenes de servicios de los almacenes de credenciales cualquier copia de seguridad.

## <a name="what-is-a-recovery-services-vault"></a>¿Qué es un almacén de Recovery Services?

Un almacén de servicios de recuperación es que una entidad de almacenamiento en línea en Azure usa datos toohold como copias de seguridad y los puntos de recuperación, las directivas de copia de seguridad. Puede usar datos de copia de seguridad de servicios de recuperación almacenes toohold para varios servicios de Azure como las máquinas virtuales de IaaS (Linux o Windows) y las bases de datos de SQL Azure. Los almacenes de Recovery Services son compatibles con System Center DPM, Windows Server, Azure Backup Server y muchos más. Almacenes de servicios de recuperación que sea fácil tooorganize los datos de copia de seguridad, y reduce su sobrecarga de administración.

Dentro de una suscripción de Azure, puede crear tantos almacenes de Recovery Services como desee.

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a>Comparación de almacenes de Recovery Services y de Backup

Almacenes de servicios de recuperación se basan en el modelo de hello Azure Resource Manager de Azure, mientras que los almacenes de copia de seguridad se basan en el modelo de hello Azure Service Manager. Cuando se actualiza un almacén de servicios de recuperación de tooa de almacén de copia de seguridad, datos de copia de seguridad de hello permanecen intactos durante y después del proceso de actualización de Hola. Los almacenes de Recovery Services proporcionan características que no están disponibles para los almacenes de Backup, como:

- **Datos de copia de seguridad segura de capacidades toohelp mejorados**: los almacenes de credenciales con los servicios de recuperación, copia de seguridad de Azure proporciona seguridad las copias de seguridad de las capacidades tooprotect en la nube. Estas características de seguridad garantizan que puede proteger las copias de seguridad y recuperar datos de forma segura de las copias de seguridad en la nube, incluso si los servidores de producción y copia de seguridad están en peligro. [Más información](backup-azure-security-feature.md)

- **Supervisión central para el entorno de TI híbrido**: con los almacenes de Recovery Services, puede supervisar no solo sus [máquinas virtuales de IaaS de Azure](backup-azure-manage-vms.md), sino también sus [recursos locales](backup-azure-manage-windows-server.md#manage-backup-items) desde un portal central. [Más información](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- **Control de acceso basado en rol (RBAC)**: RBAC permite un control muy detallado de la administración de acceso en Azure. [Azure proporciona diversas funciones integradas](../active-directory/role-based-access-built-in-roles.md), y copia de seguridad de Azure tiene tres [puntos de recuperación de funciones integradas toomanage](backup-rbac-rs-vault.md). Almacenes de servicios de recuperación son compatibles con RBAC, que restringe la copia de seguridad y restauración acceso toohello definido por conjunto de roles de usuario. [Más información](backup-rbac-rs-vault.md)

- **Protección de todas las configuraciones de Azure Virtual Machines**: los almacenes de Recovery Services protegen las máquinas virtuales basadas en Resource Manager, incluidos discos Premium, Managed Disks y máquinas virtuales cifradas. Actualizar un tooa de almacén de copia de seguridad del almacén proporciona Hola oportunidad tooupgrade su tooResource de las máquinas virtuales basadas en el administrador del servicio de las máquinas virtuales basadas en el Administrador de servicios de recuperación. Al actualizar el almacén de hello, puede conservar los puntos de recuperación de máquinas virtuales basadas en Service Manager y configurar la protección para hello actualizados (habilitadas por el Administrador de recursos), las máquinas virtuales. [Más información](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- **Restauración de instantánea para las máquinas virtuales IaaS**: usar servicios de recuperación de los almacenes de credenciales, puede restaurar archivos y carpetas desde una VM de IaaS sin restaurar Hola toda máquina virtual, lo que permite a los tiempos de restauración más rápidos. La restauración instantánea para máquinas virtuales de IaaS está disponible tanto para máquinas virtuales Windows como Linux. [Más información](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-hello-portal"></a>Administrar los almacenes de servicios de recuperación en el portal de Hola
Creación y administración de almacenes de servicios de recuperación en hello portal de Azure es fácil porque Hola servicio de copia de seguridad se integra en la hoja de configuración de Azure de Hola. Esta integración significa que se puede crear o administrar un almacén de servicios de recuperación *en contexto de Hola de servicio de destino de hello*. Por ejemplo, puntos de recuperación de Hola de tooview para una máquina virtual, selecciónela y haga clic en **copia de seguridad** en la hoja de configuración de Hola. Hola información de copia de seguridad específica toothat aparece en la máquina virtual. En el siguiente ejemplo, el Hola **ContosoVM** es Hola nombre de máquina virtual de Hola. **ContosoVM demovault** es nombre Hola de hello del almacén de servicios de recuperación. No necesita tooremember Hola nombre de almacén de servicios de recuperación de Hola que almacena los puntos de recuperación de hello, puede tener acceso a esta información de la máquina virtual de Hola.  

![Máquinas virtuales de detalles de almacén de Recovery Services](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

Si varios servidores están protegidos con hello mismos servicios de recuperación del almacén, puede ser más lógico toolook en hello que del almacén de servicios de recuperación. Puede buscar todos los almacenes de servicios de recuperación de la suscripción de Hola y elija uno de la lista de Hola.

Hello secciones siguientes contienen tooarticles de vínculos que explican cómo toouse servicios de recuperación de un almacén en cada tipo de actividad.

### <a name="back-up-data"></a>Copia de seguridad de datos
- [Copia de seguridad de máquinas virtuales de Azure](backup-azure-vms-first-look-arm.md)
- [Copia de seguridad de Windows Server o Windows Workstation](backup-try-azure-backup-in-10-mins.md)
- [Hacer copia de seguridad tooAzure de cargas de trabajo DPM](backup-azure-dpm-introduction.md)
- [Preparar tooback seguridad cargas de trabajo utilizando el servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a>Administración de puntos de recuperación
- [Administrar copias de seguridad de máquina virtual de Azure](backup-azure-manage-vms.md)
- [Administración de archivos y carpetas](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-hello-vault"></a>Restaurar los datos del almacén de Hola
- [Recuperación de archivos de máquinas virtuales de Azure](backup-azure-restore-files-from-vm.md)
- [Restauración de máquinas virtuales de Azure](backup-azure-arm-restore-vms.md)

### <a name="secure-hello-vault"></a>Almacén seguro Hola
- [Seguridad de los datos de copia de seguridad en la nube en los almacenes de Recovery Services](backup-azure-security-feature.md)



## <a name="next-steps"></a>Pasos siguientes
Usar hello artículo para siguiente:</br>
[Copia de seguridad de una máquina virtual de IaaS](backup-azure-arm-vms-prepare.md)</br>
[Copia de seguridad de Azure Backup Server](backup-azure-microsoft-azure-backup.md)</br>
[Copia de seguridad de Windows Server](backup-configure-vault.md)
