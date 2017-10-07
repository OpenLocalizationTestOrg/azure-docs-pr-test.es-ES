---
title: "redes aaaMap para el sitio secundario tooa de máquina virtual de Hyper-V replicación con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo toomap redes al replicar las máquinas virtuales de Hyper-V tooa secundaria sitio de VMM con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>Paso 7: Asignar redes para el sitio secundario de tooa de replicación de máquina virtual de Hyper-V


Después de configurar [valores de origen y destino](vmm-to-vmm-walkthrough-source-target.md) para la replicación de sitio de System Center Virtual Machine Manager (VMM) secundario de tooa de máquinas virtuales (VM) de Hyper-V, use esta asignación de red de artículo tooconfigure para Hyper-V virtual tooa de replicación de máquina (VM) secundaria del sitio, con [Azure Site Recovery](site-recovery-overview.md).

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de comenzar

- Aprenda sobre la [asignación de red](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) antes de empezar.
- Compruebe que máquinas virtuales en servidores VMM red de VM tooa conectado.

## <a name="configure-network-mapping"></a>Configurar asignación de red

1. En **Asignación de red** > **Asignaciones de red**, haga clic en **+Asignación de red**.
2. En **Agregar asignación de red** ficha, seleccione el origen de Hola y servidores VMM de destino. redes de VM de Hello asociadas con servidores VMM Hola se recuperan.
3. En **red de origen**, seleccione red Hola desea toouse de lista de Hola de redes de VM asociadas con el servidor VMM principal de Hola.
4. En **red de destino**, seleccione red Hola desea toouse en servidor VMM secundario Hola. y, a continuación, haga clic en **Aceptar**.

    ![Asignación de red](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

Esto es lo que sucede cuando comienza la asignación de red:

* Las máquinas virtuales de réplica existente que corresponden toohello red de VM de origen será conectado toohello red de VM de destino.
* Nuevas máquinas virtuales que son redes VM de origen conectado toohello será red asignada de destino conectados toohello después de la replicación.
* Si modifica una asignación existente con una nueva red, máquinas virtuales de réplica se conectarán utilizando una nueva configuración de Hola.
* Si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, entonces Hola máquina virtual será toothat conectado subred de destino después de la conmutación por error. Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 8: configurar una directiva de replicación](vmm-to-vmm-walkthrough-replication.md).
