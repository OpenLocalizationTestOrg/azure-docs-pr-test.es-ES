---
title: "arquitectura de hello aaaReview para tooa de sitio secundario con Azure Site Recovery para la replicación Hyper-V | Documentos de Microsoft"
description: "Este artículo proporciona información general sobre la arquitectura de hello para la replicación de máquinas virtuales de Hyper-V tooa secundaria System Center VMM sitio local con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="be220-103">Paso 1: Revisar la arquitectura de hello para el sitio secundario de tooa de replicación de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="be220-103">Step 1: Review hello architecture for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="be220-104">Este artículo describen los componentes de Hola y procesos que tienen lugar al replicar máquinas virtuales de Hyper-V (VM) en nubes de System Center Virtual Machine Manager (VMM), sitio VMM secundario tooa con hello local [Azure Site Recovery](site-recovery-overview.md)servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="be220-104">This article describes hello components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM site using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="be220-105">Registrar cualquier comentario a la parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="be220-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="be220-106">Componentes de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="be220-106">Architectural components</span></span>

<span data-ttu-id="be220-107">Aquí es lo que necesita para la replicación de máquinas virtuales de Hyper-V tooa sitio secundario de VMM.</span><span class="sxs-lookup"><span data-stu-id="be220-107">Here's what you need for replicating Hyper-V VMs tooa secondary VMM site.</span></span>

<span data-ttu-id="be220-108">**Componente**</span><span class="sxs-lookup"><span data-stu-id="be220-108">**Component**</span></span> | <span data-ttu-id="be220-109">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="be220-109">**Location**</span></span> | <span data-ttu-id="be220-110">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="be220-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="be220-111">**Las tablas de Azure**</span><span class="sxs-lookup"><span data-stu-id="be220-111">**Azure**</span></span> | <span data-ttu-id="be220-112">Suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="be220-112">Subscription in Azure.</span></span> | <span data-ttu-id="be220-113">Cree un almacén de servicios de recuperación en hello suscripción de Azure, tooorchestrate y administrar la replicación entre ubicaciones de VMM.</span><span class="sxs-lookup"><span data-stu-id="be220-113">You create a Recovery Services vault in hello Azure subscription, tooorchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="be220-114">**Servidor VMM**</span><span class="sxs-lookup"><span data-stu-id="be220-114">**VMM server**</span></span> | <span data-ttu-id="be220-115">Necesita una ubicación principal de VMM y otra secundaria.</span><span class="sxs-lookup"><span data-stu-id="be220-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="be220-116">Se recomienda un servidor VMM en el sitio primario de hello y otro en el sitio secundario de Hola</span><span class="sxs-lookup"><span data-stu-id="be220-116">We recommend a VMM server in hello primary site, and one in hello secondary site</span></span> 
<span data-ttu-id="be220-117">**Servidor de Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="be220-117">**Hyper-V server**</span></span> |  <span data-ttu-id="be220-118">Uno o varios servidores Hyper-V host Hola principales y secundarias en nubes de VMM.</span><span class="sxs-lookup"><span data-stu-id="be220-118">One or more Hyper-V host servers in hello primary and secondary VMM clouds.</span></span> | <span data-ttu-id="be220-119">Datos se replican entre Hola principales y secundarios Hyper-V host servidores a través de LAN de Hola o VPN, con la autenticación Kerberos o certificados.</span><span class="sxs-lookup"><span data-stu-id="be220-119">Data is replicated between hello primary and secondary Hyper-V host servers over hello LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="be220-120">**Máquinas virtuales de Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="be220-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="be220-121">En el servidor de host de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="be220-121">On Hyper-V host server.</span></span> | <span data-ttu-id="be220-122">servidor de host de origen de Hello debe tener al menos una máquina virtual que desea tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="be220-122">hello source host server should have at least one VM that you want tooreplicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="be220-123">Proceso de replicación</span><span class="sxs-lookup"><span data-stu-id="be220-123">Replication process</span></span>

1. <span data-ttu-id="be220-124">Configurar la cuenta de Azure hello, cree un almacén de servicios de recuperación y especifique qué desea tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="be220-124">You set up hello Azure account, create a Recovery Services vault, and specify what you want tooreplicate.</span></span>
2. <span data-ttu-id="be220-125">Configurar Hola origen y destino configuración de replicación, que incluye la instalación de hello Azure Site Recovery Provider en servidores VMM y el agente de servicios de recuperación de Microsoft Azure de hello en cada host de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="be220-125">You configure hello source and target replication settings, which includes installing hello Azure Site Recovery Provider on VMM servers, and hello Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="be220-126">Crear una directiva de replicación para el origen de hello nube de VMM.</span><span class="sxs-lookup"><span data-stu-id="be220-126">You create a replication policy for hello source VMM cloud.</span></span> <span data-ttu-id="be220-127">Directiva de Hello es aplicado tooall máquinas virtuales ubicadas en hosts en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="be220-127">hello policy is applied tooall VMs located on hosts in hello cloud.</span></span>
4. <span data-ttu-id="be220-128">Habilitar la replicación para cada VMM y se produce la replicación inicial de una máquina virtual de acuerdo con la configuración de Hola que elija.</span><span class="sxs-lookup"><span data-stu-id="be220-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with hello settings you choose.</span></span>
5. <span data-ttu-id="be220-129">Después de la replicación inicial, empieza la de los cambios diferenciales.</span><span class="sxs-lookup"><span data-stu-id="be220-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="be220-130">Las marcas de revisión de un elemento se conservan en un archivo .hrl.</span><span class="sxs-lookup"><span data-stu-id="be220-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Local tooon-local](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="be220-132">Proceso de conmutación por error y conmutación por recuperación</span><span class="sxs-lookup"><span data-stu-id="be220-132">Failover and failback process</span></span>

1. <span data-ttu-id="be220-133">Puede ejecutar una [conmutación por error](site-recovery-failover.md), planeada o no, entre sitios locales.</span><span class="sxs-lookup"><span data-stu-id="be220-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="be220-134">Si se ejecuta una conmutación por error planeada, las máquinas virtuales de origen se apagan tooensure sin pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="be220-134">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="be220-135">Puede conmutar por error un único equipo, o crear [planes de recuperación](site-recovery-create-recovery-plans.md) tooorchestrate conmutación por error de varias máquinas.</span><span class="sxs-lookup"><span data-stu-id="be220-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="be220-136">Si lleva a cabo un sitio secundario de conmutación por error imprevista tooa, después de máquinas de conmutación por error de hello en la ubicación secundaria hello no están habilitadas para protección o la replicación.</span><span class="sxs-lookup"><span data-stu-id="be220-136">If you perform an unplanned failover tooa secondary site, after hello failover machines in hello secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="be220-137">Si ha ejecutado una conmutación por error planeada, después de la conmutación por error de hello, máquinas en la ubicación secundaria Hola están protegidas.</span><span class="sxs-lookup"><span data-stu-id="be220-137">If you ran a planned failover, after hello failover, machines in hello secondary location are protected.</span></span>
5. <span data-ttu-id="be220-138">A continuación, confirmar Hola conmutación por error toostart acceso a Hola cargas de trabajo de VM de réplica de Hola.</span><span class="sxs-lookup"><span data-stu-id="be220-138">Then, you commit hello failover toostart accessing hello workload from hello replica VM.</span></span>
6. <span data-ttu-id="be220-139">Cuando el sitio primario vuelve a estar disponible, iniciar la replicación inversa tooreplicate de toohello de sitio secundario de hello principal.</span><span class="sxs-lookup"><span data-stu-id="be220-139">When your primary site is available again, you initiate reverse replication tooreplicate from hello secondary site toohello primary.</span></span> <span data-ttu-id="be220-140">La replicación inversa pone hello las máquinas virtuales en un estado protegido, pero Hola centro de datos secundaria sigue siendo ubicación activa Hola.</span><span class="sxs-lookup"><span data-stu-id="be220-140">Reverse replication brings hello virtual machines into a protected state, but hello secondary datacenter is still hello active location.</span></span>
7. <span data-ttu-id="be220-141">sitio primario de hello toomake en ubicación activa Hola de nuevo, que se inicie una conmutación por error planeada de tooprimary secundaria, seguido por otra replicación inversa.</span><span class="sxs-lookup"><span data-stu-id="be220-141">toomake hello primary site into hello active location again, you initiate a planned failover from secondary tooprimary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="be220-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be220-142">Next steps</span></span>

<span data-ttu-id="be220-143">Vaya demasiado[paso 2: revisar los requisitos previos de Hola y limitaciones](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="be220-143">Go too[Step 2: Review hello prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
