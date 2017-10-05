---
title: "Administración de almacenes y servidores de Copia de seguridad de Azure mediante el modelo de implementación clásica | Microsoft Docs"
description: Use este tutorial para aprender a administrar almacenes y servidores de Copia de seguridad de Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 91451b2cdc42ed05ef7c1ba9c66ad5b4b45dd788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-the-classic-deployment-model"></a><span data-ttu-id="906cd-103">Administración de almacenes y servidores de Copia de seguridad de Azure mediante el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="906cd-103">Manage Azure Backup vaults and servers using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="906cd-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="906cd-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="906cd-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="906cd-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="906cd-106">En este artículo encontrará información general sobre las tareas de administración de copias de seguridad que tiene disponibles en el Portal de Azure clásico y el agente de Copia de seguridad de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="906cd-106">In this article you'll find an overview of the backup management tasks available through the Azure classic portal and the Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="906cd-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="906cd-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="906cd-108">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="906cd-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="906cd-109">Microsoft recomienda que las implementaciones más recientes usen el modelo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="906cd-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="906cd-110">Ahora puede actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="906cd-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="906cd-111">Para más información, consulte el artículo [Actualización de un almacén de Backup a un almacén de Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="906cd-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="906cd-112">Microsoft anima a actualizar los almacenes de Backup a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="906cd-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="906cd-113">A partir del 15 de octubre de 2017, no podrá usar PowerShell para crear almacenes de Backup.</span><span class="sxs-lookup"><span data-stu-id="906cd-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="906cd-114">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="906cd-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="906cd-115">Todos los almacenes de Backup restantes se actualizarán automáticamente a almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="906cd-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="906cd-116">No podrá acceder a los datos de copia de seguridad en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="906cd-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="906cd-117">En su lugar, utilice Azure Portal para tener acceso a los datos de copia de seguridad en los almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="906cd-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="906cd-118">Tareas del Portal de administración</span><span class="sxs-lookup"><span data-stu-id="906cd-118">Management portal tasks</span></span>
1. <span data-ttu-id="906cd-119">Inicie sesión en el [Portal de administración](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="906cd-119">Sign in to the [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="906cd-120">Haga clic en **Servicios de recuperación**y luego en el nombre del almacén de copia de seguridad para ver la página de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="906cd-120">Click **Recovery Services**, then click the name of backup vault to view the Quick Start page.</span></span>

    ![Servicios de recuperación](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="906cd-122">Si selecciona las opciones que se encuentran en la parte superior de la página de Inicio rápido, podrá ver las tareas de administración disponibles.</span><span class="sxs-lookup"><span data-stu-id="906cd-122">By selecting the options at the top of the Quick Start page, you can see the available management tasks.</span></span>

![Administración de pestañas](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="906cd-124">Panel</span><span class="sxs-lookup"><span data-stu-id="906cd-124">Dashboard</span></span>
<span data-ttu-id="906cd-125">Seleccione **Panel** para ver información general sobre el uso del servidor.</span><span class="sxs-lookup"><span data-stu-id="906cd-125">Select **Dashboard** to see the usage overview for the server.</span></span> <span data-ttu-id="906cd-126">En la **información general del uso** se incluyen los siguientes datos:</span><span class="sxs-lookup"><span data-stu-id="906cd-126">The **usage overview** includes:</span></span>

* <span data-ttu-id="906cd-127">El número de servidores de Windows registrados en la nube</span><span class="sxs-lookup"><span data-stu-id="906cd-127">The number of Windows Servers registered to cloud</span></span>
* <span data-ttu-id="906cd-128">El número de máquinas virtuales de Azure protegidas en la nube</span><span class="sxs-lookup"><span data-stu-id="906cd-128">The number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="906cd-129">La cantidad total de espacio de almacenamiento utilizada en Azure</span><span class="sxs-lookup"><span data-stu-id="906cd-129">The total storage consumed in Azure</span></span>
* <span data-ttu-id="906cd-130">El estado de los trabajos recientes</span><span class="sxs-lookup"><span data-stu-id="906cd-130">The status of recent jobs</span></span>

<span data-ttu-id="906cd-131">En la parte inferior del panel puede llevar a cabo las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="906cd-131">At the bottom of the Dashboard you can perform the following tasks:</span></span>

* <span data-ttu-id="906cd-132">**Administrar certificado** : si se ha usado un certificado para registrar el servidor, utilícelo para actualizar el certificado.</span><span class="sxs-lookup"><span data-stu-id="906cd-132">**Manage certificate** - If a certificate was used to register the server, then use this to update the certificate.</span></span> <span data-ttu-id="906cd-133">Si usa credenciales de almacén, no utilice **Administrar certificado**.</span><span class="sxs-lookup"><span data-stu-id="906cd-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="906cd-134">**Eliminar** : elimina el almacén de copia de seguridad actual.</span><span class="sxs-lookup"><span data-stu-id="906cd-134">**Delete** - Deletes the current backup vault.</span></span> <span data-ttu-id="906cd-135">En caso de que ya no se use un almacén de credenciales de copia de seguridad, puede eliminarlo para liberar espacio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="906cd-135">If a backup vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="906cd-136">**Eliminar** solo está habilitado después de que todos los servidores registrados se hayan eliminado del almacén.</span><span class="sxs-lookup"><span data-stu-id="906cd-136">**Delete** is only enabled after all registered servers have been deleted from the vault.</span></span>

![Copia de seguridad de las tareas del panel](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="906cd-138">Elementos registrados</span><span class="sxs-lookup"><span data-stu-id="906cd-138">Registered items</span></span>
<span data-ttu-id="906cd-139">Seleccione la opción **Elementos registrados** para ver los nombres de los servidores que se registraron en este almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="906cd-139">Select **Registered Items** to view the names of the servers that are registered to this vault.</span></span>

![Elementos registrados](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="906cd-141">El filtro **Tipo** tiene como valor predeterminado la opción Máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="906cd-141">The **Type** filter defaults to Azure Virtual Machine.</span></span> <span data-ttu-id="906cd-142">Para ver los nombres de los servidores que están registrados en este almacén, seleccione **Servidor de Windows** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="906cd-142">To view the names of the servers that are registered to this vault, select **Windows server** from the drop down menu.</span></span>

<span data-ttu-id="906cd-143">Aquí puede realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="906cd-143">From here you can perform the following tasks:</span></span>

* <span data-ttu-id="906cd-144">**Permitir nuevo registro**: cuando se selecciona esta opción para un servidor, puede usar el **Asistente para registro** del agente local de Microsoft Azure Backup para registrar el servidor en el almacén de copia de seguridad por segunda vez.</span><span class="sxs-lookup"><span data-stu-id="906cd-144">**Allow Re-registration** - When this option is selected for a server you can use the **Registration Wizard** in the on-premises Microsoft Azure Backup agent to register the server with the backup vault a second time.</span></span> <span data-ttu-id="906cd-145">Es posible que necesite volver a registrarse debido a un error en el certificado o si un servidor tuvo que reconstruirse.</span><span class="sxs-lookup"><span data-stu-id="906cd-145">You might need to re-register due to an error in the certificate or if a server had to be rebuilt.</span></span>
* <span data-ttu-id="906cd-146">**Eliminar** : elimina un servidor del almacén de copias seguridad.</span><span class="sxs-lookup"><span data-stu-id="906cd-146">**Delete** - Deletes a server from the backup vault.</span></span> <span data-ttu-id="906cd-147">Todos los datos almacenados asociados con el servidor se eliminan inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="906cd-147">All of the stored data associated with the server is deleted immediately.</span></span>

    ![Tareas de elementos registrados](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="906cd-149">Elementos protegidos</span><span class="sxs-lookup"><span data-stu-id="906cd-149">Protected items</span></span>
<span data-ttu-id="906cd-150">Haga clic en **Elementos protegidos** para ver los elementos de los que se han hecho copias de seguridad desde los servidores.</span><span class="sxs-lookup"><span data-stu-id="906cd-150">Select **Protected Items** to view the items that have been backed up from the servers.</span></span>

![Elementos protegidos](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="906cd-152">Configuración</span><span class="sxs-lookup"><span data-stu-id="906cd-152">Configure</span></span>
<span data-ttu-id="906cd-153">Desde la pestaña **Configurar** , puede seleccionar la opción de redundancia de almacenamiento idónea.</span><span class="sxs-lookup"><span data-stu-id="906cd-153">From the **Configure** tab you can select the appropriate storage redundancy option.</span></span> <span data-ttu-id="906cd-154">El mejor momento para seleccionar la opción de redundancia de almacenamiento es justo después de la creación del almacén y antes de que las máquinas se registren en este.</span><span class="sxs-lookup"><span data-stu-id="906cd-154">The best time to select the storage redundancy option is right after creating a vault and before any machines are registered to it.</span></span>

> [!WARNING]
> <span data-ttu-id="906cd-155">Una vez que un elemento se ha registrado en el almacén, la opción de redundancia de almacenamiento está bloqueada y no se puede modificar.</span><span class="sxs-lookup"><span data-stu-id="906cd-155">Once an item has been registered to the vault, the storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Configuración](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="906cd-157">Consulte este artículo para más información sobre la [redundancia de almacenamiento](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="906cd-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="906cd-158">Tareas del agente de Copia de seguridad de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="906cd-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="906cd-159">Consola</span><span class="sxs-lookup"><span data-stu-id="906cd-159">Console</span></span>
<span data-ttu-id="906cd-160">Abra el **agente de Copia de seguridad de Microsoft Azure** (puede encontrarlo si busca en su equipo *Copia de seguridad de Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="906cd-160">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Agente de copia de seguridad](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="906cd-162">Con las **acciones** disponibles en la parte derecha de la consola del agente de Copia de seguridad, podrá llevar a cabo las siguientes tareas de administración:</span><span class="sxs-lookup"><span data-stu-id="906cd-162">From the **Actions** available at the right of the backup agent console you can perform the following management tasks:</span></span>

* <span data-ttu-id="906cd-163">Registrar un servidor</span><span class="sxs-lookup"><span data-stu-id="906cd-163">Register Server</span></span>
* <span data-ttu-id="906cd-164">Programación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="906cd-164">Schedule Backup</span></span>
* <span data-ttu-id="906cd-165">Realizar una copia de seguridad en ese momento</span><span class="sxs-lookup"><span data-stu-id="906cd-165">Back Up now</span></span>
* <span data-ttu-id="906cd-166">Cambiar propiedades</span><span class="sxs-lookup"><span data-stu-id="906cd-166">Change Properties</span></span>

![Acciones de la consola de agente](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="906cd-168">Para **recuperar datos**, consulte [Restauración de archivos en una máquina de Windows Server o del cliente de Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="906cd-168">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="906cd-169">Modificación de una copia de seguridad existente</span><span class="sxs-lookup"><span data-stu-id="906cd-169">Modify an existing backup</span></span>
1. <span data-ttu-id="906cd-170">En el agente de Copia de seguridad de Microsoft Azure, haga clic en **Programar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="906cd-170">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="906cd-172">En el **Asistente para programar copias de seguridad**, deje activada la opción **Cambiar la hora o las horas de las copias de seguridad** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="906cd-172">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Modificación de una copia de seguridad programada](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="906cd-174">Si quiere agregar o cambiar elementos, en la pantalla **Seleccionar elementos de los que realizar copia de seguridad**, haga clic en **Agregar elementos**.</span><span class="sxs-lookup"><span data-stu-id="906cd-174">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="906cd-175">También puede establecer preferencias en **Configuración de exclusión** , en esta página del asistente.</span><span class="sxs-lookup"><span data-stu-id="906cd-175">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="906cd-176">Si quiere excluir archivos o tipos de archivos, lea el procedimiento para agregar [configuración de exclusión](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="906cd-176">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="906cd-177">Seleccione los archivos y las carpetas de los que quiere realizar la copia de seguridad y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="906cd-177">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Agregar elementos](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="906cd-179">Especifique la **programación de copia de seguridad** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="906cd-179">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="906cd-180">Puede programar copias de seguridad diarias (un máximo de 3 veces al día) o semanales.</span><span class="sxs-lookup"><span data-stu-id="906cd-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Especificación de la programación de copias de seguridad](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="906cd-182">En este [artículo](backup-azure-backup-cloud-as-tape.md)se explica detalladamente cómo especificar la programación de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="906cd-182">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="906cd-183">Seleccione la **directiva de retención de la copia de seguridad** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="906cd-183">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Selección de la directiva de retención](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="906cd-185">En la pantalla **Confirmación**, revise la información y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="906cd-185">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="906cd-186">Cuando el asistente finalice la creación de la **programación de copia de seguridad**, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="906cd-186">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="906cd-187">Tras modificar la protección, puede confirmar que las copias de seguridad se estén activando correctamente; para ello, vaya a la pestaña **Trabajos** y confirme que se hayan reflejado los cambios en los trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="906cd-187">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="906cd-188">Habilitación de la limitación de la red</span><span class="sxs-lookup"><span data-stu-id="906cd-188">Enable Network Throttling</span></span>
<span data-ttu-id="906cd-189">En el agente de Azure Backup se incluye la pestaña Limitación, donde podrá controlar cómo se utiliza el ancho de banda de red durante la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="906cd-189">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="906cd-190">Este control puede resultar de ayuda si necesita realizar una copia de seguridad de los datos durante las horas de trabajo, pero no quiere que el proceso interfiera con otro tráfico de Internet.</span><span class="sxs-lookup"><span data-stu-id="906cd-190">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="906cd-191">La limitación de la transferencia de datos se aplica a las actividades de copia de seguridad y restauración.</span><span class="sxs-lookup"><span data-stu-id="906cd-191">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="906cd-192">Para habilitar la limitación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="906cd-192">To enable throttling:</span></span>

1. <span data-ttu-id="906cd-193">En el **agente de Backup**, haga clic en **Cambiar propiedades**.</span><span class="sxs-lookup"><span data-stu-id="906cd-193">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="906cd-194">Active la casilla **Habilitar límite de uso del ancho de banda de Internet para las operaciones de copia de seguridad** .</span><span class="sxs-lookup"><span data-stu-id="906cd-194">Select the **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Limitación de la red](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="906cd-196">Una vez que se ha habilitado la limitación, especifique el ancho de banda permitido para la transferencia de datos de copia de seguridad durante la **jornada laboral** y las **horas de descanso**.</span><span class="sxs-lookup"><span data-stu-id="906cd-196">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="906cd-197">Los valores de ancho de banda comienzan en 512 kilobytes por segundo (Kbps) y pueden subir hasta 1023 megabytes por segundo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="906cd-197">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="906cd-198">También puede designar el inicio y el final de la **jornada laboral**, así como qué días de la semana se consideran laborables.</span><span class="sxs-lookup"><span data-stu-id="906cd-198">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="906cd-199">El tiempo no comprendido en la jornada laboral designada se considera horas de descanso.</span><span class="sxs-lookup"><span data-stu-id="906cd-199">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
4. <span data-ttu-id="906cd-200">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="906cd-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="906cd-201">Configuración de exclusión</span><span class="sxs-lookup"><span data-stu-id="906cd-201">Exclusion settings</span></span>
1. <span data-ttu-id="906cd-202">Abra el **agente de Copia de seguridad de Microsoft Azure** (puede encontrarlo si busca en su equipo *Copia de seguridad de Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="906cd-202">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Apertura del agente de copia de seguridad](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="906cd-204">En el agente de Copia de seguridad de Microsoft Azure, haga clic en **Programar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="906cd-204">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="906cd-206">En el Asistente para programar copias de seguridad deje activada la opción **Cambiar la hora o las horas de las copias de seguridad** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="906cd-206">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Modificación de una programación](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="906cd-208">Haga clic en **Configuración de exclusión**.</span><span class="sxs-lookup"><span data-stu-id="906cd-208">Click **Exclusions Settings**.</span></span>

    ![Selección de elementos para su exclusión](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="906cd-210">Haga clic en **Agregar exclusión**.</span><span class="sxs-lookup"><span data-stu-id="906cd-210">Click **Add Exclusion**.</span></span>

    ![Adición de exclusiones](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="906cd-212">Seleccione la ubicación y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="906cd-212">Select the location and then, click **OK**.</span></span>

    ![Selección de una ubicación para la exclusión](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="906cd-214">Agregue la extensión de archivo en el campo **Tipo de archivo** .</span><span class="sxs-lookup"><span data-stu-id="906cd-214">Add the file extension in the **File Type** field.</span></span>

    ![Exclusión por tipo de archivo](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="906cd-216">Adición de una extensión .mp3</span><span class="sxs-lookup"><span data-stu-id="906cd-216">Adding an .mp3 extension</span></span>

    ![Ejemplo de tipo de archivo](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="906cd-218">Para agregar otra extensión, haga clic en **Agregar exclusión** y especifique otra extensión de tipo de archivo (por ejemplo, .jpeg).</span><span class="sxs-lookup"><span data-stu-id="906cd-218">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Otro ejemplo de tipo de archivo](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="906cd-220">Cuando haya agregado todas las extensiones, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="906cd-220">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="906cd-221">Avance por las distintas pantallas del Asistente para programar copias de seguridad haciendo clic en **Siguiente** hasta llegar a la página **Confirmación** y, después, en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="906cd-221">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Confirmación de exclusión](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="906cd-223">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="906cd-223">Next steps</span></span>
* [<span data-ttu-id="906cd-224">Restauración de Windows Server o el cliente de Windows desde Azure</span><span class="sxs-lookup"><span data-stu-id="906cd-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="906cd-225">Para obtener más información sobre Azure Backup, consulte [Información general de Azure Backup](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="906cd-225">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="906cd-226">Visite el [Foro de Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="906cd-226">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
