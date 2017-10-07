---
title: "la replicación para máquinas virtuales de VMware replicar tooAzure con Azure Site Recovery aaaEnable | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooenable tooAzure de replicación para máquinas virtuales de VMware con servicio de Azure Site Recovery Hola"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a>Paso 11: Habilitar replicación para tooAzure de máquinas virtuales de VMware


Este artículo describe cómo tooenable replicación local VMware virtual máquinas tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de comenzar

- Máquinas virtuales de VMware debe tener hello [instalado el componente de servicio de movilidad](vmware-walkthrough-install-mobility.md). -Si una máquina virtual está preparada para la instalación de inserción, servidor de procesos de hello instala automáticamente servicio de movilidad de hello cuando se habilita la replicación.
- La cuenta de usuario de Azure debe específico [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una máquina virtual tooAzure
- Al agregar o modificar las máquinas virtuales, puede tardar minutos too15 o ya cambios tootake efecto y les tooappear en el portal de Hola.
- Puede comprobar tiempo de hello descubrió por última vez para las máquinas virtuales en **servidores de configuración** > **último contacto a**.
- tooadd máquinas virtuales sin tener que esperar la detección programada de hello, servidor de configuración de hello resaltado (no haga clic en él) y haga clic en **actualizar**.



## <a name="exclude-disks-from-replication"></a>Excluir discos de la replicación

De manera predeterminada, se replican todos los discos de una máquina. Puede excluir discos de la replicación. Por ejemplo, puede no ser conveniente tooreplicate discos con los datos temporales o datos que se actualizan cada vez que una máquina o reinicia la aplicación (por ejemplo, pagefile.sys o tempdb de SQL Server). [Más información](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Replicación de máquinas virtuales

Vea un vídeo introductorio rápido antes de empezar

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Haga clic en **Paso 2: Replicar la aplicación** > **Origen**.
2. En **origen**, seleccione servidor de configuración de Hola.
3. En **Tipo de máquina**, seleccione **Máquinas virtuales**.
4. En **vCenter/vSphere hipervisor**, seleccione servidor de vCenter Hola que administra el host de vSphere hello, o host Hola.
5. Seleccione el servidor de procesos de Hola. Si no ha creado ningún servidor de proceso adicionales esto será el servidor de configuración de Hola. y, a continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. En **destino**, seleccione la suscripción de Hola y Hola grupo de recursos en el que desea hello toocreate conmutado por error las máquinas virtuales. Elija el modelo de implementación de Hola que desee toouse en Azure (clásico o recurso de administración), para hello conmutado por error las máquinas virtuales.


7. Seleccione la cuenta de almacenamiento de Azure de Hola que desee toouse para la replicación de datos. Si no desea toouse una cuenta que ya haya configurado, puede crear uno nuevo.

8. Seleccione hello Azure toowhich de red y subred de máquinas virtuales de Azure se conectará, cuando se crean después de la conmutación por error. Seleccione **configurar ahora para las máquinas seleccionadas**, tooapply Hola red configuración tooall máquinas que seleccione para la protección. Seleccione **configurar más adelante** tooselect hello Azure red por máquina. Si no desea toouse una red existente, puede crear uno.

    ![Habilitar replicación](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. En **máquinas virtuales** > **seleccionar las máquinas virtuales**, haga clic en y seleccione cada máquina tooreplicate. Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación. A continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. En **propiedades** > **configurar las propiedades**, seleccione cuenta de hello que va a utilizar Hola proceso servidor tooautomatically instale servicio de movilidad de hello en la máquina de Hola.
11. De manera predeterminada se replican todos los discos. Haga clic en **todos los discos** y desactive los discos que no desea tooreplicate. y, a continuación, haga clic en **Aceptar**. Puede establecer otras propiedades de las máquinas virtuales más adelante.

    ![Habilitar replicación](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. En **configuración de replicación** > **establecer configuración de replicación**, compruebe que Hola correcto se selecciona la directiva de replicación. Si modifica una directiva, cambios será máquina tooreplicating aplicados y toonew máquinas.
12. Habilitar **coherencia entre varias VM** si desea toogather máquinas en un grupo de replicación y especifique un nombre para el grupo de Hola. y, a continuación, haga clic en **Aceptar**. Observe lo siguiente:

    * Todas las máquinas de un grupo de replicación se replican al mismo tiempo y comparten puntos de recuperación coherentes con los bloqueos y con la aplicación cuando conmutan por error.
    * Se recomienda que recopile las máquinas virtuales y los servidores físicos juntos para que reflejen las cargas de trabajo. Habilitar la coherencia entre varias VM puede afectar al rendimiento de la carga de trabajo y solo debe usarse si las máquinas ejecutan Hola necesita la misma carga de trabajo y coherencia.

    ![Habilitar replicación](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. Haga clic en **Enable Replication**. Puede seguir el progreso del programa Hola a **Habilitar protección** de trabajo en **configuración** > **trabajos** > **trabajos de recuperación de sitio**. Después de hello **finalización de protección** ejecuciones del trabajo Hola máquina está lista para conmutación por error.

## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 12: ejecutar una prueba de conmutación por error](vmware-walkthrough-test-failover.md)
