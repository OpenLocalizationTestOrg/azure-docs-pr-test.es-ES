---
title: "nubes aaaEnable tooAzure de replicación para máquinas virtuales de Hyper-V en VMM con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo nubes tooenable tooAzure de replicación para máquinas virtuales de Hyper-V en VMM, con hello servicio Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 1a39bf65490c59a89a5e891184cadfacc2adee6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-tooazure-for-hyper-v-vms-in-vmm-clouds"></a>Paso 11: Habilitar replicación tooAzure para máquinas virtuales de Hyper-V en nubes de VMM

Después de configurar una directiva de replicación, use este artículo tooenable la replicación para máquinas virtuales de Hyper-V local (máquinas virtuales) administrada en nubes de System Center Virtual Machine Manager (VMM)), tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md)servicio Hola portal de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de comenzar

Asegúrese de que su cuenta de Azure tiene Hola correcto [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate máquinas virtuales de Azure. [Más información](../active-directory/role-based-access-built-in-roles.md) sobre el control de acceso basado en roles de Azure.

## <a name="exclude-disks-from-replication"></a>Excluir discos de la replicación

De manera predeterminada, se replican todos los discos de una máquina. Puede excluir discos de la replicación. Por ejemplo, puede no ser conveniente tooreplicate discos con los datos temporales o datos que se actualizan cada vez que una máquina o reinicia la aplicación (por ejemplo, pagefile.sys o tempdb de SQL Server). [Más información](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Replicación de máquinas virtuales

Habilite la replicación para máquinas virtuales como sigue:  

1. Haga clic en **Paso 2: Replicar la aplicación** > **Origen**. Después de habilitar la replicación para hello la primera vez, haga clic en **+ replicar** en la replicación de tooenable de almacén de Hola para máquinas adicionales.

    ![Habilitar replicación](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. Hola **origen** hoja, seleccione Hola servidor VMM y en la nube hello en qué Hola Hyper-V están ubicados los hosts. y, a continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. En **destino**, seleccione la suscripción de hello, modelo de implementación de conmutación por error de post, y Hola cuenta de almacenamiento que está usando para los datos replicados.

    ![Habilitar replicación](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. Seleccione la cuenta de almacenamiento de Hola que desee toouse. Si desea toouse una cuenta de almacenamiento diferentes que los tiene, puede [crear uno](#set-up-an-azure-storage-account). Si usa una cuenta de almacenamiento premium para los datos replicados, necesita tooselect un registros de replicación de toostore de cuenta de almacenamiento estándar adicional que capturan los cambios continuos tooon local data.toocreate una cuenta de almacenamiento mediante el modelo de administrador de recursos de Hola Haga clic en **crear nuevo**. Si desea toocreate una cuenta de almacenamiento con el modelo clásico de hello, hacerlo [Hola portal de Azure](../storage/common/storage-create-storage-account.md). y, a continuación, haga clic en **Aceptar**.
5. Seleccione hello Azure toowhich de red y subred de máquinas virtuales de Azure se conectará, cuando se crean después de la conmutación por error. Seleccione **configurar ahora para las máquinas seleccionadas**, tooapply Hola red configuración tooall máquinas que seleccione para la protección. Seleccione **configurar más adelante**, tooselect hello Azure red por máquina. Si desea toouse de las que tiene una red distinta, puede [crear uno](#set-up-an-azure-network). Haga clic en el modelo de administrador de recursos de Hola de toocreate una red con **crear nuevo**. Si desea toocreate una red con el modelo clásico de hello, hacerlo [Hola portal de Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Seleccione una subred si es posible. y, a continuación, haga clic en **Aceptar**.
6. En **máquinas virtuales** > **seleccionar las máquinas virtuales**, haga clic en y seleccione cada máquina tooreplicate. Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación. A continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. En **propiedades** > **configurar las propiedades**, seleccione sistema de operativo Hola Hola selecciona las máquinas virtuales y Hola disco del sistema operativo.

    - Comprueba cumple ese nombre de máquina virtual de Azure (nombre de destino) de hello [requisitos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - De forma predeterminada se seleccionan todos los discos de Hola de hello VM para la replicación, pero puede borrar discos tooexclude ellos.

        - Puede ser conveniente tooexclude discos tooreduce del ancho de banda. Por ejemplo, puede no ser conveniente tooreplicate discos con los datos temporales o datos que se actualizan cada vez que un equipo o en las aplicaciones se reinicia (por ejemplo, pagefile.sys o tempdb de Microsoft SQL Server). Puede excluir disco Hola de replicación por disco de hello anule su selección.
        - Solo se pueden excluir los discos básicos. Los discos del sistema operativo no se pueden excluir.
        - Se recomienda no excluir discos dinámicos. Site Recovery no se puede identificar si un disco duro virtual de una máquina virtual invitada es básico o dinámico. Si no se excluyen todos los discos de los volúmenes dinámicos dependientes, disco dinámico protegido de Hola se mostrará como un disco con errores cuando hello máquina virtual conmuta por error y datos de hello en ese disco no será accesibles.
        - Una vez habilitada la replicación, no puede agregar ni quitar discos para la replicación. Si desea que tooadd o excluir un disco, necesita protección toodisable Hola VM y, a continuación, volver a habilitarla.
        - No se produce una conmutación por recuperación de los discos que se crean manualmente en Azure. Por ejemplo, si se producirá un error en más de tres discos y cree dos directamente en la máquina virtual de Azure, solo Hola tres discos que se han conmutado por error desde Azure tooHyper-V. No se incluyen discos creados manualmente en la conmutación por recuperación, o en la replicación inversa de Hyper-V tooAzure.
        - Si excluye un disco que se necesita para una aplicación toooperate, después de la conmutación por error tooAzure debe toocreate puede ejecutarse manualmente en Azure, por lo que ese saludo replica aplicación. Como alternativa, puede integrar automatización de Azure en un plan de recuperación, disco de hello toocreate durante la conmutación por error de la máquina de Hola.

    Haga clic en **Aceptar** toosave cambios. Puede establecer propiedades adicionales más adelante.

    ![Habilitar replicación](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. En **configuración de replicación** > **establecer configuración de replicación**, seleccione Directiva de replicación de Hola que desee tooapply para hello protegido máquinas virtuales. y, a continuación, haga clic en **Aceptar**. Puede modificar la directiva de replicación de hello en **directivas de replicación** > nombre de directiva > **modificar configuración**. Los cambios que aplique se utilizarán tanto para las máquinas que ya se estén replicando como para otras nuevas.

   ![Habilitar replicación](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

Puede seguir el progreso del programa Hola a **Habilitar protección** de trabajo en **trabajos** > **trabajos de recuperación del sitio**. Después de hello **finalización de protección** se ejecuta el trabajo, Hola máquina está lista para conmutación por error.



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 12: ejecutar una prueba de conmutación por error](vmm-to-azure-walkthrough-test-failover.md)
