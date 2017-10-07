---
title: "aaaReplicate tooAzure de máquinas virtuales VMware con Azure Site Recovery | Documentos de Microsoft"
description: "Proporciona información general de los pasos de hello para la replicación de las cargas de trabajo que se ejecutan en máquinas virtuales VMware tooAzure"
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
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a><span data-ttu-id="0479f-103">Replicar máquinas virtuales VMware tooAzure con Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0479f-103">Replicate VMware VMs tooAzure with Site Recovery</span></span>

<span data-ttu-id="0479f-104">Este artículo proporciona información general de hello pasos necesarios tooreplicate local VMware máquinas virtuales tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0479f-104">This article provides an overview of hello steps required tooreplicate on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


![Proceso de implementación](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="0479f-106">**Figura 1: Resumen del proceso de implementación**</span><span class="sxs-lookup"><span data-stu-id="0479f-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="0479f-107">Paso 1: revisión de la arquitectura y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0479f-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="0479f-108">Antes de iniciar la implementación, revise la arquitectura del escenario de Hola y asegúrese de que comprende todos los componentes de hello necesita toodeploy</span><span class="sxs-lookup"><span data-stu-id="0479f-108">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="0479f-109">Vaya demasiado[paso 1: revisar la arquitectura de Hola](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-109">Go too[Step 1: Review hello architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="0479f-110">Paso 2: revisión de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0479f-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="0479f-111">Asegúrese de que tiene requisitos previos de hello en su lugar para cada componente de implementación:</span><span class="sxs-lookup"><span data-stu-id="0479f-111">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="0479f-112">**Requisitos previos de Azure**: necesita una cuenta de Microsoft Azure, redes de Azure y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0479f-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="0479f-113">**Componentes locales de Site Recovery**: necesita una máquina que ejecute componentes locales de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0479f-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="0479f-114">**Requisitos previos de VMware locales**: necesita tooset cuentas para que la recuperación del sitio puede tener acceso a los servidores de VMware y las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="0479f-114">**On-premises VMware prerequisites**: You need tooset up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="0479f-115">**Replicar máquinas virtuales**: las máquinas virtuales que desee tooreplicate necesidad toocomply requisitos de Azure y tener instalado el componente de servicio de movilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="0479f-115">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements, and have hello Mobility service component installed.</span></span>

<span data-ttu-id="0479f-116">Vaya demasiado[paso 2: revisar los requisitos previos y limitaciones](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-116">Go too[Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="0479f-117">Paso 3: planeamiento de la capacidad</span><span class="sxs-lookup"><span data-stu-id="0479f-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="0479f-118">Si está realizando una implementación completa debe toofigure qué recursos de replicación que se necesita.</span><span class="sxs-lookup"><span data-stu-id="0479f-118">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="0479f-119">Hay un par de toohelp de herramientas disponibles para ello.</span><span class="sxs-lookup"><span data-stu-id="0479f-119">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="0479f-120">Vaya tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="0479f-120">Go tooStep 2.</span></span> <span data-ttu-id="0479f-121">Si está realizando una rápida configurar tootest Hola entorno, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="0479f-121">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="0479f-122">Vaya demasiado[paso 3: planear la capacidad](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-122">Go too[Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="0479f-123">Paso 4: planeamiento de las redes</span><span class="sxs-lookup"><span data-stu-id="0479f-123">Step 4: Plan networking</span></span>

<span data-ttu-id="0479f-124">Debe toodo algunos planeación tooensure que máquinas virtuales de Azure son toonetworks conectado después de producirse la conmutación por error, y que disponen de hello derecho de direcciones IP de una red.</span><span class="sxs-lookup"><span data-stu-id="0479f-124">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="0479f-125">Vaya demasiado[paso 4: planear las redes](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-125">Go too[Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="0479f-126">Paso 5: preparación de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="0479f-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="0479f-127">Antes de empezar hay que configurar las redes y el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0479f-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="0479f-128">Puede hacerlo durante la implementación, pero se recomienda hacerlo antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="0479f-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="0479f-129">Vaya demasiado[paso 5: preparar Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-129">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="0479f-130">Paso 6: Preparación de VMware</span><span class="sxs-lookup"><span data-stu-id="0479f-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="0479f-131">Debe tooset las cuentas que va a usar para recuperación de sitio:</span><span class="sxs-lookup"><span data-stu-id="0479f-131">You need tooset up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="0479f-132">Tooautomatically de servidores de virtualización de VMware de acceso detectar máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="0479f-132">Access VMware virtualization servers tooautomatically detect VMs.</span></span>
- <span data-ttu-id="0479f-133">Obtener acceso a servicio de movilidad de máquinas virtuales tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="0479f-133">Access VMs tooinstall hello Mobility service.</span></span> <span data-ttu-id="0479f-134">Cada máquina virtual que desee tooreplicate debe tener instalado antes de el agente de servicio de movilidad de hello puede habilitar la replicación.</span><span class="sxs-lookup"><span data-stu-id="0479f-134">Each VM you want tooreplicate must have hello Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="0479f-135">Vaya demasiado[paso 6: preparar VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-135">Go too[Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="0479f-136">Paso 7: configuración de un almacén</span><span class="sxs-lookup"><span data-stu-id="0479f-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="0479f-137">Necesita tooset seguridad un tooorchestrate de almacén de servicios de recuperación y administrar la replicación.</span><span class="sxs-lookup"><span data-stu-id="0479f-137">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="0479f-138">Al configurar el almacén de hello, especifique qué desea tooreplicate, y donde quiera tooreplicate a.</span><span class="sxs-lookup"><span data-stu-id="0479f-138">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="0479f-139">Vaya demasiado[paso 7: configurar un almacén](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-139">Go too[Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="0479f-140">Paso 8: configuración de los valores de origen y destino</span><span class="sxs-lookup"><span data-stu-id="0479f-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="0479f-141">Configurar origen de Hola y de destino que se usa para la replicación.</span><span class="sxs-lookup"><span data-stu-id="0479f-141">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="0479f-142">Establecer la configuración de origen incluye ejecutando el programa de instalación unificada tooinstall componentes de Site Recovery de hello locales.</span><span class="sxs-lookup"><span data-stu-id="0479f-142">Setting up source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="0479f-143">Vaya demasiado[paso 8: configurar el origen de Hola y de destino](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-143">Go too[Step 8: Set up hello source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="0479f-144">Paso 9: configuración de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="0479f-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="0479f-145">Configurar una configuración de directiva toospecify replicación para máquinas virtuales VMware en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="0479f-145">You set up a policy toospecify replication settings for VMware VMs in hello vault.</span></span>

<span data-ttu-id="0479f-146">Vaya demasiado[paso 9: configurar una directiva de replicación](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-146">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="0479f-147">Paso 10: Instalar el servicio de movilidad de Hola</span><span class="sxs-lookup"><span data-stu-id="0479f-147">Step 10: Install hello Mobility service</span></span>

<span data-ttu-id="0479f-148">servicio de movilidad de Hello debe estar instalado en cada máquina virtual que desee tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="0479f-148">hello Mobility service must be installed on each VM you want tooreplicate.</span></span> <span data-ttu-id="0479f-149">Hay unos tooset formas servicio Hola con la instalación de inserción o extracción.</span><span class="sxs-lookup"><span data-stu-id="0479f-149">There are a few ways tooset up hello service with push or pull installation.</span></span>

<span data-ttu-id="0479f-150">Vaya demasiado[paso 10: instalar el servicio de movilidad de Hola](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-150">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="0479f-151">Paso 11: Habilitación de la replicación</span><span class="sxs-lookup"><span data-stu-id="0479f-151">Step 11: Enable replication</span></span>

<span data-ttu-id="0479f-152">Después de hello Mobility service se ejecuta en una máquina virtual se puede habilitar la replicación.</span><span class="sxs-lookup"><span data-stu-id="0479f-152">After hello Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="0479f-153">Después de habilitar esta opción, se produce la replicación inicial de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0479f-153">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="0479f-154">Vaya demasiado[paso 11: habilitar la replicación](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-154">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="0479f-155">Paso 12: Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="0479f-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="0479f-156">Después de que finalice la replicación inicial y replicación de datos se está ejecutando, puede ejecutar una toomake de conmutación por error de prueba seguro de que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="0479f-156">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="0479f-157">Vaya demasiado[paso 12: ejecutar una prueba de conmutación por error](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="0479f-157">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
