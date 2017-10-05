---
title: "Replicación de aplicaciones (Azure en Azure) | Microsoft Docs"
description: "En este artículo se explica cómo configurar la replicación de máquinas virtuales que se ejecutan en una región de Azure en otra región de Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: f9f97cf840b722c8cfee169dd1640e0682f287ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-virtual-machines-to-another-azure-region"></a><span data-ttu-id="38ad9-103">Replicación de máquinas virtuales de Azure en otra región de Azure</span><span class="sxs-lookup"><span data-stu-id="38ad9-103">Replicate Azure virtual machines to another Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="38ad9-104">La replicación de Site Recovery para máquinas virtuales de Azure está actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="38ad9-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="38ad9-105">En este artículo se explica cómo configurar la replicación de máquinas virtuales que se ejecutan en una región de Azure en otra región de Azure.</span><span class="sxs-lookup"><span data-stu-id="38ad9-105">This article describes how to set up replication of virtual machines running in one Azure region to another Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38ad9-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="38ad9-106">Prerequisites</span></span>

* <span data-ttu-id="38ad9-107">El artículo da por hecho que ya conoce Site Recovery y el almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="38ad9-107">The article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="38ad9-108">Es necesario haber creado de antemano un "almacén de Recovery Services".</span><span class="sxs-lookup"><span data-stu-id="38ad9-108">You need to have a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="38ad9-109">Se recomienda crear el "almacén de Recovery Services" en la ubicación donde quiere que se repliquen las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="38ad9-109">It is recommended that you create the 'Recovery services vault' in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="38ad9-110">Por ejemplo, si la ubicación de destino es "Centro de EE. UU.", cree el almacén en "Centro de EE. UU.".</span><span class="sxs-lookup"><span data-stu-id="38ad9-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="38ad9-111">Si usa reglas de grupos de seguridad de red (NSG) o proxy de firewall para controlar el acceso a la conectividad saliente de Internet en las máquinas virtuales de Azure, asegúrese de incluir en la lista blanca las direcciones URL o IP necesarias.</span><span class="sxs-lookup"><span data-stu-id="38ad9-111">If you are using Network Security Groups (NSG) rules or firewall proxy to control access to outbound internet connectivity on the Azure VMs, ensure that you whitelist the required URLs or IPs.</span></span> <span data-ttu-id="38ad9-112">Vea el [documento de instrucciones de redes](./site-recovery-azure-to-azure-networking-guidance.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="38ad9-112">Refer to [Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="38ad9-113">Si tiene una conexión ExpressRoute o VPN entre la ubicación local y de origen en Azure, siga el documento [Site Recovery Considerations for Azure to on-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) (Consideraciones de Site Recovery para Azure para la configuración local de ExpressRoute o VPN).</span><span class="sxs-lookup"><span data-stu-id="38ad9-113">If you have an ExpressRoute or a VPN connection between on-premises and the source location in Azure, follow [Site Recovery Considerations for Azure to on-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="38ad9-114">La cuenta de usuario de Azure debe tener ciertos [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) para habilitar la replicación de una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="38ad9-114">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="38ad9-115">La suscripción de Azure debe estar habilitada para crear máquinas virtuales en la ubicación de destino que quiere usar como región de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="38ad9-115">Your Azure subscription should be enabled to create VMs in the target location you want to use as DR region.</span></span> <span data-ttu-id="38ad9-116">Puede ponerse en contacto con el soporte técnico para habilitar la cuota necesaria.</span><span class="sxs-lookup"><span data-stu-id="38ad9-116">You can contact support to enable the required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="38ad9-117">Habilitar la replicación desde el almacén de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="38ad9-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="38ad9-118">En este ejemplo se replicarán máquinas virtuales en ejecución en la ubicación "Asia Oriental" de Azure en la ubicación "Asia Suroriental".</span><span class="sxs-lookup"><span data-stu-id="38ad9-118">For this illustration, we will replicate VMs running  in the ‘East Asia’ Azure location to the ‘South East Asia’ location.</span></span> <span data-ttu-id="38ad9-119">Los pasos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="38ad9-119">The steps are as follows:</span></span>

 <span data-ttu-id="38ad9-120">Haga clic en **+Replicar** en el almacén para habilitar la replicación de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="38ad9-120">Click **+Replicate** in the vault to enable replication for the virtual machines.</span></span>

1. <span data-ttu-id="38ad9-121">**Origen:** hace referencia al punto de origen de las máquinas, que en este caso es **Azure**.</span><span class="sxs-lookup"><span data-stu-id="38ad9-121">**Source:** It refers to the point of origin of the machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="38ad9-122">**Ubicación de origen:** es la región de Azure desde la que se quieren proteger las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="38ad9-122">**Source location:** It is the Azure region from where you want to protect your virtual machines.</span></span> <span data-ttu-id="38ad9-123">En este ejemplo, la ubicación de origen será "Asia Oriental"</span><span class="sxs-lookup"><span data-stu-id="38ad9-123">For this illustration, the source location will be 'East Asia'</span></span>

3. <span data-ttu-id="38ad9-124">**Modelo de implementación:** hace referencia al modelo de implementación de Azure de las máquinas de origen.</span><span class="sxs-lookup"><span data-stu-id="38ad9-124">**Deployment model:** It refers to the Azure deployment model of the source machines.</span></span> <span data-ttu-id="38ad9-125">Puede seleccionar clásicas o de Resource Manager y las máquinas que pertenezcan al modelo en cuestión se enumerarán para su protección en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="38ad9-125">You can select either classic or resource manager and machines belonging to the specific model will be listed for protection in the next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="38ad9-126">Solo puede replicar una máquina virtual clásica y recuperarla como máquina virtual clásica.</span><span class="sxs-lookup"><span data-stu-id="38ad9-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="38ad9-127">No puede recuperarla como máquina virtual de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="38ad9-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="38ad9-128">**Grupo de recursos:** es el grupo de recursos al que pertenecen las máquinas virtuales de origen.</span><span class="sxs-lookup"><span data-stu-id="38ad9-128">**Resource Group:** It’s the resource group to which your source virtual machines belong.</span></span> <span data-ttu-id="38ad9-129">Todas las máquinas virtuales del grupo de recursos seleccionado se enumerarán para su protección en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="38ad9-129">All the VMs under the selected resource group will be listed for protection in the next step.</span></span>

    ![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="38ad9-131">En **Máquinas virtuales > Seleccionar máquinas virtuales**, haga clic en cada máquina que quiera replicar y selecciónela.</span><span class="sxs-lookup"><span data-stu-id="38ad9-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="38ad9-132">Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación.</span><span class="sxs-lookup"><span data-stu-id="38ad9-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="38ad9-133">A continuación, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="38ad9-133">Then click OK.</span></span>
    <span data-ttu-id="38ad9-134">![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="38ad9-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="38ad9-135">En la sección Configuración puede configurar las propiedades del sitio de destino</span><span class="sxs-lookup"><span data-stu-id="38ad9-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="38ad9-136">**Ubicación de destino:** es la ubicación donde se replicarán los datos de la máquina virtual de origen.</span><span class="sxs-lookup"><span data-stu-id="38ad9-136">**Target Location:**  This is the location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="38ad9-137">Según la ubicación de las máquinas seleccionadas, Site Recovery proporcionará la lista de regiones de destino adecuadas.</span><span class="sxs-lookup"><span data-stu-id="38ad9-137">Depending upon your selected machines location, Site Recovery will provide you the list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="38ad9-138">Se recomienda conservar la ubicación de destino igual que el almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="38ad9-138">It is recommended to keep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="38ad9-139">**Grupo de recursos de destino:** es el grupo de recursos al que van a pertenecer todas las máquinas virtuales replicadas. De forma predeterminada, ASR creará un nuevo grupo de recursos en la región de destino con un nombre con el sufijo "asr".</span><span class="sxs-lookup"><span data-stu-id="38ad9-139">**Target resource group :** It is the resource group to which all your replicated virtual machines will belong.By default ASR will create a new resource group in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="38ad9-140">En caso de que ya exista el grupo de recursos creado por ASR, se volverá a usar. También puede optar por personalizarlo, como se muestra en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="38ad9-140">In case resource group created by ASR already exist, it will be reused.You can also choose to customize it as shown in the section below.</span></span>    
3. <span data-ttu-id="38ad9-141">**Red Virtual de destino:** de forma predeterminada, ASR creará una nueva red virtual en la región de destino con un nombre con el sufijo "asr".</span><span class="sxs-lookup"><span data-stu-id="38ad9-141">**Target Virtual Network:** By default, ASR will create a new virtual network in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="38ad9-142">Esta se asignará a la red de origen y se usará para todas las protecciones futuras.</span><span class="sxs-lookup"><span data-stu-id="38ad9-142">This will be mapped to your source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="38ad9-143">[Compruebe los detalles de redes](site-recovery-network-mapping-azure-to-azure.md) para obtener más información sobre la asignación de red.</span><span class="sxs-lookup"><span data-stu-id="38ad9-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) to know more about network mapping.</span></span>

4. <span data-ttu-id="38ad9-144">**Cuentas de almacenamiento de destino:** de forma predeterminada, ASR creará la nueva cuenta de almacenamiento de destino mediante la imitación de la configuración de almacenamiento de máquina virtual de origen.</span><span class="sxs-lookup"><span data-stu-id="38ad9-144">**Target Storage accounts:** By default, ASR will create the new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="38ad9-145">En caso de que ya exista la cuenta de almacenamiento creada por ASR, se volverá a usar.</span><span class="sxs-lookup"><span data-stu-id="38ad9-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="38ad9-146">**Cuentas de almacenamiento en caché:** ASR necesita una cuenta de almacenamiento adicional denominada almacenamiento en caché en la región de origen.</span><span class="sxs-lookup"><span data-stu-id="38ad9-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in the source region.</span></span> <span data-ttu-id="38ad9-147">Todos los cambios que se producen en las máquinas virtuales de origen se siguen y se envían a la cuenta de almacenamiento en caché antes de su replicación en la ubicación de destino.</span><span class="sxs-lookup"><span data-stu-id="38ad9-147">All the changes happening on the source VMs are tracked and sent to cache storage account before replicating those to the target location.</span></span>

6. <span data-ttu-id="38ad9-148">**Conjunto de disponibilidad:** de forma predeterminada, ASR creará un nuevo conjunto de disponibilidad en la región de destino con un nombre con el sufijo "asr".</span><span class="sxs-lookup"><span data-stu-id="38ad9-148">**Availability set :** By default, ASR will create a new availability set in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="38ad9-149">En caso de que ya exista el conjunto de disponibilidad creado por ASR, se volverá a usar.</span><span class="sxs-lookup"><span data-stu-id="38ad9-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="38ad9-150">**Directiva de replicación:** define la configuración del historial de retención del punto de recuperación y de la frecuencia de instantánea coherente con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="38ad9-150">**Replication Policy:** It defines the settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="38ad9-151">De forma predeterminada, ASR creará una nueva directiva de replicación con la configuración predeterminada "24 horas" para la retención del punto de recuperación y "60 minutos" para la frecuencia de instantánea coherente con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="38ad9-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="38ad9-153">Personalizar los recursos de destino</span><span class="sxs-lookup"><span data-stu-id="38ad9-153">Customize target resources</span></span>

<span data-ttu-id="38ad9-154">Si quiere cambiar los valores predeterminados que usa ASR, puede modificar la configuración según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="38ad9-154">In case you want to change the defaults used by ASR, you can change the settings based on your needs.</span></span>

1. <span data-ttu-id="38ad9-155">**Personalizar:** haga clic en esta opción para cambiar los valores predeterminados que usa ASR.</span><span class="sxs-lookup"><span data-stu-id="38ad9-155">**Customize:** Click it to change the defaults used by ASR.</span></span>

2. <span data-ttu-id="38ad9-156">**Grupo de recursos de destino:** puede seleccionar el grupo de recursos en la lista de todos los grupos de recursos que existen en la ubicación de destino dentro de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="38ad9-156">**Target resource group :**  You can select the resource group from the list of all the resource groups existing in the target location within the subscription.</span></span>

3. <span data-ttu-id="38ad9-157">**Red virtual de destino:** puede encontrar la lista de todas las redes virtuales en la ubicación de destino.</span><span class="sxs-lookup"><span data-stu-id="38ad9-157">**Target Virtual Network:** You can find the list of all the virtual network in the target location.</span></span>

4. <span data-ttu-id="38ad9-158">**Conjunto de disponibilidad:** solo puede agregar una configuración de conjuntos de disponibilidad a las máquinas virtuales que forman parte de la disponibilidad en la región de origen.</span><span class="sxs-lookup"><span data-stu-id="38ad9-158">**Availability set :** You can only add availability sets settings to the virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="38ad9-159">**Cuentas de almacenamiento de destino:**</span><span class="sxs-lookup"><span data-stu-id="38ad9-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="38ad9-160">![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Haga clic en **Crear recurso de destino** y en Habilitar replicación</span><span class="sxs-lookup"><span data-stu-id="38ad9-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="38ad9-161">Una vez protegidas las máquinas virtuales, puede comprobar su estado en **Elementos replicados**.</span><span class="sxs-lookup"><span data-stu-id="38ad9-161">Once virtual machines are protected you can check the status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="38ad9-162">Durante el tiempo de replicación inicial es posible que el estado tarde en actualizarse y no se vea el progreso durante un tiempo.</span><span class="sxs-lookup"><span data-stu-id="38ad9-162">During the time of initial replication there could a possibility that status takes time to refresh and you don't see progress for some time.</span></span> <span data-ttu-id="38ad9-163">Puede hacer clic en el botón Actualizar de la parte superior de la hoja para obtener el estado más reciente.</span><span class="sxs-lookup"><span data-stu-id="38ad9-163">You can click the Refresh button on the top of the blade to get the latest status.</span></span>
>

![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="38ad9-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="38ad9-165">Next steps</span></span>
- <span data-ttu-id="38ad9-166">[Más información](site-recovery-test-failover-to-azure.md) sobre la ejecución de una conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="38ad9-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="38ad9-167">[Aprenda más](site-recovery-failover.md) sobre los diferentes tipos de conmutación por error y cómo ejecutarlos.</span><span class="sxs-lookup"><span data-stu-id="38ad9-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="38ad9-168">Más información sobre el [uso de planes de recuperación](site-recovery-create-recovery-plans.md) para reducir el RTO.</span><span class="sxs-lookup"><span data-stu-id="38ad9-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
- <span data-ttu-id="38ad9-169">Más información sobre la [reprotección de máquinas virtuales de Azure](site-recovery-how-to-reprotect.md) después de una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="38ad9-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
