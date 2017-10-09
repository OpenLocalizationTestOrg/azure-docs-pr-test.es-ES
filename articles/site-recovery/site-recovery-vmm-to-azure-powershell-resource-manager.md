---
title: "máquinas virtuales de Hyper-V aaaReplicate en nubes VMM con Azure Site Recovery y PowerShell (Administrador de recursos) | Documentos de Microsoft"
description: "Replicar máquinas virtuales de Hyper-V en nubes VMM con Azure Site Recovery y PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="38870-103">Replicar máquinas virtuales de Hyper-V en tooAzure de nubes VMM mediante PowerShell y el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="38870-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38870-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="38870-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="38870-105">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="38870-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="38870-106">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="38870-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="38870-107">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="38870-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="38870-108">Información general</span><span class="sxs-lookup"><span data-stu-id="38870-108">Overview</span></span>
<span data-ttu-id="38870-109">Azure Site Recovery contribuye estrategia de recuperación (BCDR) ante desastres y continuidad del negocio de tooyour mediante la coordinación de replicación, la conmutación por error y la recuperación de máquinas virtuales en un número de escenarios de implementación.</span><span class="sxs-lookup"><span data-stu-id="38870-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="38870-110">Para obtener una lista completa de la implementación de escenarios vea hello [Introducción a Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38870-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="38870-111">Este artículo muestra cómo las tareas comunes de toouse PowerShell tooautomate necesita tooperform al configurar máquinas de virtuales de Hyper-V de Azure Site Recovery tooreplicate en almacenamiento de tooAzure de nubes de System Center VMM.</span><span class="sxs-lookup"><span data-stu-id="38870-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="38870-112">Hola artículo incluye requisitos previos de escenario de Hola y muestra</span><span class="sxs-lookup"><span data-stu-id="38870-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="38870-113">¿Cómo tooset un almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="38870-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="38870-114">Instalar hello Azure Site Recovery Provider Hola servidor VMM de origen</span><span class="sxs-lookup"><span data-stu-id="38870-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="38870-115">Registrar servidor hello en el almacén de hello, agregue una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="38870-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="38870-116">Instalar el agente de servicios de recuperación de Azure de hello en los servidores de host de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="38870-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="38870-117">Configurar la protección para nubes VMM, que serán aplicado tooall protegido las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="38870-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="38870-118">Habilite la protección para esas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="38870-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="38870-119">Probar toomake de conmutación por error de Hola que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="38870-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="38870-120">Si experimenta problemas al configurar este escenario, publicar sus preguntas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="38870-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="38870-121">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="38870-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="38870-122">Este artículo tratan con modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="38870-123">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="38870-123">Before you start</span></span>
<span data-ttu-id="38870-124">Asegúrese de que tiene preparados estos requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="38870-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="38870-125">Requisitos previos de Azure</span><span class="sxs-lookup"><span data-stu-id="38870-125">Azure prerequisites</span></span>
* <span data-ttu-id="38870-126">Necesitará una cuenta de [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="38870-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="38870-127">Si no tiene una, comience con un [cuenta gratuita](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="38870-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="38870-128">Además, puede leer sobre hello [precios de Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="38870-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="38870-129">Si va a probar el escenario suscripción CSP de hello replicación tooa, necesitará una suscripción de CSP.</span><span class="sxs-lookup"><span data-stu-id="38870-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="38870-130">Más información acerca del programa Hola CSP en [cómo tooenroll en programa CSP hello](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="38870-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="38870-131">Necesitará un tooAzure Azure v2 (Administrador de recursos) de almacenamiento cuenta toostore datos replicados.</span><span class="sxs-lookup"><span data-stu-id="38870-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="38870-132">cuenta de Hello tiene habilitada la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="38870-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="38870-133">Debe ser en Hola misma región que Hola servicio Azure Site Recovery y estar asociado con hello misma suscripción u Hola CSP.</span><span class="sxs-lookup"><span data-stu-id="38870-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="38870-134">toolearn más acerca de cómo configurar el almacenamiento de Azure, vea hello [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md) como referencia.</span><span class="sxs-lookup"><span data-stu-id="38870-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="38870-135">Necesitará toomake seguro de que las máquinas virtuales que desee tooprotect cumplen con hello [requisitos previos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="38870-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="38870-136">Actualmente, solo las operaciones de nivel de máquina virtual son posibles a través de Powershell.</span><span class="sxs-lookup"><span data-stu-id="38870-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="38870-137">Pronto se incluirá compatibilidad con operaciones de nivel de plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="38870-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="38870-138">Por ahora, es tooperforming limita las conmutaciones por error solo en una granularidad 'protected VM' y no en un nivel de Plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="38870-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="38870-139">Requisitos previos de VMM</span><span class="sxs-lookup"><span data-stu-id="38870-139">VMM prerequisites</span></span>
* <span data-ttu-id="38870-140">Necesitará un servidor VMM que se ejecute en System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="38870-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="38870-141">Cualquier servidor VMM que contengan máquinas virtuales que desee tooprotect debe estar en ejecución hello Azure Site Recovery Provider.</span><span class="sxs-lookup"><span data-stu-id="38870-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="38870-142">Se instala durante la implementación de Azure Site Recovery Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="38870-143">Necesitará al menos una nube en el servidor VMM que desee tooprotect Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="38870-144">en la nube Hola debe contener:</span><span class="sxs-lookup"><span data-stu-id="38870-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="38870-145">Uno o más grupos de hosts de VMM</span><span class="sxs-lookup"><span data-stu-id="38870-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="38870-146">Uno o más servidores host de Hyper-V o clústeres en cada grupo de hosts</span><span class="sxs-lookup"><span data-stu-id="38870-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="38870-147">Máquinas virtuales de uno o más en el servidor de Hyper-V de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="38870-148">Más información acerca de cómo configurar las nubes de VMM:</span><span class="sxs-lookup"><span data-stu-id="38870-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="38870-149">Obtener más información acerca de las nubes privadas de VMM en [What's New en la nube privada con System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) y en [nubes de VMM 2012 y hello](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="38870-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="38870-150">Obtenga información acerca de cómo [Hola configurar VMM tejido de nube](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="38870-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="38870-151">Una vez configurados los elementos del tejido de nube, aprenda a crear nubes privadas en [Creación de una nube privada en VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) y [Tutorial: Creación de nubes privadas con System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="38870-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="38870-152">Requisitos previos de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="38870-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="38870-153">Hello servidores host Hyper-V deben ejecutar al menos **Windows Server 2012** con el rol de Hyper-V o **Microsoft Hyper-V Server 2012** y ha hello las últimas actualizaciones instaladas.</span><span class="sxs-lookup"><span data-stu-id="38870-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="38870-154">Si está ejecutando Hyper-V en un clúster, tenga en cuenta que ese agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="38870-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="38870-155">Necesitará a un agente de clúster hello tooconfigure manualmente.</span><span class="sxs-lookup"><span data-stu-id="38870-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="38870-156">Para</span><span class="sxs-lookup"><span data-stu-id="38870-156">For</span></span>
* <span data-ttu-id="38870-157">Para obtener instrucciones, consulte [cómo tooConfigure agente de réplica de Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="38870-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="38870-158">Cualquier servidor de host de Hyper-V o clúster que se desea protección toomanage debe incluirse en una nube de VMM.</span><span class="sxs-lookup"><span data-stu-id="38870-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="38870-159">Requisitos previos de asignación de redes</span><span class="sxs-lookup"><span data-stu-id="38870-159">Network mapping prerequisites</span></span>
<span data-ttu-id="38870-160">Al proteger máquinas virtuales en Azure, la asignación de red Hola asigna redes de máquinas virtuales de hello en el servidor VMM de origen de Hola y siguientes de Hola de tooenable de redes de Azure de destino:</span><span class="sxs-lookup"><span data-stu-id="38870-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="38870-161">Todas las máquinas que conmutar por error en hello mismo pueden conectar tooeach otro, independientemente del plan de recuperación que se encuentran en red.</span><span class="sxs-lookup"><span data-stu-id="38870-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="38870-162">Si una puerta de enlace de red es el programa de instalación en red de Azure de destino de hello, máquinas virtuales pueden conectarse a máquinas virtuales de tooother local.</span><span class="sxs-lookup"><span data-stu-id="38870-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="38870-163">Si no configura la asignación de red, solo Hola máquinas virtuales que conmutan en hello mismo plan de recuperación será capaz de tooconnect tooeach otros después tooAzure de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="38870-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="38870-164">Si desea que la asignación de red toodeploy, necesitará la siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="38870-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="38870-165">Hello las máquinas virtuales que desee tooprotect Hola servidor VMM de origen debe ser una red de VM tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="38870-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="38870-166">Esta red debe ser tooa vinculado red lógica que está asociado a la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="38870-167">Puede conectar una red Azure toowhich replicado a máquinas virtuales después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="38870-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="38870-168">Esta red seleccionará en tiempo de Hola de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="38870-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="38870-169">red de Hello debe formar parte de hello misma región que su suscripción de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="38870-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="38870-170">Más información sobre asignación de redes en</span><span class="sxs-lookup"><span data-stu-id="38870-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="38870-171">¿Cómo tooconfigure redes lógicas en VMM</span><span class="sxs-lookup"><span data-stu-id="38870-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="38870-172">¿Cómo tooconfigure VM redes y puertas de enlace en VMM</span><span class="sxs-lookup"><span data-stu-id="38870-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="38870-173">¿Cómo tooconfigure y supervisar redes virtuales en Azure</span><span class="sxs-lookup"><span data-stu-id="38870-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="38870-174">Requisitos previos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="38870-174">PowerShell prerequisites</span></span>
<span data-ttu-id="38870-175">Asegúrese de que tiene listo toogo de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="38870-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="38870-176">Si ya usa PowerShell, deberá tooupgrade tooversion 0.8.10 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="38870-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="38870-177">Para obtener información acerca de cómo configurar PowerShell, vea hello [guía tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="38870-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="38870-178">Una vez que se instala y configura PowerShell, puede ver todos los cmdlets disponibles de hello para el servicio de Hola de [aquí](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="38870-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="38870-179">toolearn acerca de las sugerencias que pueden ayudarle a usar los cmdlets de hello, como cómo normalmente se controlan los valores de parámetro, las entradas y salidas en Azure PowerShell, vea hello [guía tooget iniciado con Cmdlets de Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="38870-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="38870-180">Paso 1: Configurar la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="38870-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="38870-181">De Azure powershell, inicio de sesión tooyour cuenta de Azure: mediante Hola después cmdlets</span><span class="sxs-lookup"><span data-stu-id="38870-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="38870-182">Obtenga una lista de las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="38870-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="38870-183">Esto mostrará también Hola identificadores de suscripción para cada una de las suscripciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="38870-184">Anote subscriptionID Hola de suscripción de hello en el que desea que el almacén de servicios de recuperación de hello toocreate</span><span class="sxs-lookup"><span data-stu-id="38870-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="38870-185">Establecer suscripción hello en qué Hola almacén de servicios de recuperación es toobe creado por mencionar Hola Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="38870-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="38870-186">Paso 2: Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="38870-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="38870-187">Cree un grupo de recursos en Azure Resource Manager si todavía no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="38870-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="38870-188">Crear un nuevo almacén de servicios de recuperación y guardar Hola creado el objeto de almacén de ASR en una variable (se usará más adelante).</span><span class="sxs-lookup"><span data-stu-id="38870-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="38870-189">También puede recuperar Hola ASR almacén post creación del objeto mediante el cmdlet Get-AzureRMRecoveryServicesVault Hola:-</span><span class="sxs-lookup"><span data-stu-id="38870-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="38870-190">Paso 3: Establecer contexto de almacén de servicios de recuperación de Hola</span><span class="sxs-lookup"><span data-stu-id="38870-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="38870-191">Establecer contexto de almacén de hello ejecutando Hola comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="38870-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="38870-192">Paso 4: Instalar hello Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="38870-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="38870-193">En la máquina VMM hello, cree un directorio ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="38870-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="38870-194">Extraiga los archivos de hello mediante el proveedor de hello descargado ejecutando el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="38870-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="38870-195">Instalar a proveedor de hello mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="38870-195">Install hello provider using hello following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="38870-196">Espere Hola instalación toofinish.</span><span class="sxs-lookup"><span data-stu-id="38870-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="38870-197">Registrar servidor de hello en almacén de hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="38870-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="38870-198">Paso 5: Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="38870-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="38870-199">Si no tiene una cuenta de almacenamiento de Azure, cree una cuenta de replicación geográfica habilitada en hello mismo geográfica como Hola almacén ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="38870-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="38870-200">Tenga en cuenta que debe ser la cuenta de almacenamiento de hello en Hola misma región que el servicio de Azure Site Recovery de Hola y asociarse Hola misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="38870-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="38870-201">Paso 6: Instalar Hola agente de servicios de recuperación de Azure</span><span class="sxs-lookup"><span data-stu-id="38870-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="38870-202">Descargar agente de servicios de recuperación de Azure de hello en [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) y de instalación en cada servidor de host de Hyper-V ubicado en hello VMM nubes desea tooprotect.</span><span class="sxs-lookup"><span data-stu-id="38870-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="38870-203">Ejecute hello siguiente comando en todos los hosts VMM:</span><span class="sxs-lookup"><span data-stu-id="38870-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="38870-204">Paso 7: Configuración de la protección de la nube</span><span class="sxs-lookup"><span data-stu-id="38870-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="38870-205">Crear un tooAzure de la directiva de replicación mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="38870-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="38870-206">Obtener un contenedor de protección mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="38870-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="38870-207">Obtener la Hola directiva detalles tooa variable con trabajo Hola que creó y mencionar el nombre de directiva descriptivo hello:</span><span class="sxs-lookup"><span data-stu-id="38870-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="38870-208">Comience asociación Hola del contenedor de protección de hello con la directiva de replicación de hello:</span><span class="sxs-lookup"><span data-stu-id="38870-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="38870-209">Cuando haya finalizado el trabajo de hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="38870-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="38870-210">Después de que el trabajo de hello ha finalizado el procesamiento, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="38870-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="38870-211">finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).</span><span class="sxs-lookup"><span data-stu-id="38870-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="38870-212">Paso 8: Configuración de la asignación de red</span><span class="sxs-lookup"><span data-stu-id="38870-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="38870-213">Antes de empezar la asignación de red Compruebe que máquinas virtuales en el servidor VMM de origen Hola son red de VM tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="38870-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="38870-214">Además, cree una o varias redes virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="38870-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="38870-215">Obtener más información sobre cómo toocreate a virtual red con PowerShell y el Administrador de recursos de Azure en [crear una red virtual con una conexión de VPN de sitio a sitio mediante el Administrador de recursos de Azure y PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="38870-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="38870-216">Tenga en cuenta que varias redes de máquina Virtual pueden ser asignado tooa sola red de Azure.</span><span class="sxs-lookup"><span data-stu-id="38870-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="38870-217">Si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, entonces Hola máquina virtual será toothat conectado subred de destino después de una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="38870-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="38870-218">Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="38870-219">Hola primer comando obtiene servidores de almacén de Azure Site Recovery de hello actual.</span><span class="sxs-lookup"><span data-stu-id="38870-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="38870-220">comando Hello almacena servidores de Microsoft Azure Site Recovery de hello en la variable de matriz de hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="38870-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="38870-221">Hola segundo comando obtiene red de recuperación de sitio de hello para el primer servidor de hello en la matriz de hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="38870-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="38870-222">comando Hello almacena redes hello en la variable de hello $Networks.</span><span class="sxs-lookup"><span data-stu-id="38870-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="38870-223">Hola tercer comando obtiene redes virtuales de Azure y, a continuación, ese valor en la variable de hello $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="38870-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="38870-224">Hola final cmdlet crea una asignación entre la red principal de Hola y de red de máquina virtual de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="38870-225">Hola cmdlet especifica la red principal de hello como primer elemento de Hola de $Networks.</span><span class="sxs-lookup"><span data-stu-id="38870-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="38870-226">Hola cmdlet especifica una red de máquina virtual como primer elemento de Hola de $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="38870-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="38870-227">Paso 9: Habilitación de la protección para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="38870-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="38870-228">Después de redes, las nubes y servidores de hello están configuradas correctamente, puede habilitar la protección de máquinas virtuales en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="38870-229">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="38870-229">Note hello following:</span></span>

* <span data-ttu-id="38870-230">Las máquinas virtuales de deben cumplir los requisitos de Azure.</span><span class="sxs-lookup"><span data-stu-id="38870-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="38870-231">Compruebe estos [requisitos previos y compatibilidad](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) en la Guía de planificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="38870-232">protección de tooenable, sistema operativo de Hola y las propiedades de disco de sistema operativo deben establecerse para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="38870-233">Cuando se crea una máquina virtual en VMM mediante una plantilla de máquina virtual puede establecer la propiedad Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="38870-234">También puede establecer estas propiedades para las máquinas virtuales existentes en hello **General** y **configuración de Hardware** fichas de propiedades de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="38870-235">Si no establece estas propiedades en VMM estará tooconfigure capaz de ellas en el portal de Azure Site Recovery Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="38870-236">protección de tooenable, ejecute hello después de contenedor de protección de hello tooget de comando:</span><span class="sxs-lookup"><span data-stu-id="38870-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="38870-237">Obtener la entidad de protección de hello (VM) mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="38870-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="38870-238">Habilitar hello recuperación ante desastres para hello VM mediante la ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="38870-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="38870-239">Prueba de la implementación</span><span class="sxs-lookup"><span data-stu-id="38870-239">Test your deployment</span></span>
<span data-ttu-id="38870-240">tootest su implementación, puede ejecutar una prueba de conmutación por error para una sola máquina virtual, o crear un plan de recuperación que consta de varias máquinas virtuales y ejecutar una conmutación por error de prueba para el plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="38870-241">La conmutación por error de prueba simula el mecanismo de conmutación por error y recuperación en una red aislada.</span><span class="sxs-lookup"><span data-stu-id="38870-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="38870-242">Observe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="38870-242">Note that:</span></span>

* <span data-ttu-id="38870-243">Si desea tooconnect toohello virtual machine en Azure mediante Escritorio remoto después de la conmutación por error de hello, habilite la conexión a Escritorio remoto en la máquina virtual de hello antes de ejecutar la conmutación por error de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="38870-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="38870-244">Después de una conmutación por error, deberá usar una máquina de virtual toohello pública del tooconnect de dirección IP en Azure mediante Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="38870-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="38870-245">Si desea toodo esto, asegúrese de que no hay ninguna directiva de dominio que impiden la conexión máquina virtual de tooa con una dirección pública.</span><span class="sxs-lookup"><span data-stu-id="38870-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="38870-246">finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).</span><span class="sxs-lookup"><span data-stu-id="38870-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="38870-247">Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="38870-247">Run a test failover</span></span>
- <span data-ttu-id="38870-248">Iniciar conmutación por error de prueba de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="38870-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="38870-249">Ejecución de una conmutación por error planeada</span><span class="sxs-lookup"><span data-stu-id="38870-249">Run a planned failover</span></span>
- <span data-ttu-id="38870-250">Hola de inicio de conmutación por error planeada mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="38870-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="38870-251">Ejecución de una conmutación por error no planeada</span><span class="sxs-lookup"><span data-stu-id="38870-251">Run an unplanned failover</span></span>
- <span data-ttu-id="38870-252">Iniciar Hola de conmutación por error no planeada ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="38870-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="38870-253"><a name=monitor></a> Supervisión de la actividad</span><span class="sxs-lookup"><span data-stu-id="38870-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="38870-254">Usar hello después de la actividad de hello toomonitor de comandos.</span><span class="sxs-lookup"><span data-stu-id="38870-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="38870-255">Tenga en cuenta que tiene toowait entre los trabajos de hello toofinish de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="38870-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="38870-256">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="38870-256">Next steps</span></span>
<span data-ttu-id="38870-257">[Más información](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre los cmdlets de PowerShell de Azure Site Recovery con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="38870-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
