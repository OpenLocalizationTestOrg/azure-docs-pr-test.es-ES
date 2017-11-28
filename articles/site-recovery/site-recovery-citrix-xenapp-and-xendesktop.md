---
title: "una implementación de Citrix XenDesktop y XenApp de varios nivel con Azure Site Recovery aaaReplicate | Documentos de Microsoft"
description: "Este artículo se describe cómo tooprotect y recuperar Citrix XenDesktop XenApp las implementaciones y con Azure Site Recovery."
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
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="9fd25-103">Replicar una implementación de XenApp y XenDesktop de Citrix de niveles múltiples mediante Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="9fd25-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="9fd25-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9fd25-104">Overview</span></span>

<span data-ttu-id="9fd25-105">Citrix XenDesktop es una solución de virtualización de escritorio que ofrece aplicaciones y escritorios como ondemand servicio tooany usuario, en cualquier lugar.</span><span class="sxs-lookup"><span data-stu-id="9fd25-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service tooany user, anywhere.</span></span> <span data-ttu-id="9fd25-106">Con la tecnología de entrega FlexCast, XenDesktop puede rápida y segura entregar aplicaciones y escritorios toousers.</span><span class="sxs-lookup"><span data-stu-id="9fd25-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops toousers.</span></span>
<span data-ttu-id="9fd25-107">Actualmente, XenApp de Citrix no proporciona funciones de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="9fd25-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="9fd25-108">Una solución de recuperación ante desastres conveniente, debe permitir que el modelo de planes de recuperación alrededor de Hola por encima de arquitecturas de aplicación compleja y también tienen Hola capacidad tooadd personalizar pasos toohandle aplicación asignaciones entre los distintos niveles, por lo que proporciona un con un solo clic que captura la solución en caso de hello de un desastre iniciales tooa reducir el RTO.</span><span class="sxs-lookup"><span data-stu-id="9fd25-108">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>

<span data-ttu-id="9fd25-109">Este documento proporciona instrucciones detalladas para crear una solución de recuperación ante desastres para las implementaciones locales de XenApp de Citrix en plataformas vSphere de Hyper-V y VMware.</span><span class="sxs-lookup"><span data-stu-id="9fd25-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="9fd25-110">Este documento también se describe cómo tooperform una conmutación por error de prueba (detalles de recuperación ante desastres) y tooAzure de conmutación por error imprevista con planes de recuperación, los requisitos previos y configuraciones de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="9fd25-110">This document also describes how tooperform a test failover(disaster recovery drill) and unplanned failover tooAzure using recovery plans, hello supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9fd25-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9fd25-111">Prerequisites</span></span>

<span data-ttu-id="9fd25-112">Antes de empezar, asegúrese de que comprende siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="9fd25-112">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="9fd25-113">Replicar una máquina virtual tooAzure</span><span class="sxs-lookup"><span data-stu-id="9fd25-113">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="9fd25-114">Cómo demasiado[el diseño de una red de recuperación](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="9fd25-114">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="9fd25-115">Realizar una tooAzure de conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="9fd25-115">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="9fd25-116">Realizar una conmutación por error tooAzure</span><span class="sxs-lookup"><span data-stu-id="9fd25-116">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="9fd25-117">Cómo demasiado[replicar un controlador de dominio](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="9fd25-117">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="9fd25-118">Cómo demasiado[replicar SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="9fd25-118">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="9fd25-119">Modelos de implementación</span><span class="sxs-lookup"><span data-stu-id="9fd25-119">Deployment patterns</span></span>

<span data-ttu-id="9fd25-120">Normalmente, una granja de servidores Citrix XenApp y XenDesktop tiene Hola seguir el patrón de implementación:</span><span class="sxs-lookup"><span data-stu-id="9fd25-120">A Citrix XenApp and XenDesktop farm typically has hello following deployment pattern:</span></span>

<span data-ttu-id="9fd25-121">**Patrón de implementación**</span><span class="sxs-lookup"><span data-stu-id="9fd25-121">**Deployment pattern**</span></span>

<span data-ttu-id="9fd25-122">Implementación de XenApp y XenDesktop de Citrix con servidor DNS de AD, servidor de SQL Database, controlador de entrega de Citrix, servidor de StoreFront, XenApp Master (VDA) y servidor de licencias de XenApp de Citrix</span><span class="sxs-lookup"><span data-stu-id="9fd25-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Modelo de implementación 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="9fd25-124">Compatibilidad de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="9fd25-124">Site Recovery support</span></span>

<span data-ttu-id="9fd25-125">A fin de Hola de este artículo, administra las implementaciones de Citrix en máquinas virtuales de VMware vSphere 6.0 o System Center VMM 2012 R2 han estado usado toosetup recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="9fd25-125">For hello purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used toosetup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="9fd25-126">Origen y destino</span><span class="sxs-lookup"><span data-stu-id="9fd25-126">Source and target</span></span>

<span data-ttu-id="9fd25-127">**Escenario**</span><span class="sxs-lookup"><span data-stu-id="9fd25-127">**Scenario**</span></span> | <span data-ttu-id="9fd25-128">**sitio secundario tooa**</span><span class="sxs-lookup"><span data-stu-id="9fd25-128">**tooa secondary site**</span></span> | <span data-ttu-id="9fd25-129">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="9fd25-129">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="9fd25-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="9fd25-130">**Hyper-V**</span></span> | <span data-ttu-id="9fd25-131">Fuera del ámbito</span><span class="sxs-lookup"><span data-stu-id="9fd25-131">Not in scope</span></span> | <span data-ttu-id="9fd25-132">Sí</span><span class="sxs-lookup"><span data-stu-id="9fd25-132">Yes</span></span>
<span data-ttu-id="9fd25-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="9fd25-133">**VMware**</span></span> | <span data-ttu-id="9fd25-134">Fuera del ámbito</span><span class="sxs-lookup"><span data-stu-id="9fd25-134">Not in scope</span></span> | <span data-ttu-id="9fd25-135">Sí</span><span class="sxs-lookup"><span data-stu-id="9fd25-135">Yes</span></span>
<span data-ttu-id="9fd25-136">**Servidor físico**</span><span class="sxs-lookup"><span data-stu-id="9fd25-136">**Physical server**</span></span> | <span data-ttu-id="9fd25-137">Fuera del ámbito</span><span class="sxs-lookup"><span data-stu-id="9fd25-137">Not in scope</span></span> | <span data-ttu-id="9fd25-138">Sí</span><span class="sxs-lookup"><span data-stu-id="9fd25-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="9fd25-139">Versiones</span><span class="sxs-lookup"><span data-stu-id="9fd25-139">Versions</span></span>
<span data-ttu-id="9fd25-140">Los clientes pueden implementar componentes de XenApp como máquinas virtuales que se ejecutan en Hyper-V o VMware o como servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="9fd25-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="9fd25-141">Azure Site Recovery puede proteger tanto tooAzure las implementaciones físicas y virtuales.</span><span class="sxs-lookup"><span data-stu-id="9fd25-141">Azure Site Recovery can protect both physical and virtual deployments tooAzure.</span></span>
<span data-ttu-id="9fd25-142">Como XenApp 7.7 o una versión posterior se admite en Azure, solo las implementaciones con estas versiones pueden conmutar por error tooAzure para la migración o recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="9fd25-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over tooAzure for Disaster Recovery or migration.</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="9fd25-143">Tookeep de cosas en cuenta</span><span class="sxs-lookup"><span data-stu-id="9fd25-143">Things tookeep in mind</span></span>

1. <span data-ttu-id="9fd25-144">Protección y recuperación de local se admite implementaciones con sistema operativo Server máquinas toodeliver XenApp las aplicaciones publicadas y XenApp publicado escritorios.</span><span class="sxs-lookup"><span data-stu-id="9fd25-144">Protection and recovery of on-premises deployments using Server OS machines toodeliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="9fd25-145">Protección y recuperación de las implementaciones locales mediante Escritorio toodeliver de máquinas de sistema operativo de escritorio VDI para escritorios virtuales del cliente, incluida Windows 10, no se admite.</span><span class="sxs-lookup"><span data-stu-id="9fd25-145">Protection and recovery of on-premises deployments using desktop OS machines toodeliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="9fd25-146">Esto es porque ASR no admite la recuperación de Hola de equipos con escritorio OS'es.</span><span class="sxs-lookup"><span data-stu-id="9fd25-146">This is because ASR does not support hello recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="9fd25-147">Además, todavía no se admiten algunos tipos de escritorio virtual de cliente (por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="9fd25-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="9fd25-148">Windows 7) para la concesión de licencias en Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd25-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="9fd25-149">Aquí encontrará [más información](https://azure.microsoft.com/pricing/licensing-faq/) acerca de la concesión de licencias a escritorios de cliente/servidor de Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd25-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="9fd25-150">Azure Site Recovery no puede replicar y proteger clones locales de MCS o PVS existentes.</span><span class="sxs-lookup"><span data-stu-id="9fd25-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="9fd25-151">Debe toorecreate estos clones usar Azure RM el aprovisionamiento de controlador de entrega.</span><span class="sxs-lookup"><span data-stu-id="9fd25-151">You need toorecreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="9fd25-152">No se puede proteger NetScaler con Azure Site Recovery, ya que NetScaler se basa en FreeBSD y Azure Site Recovery no admite la protección del sistema operativo de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="9fd25-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="9fd25-153">¿Necesita toodeploy y configurar un nuevo dispositivo NetScaler de mercado de Azure después de la conmutación por error tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9fd25-153">You would need toodeploy and configure a new NetScaler appliance from Azure Market place after failover tooAzure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="9fd25-154">Replicación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9fd25-154">Replicating virtual machines</span></span>

<span data-ttu-id="9fd25-155">Hola de hello Citrix XenApp implementación de los componentes siguientes necesita toobe protegido tooenable replicación y la recuperación.</span><span class="sxs-lookup"><span data-stu-id="9fd25-155">hello following components of hello Citrix XenApp deployment need toobe protected tooenable replication and recovery.</span></span>

* <span data-ttu-id="9fd25-156">Protección del servidor DNS de AD</span><span class="sxs-lookup"><span data-stu-id="9fd25-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="9fd25-157">Protección del servidor de SQL Database</span><span class="sxs-lookup"><span data-stu-id="9fd25-157">Protection of SQL database server</span></span>
* <span data-ttu-id="9fd25-158">Protección del controlador de entrega de Citrix</span><span class="sxs-lookup"><span data-stu-id="9fd25-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="9fd25-159">Protección del servidor de StoreFront</span><span class="sxs-lookup"><span data-stu-id="9fd25-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="9fd25-160">Protección de XenApp Master (VDA)</span><span class="sxs-lookup"><span data-stu-id="9fd25-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="9fd25-161">Protección del servidor de licencias de XenApp de Citrix</span><span class="sxs-lookup"><span data-stu-id="9fd25-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="9fd25-162">**Replicación del servidor DNS de AD**</span><span class="sxs-lookup"><span data-stu-id="9fd25-162">**AD DNS server replication**</span></span>

<span data-ttu-id="9fd25-163">Consulte demasiado[proteger Active Directory y DNS con Azure Site Recovery](site-recovery-active-directory.md) de guía para replicar y configurar un controlador de dominio en Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd25-163">Please refer too[Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="9fd25-164">**Replicación del servidor de SQL Database**</span><span class="sxs-lookup"><span data-stu-id="9fd25-164">**SQL database Server replication**</span></span>

<span data-ttu-id="9fd25-165">Consulte demasiado[proteger SQL Server con la recuperación ante desastres de SQL Server y Azure Site Recovery](site-recovery-sql.md) para orientación técnica detallada sobre Hola opciones recomendadas para proteger los servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="9fd25-165">Please refer too[Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on hello recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="9fd25-166">Siga [esta guía](site-recovery-vmware-to-azure.md) toostart replicar Hola otro tooAzure de máquinas virtuales de componente.</span><span class="sxs-lookup"><span data-stu-id="9fd25-166">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello other component virtual machines tooAzure.</span></span>

![Protección de componentes de XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="9fd25-168">**Configuración de proceso y red**</span><span class="sxs-lookup"><span data-stu-id="9fd25-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="9fd25-169">Después de hello equipos están protegidos (estado se muestra como "Protegido" en elementos de replicar), Hola proceso y configuración de red necesita toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="9fd25-169">After hello machines are protected (status shows as “Protected” under Replicated Items), hello Compute and Network settings need toobe configured.</span></span>
<span data-ttu-id="9fd25-170">En proceso y red > calcular propiedades, puede especificar el tamaño de nombre y de destino de la máquina virtual de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd25-170">In Compute and Network > Compute properties, you can specify hello Azure VM name and target size.</span></span>
<span data-ttu-id="9fd25-171">Modificar Hola nombre toocomply requisitos de Azure si necesita.</span><span class="sxs-lookup"><span data-stu-id="9fd25-171">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="9fd25-172">También puede ver y agregar información acerca de la red de destino de hello, subred y dirección IP que se va a asignar toohello máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd25-172">You can also view and add information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span>

<span data-ttu-id="9fd25-173">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="9fd25-173">Note hello following:</span></span>

* <span data-ttu-id="9fd25-174">Puede establecer la dirección IP de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd25-174">You can set hello target IP address.</span></span> <span data-ttu-id="9fd25-175">Si no proporciona una dirección, Hola conmutado por error equipo usará DHCP.</span><span class="sxs-lookup"><span data-stu-id="9fd25-175">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="9fd25-176">Si establece una dirección que no está disponible en la conmutación por error, conmutación por error de hello no funcionará.</span><span class="sxs-lookup"><span data-stu-id="9fd25-176">If you set an address that isn't available at failover, hello failover won't work.</span></span> <span data-ttu-id="9fd25-177">Hola la misma dirección IP de destino puede usarse para la conmutación por error si está disponible en la red de conmutación por error de prueba de Hola Hola dirección.</span><span class="sxs-lookup"><span data-stu-id="9fd25-177">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

* <span data-ttu-id="9fd25-178">Para el servidor de AD/DNS hello, conservando Hola local dirección le permite que especificar Hola igual de direcciones como servidor DNS de hello para la red Virtual de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd25-178">For hello AD/DNS server, retaining hello on-premises address lets you specify hello same address as hello DNS server for hello Azure Virtual network.</span></span>

<span data-ttu-id="9fd25-179">número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de hello, del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="9fd25-179">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

*   <span data-ttu-id="9fd25-180">Si el número de Hola de adaptadores de red en la máquina de origen de hello es menor o igual toohello de adaptadores permitidas para el tamaño de máquina de destino de hello, a continuación, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd25-180">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
*   <span data-ttu-id="9fd25-181">Si número Hola de adaptadores para la máquina virtual de origen de hello supera número Hola permitido para el tamaño de destino de hello después máximo de tamaño de destino de Hola se usará.</span><span class="sxs-lookup"><span data-stu-id="9fd25-181">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
* <span data-ttu-id="9fd25-182">Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores.</span><span class="sxs-lookup"><span data-stu-id="9fd25-182">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="9fd25-183">Si la máquina de origen hello tiene dos adaptadores de pero hello tamaño de destino admitida solo admite un equipo de destino de Hola tendrá solo un adaptador.</span><span class="sxs-lookup"><span data-stu-id="9fd25-183">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>
*   <span data-ttu-id="9fd25-184">Si la máquina virtual de hello tiene varios adaptadores de red se conectarán todos toohello misma red.</span><span class="sxs-lookup"><span data-stu-id="9fd25-184">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
*   <span data-ttu-id="9fd25-185">Si la máquina virtual de hello tiene varios adaptadores de red, a continuación, hello primera se muestra en la lista de Hola se convierte en adaptador de red predeterminada de Hola Hola máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd25-185">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello Default network adapter in hello Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="9fd25-186">Creación de un plan de recuperación</span><span class="sxs-lookup"><span data-stu-id="9fd25-186">Creating a recovery plan</span></span>

<span data-ttu-id="9fd25-187">Después de habilita la replicación para máquinas virtuales de componente de XenApp hello, Hola siguiente paso es toocreate un plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="9fd25-187">After replication is enabled for hello XenApp component VMs, hello next step is toocreate a recovery plan.</span></span>
<span data-ttu-id="9fd25-188">Un plan de recuperación agrupa las máquinas virtuales con requisitos similares para la conmutación por error y la recuperación.</span><span class="sxs-lookup"><span data-stu-id="9fd25-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="9fd25-189">**Pasos toocreate un plan de recuperación**</span><span class="sxs-lookup"><span data-stu-id="9fd25-189">**Steps toocreate a recovery plan**</span></span>

1. <span data-ttu-id="9fd25-190">Agregar máquinas virtuales de hello XenApp componente Hola Plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="9fd25-190">Add hello XenApp component virtual machines in hello Recovery Plan.</span></span>
2. <span data-ttu-id="9fd25-191">Haga clic en Planes de recuperación > + Plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="9fd25-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="9fd25-192">Proporcionar un nombre para el plan de recuperación de hello intuitiva.</span><span class="sxs-lookup"><span data-stu-id="9fd25-192">Provide an intuitive name for hello recovery plan.</span></span>
3. <span data-ttu-id="9fd25-193">Para las máquinas virtuales de VMware, seleccione como origen un servidor de procesos de VMware, como destino Microsoft Azure y como modelo de implementación el Administrador de recursos. Después, haga clic en Seleccionar elementos.</span><span class="sxs-lookup"><span data-stu-id="9fd25-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="9fd25-194">Para las máquinas virtuales de Hyper-V: Seleccionar origen como servidor de VMM, como Microsoft Azure y el modelo de implementación como el Administrador de recursos de destino y haga clic en la selección de elementos y, a continuación, seleccione VM de la implementación de XenApp Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd25-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select hello XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="9fd25-195">Agregar grupos de toofailover de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9fd25-195">Adding virtual machines toofailover groups</span></span>

<span data-ttu-id="9fd25-196">Planes de recuperación pueden ser grupos de conmutación por error de tooadd personalizados para las acciones de orden, las secuencias de comandos o manual de inicio específico.</span><span class="sxs-lookup"><span data-stu-id="9fd25-196">Recovery plans can be customized tooadd failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="9fd25-197">los grupos siguientes de Hola necesita plan de recuperación de toobe toohello agregada.</span><span class="sxs-lookup"><span data-stu-id="9fd25-197">hello following groups need toobe added toohello recovery plan.</span></span>

1. <span data-ttu-id="9fd25-198">Grupo de conmutación por error 1: DNS de AD</span><span class="sxs-lookup"><span data-stu-id="9fd25-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="9fd25-199">Grupo de conmutación por error 2: máquinas virtuales con SQL Server</span><span class="sxs-lookup"><span data-stu-id="9fd25-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="9fd25-200">Grupo de conmutación por error 3: máquina virtual de imagen maestra de VDA</span><span class="sxs-lookup"><span data-stu-id="9fd25-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="9fd25-201">Grupo de conmutación por error 4: máquinas virtuales del controlador de entrega y del servidor de StoreFront</span><span class="sxs-lookup"><span data-stu-id="9fd25-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="9fd25-202">Agregar plan de recuperación de toohello de secuencias de comandos</span><span class="sxs-lookup"><span data-stu-id="9fd25-202">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="9fd25-203">Puede ejecutar los scripts antes o después de un grupo específico en un plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="9fd25-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="9fd25-204">También puede incluir y realizar acciones manuales durante la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="9fd25-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="9fd25-205">plan de recuperación personalizada Hello es similar a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="9fd25-205">hello customized recovery plan looks like hello below:</span></span>

1. <span data-ttu-id="9fd25-206">Grupo de conmutación por error 1: DNS de AD</span><span class="sxs-lookup"><span data-stu-id="9fd25-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="9fd25-207">Grupo de conmutación por error 2: máquinas virtuales con SQL Server</span><span class="sxs-lookup"><span data-stu-id="9fd25-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="9fd25-208">Grupo de conmutación por error 3: máquina virtual de imagen maestra de VDA</span><span class="sxs-lookup"><span data-stu-id="9fd25-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="9fd25-209">Los pasos 4, 6 y 7 que contiene acciones manuales o de scripts son aplicable tooonly un XenApp local > entorno con catálogos MCS/PVS.</span><span class="sxs-lookup"><span data-stu-id="9fd25-209">Steps 4, 6 and 7 containing manual or script actions are applicable tooonly an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="9fd25-210">Acción de script o Manual del grupo 3: Hola de VDA VM maestra apagado Master VDA VM si ha conmutado tooAzure estará en estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9fd25-210">Group 3 Manual or script action: Shutdown master VDA VM hello Master VDA VM when failed over tooAzure will be in a running state.</span></span> <span data-ttu-id="9fd25-211">toocreate con Azure ARM de hospedaje nuevos catálogos MCS, maestro de hello VDA VM es necesario toobe en detenido (Alemania asignado) estado.</span><span class="sxs-lookup"><span data-stu-id="9fd25-211">toocreate new MCS catalogs using Azure ARM hosting, hello master VDA VM is required toobe in Stopped (de allocated) state.</span></span> <span data-ttu-id="9fd25-212">Hola apagar VM desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd25-212">Shutdown hello VM from Azure Portal.</span></span>

5. <span data-ttu-id="9fd25-213">Grupo de conmutación por error 4: máquinas virtuales del controlador de entrega y del servidor de StoreFront</span><span class="sxs-lookup"><span data-stu-id="9fd25-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="9fd25-214">Acción manual o de script 1 del grupo 3:</span><span class="sxs-lookup"><span data-stu-id="9fd25-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="9fd25-215">***Agregar conexión de host de Azure RM***</span><span class="sxs-lookup"><span data-stu-id="9fd25-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="9fd25-216">Crear conexión a host ARM de Azure en el controlador de entrega máquina tooprovision nuevos catálogos MCS en Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd25-216">Create Azure ARM host connection in Delivery Controller machine tooprovision new MCS catalogs in Azure.</span></span> <span data-ttu-id="9fd25-217">Siga los pasos de hello tal como se describe en este [artículo](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="9fd25-217">Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="9fd25-218">Acción manual o de script 2 del grupo 3:</span><span class="sxs-lookup"><span data-stu-id="9fd25-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="9fd25-219">***Volver a crear catálogos MCS en Azure***</span><span class="sxs-lookup"><span data-stu-id="9fd25-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="9fd25-220">Hola existente MCS o PVS clones en sitio primario de hello no estará tooAzure replicada.</span><span class="sxs-lookup"><span data-stu-id="9fd25-220">hello existing MCS or PVS clones on hello primary site will not be replicated tooAzure.</span></span> <span data-ttu-id="9fd25-221">Necesita toorecreate estos clones con hello replicaron VDA maestro y ARM de Azure de aprovisionamiento de controlador de entrega. Siga los pasos de hello tal como se describe en este [artículo](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catálogos en Azure.</span><span class="sxs-lookup"><span data-stu-id="9fd25-221">You need toorecreate these clones using hello replicated master VDA and Azure ARM provisioning from Delivery controller.Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogs in Azure.</span></span>

![Plan de recuperación para componentes de XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="9fd25-223">Puede utilizar secuencias de comandos en [ubicación](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate Hola DNS con hello conmutarán por error nuevas direcciones IP de hello > máquinas virtuales o tooattach un equilibrador de carga en hello conmutado por error la máquina virtual, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9fd25-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS with hello new IPs of hello failed over >virtual machines or tooattach a load balancer on hello failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="9fd25-224">Realización de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="9fd25-224">Doing a test failover</span></span>

<span data-ttu-id="9fd25-225">Siga [esta guía](site-recovery-test-failover-to-azure.md) toodo una conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="9fd25-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

![Plan de recuperación](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="9fd25-227">Realización de una conmutación por error</span><span class="sxs-lookup"><span data-stu-id="9fd25-227">Doing a failover</span></span>

<span data-ttu-id="9fd25-228">Siga [estas directrices](site-recovery-failover.md) cuando realice una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="9fd25-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fd25-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9fd25-229">Next steps</span></span>

<span data-ttu-id="9fd25-230">Puede obtener [más información](https://aka.ms/citrix-xenapp-xendesktop-with-asr) sobre la replicación de implementaciones de XenApp y XenDesktop de Citrix en estas notas del producto.</span><span class="sxs-lookup"><span data-stu-id="9fd25-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="9fd25-231">Mire instrucciones Hola demasiado[replicar otras aplicaciones](site-recovery-workload.md) con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9fd25-231">Look at hello guidance too[replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
