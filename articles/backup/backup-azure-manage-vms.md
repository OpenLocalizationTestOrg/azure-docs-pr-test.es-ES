---
title: "Administración de copias de seguridad de máquinas virtuales implementadas por Resource Manager | Microsoft Docs"
description: "Aprenda a administrar y supervisar las copias de seguridad de máquinas virtuales implementadas por Resource Manager."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 35a21cb99ca4bad124a9f764cef9da453e1fe47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="b5f1e-103">Administración de copias de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="b5f1e-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b5f1e-104">Administrar copias de seguridad de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="b5f1e-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="b5f1e-105">Administrar copias de seguridad de máquina virtual clásica</span><span class="sxs-lookup"><span data-stu-id="b5f1e-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="b5f1e-106">Este artículo proporciona orientación acerca de cómo administrar copias de seguridad de máquinas virtuales y explica la información disponible sobre alertas de copia de seguridad en el panel del portal.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-106">This article provides guidance on managing VM backups, and explains the backup alerts information available in the portal dashboard.</span></span> <span data-ttu-id="b5f1e-107">La orientación de este artículo se aplica al uso de máquinas virtuales con almacenes de Servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-107">The guidance in this article applies to using VMs with Recovery Services vaults.</span></span> <span data-ttu-id="b5f1e-108">Este artículo no trata sobre la creación de máquinas virtuales ni explica cómo protegerlas.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-108">This article does not cover the creation of virtual machines, nor does it explain how to protect virtual machines.</span></span> <span data-ttu-id="b5f1e-109">Para ver una introducción sobre la protección de las máquinas virtuales implementadas por Azure Resource Manager en Azure con un almacén de Servicios de recuperación, consulte [Primer análisis: copia de seguridad de máquinas virtuales con ARM en un almacén de Servicios de recuperación](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b5f1e-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="b5f1e-110">Administración de almacenes y máquinas virtuales protegidas</span><span class="sxs-lookup"><span data-stu-id="b5f1e-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="b5f1e-111">En el Portal de Azure, el panel Almacén de Servicios de recuperación proporciona acceso a información sobre el almacén, como:</span><span class="sxs-lookup"><span data-stu-id="b5f1e-111">In the Azure portal, the Recovery Services vault dashboard provides access to information about the vault including:</span></span>

* <span data-ttu-id="b5f1e-112">la instantánea de copia de seguridad más reciente, que también es el último punto de restauración <br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-112">the most recent backup snapshot, which is also the latest restore point <br\></span></span>
* <span data-ttu-id="b5f1e-113">la directiva de copia de seguridad <br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-113">the backup policy <br\></span></span>
* <span data-ttu-id="b5f1e-114">el tamaño total de todas las instantáneas de copia de seguridad <br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="b5f1e-115">número de máquinas virtuales que están protegidas con el almacén <br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-115">number of virtual machines that are protected with the vault <br\></span></span>

<span data-ttu-id="b5f1e-116">Muchas tareas de administración con una copia de seguridad de máquina virtual comienzan con la apertura del almacén en el panel.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-116">Many management tasks with a virtual machine backup begin with opening the vault in the dashboard.</span></span> <span data-ttu-id="b5f1e-117">Sin embargo, dado que los almacenes sirven para proteger varios elementos (o varias máquinas virtuales), para ver los detalles sobre una máquina virtual determinada, abra el panel del elemento del almacén.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-117">However, because vaults can be used to protect multiple items (or multiple VMs), to view details about a particular VM, open the vault item dashboard.</span></span> <span data-ttu-id="b5f1e-118">El procedimiento siguiente muestra cómo abrir el *panel del almacén* y, después, pasar al *panel del elemento del almacén*.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-118">The following procedure shows you how to open the *vault dashboard* and then continue to the *vault item dashboard*.</span></span> <span data-ttu-id="b5f1e-119">En ambos procedimientos, se ofrecen "sugerencias" sobre cómo agregar el almacén y el elemento del almacén al Panel de Azure con el comando Anclar al panel.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-119">There are "tips" in both procedures that point out how to add the vault and vault item to the Azure dashboard by using the Pin to dashboard command.</span></span> <span data-ttu-id="b5f1e-120">La opción Anclar al panel es una manera de crear un acceso directo al almacén o al elemento.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-120">Pin to dashboard is a way of creating a shortcut to the vault or item.</span></span> <span data-ttu-id="b5f1e-121">También puede ejecutar comandos habituales desde el acceso directo.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-121">You can also execute common commands from the shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="b5f1e-122">Si tiene varios paneles y hojas abiertos, use el control deslizante azul oscuro en la parte inferior de la ventana para deslizar el Panel de Azure hacia delante y hacia atrás.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-122">If you have multiple dashboards and blades open, use the dark-blue slider at the bottom of the window to slide the Azure dashboard back and forth.</span></span>
>
>

![Vista completa con control deslizante](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-the-dashboard"></a><span data-ttu-id="b5f1e-124">Apertura de un almacén de Servicios de recuperación en el panel:</span><span class="sxs-lookup"><span data-stu-id="b5f1e-124">Open a Recovery Services vault in the dashboard:</span></span>
1. <span data-ttu-id="b5f1e-125">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b5f1e-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b5f1e-126">En el menú del centro, haga clic en **Examinar** y, en la lista de recursos, escriba **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-126">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="b5f1e-127">Cuando comience a escribir, la lista se filtrará en función de la entrada.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-127">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="b5f1e-128">Haga clic en **Almacén de Servicios de recuperación**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-128">Click **Recovery Services vault**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="b5f1e-130">Se muestra la lista de almacenes de Servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-130">The list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="b5f1e-131">Lista de almacenes de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="b5f1e-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="b5f1e-132">Si ancla un almacén al Panel de Azure, ese almacén es accesible de inmediato cuando abra el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-132">If you pin a vault to the Azure Dashboard, that vault is immediately accessible when you open the Azure portal.</span></span> <span data-ttu-id="b5f1e-133">Para anclar un almacén al panel, en la lista de almacenes, haga clic con el botón derecho en el almacén y seleccione **Anclar al panel**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-133">To pin a vault to the dashboard, in the vault list, right-click the vault, and select **Pin to dashboard**.</span></span>
   >
   >
3. <span data-ttu-id="b5f1e-134">En la lista de almacenes, seleccione el almacén para abrir su panel.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-134">From the list of vaults, select the vault to open its dashboard.</span></span> <span data-ttu-id="b5f1e-135">Cuando selecciona el almacén, se abren el panel del almacén y la hoja **Configuración** .</span><span class="sxs-lookup"><span data-stu-id="b5f1e-135">When you select the vault, the vault dashboard and the **Settings** blade open.</span></span> <span data-ttu-id="b5f1e-136">En la siguiente imagen, el panel de **Contoso-vault** aparece resaltado.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-136">In the following image, the **Contoso-vault** dashboard is highlighted.</span></span>

    ![Abrir el panel del almacén y la hoja Configuración](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="b5f1e-138">Apertura del panel de un elemento del almacén</span><span class="sxs-lookup"><span data-stu-id="b5f1e-138">Open a vault item dashboard</span></span>
<span data-ttu-id="b5f1e-139">En el procedimiento anterior, abrió el panel del almacén.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-139">In the previous procedure you opened the vault dashboard.</span></span> <span data-ttu-id="b5f1e-140">Para abrir el panel de un elemento del almacén:</span><span class="sxs-lookup"><span data-stu-id="b5f1e-140">To open the vault item dashboard:</span></span>

1. <span data-ttu-id="b5f1e-141">En el panel del almacén, en el icono **Elementos de copia de seguridad**, haga clic en **Azure Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-141">In the vault dashboard, on the **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Abrir el icono Elementos de copia de seguridad](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="b5f1e-143">En la hoja **Elementos de copia de seguridad** , se muestra el último trabajo de copia de seguridad para cada elemento.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-143">The **Backup Items** blade lists the last backup job for each item.</span></span> <span data-ttu-id="b5f1e-144">En este ejemplo, hay una máquina virtual, demovm-markgal, protegida por este almacén.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Icono Elementos de copia de seguridad](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="b5f1e-146">Para facilitar el acceso, puede anclar un elemento del almacén en el Panel de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-146">For ease of access, you can pin a vault item to the Azure Dashboard.</span></span> <span data-ttu-id="b5f1e-147">Para anclar un elemento del almacén, en la lista de elementos de almacén, haga clic con el botón derecho en el elemento y seleccione **Anclar al panel**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-147">To pin a vault item, in the vault item list, right-click the item and select **Pin to dashboard**.</span></span>
   >
   >
2. <span data-ttu-id="b5f1e-148">En la hoja **Elementos de copia de seguridad** , haga clic en el elemento para abrir el panel del elemento del almacén.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-148">In the **Backup Items** blade, click the item to open the vault item dashboard.</span></span>

    ![Icono Elementos de copia de seguridad](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="b5f1e-150">Se abren el panel del elemento de almacén y su hoja **Configuración** .</span><span class="sxs-lookup"><span data-stu-id="b5f1e-150">The vault item dashboard and its **Settings** blade open.</span></span>

    ![Panel Elementos de copia de seguridad con hoja Configuración](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="b5f1e-152">En el panel del elemento del almacén, puede llevar a cabo muchas tareas de administración claves, como:</span><span class="sxs-lookup"><span data-stu-id="b5f1e-152">From the vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="b5f1e-153">cambiar de directiva o crear una directiva de copia de seguridad<br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="b5f1e-154">ver los puntos de restauración y su estado de coherencia <br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="b5f1e-155">copia de seguridad a petición de una máquina virtual <br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="b5f1e-156">detener la protección de máquinas virtuales <br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="b5f1e-157">reanudar la protección de una máquina virtual <br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="b5f1e-158">eliminar los datos de una copia de seguridad (o un punto de recuperación) <br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="b5f1e-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="b5f1e-160">Para los procedimientos siguientes, el punto de partida es el panel del elemento del almacén.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-160">For the following procedures, the starting point is the vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="b5f1e-161">Administrar directivas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b5f1e-161">Manage backup policies</span></span>
1. <span data-ttu-id="b5f1e-162">En el [panel del elemento del almacén](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **Toda la configuración** para abrir la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-162">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** to open the **Settings** blade.</span></span>

    ![Hoja Directiva de copia de seguridad](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="b5f1e-164">En la hoja **Configuración**, haga clic en **Directiva de copia de seguridad** para abrir esa hoja.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-164">On the **Settings** blade, click **Backup policy** to open that blade.</span></span>

    <span data-ttu-id="b5f1e-165">En la hoja, se muestran los detalles de frecuencia de copia de seguridad y duración de retención.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-165">On the blade, the backup frequency and retention range details are shown.</span></span>

    ![Hoja Directiva de copia de seguridad](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="b5f1e-167">En el menú **Elegir directiva de copia de seguridad** :</span><span class="sxs-lookup"><span data-stu-id="b5f1e-167">From the **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="b5f1e-168">Para cambiar de directiva, seleccione una directiva diferente y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-168">To change policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="b5f1e-169">La nueva directiva se aplica inmediatamente en el almacén.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-169">The new policy is immediately applied to the vault.</span></span> <span data-ttu-id="b5f1e-170"><br\></span><span class="sxs-lookup"><span data-stu-id="b5f1e-170"><br\></span></span>
   * <span data-ttu-id="b5f1e-171">Para crear una directiva, seleccione **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-171">To create a policy, select **Create New**.</span></span>

     ![Copia de seguridad de máquina virtual](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="b5f1e-173">Si quiere instrucciones para crear una directiva de copia de seguridad, consulte [Definición de una directiva de copia de seguridad](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="b5f1e-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="b5f1e-174">Al administrar las directivas de copia de seguridad, asegúrese de seguir los [procedimientos recomendados](backup-azure-vms-introduction.md#best-practices) para obtener el máximo rendimiento de las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-174">While managing backup policies, make sure to follow the [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="b5f1e-175">Copia de seguridad a petición de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b5f1e-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="b5f1e-176">Puede realizar una copia de seguridad a petición de una máquina virtual una vez que esta esté configurada para la protección.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="b5f1e-177">Si está pendiente la copia de seguridad inicial, la copia de seguridad a petición creará una copia completa de la máquina virtual en el almacén de Servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-177">If the initial backup is pending, on-demand backup creates a full copy of the virtual machine in the Recovery Services vault.</span></span> <span data-ttu-id="b5f1e-178">Si se ha completado la copia de seguridad inicial, una copia de seguridad a petición solo enviará los cambios respecto a la instantánea anterior al almacén de Servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-178">If the initial backup is completed, an on-demand backup will only send changes from the previous snapshot, to the Recovery Services vault.</span></span> <span data-ttu-id="b5f1e-179">Es decir, las copias de seguridad posteriores siempre son incrementales.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="b5f1e-180">La duración de retención para una copia de seguridad a petición es el valor de retención especificado para el punto de copia de seguridad diaria en la directiva.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-180">The retention range for an on-demand backup is the retention value specified for the Daily backup point in the policy.</span></span> <span data-ttu-id="b5f1e-181">Si no se selecciona ningún punto de copia de seguridad diaria, se usa el semanal.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-181">If no Daily backup point is selected, then the weekly backup point is used.</span></span>
>
>

<span data-ttu-id="b5f1e-182">Para desencadenar la copia de seguridad a petición de una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="b5f1e-182">To trigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="b5f1e-183">En el [panel del elemento del almacén](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **Realizar copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-183">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Botón Realizar copia de seguridad ahora](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="b5f1e-185">El portal se asegura de que desea iniciar un trabajo de copia de seguridad a petición.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-185">The portal makes sure that you want to start an on-demand backup job.</span></span> <span data-ttu-id="b5f1e-186">Haga clic en **Sí** para iniciar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-186">Click **Yes** to start the backup job.</span></span>

    ![Botón Realizar copia de seguridad ahora](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="b5f1e-188">El trabajo de copia de seguridad crea un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-188">The backup job creates a recovery point.</span></span> <span data-ttu-id="b5f1e-189">La duración de retención del punto de recuperación será la misma que la especificada en la directiva asociada a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-189">The retention range of the recovery point is the same as retention range specified in the policy associated with the virtual machine.</span></span> <span data-ttu-id="b5f1e-190">Para realizar un seguimiento del progreso del trabajo, en el panel del almacén, haga clic en el icono **Trabajos de copia de seguridad** .</span><span class="sxs-lookup"><span data-stu-id="b5f1e-190">To track the progress for the job, in the vault dashboard, click the **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="b5f1e-191">Detener la protección de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="b5f1e-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="b5f1e-192">Si opta por dejar de proteger una máquina virtual, se le pregunta si desea conservar los puntos de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-192">If you choose to stop protecting a virtual machine, you are asked if you want to retain the recovery points.</span></span> <span data-ttu-id="b5f1e-193">Hay dos formas de dejar de proteger máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="b5f1e-193">There are two ways to stop protecting virtual machines:</span></span>

* <span data-ttu-id="b5f1e-194">detener todos los trabajos futuros de copia de seguridad y eliminar todos los puntos de recuperación, o</span><span class="sxs-lookup"><span data-stu-id="b5f1e-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="b5f1e-195">detener todos los trabajos futuros de copia de seguridad pero dejar los puntos de recuperación </span><span class="sxs-lookup"><span data-stu-id="b5f1e-195">stop all future backup jobs but leave the recovery points</span></span> <br/>

<span data-ttu-id="b5f1e-196">Dejar los puntos de recuperación almacenados conlleva un costo.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-196">There is a cost associated with leaving the recovery points in storage.</span></span> <span data-ttu-id="b5f1e-197">Sin embargo, la ventaja de dejarlos es que puede restaurar la máquina virtual más adelante, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-197">However, the benefit of leaving the recovery points is you can restore the virtual machine later, if desired.</span></span> <span data-ttu-id="b5f1e-198">Para más información acerca del costo de dejar los puntos de recuperación, consulte la [información sobre precios](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="b5f1e-198">For information about the cost of leaving the recovery points, see the  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="b5f1e-199">Si opta por eliminar todos los puntos de recuperación, no podrá restaurar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-199">If you choose to delete all recovery points, you cannot restore the virtual machine.</span></span>

<span data-ttu-id="b5f1e-200">Para detener la protección de una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="b5f1e-200">To stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="b5f1e-201">En el [panel del elemento del almacén](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **Detener copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-201">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Botón Detener copia de seguridad](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="b5f1e-203">Se abre la hoja Detener copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-203">The Stop Backup blade opens.</span></span>

    ![Hoja Detener copia de seguridad](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="b5f1e-205">En la hoja **Detener copia de seguridad** , elija si desea conservar o eliminar los datos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-205">On the **Stop Backup** blade, choose whether to retain or delete the backup data.</span></span> <span data-ttu-id="b5f1e-206">El cuadro de información proporciona detalles acerca de su elección.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-206">The information box provides details about your choice.</span></span>

    ![Detener protección](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="b5f1e-208">Si decide conservar los datos de copia de seguridad, vaya al paso 4.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-208">If you chose to retain the backup data, skip to step 4.</span></span> <span data-ttu-id="b5f1e-209">Si opta por eliminar los datos de copia de seguridad, confirme que desea detener los trabajos de copia de seguridad y eliminar los puntos de recuperación. Escriba el nombre del elemento.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-209">If you chose to delete backup data, confirm that you want to stop the backup jobs and delete the recovery points - type the name of the item.</span></span>

    ![Comprobación de la detención](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="b5f1e-211">Si no está seguro del nombre, mantenga el mouse sobre el signo de exclamación para verlo.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-211">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="b5f1e-212">Además, el nombre del elemento aparece debajo de **Detener copia de seguridad** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-212">Also, the name of the item is under **Stop Backup** at the top of the blade.</span></span>
4. <span data-ttu-id="b5f1e-213">Opcionalmente, añada un valor a los campos **Motivo** o **Comentario**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="b5f1e-214">Para detener el trabajo de copia de seguridad para el elemento actual, haga clic en ![botón de Detener copia de seguridad](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="b5f1e-214">To stop the backup job for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="b5f1e-215">Un mensaje de notificación le confirma que se han detenido los trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-215">A notification message lets you know the backup jobs have been stopped.</span></span>

    ![Confirmación de la detención de la protección](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="b5f1e-217">Reanudación de la protección de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b5f1e-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="b5f1e-218">Si se eligió la opción **Retener datos de copia de seguridad** cuando se detuvo la protección de la máquina virtual, es posible reanudar la protección.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-218">If the **Retain Backup Data** option was chosen when protection for the virtual machine was stopped, then it is possible to resume protection.</span></span> <span data-ttu-id="b5f1e-219">Si se eligió la opción **Eliminar datos de copia de seguridad** , no se puede reanudar la protección de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-219">If the **Delete Backup Data** option was chosen, then protection for the virtual machine cannot resume.</span></span>

<span data-ttu-id="b5f1e-220">Para reanudar la protección de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b5f1e-220">To resume protection for the virtual machine</span></span>

1. <span data-ttu-id="b5f1e-221">En el [panel del elemento del almacén](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **Reanudar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-221">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Reanudar protección](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="b5f1e-223">Se abre la hoja Directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-223">The Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b5f1e-224">Al volver a proteger la máquina virtual, puede elegir una directiva diferente de la directiva con la que estaba protegida inicialmente la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-224">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="b5f1e-225">Siga los pasos de [Administrar directivas de copia de seguridad](backup-azure-manage-vms.md#manage-backup-policies) para asignar la directiva para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-225">Follow the steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) to assign the policy for the virtual machine.</span></span>

    <span data-ttu-id="b5f1e-226">Una vez que se aplique la directiva de copia de seguridad a la máquina virtual, verá el mensaje siguiente.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-226">Once the backup policy is applied to the virtual machine, you see the following message.</span></span>

    ![Máquina virtual protegida correctamente](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="b5f1e-228">Eliminar datos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b5f1e-228">Delete Backup data</span></span>
<span data-ttu-id="b5f1e-229">Puede eliminar los datos de copia de seguridad asociados a una máquina virtual durante el trabajo **Detener copia de seguridad** o en cualquier momento una vez finalizados los trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-229">You can delete the backup data associated with a virtual machine during the **Stop backup** job, or anytime after the backup job has completed.</span></span> <span data-ttu-id="b5f1e-230">Incluso puede resultar útil esperar días o semanas antes de eliminar los puntos de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-230">It may even be beneficial to wait days or weeks before deleting the recovery points.</span></span> <span data-ttu-id="b5f1e-231">A diferencia de la restauración de puntos de recuperación, cuando se eliminan datos de copia de seguridad, no se pueden elegir los puntos de recuperación específicos que se van a eliminar.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points to delete.</span></span> <span data-ttu-id="b5f1e-232">Si elige eliminar los datos de copia de seguridad, se eliminarán todos los puntos de recuperación asociados con el elemento.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-232">If you choose to delete your backup data, you delete all recovery points associated with the item.</span></span>

<span data-ttu-id="b5f1e-233">En el siguiente procedimiento se da por sentado que el trabajo de copia de seguridad de la máquina virtual se ha detenido o deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-233">The following procedure assumes the Backup job for the virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="b5f1e-234">Una vez que se haya deshabilitado el trabajo de Backup, las opciones **Reanudar copia de seguridad** y **Eliminar copia de seguridad** en el panel del elemento del almacén.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-234">Once the Backup job is disabled, the **Resume backup** and **Delete backup** options are available in the vault item dashboard.</span></span>

![Botones Reanudar y Eliminar](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="b5f1e-236">Para eliminar datos de copia de seguridad en una máquina virtual con la *copia de seguridad deshabilitada*:</span><span class="sxs-lookup"><span data-stu-id="b5f1e-236">To delete backup data on a virtual machine with the *Backup disabled*:</span></span>

1. <span data-ttu-id="b5f1e-237">En el [panel del elemento del almacén](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **Delete backup**(Eliminar copia de seguridad).</span><span class="sxs-lookup"><span data-stu-id="b5f1e-237">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="b5f1e-239">Se abre la hoja **Eliminar datos de copia de seguridad** .</span><span class="sxs-lookup"><span data-stu-id="b5f1e-239">The **Delete Backup Data** blade opens.</span></span>

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="b5f1e-241">Escriba el nombre del elemento para confirmar que desea eliminar los puntos de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-241">Type the name of the item to confirm you want to delete the recovery points.</span></span>

    ![Comprobación de la detención](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="b5f1e-243">Si no está seguro del nombre, mantenga el mouse sobre el signo de exclamación para verlo.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-243">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="b5f1e-244">Además, el nombre del elemento aparece debajo de **Eliminar datos de copia de seguridad** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-244">Also, the name of the item is under **Delete Backup Data** at the top of the blade.</span></span>
3. <span data-ttu-id="b5f1e-245">Opcionalmente, añada un valor a los campos **Motivo** o **Comentario**.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="b5f1e-246">Para eliminar los datos de copia de seguridad para el elemento actual, haga clic en ![botón de Detener copia de seguridad](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="b5f1e-246">To delete the backup data for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="b5f1e-247">Un mensaje de notificación le confirma que se han eliminado los datos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b5f1e-247">A notification message lets you know the backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5f1e-248">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5f1e-248">Next steps</span></span>
<span data-ttu-id="b5f1e-249">Para información sobre cómo volver a crear una máquina virtual a partir de un punto de recuperación, consulte [Restauración de máquinas virtuales en Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="b5f1e-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="b5f1e-250">Si necesita información sobre la protección de las máquinas virtuales, consulte [Primer análisis: copia de seguridad de máquinas virtuales con ARM en un almacén de Servicios de recuperación](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b5f1e-250">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="b5f1e-251">Para más información sobre la supervisión de eventos, consulte [Supervisión de alertas de copias de seguridad de máquinas virtuales de Azure](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="b5f1e-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
