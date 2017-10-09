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
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="cf37d-103">Paso 7: configuración de un almacén para la replicación de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="cf37d-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="cf37d-104">Este artículo describe cómo tooset una copia de seguridad un almacén y especifique qué desea tooreplicate desde la ubicación local, tooAzure con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf37d-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="cf37d-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cf37d-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="cf37d-106">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="cf37d-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="cf37d-107">Selección de un objetivo de protección</span><span class="sxs-lookup"><span data-stu-id="cf37d-107">Select a protection goal</span></span>

<span data-ttu-id="cf37d-108">Seleccione la acción que realizará tooreplicate, y donde quiera tooreplicate a.</span><span class="sxs-lookup"><span data-stu-id="cf37d-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="cf37d-109">Haga clic en **Almacenes de Recovery Services** > almacén.</span><span class="sxs-lookup"><span data-stu-id="cf37d-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="cf37d-110">Hola recurso de menú, haga clic en **Site Recovery** > **preparar infraestructura** > **objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="cf37d-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="cf37d-111">En **objetivo de protección**, seleccione **tooAzure** > **Sí, con Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="cf37d-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="cf37d-112">Seleccione **No** tooconfirm no usa VMM.</span><span class="sxs-lookup"><span data-stu-id="cf37d-112">Select **No** tooconfirm you're not using VMM.</span></span> 

    ![Elegir objetivos](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="cf37d-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf37d-114">Next steps</span></span>

<span data-ttu-id="cf37d-115">Vaya demasiado[paso 8: configurar el origen y de destino](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="cf37d-115">Go too[Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
