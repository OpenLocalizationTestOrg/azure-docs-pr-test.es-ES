---
title: "aaaSet un almacén para tooAzure de replicación (con System Center VMM) de Hyper-V con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooset un almacén para tooAzure de replicación (con VMM) de Hyper-V con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: f2c90f3c8b0a48db1e57fefd9829d29cffff8d43
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
3. En **objetivo de protección**, seleccione **tooAzure** > **Sí, con Hyper-V**. Seleccione **Sí** tooconfirm le NLA VMM. 

     ![Elegir objetivos](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 8: configurar el origen y de destino](vmm-to-azure-walkthrough-source-target.md)
