---
title: "Replicación de máquinas virtuales VMware en Azure con Azure Site Recovery | Microsoft Docs"
description: "Ofrece una introducción a los pasos necesarios para replicar cargas de trabajo que se ejecutan en máquinas virtuales VMware en Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: db6f5f95929503e82a529dba26b56af1edb0767f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-vms-to-azure-with-site-recovery"></a><span data-ttu-id="8eb88-103">Replicación de máquinas virtuales VMware en Azure con Site Recovery</span><span class="sxs-lookup"><span data-stu-id="8eb88-103">Replicate VMware VMs to Azure with Site Recovery</span></span>

<span data-ttu-id="8eb88-104">En este artículo se ofrece información general sobre los pasos necesarios para replicar máquinas virtuales VMware en Azure con el servicio [Azure Site Recovery](site-recovery-overview.md) de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8eb88-104">This article provides an overview of the steps required to replicate on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


![Proceso de implementación](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="8eb88-106">**Figura 1: Resumen del proceso de implementación**</span><span class="sxs-lookup"><span data-stu-id="8eb88-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="8eb88-107">Paso 1: Revisión de la arquitectura y los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8eb88-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="8eb88-108">Antes de empezar la implementación, revise la arquitectura del escenario y asegúrese de comprender todos los componentes que necesita implementar.</span><span class="sxs-lookup"><span data-stu-id="8eb88-108">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="8eb88-109">Vaya al [paso 1: revisión de la arquitectura](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-109">Go to [Step 1: Review the architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="8eb88-110">Paso 2: revisión de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8eb88-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="8eb88-111">Asegúrese de satisfacer los requisitos previos de cada componente de la implementación:</span><span class="sxs-lookup"><span data-stu-id="8eb88-111">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="8eb88-112">**Requisitos previos de Azure**: necesita una cuenta de Microsoft Azure, redes de Azure y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8eb88-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="8eb88-113">**Componentes locales de Site Recovery**: necesita una máquina que ejecute componentes locales de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8eb88-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="8eb88-114">**Requisitos previos de VMware**: necesita configurar cuentas para que Site Recovery pueda acceder a los servidores y las máquinas virtuales VMware.</span><span class="sxs-lookup"><span data-stu-id="8eb88-114">**On-premises VMware prerequisites**: You need to set up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="8eb88-115">**Máquinas virtuales replicadas**: las máquinas virtuales que quiera replicar tienen que cumplir con los requisitos de Azure y tener el componente Mobility Service instalado.</span><span class="sxs-lookup"><span data-stu-id="8eb88-115">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements, and have the Mobility service component installed.</span></span>

<span data-ttu-id="8eb88-116">Ir a [Paso 2: Revisión de los requisitos previos y las limitaciones](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-116">Go to [Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="8eb88-117">Paso 3: Planeamiento de la capacidad</span><span class="sxs-lookup"><span data-stu-id="8eb88-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="8eb88-118">Si está realizando una implementación completa, debe averiguar qué recursos de replicación necesita.</span><span class="sxs-lookup"><span data-stu-id="8eb88-118">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="8eb88-119">Hay un par de herramientas disponibles para ayudarle a hacerlo.</span><span class="sxs-lookup"><span data-stu-id="8eb88-119">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="8eb88-120">Vaya al paso 2.</span><span class="sxs-lookup"><span data-stu-id="8eb88-120">Go to Step 2.</span></span> <span data-ttu-id="8eb88-121">Si está realizando una configuración rápida para probar el entorno, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="8eb88-121">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="8eb88-122">Vaya al [paso 3: planeamiento de la capacidad](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-122">Go to [Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="8eb88-123">Paso 4: planeamiento de las redes</span><span class="sxs-lookup"><span data-stu-id="8eb88-123">Step 4: Plan networking</span></span>

<span data-ttu-id="8eb88-124">Debe planear las redes para asegurarse de que las máquinas virtuales de Azure estén conectadas a redes después de que se produzca la conmutación por error y de que tengan la dirección IP correcta.</span><span class="sxs-lookup"><span data-stu-id="8eb88-124">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="8eb88-125">Vaya al [paso 4: planeamiento de las redes](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-125">Go to [Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="8eb88-126">Paso 5: preparación de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="8eb88-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="8eb88-127">Antes de empezar hay que configurar las redes y el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8eb88-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="8eb88-128">Puede hacerlo durante la implementación, pero se recomienda hacerlo antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="8eb88-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="8eb88-129">Vaya al [Paso 5: Preparación de Azure](vmware-walkthrough-prepare-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8eb88-129">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="8eb88-130">Paso 6: Preparación de VMware</span><span class="sxs-lookup"><span data-stu-id="8eb88-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="8eb88-131">Debe configurar las cuentas que Site Recovery va a usar:</span><span class="sxs-lookup"><span data-stu-id="8eb88-131">You need to set up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="8eb88-132">Acceda a los servidores de virtualización VMware para detectar automáticamente las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8eb88-132">Access VMware virtualization servers to automatically detect VMs.</span></span>
- <span data-ttu-id="8eb88-133">Acceda a las máquinas virtuales para instalar Mobility Service.</span><span class="sxs-lookup"><span data-stu-id="8eb88-133">Access VMs to install the Mobility service.</span></span> <span data-ttu-id="8eb88-134">Cada máquina virtual que quiera replicar debe tener instalado el agente de Mobility Service para que pueda habilitar la replicación en él.</span><span class="sxs-lookup"><span data-stu-id="8eb88-134">Each VM you want to replicate must have the Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="8eb88-135">Ir al [Paso 6: Preparación de VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-135">Go to [Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="8eb88-136">Paso 7: Configuración de un almacén</span><span class="sxs-lookup"><span data-stu-id="8eb88-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="8eb88-137">Debe configurar un almacén de Recovery Services para organizar y administrar la replicación.</span><span class="sxs-lookup"><span data-stu-id="8eb88-137">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="8eb88-138">Cuando configure el almacén, especifique lo que quiere replicar y en dónde.</span><span class="sxs-lookup"><span data-stu-id="8eb88-138">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="8eb88-139">Ir a [Paso 7: Configuración de un almacén](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-139">Go to [Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="8eb88-140">Paso 8: Configuración de los valores de origen y destino</span><span class="sxs-lookup"><span data-stu-id="8eb88-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="8eb88-141">Configure el origen y el destino que se usan para la replicación.</span><span class="sxs-lookup"><span data-stu-id="8eb88-141">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="8eb88-142">La configuración del origen incluye la ejecución de la instalación unificada para instalar los componentes locales de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8eb88-142">Setting up source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="8eb88-143">Ir a [Paso 8: Configuración del origen y el destino](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-143">Go to [Step 8: Set up the source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="8eb88-144">Paso 9: Configuración de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="8eb88-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="8eb88-145">Configure una directiva que especifique la configuración de la replicación para las máquinas virtuales VMware del almacén.</span><span class="sxs-lookup"><span data-stu-id="8eb88-145">You set up a policy to specify replication settings for VMware VMs in the vault.</span></span>

<span data-ttu-id="8eb88-146">Ir al [Paso 9: Configuración de una directiva de replicación](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-146">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="8eb88-147">Paso 10: Instalación de Mobility Service</span><span class="sxs-lookup"><span data-stu-id="8eb88-147">Step 10: Install the Mobility service</span></span>

<span data-ttu-id="8eb88-148">Mobility Service debe instalarse en cada máquina que quiera replicar.</span><span class="sxs-lookup"><span data-stu-id="8eb88-148">The Mobility service must be installed on each VM you want to replicate.</span></span> <span data-ttu-id="8eb88-149">Hay varias maneras de configurar el servicio, con instalación de inserción o de extracción.</span><span class="sxs-lookup"><span data-stu-id="8eb88-149">There are a few ways to set up the service with push or pull installation.</span></span>

<span data-ttu-id="8eb88-150">Ir a [Paso 10: Instalación de Mobility Service](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-150">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="8eb88-151">Paso 11: Habilitación de la replicación</span><span class="sxs-lookup"><span data-stu-id="8eb88-151">Step 11: Enable replication</span></span>

<span data-ttu-id="8eb88-152">Una vez que Mobility Service se está ejecutando en una máquina virtual, puede habilitar su replicación.</span><span class="sxs-lookup"><span data-stu-id="8eb88-152">After the Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="8eb88-153">Después de habilitarla, se produce la replicación inicial de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8eb88-153">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="8eb88-154">Ir a [Paso 11: Habilitación de la replicación](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-154">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="8eb88-155">Paso 12: Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="8eb88-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="8eb88-156">Una vez que termina la replicación inicial y se está ejecutando la replicación diferencial, puede ejecutar una conmutación por error de prueba para asegurarse de que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="8eb88-156">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="8eb88-157">Ir a [Paso 12: Ejecución de una conmutación por error de prueba](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="8eb88-157">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
