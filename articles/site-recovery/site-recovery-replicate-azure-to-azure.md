---
title: aplicaciones de aaaReplicate (Azure tooAzure) | Documentos de Microsoft
description: "Este artículo describe cómo ejecutar los equipos de tooset la replicación de memoria virtual en una región de Azure demasiado otra región de Azure."
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
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="d1e97-103">Replicar máquinas virtuales de Azure tooanother región de Azure</span><span class="sxs-lookup"><span data-stu-id="d1e97-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="d1e97-104">La replicación de Site Recovery en máquinas virtuales de Azure se encuentra actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="d1e97-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="d1e97-105">Este artículo describe cómo ejecutar los equipos de tooset la replicación de memoria virtual en una región de Azure tooanother región de Azure.</span><span class="sxs-lookup"><span data-stu-id="d1e97-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1e97-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d1e97-106">Prerequisites</span></span>

* <span data-ttu-id="d1e97-107">artículo de Hola se supone que ya sabe algo acerca de Site Recovery y almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d1e97-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="d1e97-108">Deberá toohave un pre "Almacén de servicios de recuperación" creado.</span><span class="sxs-lookup"><span data-stu-id="d1e97-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="d1e97-109">Se recomienda que cree Hola "Almacén de servicios de recuperación" en ubicación Hola donde desea que su tooreplicate de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d1e97-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="d1e97-110">Por ejemplo, si la ubicación de destino es "Centro de EE. UU.", cree el almacén en "Centro de EE. UU.".</span><span class="sxs-lookup"><span data-stu-id="d1e97-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="d1e97-111">Si usan reglas de grupos de seguridad de red (NSG) o la conectividad a internet firewall proxy toocontrol acceso toooutbound en hello máquinas virtuales de Azure, asegúrese de que Hola de lista blanca de direcciones requiere direcciones URL o direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="d1e97-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="d1e97-112">Consulte demasiado[documento de orientación de las redes](./site-recovery-azure-to-azure-networking-guidance.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="d1e97-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="d1e97-113">Si tiene una ExpressRoute o una conexión VPN entre hello y local del origen de ubicación de Azure, siga [consideraciones sobre la recuperación de sitio de ExpressRoute de Azure tooon local / configuración de VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) documento.</span><span class="sxs-lookup"><span data-stu-id="d1e97-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="d1e97-114">Su cuenta de usuario de Azure necesita toohave determinados [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="d1e97-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="d1e97-115">Su suscripción de Azure debe estar habilitado toocreate las máquinas virtuales en la ubicación de destino de hello desea toouse como región de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="d1e97-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="d1e97-116">Puede ponerse en contacto con soporte técnico tooenable Hola necesario cuota.</span><span class="sxs-lookup"><span data-stu-id="d1e97-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="d1e97-117">Habilitar la replicación desde el almacén de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d1e97-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="d1e97-118">De esta ilustración, se replicará máquinas virtuales en ejecución en toohello de ubicación de Azure de 'Asia oriental' hello ' sudeste asiático ' ubicación.</span><span class="sxs-lookup"><span data-stu-id="d1e97-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="d1e97-119">pasos de Hello son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d1e97-119">hello steps are as follows:</span></span>

 <span data-ttu-id="d1e97-120">Haga clic en **+ replicar** en la replicación de tooenable de almacén de Hola para las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1e97-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="d1e97-121">**Origen:** hace referencia toohello punto de origen de máquinas de Hola que en este caso es **Azure**.</span><span class="sxs-lookup"><span data-stu-id="d1e97-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="d1e97-122">**Ubicación de origen:** es Hola región de Azure desde donde desea tooprotect las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d1e97-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="d1e97-123">En esta ilustración, ubicación de origen de hello constituye 'Asia oriental'</span><span class="sxs-lookup"><span data-stu-id="d1e97-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="d1e97-124">**Modelo de implementación:** hace referencia toohello modelo de implementación de Azure de máquinas de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="d1e97-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="d1e97-125">Puede seleccionar cualquier clásico o el Administrador de recursos y máquinas que pertenecen toohello específicos del modelo se mostrarán para la protección en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="d1e97-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="d1e97-126">Solo puede replicar una máquina virtual clásica y recuperarla como máquina virtual clásica.</span><span class="sxs-lookup"><span data-stu-id="d1e97-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="d1e97-127">No puede recuperarla como una máquina virtual de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d1e97-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="d1e97-128">**Grupo de recursos:** lo del toowhich de grupo de recursos de hello las máquinas virtuales de origen pertenecen.</span><span class="sxs-lookup"><span data-stu-id="d1e97-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="d1e97-129">Hola todas las máquinas virtuales en el grupo de recursos seleccionado Hola se enumerarán para la protección en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="d1e97-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="d1e97-131">En **máquinas virtuales > Seleccionar las máquinas virtuales**, haga clic en y seleccione cada máquina tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="d1e97-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="d1e97-132">Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación.</span><span class="sxs-lookup"><span data-stu-id="d1e97-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="d1e97-133">A continuación, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="d1e97-133">Then click OK.</span></span>
    <span data-ttu-id="d1e97-134">![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="d1e97-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="d1e97-135">En la sección Configuración puede configurar las propiedades del sitio de destino</span><span class="sxs-lookup"><span data-stu-id="d1e97-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="d1e97-136">**Ubicación de destino:** se trata de ubicación de Hola donde se replicarán los datos de la máquina virtual de origen.</span><span class="sxs-lookup"><span data-stu-id="d1e97-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="d1e97-137">Dependiendo de la ubicación de los equipos seleccionados, Site Recovery proporcionará que Hola lista de regiones de destino adecuado.</span><span class="sxs-lookup"><span data-stu-id="d1e97-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="d1e97-138">Se recomienda la ubicación de destino de tookeep igual a partir de la recuperación del almacén de servicios.</span><span class="sxs-lookup"><span data-stu-id="d1e97-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="d1e97-139">**Grupo de recursos de destino:** es toowhich de grupo de recursos de hello pertenecerá todas sus máquinas virtuales replicadas. De forma predeterminada ASR creará un nuevo grupo de recursos en la región de destino de hello con nombre con sufijo "asr".</span><span class="sxs-lookup"><span data-stu-id="d1e97-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="d1e97-140">En caso de que existe el grupo de recursos ya creado por ASR, se volverá a usar. También puede elegir toocustomize tal como se muestra en la siguiente sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1e97-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="d1e97-141">**Red Virtual de destino:** de forma predeterminada, ASR creará una nueva red virtual en la región de destino de hello con nombre con sufijo "asr".</span><span class="sxs-lookup"><span data-stu-id="d1e97-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="d1e97-142">Esto será asignada tooyour red de origen y se usará para todas las protecciones futuras.</span><span class="sxs-lookup"><span data-stu-id="d1e97-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d1e97-143">[Compruebe los detalles de la red](site-recovery-network-mapping-azure-to-azure.md) tooknow más información acerca de la asignación de red.</span><span class="sxs-lookup"><span data-stu-id="d1e97-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="d1e97-144">**Las cuentas de almacenamiento de destino:** de forma predeterminada, ASR creará Hola nueva la cuenta de almacenamiento destino imitando la configuración de almacenamiento de máquina virtual de origen.</span><span class="sxs-lookup"><span data-stu-id="d1e97-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="d1e97-145">En caso de que ya exista la cuenta de almacenamiento creada por ASR, se volverá a usar.</span><span class="sxs-lookup"><span data-stu-id="d1e97-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="d1e97-146">**Almacenar en caché las cuentas de almacenamiento:** ASR necesita la cuenta de almacenamiento adicional denominada almacenamiento en caché en la región de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1e97-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="d1e97-147">Todos los Hola los cambios que ocurren en hello máquinas virtuales de origen se realiza el seguimiento y envían toocache cuenta de almacenamiento antes de replicar esos ubicación de destino de toohello.</span><span class="sxs-lookup"><span data-stu-id="d1e97-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="d1e97-148">**Conjunto de disponibilidad:** de forma predeterminada, ASR creará un nuevo conjunto de disponibilidad en la región de destino de hello con nombre con sufijo "asr".</span><span class="sxs-lookup"><span data-stu-id="d1e97-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="d1e97-149">En caso de que ya exista el conjunto de disponibilidad creado por ASR, se volverá a usar.</span><span class="sxs-lookup"><span data-stu-id="d1e97-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="d1e97-150">**Directiva de replicación:** define opciones de configuración de Hola para recuperación punto retención historial y aplicación instantánea coherente con la frecuencia.</span><span class="sxs-lookup"><span data-stu-id="d1e97-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="d1e97-151">De forma predeterminada, ASR creará una nueva directiva de replicación con la configuración predeterminada "24 horas" para la retención del punto de recuperación y "60 minutos" para la frecuencia de instantánea coherente con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d1e97-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="d1e97-153">Personalizar los recursos de destino</span><span class="sxs-lookup"><span data-stu-id="d1e97-153">Customize target resources</span></span>

<span data-ttu-id="d1e97-154">En caso de que desea que los valores predeterminados de Hola de toochange que se utiliza ASR, puede cambiar la configuración de hello según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="d1e97-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="d1e97-155">**Personalizar:** haga clic en él toochange Hola parámetro predeterminado utilizado por ASR.</span><span class="sxs-lookup"><span data-stu-id="d1e97-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="d1e97-156">**Grupo de recursos de destino:** puede seleccionar grupo de recursos de hello en lista de Hola de todos los grupos de recursos de hello existentes en la ubicación de destino de hello dentro de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1e97-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="d1e97-157">**Red Virtual de destino:** encontrará la lista de Hola de todas las redes virtuales de hello en la ubicación de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1e97-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="d1e97-158">**Conjunto de disponibilidad:** solo puede agregar disponibilidad conjuntos de configuración toohello las máquinas virtuales que forman parte de la disponibilidad en la región de origen.</span><span class="sxs-lookup"><span data-stu-id="d1e97-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="d1e97-159">**Cuentas de almacenamiento de destino:**</span><span class="sxs-lookup"><span data-stu-id="d1e97-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="d1e97-160">![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Haga clic en **Crear recurso de destino** y en Habilitar replicación</span><span class="sxs-lookup"><span data-stu-id="d1e97-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="d1e97-161">Una vez que se protegen las máquinas virtuales se puede comprobar el estado de Hola de mantenimiento de máquinas virtuales en **elementos de replicación**</span><span class="sxs-lookup"><span data-stu-id="d1e97-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="d1e97-162">Durante el saludo momento de la replicación inicial podría una posibilidad de que el estado toma toorefresh de tiempo y no ver progreso durante algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="d1e97-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="d1e97-163">Puede hacer clic en el botón de actualización de hello en la parte superior de Hola de estado más reciente de hello hoja tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="d1e97-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![Habilitar replicación](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="d1e97-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1e97-165">Next steps</span></span>
- <span data-ttu-id="d1e97-166">[Más información](site-recovery-test-failover-to-azure.md) sobre la ejecución de una conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="d1e97-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="d1e97-167">[Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.</span><span class="sxs-lookup"><span data-stu-id="d1e97-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="d1e97-168">Obtenga más información sobre [con planes de recuperación](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="d1e97-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="d1e97-169">Más información sobre la [reprotección de máquinas virtuales de Azure](site-recovery-how-to-reprotect.md) después de una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="d1e97-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
