---
title: "aaaConfigure la asignación de red para la replicación de máquinas virtuales de Hyper-V en VMM nubes tooAzure con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo tooconfigure la asignación de red al replicar máquinas virtuales de Hyper-V en VMM nubes tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="427e8-103">Paso 9: Configurar la asignación de red para tooAzure de replicación (con VMM) de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="427e8-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="427e8-104">Después de configurar hello [configuración de replicación de origen y de destino](vmm-to-azure-walkthrough-source-target.md), use este toomap de asignación de artículo tooconfigure red entre redes VM de VMM locales y redes de Azure.</span><span class="sxs-lookup"><span data-stu-id="427e8-104">After you set up hello [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article tooconfigure network mapping toomap between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="427e8-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="427e8-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="427e8-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="427e8-106">Before you start</span></span>

- <span data-ttu-id="427e8-107">Obtenga información sobre la [asignación de redes](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="427e8-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="427e8-108">[Prepare VMM para la asignación de red](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="427e8-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="427e8-109">Compruebe que máquinas virtuales en el servidor VMM Hola son redes VM de tooa conectado y que ha creado al menos una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="427e8-109">Verify that virtual machines on hello VMM server are connected tooa VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="427e8-110">Varias redes de VM pueden ser asignado tooa sola red de Azure.</span><span class="sxs-lookup"><span data-stu-id="427e8-110">Multiple VM networks can be mapped tooa single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="427e8-111">Configuración de la asignación</span><span class="sxs-lookup"><span data-stu-id="427e8-111">Configure mapping</span></span>

<span data-ttu-id="427e8-112">Configure la asignación como sigue:</span><span class="sxs-lookup"><span data-stu-id="427e8-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="427e8-113">En **infraestructura del sitio de recuperación** > **asignaciones de red** > **asignación de red**, haga clic en hello **+ la asignación de red**  icono.</span><span class="sxs-lookup"><span data-stu-id="427e8-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click hello **+Network Mapping** icon.</span></span>

    ![Asignación de red](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="427e8-115">En **Agregar asignación de red**, seleccione servidor VMM de origen de hello, y **Azure** como destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="427e8-115">In **Add network mapping**, select hello source VMM server, and **Azure** as hello target.</span></span>
3. <span data-ttu-id="427e8-116">Comprobar la suscripción de Hola y el modelo de implementación de hello después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="427e8-116">Verify hello subscription and hello deployment model after failover.</span></span>
4. <span data-ttu-id="427e8-117">En **red de origen**, seleccione red VM de hello origen local que desee toomap de lista de hello asociado con el servidor VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="427e8-117">In **Source network**, select hello source on-premises VM network you want toomap from hello list associated with hello VMM server.</span></span>
5. <span data-ttu-id="427e8-118">En **red de destino**, seleccione Hola red de Azure en qué réplica de máquinas virtuales de Azure se ubicarán cuando se crean.</span><span class="sxs-lookup"><span data-stu-id="427e8-118">In **Target network**, select hello Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="427e8-119">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="427e8-119">Then click **OK**.</span></span>

    ![Asignación de red](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="427e8-121">Esto es lo que sucede cuando comienza la asignación de red:</span><span class="sxs-lookup"><span data-stu-id="427e8-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="427e8-122">Las máquinas virtuales existentes en la red de VM de origen Hola son redes de destino de toohello conectado cuando comience la asignación.</span><span class="sxs-lookup"><span data-stu-id="427e8-122">Existing VMs on hello source VM network are connected toohello target network when mapping begins.</span></span> <span data-ttu-id="427e8-123">Nueva red de VM de origen de toohello conectadas las máquinas virtuales conectadas toohello asigna red de Azure cuando se produce la replicación.</span><span class="sxs-lookup"><span data-stu-id="427e8-123">New VMs connected toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="427e8-124">Si modifica una asignación de red existente, máquinas virtuales de réplica conectarse con la nueva configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="427e8-124">If you modify an existing network mapping, replica virtual machines connect using hello new settings.</span></span>
* <span data-ttu-id="427e8-125">Si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, máquina virtual de réplica de hello conecta toothat subred de destino después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="427e8-125">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
* <span data-ttu-id="427e8-126">Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello conecta toohello primera subred de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="427e8-126">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="427e8-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="427e8-127">Next steps</span></span>

<span data-ttu-id="427e8-128">Vaya demasiado[paso 10: crear una directiva de replicación](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="427e8-128">Go too[Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
