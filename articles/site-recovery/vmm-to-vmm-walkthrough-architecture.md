---
title: "Revisión de la arquitectura para la replicación de Hyper-V a un sitio secundario con Azure Site Recovery | Microsoft Docs"
description: "Este artículo proporciona información general de la arquitectura usada para replicar máquinas virtuales de Hyper-V locales a un sistema sitio System Center VMM secundario con Azure Site Recovery."
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
ms.openlocfilehash: b78cd0d5a5395873afaddc8856004775f447e8ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="step-1-review-the-architecture-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="35e35-103">Paso 1: Revisión de la arquitectura para la replicación de Hyper-V a un sitio secundario</span><span class="sxs-lookup"><span data-stu-id="35e35-103">Step 1: Review the architecture for Hyper-V replication to a secondary site</span></span>

<span data-ttu-id="35e35-104">En este artículo se describen los componentes y procesos que tienen lugar al replicar máquinas virtuales de Hyper-V locales en nubes de System Center Virtual Machine Manager (VMM) a un sitio VMM secundario utilizando el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="35e35-104">This article describes the components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM site using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="35e35-105">Publique cualquier comentario que tenga en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="35e35-105">Post any comments at the bottom of this article, or in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="35e35-106">Componentes de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="35e35-106">Architectural components</span></span>

<span data-ttu-id="35e35-107">Esto es lo que necesita para la replicación de máquinas virtuales Hyper-V en un sitio secundario VMM.</span><span class="sxs-lookup"><span data-stu-id="35e35-107">Here's what you need for replicating Hyper-V VMs to a secondary VMM site.</span></span>

<span data-ttu-id="35e35-108">**Componente**</span><span class="sxs-lookup"><span data-stu-id="35e35-108">**Component**</span></span> | <span data-ttu-id="35e35-109">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="35e35-109">**Location**</span></span> | <span data-ttu-id="35e35-110">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="35e35-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="35e35-111">**Las tablas de Azure**</span><span class="sxs-lookup"><span data-stu-id="35e35-111">**Azure**</span></span> | <span data-ttu-id="35e35-112">Suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="35e35-112">Subscription in Azure.</span></span> | <span data-ttu-id="35e35-113">Cree un almacén de Recovery Services en la suscripción de Azure, para orquestar y administrar la replicación entre ubicaciones de VMM.</span><span class="sxs-lookup"><span data-stu-id="35e35-113">You create a Recovery Services vault in the Azure subscription, to orchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="35e35-114">**Servidor VMM**</span><span class="sxs-lookup"><span data-stu-id="35e35-114">**VMM server**</span></span> | <span data-ttu-id="35e35-115">Necesita una ubicación principal de VMM y otra secundaria.</span><span class="sxs-lookup"><span data-stu-id="35e35-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="35e35-116">Se recomienda un servidor VMM en el sitio principal y otro en el sitio secundario.</span><span class="sxs-lookup"><span data-stu-id="35e35-116">We recommend a VMM server in the primary site, and one in the secondary site</span></span> 
<span data-ttu-id="35e35-117">**Servidor de Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="35e35-117">**Hyper-V server**</span></span> |  <span data-ttu-id="35e35-118">Uno o varios servidores host de Hyper-V en las nubes VMM principal y secundaria.</span><span class="sxs-lookup"><span data-stu-id="35e35-118">One or more Hyper-V host servers in the primary and secondary VMM clouds.</span></span> | <span data-ttu-id="35e35-119">Los datos se replican entre los servidores host de Hyper-V principales y secundarios a través de la LAN o VPN mediante autenticación Kerberos o de certificado.</span><span class="sxs-lookup"><span data-stu-id="35e35-119">Data is replicated between the primary and secondary Hyper-V host servers over the LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="35e35-120">**Máquinas virtuales de Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="35e35-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="35e35-121">En el servidor de host de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="35e35-121">On Hyper-V host server.</span></span> | <span data-ttu-id="35e35-122">El servidor host de origen debe tener, como mínimo, una máquina virtual que se desee replicar.</span><span class="sxs-lookup"><span data-stu-id="35e35-122">The source host server should have at least one VM that you want to replicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="35e35-123">Proceso de replicación</span><span class="sxs-lookup"><span data-stu-id="35e35-123">Replication process</span></span>

1. <span data-ttu-id="35e35-124">Configure la cuenta de Azure, cree un almacén de Recovery Services y especifique lo que desea replicar.</span><span class="sxs-lookup"><span data-stu-id="35e35-124">You set up the Azure account, create a Recovery Services vault, and specify what you want to replicate.</span></span>
2. <span data-ttu-id="35e35-125">Configure los ajustes de replicación del origen y el destino, que incluye la instalación del proveedor de Azure Site Recovery en servidores VMM y del agente de Microsoft Azure Recovery Services en cada host de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="35e35-125">You configure the source and target replication settings, which includes installing the Azure Site Recovery Provider on VMM servers, and the Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="35e35-126">Cree una directiva de replicación para la nube de VMM de origen.</span><span class="sxs-lookup"><span data-stu-id="35e35-126">You create a replication policy for the source VMM cloud.</span></span> <span data-ttu-id="35e35-127">La directiva se aplica a todas las máquinas virtuales ubicadas en los hosts de la nube.</span><span class="sxs-lookup"><span data-stu-id="35e35-127">The policy is applied to all VMs located on hosts in the cloud.</span></span>
4. <span data-ttu-id="35e35-128">Habilite la replicación para cada VMM y se produce la replicación inicial de una máquina virtual de acuerdo a los ajustes que haya elegido.</span><span class="sxs-lookup"><span data-stu-id="35e35-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with the settings you choose.</span></span>
5. <span data-ttu-id="35e35-129">Después de la replicación inicial, empieza la de los cambios diferenciales.</span><span class="sxs-lookup"><span data-stu-id="35e35-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="35e35-130">Las marcas de revisión de un elemento se conservan en un archivo .hrl.</span><span class="sxs-lookup"><span data-stu-id="35e35-130">Tracked changes for an item are held in a .hrl file.</span></span>


![De local a local](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="35e35-132">Proceso de conmutación por error y conmutación por recuperación</span><span class="sxs-lookup"><span data-stu-id="35e35-132">Failover and failback process</span></span>

1. <span data-ttu-id="35e35-133">Puede ejecutar una [conmutación por error](site-recovery-failover.md), planeada o no, entre sitios locales.</span><span class="sxs-lookup"><span data-stu-id="35e35-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="35e35-134">Si ejecuta una conmutación por error planeada, las máquinas virtuales de origen se apagan para garantizar que no se pierdan datos.</span><span class="sxs-lookup"><span data-stu-id="35e35-134">If you run a planned failover, then source VMs are shut down to ensure no data loss.</span></span>
2. <span data-ttu-id="35e35-135">Puede conmutar por error una única máquina o crear [planes de recuperación](site-recovery-create-recovery-plans.md) para organizar la conmutación por error de varias máquinas.</span><span class="sxs-lookup"><span data-stu-id="35e35-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="35e35-136">Si realiza una conmutación por error no planeada en un sitio secundario, tras ella las máquinas de la ubicación secundaria no están habilitadas para su protección ni replicación.</span><span class="sxs-lookup"><span data-stu-id="35e35-136">If you perform an unplanned failover to a secondary site, after the failover machines in the secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="35e35-137">Si ejecutó una conmutación por error planeada, tras ella las máquinas de la ubicación secundaria están protegidas.</span><span class="sxs-lookup"><span data-stu-id="35e35-137">If you ran a planned failover, after the failover, machines in the secondary location are protected.</span></span>
5. <span data-ttu-id="35e35-138">Después, ejecute una conmutación por error para iniciar el acceso a la carga de trabajo desde la máquina virtual de la réplica.</span><span class="sxs-lookup"><span data-stu-id="35e35-138">Then, you commit the failover to start accessing the workload from the replica VM.</span></span>
6. <span data-ttu-id="35e35-139">Cuando el sitio principal esté disponible de nuevo, inicie la replicación inversa para replicar desde el sitio secundario al principal.</span><span class="sxs-lookup"><span data-stu-id="35e35-139">When your primary site is available again, you initiate reverse replication to replicate from the secondary site to the primary.</span></span> <span data-ttu-id="35e35-140">La replicación inversa pone las máquinas virtuales en un estado protegido pero el centro de datos secundario sigue siendo la ubicación activa.</span><span class="sxs-lookup"><span data-stu-id="35e35-140">Reverse replication brings the virtual machines into a protected state, but the secondary datacenter is still the active location.</span></span>
7. <span data-ttu-id="35e35-141">Para que el sitio principal se convierta de nuevo en la ubicación activa, debe iniciar una conmutación por error planeada desde el secundario al principal, seguida de otra replicación inversa.</span><span class="sxs-lookup"><span data-stu-id="35e35-141">To make the primary site into the active location again, you initiate a planned failover from secondary to primary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="35e35-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35e35-142">Next steps</span></span>

<span data-ttu-id="35e35-143">Ir a [Paso 2: Revisión de los requisitos previos y las limitaciones](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="35e35-143">Go to [Step 2: Review the prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
