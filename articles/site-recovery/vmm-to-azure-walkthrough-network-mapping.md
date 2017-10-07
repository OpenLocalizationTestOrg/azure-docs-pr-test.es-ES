---
title: "aaaConfigure la asignación de red para la replicación de máquinas virtuales de Hyper-V en VMM nubes tooAzure con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo tooconfigure la asignación de red al replicar máquinas virtuales de Hyper-V en VMM nubes tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a>Paso 9: Configurar la asignación de red para tooAzure de replicación (con VMM) de Hyper-V

Después de configurar hello [configuración de replicación de origen y de destino](vmm-to-azure-walkthrough-source-target.md), use este toomap de asignación de artículo tooconfigure red entre redes VM de VMM locales y redes de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Antes de comenzar

- Obtenga información sobre la [asignación de redes](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- [Prepare VMM para la asignación de red](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping). 
- Compruebe que máquinas virtuales en el servidor VMM Hola son redes VM de tooa conectado y que ha creado al menos una red virtual de Azure. Varias redes de VM pueden ser asignado tooa sola red de Azure.

## <a name="configure-mapping"></a>Configuración de la asignación

Configure la asignación como sigue:

1. En **infraestructura del sitio de recuperación** > **asignaciones de red** > **asignación de red**, haga clic en hello **+ la asignación de red**  icono.

    ![Asignación de red](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. En **Agregar asignación de red**, seleccione servidor VMM de origen de hello, y **Azure** como destino de Hola.
3. Comprobar la suscripción de Hola y el modelo de implementación de hello después de la conmutación por error.
4. En **red de origen**, seleccione red VM de hello origen local que desee toomap de lista de hello asociado con el servidor VMM Hola.
5. En **red de destino**, seleccione Hola red de Azure en qué réplica de máquinas virtuales de Azure se ubicarán cuando se crean. y, a continuación, haga clic en **Aceptar**.

    ![Asignación de red](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

Esto es lo que sucede cuando comienza la asignación de red:

* Las máquinas virtuales existentes en la red de VM de origen Hola son redes de destino de toohello conectado cuando comience la asignación. Nueva red de VM de origen de toohello conectadas las máquinas virtuales conectadas toohello asigna red de Azure cuando se produce la replicación.
* Si modifica una asignación de red existente, máquinas virtuales de réplica conectarse con la nueva configuración de Hola.
* Si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, máquina virtual de réplica de hello conecta toothat subred de destino después de la conmutación por error.
* Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello conecta toohello primera subred de red de Hola.



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 10: crear una directiva de replicación](vmm-to-azure-walkthrough-replication.md)
