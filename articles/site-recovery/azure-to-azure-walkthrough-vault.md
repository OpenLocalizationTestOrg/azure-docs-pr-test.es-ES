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
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="40c71-103">Paso 4: Configurar un almacén para la replicación de tooAzure de Azure</span><span class="sxs-lookup"><span data-stu-id="40c71-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="40c71-104">Después de [Planear redes](azure-to-azure-walkthrough-network.md), use este tooset artículo un almacén, para máquinas virtuales (VM) Azure replicar tooanother región de Azure, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="40c71-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="40c71-105">Cuando termine de artículo hello, debe tener un almacén de servicios de recuperación configurado.</span><span class="sxs-lookup"><span data-stu-id="40c71-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="40c71-106">Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="40c71-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="40c71-107">La replicación de VM de Azure se encuentra en una versión preliminar en este momento.</span><span class="sxs-lookup"><span data-stu-id="40c71-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="40c71-108">Creación de un almacén</span><span class="sxs-lookup"><span data-stu-id="40c71-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="40c71-109">Le recomendamos que cree el almacén de servicios de recuperación de hello en ubicación de Hola donde desea que su tooreplicate de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="40c71-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="40c71-110">Por ejemplo, si la ubicación de destino es hello centro nos, crear almacén de hello en **Central US**.</span><span class="sxs-lookup"><span data-stu-id="40c71-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="40c71-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="40c71-111">Next steps</span></span>

<span data-ttu-id="40c71-112">Vaya demasiado[paso 5: habilitar la replicación](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="40c71-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
