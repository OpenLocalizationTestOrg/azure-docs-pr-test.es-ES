---
title: "Replicar máquinas virtuales de Azure entre regiones de Azure para las necesidades de recuperación ante desastres: tooAzure Azure | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooreplicate máquinas virtuales de Azure entre regiones de Azure (Azure en Azure) con el servicio de Azure Site Recovery de Hola para las necesidades de recuperación ante desastres."
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
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="084e4-103">Replicación de máquinas virtuales de Azure entre regiones con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="084e4-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="084e4-104">La replicación de Azure Site Recovery en máquinas virtuales (VM) de Azure está actualmente en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="084e4-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="084e4-105">Este artículo describe cómo tooreplicate máquinas virtuales de Azure entre regiones de Azure mediante el uso de Hola [Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="084e4-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="084e4-106">Envíe los comentarios y preguntas en parte inferior de este artículo o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="084e4-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="084e4-107">Recuperación ante desastres en Azure</span><span class="sxs-lookup"><span data-stu-id="084e4-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="084e4-108">Características y capacidades de infraestructura de Azure integrada contribuyen tooa estrategia de disponibilidad sólido y flexible para cargas de trabajo que se ejecutan en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="084e4-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="084e4-109">Sin embargo, hay muchas razones por qué necesita tooplan para la recuperación ante desastres entre regiones de Azure por sí mismo:</span><span class="sxs-lookup"><span data-stu-id="084e4-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="084e4-110">Directrices de cumplimiento del toomeet que necesita para aplicaciones específicas y las cargas de trabajo que requieren una continuidad del negocio y la estrategia de recuperación (BCDR).</span><span class="sxs-lookup"><span data-stu-id="084e4-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="084e4-111">Desea tooprotect de capacidad de Hola y recuperar máquinas virtuales basándose en sus decisiones de negocios y no solo de Azure basado en la funcionalidad de Azure integrada.</span><span class="sxs-lookup"><span data-stu-id="084e4-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="084e4-112">Necesitará tootest conmutación por error y recuperación según sus necesidades empresariales y cumplimiento de normas, sin tener impacto en producción.</span><span class="sxs-lookup"><span data-stu-id="084e4-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="084e4-113">Es necesario toofail sobre toohello región de recuperación en caso de hello de un desastre y producirá un error de región de origen original toohello atrás sin problemas.</span><span class="sxs-lookup"><span data-stu-id="084e4-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="084e4-114">Use la recuperación del sitio para toohelp de replicación de máquina virtual de Azure en Azure puede realizar todas estas tareas.</span><span class="sxs-lookup"><span data-stu-id="084e4-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="084e4-115">¿Por qué usar Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="084e4-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="084e4-116">Site Recovery ofrece una manera sencilla de tooreplicate máquinas virtuales de Azure entre regiones:</span><span class="sxs-lookup"><span data-stu-id="084e4-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="084e4-117">**Implementación automática**.</span><span class="sxs-lookup"><span data-stu-id="084e4-117">**Automatic deployment**.</span></span> <span data-ttu-id="084e4-118">A diferencia de un modelo de replicación activo / activo, no es necesario para una infraestructura cara y compleja en la región secundaria Hola.</span><span class="sxs-lookup"><span data-stu-id="084e4-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="084e4-119">Cuando se habilita la replicación, Site Recovery crea automáticamente los recursos de hello necesario en la región de destino de hello, en función de la configuración de la región de origen.</span><span class="sxs-lookup"><span data-stu-id="084e4-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="084e4-120">**Controla de las regiones**.</span><span class="sxs-lookup"><span data-stu-id="084e4-120">**Control regions**.</span></span> <span data-ttu-id="084e4-121">Con la recuperación del sitio, puede replicar desde cualquier región tooany otra dentro de un continente.</span><span class="sxs-lookup"><span data-stu-id="084e4-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="084e4-122">En comparación con esto, el almacenamiento con redundancia geográfica con acceso de lectura replica de forma asincrónica solo entre [regiones emparejadas](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) estándar.</span><span class="sxs-lookup"><span data-stu-id="084e4-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="084e4-123">Almacenamiento con redundancia geográfica con acceso de lectura proporciona datos de toohello de acceso de solo lectura en la región de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="084e4-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="084e4-124">**Replicación automatizada**.</span><span class="sxs-lookup"><span data-stu-id="084e4-124">**Automated replication**.</span></span> <span data-ttu-id="084e4-125">Site Recovery proporciona replicación continua automatizada.</span><span class="sxs-lookup"><span data-stu-id="084e4-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="084e4-126">Con un solo clic es posible desencadenar la conmutación por error y por recuperación.</span><span class="sxs-lookup"><span data-stu-id="084e4-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="084e4-127">**RTO y RPO**.</span><span class="sxs-lookup"><span data-stu-id="084e4-127">**RTO and RPO**.</span></span> <span data-ttu-id="084e4-128">Recuperación de sitio aprovecha la infraestructura de red de Azure de Hola que conecta las regiones tookeep RTO y el RPO muy baja.</span><span class="sxs-lookup"><span data-stu-id="084e4-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="084e4-129">**Prueba**.</span><span class="sxs-lookup"><span data-stu-id="084e4-129">**Testing**.</span></span> <span data-ttu-id="084e4-130">Puede ejecutar maniobras de recuperación ante desastres con conmutaciones por error de prueba a petición, como y cuando sea necesario, sin que las cargas de trabajo de producción o la replicación en curso se vean afectadas.</span><span class="sxs-lookup"><span data-stu-id="084e4-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="084e4-131">**Planes de recuperación**.</span><span class="sxs-lookup"><span data-stu-id="084e4-131">**Recovery plans**.</span></span> <span data-ttu-id="084e4-132">Puede utilizar la conmutación por error el tooorchestrate de planes de recuperación y conmutación por recuperación de aplicación completo Hola se ejecuta en varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="084e4-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="084e4-133">característica de plan de recuperación de Hello tiene integración enriquecida de primera clase con runbooks de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="084e4-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="084e4-134">Resumen de implementación</span><span class="sxs-lookup"><span data-stu-id="084e4-134">Deployment summary</span></span>

<span data-ttu-id="084e4-135">Este es un resumen de lo que necesita toodo tooset la replicación de máquinas virtuales entre las regiones de Azure:</span><span class="sxs-lookup"><span data-stu-id="084e4-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="084e4-136">Cree un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="084e4-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="084e4-137">almacén de Hello contiene valores de configuración y organiza la replicación.</span><span class="sxs-lookup"><span data-stu-id="084e4-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="084e4-138">Habilitar la replicación de hello máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="084e4-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="084e4-139">Ejecutar un toomake de conmutación por error de prueba seguro de que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="084e4-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="084e4-140">Puede comprobar hello [matriz de compatibilidad para la replicación de máquina virtual de Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="084e4-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="084e4-141">Para obtener información sobre cómo tooconfigure Hola requiere conectividad de red saliente para máquinas virtuales de Azure para la replicación de Site Recovery, vea hello [documento de guía de red](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="084e4-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="084e4-142">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="084e4-142">Before you start</span></span>

* <span data-ttu-id="084e4-143">Su cuenta de usuario de Azure necesita toohave determinados [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="084e4-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="084e4-144">Su suscripción de Azure debe ser máquinas virtuales de toocreate habilitado en la ubicación de destino de Hola que desea toouse como región de recuperación ante desastres de Hola.</span><span class="sxs-lookup"><span data-stu-id="084e4-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="084e4-145">Póngase en contacto con soporte técnico tooenable Hola necesario cuota.</span><span class="sxs-lookup"><span data-stu-id="084e4-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="084e4-146">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="084e4-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="084e4-147">Le recomendamos que cree el almacén de servicios de recuperación de hello en ubicación de Hola donde desea que su tooreplicate de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="084e4-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="084e4-148">Por ejemplo, si la ubicación de destino es hello centro nos, crear almacén de hello en **Central US**.</span><span class="sxs-lookup"><span data-stu-id="084e4-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="084e4-149">Habilitar replicación</span><span class="sxs-lookup"><span data-stu-id="084e4-149">Enable replication</span></span>

<span data-ttu-id="084e4-150">En **servicios de recuperación de los almacenes de credenciales**, haga clic en el nombre del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="084e4-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="084e4-151">En el almacén de hello, haga clic en hello **+ replicar** botón.</span><span class="sxs-lookup"><span data-stu-id="084e4-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="084e4-152">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="084e4-152">Step 1.</span></span> <span data-ttu-id="084e4-153">Configurar origen de Hola</span><span class="sxs-lookup"><span data-stu-id="084e4-153">Configure hello source</span></span>
1. <span data-ttu-id="084e4-154">En **Origen**, seleccione **Azure - VERSIÓN PRELIMINAR**.</span><span class="sxs-lookup"><span data-stu-id="084e4-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="084e4-155">En **ubicación de origen**, seleccione origen Hola región de Azure donde se están ejecutando las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="084e4-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="084e4-156">Modelo de implementación de hello SELECT de las máquinas virtuales: **el Administrador de recursos** o **clásico**.</span><span class="sxs-lookup"><span data-stu-id="084e4-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="084e4-157">Seleccione hello **grupo de recursos de origen** para las máquinas virtuales del Administrador de recursos o **servicio en la nube** para las VM clásicas.</span><span class="sxs-lookup"><span data-stu-id="084e4-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Configurar origen de Hola](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="084e4-159">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="084e4-159">Step 2.</span></span> <span data-ttu-id="084e4-160">Selección de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="084e4-160">Select virtual machines</span></span>

* <span data-ttu-id="084e4-161">Seleccione hello las máquinas virtuales que desee tooreplicate y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="084e4-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![Selección de las máquinas virtuales](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="084e4-163">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="084e4-163">Step 3.</span></span> <span data-ttu-id="084e4-164">Definición de la configuración</span><span class="sxs-lookup"><span data-stu-id="084e4-164">Configure settings</span></span>

1. <span data-ttu-id="084e4-165">predeterminado de hello toooverride configuración de destino y especifique la configuración de Hola de su elección, haga clic en **personalizar**.</span><span class="sxs-lookup"><span data-stu-id="084e4-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="084e4-166">Para más información, consulte [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources) (Personalización de los recursos de destino).</span><span class="sxs-lookup"><span data-stu-id="084e4-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Definición de la configuración](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="084e4-168">De forma predeterminada, Site Recovery crea una directiva de replicación que toma cada 4 horas instantáneas coherentes con la aplicación y conserva los puntos de recuperación durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="084e4-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="084e4-169">toocreate una directiva con distintos valores, haga clic en **personalizar** siguiente demasiado**directiva de replicación**.</span><span class="sxs-lookup"><span data-stu-id="084e4-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![Personalización de la directiva](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="084e4-171">Haga clic en recursos de destino de hello aprovisionamiento toostart **crear recursos de destino**.</span><span class="sxs-lookup"><span data-stu-id="084e4-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="084e4-172">El aprovisionamiento tarda aproximadamente un minuto.</span><span class="sxs-lookup"><span data-stu-id="084e4-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="084e4-173">No cierre la hoja de Hola durante el aprovisionamiento, o si debe toostart sobre.</span><span class="sxs-lookup"><span data-stu-id="084e4-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="084e4-174">replicación tootrigger de hello seleccionado VM, haga clic en **habilitar la replicación**.</span><span class="sxs-lookup"><span data-stu-id="084e4-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="084e4-175">Puede seguir el progreso del programa Hola a **habilitar la protección** de trabajo en **configuración** > **trabajos** > **trabajos de recuperación de sitio**.</span><span class="sxs-lookup"><span data-stu-id="084e4-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="084e4-176">En **configuración** > **replican elementos**, puede ver el estado de Hola de máquinas virtuales y Hola progreso de la replicación inicial.</span><span class="sxs-lookup"><span data-stu-id="084e4-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="084e4-177">Haga clic en hello VM toodrill hacia abajo en su configuración.</span><span class="sxs-lookup"><span data-stu-id="084e4-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="084e4-178">Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="084e4-178">Run a test failover</span></span>

<span data-ttu-id="084e4-179">Una vez configurado todo, ejecute un toomake de conmutación por error de prueba que todo funciona según lo esperado:</span><span class="sxs-lookup"><span data-stu-id="084e4-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="084e4-180">toofail a través de un único equipo, en **configuración** > **replican elementos**, haga clic en hello VM **+ conmutación por error de prueba** icono.</span><span class="sxs-lookup"><span data-stu-id="084e4-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="084e4-181">toofail a través de una recuperación del plan, en **configuración** > **planes de recuperación**, plan de hello contextual **conmutación por error de prueba**.</span><span class="sxs-lookup"><span data-stu-id="084e4-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="084e4-182">un plan de recuperación, toocreate [, siga estas instrucciones](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="084e4-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="084e4-183">En **conmutación por error de prueba**, seleccione toowhich de red virtual de Azure de destino de hello máquinas virtuales de Azure están conectados después de producirse la conmutación por error de Hola.</span><span class="sxs-lookup"><span data-stu-id="084e4-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="084e4-184">toostart Hola conmutación por error, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="084e4-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="084e4-185">tootrack de progreso, haga clic en hello VM tooopen sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="084e4-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="084e4-186">O puede hacer clic en hello **conmutación por error de prueba** trabajo en el nombre del almacén de hello > **configuración** > **trabajos** > **detrabajosderecuperacióndesitio**.</span><span class="sxs-lookup"><span data-stu-id="084e4-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="084e4-187">Después de hello conmutación por error finaliza, réplica de hello máquina de Azure aparece en hello portal de Azure > **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="084e4-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="084e4-188">Asegúrese de que ese hello VM es el tamaño adecuado de hello, que ha conectado toohello de red adecuada y que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="084e4-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="084e4-189">Hola toodelete las máquinas virtuales que se crearon durante la conmutación por error de prueba hello, haga clic en **conmutación por error de prueba de limpieza** en hello replicar Hola o elemento de plan de recuperación.</span><span class="sxs-lookup"><span data-stu-id="084e4-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="084e4-190">En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="084e4-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="084e4-191">[Más información](site-recovery-test-failover-to-azure.md) sobre las conmutaciones por error de prueba.</span><span class="sxs-lookup"><span data-stu-id="084e4-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="084e4-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="084e4-192">Next steps</span></span>

<span data-ttu-id="084e4-193">Después de probar la implementación de hello:</span><span class="sxs-lookup"><span data-stu-id="084e4-193">After you test hello deployment:</span></span>

- <span data-ttu-id="084e4-194">[Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.</span><span class="sxs-lookup"><span data-stu-id="084e4-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="084e4-195">Obtenga más información sobre [con planes de recuperación](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="084e4-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
