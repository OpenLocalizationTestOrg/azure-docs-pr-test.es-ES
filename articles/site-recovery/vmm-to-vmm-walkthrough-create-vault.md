---
title: "un almacén para tooa de sitio secundario con Azure Site Recovery para la replicación Hyper-V aaaCreate | Documentos de Microsoft"
description: "Describe cómo toocreate un almacén al replicar las máquinas virtuales de Hyper-V tooa sitio de System Center VMM secundario con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a>Paso 5: Crear un almacén para el sitio secundario de tooa de replicación de Hyper-V

Después de preparar local [servidores de System Center Virtual Machine Manager (VMM) y los hosts y clústeres de Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) para el uso del sitio secundario de Hyper-V replicación tooa [Azure Site Recovery](site-recovery-overview.md), puede crear un Almacén de servicios de recuperación y escenario de replicación de hello select.

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a>Elección de un objetivo de protección

Seleccione en qué desea tooreplicate y donde quiera tooreplicate a.

1. Haga clic en **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Objetivo de protección**.
2. Seleccione **toorecovery sitio**y seleccione **Sí, con Hyper-V**.
3. Seleccione **Sí** tooindicate utilizas hosts de Hyper-V de hello toomanage VMM.
4. Seleccione **Sí** si tiene un servidor VMM secundario. Si va a implementar la replicación entre nubes en un solo servidor VMM, haga clic en **No**. y, a continuación, haga clic en **Aceptar**.

    ![Elegir objetivos](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 6: configurar el origen de replicación de Hola y de destino](vmm-to-vmm-walkthrough-source-target.md).
