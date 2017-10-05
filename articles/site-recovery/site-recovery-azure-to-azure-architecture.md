---
title: "¿Cómo funciona la replicación de máquinas virtuales de Azure entre regiones de Azure en Azure Site Recovery?  | Microsoft Docs"
description: "En este artículo se proporciona una visión general de los componentes y la arquitectura usados al replicar máquinas virtuales de Azure entre regiones de Azure mediante el servicio de Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: ec397eaeda963f257d1bd996f1f57189bcde17ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="cd47b-104">¿Cómo funciona la replicación de máquinas virtuales de Azure en Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="cd47b-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="cd47b-105">En este artículo se describen los componentes y los procesos implicados en la replicación y la recuperación de máquinas virtuales (VM) de Azure de una región a otra mediante el servicio de [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd47b-105">This article describes the components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region to another by using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="cd47b-106">La replicación de máquinas virtuales de Azure con el servicio de Site Recovery está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="cd47b-106">Azure VM replication with the Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="cd47b-107">Publique cualquier comentario en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cd47b-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="cd47b-108">Componentes de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="cd47b-108">Architectural components</span></span>

<span data-ttu-id="cd47b-109">En el siguiente diagrama se proporciona una visión de alto nivel de un entorno de máquina virtual de Azure en una región específica (en este ejemplo, la ubicación Este de EE. UU.).</span><span class="sxs-lookup"><span data-stu-id="cd47b-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="cd47b-110">En un entorno de máquina virtual de Azure:</span><span class="sxs-lookup"><span data-stu-id="cd47b-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="cd47b-111">Las aplicaciones pueden ejecutarse en máquinas virtuales con discos repartidos entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cd47b-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="cd47b-112">Las máquinas virtuales pueden incluirse en una o más subredes dentro de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="cd47b-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![Entorno de cliente](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="cd47b-114">Aprenda sobre los requisitos previos de implementación y los requisitos de la [matriz de compatibilidad](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cd47b-114">Learn about the deployment prerequisites and requirements in the [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="cd47b-115">Proceso de replicación</span><span class="sxs-lookup"><span data-stu-id="cd47b-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="cd47b-116">Paso 1</span><span class="sxs-lookup"><span data-stu-id="cd47b-116">Step 1</span></span>

<span data-ttu-id="cd47b-117">Cuando se habilita la replicación de máquinas virtuales de Azure en Azure Portal, se crean automáticamente en la región de destino los recursos que se muestran en el siguiente diagrama y tabla.</span><span class="sxs-lookup"><span data-stu-id="cd47b-117">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="cd47b-118">De forma predeterminada, los recursos se crean en función de la configuración de la región de origen.</span><span class="sxs-lookup"><span data-stu-id="cd47b-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="cd47b-119">Puede personalizar la configuración de destino según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cd47b-119">You can customize the target settings as required.</span></span> <span data-ttu-id="cd47b-120">[Más información](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cd47b-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Habilitación del proceso de replicación, paso 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="cd47b-122">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="cd47b-122">**Resource**</span></span> | <span data-ttu-id="cd47b-123">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="cd47b-123">**Details**</span></span>
--- | ---
<span data-ttu-id="cd47b-124">**Grupo de recursos de destino**</span><span class="sxs-lookup"><span data-stu-id="cd47b-124">**Target resource group**</span></span> | <span data-ttu-id="cd47b-125">El grupo de recursos a los que pertenecen las máquinas virtuales replicadas después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="cd47b-125">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="cd47b-126">**Red virtual de destino**</span><span class="sxs-lookup"><span data-stu-id="cd47b-126">**Target virtual network**</span></span> | <span data-ttu-id="cd47b-127">La red virtual en el que se encuentran las máquinas virtuales replicadas después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="cd47b-127">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="cd47b-128">Se crea una asignación de red entre las redes virtuales de origen y de destino y viceversa.</span><span class="sxs-lookup"><span data-stu-id="cd47b-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="cd47b-129">**Cuentas de almacenamiento en caché**</span><span class="sxs-lookup"><span data-stu-id="cd47b-129">**Cache storage accounts**</span></span> | <span data-ttu-id="cd47b-130">Antes de que los cambios en las máquinas virtuales de origen se repliquen en la cuenta de almacenamiento de destino, se realiza un seguimiento de ellos y se envían a la cuenta de almacenamiento en caché de la ubicación de destino.</span><span class="sxs-lookup"><span data-stu-id="cd47b-130">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="cd47b-131">De esta forma las aplicaciones de producción que se ejecutan en la máquina virtual resultan mínimamente afectadas.</span><span class="sxs-lookup"><span data-stu-id="cd47b-131">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="cd47b-132">**Cuentas de almacenamiento de destino**</span><span class="sxs-lookup"><span data-stu-id="cd47b-132">**Target storage accounts**</span></span>  | <span data-ttu-id="cd47b-133">Las cuentas de almacenamiento de la ubicación de destino en la que se replican los datos.</span><span class="sxs-lookup"><span data-stu-id="cd47b-133">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="cd47b-134">**Conjuntos de disponibilidad de destino**</span><span class="sxs-lookup"><span data-stu-id="cd47b-134">**Target availability sets**</span></span>  | <span data-ttu-id="cd47b-135">Los conjuntos de disponibilidad en los que se encuentran las máquinas virtuales replicadas tras la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="cd47b-135">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="cd47b-136">Paso 2</span><span class="sxs-lookup"><span data-stu-id="cd47b-136">Step 2</span></span>

<span data-ttu-id="cd47b-137">Cuando la replicación está habilitada, la extensión Mobility Service de Site Recovery se instala automáticamente en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cd47b-137">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="cd47b-138">Ocurre lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cd47b-138">The following occurs:</span></span>

1. <span data-ttu-id="cd47b-139">La máquina virtual está registrada en Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cd47b-139">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="cd47b-140">La replicación continua está configurada en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cd47b-140">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="cd47b-141">Las escrituras de datos en los discos de máquina virtual se transfieren continuamente a la cuenta de almacenamiento en caché de la ubicación de origen.</span><span class="sxs-lookup"><span data-stu-id="cd47b-141">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![Habilitación del proceso de replicación, paso 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="cd47b-143">Site Recovery no necesita nunca conectividad de entrada a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cd47b-143">Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="cd47b-144">La máquina virtual solo necesita conectividad de salida a las direcciones URL e IP del servicio de Site Recovery, a las direcciones URL o IP de autenticación de Office 365 y a las direcciones IP de la cuenta de almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="cd47b-144">The VM needs only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="cd47b-145">Para más información, consulte el artículo [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) (Instrucciones de redes para la replicación de máquinas virtuales de Azure).</span><span class="sxs-lookup"><span data-stu-id="cd47b-145">For more information, see the [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="cd47b-146">Proceso de replicación continua</span><span class="sxs-lookup"><span data-stu-id="cd47b-146">Continuous replication process</span></span>

<span data-ttu-id="cd47b-147">Una vez que la replicación continua está funcionando, las escrituras en disco se transfieren inmediatamente a la cuenta de almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="cd47b-147">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="cd47b-148">Site Recovery procesa los datos y los envía a la cuenta de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="cd47b-148">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="cd47b-149">Una vez procesados los datos, cada pocos minutos se generan los puntos de recuperación en la cuenta de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="cd47b-149">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="cd47b-150">Proceso de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="cd47b-150">Failover process</span></span>

<span data-ttu-id="cd47b-151">Cuando se inicia una conmutación por error, las máquinas virtuales se crean en el grupo de recursos de destino, la red virtual de destino, la subred de destino y el conjunto de disponibilidad de destino.</span><span class="sxs-lookup"><span data-stu-id="cd47b-151">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="cd47b-152">Durante una conmutación por error, puede usar cualquier punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="cd47b-152">During a failover, you can use any recovery point.</span></span>

![Proceso de conmutación por error](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="cd47b-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd47b-154">Next steps</span></span>

- <span data-ttu-id="cd47b-155">Aprenda sobre las [redes](site-recovery-azure-to-azure-networking-guidance.md) para la replicación de máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd47b-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="cd47b-156">Siga un tutorial para [replicar máquinas virtuales de Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="cd47b-156">Follow a walkthrough to [replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
