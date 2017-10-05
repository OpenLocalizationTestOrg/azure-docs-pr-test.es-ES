---
title: "Administración y supervisión de copias de seguridad de máquinas virtuales de Azure | Microsoft Docs"
description: "Aprenda a administrar y supervisar las copias de seguridad de máquinas virtuales de Azure"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d876bb1759600fa29a26730bfa8b4ec19db1e442
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-the-classic-portal"></a><span data-ttu-id="6d9df-103">Administración de trabajos comunes de copia de seguridad de Azure y desencadenado de alertas en el Portal clásico</span><span class="sxs-lookup"><span data-stu-id="6d9df-103">Manage common Azure Backup jobs and trigger alerts in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d9df-104">Administrar copias de seguridad de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="6d9df-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="6d9df-105">Administrar copias de seguridad de máquina virtual clásica</span><span class="sxs-lookup"><span data-stu-id="6d9df-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="6d9df-106">Este artículo proporciona información acerca de las tareas de administración y supervisión comunes para las máquinas virtuales de modelo clásico protegidas en Azure.</span><span class="sxs-lookup"><span data-stu-id="6d9df-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="6d9df-107">Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6d9df-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6d9df-108">Consulte [Preparación del entorno de copia de seguridad de máquinas virtuales de Azure](backup-azure-vms-prepare.md) para más información sobre cómo trabajar con las máquinas virtuales del modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="6d9df-108">See [Prepare your environment to back up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="6d9df-109">A partir de marzo de 2017, ya no podrá usar el portal clásico para crear almacenes de Backup.</span><span class="sxs-lookup"><span data-stu-id="6d9df-109">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
>
> <span data-ttu-id="6d9df-110">Ahora puede actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="6d9df-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="6d9df-111">Para más información, consulte el artículo [Actualización de un almacén de Backup a un almacén de Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="6d9df-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="6d9df-112">Microsoft anima a actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="6d9df-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="6d9df-113">A partir del 15 de octubre de 2017, no podrá usar PowerShell para crear almacenes de Backup.</span><span class="sxs-lookup"><span data-stu-id="6d9df-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="6d9df-114">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="6d9df-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="6d9df-115">Todos los almacenes de Backup restantes se actualizarán automáticamente a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="6d9df-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="6d9df-116">No podrá acceder a los datos de copia de seguridad en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="6d9df-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="6d9df-117">En su lugar, utilice Azure Portal para tener acceso a los datos de copia de seguridad en los almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="6d9df-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="6d9df-118">Administrar máquinas virtuales protegidas</span><span class="sxs-lookup"><span data-stu-id="6d9df-118">Manage protected virtual machines</span></span>
<span data-ttu-id="6d9df-119">Para administrar máquinas virtuales protegidas:</span><span class="sxs-lookup"><span data-stu-id="6d9df-119">To manage protected virtual machines:</span></span>

1. <span data-ttu-id="6d9df-120">Para ver y administrar la configuración de copia de seguridad para una máquina virtual, haga clic en la pestaña **Elementos protegidos** .</span><span class="sxs-lookup"><span data-stu-id="6d9df-120">To view and manage backup settings for a virtual machine click the **Protected Items** tab.</span></span>
2. <span data-ttu-id="6d9df-121">Haga clic en el nombre de un elemento protegido para ver la pestaña **Detalles de copia de seguridad** , que muestra información acerca de la última copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6d9df-121">Click on the name of a protected item to see the **Backup Details** tab, which shows you information about the last backup.</span></span>

    ![Copia de seguridad de máquina virtual](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="6d9df-123">Para ver y administrar la configuración de directiva de copia de seguridad para una máquina virtual, haga clic en la pestaña **Directivas** .</span><span class="sxs-lookup"><span data-stu-id="6d9df-123">To view and manage backup policy settings for a virtual machine click the **Policies** tab.</span></span>

    ![Directiva de máquina virtual](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="6d9df-125">La pestaña **Directivas de copia de seguridad** muestra la directiva existente.</span><span class="sxs-lookup"><span data-stu-id="6d9df-125">The **Backup Policies** tab shows you the existing policy.</span></span> <span data-ttu-id="6d9df-126">Se puede modificar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6d9df-126">You can modify as needed.</span></span> <span data-ttu-id="6d9df-127">Si necesita crear una nueva directiva, haga clic en **Crear** en la página **Directivas**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-127">If you need to create a new policy click **Create** on the **Policies** page.</span></span> <span data-ttu-id="6d9df-128">Tenga en cuenta que si desea quitar una directiva no debería tener ninguna máquina virtual asociada a esta.</span><span class="sxs-lookup"><span data-stu-id="6d9df-128">Note that if you want to remove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Directiva de máquina virtual](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="6d9df-130">Puede obtener más información sobre las acciones o el estado de una máquina virtual en la página **Trabajos** .</span><span class="sxs-lookup"><span data-stu-id="6d9df-130">You can get more information about actions or status for a virtual machine on the **Jobs** page.</span></span> <span data-ttu-id="6d9df-131">Haga clic en un trabajo en la lista para obtener más detalles, o filtre los trabajos de una máquina virtual específica.</span><span class="sxs-lookup"><span data-stu-id="6d9df-131">Click a job in the list to get more details, or filter jobs for a specific virtual machine.</span></span>

    ![Trabajos](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="6d9df-133">Copia de seguridad a petición de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6d9df-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="6d9df-134">Puede realizar una copia de seguridad a petición de una máquina virtual una vez que esta esté configurada para la protección.</span><span class="sxs-lookup"><span data-stu-id="6d9df-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="6d9df-135">Si está pendiente la copia de seguridad inicial para la máquina virtual, la copia de seguridad a petición creará una copia completa de la máquina virtual en el almacén de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d9df-135">If the initial backup is pending for the virtual machine, on-demand backup will create a full copy of the virtual machine in Azure backup vault.</span></span> <span data-ttu-id="6d9df-136">Si se ha realizado la primera copia de seguridad, la copia de seguridad a petición solo enviará al almacén de copia de seguridad de Azure los cambios que se hayan realizado desde la copia de seguridad anterior, es decir, siempre es incremental.</span><span class="sxs-lookup"><span data-stu-id="6d9df-136">If first backup is completed, on-demand backup will only send changes from previous backup to Azure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="6d9df-137">El intervalo de retención de una copia de seguridad a petición se establece en el valor de retención especificado para la retención diaria en la directiva de copia de seguridad correspondiente a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d9df-137">Retention range of an on-demand backup is set to retention value specified for Daily retention in backup policy corresponding to the VM.</span></span>  
>
>

<span data-ttu-id="6d9df-138">Para realizar una copia de seguridad a petición de una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="6d9df-138">To take an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="6d9df-139">Vaya a la página **Elementos protegidos** y elija **Máquina virtual de Azure** como valor del campo **Tipo** (si no está ya seleccionado) y haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-139">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="6d9df-141">Seleccione la máquina virtual de la que desea realizar copia de seguridad a petición. A continuación, haga clic en el botón **Copia de seguridad ahora**, situado en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="6d9df-141">Select the virtual machine on which you want to take an on-demand backup and click on **Backup Now** button at the bottom of the page.</span></span>

    ![Copia de seguridad ahora](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="6d9df-143">Esto creará un trabajo de copia de seguridad en la máquina virtual seleccionada.</span><span class="sxs-lookup"><span data-stu-id="6d9df-143">This will create a backup job on the selected virtual machine.</span></span> <span data-ttu-id="6d9df-144">El periodo de retención del punto de recuperación creado con este trabajo será el mismo que el especificado en la directiva asociada a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d9df-144">Retention range of recovery point created through this job will be same as that specified in the policy associated with the virtual machine.</span></span>

    ![Creación de trabajo de copia de seguridad](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="6d9df-146">Para ver la directiva asociada a una máquina virtual, acceda a la máquina virtual en la página **Elementos protegidos** y vaya a la pestaña de la directiva de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6d9df-146">To view the policy associated with a virtual machine, drill down into virtual machine in the **Protected Items** page and go to backup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="6d9df-147">Una vez que se crea el trabajo, puede hacer clic en el botón **Ver trabajo** de la barra de notificación del sistema para ver el trabajo correspondiente en la página de los trabajos.</span><span class="sxs-lookup"><span data-stu-id="6d9df-147">Once the job is created, you can click on **View job** button in the toast bar to see the corresponding job in the jobs page.</span></span>

    ![Trabajo de copia de seguridad creado](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="6d9df-149">Tras finalizar correctamente el trabajo, se creará un punto de recuperación que puede utilizar para restaurar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d9df-149">After successful completion of the job, a recovery point will be created which you can use to restore the virtual machine.</span></span> <span data-ttu-id="6d9df-150">Esto también incrementará el valor de la columna del punto de recuperación en 1 unidad en la página **Elementos protegidos** .</span><span class="sxs-lookup"><span data-stu-id="6d9df-150">This will also increment the recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="6d9df-151">Detener la protección de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="6d9df-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="6d9df-152">Puede detener las futuras copias de seguridad de una máquina virtual con las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="6d9df-152">You can choose to stop the future backups of a virtual machine with the following options:</span></span>

* <span data-ttu-id="6d9df-153">Conservar los datos de copia de seguridad asociados a la máquina virtual en el almacén de copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="6d9df-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="6d9df-154">Eliminación de datos de copia de seguridad asociados a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6d9df-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="6d9df-155">Si ha seleccionado la opción de conservar los datos de copia de seguridad asociados a la máquina virtual, puede usar estos datos para restaurar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d9df-155">If you have selected to retain backup data associated with virtual machine, you can use the backup data to restore the virtual machine.</span></span> <span data-ttu-id="6d9df-156">Para obtener más detalles sobre el precio de estas máquinas virtuales, haga clic [aquí](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="6d9df-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="6d9df-157">Para detener la protección de una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="6d9df-157">To Stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="6d9df-158">Vaya a la página **Elementos protegidos** y elija **Máquina virtual de Azure** como tipo de filtro (si no está ya seleccionado) y haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-158">Navigate to **Protected Items** page and select **Azure virtual machine** as the filter type (if not already selected) and click on **Select** button.</span></span>

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="6d9df-160">Elija la máquina virtual y haga clic en **Detener protección** , en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="6d9df-160">Select the virtual machine and click on **Stop Protection** at the bottom of the page.</span></span>

    ![Detener protección](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="6d9df-162">De forma predeterminada, la copia de seguridad de Azure no elimina los datos de copia de seguridad asociados a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d9df-162">By default, Azure Backup doesn’t delete the backup data associated with the virtual machine.</span></span>

    ![Confirmación de la detención de la protección](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="6d9df-164">Si desea eliminar los datos de copia de seguridad, active la casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="6d9df-164">If you want to delete backup data, select the check box.</span></span>

    ![Casilla de verificación](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="6d9df-166">Especifique un motivo para detener la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6d9df-166">Please select a reason for stopping the backup.</span></span> <span data-ttu-id="6d9df-167">Aunque esto es opcional, proporcionar un motivo ayudará a Copia de seguridad de Azure a trabajar en los comentarios y dar prioridad a los escenarios del cliente.</span><span class="sxs-lookup"><span data-stu-id="6d9df-167">While this is optional, providing a reason will help Azure Backup to work on the feedback and prioritize the customer scenarios.</span></span>
4. <span data-ttu-id="6d9df-168">Haga clic en el botón **Enviar** para enviar el trabajo **Detener protección**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-168">Click on **Submit** button to submit the **Stop protection** job.</span></span> <span data-ttu-id="6d9df-169">Haga clic en **Ver trabajo** para ver el trabajo correspondiente en la página **Trabajos**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-169">Click on **View Job** to see the corresponding the job in **Jobs** page.</span></span>

    ![Detener protección](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="6d9df-171">Si no ha elegido la opción **Eliminar datos de copia de seguridad asociados** en el asistente **Detener protección**, publique los cambios del estado de protección y la finalización del trabajo en **Protección detenida**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes to **Protection Stopped**.</span></span> <span data-ttu-id="6d9df-172">Los datos permanecen en Copia de seguridad de Azure hasta que se eliminen explícitamente.</span><span class="sxs-lookup"><span data-stu-id="6d9df-172">The data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="6d9df-173">Para eliminar los datos, seleccione la máquina virtual en la página **Elementos protegidos** y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-173">You can always delete the data by selecting the virtual machine in the **Protected Items** page and clicking **Delete**.</span></span>

    ![Protección detenida](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="6d9df-175">Si ha elegido la opción **Eliminar datos de copia de seguridad asociados**, la máquina virtual no formará parte de la página **Elementos protegidos**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-175">If you have selected the **Delete associated backup data** option, the virtual machine won’t be part of the **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="6d9df-176">Volver a proteger la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6d9df-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="6d9df-177">Si no ha elegido la opción **Eliminar datos de copia de seguridad asociados** en **Detener protección**, puede volver a proteger la máquina virtual siguiendo unos pasos similares a los de la copia de seguridad de las máquinas virtuales registradas.</span><span class="sxs-lookup"><span data-stu-id="6d9df-177">If you have not selected the **Delete associate backup data** option in **Stop Protection**, you can re-protect the virtual machine by following the steps similar to backing up registered virtual machines.</span></span> <span data-ttu-id="6d9df-178">Una vez protegida, esta máquina virtual conservará los datos de copia de seguridad antes de detener la protección, así como los puntos de recuperación creados después de aplicar de nuevo la protección.</span><span class="sxs-lookup"><span data-stu-id="6d9df-178">Once protected, this virtual machine will have backup data retained prior to stop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="6d9df-179">Después de aplicar de nuevo la protección, el estado de protección de la máquina virtual cambiará a **Protegida** si hay puntos de recuperación anteriores a la **detención de la protección**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-179">After re-protect, the virtual machine’s protection status will be changed to **Protected** if there are recovery points prior to **Stop Protection**.</span></span>

  ![Máquina virtual protegida de nuevo](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="6d9df-181">Al volver a proteger la máquina virtual, puede elegir una directiva diferente de la directiva con la que estaba protegida inicialmente la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d9df-181">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="6d9df-182">Anular registro de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="6d9df-182">Unregister virtual machines</span></span>
<span data-ttu-id="6d9df-183">Si desea quitar la máquina virtual del almacén de copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="6d9df-183">If you want to remove the virtual machine from the backup vault:</span></span>

1. <span data-ttu-id="6d9df-184">Haga clic en el botón **ANULAR REGISTRO** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="6d9df-184">Click on the **UNREGISTER** button at the bottom of the page.</span></span>

    ![Deshabilitar protección](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="6d9df-186">Aparecerá una notificación en la parte inferior de la pantalla de confirmación de solicitud.</span><span class="sxs-lookup"><span data-stu-id="6d9df-186">A toast notification will appear at the bottom of the screen requesting confirmation.</span></span> <span data-ttu-id="6d9df-187">Haga clic en **Sí** para continuar.</span><span class="sxs-lookup"><span data-stu-id="6d9df-187">Click **YES** to continue.</span></span>

    ![Deshabilitar protección](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="6d9df-189">Eliminación de datos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="6d9df-189">Delete Backup data</span></span>
<span data-ttu-id="6d9df-190">Los datos de copia de seguridad asociados a una máquina virtual se pueden eliminar en los siguientes momentos:</span><span class="sxs-lookup"><span data-stu-id="6d9df-190">You can delete the backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="6d9df-191">Durante el trabajo de detención de la protección</span><span class="sxs-lookup"><span data-stu-id="6d9df-191">During Stop Protection Job</span></span>
* <span data-ttu-id="6d9df-192">Después de realizar un trabajo de detención de la protección en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6d9df-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="6d9df-193">Para eliminar los datos de copia de seguridad de una máquina virtual que se encuentre en estado de *Protección detenida* después de haber realizado correctamente un trabajo **Detener copia de seguridad** :</span><span class="sxs-lookup"><span data-stu-id="6d9df-193">To delete backup data on a virtual machine, which is in the *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="6d9df-194">Vaya a la página **Elementos protegidos**, elija **Máquina virtual de Azure** como *tipo* y haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-194">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as *type* and click the **Select** button.</span></span>

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="6d9df-196">Seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d9df-196">Select the virtual machine.</span></span> <span data-ttu-id="6d9df-197">La máquina virtual estará en el estado **Protección detenida** .</span><span class="sxs-lookup"><span data-stu-id="6d9df-197">The virtual machine will be in **Protection Stopped** state.</span></span>

    ![Protección detenida](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="6d9df-199">Haga clic en el botón **ELIMINAR** , situado en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="6d9df-199">Click the **DELETE** button at the bottom of the page.</span></span>

    ![Eliminación de copia de seguridad](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="6d9df-201">En el asistente **Eliminar datos de copia de seguridad**, elija un motivo para eliminar los datos de copia de seguridad (muy recomendable) y haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-201">In the **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Eliminación de datos de copia de seguridad](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="6d9df-203">Esto creará un trabajo para eliminar los datos de copia de seguridad de la máquina virtual seleccionada.</span><span class="sxs-lookup"><span data-stu-id="6d9df-203">This will create a job to delete backup data of selected virtual machine.</span></span> <span data-ttu-id="6d9df-204">Haga clic en **Ver trabajo** para ver el trabajo correspondiente en la página Trabajos.</span><span class="sxs-lookup"><span data-stu-id="6d9df-204">Click **View job** to see corresponding job in Jobs page.</span></span>

    ![Eliminación de datos correcta](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="6d9df-206">Una vez completado el trabajo, se eliminará la entrada correspondiente a la máquina virtual de la página **Elementos protegidos** .</span><span class="sxs-lookup"><span data-stu-id="6d9df-206">Once the job is completed, the entry corresponding to the virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="6d9df-207">Panel</span><span class="sxs-lookup"><span data-stu-id="6d9df-207">Dashboard</span></span>
<span data-ttu-id="6d9df-208">En la página **Panel** , puede revisar la información sobre las máquinas virtuales de Azure, su almacenamiento y los trabajos asociados a ellas durante las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="6d9df-208">On the **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in the last 24 hours.</span></span> <span data-ttu-id="6d9df-209">Puede ver el estado de copia de seguridad y los errores de copia de seguridad asociados.</span><span class="sxs-lookup"><span data-stu-id="6d9df-209">You can view backup status and any associated backup errors.</span></span>

![Panel](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="6d9df-211">Los valores indicados en el panel se actualizan cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="6d9df-211">Values in the dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="6d9df-212">Operaciones de auditoría</span><span class="sxs-lookup"><span data-stu-id="6d9df-212">Auditing Operations</span></span>
<span data-ttu-id="6d9df-213">Copia de seguridad de Azure proporciona la revisión de los "registros de operación" de las operaciones de copia de seguridad desencadenadas por el cliente, lo que facilita ver exactamente qué operaciones de administración se realizaron en el almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6d9df-213">Azure backup provides review of the "operation logs" of backup operations triggered by the customer making it easy to see exactly what management operations were performed on the backup vault.</span></span> <span data-ttu-id="6d9df-214">Los registros de operaciones permiten excelentes análisis finales y soportes técnicos de auditoría para las operaciones de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6d9df-214">Operations logs enable great post-mortem and audit support for the backup operations.</span></span>

<span data-ttu-id="6d9df-215">Las siguientes operaciones se registran en los registros de operaciones:</span><span class="sxs-lookup"><span data-stu-id="6d9df-215">The following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="6d9df-216">Registro</span><span class="sxs-lookup"><span data-stu-id="6d9df-216">Register</span></span>
* <span data-ttu-id="6d9df-217">Unregister </span><span class="sxs-lookup"><span data-stu-id="6d9df-217">Unregister</span></span>
* <span data-ttu-id="6d9df-218">Configuración de protección</span><span class="sxs-lookup"><span data-stu-id="6d9df-218">Configure protection</span></span>
* <span data-ttu-id="6d9df-219">Copia de seguridad (tanto programada como a petición mediante BackupNow)</span><span class="sxs-lookup"><span data-stu-id="6d9df-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="6d9df-220">Restauración</span><span class="sxs-lookup"><span data-stu-id="6d9df-220">Restore</span></span>
* <span data-ttu-id="6d9df-221">Detener protección</span><span class="sxs-lookup"><span data-stu-id="6d9df-221">Stop protection</span></span>
* <span data-ttu-id="6d9df-222">Eliminación de datos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="6d9df-222">Delete backup data</span></span>
* <span data-ttu-id="6d9df-223">Add policy</span><span class="sxs-lookup"><span data-stu-id="6d9df-223">Add policy</span></span>
* <span data-ttu-id="6d9df-224">Eliminación de directiva</span><span class="sxs-lookup"><span data-stu-id="6d9df-224">Delete policy</span></span>
* <span data-ttu-id="6d9df-225">Actualización de directiva</span><span class="sxs-lookup"><span data-stu-id="6d9df-225">Update policy</span></span>
* <span data-ttu-id="6d9df-226">Cancelar trabajo</span><span class="sxs-lookup"><span data-stu-id="6d9df-226">Cancel job</span></span>

<span data-ttu-id="6d9df-227">Para ver los registros de operación correspondientes a un almacén de copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="6d9df-227">To view operation logs corresponding to a backup vault:</span></span>

1. <span data-ttu-id="6d9df-228">Vaya a **Servicios de administración** en Azure Portal y, a continuación, haga clic en la pestaña **Registros de operaciones**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-228">Navigate to **Management services** in Azure portal, and then click the **Operation Logs** tab.</span></span>

    ![Registros de operaciones](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="6d9df-230">En los filtros, seleccione **Copia de seguridad** como *Tipo*, especifique el nombre del almacén de copia de seguridad en *Nombre de servicio* y haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="6d9df-230">In the filters, select **Backup** as *Type* and specify the backup vault name in *service name* and click on **Submit**.</span></span>

    ![Filtro de registros de operaciones](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="6d9df-232">En los registros de operaciones, seleccione cualquier operación y haga clic en **Detalles** para ver los detalles correspondientes a una operación.</span><span class="sxs-lookup"><span data-stu-id="6d9df-232">In the operations logs, select any operation and click  **Details** to see details corresponding to an operation.</span></span>

    ![Detalles de obtención de registros de operaciones](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="6d9df-234">El **asistente para detalles** contiene información sobre la operación desencadenada, Id. de trabajo, recurso en el que se desencadena esta operación y hora de inicio de la operación.</span><span class="sxs-lookup"><span data-stu-id="6d9df-234">The **Details wizard** contains information about the operation triggered, job Id, resource on which this operation is triggered, and start time of the operation.</span></span>

    ![Detalles de la operación](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="6d9df-236">Notificaciones de alerta</span><span class="sxs-lookup"><span data-stu-id="6d9df-236">Alert notifications</span></span>
<span data-ttu-id="6d9df-237">Puede obtener notificaciones de alerta personalizadas para los trabajos del portal.</span><span class="sxs-lookup"><span data-stu-id="6d9df-237">You can get custom alert notifications for the jobs in portal.</span></span> <span data-ttu-id="6d9df-238">Esto se consigue mediante la definición de reglas de alerta basadas en PowerShell en los eventos de registros operativos.</span><span class="sxs-lookup"><span data-stu-id="6d9df-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="6d9df-239">Se recomienda usar *PowerShell versión 1.3.0 o posterior*.</span><span class="sxs-lookup"><span data-stu-id="6d9df-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="6d9df-240">Para definir una notificación personalizada que avise de errores de copia de seguridad, puede ver un comando de ejemplo parecido al siguiente:</span><span class="sxs-lookup"><span data-stu-id="6d9df-240">To define a custom notification to alert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="6d9df-241">**ResourceId**: puede obtenerlo en la ventana emergente de registros de operaciones tal como se describe en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="6d9df-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="6d9df-242">ResourceUri en una ventana emergente de detalles de una operación es el ResourceId que se debe indicar para este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6d9df-242">ResourceUri in details popup window of an operation is the ResourceId to be supplied for this cmdlet.</span></span>

<span data-ttu-id="6d9df-243">**OperationName**: tendrá el formato "Microsoft.Backup/backupvault/<EventName>" donde EventName es uno de estos valores: Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="6d9df-243">**OperationName**: This will be of the format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="6d9df-244">**Status**: los valores admitidos son: Started, Succeeded y Failed.</span><span class="sxs-lookup"><span data-stu-id="6d9df-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="6d9df-245">**ResourceGroup**: ResourceGroup del recurso en el que se desencadena la operación.</span><span class="sxs-lookup"><span data-stu-id="6d9df-245">**ResourceGroup**:ResourceGroup of the resource on which operation is triggered.</span></span> <span data-ttu-id="6d9df-246">Puede obtenerlo del valor de ResourceId.</span><span class="sxs-lookup"><span data-stu-id="6d9df-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="6d9df-247">El valor entre los campos */resourceGroups/* y */providers/* en el valor de ResourceId es el valor de ResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="6d9df-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is the value for ResourceGroup.</span></span>

<span data-ttu-id="6d9df-248">**Name**: nombre de la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="6d9df-248">**Name**: Name of the Alert Rule.</span></span>

<span data-ttu-id="6d9df-249">**CustomEmail**: especifique la dirección de correo electrónico personalizada a la que desea enviar la notificación de alerta.</span><span class="sxs-lookup"><span data-stu-id="6d9df-249">**CustomEmail**: Specify the custom email address to which you want to send alert notification</span></span>

<span data-ttu-id="6d9df-250">**SendToServiceOwners**: esta opción envía la notificación de alerta a todos los administradores y coadministradores de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="6d9df-250">**SendToServiceOwners**: This option sends alert notification to all administrators and co-administrators of the subscription.</span></span> <span data-ttu-id="6d9df-251">Se puede utilizar en el cmdlet **New-AzureRmAlertRuleEmail** .</span><span class="sxs-lookup"><span data-stu-id="6d9df-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="6d9df-252">Limitaciones de las alertas</span><span class="sxs-lookup"><span data-stu-id="6d9df-252">Limitations on Alerts</span></span>
<span data-ttu-id="6d9df-253">Las alertas basadas en eventos están sometidas a las siguientes limitaciones:</span><span class="sxs-lookup"><span data-stu-id="6d9df-253">Event-based alerts are subjected to the following limitations:</span></span>

1. <span data-ttu-id="6d9df-254">Las alertas se activan en todas las máquinas virtuales del almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6d9df-254">Alerts are triggered on all virtual machines in the backup vault.</span></span> <span data-ttu-id="6d9df-255">No es posible personalizar esto para obtener alertas para un conjunto específico de máquinas virtuales de un almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6d9df-255">You cannot customize it to get alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="6d9df-256">Esta característica se encuentra en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="6d9df-256">This feature is in Preview.</span></span> [<span data-ttu-id="6d9df-257">Más información</span><span class="sxs-lookup"><span data-stu-id="6d9df-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="6d9df-258">Recibirá las alertas de alerts-noreply@mail.windowsazure.com.</span><span class="sxs-lookup"><span data-stu-id="6d9df-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="6d9df-259">Actualmente, no se puede modificar el remitente de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="6d9df-259">Currently you can't modify the email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d9df-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d9df-260">Next steps</span></span>
* [<span data-ttu-id="6d9df-261">Restauración de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="6d9df-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
