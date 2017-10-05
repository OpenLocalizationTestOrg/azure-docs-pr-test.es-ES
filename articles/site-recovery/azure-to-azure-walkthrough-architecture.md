---
title: "Revise la arquitectura para la replicación de máquinas virtuales de Azure entre regiones de Azure | Microsoft Docs"
description: "En este artículo se proporciona una visión general de los componentes y la arquitectura usados al replicar máquinas virtuales de Azure entre regiones de Azure mediante el servicio de Azure Site Recovery."
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
ms.openlocfilehash: f471add4f4dee26482e2820fb06d010d6c0c0e88
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="step-1-review-the-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="613f4-103">Paso 1: Revisión de la arquitectura para la replicación de una máquina virtual de Azure entre regiones de Azure</span><span class="sxs-lookup"><span data-stu-id="613f4-103">Step 1: Review the architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="613f4-104">Después de revisar los [pasos generales](azure-to-azure-walkthrough-overview.md) para esta implementación, lea este artículo para entender los componentes y procesos que se utilizan cuando se replican y recuperan Azure Virtual Machines (VM) de una región de Azure en otra, mediante [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="613f4-104">After reviewing the [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article to understand the components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region to another, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="613f4-105">Cuando termine el artículo, debe tener una idea clara de cómo funciona la replicación de una máquina virtual de Azure en otra región.</span><span class="sxs-lookup"><span data-stu-id="613f4-105">When you finish the article, you should have a clear understanding of how Azure VM replication to another region works.</span></span>
- <span data-ttu-id="613f4-106">Publique cualquier comentario en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="613f4-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="613f4-107">La replicación de máquinas virtuales de Azure con el servicio de Site Recovery está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="613f4-107">Azure VM replication with the Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="613f4-108">Componentes de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="613f4-108">Architectural components</span></span>

<span data-ttu-id="613f4-109">En el siguiente diagrama se proporciona una visión de alto nivel de un entorno de máquina virtual de Azure en una región específica (en este ejemplo, la ubicación Este de EE. UU.).</span><span class="sxs-lookup"><span data-stu-id="613f4-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="613f4-110">En un entorno de máquina virtual de Azure:</span><span class="sxs-lookup"><span data-stu-id="613f4-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="613f4-111">Las aplicaciones pueden ejecutarse en máquinas virtuales con discos repartidos entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="613f4-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="613f4-112">Las máquinas virtuales pueden incluirse en una o más subredes dentro de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="613f4-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![Entorno de cliente](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="613f4-114">Proceso de replicación</span><span class="sxs-lookup"><span data-stu-id="613f4-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="613f4-115">Paso 1</span><span class="sxs-lookup"><span data-stu-id="613f4-115">Step 1</span></span>

<span data-ttu-id="613f4-116">Cuando se habilita la replicación de máquinas virtuales de Azure en Azure Portal, se crean automáticamente en la región de destino los recursos que se muestran en el siguiente diagrama y tabla.</span><span class="sxs-lookup"><span data-stu-id="613f4-116">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="613f4-117">De forma predeterminada, los recursos se crean en función de la configuración de la región de origen.</span><span class="sxs-lookup"><span data-stu-id="613f4-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="613f4-118">Puede personalizar la configuración de destino según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="613f4-118">You can customize the target settings as required.</span></span> <span data-ttu-id="613f4-119">[Más información](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="613f4-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Habilitación del proceso de replicación, paso 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="613f4-121">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="613f4-121">**Resource**</span></span> | <span data-ttu-id="613f4-122">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="613f4-122">**Details**</span></span>
--- | ---
<span data-ttu-id="613f4-123">**Grupo de recursos de destino**</span><span class="sxs-lookup"><span data-stu-id="613f4-123">**Target resource group**</span></span> | <span data-ttu-id="613f4-124">El grupo de recursos a los que pertenecen las máquinas virtuales replicadas después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="613f4-124">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="613f4-125">**Red virtual de destino**</span><span class="sxs-lookup"><span data-stu-id="613f4-125">**Target virtual network**</span></span> | <span data-ttu-id="613f4-126">La red virtual en el que se encuentran las máquinas virtuales replicadas después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="613f4-126">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="613f4-127">Se crea una asignación de red entre las redes virtuales de origen y de destino y viceversa.</span><span class="sxs-lookup"><span data-stu-id="613f4-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="613f4-128">**Cuentas de almacenamiento en caché**</span><span class="sxs-lookup"><span data-stu-id="613f4-128">**Cache storage accounts**</span></span> | <span data-ttu-id="613f4-129">Antes de que los cambios en las máquinas virtuales de origen se repliquen en la cuenta de almacenamiento de destino, se realiza un seguimiento de ellos y se envían a la cuenta de almacenamiento en caché de la ubicación de destino.</span><span class="sxs-lookup"><span data-stu-id="613f4-129">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="613f4-130">De esta forma las aplicaciones de producción que se ejecutan en la máquina virtual resultan mínimamente afectadas.</span><span class="sxs-lookup"><span data-stu-id="613f4-130">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="613f4-131">**Cuentas de almacenamiento de destino**</span><span class="sxs-lookup"><span data-stu-id="613f4-131">**Target storage accounts**</span></span>  | <span data-ttu-id="613f4-132">Las cuentas de almacenamiento de la ubicación de destino en la que se replican los datos.</span><span class="sxs-lookup"><span data-stu-id="613f4-132">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="613f4-133">**Conjuntos de disponibilidad de destino**</span><span class="sxs-lookup"><span data-stu-id="613f4-133">**Target availability sets**</span></span>  | <span data-ttu-id="613f4-134">Los conjuntos de disponibilidad en los que se encuentran las máquinas virtuales replicadas tras la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="613f4-134">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="613f4-135">Paso 2</span><span class="sxs-lookup"><span data-stu-id="613f4-135">Step 2</span></span>

<span data-ttu-id="613f4-136">Cuando la replicación está habilitada, la extensión Mobility Service de Site Recovery se instala automáticamente en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="613f4-136">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="613f4-137">Ocurre lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="613f4-137">The following occurs:</span></span>

1. <span data-ttu-id="613f4-138">La máquina virtual está registrada en Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="613f4-138">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="613f4-139">La replicación continua está configurada en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="613f4-139">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="613f4-140">Las escrituras de datos en los discos de máquina virtual se transfieren continuamente a la cuenta de almacenamiento en caché de la ubicación de origen.</span><span class="sxs-lookup"><span data-stu-id="613f4-140">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![Habilitación del proceso de replicación, paso 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="613f4-142">Tenga en cuenta que Site Recovery no necesita conectividad de entrada a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="613f4-142">Note that Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="613f4-143">Solo se necesita conectividad de salida a las direcciones URL e IP del servicio de Site Recovery, a las direcciones URL o IP de autenticación de Office 365 y a las direcciones IP de la cuenta de almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="613f4-143">Only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="613f4-144">Proceso de replicación continua</span><span class="sxs-lookup"><span data-stu-id="613f4-144">Continuous replication process</span></span>

<span data-ttu-id="613f4-145">Una vez que la replicación continua está funcionando, las escrituras en disco se transfieren inmediatamente a la cuenta de almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="613f4-145">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="613f4-146">Site Recovery procesa los datos y los envía a la cuenta de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="613f4-146">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="613f4-147">Una vez procesados los datos, cada pocos minutos se generan los puntos de recuperación en la cuenta de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="613f4-147">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="613f4-148">Proceso de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="613f4-148">Failover process</span></span>

<span data-ttu-id="613f4-149">Cuando se inicia una conmutación por error, las máquinas virtuales se crean en el grupo de recursos de destino, la red virtual de destino, la subred de destino y el conjunto de disponibilidad de destino.</span><span class="sxs-lookup"><span data-stu-id="613f4-149">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="613f4-150">Durante una conmutación por error, puede usar cualquier punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="613f4-150">During a failover, you can use any recovery point.</span></span>

![Proceso de conmutación por error](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="613f4-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="613f4-152">Next steps</span></span>

<span data-ttu-id="613f4-153">Vaya a [Paso 2: Comprobación de los requisitos previos y las limitaciones](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="613f4-153">Go to [Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
