---
title: "aaaSet un almacén para tooAzure de replicación de servidor físico con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooset seguridad un tooAzure de almacén tooreplicate servidores físicos con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a>Paso 6: Configurar un almacén para tooAzure de replicación del servidor físico


Este artículo se describe cómo tooset un almacén. Crear almacén de Hola y especifique qué desea tooreplicate desde su tooAzure de ubicación local, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.


Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Selección de un objetivo de protección

Seleccione la acción que realizará tooreplicate, y donde quiera tooreplicate a.

1. Haga clic en **Almacenes de Recovery Services** > almacén.
2. Hola recurso de menú, haga clic en **Site Recovery** > **preparar infraestructura** > **objetivo de protección**.
3. En **objetivo de protección**, seleccione **tooAzure** > **no virtualizados/otros**.


## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 7: configurar el origen y de destino](physical-walkthrough-source-target.md)
