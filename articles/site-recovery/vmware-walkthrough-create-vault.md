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
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a><span data-ttu-id="de67d-103">Paso 7: Configurar un almacén para tooAzure de replicación de VMware</span><span class="sxs-lookup"><span data-stu-id="de67d-103">Step 7: Set up a vault for VMware replication tooAzure</span></span>


<span data-ttu-id="de67d-104">Este artículo describe cómo tooset una copia de seguridad un almacén y especifique qué desea tooreplicate desde la ubicación local, tooAzure con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="de67d-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="de67d-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="de67d-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="de67d-106">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="de67d-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="de67d-107">Selección de un objetivo de protección</span><span class="sxs-lookup"><span data-stu-id="de67d-107">Select a protection goal</span></span>

<span data-ttu-id="de67d-108">Seleccione la acción que realizará tooreplicate, y donde quiera tooreplicate a.</span><span class="sxs-lookup"><span data-stu-id="de67d-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="de67d-109">Haga clic en **Almacenes de Recovery Services** > almacén.</span><span class="sxs-lookup"><span data-stu-id="de67d-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="de67d-110">Hola recurso de menú, haga clic en **Site Recovery** > **preparar infraestructura** > **objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="de67d-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="de67d-111">En **objetivo de protección**, seleccione **tooAzure** > **Sí, con el hipervisor de VMware vSphere**.</span><span class="sxs-lookup"><span data-stu-id="de67d-111">In **Protection goal**, select **tooAzure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="de67d-112">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de67d-112">Next steps</span></span>

<span data-ttu-id="de67d-113">Vaya demasiado[paso 8: configurar el origen y de destino](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="de67d-113">Go too[Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
