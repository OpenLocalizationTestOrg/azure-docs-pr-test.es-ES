---
title: "replicación de aaaEnable para los servidores físicos que se replican tooAzure con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooenable tooAzure de replicación para los servidores físicos, con el servicio de Azure Site Recovery Hola"
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
ms.openlocfilehash: dde4b1463023d2ccefa498f72bb51e57d60ac0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-physical-servers-tooazure"></a>Paso 10: Habilitar la replicación de servidores físicos tooAzure


Este artículo describe cómo tooenable replicación local Windows/Linux tooAzure servidores físicos, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de comenzar

- Los servidores deben tener hello [instalado el componente de servicio de movilidad](physical-walkthrough-install-mobility.md).
- Si una máquina virtual está preparada para la instalación de inserción, servidor de procesos de hello instala automáticamente servicio de movilidad de hello cuando se habilita la replicación.
- Cuando se habilita una máquina para la replicación, su cuenta de usuario de Azure necesita específico [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooensure está toouse capaz de almacenamiento de Azure y crear máquinas virtuales de Azure.
- Al agregar o modificar las direcciones IP de servidores, puede tardar minutos too15 o ya cambios tootake efecto y les tooappear en el portal de Hola.


## <a name="exclude-disks-from-replication"></a>Excluir discos de la replicación

De manera predeterminada, se replican todos los discos de una máquina. Puede excluir discos de la replicación. Por ejemplo, puede no ser conveniente tooreplicate discos con los datos temporales o datos que se actualizan cada vez que una máquina o reinicia la aplicación (por ejemplo, pagefile.sys o tempdb de SQL Server). [Más información](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a>Replicación de servidores

1. Haga clic en **Paso 2: Replicar la aplicación** > **Origen**.
2. En **origen**, seleccione servidor de configuración de Hola.
3. En **Tipo de máquina**, seleccione **Máquinas físicas**.
4. Seleccione el servidor de procesos de Hola. Si no ha creado ningún servidor de proceso adicionales esto será el servidor de configuración de Hola. y, a continuación, haga clic en **Aceptar**.
5. En **destino**, seleccione la suscripción de Hola y Hola grupo de recursos en el que desea hello toocreate conmutado por error las máquinas virtuales. Elija el modelo de implementación de Hola que desee toouse en Azure (clásico o recurso de administración), para hello conmutado por error las máquinas virtuales.
6. Seleccione la cuenta de almacenamiento de Azure de Hola que desee toouse para la replicación de datos. Si no desea toouse una cuenta que ya haya configurado, puede crear uno nuevo.
7. Seleccione hello **red Azure** y **subred** toowhich máquinas virtuales de Azure conectarse después de la conmutación por error. Seleccione **configurar ahora para las máquinas seleccionadas** tooapply Hola red configuración tooall máquinas que seleccione para la protección. Seleccione **configurar más adelante** tooselect hello Azure red por máquina. Si no desea toouse una red existente, puede crear uno.

    ![Habilitar replicación](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. En **máquinas físicas**, haga clic en **+ máquina física** y escriba hello **nombre** y **dirección IP**. Elija el sistema operativo de Hola de máquina de hello desea tooreplicate. Tarda unos minutos hasta que se detectan y se muestra en la lista de hello máquinas.
9. En **propiedades** > **configurar las propiedades**, seleccione cuenta de hello que va a utilizar Hola proceso servidor tooautomatically instale servicio de movilidad de hello en la máquina de Hola.
10. De manera predeterminada se replican todos los discos. Haga clic en **todos los discos** y desactive los discos que no desea tooreplicate. y, a continuación, haga clic en **Aceptar**. Puede establecer otras propiedades de las máquinas virtuales más adelante.

    ![Habilitar replicación](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. En **configuración de replicación** > **establecer configuración de replicación**, compruebe que Hola correcto se selecciona la directiva de replicación. Si modifica una directiva, cambios será máquina tooreplicating aplicados y toonew máquinas.
12. Habilitar **coherencia entre varias VM** si desea toogather máquinas en un grupo de replicación y especifique un nombre para el grupo de Hola. y, a continuación, haga clic en **Aceptar**. Observe lo siguiente:

    * Todas las máquinas de un grupo de replicación se replican al mismo tiempo y comparten puntos de recuperación coherentes con los bloqueos y con la aplicación cuando conmutan por error.
    * Se recomienda que recopile los servidores físicos juntos para que reflejen las cargas de trabajo. Habilitar la coherencia entre varias VM puede afectar al rendimiento de la carga de trabajo y solo debe usarse si las máquinas ejecutan Hola necesita la misma carga de trabajo y coherencia.

13. Haga clic en **Enable Replication**. Puede seguir el progreso del programa Hola a **Habilitar protección** de trabajo en **configuración** > **trabajos** > **trabajos de recuperación de sitio**. Después de hello **finalización de protección** ejecuciones del trabajo Hola máquina está lista para conmutación por error.

## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 11: ejecutar una prueba de conmutación por error](physical-walkthrough-test-failover.md)
