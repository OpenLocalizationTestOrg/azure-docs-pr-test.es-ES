---
title: "aaaSet un almacén para tooAzure de replicación de VMware con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooset un almacén para tooAzure de replicación de VMware con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a>Paso 7: Configurar un almacén para tooAzure de replicación de VMware


Este artículo describe cómo tooset una copia de seguridad un almacén y especifique qué desea tooreplicate desde la ubicación local, tooAzure con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.


Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Selección de un objetivo de protección

Seleccione la acción que realizará tooreplicate, y donde quiera tooreplicate a.

1. Haga clic en **Almacenes de Recovery Services** > almacén.
2. Hola recurso de menú, haga clic en **Site Recovery** > **preparar infraestructura** > **objetivo de protección**.
3. En **objetivo de protección**, seleccione **tooAzure** > **Sí, con el hipervisor de VMware vSphere**.



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 8: configurar el origen y de destino](vmware-walkthrough-source-target.md)
