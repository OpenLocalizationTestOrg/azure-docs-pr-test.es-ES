---
title: "aaaSet un almacén para tooAzure de replicación (sin System Center VMM) de Hyper-V con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooset un almacén para tooAzure de replicación de Hyper-V con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a>Paso 7: configuración de un almacén para la replicación de Hyper-V

Este artículo describe cómo tooset una copia de seguridad un almacén y especifique qué desea tooreplicate desde la ubicación local, tooAzure con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.


Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a>Selección de un objetivo de protección

Seleccione la acción que realizará tooreplicate, y donde quiera tooreplicate a.

1. Haga clic en **Almacenes de Recovery Services** > almacén.
2. Hola recurso de menú, haga clic en **Site Recovery** > **preparar infraestructura** > **objetivo de protección**.
3. En **objetivo de protección**, seleccione **tooAzure** > **Sí, con Hyper-V**. Seleccione **No** tooconfirm no usa VMM. 

    ![Elegir objetivos](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 8: configurar el origen y de destino](hyper-v-site-walkthrough-source-target.md)
