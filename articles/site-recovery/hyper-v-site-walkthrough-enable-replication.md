---
title: "la replicación para máquinas virtuales de Hyper-V replicar tooAzure (sin System Center VMM) con Azure Site Recovery aaaEnable | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooenable tooAzure de replicación para máquinas virtuales de Hyper-V con servicio de Azure Site Recovery Hola"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a><span data-ttu-id="1b25c-103">Paso 10: Habilitar replicación para replicar tooAzure de las máquinas virtuales de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="1b25c-103">Step 10: Enable replication for Hyper-V VMs replicating tooAzure</span></span>


<span data-ttu-id="1b25c-104">Este artículo describe cómo tooenable replicación local máquinas virtuales de Hyper-V (no administradas por System Center VMM) tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b25c-104">This article describes how tooenable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="1b25c-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1b25c-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="1b25c-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="1b25c-106">Before you start</span></span>

<span data-ttu-id="1b25c-107">Antes de empezar, asegúrese de que la cuenta de usuario de Azure tiene Hola necesario [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una nueva tooAzure de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1b25c-107">Before you start, ensure that your Azure user account has hello required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="1b25c-108">Excluir discos de la replicación</span><span class="sxs-lookup"><span data-stu-id="1b25c-108">Exclude disks from replication</span></span>

<span data-ttu-id="1b25c-109">De manera predeterminada, se replican todos los discos de una máquina.</span><span class="sxs-lookup"><span data-stu-id="1b25c-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="1b25c-110">Puede excluir discos de la replicación.</span><span class="sxs-lookup"><span data-stu-id="1b25c-110">You can exclude disks from replication.</span></span> <span data-ttu-id="1b25c-111">Por ejemplo, puede no ser conveniente tooreplicate discos con los datos temporales o datos que se actualizan cada vez que una máquina o reinicia la aplicación (por ejemplo, pagefile.sys o tempdb de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="1b25c-111">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="1b25c-112">Más información</span><span class="sxs-lookup"><span data-stu-id="1b25c-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="1b25c-113">Replicación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="1b25c-113">Replicate VMs</span></span>

<span data-ttu-id="1b25c-114">Habilite la replicación para máquinas virtuales como sigue:</span><span class="sxs-lookup"><span data-stu-id="1b25c-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="1b25c-115">Haga clic en **Replicar la aplicación** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="1b25c-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="1b25c-116">Una vez haya configurado la replicación para hello la primera vez, puede hacer clic en **+ replicar** tooenable replicación para máquinas adicionales.</span><span class="sxs-lookup"><span data-stu-id="1b25c-116">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="1b25c-118">En **origen**, seleccione el sitio de Hyper-V de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b25c-118">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="1b25c-119">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1b25c-119">Then click **OK**.</span></span>
3. <span data-ttu-id="1b25c-120">En **destino**, seleccione la suscripción de almacén de Hola y Hola modelo de conmutación por error que desee toouse en Azure (classic o recurso management) después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1b25c-120">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="1b25c-121">Seleccione la cuenta de almacenamiento de Hola que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="1b25c-121">Select hello storage account you want toouse.</span></span> <span data-ttu-id="1b25c-122">Si no tienes una cuenta que desee toouse, puede [crear uno](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="1b25c-122">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="1b25c-123">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1b25c-123">Then click **OK**.</span></span>
5. <span data-ttu-id="1b25c-124">Seleccione hello Azure toowhich de red y subred de máquinas virtuales de Azure se conectará cuando se crean conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1b25c-124">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="1b25c-125">Seleccione tooapply Hola configuración tooall máquinas de la red se habilita para la replicación, **configurar ahora para las máquinas seleccionadas**.</span><span class="sxs-lookup"><span data-stu-id="1b25c-125">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="1b25c-126">Seleccione **configurar más adelante** tooselect hello Azure red por máquina.</span><span class="sxs-lookup"><span data-stu-id="1b25c-126">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="1b25c-127">Si no dispone de una red que desee toouse, puede [crear uno](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="1b25c-127">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="1b25c-128">Seleccione una subred si es posible.</span><span class="sxs-lookup"><span data-stu-id="1b25c-128">Select a subnet if applicable.</span></span> <span data-ttu-id="1b25c-129">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1b25c-129">Then click **OK**.</span></span>

   ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="1b25c-131">En **máquinas virtuales** > **seleccionar las máquinas virtuales**, haga clic en y seleccione cada máquina tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="1b25c-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="1b25c-132">Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación.</span><span class="sxs-lookup"><span data-stu-id="1b25c-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="1b25c-133">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1b25c-133">Then click **OK**.</span></span>

    ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="1b25c-135">En **propiedades** > **configurar las propiedades**, seleccione sistema de operativo Hola Hola selecciona las máquinas virtuales y Hola disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="1b25c-135">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="1b25c-136">Comprueba cumple ese nombre de máquina virtual de Azure (nombre de destino) de hello [requisitos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="1b25c-136">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="1b25c-137">De forma predeterminada se seleccionan todos los discos de Hola de hello VM para la replicación.</span><span class="sxs-lookup"><span data-stu-id="1b25c-137">By default all hello disks of hello VM are selected for replication.</span></span> <span data-ttu-id="1b25c-138">Borrar discos tooexclude ellos.</span><span class="sxs-lookup"><span data-stu-id="1b25c-138">Clear disks tooexclude them.</span></span>
10. <span data-ttu-id="1b25c-139">Haga clic en **Aceptar** toosave cambios.</span><span class="sxs-lookup"><span data-stu-id="1b25c-139">Click **OK** toosave changes.</span></span> <span data-ttu-id="1b25c-140">Puede establecer propiedades adicionales más adelante.</span><span class="sxs-lookup"><span data-stu-id="1b25c-140">You can set additional properties later.</span></span>

    ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="1b25c-142">En **configuración de replicación** > **establecer configuración de replicación**, seleccione Directiva de replicación de Hola que desee tooapply para hello protegido máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1b25c-142">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="1b25c-143">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1b25c-143">Then click **OK**.</span></span> <span data-ttu-id="1b25c-144">Puede modificar la directiva de replicación de hello en **directivas de replicación** > nombre de directiva > **modificar configuración**.</span><span class="sxs-lookup"><span data-stu-id="1b25c-144">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="1b25c-145">Los cambios que aplique se utilizarán tanto para las máquinas que ya se estén replicando como para otras nuevas.</span><span class="sxs-lookup"><span data-stu-id="1b25c-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="1b25c-147">Puede seguir el progreso del programa Hola a **Habilitar protección** de trabajo en **trabajos** > **trabajos de recuperación del sitio**.</span><span class="sxs-lookup"><span data-stu-id="1b25c-147">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="1b25c-148">Después de hello **finalización de protección** ejecuciones del trabajo Hola máquina está lista para conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1b25c-148">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1b25c-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b25c-149">Next steps</span></span>


<span data-ttu-id="1b25c-150">Vaya demasiado[paso 11: ejecutar una prueba de conmutación por error](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="1b25c-150">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
