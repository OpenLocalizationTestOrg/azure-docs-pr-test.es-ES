---
title: "¿aaaHow realiza la replicación de máquina virtual de Azure entre el trabajo de regiones de Azure en Azure Site Recovery?  | Microsoft Docs"
description: "Este artículo proporciona información general de componentes y arquitectura que se usa al replicar máquinas virtuales de Azure entre regiones de Azure mediante el servicio de Azure Site Recovery Hola."
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
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="61c23-104">¿Cómo funciona la replicación de máquinas virtuales de Azure en Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="61c23-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="61c23-105">Este artículo describen los componentes de Hola y procesos implicados en la replicación y recuperación de máquinas virtuales de Azure (VM) desde una región tooanother mediante el uso de hello [Azure Site Recovery](site-recovery-overview.md) servicio.</span><span class="sxs-lookup"><span data-stu-id="61c23-105">This article describes hello components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region tooanother by using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="61c23-106">Replicación de máquina virtual de Azure con hello servicio Site Recovery está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="61c23-106">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="61c23-107">Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="61c23-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="61c23-108">Componentes de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="61c23-108">Architectural components</span></span>

<span data-ttu-id="61c23-109">Hola siguiente diagrama proporciona una visión general de un entorno de máquina virtual de Azure en una región específica (en este ejemplo, hello ubicación UU).</span><span class="sxs-lookup"><span data-stu-id="61c23-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="61c23-110">En un entorno de máquina virtual de Azure:</span><span class="sxs-lookup"><span data-stu-id="61c23-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="61c23-111">Las aplicaciones pueden ejecutarse en máquinas virtuales con discos repartidos entre cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="61c23-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="61c23-112">Hola máquinas virtuales puede incluirse en una o más subredes dentro de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="61c23-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![Entorno de cliente](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="61c23-114">Obtenga información acerca de los requisitos previos de implementación de Hola y los requisitos en hello [matriz de compatibilidad](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="61c23-114">Learn about hello deployment prerequisites and requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="61c23-115">Proceso de replicación</span><span class="sxs-lookup"><span data-stu-id="61c23-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="61c23-116">Paso 1</span><span class="sxs-lookup"><span data-stu-id="61c23-116">Step 1</span></span>

<span data-ttu-id="61c23-117">Cuando se habilita la replicación de máquina virtual de Azure en hello portal de Azure, Hola recursos que se muestran en hello después de diagrama y la tabla se crean automáticamente en la región de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="61c23-117">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="61c23-118">De forma predeterminada, los recursos se crean en función de la configuración de la región de origen.</span><span class="sxs-lookup"><span data-stu-id="61c23-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="61c23-119">Puede personalizar la configuración de destino de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="61c23-119">You can customize hello target settings as required.</span></span> <span data-ttu-id="61c23-120">[Más información](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="61c23-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Habilitación del proceso de replicación, paso 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="61c23-122">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="61c23-122">**Resource**</span></span> | <span data-ttu-id="61c23-123">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="61c23-123">**Details**</span></span>
--- | ---
<span data-ttu-id="61c23-124">**Grupo de recursos de destino**</span><span class="sxs-lookup"><span data-stu-id="61c23-124">**Target resource group**</span></span> | <span data-ttu-id="61c23-125">Hola toowhich de grupo de recursos pertenecen máquinas virtuales replicadas después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="61c23-125">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="61c23-126">**Red virtual de destino**</span><span class="sxs-lookup"><span data-stu-id="61c23-126">**Target virtual network**</span></span> | <span data-ttu-id="61c23-127">red virtual de Hello en el que se encuentran máquinas virtuales replicadas después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="61c23-127">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="61c23-128">Se crea una asignación de red entre las redes virtuales de origen y de destino y viceversa.</span><span class="sxs-lookup"><span data-stu-id="61c23-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="61c23-129">**Cuentas de almacenamiento en caché**</span><span class="sxs-lookup"><span data-stu-id="61c23-129">**Cache storage accounts**</span></span> | <span data-ttu-id="61c23-130">Antes de que los cambios en el origen de que las máquinas virtuales repliquen toohello cuenta de almacenamiento de destino, se realiza un seguimiento y envían toohello cuenta de almacenamiento de caché en la ubicación de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="61c23-130">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="61c23-131">Esto garantiza un impacto mínimo en aplicaciones de producción que se ejecutan en VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="61c23-131">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="61c23-132">**Cuentas de almacenamiento de destino**</span><span class="sxs-lookup"><span data-stu-id="61c23-132">**Target storage accounts**</span></span>  | <span data-ttu-id="61c23-133">Cuentas de almacenamiento de datos de hello destino ubicación toowhich Hola se replica.</span><span class="sxs-lookup"><span data-stu-id="61c23-133">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="61c23-134">**Conjuntos de disponibilidad de destino**</span><span class="sxs-lookup"><span data-stu-id="61c23-134">**Target availability sets**</span></span>  | <span data-ttu-id="61c23-135">Conjuntos de disponibilidad de qué Hola replicar las máquinas virtuales se encuentran después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="61c23-135">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="61c23-136">Paso 2</span><span class="sxs-lookup"><span data-stu-id="61c23-136">Step 2</span></span>

<span data-ttu-id="61c23-137">Como la replicación está habilitada, Hola extensión servicio de movilidad de Site Recovery se instala automáticamente en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61c23-137">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="61c23-138">se produce el siguiente Hello:</span><span class="sxs-lookup"><span data-stu-id="61c23-138">hello following occurs:</span></span>

1. <span data-ttu-id="61c23-139">Hola VM está registrado con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="61c23-139">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="61c23-140">La replicación continua está configurada para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61c23-140">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="61c23-141">Escrituras de datos en hello VM discos estén continuamente transfieren toohello cuenta de almacenamiento de caché en la ubicación de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="61c23-141">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Habilitación del proceso de replicación, paso 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="61c23-143">Recuperación del sitio nunca necesita conectividad entrante toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61c23-143">Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="61c23-144">Hola VM debe solo direcciones de TCP/IP direcciones URL del servicio de recuperación de tooSite de conectividad saliente, Office 365 autenticación direcciones URL y direcciones IP y direcciones IP de cuenta de almacenamiento de caché.</span><span class="sxs-lookup"><span data-stu-id="61c23-144">hello VM needs only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="61c23-145">Para obtener más información, vea hello [Guía de red para la replicación de máquinas virtuales de Azure](site-recovery-azure-to-azure-networking-guidance.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="61c23-145">For more information, see hello [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="61c23-146">Proceso de replicación continua</span><span class="sxs-lookup"><span data-stu-id="61c23-146">Continuous replication process</span></span>

<span data-ttu-id="61c23-147">Después de que funciona la replicación continua, disco escribe inmediatamente transfiere toohello cuenta de almacenamiento de caché.</span><span class="sxs-lookup"><span data-stu-id="61c23-147">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="61c23-148">Recuperación de sitio procesa los datos de Hola y envía toohello cuenta de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="61c23-148">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="61c23-149">Después de que se procesan los datos de hello, puntos de recuperación se generan en la cuenta de almacenamiento de destino de hello cada pocos minutos.</span><span class="sxs-lookup"><span data-stu-id="61c23-149">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="61c23-150">Proceso de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="61c23-150">Failover process</span></span>

<span data-ttu-id="61c23-151">Cuando se inicia una conmutación por error, hello y hello que las máquinas virtuales se crean en el grupo de recursos de destino de hello, la red virtual de destino, la subred de destino conjunto de disponibilidad de destino.</span><span class="sxs-lookup"><span data-stu-id="61c23-151">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="61c23-152">Durante una conmutación por error, puede usar cualquier punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="61c23-152">During a failover, you can use any recovery point.</span></span>

![Proceso de conmutación por error](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="61c23-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61c23-154">Next steps</span></span>

- <span data-ttu-id="61c23-155">Aprenda sobre las [redes](site-recovery-azure-to-azure-networking-guidance.md) para la replicación de máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="61c23-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="61c23-156">Siga un tutorial demasiado[replicar máquinas virtuales de Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="61c23-156">Follow a walkthrough too[replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
