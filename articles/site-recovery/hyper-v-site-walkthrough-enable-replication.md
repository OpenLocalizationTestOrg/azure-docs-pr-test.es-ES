---
title: "Habilitar la replicación para la replicación de máquinas virtuales de Hyper-V en Azure (sin System Center VMM) con Azure Site Recovery | Microsoft Docs"
description: "Resume los pasos necesarios para habilitar la replicación en Azure para máquinas virtuales de Hyper-V con el servicio de Azure Site Recovery"
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
ms.openlocfilehash: aabe99dbd375b80e4a87ca7a067927008672b4ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-to-azure"></a><span data-ttu-id="89f3e-103">Paso 10: habilitación de la replicación para replicar máquinas virtuales de Hyper-V en Azure</span><span class="sxs-lookup"><span data-stu-id="89f3e-103">Step 10: Enable replication for Hyper-V VMs replicating to Azure</span></span>


<span data-ttu-id="89f3e-104">Este artículo describe cómo habilitar la replicación de máquinas virtuales de Hyper-V locales (no administradas por System Center VMM) en Azure, mediante el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="89f3e-104">This article describes how to enable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="89f3e-105">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="89f3e-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="89f3e-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="89f3e-106">Before you start</span></span>

<span data-ttu-id="89f3e-107">Antes de empezar, asegúrese de que la cuenta de usuario de Azure tiene los [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) necesarios para habilitar la replicación de una nueva máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="89f3e-107">Before you start, ensure that your Azure user account has the required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="89f3e-108">Excluir discos de la replicación</span><span class="sxs-lookup"><span data-stu-id="89f3e-108">Exclude disks from replication</span></span>

<span data-ttu-id="89f3e-109">De manera predeterminada, se replican todos los discos de una máquina.</span><span class="sxs-lookup"><span data-stu-id="89f3e-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="89f3e-110">Puede excluir discos de la replicación.</span><span class="sxs-lookup"><span data-stu-id="89f3e-110">You can exclude disks from replication.</span></span> <span data-ttu-id="89f3e-111">Por ejemplo, es posible que no desee replicar los discos con datos temporales, o los datos que se actualizan cada vez que una máquina o aplicación se reinicia (por ejemplo, pagefile.sys o tempdb de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="89f3e-111">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="89f3e-112">Más información</span><span class="sxs-lookup"><span data-stu-id="89f3e-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="89f3e-113">Replicación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="89f3e-113">Replicate VMs</span></span>

<span data-ttu-id="89f3e-114">Habilite la replicación para máquinas virtuales como sigue:</span><span class="sxs-lookup"><span data-stu-id="89f3e-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="89f3e-115">Haga clic en **Replicar la aplicación** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="89f3e-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="89f3e-116">Después de configurar la replicación por primera vez, haga clic en **+Replicar** para habilitar la replicación de más máquinas.</span><span class="sxs-lookup"><span data-stu-id="89f3e-116">After you've set up replication for the first time, you can click **+Replicate** to enable replication for additional machines.</span></span>

    ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="89f3e-118">En **Origen**, seleccione el sitio Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="89f3e-118">In **Source**, select the Hyper-V site.</span></span> <span data-ttu-id="89f3e-119">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="89f3e-119">Then click **OK**.</span></span>
3. <span data-ttu-id="89f3e-120">En **Destino** seleccione la suscripción de almacén y el modelo de conmutación por error que se va a utilizar en Azure (Resource Manager o clásico) después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="89f3e-120">In **Target**, select the vault subscription, and the failover model you want to use in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="89f3e-121">Seleccione la cuenta de almacenamiento que desea usar.</span><span class="sxs-lookup"><span data-stu-id="89f3e-121">Select the storage account you want to use.</span></span> <span data-ttu-id="89f3e-122">Si no tiene una cuenta que desea utilizar, puede [crear una](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="89f3e-122">If you don't have an account you want to use, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="89f3e-123">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="89f3e-123">Then click **OK**.</span></span>
5. <span data-ttu-id="89f3e-124">Seleccione la red y la subred de Azure a la que se conectarán las máquinas virtuales de Azure cuando se creen después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="89f3e-124">Select the Azure network and subnet to which Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="89f3e-125">Para aplicar la configuración de red a todas las máquinas habilitadas para replicación, seleccione la opción **Configurar ahora para las máquinas seleccionadas**.</span><span class="sxs-lookup"><span data-stu-id="89f3e-125">To apply the network settings to all machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="89f3e-126">Seleccione **Configurar más tarde** para seleccionar la red de Azure por máquina.</span><span class="sxs-lookup"><span data-stu-id="89f3e-126">Select **Configure later** to select the Azure network per machine.</span></span>
    - <span data-ttu-id="89f3e-127">Si no tiene una red que desea utilizar, puede [crear una](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="89f3e-127">If you don't have a network you want to use, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="89f3e-128">Seleccione una subred si es posible.</span><span class="sxs-lookup"><span data-stu-id="89f3e-128">Select a subnet if applicable.</span></span> <span data-ttu-id="89f3e-129">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="89f3e-129">Then click **OK**.</span></span>

   ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="89f3e-131">En **Máquinas virtuales** > **Seleccionar máquinas virtuales**, haga clic en cada máquina que desea replicar y selecciónela.</span><span class="sxs-lookup"><span data-stu-id="89f3e-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="89f3e-132">Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación.</span><span class="sxs-lookup"><span data-stu-id="89f3e-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="89f3e-133">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="89f3e-133">Then click **OK**.</span></span>

    ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="89f3e-135">En **Propiedades** > **Configurar propiedades**, seleccione el sistema operativo para las máquinas virtuales seleccionadas y el disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="89f3e-135">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>
8. <span data-ttu-id="89f3e-136">Compruebe que el nombre de la máquina virtual de Azure (nombre de destino) cumple los [requisitos de las máquinas virtuales de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="89f3e-136">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="89f3e-137">De forma predeterminada se seleccionan todos los discos de la máquina virtual para la replicación.</span><span class="sxs-lookup"><span data-stu-id="89f3e-137">By default all the disks of the VM are selected for replication.</span></span> <span data-ttu-id="89f3e-138">Borre discos para excluirlos.</span><span class="sxs-lookup"><span data-stu-id="89f3e-138">Clear disks to exclude them.</span></span>
10. <span data-ttu-id="89f3e-139">Haga clic en **Aceptar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="89f3e-139">Click **OK** to save changes.</span></span> <span data-ttu-id="89f3e-140">Puede establecer propiedades adicionales más adelante.</span><span class="sxs-lookup"><span data-stu-id="89f3e-140">You can set additional properties later.</span></span>

    ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="89f3e-142">En **Configuración de replicación** > **Establecer configuración de replicación**, seleccione la directiva de replicación que desea aplicar para las máquinas virtuales protegidas.</span><span class="sxs-lookup"><span data-stu-id="89f3e-142">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="89f3e-143">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="89f3e-143">Then click **OK**.</span></span> <span data-ttu-id="89f3e-144">Puede modificar la directiva de replicación en **Directivas de replicación** > nombre de directiva > **Editar configuración**.</span><span class="sxs-lookup"><span data-stu-id="89f3e-144">You can modify the replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="89f3e-145">Los cambios que aplique se utilizarán tanto para las máquinas que ya se estén replicando como para otras nuevas.</span><span class="sxs-lookup"><span data-stu-id="89f3e-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Habilitar replicación](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="89f3e-147">Puede hacer un seguimiento del progreso del trabajo **Habilitar protección** en **Trabajos** > **Trabajos de Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="89f3e-147">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="89f3e-148">La máquina estará preparada para la conmutación por error después de que finalice el trabajo **Finalizar la protección** .</span><span class="sxs-lookup"><span data-stu-id="89f3e-148">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="89f3e-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89f3e-149">Next steps</span></span>


<span data-ttu-id="89f3e-150">Vaya a [Paso 11: Ejecución de una conmutación por error de prueba](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="89f3e-150">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
