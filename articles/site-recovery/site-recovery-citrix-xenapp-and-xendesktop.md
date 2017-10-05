---
title: "Replicar una implementación de XenDesktop y XenApp de Citrix de niveles múltiples mediante Azure Site Recovery | Microsoft Docs"
description: "En este artículo se describe cómo proteger y recuperar implementaciones de XenDesktop y XenApp de Citrix con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: dc064352b1841ff346b705dc63186b12d79350b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="902a6-103">Replicar una implementación de XenApp y XenDesktop de Citrix de niveles múltiples mediante Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="902a6-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="902a6-104">Información general</span><span class="sxs-lookup"><span data-stu-id="902a6-104">Overview</span></span>

<span data-ttu-id="902a6-105">XenDesktop de Citrix es una solución de virtualización de escritorio que ofrece aplicaciones y escritorios como servicio a petición a cualquier usuario y en cualquier lugar.</span><span class="sxs-lookup"><span data-stu-id="902a6-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service to any user, anywhere.</span></span> <span data-ttu-id="902a6-106">Gracias a la tecnología de entrega FlexCast, XenDesktop puede entregar de forma rápida y segura aplicaciones y escritorios a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="902a6-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops to users.</span></span>
<span data-ttu-id="902a6-107">Actualmente, XenApp de Citrix no proporciona funciones de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="902a6-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="902a6-108">Una buena solución de recuperación ante desastres debería permitir que se pudieran desarrollar planes de recuperación para este tipo de arquitecturas de aplicaciones complejas que se describieron anteriormente. También deberían brindar la posibilidad de agregar pasos personalizados para administrar las asignaciones de la aplicación entre diferentes niveles, así como proporcionar una solución confiable de un solo clic en caso de que un desastre produjera un descenso del RTO.</span><span class="sxs-lookup"><span data-stu-id="902a6-108">A good disaster recovery solution, should allow modeling of recovery plans around the above complex application architectures and also have the ability to add customized steps to handle application mappings between various tiers hence providing a single-click sure shot solution in the event of a disaster leading to a lower RTO.</span></span>

<span data-ttu-id="902a6-109">Este documento proporciona instrucciones detalladas para crear una solución de recuperación ante desastres para las implementaciones locales de XenApp de Citrix en plataformas vSphere de Hyper-V y VMware.</span><span class="sxs-lookup"><span data-stu-id="902a6-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="902a6-110">Además, se describe cómo realizar una conmutación por error de prueba (obtención de detalles de recuperación ante desastres) y una conmutación por error no planeada en Azure con los planes de recuperación, las configuraciones admitidas y los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="902a6-110">This document also describes how to perform a test failover(disaster recovery drill) and unplanned failover to Azure using recovery plans, the supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="902a6-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="902a6-111">Prerequisites</span></span>

<span data-ttu-id="902a6-112">Antes de empezar, no olvide informarse sobre las cuestione siguientes:</span><span class="sxs-lookup"><span data-stu-id="902a6-112">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="902a6-113">Replicación de una máquina virtual en Azure</span><span class="sxs-lookup"><span data-stu-id="902a6-113">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="902a6-114">[Diseño de una red de recuperación](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="902a6-114">How to [design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="902a6-115">Realización de una conmutación por error de prueba en Azure</span><span class="sxs-lookup"><span data-stu-id="902a6-115">Doing a test failover to Azure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="902a6-116">Ejecución de una conmutación por error en Azure</span><span class="sxs-lookup"><span data-stu-id="902a6-116">Doing a failover to Azure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="902a6-117">[Replicación de un controlador de dominio](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="902a6-117">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="902a6-118">[Replicación de SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="902a6-118">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="902a6-119">Modelos de implementación</span><span class="sxs-lookup"><span data-stu-id="902a6-119">Deployment patterns</span></span>

<span data-ttu-id="902a6-120">Una granja de XenApp y XenDesktop de Citrix suele tener el siguiente patrón de implementación:</span><span class="sxs-lookup"><span data-stu-id="902a6-120">A Citrix XenApp and XenDesktop farm typically has the following deployment pattern:</span></span>

<span data-ttu-id="902a6-121">**Patrón de implementación**</span><span class="sxs-lookup"><span data-stu-id="902a6-121">**Deployment pattern**</span></span>

<span data-ttu-id="902a6-122">Implementación de XenApp y XenDesktop de Citrix con servidor DNS de AD, servidor de SQL Database, controlador de entrega de Citrix, servidor de StoreFront, XenApp Master (VDA) y servidor de licencias de XenApp de Citrix</span><span class="sxs-lookup"><span data-stu-id="902a6-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Modelo de implementación 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="902a6-124">Compatibilidad de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="902a6-124">Site Recovery support</span></span>

<span data-ttu-id="902a6-125">Para este artículo, se han usado implementaciones de Citrix en máquinas virtuales de VMware administradas por vSphere 6.0 / System Center VMM 2012 R2 para la configuración de la recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="902a6-125">For the purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used to setup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="902a6-126">Origen y destino</span><span class="sxs-lookup"><span data-stu-id="902a6-126">Source and target</span></span>

<span data-ttu-id="902a6-127">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="902a6-127">**Scenario**</span></span> | <span data-ttu-id="902a6-128">**En un sitio secundario**</span><span class="sxs-lookup"><span data-stu-id="902a6-128">**To a secondary site**</span></span> | <span data-ttu-id="902a6-129">**En Azure**</span><span class="sxs-lookup"><span data-stu-id="902a6-129">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="902a6-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="902a6-130">**Hyper-V**</span></span> | <span data-ttu-id="902a6-131">Fuera del ámbito</span><span class="sxs-lookup"><span data-stu-id="902a6-131">Not in scope</span></span> | <span data-ttu-id="902a6-132">Sí</span><span class="sxs-lookup"><span data-stu-id="902a6-132">Yes</span></span>
<span data-ttu-id="902a6-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="902a6-133">**VMware**</span></span> | <span data-ttu-id="902a6-134">Fuera del ámbito</span><span class="sxs-lookup"><span data-stu-id="902a6-134">Not in scope</span></span> | <span data-ttu-id="902a6-135">Sí</span><span class="sxs-lookup"><span data-stu-id="902a6-135">Yes</span></span>
<span data-ttu-id="902a6-136">**Servidor físico**</span><span class="sxs-lookup"><span data-stu-id="902a6-136">**Physical server**</span></span> | <span data-ttu-id="902a6-137">Fuera del ámbito</span><span class="sxs-lookup"><span data-stu-id="902a6-137">Not in scope</span></span> | <span data-ttu-id="902a6-138">Sí</span><span class="sxs-lookup"><span data-stu-id="902a6-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="902a6-139">Versiones</span><span class="sxs-lookup"><span data-stu-id="902a6-139">Versions</span></span>
<span data-ttu-id="902a6-140">Los clientes pueden implementar componentes de XenApp como máquinas virtuales que se ejecutan en Hyper-V o VMware o como servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="902a6-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="902a6-141">Azure Site Recovery puede proteger las implementaciones físicas y virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-141">Azure Site Recovery can protect both physical and virtual deployments to Azure.</span></span>
<span data-ttu-id="902a6-142">Dado que en Azure se admite XenApp 7.7 o una versión posterior, solo se pueden conmutar por error a Azure las implementaciones con estas versiones para la migración o la recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="902a6-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over to Azure for Disaster Recovery or migration.</span></span>

### <a name="things-to-keep-in-mind"></a><span data-ttu-id="902a6-143">Aspectos que debe tener en cuenta</span><span class="sxs-lookup"><span data-stu-id="902a6-143">Things to keep in mind</span></span>

1. <span data-ttu-id="902a6-144">No se admite la protección y la recuperación de implementaciones locales mediante equipos con sistema operativo de servidor para entregar aplicaciones y escritorios de XenApp publicados.</span><span class="sxs-lookup"><span data-stu-id="902a6-144">Protection and recovery of on-premises deployments using Server OS machines to deliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="902a6-145">No se admite la protección y la recuperación de implementaciones locales mediante equipos con sistema operativo de escritorio para entregar VDI para escritorios virtuales de cliente, incluido Windows 10.</span><span class="sxs-lookup"><span data-stu-id="902a6-145">Protection and recovery of on-premises deployments using desktop OS machines to deliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="902a6-146">Esto se debe a que ASR no admite la recuperación de equipos con sistemas operativos de escritorio.</span><span class="sxs-lookup"><span data-stu-id="902a6-146">This is because ASR does not support the recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="902a6-147">Además, todavía no se admiten algunos tipos de escritorio virtual de cliente (por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="902a6-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="902a6-148">Windows 7) para la concesión de licencias en Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="902a6-149">Aquí encontrará [más información](https://azure.microsoft.com/pricing/licensing-faq/) acerca de la concesión de licencias a escritorios de cliente/servidor de Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="902a6-150">Azure Site Recovery no puede replicar y proteger clones locales de MCS o PVS existentes.</span><span class="sxs-lookup"><span data-stu-id="902a6-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="902a6-151">Debe volver a crear estos clones mediante el aprovisionamiento de Azure RM desde el controlador de entrega.</span><span class="sxs-lookup"><span data-stu-id="902a6-151">You need to recreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="902a6-152">No se puede proteger NetScaler con Azure Site Recovery, ya que NetScaler se basa en FreeBSD y Azure Site Recovery no admite la protección del sistema operativo de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="902a6-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="902a6-153">Debe implementar y configurar una nueva aplicación NetScaler desde Azure Marketplace después de la conmutación por error a Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-153">You would need to deploy and configure a new NetScaler appliance from Azure Market place after failover to Azure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="902a6-154">Replicación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="902a6-154">Replicating virtual machines</span></span>

<span data-ttu-id="902a6-155">Es necesario proteger los siguientes componentes de la implementación de XenApp de Citrix para habilitar la replicación y la recuperación.</span><span class="sxs-lookup"><span data-stu-id="902a6-155">The following components of the Citrix XenApp deployment need to be protected to enable replication and recovery.</span></span>

* <span data-ttu-id="902a6-156">Protección del servidor DNS de AD</span><span class="sxs-lookup"><span data-stu-id="902a6-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="902a6-157">Protección del servidor de SQL Database</span><span class="sxs-lookup"><span data-stu-id="902a6-157">Protection of SQL database server</span></span>
* <span data-ttu-id="902a6-158">Protección del controlador de entrega de Citrix</span><span class="sxs-lookup"><span data-stu-id="902a6-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="902a6-159">Protección del servidor de StoreFront</span><span class="sxs-lookup"><span data-stu-id="902a6-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="902a6-160">Protección de XenApp Master (VDA)</span><span class="sxs-lookup"><span data-stu-id="902a6-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="902a6-161">Protección del servidor de licencias de XenApp de Citrix</span><span class="sxs-lookup"><span data-stu-id="902a6-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="902a6-162">**Replicación del servidor DNS de AD**</span><span class="sxs-lookup"><span data-stu-id="902a6-162">**AD DNS server replication**</span></span>

<span data-ttu-id="902a6-163">Vea [Protección de Active Directory y DNS con Azure Site Recovery](site-recovery-active-directory.md) para obtener instrucciones sobre cómo replicar y configurar un controlador de dominio en Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-163">Please refer to [Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="902a6-164">**Replicación del servidor de SQL Database**</span><span class="sxs-lookup"><span data-stu-id="902a6-164">**SQL database Server replication**</span></span>

<span data-ttu-id="902a6-165">Vea [Proteger SQL Server con la recuperación ante desastres de SQL Server y Azure Site Recovery](site-recovery-sql.md) para obtener instrucciones técnicas detalladas sobre las opciones recomendadas para proteger servidores SQL Server.</span><span class="sxs-lookup"><span data-stu-id="902a6-165">Please refer to [Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on the recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="902a6-166">Siga [estas instrucciones](site-recovery-vmware-to-azure.md) para empezar a replicar en Azure las demás máquinas virtuales de los componentes.</span><span class="sxs-lookup"><span data-stu-id="902a6-166">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating the other component virtual machines to Azure.</span></span>

![Protección de componentes de XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="902a6-168">**Configuración de proceso y red**</span><span class="sxs-lookup"><span data-stu-id="902a6-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="902a6-169">Una vez que las máquinas estén protegidas (en Elementos replicados se muestra el estado "Protegido"), debe configurar los valores de Proceso y red.</span><span class="sxs-lookup"><span data-stu-id="902a6-169">After the machines are protected (status shows as “Protected” under Replicated Items), the Compute and Network settings need to be configured.</span></span>
<span data-ttu-id="902a6-170">En Proceso y red > Propiedades de Proceso, puede especificar el nombre y el tamaño de destino de la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-170">In Compute and Network > Compute properties, you can specify the Azure VM name and target size.</span></span>
<span data-ttu-id="902a6-171">Modifique el nombre para que cumpla con los requisitos de Azure si es necesario.</span><span class="sxs-lookup"><span data-stu-id="902a6-171">Modify the name to comply with Azure requirements if you need to.</span></span> <span data-ttu-id="902a6-172">También puede ver y agregar la información sobre la red, la subred y la dirección IP de destino que se asignarán a la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-172">You can also view and add information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span></span>

<span data-ttu-id="902a6-173">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="902a6-173">Note the following:</span></span>

* <span data-ttu-id="902a6-174">Puede establecer la dirección IP de destino.</span><span class="sxs-lookup"><span data-stu-id="902a6-174">You can set the target IP address.</span></span> <span data-ttu-id="902a6-175">Si no proporciona una dirección, la máquina conmutada por error usará DHCP.</span><span class="sxs-lookup"><span data-stu-id="902a6-175">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="902a6-176">Si establece una dirección que no está disponible en el momento de la conmutación por error, la conmutación no funcionará.</span><span class="sxs-lookup"><span data-stu-id="902a6-176">If you set an address that isn't available at failover, the failover won't work.</span></span> <span data-ttu-id="902a6-177">Se puede utilizar la misma dirección IP de destino para la conmutación por error de prueba si la dirección está disponible en la red.</span><span class="sxs-lookup"><span data-stu-id="902a6-177">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>

* <span data-ttu-id="902a6-178">En el caso del servidor AD/DNS, si conserva la dirección local, puede especificar la misma dirección del servidor DNS para Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="902a6-178">For the AD/DNS server, retaining the on-premises address lets you specify the same address as the DNS server for the Azure Virtual network.</span></span>

<span data-ttu-id="902a6-179">El número de adaptadores de red viene determinado por el tamaño que especifique para la máquina virtual de destino, de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="902a6-179">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>

*   <span data-ttu-id="902a6-180">Si el número de adaptadores de red en el equipo de origen es menor o igual al número de adaptadores permitido para el tamaño de la máquina de destino, el destino tendrá el mismo número de adaptadores que el origen.</span><span class="sxs-lookup"><span data-stu-id="902a6-180">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
*   <span data-ttu-id="902a6-181">Si el número de adaptadores para la máquina virtual de origen supera el número permitido para el tamaño de destino, entonces se utilizará el tamaño máximo de destino.</span><span class="sxs-lookup"><span data-stu-id="902a6-181">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
* <span data-ttu-id="902a6-182">Por ejemplo, si una máquina de origen tiene dos adaptadores de red y el tamaño de la máquina de destino admite cuatro, el equipo de destino tendrá dos adaptadores.</span><span class="sxs-lookup"><span data-stu-id="902a6-182">For example, if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="902a6-183">Si el equipo de origen tiene dos adaptadores pero el tamaño de destino compatible solo admite uno, el equipo de destino tendrá solo un adaptador.</span><span class="sxs-lookup"><span data-stu-id="902a6-183">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>
*   <span data-ttu-id="902a6-184">Si la máquina virtual tiene varios adaptadores de red, todos ellos se conectarán a la misma red.</span><span class="sxs-lookup"><span data-stu-id="902a6-184">If the virtual machine has multiple network adapters they will all connect to the same network.</span></span>
*   <span data-ttu-id="902a6-185">Si la máquina virtual tiene varios adaptadores de red, el primero que se muestre en la lista se convertirá en el predeterminado en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-185">If the virtual machine has multiple network adapters, then the first one shown in the list becomes the Default network adapter in the Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="902a6-186">Creación de un plan de recuperación</span><span class="sxs-lookup"><span data-stu-id="902a6-186">Creating a recovery plan</span></span>

<span data-ttu-id="902a6-187">Una vez que se haya habilitado la replicación para las máquinas virtuales del componente XenApp, el paso siguiente consiste en crear un plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="902a6-187">After replication is enabled for the XenApp component VMs, the next step is to create a recovery plan.</span></span>
<span data-ttu-id="902a6-188">Un plan de recuperación agrupa las máquinas virtuales con requisitos similares para la conmutación por error y la recuperación.</span><span class="sxs-lookup"><span data-stu-id="902a6-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="902a6-189">**Pasos para crear un plan de recuperación**</span><span class="sxs-lookup"><span data-stu-id="902a6-189">**Steps to create a recovery plan**</span></span>

1. <span data-ttu-id="902a6-190">Agregue las máquinas virtuales del componente XenApp al plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="902a6-190">Add the XenApp component virtual machines in the Recovery Plan.</span></span>
2. <span data-ttu-id="902a6-191">Haga clic en Planes de recuperación > + Plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="902a6-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="902a6-192">Proporcione un nombre intuitivo para el plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="902a6-192">Provide an intuitive name for the recovery plan.</span></span>
3. <span data-ttu-id="902a6-193">Para las máquinas virtuales de VMware, seleccione como origen un servidor de procesos de VMware, como destino Microsoft Azure y como modelo de implementación el Administrador de recursos. Después, haga clic en Seleccionar elementos.</span><span class="sxs-lookup"><span data-stu-id="902a6-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="902a6-194">Para las máquinas virtuales de Hyper-V, seleccione como origen un servidor VMM, como destino Microsoft Azure y como modelo de implementación el Administrador de recursos. Después, haga clic en Seleccionar elementos y elija las máquinas virtuales de implementación de XenApp.</span><span class="sxs-lookup"><span data-stu-id="902a6-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select the XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="902a6-195">Incorporación de máquinas virtuales a grupos de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="902a6-195">Adding virtual machines to failover groups</span></span>

<span data-ttu-id="902a6-196">Puede personalizar los planes de recuperación para agregar grupos de conmutación por error para especificar un orden de inicio, scripts o acciones manuales.</span><span class="sxs-lookup"><span data-stu-id="902a6-196">Recovery plans can be customized to add failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="902a6-197">Debe agregar los grupos siguientes al plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="902a6-197">The following groups need to be added to the recovery plan.</span></span>

1. <span data-ttu-id="902a6-198">Grupo de conmutación por error 1: DNS de AD</span><span class="sxs-lookup"><span data-stu-id="902a6-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="902a6-199">Grupo de conmutación por error 2: máquinas virtuales con SQL Server</span><span class="sxs-lookup"><span data-stu-id="902a6-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="902a6-200">Grupo de conmutación por error 3: máquina virtual de imagen maestra de VDA</span><span class="sxs-lookup"><span data-stu-id="902a6-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="902a6-201">Grupo de conmutación por error 4: máquinas virtuales del controlador de entrega y del servidor de StoreFront</span><span class="sxs-lookup"><span data-stu-id="902a6-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="902a6-202">Incorporación de scripts al plan de recuperación</span><span class="sxs-lookup"><span data-stu-id="902a6-202">Adding scripts to the recovery plan</span></span>

<span data-ttu-id="902a6-203">Puede ejecutar los scripts antes o después de un grupo específico en un plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="902a6-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="902a6-204">También puede incluir y realizar acciones manuales durante la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="902a6-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="902a6-205">El plan de recuperación personalizado es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="902a6-205">The customized recovery plan looks like the below:</span></span>

1. <span data-ttu-id="902a6-206">Grupo de conmutación por error 1: DNS de AD</span><span class="sxs-lookup"><span data-stu-id="902a6-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="902a6-207">Grupo de conmutación por error 2: máquinas virtuales con SQL Server</span><span class="sxs-lookup"><span data-stu-id="902a6-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="902a6-208">Grupo de conmutación por error 3: máquina virtual de imagen maestra de VDA</span><span class="sxs-lookup"><span data-stu-id="902a6-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="902a6-209">Los pasos 4, 6 y 7, que contienen acciones manuales o de script, solo son aplicables a un entorno de XenApp local con catálogos MCS/PVS.</span><span class="sxs-lookup"><span data-stu-id="902a6-209">Steps 4, 6 and 7 containing manual or script actions are applicable to only an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="902a6-210">Acción manual o de script del grupo 3: apagado de la máquina virtual del VDA maestro. Esta máquina, cuando se realice la conmutación por error a Azure, se encontrará en el estado "En ejecución".</span><span class="sxs-lookup"><span data-stu-id="902a6-210">Group 3 Manual or script action: Shutdown master VDA VM The Master VDA VM when failed over to Azure will be in a running state.</span></span> <span data-ttu-id="902a6-211">Para crear catálogos MCS con el hospedaje de Azure ARM, la máquina virtual del VDA maestro debe encontrarse en el estado "Detenido" (desasignada).</span><span class="sxs-lookup"><span data-stu-id="902a6-211">To create new MCS catalogs using Azure ARM hosting, the master VDA VM is required to be in Stopped (de allocated) state.</span></span> <span data-ttu-id="902a6-212">Apague la máquina virtual desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="902a6-212">Shutdown the VM from Azure Portal.</span></span>

5. <span data-ttu-id="902a6-213">Grupo de conmutación por error 4: máquinas virtuales del controlador de entrega y del servidor de StoreFront</span><span class="sxs-lookup"><span data-stu-id="902a6-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="902a6-214">Acción manual o de script 1 del grupo 3:</span><span class="sxs-lookup"><span data-stu-id="902a6-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="902a6-215">***Agregar conexión de host de Azure RM***</span><span class="sxs-lookup"><span data-stu-id="902a6-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="902a6-216">Cree una conexión de host de Azure ARM en la máquina del controlador de entrega para aprovisionar nuevos catálogos MCS en Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-216">Create Azure ARM host connection in Delivery Controller machine to provision new MCS catalogs in Azure.</span></span> <span data-ttu-id="902a6-217">Siga los pasos que se describen en este [artículo](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="902a6-217">Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="902a6-218">Acción manual o de script 2 del grupo 3:</span><span class="sxs-lookup"><span data-stu-id="902a6-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="902a6-219">***Volver a crear catálogos MCS en Azure***</span><span class="sxs-lookup"><span data-stu-id="902a6-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="902a6-220">Los clones MCS o PVS existentes en el sitio principal no se replicarán en Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-220">The existing MCS or PVS clones on the primary site will not be replicated to Azure.</span></span> <span data-ttu-id="902a6-221">Debe volver a crear estos clones mediante el VDA maestro replicado y el aprovisionamiento de Azure ARM desde el controlador de entrega. Siga los pasos que se describen en este [artículo](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) para crear catálogos MCS en Azure.</span><span class="sxs-lookup"><span data-stu-id="902a6-221">You need to recreate these clones using the replicated master VDA and Azure ARM provisioning from Delivery controller.Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) to create MCS catalogs in Azure.</span></span>

![Plan de recuperación para componentes de XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="902a6-223">Puede usar scripts en la [ubicación](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) para actualizar el DNS con las nuevas direcciones IP de las máquinas virtuales conmutadas por error o para asociar un equilibrador de carga a la máquina virtual conmutada por error, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="902a6-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) to update the DNS with the new IPs of the failed over >virtual machines or to attach a load balancer on the failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="902a6-224">Realización de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="902a6-224">Doing a test failover</span></span>

<span data-ttu-id="902a6-225">Siga [estas directrices](site-recovery-test-failover-to-azure.md) para llevar a cabo una conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="902a6-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

![Plan de recuperación](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="902a6-227">Realización de una conmutación por error</span><span class="sxs-lookup"><span data-stu-id="902a6-227">Doing a failover</span></span>

<span data-ttu-id="902a6-228">Siga [estas directrices](site-recovery-failover.md) cuando realice una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="902a6-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="902a6-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="902a6-229">Next steps</span></span>

<span data-ttu-id="902a6-230">Puede obtener [más información](https://aka.ms/citrix-xenapp-xendesktop-with-asr) sobre la replicación de implementaciones de XenApp y XenDesktop de Citrix en estas notas del producto.</span><span class="sxs-lookup"><span data-stu-id="902a6-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="902a6-231">Consulte las instrucciones para la [replicación de otras aplicaciones](site-recovery-workload.md) mediante Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="902a6-231">Look at the guidance to [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
