---
title: "aaaRun una conmutación por error de prueba para VMware replicación tooAzure | Documentos de Microsoft"
description: "Resume los pasos de Hola que necesita para ejecutar una prueba de conmutación por error para replicar tooAzure mediante el servicio de Azure Site Recovery Hola de las máquinas virtuales de VMware."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: bed934446f0c6940089bfae24a13de4fb1556a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-12-run-a-test-failover-tooazure-for-vmware-vms"></a><span data-ttu-id="ea496-103">Paso 12: Ejecutar una tooAzure de conmutación por error de prueba para las máquinas virtuales de VMware</span><span class="sxs-lookup"><span data-stu-id="ea496-103">Step 12: Run a test failover tooAzure for VMware VMs</span></span>

<span data-ttu-id="ea496-104">Este artículo describe cómo toorun una prueba de conmutación por error de local VMware virtual máquinas tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea496-104">This article describes how toorun a test failover from  on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="ea496-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ea496-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="ea496-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="ea496-106">Before you start</span></span>

<span data-ttu-id="ea496-107">Antes de ejecutar una conmutación por error de prueba que se recomienda que compruebe las propiedades de la máquina virtual de Hola y realice los cambios necesite.</span><span class="sxs-lookup"><span data-stu-id="ea496-107">Before you run a test failover we recommend that you verify hello VM properties, and make any changes you need to.</span></span> <span data-ttu-id="ea496-108">puede tener acceso a propiedades de la máquina virtual de hello en **replican elementos**.</span><span class="sxs-lookup"><span data-stu-id="ea496-108">you can access hello VM properties in **Replicated items**.</span></span> <span data-ttu-id="ea496-109">Hola **Essentials** hoja muestra información sobre la configuración de máquinas y estado.</span><span class="sxs-lookup"><span data-stu-id="ea496-109">hello **Essentials** blade shows information about machines settings and status.</span></span>

## <a name="managed-disk-considerations"></a><span data-ttu-id="ea496-110">Consideraciones sobre discos administrados</span><span class="sxs-lookup"><span data-stu-id="ea496-110">Managed disk considerations</span></span>

<span data-ttu-id="ea496-111">[Discos administrados por](../virtual-machines/windows/managed-disks-overview.md) simplificar la administración de disco para máquinas virtuales de Azure, debido a que administra las cuentas de almacenamiento de hello asociadas con discos de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea496-111">[Managed disks](../virtual-machines/windows/managed-disks-overview.md) simplify disk management for Azure VMs, by managing hello storage accounts associated with hello VM disks.</span></span> 

- <span data-ttu-id="ea496-112">Al habilitar la protección para una máquina virtual, datos de máquinas virtuales replican tooa cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ea496-112">When you enable protection for a VM, VM data replicates tooa storage account.</span></span> <span data-ttu-id="ea496-113">Discos administrados se crean y adjunta toohello VM solo cuando se produce la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="ea496-113">Managed disks are created and attached toohello VM only when failover occurs.</span></span>
- <span data-ttu-id="ea496-114">Discos administrados pueden crearse únicamente para máquinas virtuales implementadas mediante el modelo de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea496-114">Managed disks can be created only for VMs deployed using hello Resource Manager model.</span></span>  
- <span data-ttu-id="ea496-115">Con esta opción habilitada, solo se pueden seleccionar los conjuntos de disponibilidad de los grupos de recursos que tienen habilitada la opción **Usar discos administrados**.</span><span class="sxs-lookup"><span data-stu-id="ea496-115">With this setting enabled, only availability sets in Resource Groups that have **Use managed disks** enabled can be selected.</span></span> <span data-ttu-id="ea496-116">Las máquinas virtuales con discos administrados deben estar en conjuntos de disponibilidad con **discos administrados por uso** establecido demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="ea496-116">VMs with managed disks must be in availability sets with **Use managed disks** set too**Yes**.</span></span> <span data-ttu-id="ea496-117">Si no está habilitada la configuración de Hola para las máquinas virtuales, pueden seleccionarse conjuntos de disponibilidad solo en grupos de recursos sin discos administrados habilitados.</span><span class="sxs-lookup"><span data-stu-id="ea496-117">If hello setting isn't enabled for VMs, then only availability sets in Resource Groups without managed disks enabled can be selected.</span></span>
- <span data-ttu-id="ea496-118">Obtenga [más información](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) sobre discos administrados y conjuntos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="ea496-118">[Learn more](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) about managed disks and availability sets.</span></span>
- <span data-ttu-id="ea496-119">Si la cuenta de almacenamiento de hello que utiliza para la replicación se ha cifrado con cifrado de servicio de almacenamiento, no se puede crear discos administrados durante la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="ea496-119">If hello storage account you use for replication has been encrypted with Storage Service Encryption, managed disks can't be created during failover.</span></span> <span data-ttu-id="ea496-120">En este caso cualquiera no habilitar el uso de discos administrados, o deshabilite la protección de hello VM y volver a habilitar toouse una cuenta de almacenamiento que no tiene habilitado el cifrado.</span><span class="sxs-lookup"><span data-stu-id="ea496-120">In this case either don't enable use of managed disks, or disable protection for hello VM, and reenable it toouse a storage account that doesn't have encryption enabled.</span></span> <span data-ttu-id="ea496-121">[Más información](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span><span class="sxs-lookup"><span data-stu-id="ea496-121">[Learn more](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>


## <a name="network-considerations"></a><span data-ttu-id="ea496-122">Consideraciones sobre la red</span><span class="sxs-lookup"><span data-stu-id="ea496-122">Network considerations</span></span>

<span data-ttu-id="ea496-123">Puede establecer la dirección IP de destino de Hola para una máquina virtual de Azure creado después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="ea496-123">You can set hello target IP address for an Azure VM created after failover.</span></span>

- <span data-ttu-id="ea496-124">Si no proporciona una dirección, Hola conmutado por error equipo usará DHCP.</span><span class="sxs-lookup"><span data-stu-id="ea496-124">If you don't provide an address, hello failed over machine will use DHCP.</span></span>
- <span data-ttu-id="ea496-125">Si establece una dirección que no esté disponible en el momento de la conmutación por error, esta no funcionará.</span><span class="sxs-lookup"><span data-stu-id="ea496-125">If you set an address that isn't available at failover, failover won't work.</span></span>
- <span data-ttu-id="ea496-126">Hola la misma dirección IP de destino puede usarse para conmutación por error de prueba, si está disponible en la red de conmutación por error de prueba de Hola Hola dirección.</span><span class="sxs-lookup"><span data-stu-id="ea496-126">hello same target IP address can be used for test failover, if hello address is available in hello test failover network.</span></span>
- <span data-ttu-id="ea496-127">número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de hello:</span><span class="sxs-lookup"><span data-stu-id="ea496-127">hello number of network adapters is dictated by hello size you specify for hello target virtual machine:</span></span>

     - <span data-ttu-id="ea496-128">Si Hola algunos adaptadores de red de máquina de origen de Hola Hola igual o menor, número de Hola de adaptadores permitido para el tamaño de máquina de destino de hello, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea496-128">If hello number of network adapters on hello source machine is hello same as, or less than, hello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
     - <span data-ttu-id="ea496-129">Si número Hola de adaptadores para la máquina virtual de origen de hello supera número de hello permitido para el tamaño de destino de hello, se utilizará el tamaño máximo de hello destino.</span><span class="sxs-lookup"><span data-stu-id="ea496-129">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size, then hello target size maximum will be used.</span></span>
     - <span data-ttu-id="ea496-130">Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores.</span><span class="sxs-lookup"><span data-stu-id="ea496-130">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="ea496-131">Si la máquina de origen hello tiene dos adaptadores de pero hello tamaño de destino admitida solo admite un equipo de destino de Hola tendrá solo un adaptador.</span><span class="sxs-lookup"><span data-stu-id="ea496-131">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>     
   - <span data-ttu-id="ea496-132">Si la máquina virtual de hello tiene varios adaptadores de red se conectarán todos toohello misma red.</span><span class="sxs-lookup"><span data-stu-id="ea496-132">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
   - <span data-ttu-id="ea496-133">Si la máquina virtual de hello tiene varios adaptadores de red, a continuación, Hola mostrado en la lista de hello deja de estar hello *predeterminado* adaptador de red de máquina virtual de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="ea496-133">If hello virtual machine has multiple network adapters then hello first one shown in hello list becomes hello *Default* network adapter in hello Azure virtual machine.</span></span>
 - <span data-ttu-id="ea496-134">Obtenga [más información](vmware-walkthrough-network.md) sobre direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="ea496-134">[Learn more](vmware-walkthrough-network.md) about IP addressing.</span></span>



## <a name="view-and-modify-vm-settings"></a><span data-ttu-id="ea496-135">Vista y modificación de la configuración de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ea496-135">View and modify VM settings</span></span>

<span data-ttu-id="ea496-136">Se recomienda que compruebe las propiedades de Hola de máquina de origen de hello antes de ejecutar una conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="ea496-136">We recommend that you verify hello properties of hello source machine before you run a failover.</span></span>

1. <span data-ttu-id="ea496-137">En **elementos protegidos**, haga clic en **replican elementos**y haga clic en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea496-137">In **Protected Items**, click **Replicated Items**, and click hello VM.</span></span>
2. <span data-ttu-id="ea496-138">Hola **replicadas elemento** panel, puede ver un resumen de información de máquina virtual, estado y puntos de recuperación disponible más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea496-138">In hello **Replicated item** pane, you can see a summary of VM information, health status, and hello latest available recovery points.</span></span> <span data-ttu-id="ea496-139">Haga clic en **propiedades** tooview más detalles.</span><span class="sxs-lookup"><span data-stu-id="ea496-139">Click **Properties** tooview more details.</span></span>
3. <span data-ttu-id="ea496-140">En **Compute and Network** (Proceso y red), puede:</span><span class="sxs-lookup"><span data-stu-id="ea496-140">In **Compute and Network**, you can:</span></span>
    - <span data-ttu-id="ea496-141">Modifique el nombre de la máquina virtual de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea496-141">Modify hello Azure VM name.</span></span> <span data-ttu-id="ea496-142">Hola nombre debe cumplir [requisitos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="ea496-142">hello name must meet [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
    - <span data-ttu-id="ea496-143">Especificar un [grupo de recursos] posterior a la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="ea496-143">Specify a post-failover [resource group].</span></span>
    - <span data-ttu-id="ea496-144">Especifique un tamaño de destino para hello VM de Azure</span><span class="sxs-lookup"><span data-stu-id="ea496-144">Specify a target size for hello Azure VM</span></span>
    - <span data-ttu-id="ea496-145">Seleccione un [conjunto de disponibilidad](../virtual-machines/windows/tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="ea496-145">Select an [availability set](../virtual-machines/windows/tutorial-availability-sets.md).</span></span>
    - <span data-ttu-id="ea496-146">Especifique si toouse [discos administrados por](#managed-disk-considerations).</span><span class="sxs-lookup"><span data-stu-id="ea496-146">Specify whether toouse [managed disks](#managed-disk-considerations).</span></span> <span data-ttu-id="ea496-147">Seleccione **Sí**, si desea que tooattach discos administrados tooyour máquina en tooAzure de migración.</span><span class="sxs-lookup"><span data-stu-id="ea496-147">Select **Yes**, if you want tooattach managed disks tooyour machine on migration tooAzure.</span></span>
    - <span data-ttu-id="ea496-148">Ver o modificar la configuración de red, incluidos red/subred de hello en qué Hola VM de Azure se ubicarán después de la conmutación por error y la dirección IP de Hola que se va a asignar tooit.</span><span class="sxs-lookup"><span data-stu-id="ea496-148">View or modify network settings, including hello network/subnet in which hello Azure VM will be located after failover, and hello IP address that will be assigned tooit.</span></span>
4. <span data-ttu-id="ea496-149">En **discos**, puede ver información sobre el sistema operativo de Hola y Hola de discos de datos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea496-149">In **Disks**, you can see information about hello operating system and data disks on hello VM.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="ea496-150">Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="ea496-150">Run a test failover</span></span>

<span data-ttu-id="ea496-151">Una vez que hayas configurado todo, ejecute un toomake de conmutación por error de prueba que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="ea496-151">After you've set everything up, run a test failover toomake sure everything's working as expected.</span></span>

- <span data-ttu-id="ea496-152">Si desea que tooconnect tooAzure máquinas virtuales mediante RDP después de la conmutación por error, [preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span><span class="sxs-lookup"><span data-stu-id="ea496-152">If you want tooconnect tooAzure VMs using RDP after failover, [prepare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="ea496-153">prueba de toofully necesita toocopy de Active Directory y DNS en el entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ea496-153">toofully test you need toocopy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="ea496-154">[Más información](site-recovery-active-directory.md#test-failover-considerations).</span><span class="sxs-lookup"><span data-stu-id="ea496-154">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>
 - <span data-ttu-id="ea496-155">Para obtener información completa sobre la conmutación por error de prueba, lea [este artículo](site-recovery-test-failover-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ea496-155">For full information about test failover, read [this article](site-recovery-test-failover-to-azure.md) article.</span></span>
- <span data-ttu-id="ea496-156">Vea un vídeo introductorio rápido antes de empezar:</span><span class="sxs-lookup"><span data-stu-id="ea496-156">Get a quick video overview before you start:</span></span>


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


<span data-ttu-id="ea496-157">Ahora ejecute una conmutación por error:</span><span class="sxs-lookup"><span data-stu-id="ea496-157">Now, run a failover:</span></span>

1. <span data-ttu-id="ea496-158">toofail a través de un único equipo, en **configuración** > **replican elementos**, haga clic en hello VM > **+ conmutación por error de prueba** icono.</span><span class="sxs-lookup"><span data-stu-id="ea496-158">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM > **+Test Failover** icon.</span></span>

    ![Probar conmutación por error](./media/vmware-walkthrough-test-failover/test-failover.png)

2. <span data-ttu-id="ea496-160">toofail a través de una recuperación del plan, en **configuración** > **planes de recuperación**, plan de hello contextual > **conmutación por error de prueba**.</span><span class="sxs-lookup"><span data-stu-id="ea496-160">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan > **Test Failover**.</span></span> <span data-ttu-id="ea496-161">un plan de recuperación, toocreate [, siga estas instrucciones](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="ea496-161">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>  

3. <span data-ttu-id="ea496-162">En **conmutación por error de prueba**, seleccione toowhich de red de Azure Hola máquinas virtuales de Azure se conectará después de producirse la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="ea496-162">In **Test Failover**, select hello Azure network toowhich Azure VMs will be connected after failover occurs.</span></span>

4. <span data-ttu-id="ea496-163">Haga clic en **Aceptar** conmutación por error de toobegin Hola.</span><span class="sxs-lookup"><span data-stu-id="ea496-163">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="ea496-164">Pueda seguir el progreso haciendo clic en hello VM tooopen sus propiedades o en hello **conmutación por error de prueba** trabajo en nombre de almacén > **configuración** > **trabajos**  >  **Trabajos de recuperación del sitio**.</span><span class="sxs-lookup"><span data-stu-id="ea496-164">You can track progress by clicking on hello VM tooopen its properties, or on hello **Test Failover** job in vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="ea496-165">Una vez completada la conmutación por error de hello, también debe poder réplica de hello toosee máquina Azure aparecen en hello portal de Azure > **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="ea496-165">After hello failover completes, you should also be able toosee hello replica Azure machine appear in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="ea496-166">Debe asegurarse de que esa máquina virtual de hello es el tamaño adecuado de hello, que ha conectado toohello de red adecuada y que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="ea496-166">You should make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="ea496-167">Si preparado para las conexiones después de la conmutación por error, debe ser capaz de tooconnect toohello máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea496-167">If you prepared for connections after failover, you should be able tooconnect toohello Azure VM.</span></span>

7. <span data-ttu-id="ea496-168">Cuando termine, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="ea496-168">After you finish, click on **Cleanup test failover** on hello recovery plan.</span></span> <span data-ttu-id="ea496-169">En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea496-169">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="ea496-170">Esto eliminará las máquinas virtuales de Hola que se crearon durante la conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="ea496-170">This will delete hello VMs that were created during test failover.</span></span>



## <a name="next-steps"></a><span data-ttu-id="ea496-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea496-171">Next steps</span></span>

- <span data-ttu-id="ea496-172">[Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.</span><span class="sxs-lookup"><span data-stu-id="ea496-172">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="ea496-173">Si migra máquinas en lugar de replicar y conmutar por recuperación, [lea más](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span><span class="sxs-lookup"><span data-stu-id="ea496-173">If you're migrating machines rather than replicating and failing back, [read more](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span></span>
- <span data-ttu-id="ea496-174">[Obtenga información sobre la conmutación por recuperación](site-recovery-failback-azure-to-vmware.md), toofail back y replicar máquinas virtuales de Azure nuevo sitio de toohello local principal.</span><span class="sxs-lookup"><span data-stu-id="ea496-174">[Read about failback](site-recovery-failback-azure-to-vmware.md), toofail back and replicate Azure VMs back toohello primary on-premises site.</span></span>