---
title: "máquinas virtuales de Hyper-V en el sitio secundario de VMM tooa con PowerShell (Administrador de recursos de Azure) aaaReplicate | Documentos de Microsoft"
description: "Describe cómo la replicación de tooorchestrate de Azure Site Recovery toodeploy, la conmutación por error y la recuperación de máquinas virtuales de Hyper-V en VMM nubes sitio VMM secundario tooa con PowerShell (Administrador de recursos)"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="a6b9d-103">Replicar máquinas virtuales de Hyper-V en VMM nubes tooa sitio VMM secundario con PowerShell (Administrador de recursos)</span><span class="sxs-lookup"><span data-stu-id="a6b9d-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6b9d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a6b9d-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="a6b9d-105">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="a6b9d-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="a6b9d-106">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="a6b9d-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="a6b9d-107">Bienvenido tooAzure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-107">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="a6b9d-108">Use este artículo si desea tooreplicate máquinas virtuales de Hyper-V administrados en el sitio secundario de tooa de nubes de System Center Virtual Machine Manager (VMM) local.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-108">Use this article if you want tooreplicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooa secondary site.</span></span>

<span data-ttu-id="a6b9d-109">Este artículo muestra cómo las tareas comunes de toouse PowerShell tooautomate necesita tooperform al configurar máquinas virtuales de Azure Site Recovery tooreplicate Hyper-V en nubes VMM de System Center VMM nubes tooSystem Center en el sitio secundario.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-109">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooSystem Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="a6b9d-110">Hola artículo incluye requisitos previos de escenario de Hola y muestra</span><span class="sxs-lookup"><span data-stu-id="a6b9d-110">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="a6b9d-111">¿Cómo tooset un almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="a6b9d-111">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="a6b9d-112">Instalar hello Azure Site Recovery Provider en el servidor VMM de origen de Hola y servidor VMM de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="a6b9d-112">Install hello Azure Site Recovery Provider on hello source VMM server and hello target VMM server</span></span>
* <span data-ttu-id="a6b9d-113">Registrar servidores VMM de hello en el almacén de Hola</span><span class="sxs-lookup"><span data-stu-id="a6b9d-113">Register hello VMM server(s) in hello vault</span></span>
* <span data-ttu-id="a6b9d-114">Configurar la directiva de replicación de hello nube de VMM.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-114">Configure replication policy for hello VMM Cloud.</span></span> <span data-ttu-id="a6b9d-115">configuración de replicación de Hello en la directiva de hello será aplicado tooall protegido las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a6b9d-115">hello replication settings in hello policy will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="a6b9d-116">Habilitar la protección de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-116">Enable protection for hello virtual machines.</span></span>
* <span data-ttu-id="a6b9d-117">Conmutación por error de prueba Hola de máquinas virtuales individualmente o como parte de una recuperación del plan toomake seguro de que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-117">Test hello failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>
* <span data-ttu-id="a6b9d-118">Realizar planeada o una conmutación por error no planeada de máquinas virtuales individualmente o como parte de una toomake del plan de recuperación que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>

<span data-ttu-id="a6b9d-119">Si experimenta problemas al configurar este escenario, publicar sus preguntas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-119">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="a6b9d-120">Azure tiene dos [modelos de implementación](../azure-resource-manager/resource-manager-deployment-model.md) diferentes para crear y utilizar recursos: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="a6b9d-121">Azure también tiene dos portales: Hola portal de Azure clásico que admite el modelo de implementación clásica de Hola y Hola portal de Azure con compatibilidad para dos modelos de implementación.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-121">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="a6b9d-122">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-122">This article covers hello Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="a6b9d-123">Requisitos previos locales</span><span class="sxs-lookup"><span data-stu-id="a6b9d-123">On-premises prerequisites</span></span>
<span data-ttu-id="a6b9d-124">Aquí es lo que necesitará en hello principal y secundaria local sitios toodeploy este escenario:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-124">Here's what you'll need in hello primary and secondary on-premises sites toodeploy this scenario:</span></span>

| <span data-ttu-id="a6b9d-125">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="a6b9d-125">**Prerequisites**</span></span> | <span data-ttu-id="a6b9d-126">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="a6b9d-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="a6b9d-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="a6b9d-127">**VMM**</span></span> |<span data-ttu-id="a6b9d-128">Se recomienda que implementar un servidor VMM en el sitio primario de Hola y un servidor VMM en el sitio secundario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-128">We recommend you deploy a VMM server in hello primary site and a VMM server in hello secondary site.</span></span><br/><br/> <span data-ttu-id="a6b9d-129">También puede [llevar a cabo una replicación entre nubes en un solo servidor VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="a6b9d-130">toodo Esto necesitará al menos dos nubes configuradas en el servidor VMM Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-130">toodo this you'll need at least two clouds configured on hello VMM server.</span></span><br/><br/> <span data-ttu-id="a6b9d-131">Servidores VMM se deben ejecutar al menos System Center 2012 SP1 con las últimas actualizaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-131">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="a6b9d-132">Cada servidor VMM debe tener uno o más nubes configuradas y todas las nubes deben tener perfil de capacidad de Hyper-V de hello establecido.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-132">Each VMM server must have at one or more clouds configured and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="a6b9d-133">Las nubes deben incluir uno o más grupos de hosts de VMM.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="a6b9d-134">Más información sobre la configuración de nubes VMM en [Hola configurar VMM en la nube tejido](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), y [Tutorial: crear nubes privadas con System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-134">Learn more about setting up VMM clouds in [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="a6b9d-135">Los servidores VMM deben tener acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="a6b9d-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="a6b9d-136">**Hyper-V**</span></span> |<span data-ttu-id="a6b9d-137">Servidores de Hyper-V deben ejecutar al menos Windows Server 2012 con el rol de Hyper-V de Hola y Hola a las últimas actualizaciones instaladas.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-137">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="a6b9d-138">Un servidor de Hyper-V debe contener una o varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="a6b9d-139">Servidores de host de Hyper-V deben estar en grupos host en nubes VMM principales y secundarias de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-139">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="a6b9d-140">Si está ejecutando Hyper-V en un clúster en Windows Server 2012 R2, debe instalar la [actualización 2961977](https://support.microsoft.com/kb/2961977).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="a6b9d-141">Si va a ejecutar Hyper-V en un clúster de Windows Server 2012, tenga en cuenta que el agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="a6b9d-142">Necesitará a un agente de clúster hello tooconfigure manualmente.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-142">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="a6b9d-143">[Más información](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="a6b9d-144">**Proveedor**</span><span class="sxs-lookup"><span data-stu-id="a6b9d-144">**Provider**</span></span> |<span data-ttu-id="a6b9d-145">Durante la implementación de Site Recovery se instale hello Azure Site Recovery Provider en servidores VMM.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-145">During Site Recovery deployment you install hello Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="a6b9d-146">Hola proveedor se comunica con Site Recovery a través de HTTPS 443 tooorchestrate replicación.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-146">hello Provider communicates with Site Recovery over HTTPS 443 tooorchestrate replication.</span></span> <span data-ttu-id="a6b9d-147">Se produce la replicación de datos entre Hola principales y secundarios Hyper-V servidores a través de hello LAN o una conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-147">Data replication occurs between hello primary and secondary Hyper-V servers over hello LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="a6b9d-148">Hello proveedor se ejecuta en el servidor VMM Hola necesita tener acceso a direcciones URL toothese: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-148">hello Provider running on hello VMM server needs access toothese URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="a6b9d-149">Además permite la comunicación de firewall de hello VMM servidores toohello [intervalos IP del centro de datos Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) y permitir que el protocolo de hello HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-149">In addition allow firewall communication from hello VMM servers toohello [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow hello HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="a6b9d-150">Requisitos previos de asignación de redes</span><span class="sxs-lookup"><span data-stu-id="a6b9d-150">Network mapping prerequisites</span></span>
<span data-ttu-id="a6b9d-151">Mapas de asignación de red entre redes de VM de VMM en servidores VMM de hello principales y secundarias para:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-151">Network mapping maps between VMM VM networks on hello primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="a6b9d-152">Colocar óptimamente las máquinas virtuales de réplica en los hosts de Hyper-V secundarios tras la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="a6b9d-153">Conectar redes de VM de tooappropriate de las máquinas virtuales de réplica.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-153">Connect replica VMs tooappropriate VM networks.</span></span>
* <span data-ttu-id="a6b9d-154">Si no configura la red asignación réplica máquinas virtuales no estarán conectada tooany red después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-154">If you don't configure network mapping replica VMs won't be connected tooany network after failover.</span></span>
* <span data-ttu-id="a6b9d-155">Si desea que tooset de red asignar durante la recuperación del sitio aquí la implementación es qué se necesita:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-155">If you want tooset up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="a6b9d-156">Asegúrese de que las máquinas virtuales en el origen de hello servidor host Hyper-V están conectado tooa red de VM de VMM.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-156">Make sure that VMs on hello source Hyper-V host server are connected tooa VMM VM network.</span></span> <span data-ttu-id="a6b9d-157">Esta red debe ser tooa vinculado red lógica que está asociado a la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-157">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
  * <span data-ttu-id="a6b9d-158">Compruebe que Hola secundaria en la nube que va a utilizar para la recuperación tiene configurada una red VM correspondiente.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-158">Verify that hello secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="a6b9d-159">Dicha red de máquina virtual debe ser tooa vinculado red lógica que esté asociada con la nube secundaria Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-159">That VM network should be linked tooa logical network that's associated with hello secondary cloud.</span></span>

<span data-ttu-id="a6b9d-160">Más información acerca de cómo configurar redes de VMM en hello debajo de artículos</span><span class="sxs-lookup"><span data-stu-id="a6b9d-160">Learn more about configuring VMM networks in hello below articles</span></span>

* [<span data-ttu-id="a6b9d-161">¿Cómo tooconfigure redes lógicas en VMM</span><span class="sxs-lookup"><span data-stu-id="a6b9d-161">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="a6b9d-162">¿Cómo tooconfigure VM redes y puertas de enlace en VMM</span><span class="sxs-lookup"><span data-stu-id="a6b9d-162">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="a6b9d-163">[Más información](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sobre cómo funciona la asignación de redes.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="a6b9d-164">Requisitos previos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6b9d-164">PowerShell prerequisites</span></span>
<span data-ttu-id="a6b9d-165">Asegúrese de que tiene listo toogo de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-165">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="a6b9d-166">Si ya usa PowerShell, deberá tooupgrade tooversion 0.8.10 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-166">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="a6b9d-167">Para obtener información acerca de cómo configurar PowerShell, vea hello [guía tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-167">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="a6b9d-168">Una vez que se instala y configura PowerShell, puede ver todos los cmdlets disponibles de hello para el servicio de Hola de [aquí](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-168">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="a6b9d-169">toolearn acerca de las sugerencias que pueden ayudarle a usar los cmdlets de hello, como cómo normalmente se controlan los valores de parámetro, las entradas y salidas en Azure PowerShell, vea hello [guía tooget iniciado con Cmdlets de Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-169">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="a6b9d-170">Paso 1: Configurar la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="a6b9d-170">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="a6b9d-171">De Azure powershell, inicio de sesión tooyour cuenta de Azure: mediante Hola después cmdlets</span><span class="sxs-lookup"><span data-stu-id="a6b9d-171">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="a6b9d-172">Obtenga una lista de las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="a6b9d-173">Esto mostrará también Hola identificadores de suscripción para cada una de las suscripciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-173">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="a6b9d-174">Anote subscriptionID Hola de suscripción de hello en el que desea que el almacén de servicios de recuperación de hello toocreate</span><span class="sxs-lookup"><span data-stu-id="a6b9d-174">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="a6b9d-175">Establecer suscripción hello en qué Hola almacén de servicios de recuperación es toobe creado por mencionar Hola Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="a6b9d-175">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="a6b9d-176">Paso 2: Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="a6b9d-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="a6b9d-177">Cree un grupo de recursos de Azure Resource Manager si todavía no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="a6b9d-178">Crear un nuevo almacén de servicios de recuperación y guardar Hola creado el objeto de almacén de ASR en una variable (se usará más adelante).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-178">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="a6b9d-179">También puede recuperar Hola ASR almacén post creación del objeto mediante el cmdlet Get-AzureRMRecoveryServicesVault Hola:-</span><span class="sxs-lookup"><span data-stu-id="a6b9d-179">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="a6b9d-180">Paso 3: Establecer contexto de almacén de servicios de recuperación de Hola</span><span class="sxs-lookup"><span data-stu-id="a6b9d-180">Step 3: Set hello Recovery Services Vault context</span></span>
1. <span data-ttu-id="a6b9d-181">Si tiene un almacén ya creado, ejecute hello debajo de almacén de comando tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-181">If you have a vault already created, run hello below command tooget hello vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="a6b9d-182">Establecer contexto de almacén de hello ejecutando Hola comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-182">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="a6b9d-183">Paso 4: Instalar hello Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="a6b9d-183">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="a6b9d-184">En la máquina VMM hello, cree un directorio ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-184">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="a6b9d-185">Extraiga los archivos de hello mediante el proveedor de hello descargado ejecutando el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="a6b9d-185">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="a6b9d-186">Instalar a proveedor de hello mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-186">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="a6b9d-187">Espere Hola instalación toofinish.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-187">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="a6b9d-188">Registrar servidor de hello en almacén de hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-188">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="a6b9d-189">Paso 5: Creación y asociación de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="a6b9d-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="a6b9d-190">Crear una directiva de replicación de Hyper-V 2012 R2 ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-190">Create a Hyper-V 2012 R2 replication policy by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="a6b9d-191">Hola nube de VMM puede contener hosts de Hyper-V que ejecutan versiones distintas de Windows Server (como se menciona en los requisitos previos de hello Hyper-V), pero la directiva de replicación de hello es específicos de la versión de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-191">hello VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in hello Hyper-V prerequisites), but hello replication policy is OS version specific.</span></span> <span data-ttu-id="a6b9d-192">Si tiene diferentes hosts que ejecutan diferentes versiones del sistema operativo, cree directivas de replicación independientes para cada tipo de versión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="a6b9d-193">Por ejemplo, si tiene 5 hosts que se ejecutan en Windows Servers 2012 y 3 en Windows Server 2012 R2, cree 2 directivas de replicación: una para cada tipo de versión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="a6b9d-194">Obtengan contenedor de protección primaria de hello (nube de VMM principal) y el contenedor de protección de recuperación (recuperación de nube de VMM) mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-194">Get hello primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running hello following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="a6b9d-195">Recuperar la directiva de Hola que creó en el paso 1 mediante nombre descriptivo de Hola de directiva de Hola</span><span class="sxs-lookup"><span data-stu-id="a6b9d-195">Retrieve hello policy you created in step 1 using hello friendly name of hello policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="a6b9d-196">Comience asociación Hola del contenedor de protección de hello (nube de VMM) con la directiva de replicación de hello:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-196">Start hello association of hello protection container (VMM Cloud) with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="a6b9d-197">Espere a que toocomplete de trabajo de asociación de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-197">Wait for hello policy association job toocomplete.</span></span> <span data-ttu-id="a6b9d-198">Puede comprobar si el trabajo de Hola se ha completado utilizando el siguiente fragmento de código de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-198">You can check if hello job has completed using hello following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="a6b9d-199">Después de que el trabajo de hello ha finalizado el procesamiento, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-199">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="a6b9d-200">finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-200">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="a6b9d-201">Paso 6: Configuración de la asignación de red</span><span class="sxs-lookup"><span data-stu-id="a6b9d-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="a6b9d-202">Hola primer comando obtiene servidores de almacén de Azure Site Recovery de hello actual.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-202">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="a6b9d-203">comando Hello almacena servidores de Microsoft Azure Site Recovery de hello en la variable de matriz de hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-203">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="a6b9d-204">Hola por debajo de los comandos obtener red de recuperación de sitio de hello para el servidor VMM de origen de Hola y servidor VMM de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-204">hello below commands get hello site recovery network for hello source VMM server and hello target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="a6b9d-205">servidor VMM de origen de Hello puede ser Hola primera o segunda matriz de servidores de un saludo en hello.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-205">hello source VMM server can be hello first one or hello second one in hello servers array.</span></span> <span data-ttu-id="a6b9d-206">Comprobar los nombres de Hola Hola de servidores de VMM y obtener redes Hola correctamente</span><span class="sxs-lookup"><span data-stu-id="a6b9d-206">Check hello names of hello VMM servers and get hello networks appropriately</span></span>


1. <span data-ttu-id="a6b9d-207">Hola final cmdlet crea una asignación entre la red principal de Hola y red de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-207">hello final cmdlet creates a mapping between hello primary network and hello recovery network.</span></span> <span data-ttu-id="a6b9d-208">Hola cmdlet especifica red principal de hello como primer elemento de Hola de red de recuperación $PrimaryNetworks y hello como primer elemento de Hola de $RecoveryNetworks.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-208">hello cmdlet specifies hello primary network as hello first element of $PrimaryNetworks and hello recovery network as hello first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="a6b9d-209">Paso 7: Configuración de la asignación de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a6b9d-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="a6b9d-210">Hola comando siguiente obtiene la lista de Hola de clasificaciones de almacenamiento en la variable $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-210">hello below command gets hello list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="a6b9d-211">Hola por debajo de los comandos obtener la clasificación de origen de hello en $SourceClassificaion variable y la clasificación de destino en la variable $TargetClassification.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-211">hello below commands get hello source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="a6b9d-212">clasificaciones de origen y destino de Hello pueden ser cualquier elemento de matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-212">hello source and target classifications can be any element in hello array.</span></span> <span data-ttu-id="a6b9d-213">Consulte toohello salida de hello debajo de índice del comando toofigure Hola de clasificaciones de origen y destino de matriz $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-213">Refer toohello output of hello below command toofigure hello index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="a6b9d-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="a6b9d-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="a6b9d-215">Hola siguiente cmdlet crea una asignación entre la clasificación de origen de Hola y clasificación de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-215">hello below cmdlet creates a mapping between hello source classification and hello target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="a6b9d-216">Paso 8: Habilitación de la protección para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a6b9d-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="a6b9d-217">Después de redes, las nubes y servidores de hello están configuradas correctamente, puede habilitar la protección de máquinas virtuales en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-217">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

1. <span data-ttu-id="a6b9d-218">protección de tooenable, ejecute hello después de contenedor de protección de hello tooget de comando:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-218">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="a6b9d-219">Obtener la entidad de protección de hello (VM) mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-219">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="a6b9d-220">Habilitar la replicación de hello VM mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-220">Enable replication for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="a6b9d-221">Prueba de la implementación</span><span class="sxs-lookup"><span data-stu-id="a6b9d-221">Test your deployment</span></span>
<span data-ttu-id="a6b9d-222">plan de la implementación, puede ejecutar una prueba de conmutación por error para una sola máquina virtual, o crear un plan de recuperación que consta de varias máquinas virtuales y ejecutar una prueba de conmutación por error para hello tootest.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-222">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="a6b9d-223">La conmutación por error de prueba simula su mecanismo de conmutación por error y recuperación en una red aislada.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="a6b9d-224">Puede crear un plan de recuperación para su aplicación en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="a6b9d-225">finalización de hello toocheck de operación de hello, siga los pasos de hello en [supervisar la actividad](#monitor).</span><span class="sxs-lookup"><span data-stu-id="a6b9d-225">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="a6b9d-226">Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="a6b9d-226">Run a test failover</span></span>
1. <span data-ttu-id="a6b9d-227">Ejecute hello debajo toowhich de red VM de cmdlets tooget Hola desea tootest conmutación por error las máquinas virtuales se.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-227">Run hello below cmdlets tooget hello VM network toowhich you want tootest failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="a6b9d-228">Realizar una conmutación por error de prueba de una máquina virtual haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-228">Perform a test failover of a VM by doing hello following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="a6b9d-229">Realizar una conmutación por error de prueba de un plan de recuperación haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-229">Perform a test failover of a recovery plan by doing hello following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="a6b9d-230">Ejecución de una conmutación por error planeada</span><span class="sxs-lookup"><span data-stu-id="a6b9d-230">Run a planned failover</span></span>
1. <span data-ttu-id="a6b9d-231">Realizar una conmutación por error planeada de una máquina virtual haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-231">Perform a planned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="a6b9d-232">Realizar una conmutación por error planeada de un plan de recuperación haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-232">Perform a planned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="a6b9d-233">Ejecución de una conmutación por error no planeada</span><span class="sxs-lookup"><span data-stu-id="a6b9d-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="a6b9d-234">Realizar una conmutación por error no planeada de una máquina virtual haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-234">Perform an unplanned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="a6b9d-235">2. realizar una conmutación por error no planeada de un plan de recuperación haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6b9d-235">2.Perform an unplanned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="a6b9d-236"><a name=monitor></a> Supervisión de la actividad</span><span class="sxs-lookup"><span data-stu-id="a6b9d-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="a6b9d-237">Usar hello después de la actividad de hello toomonitor de comandos.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-237">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="a6b9d-238">Tenga en cuenta que tiene toowait entre los trabajos de hello toofinish de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-238">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="a6b9d-239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a6b9d-239">Next steps</span></span>
<span data-ttu-id="a6b9d-240">[Más información](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre los cmdlets de PowerShell de Azure Site Recovery con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a6b9d-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
