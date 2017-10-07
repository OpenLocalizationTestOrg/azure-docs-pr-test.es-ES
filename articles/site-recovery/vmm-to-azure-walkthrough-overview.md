---
title: "nubes de máquinas virtuales de Hyper-V en VMM aaaReplicate tooAzure con Azure Site Recovery | Documentos de Microsoft"
description: "Proporciona información general para la replicación de máquinas virtuales de Hyper-V en tooAzure de nubes VMM con el servicio de Azure Site Recovery Hola"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a><span data-ttu-id="71e65-103">Replicar máquinas virtuales de Hyper-V en tooAzure de nubes VMM con Site Recovery en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="71e65-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71e65-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="71e65-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="71e65-105">Azure clásico</span><span class="sxs-lookup"><span data-stu-id="71e65-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="71e65-106">PowerShell Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71e65-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="71e65-107">PowerShell clásico</span><span class="sxs-lookup"><span data-stu-id="71e65-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="71e65-108">Este artículo se proporciona una visión general de hello pasos necesarios tooreplicate máquinas de virtuales de Hyper-V (VM) administradas en tooAzure de nubes de System Center Virtual Machine Manager (VMM), con hello local [Azure Site Recovery](site-recovery-overview.md) servicio en Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="71e65-108">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="71e65-109">Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="71e65-109">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="71e65-110">Paso 1: Revisar la arquitectura del escenario de Hola</span><span class="sxs-lookup"><span data-stu-id="71e65-110">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="71e65-111">Antes de iniciar la implementación, revise la arquitectura del escenario de Hola y asegúrese de que comprende todos los componentes de hello debe toodeploy.</span><span class="sxs-lookup"><span data-stu-id="71e65-111">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="71e65-112">Vaya demasiado[paso 1: revisar la arquitectura de Hola](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-112">Go too[Step 1: Review hello architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="71e65-113">Paso 2: Revisión de los requisitos previos y las limitaciones</span><span class="sxs-lookup"><span data-stu-id="71e65-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="71e65-114">Asegúrese de que comprende las limitaciones y requisitos previos de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="71e65-114">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="71e65-115">**Requisitos previos de Azure**: necesita una cuenta de Microsoft Azure, redes de Azure y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="71e65-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="71e65-116">**Servidores VMM locales y hosts de Hyper-V**: asegúrese de que los servidores VMM y los hosts de Hyper-V son compatibles y están preparados para la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="71e65-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="71e65-117">**Replicar máquinas virtuales**: Compruebe que las máquinas virtuales que desee tooreplicate cumplan con requisitos de Azure.</span><span class="sxs-lookup"><span data-stu-id="71e65-117">**Replicated VMs**: Check that VMs you want tooreplicate comply with Azure requirements.</span></span>

<span data-ttu-id="71e65-118">Vaya demasiado[paso 2: comprobar los requisitos previos y limitaciones](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-118">Go too[Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="71e65-119">Paso 3: planeamiento de la capacidad</span><span class="sxs-lookup"><span data-stu-id="71e65-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="71e65-120">Si está realizando una implementación completa, deberá toofigure qué recursos de replicación que se necesita.</span><span class="sxs-lookup"><span data-stu-id="71e65-120">If you're doing a full deployment, you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="71e65-121">Hay un par de toohelp de herramientas disponibles para ello.</span><span class="sxs-lookup"><span data-stu-id="71e65-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="71e65-122">Si está realizando una rápida configurar tootest Hola entorno, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="71e65-122">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="71e65-123">Vaya demasiado[paso 3: planear la capacidad](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-123">Go too[Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="71e65-124">Paso 4: planeamiento de las redes</span><span class="sxs-lookup"><span data-stu-id="71e65-124">Step 4: Plan networking</span></span>

<span data-ttu-id="71e65-125">Debe toodo alguna de las redes planeación tooensure que puede configurar la asignación de red al implementar el escenario de hello, máquinas virtuales de Azure será tooAzure conectado las redes virtuales después de que se produce la conmutación por error y que estén asignados IP adecuado se resuelve.</span><span class="sxs-lookup"><span data-stu-id="71e65-125">You need toodo some network planning tooensure that you can configure network mapping when you deploy hello scenario, that Azure VMs will be connected tooAzure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="71e65-126">Vaya demasiado[paso 4: planear las redes](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-126">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="71e65-127">Paso 5: preparación de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="71e65-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="71e65-128">Configure almacenamiento, redes y una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="71e65-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="71e65-129">Puede hacerlo durante la implementación, pero se recomienda hacerlo antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="71e65-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="71e65-130">Vaya demasiado[paso 5: preparar Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-130">Go too[Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="71e65-131">Paso 6: Preparación de VMM y Hyper-V</span><span class="sxs-lookup"><span data-stu-id="71e65-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="71e65-132">Preparar servidores VMM locales de Hola y hosts de Hyper-V para la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="71e65-132">Prepare hello on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="71e65-133">Vaya demasiado[paso 6: preparar servidores locales](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-133">Go too[Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="71e65-134">Paso 7: configuración de un almacén</span><span class="sxs-lookup"><span data-stu-id="71e65-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="71e65-135">Configure un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="71e65-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="71e65-136">Hola almacén contiene valores de configuración y organiza la replicación.</span><span class="sxs-lookup"><span data-stu-id="71e65-136">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="71e65-137">[Step 7: Set up a vault](vmm-to-azure-walkthrough-create-vault.md) (Paso 7: Configuración de un almacén)</span><span class="sxs-lookup"><span data-stu-id="71e65-137">[Step 7: Set up a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="71e65-138">Paso 8: configuración de los valores de origen y destino</span><span class="sxs-lookup"><span data-stu-id="71e65-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="71e65-139">Configurar ubicaciones de replicación de origen y destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="71e65-139">Set up hello source and target replication locations.</span></span> <span data-ttu-id="71e65-140">Agregar el almacén de toohello de servidor VMM hello y descargar archivos de instalación de Hola para los componentes de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="71e65-140">Add hello VMM server toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="71e65-141">Ejecute el programa de instalación del proveedor de Azure Site Recovery en el servidor VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="71e65-141">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="71e65-142">El programa de instalación instala Hola proveedor en el servidor VMM de Hola y registra el servidor hello en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="71e65-142">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="71e65-143">Instalar a agente de servicios de recuperación de Microsoft de hello en cada host de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="71e65-143">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="71e65-144">Vaya demasiado[paso 8: configurar opciones de origen y de destino](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-144">Go too[Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="71e65-145">Paso 9: Configuración de la asignación de red</span><span class="sxs-lookup"><span data-stu-id="71e65-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="71e65-146">Asignación de redes virtuales de tooAzure de redes de VM de VMM en local.</span><span class="sxs-lookup"><span data-stu-id="71e65-146">Map on-premises VMM VM networks tooAzure virtual networks.</span></span> <span data-ttu-id="71e65-147">Después de la conmutación por error, máquinas virtuales de Azure se crean en hello red de Azure que se asigna la red de máquina virtual local toohello en qué Hola Hyper-V de origen se encuentra.</span><span class="sxs-lookup"><span data-stu-id="71e65-147">After failover, Azure VMs are created in hello Azure network that maps toohello on-premises VM network in which hello source Hyper-V is located.</span></span>

<span data-ttu-id="71e65-148">Vaya demasiado[paso 9: configurar la asignación de red](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-148">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="71e65-149">Paso 10: Configuración de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="71e65-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="71e65-150">Especificar cómo máquinas virtuales locales serán tooAzure replicada.</span><span class="sxs-lookup"><span data-stu-id="71e65-150">Specify how on-premises VMs will be replicated tooAzure.</span></span>

<span data-ttu-id="71e65-151">Vaya demasiado[paso 10: configurar una directiva de replicación](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-151">Go too[Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="71e65-152">Paso 11: Habilitación de la replicación para máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="71e65-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="71e65-153">Seleccione hello las máquinas virtuales que desee tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="71e65-153">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="71e65-154">Habilitación de una máquina virtual para tooAzure de replicación inicial de Hola de desencadenadores de replicación, seguido de la replicación de datos en curso.</span><span class="sxs-lookup"><span data-stu-id="71e65-154">ENabling a VM for replication triggers hello initial replication tooAzure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="71e65-155">Vaya demasiado[paso 11: habilitar la replicación](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-155">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="71e65-156">Paso 12: Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="71e65-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="71e65-157">Ejecutar un toomake de conmutación por error de prueba que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="71e65-157">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="71e65-158">Vaya demasiado[paso 12: ejecutar una prueba de conmutación por error](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="71e65-158">Go too[Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


