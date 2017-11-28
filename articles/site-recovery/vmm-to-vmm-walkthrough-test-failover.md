---
title: "aaaRun una conmutación por error de prueba para el sitio secundario tooa de máquina virtual de Hyper-V replicación con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo toorun una conmutación por error de prueba para la máquina virtual de Hyper-V replicación tooa sitio de System Center VMM secundario con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="36d66-103">Paso 10: Ejecutar una prueba de conmutación por error para el sitio secundario de tooa de replicación de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="36d66-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="36d66-104">Después de habilitar la replicación de máquinas virtuales de Hyper-V (VM) con [Azure Site Recovery](site-recovery-overview.md), use este toorun artículo una conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="36d66-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="36d66-105">Una conmutación por error de prueba comprueba que la replicación funciona, sin afectar a su entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="36d66-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="36d66-106">Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="36d66-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="36d66-107">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="36d66-107">Before you start</span></span>

- <span data-ttu-id="36d66-108">Cuando está desencadenan una conmutación por error de prueba, puede especificar réplica Hola red toowhich Hola prueba que se conectarán las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="36d66-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="36d66-109">[Obtener más información](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) acerca de las opciones de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="36d66-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="36d66-110">Le recomendamos que no seleccione una red que haya seleccionado durante la asignación de red.</span><span class="sxs-lookup"><span data-stu-id="36d66-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="36d66-111">las instrucciones de Hello en este artículo se describe cómo toofail a través de una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="36d66-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="36d66-112">Obtenga información sobre [crear planes de recuperación](site-recovery-create-recovery-plans.md) si desea toofail a varias máquinas virtuales juntas.</span><span class="sxs-lookup"><span data-stu-id="36d66-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="36d66-113">Obtenga información sobre las [limitaciones para las conmutaciones por error de prueba](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="36d66-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="36d66-114">dirección IP dada tooa VM durante la conmutación por error de prueba Hello es hello misma dirección IP que Hola VM recibiría una planeada o no planeada conmutación por error (suponiendo que la dirección IP de hello está disponible en la red de conmutación por error de prueba de hello).</span><span class="sxs-lookup"><span data-stu-id="36d66-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="36d66-115">Si la dirección IP de hello no está disponible en la red de conmutación por error de prueba de hello, Hola VM recibe otra dirección IP que está disponible en la red de conmutación por error de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="36d66-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="36d66-116">Si desea toodo una conmutación por error de prueba en la red de producción, para la validación completa de la máquina de conectividad de red de extremo a extremo, tenga en cuenta que:</span><span class="sxs-lookup"><span data-stu-id="36d66-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="36d66-117">Hola que máquina virtual principal se debe cerrar cuando está realizando la conmutación por error de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="36d66-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="36d66-118">En caso contrario, dos máquinas virtuales con hello misma identidad se ejecutará en hello misma red hello en el mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="36d66-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="36d66-119">Si realiza cambios tootest las máquinas virtuales, estos cambios se perderán al limpiar Hola probar conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="36d66-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="36d66-120">Estos cambios no replicado toohello back-VM principal.</span><span class="sxs-lookup"><span data-stu-id="36d66-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="36d66-121">Pruebas de una red de producción conduce toodowntime para las cargas de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="36d66-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="36d66-122">Pedir a los usuarios no toouse aplicación de hello cuando detalles de recuperación ante desastres de hello está en curso.</span><span class="sxs-lookup"><span data-stu-id="36d66-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="36d66-123">Ejecutar una prueba de conmutación por error para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="36d66-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="36d66-124">toofail a través de una sola máquina virtual, en **replican elementos**, haga clic en hello VM > **conmutación por error de prueba**.</span><span class="sxs-lookup"><span data-stu-id="36d66-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="36d66-125">En **probar conmutación por error**, especificar cómo prueba máquinas virtuales estarán conectados toonetworks después de la conmutación por error de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="36d66-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="36d66-126">Haga clic en **Aceptar** conmutación por error de toobegin Hola.</span><span class="sxs-lookup"><span data-stu-id="36d66-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="36d66-127">Realizar un seguimiento del progreso en hello **trabajos** ficha.</span><span class="sxs-lookup"><span data-stu-id="36d66-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="36d66-128">Una vez completada la conmutación por error, compruebe que inicio de máquinas virtuales de la prueba de hello correctamente.</span><span class="sxs-lookup"><span data-stu-id="36d66-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="36d66-129">Cuando haya terminado, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="36d66-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="36d66-130">En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="36d66-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="36d66-131">Este paso elimina hello las máquinas virtuales y redes que se crearon durante la conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="36d66-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="36d66-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="36d66-132">Next steps</span></span>

<span data-ttu-id="36d66-133">Después de haberlo probado implementación hello, obtener más información sobre otros tipos de [conmutación por error](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="36d66-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
