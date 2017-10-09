---
title: "la replicación para máquinas virtuales de Azure tooanother región de Azure con Azure Site Recovery aaaEnable | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooenable replicación tooanother región de Azure para máquinas virtuales de Azure, mediante el servicio de Azure Site Recovery Hola"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="a9f93-103">Paso 5: Habilitación de la replicación para máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="a9f93-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="a9f93-104">Después de configurar un [del almacén de servicios de recuperación](azure-to-azure-walkthrough-vault.md), use este artículo tooenable la replicación de máquinas virtuales (VM), región de Azure, tooanother con [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9f93-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article tooenable replication of virtual machines (VMs), tooanother Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="a9f93-105">replicación de tooenable, se configuran los valores de origen y destino, compruebe la directiva de replicación de Hola y seleccione las máquinas virtuales que desee tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="a9f93-105">tooenable replication, you set up source and target settings, verify hello replication policy, and select VMs you want tooreplicate.</span></span>

- <span data-ttu-id="a9f93-106">Cuando termine de artículo hello, las máquinas virtuales de Azure debe replicar toohello región secundaria de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9f93-106">When you finish hello article, your Azure VMs should be replicating toohello secondary Azure region.</span></span>
- <span data-ttu-id="a9f93-107">Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="a9f93-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="a9f93-108">La replicación de VM de Azure se encuentra en una versión preliminar en este momento.</span><span class="sxs-lookup"><span data-stu-id="a9f93-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-hello-source"></a><span data-ttu-id="a9f93-109">Seleccionar origen de Hola</span><span class="sxs-lookup"><span data-stu-id="a9f93-109">Select hello source</span></span> 

1. <span data-ttu-id="a9f93-110">En los almacenes de servicios de recuperación, haga clic en el nombre del almacén de hello > **+ replicar**.</span><span class="sxs-lookup"><span data-stu-id="a9f93-110">In Recovery Services vaults, click hello vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="a9f93-111">En **Origen**, seleccione **Azure - VERSIÓN PRELIMINAR**.</span><span class="sxs-lookup"><span data-stu-id="a9f93-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="a9f93-112">En **ubicación de origen**, seleccione origen Hola región de Azure donde se están ejecutando las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a9f93-112">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="a9f93-113">Seleccione hello **modelo de implementación de máquina virtual de Azure** para las máquinas virtuales: **el Administrador de recursos** o **clásico**.</span><span class="sxs-lookup"><span data-stu-id="a9f93-113">Select hello **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="a9f93-114">Seleccione hello **grupo de recursos de origen** para máquinas virtuales del Administrador de recursos, o **servicio en la nube** para las VM clásicas.</span><span class="sxs-lookup"><span data-stu-id="a9f93-114">Select hello **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="a9f93-115">Haga clic en **Aceptar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="a9f93-115">Click **OK** toosave hello settings.</span></span>

    ![Configurar origen de Hola](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a><span data-ttu-id="a9f93-117">Seleccione hello las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a9f93-117">Select hello VMs</span></span>

<span data-ttu-id="a9f93-118">Recuperación del sitio recupera una lista de hello que máquinas virtuales asociadas con suscripciones de Hola y servicio de nube/grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a9f93-118">Site Recovery retrieves a list of hello VMs associated with hello subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="a9f93-119">En **máquinas virtuales**, seleccione hello las máquinas virtuales que desee tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="a9f93-119">In **Virtual Machines**, select hello VMs you want tooreplicate.</span></span>
2. <span data-ttu-id="a9f93-120">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a9f93-120">Click **OK**.</span></span>

    ![Selección de las máquinas virtuales](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="a9f93-122">Definición de la configuración</span><span class="sxs-lookup"><span data-stu-id="a9f93-122">Configure settings</span></span>

<span data-ttu-id="a9f93-123">Recuperación de sitio aprovisiona la configuración predeterminada para la región de destino de hello (basado en la configuración de región de código fuente de hello) y la directiva de replicación de hello:</span><span class="sxs-lookup"><span data-stu-id="a9f93-123">Site Recovery provisions default settings for hello target region (based on hello source region settings), and hello replication policy:</span></span>

   - <span data-ttu-id="a9f93-124">**Ubicación de destino**: región de destino de Hola que desee toouse para recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="a9f93-124">**Target location**: hello target region you want toouse for disaster recovery.</span></span> <span data-ttu-id="a9f93-125">Se recomienda que ubicación de destino de hello coincide con ubicación Hola de almacén de Site Recovery Hola.</span><span class="sxs-lookup"><span data-stu-id="a9f93-125">We recommend that hello target location matches hello location of hello Site Recovery vault.</span></span>
   - <span data-ttu-id="a9f93-126">**Grupo de recursos de destino**: grupo de recursos toowhich máquinas virtuales de Azure en la región de destino de hello pertenecerá después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="a9f93-126">**Target resource group**: Resource group toowhich Azure VMs in hello target region will belong after failover.</span></span> <span data-ttu-id="a9f93-127">De forma predeterminada, Site Recovery crea un nuevo grupo de recursos en la región de destino de hello con un sufijo "asr".</span><span class="sxs-lookup"><span data-stu-id="a9f93-127">By default, Site Recovery creates a new resource group in hello target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="a9f93-128">**Red virtual de destino**: red de hello en las máquinas virtuales de Azure en Hola se ubicarán región de destino después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="a9f93-128">**Target virtual network**: hello network in which Azure VMs in hello target region will be located after failover.</span></span> <span data-ttu-id="a9f93-129">De forma predeterminada, Site Recovery crea una nueva red virtual (y las subredes) en la región de destino de hello con un sufijo "asr".</span><span class="sxs-lookup"><span data-stu-id="a9f93-129">By default, Site Recovery creates a new virtual network (and subnets) in hello target region with an "asr" suffix.</span></span> <span data-ttu-id="a9f93-130">Esta red esté asignada tooyour red de origen.</span><span class="sxs-lookup"><span data-stu-id="a9f93-130">This network is mapped tooyour source network.</span></span> <span data-ttu-id="a9f93-131">Tenga en cuenta que puede asignar una dirección IP específica después de la conmutación por error de una máquina virtual, si necesita tooretain Hola igual de direcciones IP en las ubicaciones de origen y destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9f93-131">Note that you can assign a specific IP address after failover of a VM, if you need tooretain hello same IP address in hello source and target locations.</span></span> 
   - <span data-ttu-id="a9f93-132">**Almacenar en caché las cuentas de almacenamiento**: recuperación del sitio utiliza una cuenta de almacenamiento en región de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9f93-132">**Cache storage accounts**: Site Recovery uses a storage account in hello source region.</span></span> <span data-ttu-id="a9f93-133">Cambios en máquinas virtuales de origen se envían toothis cuenta, antes de la ubicación de destino de replicación toohello.</span><span class="sxs-lookup"><span data-stu-id="a9f93-133">Changes on source VMs are sent toothis account, before replication toohello target location.</span></span> 
   - <span data-ttu-id="a9f93-134">**Las cuentas de almacenamiento de destino**: de forma predeterminada, Site Recovery crea una nueva cuenta de almacenamiento en la región de destino de hello, origen de hello toomirror cuenta de almacenamiento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9f93-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in hello target region, toomirror hello source VM storage account.</span></span>
   -  <span data-ttu-id="a9f93-135">**Conjuntos de disponibilidad de destino**: de forma predeterminada, Site Recovery crea un nuevo conjunto de disponibilidad en región de destino de hello, con el sufijo de "asr" Hola.</span><span class="sxs-lookup"><span data-stu-id="a9f93-135">**Target availability sets**: By default, Site Recovery creates a new availability set in hello target region, with hello "asr" suffix.</span></span> 
   - <span data-ttu-id="a9f93-136">**Nombre de la directiva de replicación**: Nombre de la directiva.</span><span class="sxs-lookup"><span data-stu-id="a9f93-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="a9f93-137">**Retención del punto de recuperación**: De forma predeterminada, Site Recovery conserva los puntos de recuperación durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="a9f93-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="a9f93-138">Puede configurar un valor entre 1 y 72 horas.</span><span class="sxs-lookup"><span data-stu-id="a9f93-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="a9f93-139">**Frecuencia de instantáneas coherentes con la aplicación**: De forma predeterminada, Site Recovery toma una instantánea coherente con la aplicación cada 4 horas.</span><span class="sxs-lookup"><span data-stu-id="a9f93-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="a9f93-140">Puede configurar cualquier valor entre 1 y 12 horas.</span><span class="sxs-lookup"><span data-stu-id="a9f93-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="a9f93-141">Los datos se replican continuamente:</span><span class="sxs-lookup"><span data-stu-id="a9f93-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="a9f93-142">Los puntos de recuperación coherentes para el bloqueo mantienen una orden de escritura de datos coherente cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="a9f93-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="a9f93-143">Este tipo de punto de recuperación es generalmente es suficiente si la aplicación está diseñada toorecover desde un bloqueo sin incoherencias en los datos</span><span class="sxs-lookup"><span data-stu-id="a9f93-143">This type of recovery point is usually sufficient if your app is designed toorecover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="a9f93-144">Los puntos de recuperación coherentes para el bloqueo se generan cada pocos minutos.</span><span class="sxs-lookup"><span data-stu-id="a9f93-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="a9f93-145">Mediante estos toofail de puntos de recuperación a través de y recuperar las máquinas virtuales proporcionan un objetivo de punto de recuperación (RPO) en orden de Hola de minutos.</span><span class="sxs-lookup"><span data-stu-id="a9f93-145">Using these recovery points toofail over and recover your VMs provides a Recovery Point Objective (RPO) in hello order of minutes.</span></span>
    - <span data-ttu-id="a9f93-146">Puntos de recuperación coherente con la aplicación (en coherencia toowrite orden de adición) asegúrese de que las aplicaciones de ejecución completen todas las operaciones y vaciar búferes toodisk (modo de inactividad de aplicación).</span><span class="sxs-lookup"><span data-stu-id="a9f93-146">App-consistent recovery points (in addition toowrite-order consistency) ensure that running apps complete all operations and flush buffers toodisk (application quiescing).</span></span> <span data-ttu-id="a9f93-147">Se recomienda usar estos puntos de recuperación para aplicaciones de base de datos como SQL Server, Oracle y Exchange.</span><span class="sxs-lookup"><span data-stu-id="a9f93-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Definición de la configuración](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="a9f93-149">Modificar la configuración</span><span class="sxs-lookup"><span data-stu-id="a9f93-149">Modify settings</span></span>

<span data-ttu-id="a9f93-150">Si desea que la configuración de directiva de destino y la replicación toomodify, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a9f93-150">If you want toomodify target and replication policy settings, do hello following:</span></span>

1. <span data-ttu-id="a9f93-151">tooview o modificar la configuración de destino, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="a9f93-151">tooview or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="a9f93-152">configuración de destino de toooverride Hola predeterminado, haga clic en **personalizar**.</span><span class="sxs-lookup"><span data-stu-id="a9f93-152">toooverride hello default target settings, click **Customize**.</span></span> <span data-ttu-id="a9f93-153">Puede especificar un grupo de recursos de destino, la red virtual, el conjunto de disponibilidad y la cuenta de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="a9f93-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="a9f93-154">Solo puede agregar conjuntos de disponibilidad si las máquinas virtuales que forman parte de un conjunto en la región de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9f93-154">You can only add availability sets if VMs are part of a set in hello source region.</span></span>

    ![Definición de la configuración](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="a9f93-156">Haga clic en la configuración de puntos de recuperación y las instantáneas coherentes con la aplicación, replicación toooverride **personalizar** siguiente demasiado**directiva de replicación**.</span><span class="sxs-lookup"><span data-stu-id="a9f93-156">toooverride replication settings for recovery points and app-consistent snapshots, click **Customize** next too**Replication Policy**.</span></span>
 
    ![Definición de la configuración](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="a9f93-158">Haga clic en recursos de destino de hello aprovisionamiento toostart **crear recursos de destino**.</span><span class="sxs-lookup"><span data-stu-id="a9f93-158">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="a9f93-159">El aprovisionamiento tarda aproximadamente un minuto.</span><span class="sxs-lookup"><span data-stu-id="a9f93-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="a9f93-160">No cierre la hoja de Hola durante el aprovisionamiento o tendrá toostart sobre.</span><span class="sxs-lookup"><span data-stu-id="a9f93-160">Don't close hello blade during provisioning, or you'll have toostart over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="a9f93-161">Habilitar replicación</span><span class="sxs-lookup"><span data-stu-id="a9f93-161">Enable replication</span></span>

1. <span data-ttu-id="a9f93-162">En **Configuración**, haga clic en **Habilitar replicación**.</span><span class="sxs-lookup"><span data-stu-id="a9f93-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="a9f93-163">Esto permite la replicación inicial de hello máquinas virtuales que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="a9f93-163">This enables initial replication of hello VMs you selected.</span></span> <span data-ttu-id="a9f93-164">Estado de la replicación inicial puede tardar algún tiempo toorefresh.</span><span class="sxs-lookup"><span data-stu-id="a9f93-164">Initial replication status might take some time toorefresh.</span></span> <span data-ttu-id="a9f93-165">Haga clic en **actualizar** estado más reciente de tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="a9f93-165">Click **Refresh** tooget hello latest status.</span></span>

2. <span data-ttu-id="a9f93-166">Puede seguir el progreso del programa Hola a **habilitar la protección** de trabajo en **configuración** > **trabajos** > **trabajos de recuperación de sitio**.</span><span class="sxs-lookup"><span data-stu-id="a9f93-166">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="a9f93-167">En **configuración** > **replican elementos**, puede ver el estado de Hola de máquinas virtuales y Hola progreso de la replicación inicial.</span><span class="sxs-lookup"><span data-stu-id="a9f93-167">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="a9f93-168">Haga clic en hello VM toodrill hacia abajo en su configuración.</span><span class="sxs-lookup"><span data-stu-id="a9f93-168">Click hello VM toodrill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a9f93-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9f93-169">Next steps</span></span>

<span data-ttu-id="a9f93-170">Vaya demasiado[paso 6: ejecutar una prueba de conmutación por error](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="a9f93-170">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
