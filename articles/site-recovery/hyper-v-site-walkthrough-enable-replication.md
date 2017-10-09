---
title: "la replicación para máquinas virtuales de Hyper-V replicar tooAzure (sin System Center VMM) con Azure Site Recovery aaaEnable | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooenable tooAzure de replicación para máquinas virtuales de Hyper-V con servicio de Azure Site Recovery Hola"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a>Paso 10: Habilitar replicación para replicar tooAzure de las máquinas virtuales de Hyper-V


Este artículo describe cómo tooenable replicación local máquinas virtuales de Hyper-V (no administradas por System Center VMM) tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="before-you-start"></a>Antes de comenzar

Antes de empezar, asegúrese de que la cuenta de usuario de Azure tiene Hola necesario [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una nueva tooAzure de máquina virtual.

## <a name="exclude-disks-from-replication"></a>Excluir discos de la replicación

De manera predeterminada, se replican todos los discos de una máquina. Puede excluir discos de la replicación. Por ejemplo, puede no ser conveniente tooreplicate discos con los datos temporales o datos que se actualizan cada vez que una máquina o reinicia la aplicación (por ejemplo, pagefile.sys o tempdb de SQL Server). [Más información](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a>Replicación de máquinas virtuales

Habilite la replicación para máquinas virtuales como sigue:          

1. Haga clic en **Replicar la aplicación** > **Origen**. Una vez haya configurado la replicación para hello la primera vez, puede hacer clic en **+ replicar** tooenable replicación para máquinas adicionales.

    ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. En **origen**, seleccione el sitio de Hyper-V de Hola. y, a continuación, haga clic en **Aceptar**.
3. En **destino**, seleccione la suscripción de almacén de Hola y Hola modelo de conmutación por error que desee toouse en Azure (classic o recurso management) después de la conmutación por error.
4. Seleccione la cuenta de almacenamiento de Hola que desee toouse. Si no tienes una cuenta que desee toouse, puede [crear uno](#set-up-an-azure-storage-account). y, a continuación, haga clic en **Aceptar**.
5. Seleccione hello Azure toowhich de red y subred de máquinas virtuales de Azure se conectará cuando se crean conmutación por error.

    - Seleccione tooapply Hola configuración tooall máquinas de la red se habilita para la replicación, **configurar ahora para las máquinas seleccionadas**.
    - Seleccione **configurar más adelante** tooselect hello Azure red por máquina.
    - Si no dispone de una red que desee toouse, puede [crear uno](#set-up-an-azure-network). Seleccione una subred si es posible. A continuación, haga clic en **Aceptar**.

   ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. En **máquinas virtuales** > **seleccionar las máquinas virtuales**, haga clic en y seleccione cada máquina tooreplicate. Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación. A continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. En **propiedades** > **configurar las propiedades**, seleccione sistema de operativo Hola Hola selecciona las máquinas virtuales y Hola disco del sistema operativo.
8. Comprueba cumple ese nombre de máquina virtual de Azure (nombre de destino) de hello [requisitos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. De forma predeterminada se seleccionan todos los discos de Hola de hello VM para la replicación. Borrar discos tooexclude ellos.
10. Haga clic en **Aceptar** toosave cambios. Puede establecer propiedades adicionales más adelante.

    ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. En **configuración de replicación** > **establecer configuración de replicación**, seleccione Directiva de replicación de Hola que desee tooapply para hello protegido máquinas virtuales. y, a continuación, haga clic en **Aceptar**. Puede modificar la directiva de replicación de hello en **directivas de replicación** > nombre de directiva > **modificar configuración**. Los cambios que aplique se utilizarán tanto para las máquinas que ya se estén replicando como para otras nuevas.


   ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

Puede seguir el progreso del programa Hola a **Habilitar protección** de trabajo en **trabajos** > **trabajos de recuperación del sitio**. Después de hello **finalización de protección** ejecuciones del trabajo Hola máquina está lista para conmutación por error.


## <a name="next-steps"></a>Pasos siguientes


Vaya demasiado[paso 11: ejecutar una prueba de conmutación por error](hyper-v-site-walkthrough-test-failover.md)
