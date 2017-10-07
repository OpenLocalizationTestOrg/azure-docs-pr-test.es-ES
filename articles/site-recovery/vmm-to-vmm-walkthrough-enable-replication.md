---
title: "tooa de sitio secundario con Azure Site Recovery para la replicación aaaEnable Hyper-V | Documentos de Microsoft"
description: "Describe cómo tooenable replicación para máquinas virtuales de Hyper-V replicar tooa sitio de System Center VMM secundario con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>Paso 9: Habilitar el sitio secundario de tooa de replicación para máquinas virtuales de Hyper-V


Después de configurar una directiva de replicación, use este artículo tooenable replicación tooa secundaria System Center Virtual Machine Manager (VMM) sitio de Hyper-V virtual máquinas locales (VM), con [Azure Site Recovery](site-recovery-overview.md).

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="select-vms-tooreplicate"></a>Seleccione tooreplicate de máquinas virtuales

1. Haga clic en **Paso 2: Replicar la aplicación** > **Origen**. 

    ![Habilitar replicación](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. En **origen**, seleccione servidor VMM de Hola y Hola en la nube en qué Hola están ubicados los hosts de Hyper-V que desee tooreplicate. y, a continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. En **destino**, compruebe el servidor VMM secundario de Hola y en la nube.
4. En **máquinas virtuales**, seleccione hello las máquinas virtuales que desee tooprotect de lista de Hola.

    ![Habilitar protección de máquina virtual](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

Puede seguir el progreso de hello **habilitar la protección de** acción en **trabajos** > **trabajos de recuperación del sitio**. Después de hello **finalización de protección** trabajo se completa, la replicación inicial de Hola se ha completado y máquina virtual de hello está preparado para conmutación por error.

Observe lo siguiente:

- También puede habilitar la protección de máquinas virtuales en la consola VMM Hola. Haga clic en **Habilitar protección** en barra de herramientas de hello en Propiedades de la máquina virtual de hello > **Azure Site Recovery** ficha.
- Después de habilitar la replicación, puede ver propiedades de hello VM en **replican elementos**. En hello **Essentials** panel, puede ver información acerca de la directiva de replicación de hello hello VM y su estado. Haga clic en **Propiedades** para obtener más información.

## <a name="onboard-existing-vms"></a>Incorporar máquinas virtuales existentes

Si tiene máquinas virtuales en VMM que se replican mediante Réplica de Hyper-V, puede incorporarlas a la replicación de Azure Site Recovery de la forma siguiente:

1. Compruebe que el servidor Hyper-V de Hola Hola que máquina virtual existente se encuentra en la nube principal Hola de hospedaje, y ese servidor de Hyper-V de hello hospeda la máquina virtual de réplica de Hola se encuentra en la nube secundaria Hola.
2. Asegúrese de que se configura una directiva de replicación para la nube VMM principal Hola.
3. Habilitar la replicación de máquina virtual principal de Hola. Azure Site Recovery y VMM aseguran de que hello mismo host de réplica y la máquina virtual se detecta y volverá a utilizar Azure Site Recovery y restablecer la replicación mediante Hola especificada la configuración.


## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 10: ejecutar una prueba de conmutación por error](vmm-to-vmm-walkthrough-test-failover.md).
