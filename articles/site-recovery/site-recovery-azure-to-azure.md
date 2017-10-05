---
title: "Replicación de máquinas virtuales de Azure entre regiones de Azure para las necesidades de recuperación ante desastres: de Azure a Azure | Microsoft Docs"
description: "Se resumen los pasos que necesarios para replicar máquinas virtuales de Azure entre regiones de Azure (de Azure a Azure) con el servicio de Azure Site Recovery para las necesidades de recuperación ante desastres."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: 9ca33057f6030fdcc233f6053fdc392d62f8f9f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="94c86-103">Replicación de máquinas virtuales de Azure entre regiones con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="94c86-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="94c86-104">La replicación de Azure Site Recovery en máquinas virtuales (VM) de Azure está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="94c86-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="94c86-105">En este artículo se describe cómo replicar máquinas virtuales de Azure entre regiones de Azure mediante el servicio de [Site Recovery](site-recovery-overview.md) de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="94c86-105">This article describes how to replicate Azure VMs between Azure regions by using the [Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="94c86-106">Cualquier comentario o pregunta que tenga puede publicarlo en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="94c86-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="94c86-107">Recuperación ante desastres en Azure</span><span class="sxs-lookup"><span data-stu-id="94c86-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="94c86-108">Las características y funcionalidades de infraestructura de Azure integradas contribuyen a una estrategia de disponibilidad sólida y resistente para las cargas de trabajo que se ejecutan en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="94c86-108">Built-in Azure infrastructure capabilities and features contribute to a robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="94c86-109">Sin embargo, hay muchas razones por las que deberá planear por su cuenta la recuperación ante desastres entre regiones de Azure:</span><span class="sxs-lookup"><span data-stu-id="94c86-109">However, there are many reasons why you need to plan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="94c86-110">Debe cumplir las instrucciones de cumplimiento para aplicaciones y cargas de trabajo específicas que requieren una estrategia de continuidad empresarial y recuperación ante desastres (BCDR).</span><span class="sxs-lookup"><span data-stu-id="94c86-110">You need to meet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="94c86-111">Quiere la posibilidad de proteger y recuperar máquinas virtuales de Azure en función de sus decisiones empresariales y no solo de la funcionalidad de Azure integrada.</span><span class="sxs-lookup"><span data-stu-id="94c86-111">You want the ability to protect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="94c86-112">Debe probar la conmutación por error y la recuperación de acuerdo con las necesidades empresariales y de cumplimiento, sin afectar al entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="94c86-112">You need to test failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="94c86-113">Debe conmutar por error a la región de recuperación en caso de desastre y conmutar por recuperación a la región de origen original sin problemas.</span><span class="sxs-lookup"><span data-stu-id="94c86-113">You need to fail over to the recovery region in the event of a disaster and fail back to the original source region seamlessly.</span></span>

<span data-ttu-id="94c86-114">Use Site Recovery para la replicación de máquinas virtuales de Azure a Azure a fin de ayudarle a realizar todas estas tareas.</span><span class="sxs-lookup"><span data-stu-id="94c86-114">Use Site Recovery for Azure-to-Azure VM replication to help you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="94c86-115">¿Por qué usar Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="94c86-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="94c86-116">Site Recovery ofrece una manera sencilla de replicar máquinas virtuales de Azure entre regiones:</span><span class="sxs-lookup"><span data-stu-id="94c86-116">Site Recovery provides a simple way to replicate Azure VMs between regions:</span></span>

- <span data-ttu-id="94c86-117">**Implementación automática**.</span><span class="sxs-lookup"><span data-stu-id="94c86-117">**Automatic deployment**.</span></span> <span data-ttu-id="94c86-118">A diferencia de un modelo de replicación activo/activo, no hay necesidad de una infraestructura cara y compleja en la región secundaria.</span><span class="sxs-lookup"><span data-stu-id="94c86-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in the secondary region.</span></span> <span data-ttu-id="94c86-119">Cuando se habilita la replicación, Site Recovery crea automáticamente los recursos necesarios en la región de destino, en función de la configuración de la región de origen.</span><span class="sxs-lookup"><span data-stu-id="94c86-119">When you enable replication, Site Recovery automatically creates the required resources in the target region, based on source region settings.</span></span>
- <span data-ttu-id="94c86-120">**Controla de las regiones**.</span><span class="sxs-lookup"><span data-stu-id="94c86-120">**Control regions**.</span></span> <span data-ttu-id="94c86-121">Con Site Recovery, puede replicar de una región a otra dentro de un continente.</span><span class="sxs-lookup"><span data-stu-id="94c86-121">With Site Recovery, you can replicate from any region to any region within a continent.</span></span> <span data-ttu-id="94c86-122">En comparación con esto, el almacenamiento con redundancia geográfica con acceso de lectura replica de forma asincrónica solo entre [regiones emparejadas](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) estándar.</span><span class="sxs-lookup"><span data-stu-id="94c86-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="94c86-123">El almacenamiento con redundancia geográfica con acceso de lectura proporciona acceso de solo lectura a los datos de la región de destino.</span><span class="sxs-lookup"><span data-stu-id="94c86-123">Read-access geo-redundant storage provides read-only access to the data in the target region.</span></span>
- <span data-ttu-id="94c86-124">**Replicación automatizada**.</span><span class="sxs-lookup"><span data-stu-id="94c86-124">**Automated replication**.</span></span> <span data-ttu-id="94c86-125">Site Recovery proporciona replicación continua automatizada.</span><span class="sxs-lookup"><span data-stu-id="94c86-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="94c86-126">Con un solo clic es posible desencadenar la conmutación por error y por recuperación.</span><span class="sxs-lookup"><span data-stu-id="94c86-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="94c86-127">**RTO y RPO**.</span><span class="sxs-lookup"><span data-stu-id="94c86-127">**RTO and RPO**.</span></span> <span data-ttu-id="94c86-128">Site Recovery aprovecha la infraestructura de red de Azure que conecta las regiones para mantener el RTO y el RPO en unos niveles muy bajos.</span><span class="sxs-lookup"><span data-stu-id="94c86-128">Site Recovery takes advantage of the Azure network infrastructure that connects regions to keep RTO and RPO very low.</span></span>
- <span data-ttu-id="94c86-129">**Prueba**.</span><span class="sxs-lookup"><span data-stu-id="94c86-129">**Testing**.</span></span> <span data-ttu-id="94c86-130">Puede ejecutar maniobras de recuperación ante desastres con conmutaciones por error de prueba a petición, como y cuando sea necesario, sin que las cargas de trabajo de producción o la replicación en curso se vean afectadas.</span><span class="sxs-lookup"><span data-stu-id="94c86-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="94c86-131">**Planes de recuperación**.</span><span class="sxs-lookup"><span data-stu-id="94c86-131">**Recovery plans**.</span></span> <span data-ttu-id="94c86-132">Puede usar planes de recuperación para orquestar la conmutación por error y la conmutación por recuperación de toda la aplicación que se ejecuta en varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="94c86-132">You can use recovery plans to orchestrate failover and failback of the entire application running on multiple VMs.</span></span> <span data-ttu-id="94c86-133">La característica del plan de recuperación presenta una completa integración de primera clase con los runbooks de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="94c86-133">The recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="94c86-134">Resumen de implementación</span><span class="sxs-lookup"><span data-stu-id="94c86-134">Deployment summary</span></span>

<span data-ttu-id="94c86-135">A continuación se muestra un resumen de lo que debe hacer para configurar la replicación de las máquinas virtuales entre regiones de Azure:</span><span class="sxs-lookup"><span data-stu-id="94c86-135">Here's a summary of what you need to do to set up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="94c86-136">Cree un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="94c86-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="94c86-137">El almacén contiene valores de configuración y orquesta la replicación.</span><span class="sxs-lookup"><span data-stu-id="94c86-137">The vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="94c86-138">Habilite la replicación en las máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="94c86-138">Enable replication for the Azure VMs.</span></span>
3. <span data-ttu-id="94c86-139">Ejecute una conmutación por error de prueba para asegurarse de que todo funcione según lo esperado.</span><span class="sxs-lookup"><span data-stu-id="94c86-139">Run a test failover to make sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="94c86-140">Puede comprobar la [matriz de compatibilidad de la replicación de máquinas virtuales de Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="94c86-140">You can check the [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="94c86-141">Para más información sobre cómo configurar la conectividad de red de salida necesaria en las máquinas virtuales de Azure para la replicación de Site Recovery, consulte el [documento de instrucciones para redes](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="94c86-141">For information on how to configure the required network outbound connectivity for Azure VMs for Site Recovery replication, see the [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="94c86-142">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="94c86-142">Before you start</span></span>

* <span data-ttu-id="94c86-143">Su cuenta de usuario de Azure debe tener ciertos [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) para habilitar la replicación de una máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="94c86-143">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="94c86-144">Su suscripción de Azure debe estar habilitada para crear máquinas virtuales en la ubicación de destino que quiera usar como región de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="94c86-144">Your Azure subscription should be enabled to create VMs in the target location that you want to use as the disaster recovery region.</span></span> <span data-ttu-id="94c86-145">Para habilitar la cuota necesaria, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="94c86-145">Contact support to enable the required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="94c86-146">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="94c86-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="94c86-147">Le recomendamos que cree el almacén de Recovery Services en la ubicación donde quiere que se repliquen las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="94c86-147">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="94c86-148">Por ejemplo, si la ubicación de destino está en el centro de EE. UU., crear el almacén en **Centro de EE. UU**.</span><span class="sxs-lookup"><span data-stu-id="94c86-148">For example, if your target location is the central US, create the vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="94c86-149">Habilitar replicación</span><span class="sxs-lookup"><span data-stu-id="94c86-149">Enable replication</span></span>

<span data-ttu-id="94c86-150">En **Almacenes de Recovery**, haga clic en el nombre del almacén.</span><span class="sxs-lookup"><span data-stu-id="94c86-150">In **Recovery Services vaults**, click the vault name.</span></span> <span data-ttu-id="94c86-151">En el almacén, haga clic en el botón **+ +Replicar** botón.</span><span class="sxs-lookup"><span data-stu-id="94c86-151">In the vault, click the **+Replicate** button.</span></span>

### <a name="step-1-configure-the-source"></a><span data-ttu-id="94c86-152">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="94c86-152">Step 1.</span></span> <span data-ttu-id="94c86-153">Configuración del origen</span><span class="sxs-lookup"><span data-stu-id="94c86-153">Configure the source</span></span>
1. <span data-ttu-id="94c86-154">En **Origen**, seleccione **Azure - VERSIÓN PRELIMINAR**.</span><span class="sxs-lookup"><span data-stu-id="94c86-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="94c86-155">En **Ubicación de origen**, seleccione la región de Azure de origen donde se ejecutan actualmente sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="94c86-155">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="94c86-156">Seleccione el modelo de implementación de las máquinas virtuales: **Resource Manager** o **Clásico**.</span><span class="sxs-lookup"><span data-stu-id="94c86-156">Select the deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="94c86-157">Seleccione el **grupo de recursos de origen** para las máquinas virtuales de Resource Manager o **servicio en la nube** para las máquinas virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="94c86-157">Select the **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Configuración del origen](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="94c86-159">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="94c86-159">Step 2.</span></span> <span data-ttu-id="94c86-160">Selección de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="94c86-160">Select virtual machines</span></span>

* <span data-ttu-id="94c86-161">Seleccione las máquinas virtuales que quiere replicar y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="94c86-161">Select the VMs you want to replicate, and then click **OK**.</span></span>

    ![Selección de las máquinas virtuales](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="94c86-163">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="94c86-163">Step 3.</span></span> <span data-ttu-id="94c86-164">Definición de la configuración</span><span class="sxs-lookup"><span data-stu-id="94c86-164">Configure settings</span></span>

1. <span data-ttu-id="94c86-165">Para invalidar la configuración de destino predeterminada y especificar la configuración de su elección, haga clic en **Personalizar**.</span><span class="sxs-lookup"><span data-stu-id="94c86-165">To override the default target settings and specify the settings of your choice, click **Customize**.</span></span> <span data-ttu-id="94c86-166">Para más información, consulte [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources) (Personalización de los recursos de destino).</span><span class="sxs-lookup"><span data-stu-id="94c86-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Definición de la configuración](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="94c86-168">De forma predeterminada, Site Recovery crea una directiva de replicación que toma cada 4 horas instantáneas coherentes con la aplicación y conserva los puntos de recuperación durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="94c86-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="94c86-169">Para crear una directiva con una configuración diferente, haga clic en **Personalizar** junto a **Directiva de replicación**.</span><span class="sxs-lookup"><span data-stu-id="94c86-169">To create a policy with different settings, click **Customize** next to **Replication Policy**.</span></span>

    ![Personalización de la directiva](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="94c86-171">Para iniciar el aprovisionamiento de los recursos de destino, haga clic en **Crear recursos de destino**.</span><span class="sxs-lookup"><span data-stu-id="94c86-171">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="94c86-172">El aprovisionamiento tarda aproximadamente un minuto.</span><span class="sxs-lookup"><span data-stu-id="94c86-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="94c86-173">No cierre la hoja durante la operación o deberá empezar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="94c86-173">Don't close the blade during provisioning, or you need to start over.</span></span>

4. <span data-ttu-id="94c86-174">Para desencadenar la replicación de la máquina virtual seleccionada, haga clic en **Habilitar la replicación**.</span><span class="sxs-lookup"><span data-stu-id="94c86-174">To trigger replication of the selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="94c86-175">Puede hacer un seguimiento del progreso del trabajo **Habilitar la protección** en **Configuración** > **Trabajos** > **Trabajos de Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="94c86-175">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="94c86-176">En **Configuración** > **Elementos replicados**, puede ver el estado de las máquinas virtuales y el progreso inicial de la replicación.</span><span class="sxs-lookup"><span data-stu-id="94c86-176">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="94c86-177">Haga clic en la máquina virtual para ir a los detalles de su configuración.</span><span class="sxs-lookup"><span data-stu-id="94c86-177">Click the VM to drill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="94c86-178">Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="94c86-178">Run a test failover</span></span>

<span data-ttu-id="94c86-179">Una vez terminada la configuración, ejecute una conmutación por error de prueba para asegurarse de que todo funcione de la forma esperada:</span><span class="sxs-lookup"><span data-stu-id="94c86-179">After you set up everything, run a test failover to make sure everything's working as expected:</span></span>

1. <span data-ttu-id="94c86-180">Para conmutar por error una sola máquina, en **Configuración** > **Elementos replicados**, haga clic en a máquina virtual **+Conmutación por error de prueba**.</span><span class="sxs-lookup"><span data-stu-id="94c86-180">To fail over a single machine, in **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="94c86-181">Para conmutar por error un plan de recuperación, en **Configuración** > **Planes de recuperación**, haga clic con el botón derecho en el plan **Conmutación por error de prueba**.</span><span class="sxs-lookup"><span data-stu-id="94c86-181">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan **Test Failover**.</span></span> <span data-ttu-id="94c86-182">Para crear un plan de recuperación, [siga estas instrucciones](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="94c86-182">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="94c86-183">En **Conmutación por error de prueba**, seleccione la red virtual de Azure a la que están conectadas las máquinas virtuales después de que se produce la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="94c86-183">In **Test Failover**, select the target Azure virtual network to which Azure VMs are connected after the failover occurs.</span></span>

4. <span data-ttu-id="94c86-184">Para iniciar la conmutación por error, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="94c86-184">To start the failover, click **OK**.</span></span> <span data-ttu-id="94c86-185">Para realizar el seguimiento del progreso, haga clic en la máquina virtual para abrir sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="94c86-185">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="94c86-186">También puede hacer clic en el trabajo **Conmutación por error de prueba** en el nombre del almacén > **Configuración** > **Trabajos** > **Trabajos de Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="94c86-186">Or you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="94c86-187">Una vez finalizada la conmutación por error, la máquina de Azure de réplica aparece en Azure Portal > **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="94c86-187">After the failover finishes, the replica Azure machine appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="94c86-188">Debe asegurarse de que la VM tiene el tamaño adecuado, que está conectada a la red correspondiente y que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="94c86-188">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="94c86-189">Para eliminar las máquinas virtuales que se crearon durante la conmutación por error de prueba, haga clic en **Cleanup test failover** (Limpiar conmutación por error de prueba) en el artículo replicado o el plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="94c86-189">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="94c86-190">En **Notas**, registre y guarde las observaciones asociadas a la conmutación por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="94c86-190">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="94c86-191">[Más información](site-recovery-test-failover-to-azure.md) sobre las conmutaciones por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="94c86-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="94c86-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94c86-192">Next steps</span></span>

<span data-ttu-id="94c86-193">Después de probar la implementación:</span><span class="sxs-lookup"><span data-stu-id="94c86-193">After you test the deployment:</span></span>

- <span data-ttu-id="94c86-194">[Obtenga más información](site-recovery-failover.md) sobre los diferentes tipos de conmutación por error y cómo ejecutarlos.</span><span class="sxs-lookup"><span data-stu-id="94c86-194">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
- <span data-ttu-id="94c86-195">Aprenda sobre el [uso de planes de recuperación](site-recovery-create-recovery-plans.md) para reducir el RTO.</span><span class="sxs-lookup"><span data-stu-id="94c86-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
