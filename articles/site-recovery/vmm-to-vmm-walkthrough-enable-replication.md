---
title: "tooa de sitio secundario con Azure Site Recovery para la replicación aaaEnable Hyper-V | Documentos de Microsoft"
description: "Describe cómo tooenable replicación para máquinas virtuales de Hyper-V replicar tooa sitio de System Center VMM secundario con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="628a6-103">Paso 9: Habilitar el sitio secundario de tooa de replicación para máquinas virtuales de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="628a6-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="628a6-104">Después de configurar una directiva de replicación, use este artículo tooenable replicación tooa secundaria System Center Virtual Machine Manager (VMM) sitio de Hyper-V virtual máquinas locales (VM), con [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="628a6-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="628a6-105">Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="628a6-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="628a6-106">Seleccione tooreplicate de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="628a6-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="628a6-107">Haga clic en **Paso 2: Replicar la aplicación** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="628a6-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Habilitar replicación](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="628a6-109">En **origen**, seleccione servidor VMM de Hola y Hola en la nube en qué Hola están ubicados los hosts de Hyper-V que desee tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="628a6-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="628a6-110">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="628a6-110">Then click **OK**.</span></span>

    ![Habilitar replicación](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="628a6-112">En **destino**, compruebe el servidor VMM secundario de Hola y en la nube.</span><span class="sxs-lookup"><span data-stu-id="628a6-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="628a6-113">En **máquinas virtuales**, seleccione hello las máquinas virtuales que desee tooprotect de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="628a6-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![Habilitar protección de máquina virtual](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="628a6-115">Puede seguir el progreso de hello **habilitar la protección de** acción en **trabajos** > **trabajos de recuperación del sitio**.</span><span class="sxs-lookup"><span data-stu-id="628a6-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="628a6-116">Después de hello **finalización de protección** trabajo se completa, la replicación inicial de Hola se ha completado y máquina virtual de hello está preparado para conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="628a6-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="628a6-117">Observe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="628a6-117">Note that:</span></span>

- <span data-ttu-id="628a6-118">También puede habilitar la protección de máquinas virtuales en la consola VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="628a6-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="628a6-119">Haga clic en **Habilitar protección** en barra de herramientas de hello en Propiedades de la máquina virtual de hello > **Azure Site Recovery** ficha.</span><span class="sxs-lookup"><span data-stu-id="628a6-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="628a6-120">Después de habilitar la replicación, puede ver propiedades de hello VM en **replican elementos**.</span><span class="sxs-lookup"><span data-stu-id="628a6-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="628a6-121">En hello **Essentials** panel, puede ver información acerca de la directiva de replicación de hello hello VM y su estado.</span><span class="sxs-lookup"><span data-stu-id="628a6-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="628a6-122">Haga clic en **Propiedades** para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="628a6-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="628a6-123">Incorporar máquinas virtuales existentes</span><span class="sxs-lookup"><span data-stu-id="628a6-123">Onboard existing VMs</span></span>

<span data-ttu-id="628a6-124">Si tiene máquinas virtuales en VMM que se replican mediante Réplica de Hyper-V, puede incorporarlas a la replicación de Azure Site Recovery de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="628a6-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="628a6-125">Compruebe que el servidor Hyper-V de Hola Hola que máquina virtual existente se encuentra en la nube principal Hola de hospedaje, y ese servidor de Hyper-V de hello hospeda la máquina virtual de réplica de Hola se encuentra en la nube secundaria Hola.</span><span class="sxs-lookup"><span data-stu-id="628a6-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="628a6-126">Asegúrese de que se configura una directiva de replicación para la nube VMM principal Hola.</span><span class="sxs-lookup"><span data-stu-id="628a6-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="628a6-127">Habilitar la replicación de máquina virtual principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="628a6-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="628a6-128">Azure Site Recovery y VMM aseguran de que hello mismo host de réplica y la máquina virtual se detecta y volverá a utilizar Azure Site Recovery y restablecer la replicación mediante Hola especificada la configuración.</span><span class="sxs-lookup"><span data-stu-id="628a6-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="628a6-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="628a6-129">Next steps</span></span>

<span data-ttu-id="628a6-130">Vaya demasiado[paso 10: ejecutar una prueba de conmutación por error](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="628a6-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
