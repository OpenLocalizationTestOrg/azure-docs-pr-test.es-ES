---
title: "aaaReplicate máquinas virtuales de Hyper-V tooa sitio VMM secundario con Azure Site Recovery | Documentos de Microsoft"
description: "Proporciona información general para la replicación de sitio máquinas virtuales de Hyper-V tooa VMM secundario con hello portal de Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a><span data-ttu-id="cbcdb-103">Replicar máquinas virtuales de Hyper-V en el sitio secundario de VMM de VMM nubes tooa</span><span class="sxs-lookup"><span data-stu-id="cbcdb-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cbcdb-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cbcdb-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="cbcdb-105">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="cbcdb-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="cbcdb-106">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="cbcdb-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="cbcdb-107">Este artículo proporciona información general de hello pasos necesarios tooreplicate máquinas de virtuales de Hyper-V (máquinas virtuales) administradas en nubes de System Center Virtual Machine Manager (VMM), tooa la ubicación secundaria de VMM, locales mediante [Azure Site Recovery](site-recovery-overview.md)Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="cbcdb-108">Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-108">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="cbcdb-109">Paso 1: Revisar la arquitectura del escenario de Hola</span><span class="sxs-lookup"><span data-stu-id="cbcdb-109">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="cbcdb-110">Antes de iniciar la implementación, revise la arquitectura del escenario de Hola y asegúrese de que comprende todos los componentes de hello debe toodeploy.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-110">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="cbcdb-111">Vaya demasiado[paso 1: revisar la arquitectura de hello](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-111">Go too[Step 1: Review hello architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="cbcdb-112">Paso 2: Revisión de los requisitos previos y las limitaciones</span><span class="sxs-lookup"><span data-stu-id="cbcdb-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="cbcdb-113">Asegúrese de que comprende las limitaciones y requisitos previos de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-113">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="cbcdb-114">**Requisitos previos de Azure**: se necesita una suscripción de Microsoft Azure y servicios de recuperación de Azure del almacén, tooorchestrate y administrar la replicación.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, tooorchestrate and manage replication.</span></span>
<span data-ttu-id="cbcdb-115">**Servidores VMM locales y hosts de Hyper-V**: asegúrese de que los servidores VMM y los hosts de Hyper-V son compatibles y están preparados para la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="cbcdb-116">Vaya demasiado[paso 2: comprobar los requisitos previos y limitaciones](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-116">Go too[Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="cbcdb-117">Paso 3: Planeamiento de redes</span><span class="sxs-lookup"><span data-stu-id="cbcdb-117">Step 3: Plan networking</span></span>

<span data-ttu-id="cbcdb-118">Debe toodo algunos tooensure que puede configurar la asignación de red entre redes de VM de VMM al implementar el escenario de Hola de planeación de una red.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-118">You need toodo some network planning tooensure that you can configure network mapping between VMM VM networks when you deploy hello scenario.</span></span>

<span data-ttu-id="cbcdb-119">Vaya demasiado[paso 3: planear las redes](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-119">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="cbcdb-120">Paso 4: Preparación de VMM y de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="cbcdb-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="cbcdb-121">Preparar servidores VMM de Hola y hosts de Hyper-V para la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-121">Prepare hello VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="cbcdb-122">Vaya demasiado[paso 4: preparar servidores locales](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-122">Go too[Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="cbcdb-123">Paso 5: Configuración de un almacén</span><span class="sxs-lookup"><span data-stu-id="cbcdb-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="cbcdb-124">Configure un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="cbcdb-125">Hola almacén contiene valores de configuración y organiza la replicación.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-125">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="cbcdb-126">Vaya al [paso 5: Configuración de un almacén](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="cbcdb-127">Paso 6: Configuración de los valores de origen y destino</span><span class="sxs-lookup"><span data-stu-id="cbcdb-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="cbcdb-128">Configurar ubicaciones de VMM de replicación de origen y destino Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-128">Set up hello source and target replication VMM locations.</span></span> <span data-ttu-id="cbcdb-129">Agregar el almacén de toohello de servidores VMM hello y descargar archivos de instalación de Hola para los componentes de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-129">Add hello VMM servers toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="cbcdb-130">Ejecute el programa de instalación del proveedor de Azure Site Recovery en el servidor VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-130">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="cbcdb-131">El programa de instalación instala Hola proveedor en el servidor VMM de Hola y registra el servidor hello en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-131">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="cbcdb-132">Instalar a agente de servicios de recuperación de Microsoft de hello en cada host de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-132">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="cbcdb-133">Vaya demasiado[paso 6: configurar los parámetros de origen y de destino de hello](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-133">Go too[Step 6: Set up hello source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="cbcdb-134">Paso 7: Configuración de la asignación de red</span><span class="sxs-lookup"><span data-stu-id="cbcdb-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="cbcdb-135">Asigne redes de VM de VMM en las ubicaciones de origen y destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-135">Map VMM VM networks in hello source and target locations.</span></span> <span data-ttu-id="cbcdb-136">Después de la conmutación por error, las máquinas virtuales se crean en la red de destino de hello esa red de VM de origen de mapas toohello en qué Hola se encuentra una VM de Hyper-V de origen.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-136">After failover, VMs are created in hello target network that maps toohello source VM network in which hello source Hyper-V VM is located.</span></span>

<span data-ttu-id="cbcdb-137">Vaya demasiado[paso 7: configurar la asignación de red](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-137">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="cbcdb-138">Paso 8: Configurar una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="cbcdb-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="cbcdb-139">Especifique cómo se replicarán las máquinas virtuales entre las ubicaciones de VMM.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="cbcdb-140">Vaya demasiado[paso 8: configurar una directiva de replicación](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-140">Go too[Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="cbcdb-141">Paso 9: Habilitación de la replicación para máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="cbcdb-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="cbcdb-142">Seleccione hello las máquinas virtuales que desee tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-142">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="cbcdb-143">Habilitación de una máquina virtual para el sitio secundario de toohello de replicación inicial de Hola de replicación desencadenadores, seguido de la replicación de datos en curso.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-143">Enabling a VM for replication triggers hello initial replication toohello secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="cbcdb-144">Vaya demasiado[paso 9: Habilitar replicación](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-144">Go too[Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="cbcdb-145">Paso 10: Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="cbcdb-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="cbcdb-146">Ejecutar un toomake de conmutación por error de prueba que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="cbcdb-146">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="cbcdb-147">Vaya demasiado[paso 10: ejecutar una prueba de conmutación por error](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="cbcdb-147">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
