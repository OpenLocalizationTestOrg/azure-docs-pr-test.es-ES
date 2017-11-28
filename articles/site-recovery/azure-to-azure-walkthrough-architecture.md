---
title: "arquitectura de hello aaaReview para la replicación de máquinas virtuales de Azure entre regiones de Azure | Documentos de Microsoft"
description: "Este artículo proporciona información general de componentes y arquitectura que se usa al replicar máquinas virtuales de Azure entre regiones de Azure mediante el servicio de Azure Site Recovery Hola."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="a2f1f-103">Paso 1: Revisar la arquitectura de hello para la replicación de máquina virtual de Azure entre regiones de Azure</span><span class="sxs-lookup"><span data-stu-id="a2f1f-103">Step 1: Review hello architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="a2f1f-104">Después de revisar hello [pasos generales](azure-to-azure-walkthrough-overview.md) para esta implementación, lea este componentes de artículo toounderstand hello y procesos que se utilizan cuando la replicación y recuperación de máquinas virtuales de Azure (VM) de tooanother de una región de Azure, usando [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2f1f-104">After reviewing hello [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article toounderstand hello components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region tooanother, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="a2f1f-105">Cuando termine de artículo hello, debe tener una idea clara de cómo funciona la región de tooanother de replicación de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-105">When you finish hello article, you should have a clear understanding of how Azure VM replication tooanother region works.</span></span>
- <span data-ttu-id="a2f1f-106">Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a2f1f-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="a2f1f-107">Replicación de máquina virtual de Azure con hello servicio Site Recovery está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-107">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="a2f1f-108">Componentes de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="a2f1f-108">Architectural components</span></span>

<span data-ttu-id="a2f1f-109">Hola siguiente diagrama proporciona una visión general de un entorno de máquina virtual de Azure en una región específica (en este ejemplo, hello ubicación UU).</span><span class="sxs-lookup"><span data-stu-id="a2f1f-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="a2f1f-110">En un entorno de máquina virtual de Azure:</span><span class="sxs-lookup"><span data-stu-id="a2f1f-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="a2f1f-111">Las aplicaciones pueden ejecutarse en máquinas virtuales con discos repartidos entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="a2f1f-112">Hola máquinas virtuales puede incluirse en una o más subredes dentro de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![Entorno de cliente](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="a2f1f-114">Proceso de replicación</span><span class="sxs-lookup"><span data-stu-id="a2f1f-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="a2f1f-115">Paso 1</span><span class="sxs-lookup"><span data-stu-id="a2f1f-115">Step 1</span></span>

<span data-ttu-id="a2f1f-116">Cuando se habilita la replicación de máquina virtual de Azure en hello portal de Azure, Hola recursos que se muestran en hello después de diagrama y la tabla se crean automáticamente en la región de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-116">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="a2f1f-117">De forma predeterminada, los recursos se crean en función de la configuración de la región de origen.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="a2f1f-118">Puede personalizar la configuración de destino de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-118">You can customize hello target settings as required.</span></span> <span data-ttu-id="a2f1f-119">[Más información](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a2f1f-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Habilitación del proceso de replicación, paso 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="a2f1f-121">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="a2f1f-121">**Resource**</span></span> | <span data-ttu-id="a2f1f-122">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="a2f1f-122">**Details**</span></span>
--- | ---
<span data-ttu-id="a2f1f-123">**Grupo de recursos de destino**</span><span class="sxs-lookup"><span data-stu-id="a2f1f-123">**Target resource group**</span></span> | <span data-ttu-id="a2f1f-124">Hola toowhich de grupo de recursos pertenecen máquinas virtuales replicadas después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-124">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="a2f1f-125">**Red virtual de destino**</span><span class="sxs-lookup"><span data-stu-id="a2f1f-125">**Target virtual network**</span></span> | <span data-ttu-id="a2f1f-126">red virtual de Hello en el que se encuentran máquinas virtuales replicadas después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-126">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="a2f1f-127">Se crea una asignación de red entre las redes virtuales de origen y de destino y viceversa.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="a2f1f-128">**Cuentas de almacenamiento en caché**</span><span class="sxs-lookup"><span data-stu-id="a2f1f-128">**Cache storage accounts**</span></span> | <span data-ttu-id="a2f1f-129">Antes de que los cambios en el origen de que las máquinas virtuales repliquen toohello cuenta de almacenamiento de destino, se realiza un seguimiento y envían toohello cuenta de almacenamiento de caché en la ubicación de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-129">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="a2f1f-130">Esto garantiza un impacto mínimo en aplicaciones de producción que se ejecutan en VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-130">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="a2f1f-131">**Cuentas de almacenamiento de destino**</span><span class="sxs-lookup"><span data-stu-id="a2f1f-131">**Target storage accounts**</span></span>  | <span data-ttu-id="a2f1f-132">Cuentas de almacenamiento de datos de hello destino ubicación toowhich Hola se replica.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-132">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="a2f1f-133">**Conjuntos de disponibilidad de destino**</span><span class="sxs-lookup"><span data-stu-id="a2f1f-133">**Target availability sets**</span></span>  | <span data-ttu-id="a2f1f-134">Conjuntos de disponibilidad de qué Hola replicar las máquinas virtuales se encuentran después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-134">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="a2f1f-135">Paso 2</span><span class="sxs-lookup"><span data-stu-id="a2f1f-135">Step 2</span></span>

<span data-ttu-id="a2f1f-136">Como la replicación está habilitada, Hola extensión servicio de movilidad de Site Recovery se instala automáticamente en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-136">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="a2f1f-137">se produce el siguiente Hello:</span><span class="sxs-lookup"><span data-stu-id="a2f1f-137">hello following occurs:</span></span>

1. <span data-ttu-id="a2f1f-138">Hola VM está registrado con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-138">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="a2f1f-139">La replicación continua está configurada para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-139">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="a2f1f-140">Escrituras de datos en hello VM discos estén continuamente transfieren toohello cuenta de almacenamiento de caché en la ubicación de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-140">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Habilitación del proceso de replicación, paso 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="a2f1f-142">Tenga en cuenta que Site Recovery nunca necesita conectividad toohello VM de entrada.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-142">Note that Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="a2f1f-143">Solo salida direcciones TCP/IP direcciones URL de servicio de recuperación de tooSite de conectividad, direcciones de TCP/IP direcciones URL de autenticación de Office 365 y direcciones IP de cuenta de almacenamiento de caché es necesario.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-143">Only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="a2f1f-144">Proceso de replicación continua</span><span class="sxs-lookup"><span data-stu-id="a2f1f-144">Continuous replication process</span></span>

<span data-ttu-id="a2f1f-145">Después de que funciona la replicación continua, disco escribe inmediatamente transfiere toohello cuenta de almacenamiento de caché.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-145">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="a2f1f-146">Recuperación de sitio procesa los datos de Hola y envía toohello cuenta de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-146">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="a2f1f-147">Después de que se procesan los datos de hello, puntos de recuperación se generan en la cuenta de almacenamiento de destino de hello cada pocos minutos.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-147">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="a2f1f-148">Proceso de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="a2f1f-148">Failover process</span></span>

<span data-ttu-id="a2f1f-149">Cuando se inicia una conmutación por error, hello y hello que las máquinas virtuales se crean en el grupo de recursos de destino de hello, la red virtual de destino, la subred de destino conjunto de disponibilidad de destino.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-149">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="a2f1f-150">Durante una conmutación por error, puede usar cualquier punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="a2f1f-150">During a failover, you can use any recovery point.</span></span>

![Proceso de conmutación por error](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="a2f1f-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2f1f-152">Next steps</span></span>

<span data-ttu-id="a2f1f-153">Vaya demasiado[paso 2: comprobar los requisitos previos y limitaciones](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="a2f1f-153">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
