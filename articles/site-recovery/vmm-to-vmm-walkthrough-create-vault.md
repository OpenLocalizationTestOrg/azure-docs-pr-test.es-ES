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
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="35049-103">Paso 5: Crear un almacén para el sitio secundario de tooa de replicación de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="35049-103">Step 5: Create a vault for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="35049-104">Después de preparar local [servidores de System Center Virtual Machine Manager (VMM) y los hosts y clústeres de Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) para el uso del sitio secundario de Hyper-V replicación tooa [Azure Site Recovery](site-recovery-overview.md), puede crear un Almacén de servicios de recuperación y escenario de replicación de hello select.</span><span class="sxs-lookup"><span data-stu-id="35049-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication tooa secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select hello replication scenario.</span></span>

<span data-ttu-id="35049-105">Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="35049-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="35049-106">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="35049-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="35049-107">Elección de un objetivo de protección</span><span class="sxs-lookup"><span data-stu-id="35049-107">Choose a protection goal</span></span>

<span data-ttu-id="35049-108">Seleccione en qué desea tooreplicate y donde quiera tooreplicate a.</span><span class="sxs-lookup"><span data-stu-id="35049-108">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="35049-109">Haga clic en **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="35049-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="35049-110">Seleccione **toorecovery sitio**y seleccione **Sí, con Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="35049-110">Select **toorecovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="35049-111">Seleccione **Sí** tooindicate utilizas hosts de Hyper-V de hello toomanage VMM.</span><span class="sxs-lookup"><span data-stu-id="35049-111">Select **Yes** tooindicate you're using VMM toomanage hello Hyper-V hosts.</span></span>
4. <span data-ttu-id="35049-112">Seleccione **Sí** si tiene un servidor VMM secundario.</span><span class="sxs-lookup"><span data-stu-id="35049-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="35049-113">Si va a implementar la replicación entre nubes en un solo servidor VMM, haga clic en **No**.</span><span class="sxs-lookup"><span data-stu-id="35049-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="35049-114">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="35049-114">Then click **OK**.</span></span>

    ![Elegir objetivos](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="35049-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35049-116">Next steps</span></span>

<span data-ttu-id="35049-117">Vaya demasiado[paso 6: configurar el origen de replicación de Hola y de destino](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="35049-117">Go too[Step 6: Set up hello replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>
