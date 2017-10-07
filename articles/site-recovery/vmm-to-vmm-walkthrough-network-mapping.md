---
title: "redes aaaMap para el sitio secundario tooa de máquina virtual de Hyper-V replicación con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo toomap redes al replicar las máquinas virtuales de Hyper-V tooa secundaria sitio de VMM con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="6c41c-103">Paso 7: Asignar redes para el sitio secundario de tooa de replicación de máquina virtual de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="6c41c-103">Step 7: Map networks for Hyper-V VM replication tooa secondary site</span></span>


<span data-ttu-id="6c41c-104">Después de configurar [valores de origen y destino](vmm-to-vmm-walkthrough-source-target.md) para la replicación de sitio de System Center Virtual Machine Manager (VMM) secundario de tooa de máquinas virtuales (VM) de Hyper-V, use esta asignación de red de artículo tooconfigure para Hyper-V virtual tooa de replicación de máquina (VM) secundaria del sitio, con [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c41c-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) tooa secondary System Center Virtual Machine Manager (VMM) site, use this article tooconfigure network mapping for Hyper-V virtual machine (VM) replication tooa secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="6c41c-105">Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6c41c-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="6c41c-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="6c41c-106">Before you start</span></span>

- <span data-ttu-id="6c41c-107">Aprenda sobre la [asignación de red](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="6c41c-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="6c41c-108">Compruebe que máquinas virtuales en servidores VMM red de VM tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="6c41c-108">Verify that virtual machines on VMM servers are connected tooa VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="6c41c-109">Configurar asignación de red</span><span class="sxs-lookup"><span data-stu-id="6c41c-109">Configure network mapping</span></span>

1. <span data-ttu-id="6c41c-110">En **Asignación de red** > **Asignaciones de red**, haga clic en **+Asignación de red**.</span><span class="sxs-lookup"><span data-stu-id="6c41c-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="6c41c-111">En **Agregar asignación de red** ficha, seleccione el origen de Hola y servidores VMM de destino.</span><span class="sxs-lookup"><span data-stu-id="6c41c-111">In **Add network mapping** tab, select hello source and target VMM servers.</span></span> <span data-ttu-id="6c41c-112">redes de VM de Hello asociadas con servidores VMM Hola se recuperan.</span><span class="sxs-lookup"><span data-stu-id="6c41c-112">hello VM networks associated with hello VMM servers are retrieved.</span></span>
3. <span data-ttu-id="6c41c-113">En **red de origen**, seleccione red Hola desea toouse de lista de Hola de redes de VM asociadas con el servidor VMM principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c41c-113">In **Source network**, select hello network you want toouse from hello list of VM networks associated with hello primary VMM server.</span></span>
4. <span data-ttu-id="6c41c-114">En **red de destino**, seleccione red Hola desea toouse en servidor VMM secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="6c41c-114">In **Target network**, select hello network you want toouse on hello secondary VMM server.</span></span> <span data-ttu-id="6c41c-115">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6c41c-115">Then click **OK**.</span></span>

    ![Asignación de red](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="6c41c-117">Esto es lo que sucede cuando comienza la asignación de red:</span><span class="sxs-lookup"><span data-stu-id="6c41c-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="6c41c-118">Las máquinas virtuales de réplica existente que corresponden toohello red de VM de origen será conectado toohello red de VM de destino.</span><span class="sxs-lookup"><span data-stu-id="6c41c-118">Any existing replica virtual machines that correspond toohello source VM network will be connected toohello target VM network.</span></span>
* <span data-ttu-id="6c41c-119">Nuevas máquinas virtuales que son redes VM de origen conectado toohello será red asignada de destino conectados toohello después de la replicación.</span><span class="sxs-lookup"><span data-stu-id="6c41c-119">New virtual machines that are connected toohello source VM network will be connected toohello target mapped network after replication.</span></span>
* <span data-ttu-id="6c41c-120">Si modifica una asignación existente con una nueva red, máquinas virtuales de réplica se conectarán utilizando una nueva configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c41c-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using hello new settings.</span></span>
* <span data-ttu-id="6c41c-121">Si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, entonces Hola máquina virtual será toothat conectado subred de destino después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="6c41c-121">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="6c41c-122">Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c41c-122">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6c41c-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c41c-123">Next steps</span></span>

<span data-ttu-id="6c41c-124">Vaya demasiado[paso 8: configurar una directiva de replicación](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="6c41c-124">Go too[Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>
