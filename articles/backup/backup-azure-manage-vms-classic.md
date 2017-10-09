---
title: "aaaManage y monitor de copias de seguridad de máquina virtual de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage y monitor un virtual de Azure las copias de seguridad de máquinas"
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
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a><span data-ttu-id="b370a-103">Administrar trabajos de copia de seguridad de Azure comunes y las alertas de desencadenador en el portal clásico de Hola</span><span class="sxs-lookup"><span data-stu-id="b370a-103">Manage common Azure Backup jobs and trigger alerts in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b370a-104">Administrar copias de seguridad de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="b370a-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="b370a-105">Administrar copias de seguridad de máquina virtual clásica</span><span class="sxs-lookup"><span data-stu-id="b370a-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="b370a-106">Este artículo proporciona información acerca de las tareas de administración y supervisión comunes para las máquinas virtuales de modelo clásico protegidas en Azure.</span><span class="sxs-lookup"><span data-stu-id="b370a-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="b370a-107">Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b370a-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b370a-108">Vea [preparar su tooback entorno las máquinas virtuales de Azure](backup-azure-vms-prepare.md) para obtener más información acerca de cómo trabajar con la implementación estándar de modelo máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b370a-108">See [Prepare your environment tooback up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="b370a-109">A partir de marzo de 2017, no podrá usar almacenes de copia de seguridad de hello toocreate portal clásico.</span><span class="sxs-lookup"><span data-stu-id="b370a-109">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="b370a-110">Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b370a-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="b370a-111">Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="b370a-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="b370a-112">Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b370a-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="b370a-113">Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b370a-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="b370a-114">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="b370a-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="b370a-115">Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b370a-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="b370a-116">No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="b370a-117">En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b370a-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="b370a-118">Administrar máquinas virtuales protegidas</span><span class="sxs-lookup"><span data-stu-id="b370a-118">Manage protected virtual machines</span></span>
<span data-ttu-id="b370a-119">toomanage máquinas virtuales protegidas:</span><span class="sxs-lookup"><span data-stu-id="b370a-119">toomanage protected virtual machines:</span></span>

1. <span data-ttu-id="b370a-120">tooview y administrar la configuración de copia de seguridad para una máquina virtual, haga clic en hello **elementos protegidos** ficha.</span><span class="sxs-lookup"><span data-stu-id="b370a-120">tooview and manage backup settings for a virtual machine click hello **Protected Items** tab.</span></span>
2. <span data-ttu-id="b370a-121">Haga clic en nombre de Hola de un saludo de toosee elemento protegido **detalles de la copia de seguridad** ficha, que muestra información acerca de la última copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-121">Click on hello name of a protected item toosee hello **Backup Details** tab, which shows you information about hello last backup.</span></span>

    ![Copia de seguridad de máquina virtual](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="b370a-123">tooview y administrar la configuración de directiva de copia de seguridad para una máquina virtual, haga clic en hello **directivas** ficha.</span><span class="sxs-lookup"><span data-stu-id="b370a-123">tooview and manage backup policy settings for a virtual machine click hello **Policies** tab.</span></span>

    ![Directiva de máquina virtual](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="b370a-125">Hola **directivas de copia de seguridad** ficha muestra Hola directiva existente.</span><span class="sxs-lookup"><span data-stu-id="b370a-125">hello **Backup Policies** tab shows you hello existing policy.</span></span> <span data-ttu-id="b370a-126">Se puede modificar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b370a-126">You can modify as needed.</span></span> <span data-ttu-id="b370a-127">Si necesita toocreate una nueva directiva, haga clic en **crear** en hello **directivas** página.</span><span class="sxs-lookup"><span data-stu-id="b370a-127">If you need toocreate a new policy click **Create** on hello **Policies** page.</span></span> <span data-ttu-id="b370a-128">Tenga en cuenta que si desea tooremove una directiva no debe tener las máquinas virtuales asociadas a él.</span><span class="sxs-lookup"><span data-stu-id="b370a-128">Note that if you want tooremove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Directiva de máquina virtual](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="b370a-130">Puede obtener más información sobre acciones o estado de una máquina virtual en hello **trabajos** página.</span><span class="sxs-lookup"><span data-stu-id="b370a-130">You can get more information about actions or status for a virtual machine on hello **Jobs** page.</span></span> <span data-ttu-id="b370a-131">Haga clic en un trabajo en hello lista tooget más detalles o filtre los trabajos de una máquina virtual específica.</span><span class="sxs-lookup"><span data-stu-id="b370a-131">Click a job in hello list tooget more details, or filter jobs for a specific virtual machine.</span></span>

    ![Trabajos](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="b370a-133">Copia de seguridad a petición de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b370a-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="b370a-134">Puede realizar una copia de seguridad a petición de una máquina virtual una vez que esta esté configurada para la protección.</span><span class="sxs-lookup"><span data-stu-id="b370a-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="b370a-135">Si la copia de seguridad inicial de hello está pendiente para la máquina virtual de hello, copia de seguridad a petición creará una copia completa de la máquina virtual de hello en el almacén de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="b370a-135">If hello initial backup is pending for hello virtual machine, on-demand backup will create a full copy of hello virtual machine in Azure backup vault.</span></span> <span data-ttu-id="b370a-136">Si se ha completado la primera copia de seguridad, copia de seguridad de petición se solo almacén de envío de cambios desde la copia de seguridad de copia de seguridad tooAzure anterior, es decir, es siempre incremental.</span><span class="sxs-lookup"><span data-stu-id="b370a-136">If first backup is completed, on-demand backup will only send changes from previous backup tooAzure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="b370a-137">Duración de retención de una copia de seguridad a petición se establece el valor tooretention especificado para la retención diaria en directiva de copia de seguridad correspondiente toohello VM.</span><span class="sxs-lookup"><span data-stu-id="b370a-137">Retention range of an on-demand backup is set tooretention value specified for Daily retention in backup policy corresponding toohello VM.</span></span>  
>
>

<span data-ttu-id="b370a-138">copia de seguridad de tootake una petición de una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="b370a-138">tootake an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="b370a-139">Navegue toohello **elementos protegidos** página y seleccione **Máquina Virtual de Azure** como **tipo** (si aún no está seleccionado) y haga clic en **seleccione**botón.</span><span class="sxs-lookup"><span data-stu-id="b370a-139">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="b370a-141">Seleccione la máquina virtual de hello en el que desea tootake a petición en copia de seguridad y haga clic en **copia de seguridad ahora** situado en la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-141">Select hello virtual machine on which you want tootake an on-demand backup and click on **Backup Now** button at hello bottom of hello page.</span></span>

    ![Copia de seguridad ahora](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="b370a-143">Esto creará un trabajo de copia de seguridad en la máquina virtual de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="b370a-143">This will create a backup job on hello selected virtual machine.</span></span> <span data-ttu-id="b370a-144">Duración de retención de punto de recuperación creado a través de este trabajo será igual a la que especificó en la directiva de hello asociado a la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-144">Retention range of recovery point created through this job will be same as that specified in hello policy associated with hello virtual machine.</span></span>

    ![Creación de trabajo de copia de seguridad](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="b370a-146">Directiva de hello tooview asociada a una máquina virtual, explorar hacia abajo en la máquina virtual en hello **elementos protegidos** toobackup vaya directiva fichas y páginas.</span><span class="sxs-lookup"><span data-stu-id="b370a-146">tooview hello policy associated with a virtual machine, drill down into virtual machine in hello **Protected Items** page and go toobackup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="b370a-147">Una vez que se crea el trabajo de hello, puede hacer clic en **ver trabajo** botón de notificación de hello barra toosee trabajo de hello correspondiente en la página de trabajos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-147">Once hello job is created, you can click on **View job** button in hello toast bar toosee hello corresponding job in hello jobs page.</span></span>

    ![Trabajo de copia de seguridad creado](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="b370a-149">Tras finalizar correctamente el trabajo de hello, un punto de recuperación se creará que puede usar máquinas virtuales de toorestore Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-149">After successful completion of hello job, a recovery point will be created which you can use toorestore hello virtual machine.</span></span> <span data-ttu-id="b370a-150">Esto también incrementará el valor de columna de punto de recuperación de hello en 1 en **elementos protegidos** página.</span><span class="sxs-lookup"><span data-stu-id="b370a-150">This will also increment hello recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="b370a-151">Detener la protección de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="b370a-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="b370a-152">Puede elegir toostop Hola copias de seguridad de una máquina virtual con hello siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="b370a-152">You can choose toostop hello future backups of a virtual machine with hello following options:</span></span>

* <span data-ttu-id="b370a-153">Conservar los datos de copia de seguridad asociados a la máquina virtual en el almacén de copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="b370a-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="b370a-154">Eliminación de datos de copia de seguridad asociados a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b370a-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="b370a-155">Si ha seleccionado los datos de copia de seguridad de tooretain asociados a la máquina virtual, puede usar máquina virtual de hello datos de copia de seguridad toorestore Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-155">If you have selected tooretain backup data associated with virtual machine, you can use hello backup data toorestore hello virtual machine.</span></span> <span data-ttu-id="b370a-156">Para obtener más detalles sobre el precio de estas máquinas virtuales, haga clic [aquí](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="b370a-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="b370a-157">protección de tooStop para una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="b370a-157">tooStop protection for a virtual machine:</span></span>

1. <span data-ttu-id="b370a-158">Navegue demasiado**elementos protegidos** página y seleccione **máquina virtual de Azure** como tipo de filtro de hello (si aún no está seleccionado) y haga clic en **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="b370a-158">Navigate too**Protected Items** page and select **Azure virtual machine** as hello filter type (if not already selected) and click on **Select** button.</span></span>

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="b370a-160">Seleccione la máquina virtual de Hola y haga clic en **detener protección** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-160">Select hello virtual machine and click on **Stop Protection** at hello bottom of hello page.</span></span>

    ![Detener protección](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="b370a-162">De forma predeterminada, copia de seguridad de Azure no se elimina datos de copia de seguridad de hello asociados a la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-162">By default, Azure Backup doesn’t delete hello backup data associated with hello virtual machine.</span></span>

    ![Confirmación de la detención de la protección](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="b370a-164">Si desea que los datos de copia de seguridad de toodelete, active la casilla de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-164">If you want toodelete backup data, select hello check box.</span></span>

    ![Casilla de verificación](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="b370a-166">Seleccione un motivo para detener la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-166">Please select a reason for stopping hello backup.</span></span> <span data-ttu-id="b370a-167">Aunque esto es opcional, proporcionar un motivo ayuda toowork de copia de seguridad de Azure en los comentarios de Hola y dar prioridad a los escenarios de clientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-167">While this is optional, providing a reason will help Azure Backup toowork on hello feedback and prioritize hello customer scenarios.</span></span>
4. <span data-ttu-id="b370a-168">Haga clic en **enviar** Hola de botón toosubmit **detener la protección** trabajo.</span><span class="sxs-lookup"><span data-stu-id="b370a-168">Click on **Submit** button toosubmit hello **Stop protection** job.</span></span> <span data-ttu-id="b370a-169">Haga clic en **ver trabajo** toosee Hola trabajo Hola correspondiente en **trabajos** página.</span><span class="sxs-lookup"><span data-stu-id="b370a-169">Click on **View Job** toosee hello corresponding hello job in **Jobs** page.</span></span>

    ![Detener protección](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="b370a-171">Si no ha seleccionado **eliminar los datos de copia de seguridad asociados** opción durante la **detener protección** protección Asistente y, a continuación, complete el trabajo posterior, también cambia el estado**protección detiene**.</span><span class="sxs-lookup"><span data-stu-id="b370a-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes too**Protection Stopped**.</span></span> <span data-ttu-id="b370a-172">datos de Hello permanecen con la copia de seguridad de Azure hasta que se elimine de forma explícita.</span><span class="sxs-lookup"><span data-stu-id="b370a-172">hello data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="b370a-173">Siempre se pueden eliminar datos de hello seleccionando la máquina virtual de Hola Hola **elementos protegidos** página y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="b370a-173">You can always delete hello data by selecting hello virtual machine in hello **Protected Items** page and clicking **Delete**.</span></span>

    ![Protección detenida](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="b370a-175">Si ha seleccionado hello **eliminar los datos de copia de seguridad asociados** opción, hello máquina virtual no formar parte del programa Hola a **elementos protegidos** página.</span><span class="sxs-lookup"><span data-stu-id="b370a-175">If you have selected hello **Delete associated backup data** option, hello virtual machine won’t be part of hello **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="b370a-176">Volver a proteger la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b370a-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="b370a-177">Si no ha seleccionado hello **eliminar datos de copia de seguridad asociados** opción **detener protección**, poder volver a proteger máquinas virtuales de hello siguiendo Hola pasos similares toobacking seguridad registrado virtual máquinas.</span><span class="sxs-lookup"><span data-stu-id="b370a-177">If you have not selected hello **Delete associate backup data** option in **Stop Protection**, you can re-protect hello virtual machine by following hello steps similar toobacking up registered virtual machines.</span></span> <span data-ttu-id="b370a-178">Una vez protegida, esta máquina virtual tendrá protección de datos de copia de seguridad almacenados toostop anterior y puntos de recuperación crean después de volver a proteger.</span><span class="sxs-lookup"><span data-stu-id="b370a-178">Once protected, this virtual machine will have backup data retained prior toostop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="b370a-179">Después de volver a proteger, estado de protección de la máquina virtual Hola se cambiarán demasiado**Protected** si demasiado hay puntos de recuperación anterior**detener protección**.</span><span class="sxs-lookup"><span data-stu-id="b370a-179">After re-protect, hello virtual machine’s protection status will be changed too**Protected** if there are recovery points prior too**Stop Protection**.</span></span>

  ![Máquina virtual protegida de nuevo](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="b370a-181">Al volver a proteger máquinas virtuales de hello, puede elegir una directiva diferente a la directiva de hello con la que se protegió inicialmente máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b370a-181">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="b370a-182">Anular registro de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="b370a-182">Unregister virtual machines</span></span>
<span data-ttu-id="b370a-183">Si desea que tooremove Hola virtual machine del almacén de copia de seguridad de hello:</span><span class="sxs-lookup"><span data-stu-id="b370a-183">If you want tooremove hello virtual machine from hello backup vault:</span></span>

1. <span data-ttu-id="b370a-184">Haga clic en hello **UNREGISTER** situado en la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-184">Click on hello **UNREGISTER** button at hello bottom of hello page.</span></span>

    ![Deshabilitar protección](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="b370a-186">Una notificación del sistema aparecerá en la parte inferior de Hola de pantalla de bienvenida que solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="b370a-186">A toast notification will appear at hello bottom of hello screen requesting confirmation.</span></span> <span data-ttu-id="b370a-187">Haga clic en **Sí** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b370a-187">Click **YES** toocontinue.</span></span>

    ![Deshabilitar protección](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="b370a-189">Eliminación de datos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b370a-189">Delete Backup data</span></span>
<span data-ttu-id="b370a-190">Puede eliminar los datos de copia de seguridad de hello asociados con una máquina virtual, ya sea:</span><span class="sxs-lookup"><span data-stu-id="b370a-190">You can delete hello backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="b370a-191">Durante el trabajo de detención de la protección</span><span class="sxs-lookup"><span data-stu-id="b370a-191">During Stop Protection Job</span></span>
* <span data-ttu-id="b370a-192">Después de realizar un trabajo de detención de la protección en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b370a-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="b370a-193">datos de copia de seguridad de toodelete en una máquina virtual, que se encuentra en hello *protección detiene* estado registrar la finalización correcta de un **Detener copia de seguridad** trabajo:</span><span class="sxs-lookup"><span data-stu-id="b370a-193">toodelete backup data on a virtual machine, which is in hello *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="b370a-194">Navegue toohello **elementos protegidos** página y seleccione **Máquina Virtual de Azure** como *tipo* y haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="b370a-194">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as *type* and click hello **Select** button.</span></span>

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="b370a-196">Seleccione la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-196">Select hello virtual machine.</span></span> <span data-ttu-id="b370a-197">máquina virtual de Hello estará en **protección detiene** estado.</span><span class="sxs-lookup"><span data-stu-id="b370a-197">hello virtual machine will be in **Protection Stopped** state.</span></span>

    ![Protección detenida](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="b370a-199">Haga clic en hello **eliminar** situado en la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-199">Click hello **DELETE** button at hello bottom of hello page.</span></span>

    ![Eliminación de copia de seguridad](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="b370a-201">Hola **eliminar datos de copia de seguridad** asistente, seleccione un motivo para eliminar datos de copia de seguridad (muy recomendados) y haga clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="b370a-201">In hello **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Eliminación de datos de copia de seguridad](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="b370a-203">Esto creará una copia de seguridad de datos de toodelete de trabajo de máquina virtual seleccionada.</span><span class="sxs-lookup"><span data-stu-id="b370a-203">This will create a job toodelete backup data of selected virtual machine.</span></span> <span data-ttu-id="b370a-204">Haga clic en **ver trabajo** toosee trabajo correspondiente en la página trabajos.</span><span class="sxs-lookup"><span data-stu-id="b370a-204">Click **View job** toosee corresponding job in Jobs page.</span></span>

    ![Eliminación de datos correcta](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="b370a-206">Una vez que se complete el trabajo de hello, Hola entrada correspondiente máquina virtual de toohello se quitarán de **elementos protegidos** página.</span><span class="sxs-lookup"><span data-stu-id="b370a-206">Once hello job is completed, hello entry corresponding toohello virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="b370a-207">Panel</span><span class="sxs-lookup"><span data-stu-id="b370a-207">Dashboard</span></span>
<span data-ttu-id="b370a-208">En hello **panel** página puede revisar información sobre máquinas virtuales de Azure, su almacenamiento y los trabajos asociados con ellos en hello últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b370a-208">On hello **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in hello last 24 hours.</span></span> <span data-ttu-id="b370a-209">Puede ver el estado de copia de seguridad y los errores de copia de seguridad asociados.</span><span class="sxs-lookup"><span data-stu-id="b370a-209">You can view backup status and any associated backup errors.</span></span>

![Panel](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="b370a-211">Los valores en el panel de Hola se actualizan una vez cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b370a-211">Values in hello dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="b370a-212">Operaciones de auditoría</span><span class="sxs-lookup"><span data-stu-id="b370a-212">Auditing Operations</span></span>
<span data-ttu-id="b370a-213">Copia de seguridad de Azure proporciona revisión de Hola "registros de operaciones" de las operaciones de copia de seguridad desencadenados por cliente hello toosee fácil exactamente qué operaciones de administración se realizaron en el almacén de copia de seguridad de Hola para convertirla.</span><span class="sxs-lookup"><span data-stu-id="b370a-213">Azure backup provides review of hello "operation logs" of backup operations triggered by hello customer making it easy toosee exactly what management operations were performed on hello backup vault.</span></span> <span data-ttu-id="b370a-214">Registros de operaciones Habilitar evaluación excelente y compatibilidad para las operaciones de copia de seguridad de Hola de auditoría.</span><span class="sxs-lookup"><span data-stu-id="b370a-214">Operations logs enable great post-mortem and audit support for hello backup operations.</span></span>

<span data-ttu-id="b370a-215">Hola las siguientes operaciones se registra en los registros de operaciones:</span><span class="sxs-lookup"><span data-stu-id="b370a-215">hello following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="b370a-216">Registro</span><span class="sxs-lookup"><span data-stu-id="b370a-216">Register</span></span>
* <span data-ttu-id="b370a-217">Unregister </span><span class="sxs-lookup"><span data-stu-id="b370a-217">Unregister</span></span>
* <span data-ttu-id="b370a-218">Configuración de protección</span><span class="sxs-lookup"><span data-stu-id="b370a-218">Configure protection</span></span>
* <span data-ttu-id="b370a-219">Copia de seguridad (tanto programada como a petición mediante BackupNow)</span><span class="sxs-lookup"><span data-stu-id="b370a-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="b370a-220">Restauración</span><span class="sxs-lookup"><span data-stu-id="b370a-220">Restore</span></span>
* <span data-ttu-id="b370a-221">Detener protección</span><span class="sxs-lookup"><span data-stu-id="b370a-221">Stop protection</span></span>
* <span data-ttu-id="b370a-222">Eliminación de datos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b370a-222">Delete backup data</span></span>
* <span data-ttu-id="b370a-223">Add policy</span><span class="sxs-lookup"><span data-stu-id="b370a-223">Add policy</span></span>
* <span data-ttu-id="b370a-224">Eliminación de directiva</span><span class="sxs-lookup"><span data-stu-id="b370a-224">Delete policy</span></span>
* <span data-ttu-id="b370a-225">Actualización de directiva</span><span class="sxs-lookup"><span data-stu-id="b370a-225">Update policy</span></span>
* <span data-ttu-id="b370a-226">Cancelar trabajo</span><span class="sxs-lookup"><span data-stu-id="b370a-226">Cancel job</span></span>

<span data-ttu-id="b370a-227">los registros de operaciones de tooview almacén de copia de seguridad tooa correspondiente:</span><span class="sxs-lookup"><span data-stu-id="b370a-227">tooview operation logs corresponding tooa backup vault:</span></span>

1. <span data-ttu-id="b370a-228">Navegue demasiado**servicios de administración de** en el portal de Azure y, a continuación, haga clic en hello **registros de operaciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="b370a-228">Navigate too**Management services** in Azure portal, and then click hello **Operation Logs** tab.</span></span>

    ![Registros de operaciones](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="b370a-230">En filtros de hello, seleccione **copia de seguridad** como *tipo* y especifique el nombre del almacén de copia de seguridad de hello en *nombre del servicio* y haga clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="b370a-230">In hello filters, select **Backup** as *Type* and specify hello backup vault name in *service name* and click on **Submit**.</span></span>

    ![Filtro de registros de operaciones](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="b370a-232">En los registros de operaciones de hello, seleccione cualquier operación y haga clic en **detalles** toosee detalles operación tooan correspondiente.</span><span class="sxs-lookup"><span data-stu-id="b370a-232">In hello operations logs, select any operation and click  **Details** toosee details corresponding tooan operation.</span></span>

    ![Detalles de obtención de registros de operaciones](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="b370a-234">Hola **Asistente detalles** contiene información sobre Hola operación de desencadena, Id., uso de recursos en el que se desencadena esta operación y hora de inicio de la operación de Hola de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b370a-234">hello **Details wizard** contains information about hello operation triggered, job Id, resource on which this operation is triggered, and start time of hello operation.</span></span>

    ![Detalles de la operación](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="b370a-236">Notificaciones de alerta</span><span class="sxs-lookup"><span data-stu-id="b370a-236">Alert notifications</span></span>
<span data-ttu-id="b370a-237">Puede obtener las notificaciones de alerta personalizadas para los trabajos de hello en el portal.</span><span class="sxs-lookup"><span data-stu-id="b370a-237">You can get custom alert notifications for hello jobs in portal.</span></span> <span data-ttu-id="b370a-238">Esto se consigue mediante la definición de reglas de alerta basadas en PowerShell en los eventos de registros operativos.</span><span class="sxs-lookup"><span data-stu-id="b370a-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="b370a-239">Se recomienda usar *PowerShell versión 1.3.0 o posterior*.</span><span class="sxs-lookup"><span data-stu-id="b370a-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="b370a-240">toodefine un tooalert de notificación personalizada para errores de copia de seguridad, un comando de ejemplo será similar:</span><span class="sxs-lookup"><span data-stu-id="b370a-240">toodefine a custom notification tooalert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="b370a-241">**ResourceId**: puede obtenerlo en la ventana emergente de registros de operaciones tal como se describe en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="b370a-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="b370a-242">ResourceUri en ventana emergente de detalles de una operación es Hola ResourceId toobe proporcionado para este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b370a-242">ResourceUri in details popup window of an operation is hello ResourceId toobe supplied for this cmdlet.</span></span>

<span data-ttu-id="b370a-243">**OperationName**: se trata del formato de Hola "Microsoft.Backup/backupvault/<EventName>" donde EventName es uno de registrar, anular el registro, ConfigureProtection, copia de seguridad, restauración, StopProtection, DeleteBackupData, CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="b370a-243">**OperationName**: This will be of hello format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="b370a-244">**Status**: los valores admitidos son: Started, Succeeded y Failed.</span><span class="sxs-lookup"><span data-stu-id="b370a-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="b370a-245">**ResourceGroup**: grupo de recursos del recurso de hello en el que se desencadena la operación.</span><span class="sxs-lookup"><span data-stu-id="b370a-245">**ResourceGroup**:ResourceGroup of hello resource on which operation is triggered.</span></span> <span data-ttu-id="b370a-246">Puede obtenerlo del valor de ResourceId.</span><span class="sxs-lookup"><span data-stu-id="b370a-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="b370a-247">Valor entre campos */ResourceGroups /* y */providers/* en ResourceId valor es el valor de hello para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b370a-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is hello value for ResourceGroup.</span></span>

<span data-ttu-id="b370a-248">**Nombre**: nombre de regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-248">**Name**: Name of hello Alert Rule.</span></span>

<span data-ttu-id="b370a-249">**CustomEmail**: especificar toowhich de dirección de correo electrónico personalizada hello desea toosend notificación de alerta</span><span class="sxs-lookup"><span data-stu-id="b370a-249">**CustomEmail**: Specify hello custom email address toowhich you want toosend alert notification</span></span>

<span data-ttu-id="b370a-250">**SendToServiceOwners**: esta opción envía los administradores de tooall de notificación de alertas y los coadministradores tienen permisos de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-250">**SendToServiceOwners**: This option sends alert notification tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="b370a-251">Se puede utilizar en el cmdlet **New-AzureRmAlertRuleEmail** .</span><span class="sxs-lookup"><span data-stu-id="b370a-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="b370a-252">Limitaciones de las alertas</span><span class="sxs-lookup"><span data-stu-id="b370a-252">Limitations on Alerts</span></span>
<span data-ttu-id="b370a-253">Alertas basadas en eventos son sometido toohello siguientes limitaciones:</span><span class="sxs-lookup"><span data-stu-id="b370a-253">Event-based alerts are subjected toohello following limitations:</span></span>

1. <span data-ttu-id="b370a-254">Las alertas se activan en todas las máquinas virtuales en el almacén de copia de seguridad Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-254">Alerts are triggered on all virtual machines in hello backup vault.</span></span> <span data-ttu-id="b370a-255">No se puede personalizar tooget alertas para un conjunto específico de máquinas virtuales en un almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b370a-255">You cannot customize it tooget alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="b370a-256">Esta característica se encuentra en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="b370a-256">This feature is in Preview.</span></span> [<span data-ttu-id="b370a-257">Más información</span><span class="sxs-lookup"><span data-stu-id="b370a-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="b370a-258">Recibirá las alertas de alerts-noreply@mail.windowsazure.com.</span><span class="sxs-lookup"><span data-stu-id="b370a-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="b370a-259">Actualmente no se puede modificar el remitente del correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="b370a-259">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b370a-260">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b370a-260">Next steps</span></span>
* [<span data-ttu-id="b370a-261">Restauración de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="b370a-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
