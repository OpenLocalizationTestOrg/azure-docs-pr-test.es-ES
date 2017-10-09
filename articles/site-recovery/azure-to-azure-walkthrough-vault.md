---
title: "aaaSet un almacén para su máquina virtual de Azure repliction entre las regiones con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooset un almacén para la replicación de Azure entre regiones de Azure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a>Paso 4: Configurar un almacén para la replicación de tooAzure de Azure

Después de [Planear redes](azure-to-azure-walkthrough-network.md), use este tooset artículo un almacén, para máquinas virtuales (VM) Azure replicar tooanother región de Azure, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

- Cuando termine de artículo hello, debe tener un almacén de servicios de recuperación configurado.
- Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



>[!NOTE]
>
> La replicación de VM de Azure se encuentra en una versión preliminar en este momento.




## <a name="create-a-vault"></a>Creación de un almacén

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Le recomendamos que cree el almacén de servicios de recuperación de hello en ubicación de Hola donde desea que su tooreplicate de máquinas virtuales. Por ejemplo, si la ubicación de destino es hello centro nos, crear almacén de hello en **Central US**.


## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 5: habilitar la replicación](azure-to-azure-walkthrough-enable-replication.md)
