---
title: "Replicación de máquinas virtuales de Hyper-V en VMM en un sitio secundario con PowerShell (Azure Resource Manager) | Microsoft Docs"
description: "En este artículo se describe cómo implementar Azure Site Recovery para organizar la replicación, la conmutación por error y la recuperación de máquinas virtuales Hyper-V de nubes VMM en un sitio VMM secundario mediante PowerShell (Resource Manager)."
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
ms.openlocfilehash: 5a6e00877b0a2b139d5322f610c1901ad76a710f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="95d6c-103">Replicación de máquinas virtuales Hyper-V de nubes VMM en un sitio VMM secundario mediante PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="95d6c-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95d6c-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="95d6c-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="95d6c-105">Portal clásico</span><span class="sxs-lookup"><span data-stu-id="95d6c-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="95d6c-106">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="95d6c-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="95d6c-107">Bienvenido a Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="95d6c-107">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="95d6c-108">Utilice este artículo si quiere replicar máquinas virtuales locales de Hyper-V administradas en nubes de System Center Virtual Machine Manager (VMM) en un sitio secundario.</span><span class="sxs-lookup"><span data-stu-id="95d6c-108">Use this article if you want to replicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to a secondary site.</span></span>

<span data-ttu-id="95d6c-109">En este artículo se muestra cómo usar PowerShell para automatizar las tareas comunes que debe realizar al configurar Azure Site Recovery para replicar máquinas virtuales Hyper-V de nubes VMM de System Center en nubes del mismo tipo del sitio secundario.</span><span class="sxs-lookup"><span data-stu-id="95d6c-109">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to System Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="95d6c-110">El artículo incluye los requisitos previos para el escenario y muestra</span><span class="sxs-lookup"><span data-stu-id="95d6c-110">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="95d6c-111">Configuración del almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="95d6c-111">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="95d6c-112">Instalar el proveedor de Azure Site Recovery en los servidores VMM de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="95d6c-112">Install the Azure Site Recovery Provider on the source VMM server and the target VMM server</span></span>
* <span data-ttu-id="95d6c-113">Registrar los servidores VMM en el almacén.</span><span class="sxs-lookup"><span data-stu-id="95d6c-113">Register the VMM server(s) in the vault</span></span>
* <span data-ttu-id="95d6c-114">Configurar la directiva de replicación para la nube VMM.</span><span class="sxs-lookup"><span data-stu-id="95d6c-114">Configure replication policy for the VMM Cloud.</span></span> <span data-ttu-id="95d6c-115">La configuración de replicación de la directiva se aplicará a todas las máquinas virtuales protegidas.</span><span class="sxs-lookup"><span data-stu-id="95d6c-115">The replication settings in the policy will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="95d6c-116">Habilitar la protección en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="95d6c-116">Enable protection for the virtual machines.</span></span>
* <span data-ttu-id="95d6c-117">Probar la conmutación por error de máquinas virtuales de manera individual o como parte de un plan de recuperación para garantizar que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="95d6c-117">Test the failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>
* <span data-ttu-id="95d6c-118">Realizar una conmutación por error (planeada o no planeada) de máquinas virtuales de manera individual o como parte de un plan de recuperación para garantizar todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="95d6c-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>

<span data-ttu-id="95d6c-119">Si tiene problemas al configurar este escenario, publique sus preguntas en el [Foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="95d6c-119">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="95d6c-120">Azure tiene dos [modelos de implementación](../azure-resource-manager/resource-manager-deployment-model.md) diferentes para crear y utilizar recursos: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="95d6c-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="95d6c-121">Azure también tiene dos portales: el Portal de Azure clásico que admite el modelo de implementación clásico y el Portal de Azure que es compatible con ambos modelos de implementación.</span><span class="sxs-lookup"><span data-stu-id="95d6c-121">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="95d6c-122">Este artículo trata sobre el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="95d6c-122">This article covers the Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="95d6c-123">Requisitos previos locales</span><span class="sxs-lookup"><span data-stu-id="95d6c-123">On-premises prerequisites</span></span>
<span data-ttu-id="95d6c-124">Esto es lo que necesita tener en los sitios locales principal y secundario para implementar este escenario:</span><span class="sxs-lookup"><span data-stu-id="95d6c-124">Here's what you'll need in the primary and secondary on-premises sites to deploy this scenario:</span></span>

| <span data-ttu-id="95d6c-125">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="95d6c-125">**Prerequisites**</span></span> | <span data-ttu-id="95d6c-126">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="95d6c-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="95d6c-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="95d6c-127">**VMM**</span></span> |<span data-ttu-id="95d6c-128">Se recomienda implementar un servidor VMM en el sitio principal y otro del mismo tipo en el secundario.</span><span class="sxs-lookup"><span data-stu-id="95d6c-128">We recommend you deploy a VMM server in the primary site and a VMM server in the secondary site.</span></span><br/><br/> <span data-ttu-id="95d6c-129">También puede [llevar a cabo una replicación entre nubes en un solo servidor VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="95d6c-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="95d6c-130">Para ello, necesitará, al menos, dos nubes configuradas en el servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="95d6c-130">To do this you'll need at least two clouds configured on the VMM server.</span></span><br/><br/> <span data-ttu-id="95d6c-131">Los servidores VMM deben estar ejecutando, como mínimo, System Center 2012 SP1 con las actualizaciones más recientes.</span><span class="sxs-lookup"><span data-stu-id="95d6c-131">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span></span><br/><br/> <span data-ttu-id="95d6c-132">Cada servidor VMM debe tener una o más nubes configuradas y todas las nubes deben tener definido el perfil de capacidad de Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="95d6c-132">Each VMM server must have at one or more clouds configured and all clouds must have the Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="95d6c-133">Las nubes deben incluir uno o más grupos de hosts de VMM.</span><span class="sxs-lookup"><span data-stu-id="95d6c-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="95d6c-134">Aprenda a configurar nubes de VMM en [Configuración del tejido de nube de VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric) y [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx) (Tutorial: Creación de nubes privadas con System Center 2012 SP1 VMM).</span><span class="sxs-lookup"><span data-stu-id="95d6c-134">Learn more about setting up VMM clouds in [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="95d6c-135">Los servidores VMM deben tener acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="95d6c-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="95d6c-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="95d6c-136">**Hyper-V**</span></span> |<span data-ttu-id="95d6c-137">Los servidores Hyper-V deben estar ejecutando, como mínimo, Windows Server 2012 con el rol Hyper-V y tener instaladas las actualizaciones más recientes.</span><span class="sxs-lookup"><span data-stu-id="95d6c-137">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role and have the latest updates installed.</span></span><br/><br/> <span data-ttu-id="95d6c-138">Un servidor de Hyper-V debe contener una o varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="95d6c-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="95d6c-139">Los servidores host de Hyper-V deben estar ubicados en grupos host de las nubes de VMM principal y secundaria.</span><span class="sxs-lookup"><span data-stu-id="95d6c-139">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="95d6c-140">Si está ejecutando Hyper-V en un clúster en Windows Server 2012 R2, debe instalar la [actualización 2961977](https://support.microsoft.com/kb/2961977).</span><span class="sxs-lookup"><span data-stu-id="95d6c-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="95d6c-141">Si va a ejecutar Hyper-V en un clúster de Windows Server 2012, tenga en cuenta que el agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="95d6c-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="95d6c-142">Tendrá que configurar manualmente el agente de clúster.</span><span class="sxs-lookup"><span data-stu-id="95d6c-142">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="95d6c-143">[Más información](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="95d6c-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="95d6c-144">**Proveedor**</span><span class="sxs-lookup"><span data-stu-id="95d6c-144">**Provider**</span></span> |<span data-ttu-id="95d6c-145">Durante la implementación de Site Recovery, se instala el proveedor de Azure Site Recovery en los servidores VMM.</span><span class="sxs-lookup"><span data-stu-id="95d6c-145">During Site Recovery deployment you install the Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="95d6c-146">El proveedor se comunica con Site Recovery mediante HTTPS 443 para organizar la replicación.</span><span class="sxs-lookup"><span data-stu-id="95d6c-146">The Provider communicates with Site Recovery over HTTPS 443 to orchestrate replication.</span></span> <span data-ttu-id="95d6c-147">La replicación de datos se produce entre los servidores Hyper-V principal y secundario mediante la conexión LAN o VPN.</span><span class="sxs-lookup"><span data-stu-id="95d6c-147">Data replication occurs between the primary and secondary Hyper-V servers over the LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="95d6c-148">El proveedor que se ejecuta en el servidor VMM necesita acceso a estas direcciones URL: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="95d6c-148">The Provider running on the VMM server needs access to these URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="95d6c-149">Además, hay que permitir tanto la comunicación del firewall entre los servidores VMM y los [intervalos IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) como el protocolo HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="95d6c-149">In addition allow firewall communication from the VMM servers to the [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow the HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="95d6c-150">Requisitos previos de asignación de redes</span><span class="sxs-lookup"><span data-stu-id="95d6c-150">Network mapping prerequisites</span></span>
<span data-ttu-id="95d6c-151">La asignación de red se realiza entre las redes de VM de VMM en los servidores VMM principal y secundario con el fin de:</span><span class="sxs-lookup"><span data-stu-id="95d6c-151">Network mapping maps between VMM VM networks on the primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="95d6c-152">Colocar óptimamente las máquinas virtuales de réplica en los hosts de Hyper-V secundarios tras la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="95d6c-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="95d6c-153">Conectar las máquinas virtuales de réplica a las redes VM adecuadas.</span><span class="sxs-lookup"><span data-stu-id="95d6c-153">Connect replica VMs to appropriate VM networks.</span></span>
* <span data-ttu-id="95d6c-154">Si no configura la asignación de red, las máquinas virtuales de réplica no se conectarán a ninguna red tras la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="95d6c-154">If you don't configure network mapping replica VMs won't be connected to any network after failover.</span></span>
* <span data-ttu-id="95d6c-155">Si quiere configurar la asignación de red durante la implementación de Site Recovery, esto es lo que debe hacer:</span><span class="sxs-lookup"><span data-stu-id="95d6c-155">If you want to set up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="95d6c-156">Asegúrese de que las máquinas virtuales del servidor host de Hyper-V de origen estén conectadas a una red de máquinas virtuales de VMM.</span><span class="sxs-lookup"><span data-stu-id="95d6c-156">Make sure that VMs on the source Hyper-V host server are connected to a VMM VM network.</span></span> <span data-ttu-id="95d6c-157">Esa red debe estar vinculada a una red lógica asociada con la nube.</span><span class="sxs-lookup"><span data-stu-id="95d6c-157">That network should be linked to a logical network that is associated with the cloud.</span></span>
  * <span data-ttu-id="95d6c-158">Compruebe que la nube secundaria que se va a utilizar para la recuperación tenga configurada una red de VM correspondiente.</span><span class="sxs-lookup"><span data-stu-id="95d6c-158">Verify that the secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="95d6c-159">Dicha red de máquina virtual debe estar vinculada a una red lógica asociada con la nube secundaria.</span><span class="sxs-lookup"><span data-stu-id="95d6c-159">That VM network should be linked to a logical network that's associated with the secondary cloud.</span></span>

<span data-ttu-id="95d6c-160">Puede encontrar información sobre cómo configurar redes VMM en los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="95d6c-160">Learn more about configuring VMM networks in the below articles</span></span>

* [<span data-ttu-id="95d6c-161">Configuración de redes lógicas en VMM</span><span class="sxs-lookup"><span data-stu-id="95d6c-161">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="95d6c-162">Configuración de redes de máquina virtual y puertas de enlace en VMM</span><span class="sxs-lookup"><span data-stu-id="95d6c-162">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="95d6c-163">[más información](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sobre cómo funciona la asignación de red.</span><span class="sxs-lookup"><span data-stu-id="95d6c-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="95d6c-164">Requisitos previos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="95d6c-164">PowerShell prerequisites</span></span>
<span data-ttu-id="95d6c-165">Asegúrese de que tiene Azure PowerShell listo para usar.</span><span class="sxs-lookup"><span data-stu-id="95d6c-165">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="95d6c-166">Si ya usa PowerShell, necesitará actualizar a la versión 0.8.10 o posterior.</span><span class="sxs-lookup"><span data-stu-id="95d6c-166">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="95d6c-167">Para obtener más información sobre cómo configurar PowerShell, lea la [guía para instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="95d6c-167">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="95d6c-168">Una vez que haya configurado PowerShell, puede ver todos los cmdlets disponibles para el servicio [aquí](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="95d6c-168">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="95d6c-169">Para ver sugerencias que puedan ayudarlo a usar los cmdlets —por ejemplo, cómo se controlan normalmente los valores de parámetro, las entradas y las salidas en Azure PowerShell—, lea la [guía de introducción a los cmdlets de Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="95d6c-169">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="95d6c-170">Paso 1: Establecimiento de la suscripción</span><span class="sxs-lookup"><span data-stu-id="95d6c-170">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="95d6c-171">Desde Azure PowerShell, inicie sesión en la cuenta de Azure mediante los siguientes cmdlets</span><span class="sxs-lookup"><span data-stu-id="95d6c-171">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="95d6c-172">Obtenga una lista de las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="95d6c-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="95d6c-173">También mostrará los identificadores de suscripción de cada una de las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="95d6c-173">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="95d6c-174">Anotación del identificador de suscripción de la suscripción en la que desea crear el almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="95d6c-174">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="95d6c-175">Establecimiento de la suscripción en la que se va a crear el almacén de Servicios de recuperación mediante la mención del identificador de suscripción</span><span class="sxs-lookup"><span data-stu-id="95d6c-175">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="95d6c-176">Paso 2: Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="95d6c-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="95d6c-177">Cree un grupo de recursos de Azure Resource Manager si todavía no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="95d6c-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="95d6c-178">Cree un almacén de Servicios de recuperación y guarde el objeto de almacén de ASR creado en una variable (se utilizará más adelante).</span><span class="sxs-lookup"><span data-stu-id="95d6c-178">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="95d6c-179">También puede recuperar el objeto de almacén de ASR tras la creación con el cmdlet Get-AzureRMRecoveryServicesVault:-</span><span class="sxs-lookup"><span data-stu-id="95d6c-179">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="95d6c-180">Paso 3: Configuración del contexto de almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="95d6c-180">Step 3: Set the Recovery Services Vault context</span></span>
1. <span data-ttu-id="95d6c-181">Si ya ha creado un almacén, ejecute el siguiente comando para obtenerlo.</span><span class="sxs-lookup"><span data-stu-id="95d6c-181">If you have a vault already created, run the below command to get the vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="95d6c-182">Establezca el contexto de almacén mediante la ejecución del comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="95d6c-182">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="95d6c-183">Paso 4: Instalación del proveedor de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="95d6c-183">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="95d6c-184">En el equipo VMM, cree un directorio ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="95d6c-184">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="95d6c-185">Extraiga los archivos mediante el proveedor descargado ejecutando comando siguiente</span><span class="sxs-lookup"><span data-stu-id="95d6c-185">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="95d6c-186">Instale el proveedor mediante los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="95d6c-186">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="95d6c-187">Espere hasta que la instalación se complete.</span><span class="sxs-lookup"><span data-stu-id="95d6c-187">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="95d6c-188">Registre el servidor en el almacén con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="95d6c-188">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="95d6c-189">Paso 5: Creación y asociación de una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="95d6c-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="95d6c-190">Cree una directiva de replicación en Hyper-V 2012 R2 ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="95d6c-190">Create a Hyper-V 2012 R2 replication policy by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify the number of hours to retain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify the frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify the port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="95d6c-191">La nube VMM puede contener hosts Hyper-V que ejecuten versiones distintas de Windows Server (tal y como se mencionó en los requisitos previos de Hyper-V), pero la directiva de replicación es específica de la versión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="95d6c-191">The VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in the Hyper-V prerequisites), but the replication policy is OS version specific.</span></span> <span data-ttu-id="95d6c-192">Si tiene diferentes hosts que ejecutan diferentes versiones del sistema operativo, cree directivas de replicación independientes para cada tipo de versión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="95d6c-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="95d6c-193">Por ejemplo, si tiene 5 hosts que se ejecutan en Windows Servers 2012 y 3 en Windows Server 2012 R2, cree 2 directivas de replicación: una para cada tipo de versión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="95d6c-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="95d6c-194">Obtenga el contenedor de protección principal (nube VMM principal) y el de recuperación (nube VMM de recuperación) ejecutando los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="95d6c-194">Get the primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running the following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="95d6c-195">Recupere la directiva que creó en el paso 1 usando su nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="95d6c-195">Retrieve the policy you created in step 1 using the friendly name of the policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="95d6c-196">Inicie la asociación del contenedor de protección (nube VMM) con la directiva de replicación:</span><span class="sxs-lookup"><span data-stu-id="95d6c-196">Start the association of the protection container (VMM Cloud) with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="95d6c-197">Espere a que finalice el trabajo de asociación de directivas.</span><span class="sxs-lookup"><span data-stu-id="95d6c-197">Wait for the policy association job to complete.</span></span> <span data-ttu-id="95d6c-198">Puede comprobar si se ha completado el trabajo ejecutando el siguiente fragmento de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95d6c-198">You can check if the job has completed using the following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="95d6c-199">Cuando haya finalizado el procesamiento, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="95d6c-199">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="95d6c-200">Para comprobar la finalización de la operación, siga los pasos en [Supervisión de la actividad](#monitor).</span><span class="sxs-lookup"><span data-stu-id="95d6c-200">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="95d6c-201">Paso 6: Configuración de la asignación de red</span><span class="sxs-lookup"><span data-stu-id="95d6c-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="95d6c-202">El primer comando obtiene los servidores para el almacén actual de Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="95d6c-202">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="95d6c-203">El comando almacena los servidores de Microsoft Azure Site Recovery en la variable de matriz $Servers.</span><span class="sxs-lookup"><span data-stu-id="95d6c-203">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="95d6c-204">Con los siguientes comandos se obtiene la red de recuperación del sitio para los servidores VMM de origen y de destino.</span><span class="sxs-lookup"><span data-stu-id="95d6c-204">The below commands get the site recovery network for the source VMM server and the target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="95d6c-205">El servidor VMM de origen puede ser el primero o el segundo en la matriz de servidores.</span><span class="sxs-lookup"><span data-stu-id="95d6c-205">The source VMM server can be the first one or the second one in the servers array.</span></span> <span data-ttu-id="95d6c-206">Compruebe los nombres de los servidores VMM y obtenga las redes de forma apropiada.</span><span class="sxs-lookup"><span data-stu-id="95d6c-206">Check the names of the VMM servers and get the networks appropriately</span></span>


1. <span data-ttu-id="95d6c-207">El cmdlet final crea una asignación entre la red principal y la de recuperación.</span><span class="sxs-lookup"><span data-stu-id="95d6c-207">The final cmdlet creates a mapping between the primary network and the recovery network.</span></span> <span data-ttu-id="95d6c-208">El cmdlet especifica la red principal como primer elemento de $PrimaryNetworks y la de recuperación como primer elemento de $RecoveryNetworks.</span><span class="sxs-lookup"><span data-stu-id="95d6c-208">The cmdlet specifies the primary network as the first element of $PrimaryNetworks and the recovery network as the first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="95d6c-209">Paso 7: Configuración de la asignación de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="95d6c-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="95d6c-210">El comando siguiente introduce la lista de clasificaciones de almacenamiento en la variable $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="95d6c-210">The below command gets the list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="95d6c-211">Los siguientes comandos introducen la clasificación de origen en la variable $SourceClassification y la de destino en $TargetClassification.</span><span class="sxs-lookup"><span data-stu-id="95d6c-211">The below commands get the source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="95d6c-212">Las clasificaciones de origen y de destino pueden ser cualquier elemento de la matriz.</span><span class="sxs-lookup"><span data-stu-id="95d6c-212">The source and target classifications can be any element in the array.</span></span> <span data-ttu-id="95d6c-213">Consulte el resultado del siguiente comando para calcular el índice de clasificaciones de origen y destino de la matriz $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="95d6c-213">Refer to the output of the below command to figure the index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="95d6c-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="95d6c-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="95d6c-215">El siguiente cmdlet crea una asignación entre la clasificación de origen y la de destino.</span><span class="sxs-lookup"><span data-stu-id="95d6c-215">The below cmdlet creates a mapping between the source classification and the target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="95d6c-216">Paso 8: Habilitación de la protección para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="95d6c-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="95d6c-217">Una vez configurados correctamente los servidores, las nubes y las redes, puede habilitar la protección para las máquinas virtuales en la nube.</span><span class="sxs-lookup"><span data-stu-id="95d6c-217">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

1. <span data-ttu-id="95d6c-218">Para habilitar la protección, ejecute el siguiente comando para obtener el contenedor de protección:</span><span class="sxs-lookup"><span data-stu-id="95d6c-218">To enable protection, run the following command to get the protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="95d6c-219">Obtenga una entidad de protección (VM) ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95d6c-219">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="95d6c-220">Habilite la replicación de la máquina virtual ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="95d6c-220">Enable replication for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="95d6c-221">Prueba de la implementación</span><span class="sxs-lookup"><span data-stu-id="95d6c-221">Test your deployment</span></span>
<span data-ttu-id="95d6c-222">Para probar la implementación puede realizar una prueba de conmutación por error para una máquina virtual individual o crear un plan de recuperación que incluya numerosas máquinas virtuales y realizar una conmutación por error de prueba para el plan.</span><span class="sxs-lookup"><span data-stu-id="95d6c-222">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="95d6c-223">La conmutación por error de prueba simula su mecanismo de conmutación por error y recuperación en una red aislada.</span><span class="sxs-lookup"><span data-stu-id="95d6c-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="95d6c-224">Puede crear un plan de recuperación para su aplicación en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="95d6c-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="95d6c-225">Para comprobar la finalización de la operación, siga los pasos en [Supervisión de la actividad](#monitor).</span><span class="sxs-lookup"><span data-stu-id="95d6c-225">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="95d6c-226">Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="95d6c-226">Run a test failover</span></span>
1. <span data-ttu-id="95d6c-227">Ejecute los siguientes cmdlets para obtener la red de máquina virtual en la que quiere probar la conmutación por error a sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="95d6c-227">Run the below cmdlets to get the VM network to which you want to test failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="95d6c-228">Realice una conmutación por error de prueba de una máquina virtual ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="95d6c-228">Perform a test failover of a VM by doing the following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="95d6c-229">Realice una conmutación por error de prueba de un plan de recuperación ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="95d6c-229">Perform a test failover of a recovery plan by doing the following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="95d6c-230">Ejecución de una conmutación por error planeada</span><span class="sxs-lookup"><span data-stu-id="95d6c-230">Run a planned failover</span></span>
1. <span data-ttu-id="95d6c-231">Realice una conmutación por error planeada de una máquina virtual ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="95d6c-231">Perform a planned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="95d6c-232">Realice una conmutación por error planeada de un plan de recuperación ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="95d6c-232">Perform a planned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="95d6c-233">Ejecución de una conmutación por error no planeada</span><span class="sxs-lookup"><span data-stu-id="95d6c-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="95d6c-234">Realice una conmutación por error no planeada de una máquina virtual ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="95d6c-234">Perform an unplanned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="95d6c-235">2. Realice una conmutación por error no planeada de un plan de recuperación ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="95d6c-235">2.Perform an unplanned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="95d6c-236"><a name=monitor></a> Supervisión de la actividad</span><span class="sxs-lookup"><span data-stu-id="95d6c-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="95d6c-237">Utilice los comandos siguientes para supervisar la actividad.</span><span class="sxs-lookup"><span data-stu-id="95d6c-237">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="95d6c-238">Tenga en cuenta que debe esperar entre los trabajos para que el procesamiento finalice.</span><span class="sxs-lookup"><span data-stu-id="95d6c-238">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="95d6c-239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95d6c-239">Next steps</span></span>
<span data-ttu-id="95d6c-240">[Más información](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre los cmdlets de PowerShell de Azure Site Recovery con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="95d6c-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
