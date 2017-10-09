---
title: "aaaReplicate tooAzure de máquinas virtuales de Hyper-V con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo la replicación tooorchestrate, conmutación por error y recuperación de local Hyper-V VM tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a><span data-ttu-id="ff368-103">Replicar tooAzure de máquinas virtuales (sin WMM) de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ff368-103">Replicate Hyper-V virtual machines (without VMM) tooAzure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff368-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ff368-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="ff368-105">Azure clásico</span><span class="sxs-lookup"><span data-stu-id="ff368-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="ff368-106">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="ff368-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="ff368-107">Este artículo proporciona información general de hello pasos necesarios tooreplicate local Hyper-V máquinas virtuales tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff368-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="ff368-108">En esta implementación, las máquinas virtuales de Hyper-V no están administradas por System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="ff368-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="ff368-109">Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ff368-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="ff368-110">Paso 1: revisión de la arquitectura y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ff368-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="ff368-111">Antes de iniciar la implementación, revise la arquitectura del escenario de Hola y asegúrese de que comprende todos los componentes de hello necesita toodeploy</span><span class="sxs-lookup"><span data-stu-id="ff368-111">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="ff368-112">Vaya demasiado[paso 1: revisar la arquitectura de Hola](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-112">Go too[Step 1: Review hello architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="ff368-113">Paso 2: revisión de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ff368-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="ff368-114">Asegúrese de que tiene requisitos previos de hello en su lugar para cada componente de implementación:</span><span class="sxs-lookup"><span data-stu-id="ff368-114">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="ff368-115">**Requisitos previos de Azure**: necesita una cuenta de Microsoft Azure, redes de Azure y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ff368-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="ff368-116">**Requisitos previos de Hyper-V local**: asegúrese de que los hosts de Hyper-V están preparados para la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ff368-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="ff368-117">**Replicar máquinas virtuales**: las máquinas virtuales que desee tooreplicate necesita toocomply requisitos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff368-117">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements.</span></span>

<span data-ttu-id="ff368-118">Vaya demasiado[paso 2: comprobar los requisitos previos y limitaciones](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-118">Go too[Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="ff368-119">Paso 3: planeamiento de la capacidad</span><span class="sxs-lookup"><span data-stu-id="ff368-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="ff368-120">Si está realizando una implementación completa debe toofigure qué recursos de replicación que se necesita.</span><span class="sxs-lookup"><span data-stu-id="ff368-120">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="ff368-121">Hay un par de toohelp de herramientas disponibles para ello.</span><span class="sxs-lookup"><span data-stu-id="ff368-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="ff368-122">Vaya tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="ff368-122">Go tooStep 2.</span></span> <span data-ttu-id="ff368-123">Si está realizando una rápida configurar tootest Hola entorno, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="ff368-123">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="ff368-124">Vaya demasiado[paso 3: planear la capacidad](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-124">Go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="ff368-125">Paso 4: planeamiento de las redes</span><span class="sxs-lookup"><span data-stu-id="ff368-125">Step 4: Plan networking</span></span>

<span data-ttu-id="ff368-126">Debe toodo algunos planeación tooensure que máquinas virtuales de Azure son toonetworks conectado después de producirse la conmutación por error, y que disponen de hello derecho de direcciones IP de una red.</span><span class="sxs-lookup"><span data-stu-id="ff368-126">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="ff368-127">Vaya demasiado[paso 4: planear las redes](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-127">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="ff368-128">Paso 5: preparación de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="ff368-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="ff368-129">Antes de empezar hay que configurar las redes y el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff368-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="ff368-130">Puede hacerlo durante la implementación, pero se recomienda hacerlo antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="ff368-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="ff368-131">Vaya demasiado[paso 5: preparar Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-131">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="ff368-132">Paso 6: preparación de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ff368-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="ff368-133">Asegúrese de que los servidores de Hyper-V cumplen los requisitos de implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ff368-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="ff368-134">Vaya demasiado[paso 6: preparar Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-134">Go too[Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="ff368-135">Paso 7: configuración de un almacén</span><span class="sxs-lookup"><span data-stu-id="ff368-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="ff368-136">Necesita tooset seguridad un tooorchestrate de almacén de servicios de recuperación y administrar la replicación.</span><span class="sxs-lookup"><span data-stu-id="ff368-136">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="ff368-137">Al configurar el almacén de hello, especifique qué desea tooreplicate, y donde quiera tooreplicate a.</span><span class="sxs-lookup"><span data-stu-id="ff368-137">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="ff368-138">Vaya demasiado[paso 7: crear un almacén](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-138">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="ff368-139">Paso 8: configuración de los valores de origen y destino</span><span class="sxs-lookup"><span data-stu-id="ff368-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="ff368-140">Configurar origen de Hola y de destino que se usa para la replicación.</span><span class="sxs-lookup"><span data-stu-id="ff368-140">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="ff368-141">Establecer la configuración de origen incluye la adición de hosts de Hyper-V tooa sitio de Hyper-V, instalar Hola proveedor de Site Recovery y el agente de servicios de recuperación en cada host de Hyper-V y registrar sitio Hola Hola que del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="ff368-141">Setting up source settings includes adding Hyper-V hosts tooa Hyper-V site, installing hello Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering hello site in hello Recovery Services vault.</span></span>

<span data-ttu-id="ff368-142">Vaya demasiado[paso 8: configurar el origen de Hola y de destino](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-142">Go too[Step 8: Set up hello source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="ff368-143">Paso 9: configuración de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="ff368-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="ff368-144">Configurar una configuración de directiva toospecify replicación para máquinas virtuales de Hyper-V en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff368-144">You set up a policy toospecify replication settings for Hyper-V VMs in hello vault.</span></span>

<span data-ttu-id="ff368-145">Vaya demasiado[paso 9: configurar una directiva de replicación](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-145">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="ff368-146">Paso 10: habilitación de la replicación</span><span class="sxs-lookup"><span data-stu-id="ff368-146">Step 10: Enable replication</span></span>

<span data-ttu-id="ff368-147">Una vez que una directiva de replicación en su lugar, después de habilitar, se produce la replicación inicial de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ff368-147">After you have a replication policy in place,  After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="ff368-148">Vaya demasiado[paso 10: habilitar la replicación](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-148">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="ff368-149">Paso 11: ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="ff368-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="ff368-150">Después de que finalice la replicación inicial y replicación de datos se está ejecutando, puede ejecutar una toomake de conmutación por error de prueba seguro de que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="ff368-150">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="ff368-151">Vaya demasiado[paso 11: ejecutar una prueba de conmutación por error](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="ff368-151">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
