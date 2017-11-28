---
title: "Administración de almacenes y servidores de Azure Recovery Services | Microsoft Docs"
description: "Use este tutorial para aprender a administrar almacenes y servidores de Servicios de recuperación de Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: 5922e308f5c205a07bd329c28322ae82cea0e1fa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="b551a-103">Supervisión y administración de almacenes y servidores de los Servicios de recuperación de Azure para máquinas Windows</span><span class="sxs-lookup"><span data-stu-id="b551a-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b551a-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b551a-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="b551a-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="b551a-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="b551a-106">En este artículo encontrará información general sobre las tareas de administración y supervisión de copias de seguridad que tiene disponibles en Azure Portal y en el agente de Microsoft Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="b551a-106">In this article you'll find an overview of the backup monitor and management tasks available through the Azure portal and the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="b551a-107">En este artículo se asume que ya tiene una suscripción de Azure y que ha creado al menos un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="b551a-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="b551a-108">Apertura de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b551a-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="b551a-109">El panel de almacén de Recovery Services muestra los detalles o los atributos de un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="b551a-109">The Recovery Services vault dashboard shows you the details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="b551a-110">Inicie sesión en el [Portal de Azure](https://portal.azure.com/) mediante la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b551a-110">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="b551a-111">En el menú central, haga clic en **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="b551a-111">On the Hub menu, click **More Services**.</span></span>

    ![Apertura de la lista de almacenes de Recovery Services paso 1.](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="b551a-113">Quiere abrir un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="b551a-113">You want to open a Recovery Services vault.</span></span> <span data-ttu-id="b551a-114">En el cuadro de diálogo, comience a escribir **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="b551a-114">In the dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="b551a-115">Cuando comience a escribir, la lista se filtrará en función de la entrada.</span><span class="sxs-lookup"><span data-stu-id="b551a-115">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="b551a-116">Haga clic en **Almacenes de Recovery Services** para mostrar la lista de almacenes de Recovery Services de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b551a-116">Click **Recovery Services vaults** to display the list of Recovery Services vaults in your subscription.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="b551a-118">Se abre la lista de almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="b551a-118">The list of Recovery Services vaults opens.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="b551a-120">En la lista de almacenes, seleccione el nombre del almacén de Recovery Services que quiere abrir.</span><span class="sxs-lookup"><span data-stu-id="b551a-120">From the list of vaults, select the name of the Recovery Services vault you want to open.</span></span> <span data-ttu-id="b551a-121">Se abre la hoja del panel del almacén de Servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b551a-121">The Recovery Services vault dashboard blade opens.</span></span>

    ![panel del almacén de Servicios de recuperación](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="b551a-123">Ahora que ha abierto el almacén de Recovery Services, pruebe cualquiera de las tareas de supervisión o administración.</span><span class="sxs-lookup"><span data-stu-id="b551a-123">Now that you have opened the Recovery Services vault, try any of the monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="b551a-124">Supervisión de trabajos y alertas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b551a-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="b551a-125">Puede supervisar los trabajos y alertas desde el panel del almacén de Servicios de recuperación, en el que encontrará:</span><span class="sxs-lookup"><span data-stu-id="b551a-125">You monitor jobs and alerts from the Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="b551a-126">Detalles de las alertas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b551a-126">Backup alerts details</span></span>
* <span data-ttu-id="b551a-127">Archivos y carpetas, así como las máquinas virtuales de Azure protegidas en la nube</span><span class="sxs-lookup"><span data-stu-id="b551a-127">Files and folders, as well as Azure virtual machines protected in the cloud</span></span>
* <span data-ttu-id="b551a-128">Almacenamiento total usado en Azure</span><span class="sxs-lookup"><span data-stu-id="b551a-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="b551a-129">Estado del trabajo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b551a-129">Backup job status</span></span>

![Copia de seguridad de las tareas del panel](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="b551a-131">Si hace clic en la información de cada uno de estos iconos, se abrirá la hoja asociada en la que podrá administrar las tareas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="b551a-131">Clicking the information in each of these tiles will open the associated blade where you manage related tasks.</span></span>

<span data-ttu-id="b551a-132">En la parte superior del panel:</span><span class="sxs-lookup"><span data-stu-id="b551a-132">From the top of the Dashboard:</span></span>

* <span data-ttu-id="b551a-133">El icono de configuración proporciona acceso a las tareas de copia de seguridad disponibles.</span><span class="sxs-lookup"><span data-stu-id="b551a-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="b551a-134">El icono de copia de seguridad: ayuda a realizar la copia de seguridad de nuevos archivos y carpetas (o máquinas virtuales de Azure) en el almacén de Servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b551a-134">Backup - helps you back up new files and folders (or Azure VMs) to the Recovery Services vault.</span></span>
* <span data-ttu-id="b551a-135">El icono de eliminación: en caso de que ya no se use un almacén de Servicios de recuperación, puede eliminarlo para liberar espacio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b551a-135">Delete - If a recovery services vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="b551a-136">Este icono solo estará habilitado después de que todos los servidores protegidos se hayan eliminado del almacén.</span><span class="sxs-lookup"><span data-stu-id="b551a-136">Delete is only enabled after all protected servers have been deleted from the vault.</span></span>

![Copia de seguridad de las tareas del panel](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="b551a-138">Alertas de copias de seguridad mediante el agente de Azure Backup:</span><span class="sxs-lookup"><span data-stu-id="b551a-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="b551a-139">Nivel de alerta</span><span class="sxs-lookup"><span data-stu-id="b551a-139">Alert Level</span></span> | <span data-ttu-id="b551a-140">Alertas enviadas</span><span class="sxs-lookup"><span data-stu-id="b551a-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="b551a-141">Crítico</span><span class="sxs-lookup"><span data-stu-id="b551a-141">Critical</span></span> |<span data-ttu-id="b551a-142">Error de copia de seguridad, error de recuperación</span><span class="sxs-lookup"><span data-stu-id="b551a-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="b551a-143">Warning (Advertencia)</span><span class="sxs-lookup"><span data-stu-id="b551a-143">Warning</span></span> |<span data-ttu-id="b551a-144">Copia de seguridad completada con advertencias (cuando menos de cien archivos no se copian debido a problemas de daños y más de un millón de archivos se copian correctamente)</span><span class="sxs-lookup"><span data-stu-id="b551a-144">Backup completed with warnings (when fewer than one hundred files are not backed up due to corruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="b551a-145">Informativo</span><span class="sxs-lookup"><span data-stu-id="b551a-145">Informational</span></span> |<span data-ttu-id="b551a-146">None</span><span class="sxs-lookup"><span data-stu-id="b551a-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="b551a-147">Administración de alertas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b551a-147">Manage Backup alerts</span></span>
<span data-ttu-id="b551a-148">Haga clic en el icono de **Alertas de copias de seguridad** para abrir la hoja **Alertas de copias de seguridad** y administrar las alertas.</span><span class="sxs-lookup"><span data-stu-id="b551a-148">Click the **Backup Alerts** tile to open the **Backup Alerts** blade and manage alerts.</span></span>

![Alertas de copias de seguridad](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="b551a-150">El icono de alertas de copia de seguridad le muestra el número de:</span><span class="sxs-lookup"><span data-stu-id="b551a-150">The Backup Alerts tile shows you the number of:</span></span>

* <span data-ttu-id="b551a-151">alertas críticas sin resolver en las últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="b551a-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="b551a-152">alertas de advertencia sin resolver en las últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="b551a-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="b551a-153">Si hace clic en cada uno de estos vínculos le llevarán a la hoja **Alertas de copias de seguridad** con una vista filtrada de estas alertas (críticas o de advertencia).</span><span class="sxs-lookup"><span data-stu-id="b551a-153">Clicking on each of these links takes you to the **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="b551a-154">En la hoja Alertas de copias de seguridad, puede:</span><span class="sxs-lookup"><span data-stu-id="b551a-154">From the Backup Alerts blade, you:</span></span>

* <span data-ttu-id="b551a-155">Elegir la información adecuada para incluir con sus alertas.</span><span class="sxs-lookup"><span data-stu-id="b551a-155">Choose the appropriate information to include with your alerts.</span></span>

    ![Elegir columnas](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="b551a-157">Filtrar alertas por gravedad, el estado y la hora de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="b551a-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filtrar alertas](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="b551a-159">Configure las notificaciones según la gravedad, la frecuencia y los destinatarios, y active o desactive las alertas.</span><span class="sxs-lookup"><span data-stu-id="b551a-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filtrar alertas](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="b551a-161">Si está seleccionada la opción **Por alerta** como frecuencia en **Notificar** no se producirá ninguna agrupación ni reducción de los correos electrónicos.</span><span class="sxs-lookup"><span data-stu-id="b551a-161">If **Per Alert** is selected as the **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="b551a-162">Cada alerta generará una notificación.</span><span class="sxs-lookup"><span data-stu-id="b551a-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="b551a-163">Esta es la configuración predeterminada y el correo electrónico de resolución también se envía inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="b551a-163">This is the default setting and the resolution email is also sent out immediately.</span></span>

<span data-ttu-id="b551a-164">Si se selecciona la opción **Resumen cada hora** como frecuencia en **Notificar** se envía un correo electrónico al usuario indicándole que hay nuevas alertas sin resolver generadas en la última hora.</span><span class="sxs-lookup"><span data-stu-id="b551a-164">If **Hourly Digest** is selected as the **Notify** frequency one email is sent to the user telling them that there are unresolved new alerts generated in the last hour.</span></span> <span data-ttu-id="b551a-165">Se envía un correo electrónico de resolución al final del período de una hora.</span><span class="sxs-lookup"><span data-stu-id="b551a-165">A resolution email is sent out at the end of the hour.</span></span>

<span data-ttu-id="b551a-166">Se pueden enviar alertas para los siguientes niveles de gravedad:</span><span class="sxs-lookup"><span data-stu-id="b551a-166">Alerts can be sent for the following severity levels:</span></span>

* <span data-ttu-id="b551a-167">Crítico</span><span class="sxs-lookup"><span data-stu-id="b551a-167">critical</span></span>
* <span data-ttu-id="b551a-168">Warning (Advertencia)</span><span class="sxs-lookup"><span data-stu-id="b551a-168">warning</span></span>
* <span data-ttu-id="b551a-169">informativo</span><span class="sxs-lookup"><span data-stu-id="b551a-169">information</span></span>

<span data-ttu-id="b551a-170">Desactive la alerta con el botón **Desactivar** en la hoja de detalles del trabajo.</span><span class="sxs-lookup"><span data-stu-id="b551a-170">You inactivate the alert with the **inactivate** button in the job details blade.</span></span> <span data-ttu-id="b551a-171">Al hacer clic en Desactivar, puede proporcionar notas de resolución.</span><span class="sxs-lookup"><span data-stu-id="b551a-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="b551a-172">Elija las columnas que desea que aparezcan como parte de la alerta con el botón **Elegir columnas** .</span><span class="sxs-lookup"><span data-stu-id="b551a-172">You choose the columns you want to appear as part of the alert with the **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="b551a-173">En la hoja **Configuración**, puede administrar alertas de copias de seguridad seleccionando **Supervisión e informes > Alertas y eventos > Alertas de copias de seguridad** y haciendo clic en **Filtrar** o en **Configurar notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="b551a-173">From the **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="b551a-174">Administración de elementos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b551a-174">Manage Backup items</span></span>
<span data-ttu-id="b551a-175">La administración de copias de seguridad locales ya está disponible en el Portal de administración.</span><span class="sxs-lookup"><span data-stu-id="b551a-175">Managing on-premises backups is now available in the management portal.</span></span> <span data-ttu-id="b551a-176">En la sección Copia de seguridad del panel, el icono **Elementos de copia de seguridad** muestra el número de elementos de copia de seguridad protegidos en el almacén.</span><span class="sxs-lookup"><span data-stu-id="b551a-176">In the Backup section of the dashboard, the **Backup Items** tile shows the number of backup items protected to the vault.</span></span>

<span data-ttu-id="b551a-177">Haga clic en **Archivos y carpetas** en el icono Elementos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b551a-177">Click **File-Folders** in the Backup Items tile.</span></span>

![Icono Elementos de copia de seguridad](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="b551a-179">Se abre la hoja Elementos de copia de seguridad con el filtro establecido en Archivos y carpetas en el que podrá ver cada elemento de copia de seguridad específico en una lista.</span><span class="sxs-lookup"><span data-stu-id="b551a-179">The Backup Items blade opens with the filter set to File-Folder where you see each specific backup item listed.</span></span>

![Elementos de copia de seguridad](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="b551a-181">Si selecciona un elemento de una copia de seguridad específica de la lista, podrá ver los detalles esenciales de ese elemento.</span><span class="sxs-lookup"><span data-stu-id="b551a-181">If you select a specific backup item from the list, you see the essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="b551a-182">Desde la hoja **Configuración**, puede administrar los archivos y carpetas seleccionando **Elementos protegidos > Elementos de copia de seguridad** y, a continuación, **Archivos y carpetas** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="b551a-182">From the **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

![Elementos de copia de seguridad en la configuración](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="b551a-184">Administración de trabajos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b551a-184">Manage Backup jobs</span></span>
<span data-ttu-id="b551a-185">Los trabajos de copia de seguridad locales (cuando el servidor local realiza la copia de seguridad en Azure) y los de copias de seguridad de Azure aparecen en el panel.</span><span class="sxs-lookup"><span data-stu-id="b551a-185">Backup jobs for both on-premises (when the on-premises server is backing up to Azure) and Azure backups are visible in the dashboard.</span></span>

<span data-ttu-id="b551a-186">En la sección Copia de seguridad del panel, el icono Trabajo de copia de seguridad muestra el número de trabajos:</span><span class="sxs-lookup"><span data-stu-id="b551a-186">In the Backup section of the dashboard, the Backup job tile shows the number of jobs:</span></span>

* <span data-ttu-id="b551a-187">En curso</span><span class="sxs-lookup"><span data-stu-id="b551a-187">in progress</span></span>
* <span data-ttu-id="b551a-188">Con error en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b551a-188">failed in the last 24 hours.</span></span>

<span data-ttu-id="b551a-189">Para administrar los trabajos de copia de seguridad, haga clic en el icono **Trabajos de copia de seguridad** que permite abrir la hoja del mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="b551a-189">To manage your backup jobs, click the **Backup Jobs** tile, which opens the Backup Jobs blade.</span></span>

![Elementos de copia de seguridad en la configuración](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="b551a-191">Puede modificar la información disponible en la hoja Trabajos de copia de seguridad con el botón **Elegir columnas** situado en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="b551a-191">You modify the information available in the Backup Jobs blade with the **Choose columns** button at the top of the page.</span></span>

<span data-ttu-id="b551a-192">Use el botón **Filtrar** para seleccionar entre Archivos y carpetas y Copia de seguridad de la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="b551a-192">Use the **Filter** button to select between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="b551a-193">Si no ve los archivos y carpetas de los que se ha realizado la copia de seguridad, haga clic en el botón **Filtrar** situado en la parte superior de la página y seleccione **Archivos y carpetas** en el menú Tipo de elemento.</span><span class="sxs-lookup"><span data-stu-id="b551a-193">If you don't see your backed up files and folders, click **Filter** button at the top of the page and select **Files and folders** from the Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="b551a-194">En la hoja **Configuración**, puede administrar los trabajos de copia de seguridad mediante **Supervisión e informes > Trabajos > Trabajos de copia de seguridad** y, a continuación, seleccionando **Archivos y carpetas** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="b551a-194">From the **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="b551a-195">Supervisión del uso de Copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b551a-195">Monitor Backup usage</span></span>
<span data-ttu-id="b551a-196">En la sección Copia de seguridad del panel, el icono Uso de copia de seguridad muestra el almacenamiento consumido en Azure.</span><span class="sxs-lookup"><span data-stu-id="b551a-196">In the Backup section of the dashboard, the Backup Usage tile shows the storage consumed in Azure.</span></span> <span data-ttu-id="b551a-197">El uso de almacenamiento se proporciona para:</span><span class="sxs-lookup"><span data-stu-id="b551a-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="b551a-198">Uso de almacenamiento LRS en la nube asociado con el almacén</span><span class="sxs-lookup"><span data-stu-id="b551a-198">Cloud LRS storage usage associated with the vault</span></span>
* <span data-ttu-id="b551a-199">Uso de almacenamiento GRS en la nube asociado con el almacén</span><span class="sxs-lookup"><span data-stu-id="b551a-199">Cloud GRS storage usage associated with the vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="b551a-200">Administración de los servidores de producción</span><span class="sxs-lookup"><span data-stu-id="b551a-200">Manage your production servers</span></span>
<span data-ttu-id="b551a-201">Para administrar los servidores de producción, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="b551a-201">To manage your production servers, click **Settings**.</span></span>

<span data-ttu-id="b551a-202">En Administrar, haga clic en **Infraestructura de copia de seguridad > Servidores de producción**.</span><span class="sxs-lookup"><span data-stu-id="b551a-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="b551a-203">La hoja Servidores de producción muestra todos los servidores de producción disponibles.</span><span class="sxs-lookup"><span data-stu-id="b551a-203">The Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="b551a-204">Haga clic en un servidor de la lista para abrir los detalles del servidor.</span><span class="sxs-lookup"><span data-stu-id="b551a-204">Click on a server in the list to open the server details.</span></span>

![Elementos protegidos](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-the-azure-backup-agent"></a><span data-ttu-id="b551a-206">Apertura del agente de Azure Backup</span><span class="sxs-lookup"><span data-stu-id="b551a-206">Open the Azure Backup agent</span></span>
<span data-ttu-id="b551a-207">Abra el **agente de Microsoft Azure Backup** (puede encontrarlo si busca en su equipo *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="b551a-207">Open the **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="b551a-209">Con las **acciones** disponibles en la parte derecha de la consola del agente de Copia de seguridad, podrá llevar a cabo las siguientes tareas de administración:</span><span class="sxs-lookup"><span data-stu-id="b551a-209">From the **Actions** available at the right of the backup agent console you perform the following management tasks:</span></span>

* <span data-ttu-id="b551a-210">Registrar un servidor</span><span class="sxs-lookup"><span data-stu-id="b551a-210">Register Server</span></span>
* <span data-ttu-id="b551a-211">Programación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="b551a-211">Schedule Backup</span></span>
* <span data-ttu-id="b551a-212">Realizar una copia de seguridad en ese momento</span><span class="sxs-lookup"><span data-stu-id="b551a-212">Back Up now</span></span>
* <span data-ttu-id="b551a-213">Cambiar propiedades</span><span class="sxs-lookup"><span data-stu-id="b551a-213">Change Properties</span></span>

![Acciones de la consola del agente de Microsoft Azure Backup](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="b551a-215">Para **recuperar datos**, consulte [Restauración de archivos en una máquina de Windows Server o del cliente de Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="b551a-215">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-the-backup-schedule"></a><span data-ttu-id="b551a-216">Modificación de la programación de copias de seguridad</span><span class="sxs-lookup"><span data-stu-id="b551a-216">Modify the backup schedule</span></span>
1. <span data-ttu-id="b551a-217">En el agente de Microsoft Azure Backup, haga clic en **Programar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="b551a-217">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="b551a-219">En el **Asistente para programar copias de seguridad**, deje activada la opción **Cambiar la hora o las horas de las copias de seguridad** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b551a-219">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="b551a-221">Si quiere agregar o cambiar elementos, en la pantalla **Seleccionar elementos de los que realizar copia de seguridad**, haga clic en **Agregar elementos**.</span><span class="sxs-lookup"><span data-stu-id="b551a-221">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="b551a-222">También puede establecer preferencias en **Configuración de exclusión** , en esta página del asistente.</span><span class="sxs-lookup"><span data-stu-id="b551a-222">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="b551a-223">Si quiere excluir archivos o tipos de archivos, lea el procedimiento para agregar [configuración de exclusión](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="b551a-223">If you want to exclude files or file types read the procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="b551a-224">Seleccione los archivos y las carpetas de los que quiere realizar la copia de seguridad y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b551a-224">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="b551a-226">Especifique la **programación de copia de seguridad** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b551a-226">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="b551a-227">Puede programar copias de seguridad diarias (un máximo de 3 veces al día) o semanales.</span><span class="sxs-lookup"><span data-stu-id="b551a-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="b551a-229">En este [artículo](backup-azure-backup-cloud-as-tape.md)se explica detalladamente cómo especificar la programación de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b551a-229">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="b551a-230">Seleccione la **directiva de retención de la copia de seguridad** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b551a-230">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="b551a-232">En la pantalla **Confirmación**, revise la información y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="b551a-232">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="b551a-233">Cuando el asistente finalice la creación de la **programación de copia de seguridad**, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="b551a-233">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="b551a-234">Tras modificar la protección, puede confirmar que las copias de seguridad se estén activando correctamente; para ello, vaya a la pestaña **Trabajos** y confirme que se hayan reflejado los cambios en los trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b551a-234">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="b551a-235">Habilitación de la limitación de la red</span><span class="sxs-lookup"><span data-stu-id="b551a-235">Enable Network Throttling</span></span>

<span data-ttu-id="b551a-236">En el agente de Azure Backup se incluye la pestaña Limitación, donde podrá controlar cómo se utiliza el ancho de banda de red durante la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="b551a-236">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="b551a-237">Este control puede resultar de ayuda si necesita realizar una copia de seguridad de los datos durante las horas de trabajo, pero no quiere que el proceso interfiera con otro tráfico de Internet.</span><span class="sxs-lookup"><span data-stu-id="b551a-237">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="b551a-238">La limitación de la transferencia de datos se aplica a las actividades de copia de seguridad y restauración.</span><span class="sxs-lookup"><span data-stu-id="b551a-238">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="b551a-239">Para habilitar la limitación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b551a-239">To enable throttling:</span></span>

1. <span data-ttu-id="b551a-240">En el **agente de Backup**, haga clic en **Cambiar propiedades**.</span><span class="sxs-lookup"><span data-stu-id="b551a-240">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="b551a-241">En la pestaña **Limitación, seleccione la opción **Habilitar límite de uso del ancho de banda de Internet para las operaciones de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="b551a-241">On the **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Limitación de la red](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="b551a-243">Una vez que se ha habilitado la limitación, especifique el ancho de banda permitido para la transferencia de datos de copia de seguridad durante la **jornada laboral** y las **horas de descanso**.</span><span class="sxs-lookup"><span data-stu-id="b551a-243">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="b551a-244">Los valores de ancho de banda comienzan en 512 kilobytes por segundo (Kbps) y pueden subir hasta 1023 megabytes por segundo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="b551a-244">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="b551a-245">También puede designar el inicio y el final de la **jornada laboral**, así como qué días de la semana se consideran laborables.</span><span class="sxs-lookup"><span data-stu-id="b551a-245">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="b551a-246">El tiempo no comprendido en la jornada laboral designada se considera horas de descanso.</span><span class="sxs-lookup"><span data-stu-id="b551a-246">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
3. <span data-ttu-id="b551a-247">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b551a-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="b551a-248">Administración de la configuración de exclusión</span><span class="sxs-lookup"><span data-stu-id="b551a-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="b551a-249">Abra el **agente de Microsoft Azure Backup** (puede encontrarlo si busca en su equipo *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="b551a-249">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="b551a-251">En el agente de Microsoft Azure Backup, haga clic en **Programar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="b551a-251">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="b551a-253">En el Asistente para programar copias de seguridad deje activada la opción **Cambiar la hora o las horas de las copias de seguridad** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b551a-253">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="b551a-255">Haga clic en **Configuración de exclusión**.</span><span class="sxs-lookup"><span data-stu-id="b551a-255">Click **Exclusions Settings**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="b551a-257">Haga clic en **Agregar exclusión**.</span><span class="sxs-lookup"><span data-stu-id="b551a-257">Click **Add Exclusion**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="b551a-259">Seleccione la ubicación y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b551a-259">Select the location and then, click **OK**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="b551a-261">Agregue la extensión de archivo en el campo **Tipo de archivo** .</span><span class="sxs-lookup"><span data-stu-id="b551a-261">Add the file extension in the **File Type** field.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="b551a-263">Adición de una extensión .mp3</span><span class="sxs-lookup"><span data-stu-id="b551a-263">Adding an .mp3 extension</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="b551a-265">Para agregar otra extensión, haga clic en **Agregar exclusión** y especifique otra extensión de tipo de archivo (por ejemplo, .jpeg).</span><span class="sxs-lookup"><span data-stu-id="b551a-265">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="b551a-267">Cuando haya agregado todas las extensiones, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b551a-267">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="b551a-268">Avance por las distintas pantallas del Asistente para programar copias de seguridad haciendo clic en **Siguiente** hasta llegar a la página **Confirmación** y, después, en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="b551a-268">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="b551a-270">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="b551a-270">Frequently asked questions</span></span>
<span data-ttu-id="b551a-271">**P1. El estado del trabajo de copia de seguridad aparece como completado en el agente de Azure Backup, ¿por qué no se ve reflejado inmediatamente en el portal?**</span><span class="sxs-lookup"><span data-stu-id="b551a-271">**Q1. The backup job status shows as completed in the Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="b551a-272">R1.</span><span class="sxs-lookup"><span data-stu-id="b551a-272">A1.</span></span> <span data-ttu-id="b551a-273">Hay un retraso máximo de 15 minutos entre que el estado del trabajo de copia de seguridad se refleja en el agente de Azure Backup y en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b551a-273">There is at maximum delay of 15 mins between the backup job status reflected in the Azure backup agent and the Azure portal.</span></span>

<span data-ttu-id="b551a-274">**P.2 Cuando se produce un error en un trabajo de copia de seguridad, ¿cuánto tiempo se tarda en generar una alerta?**</span><span class="sxs-lookup"><span data-stu-id="b551a-274">**Q.2 When a backup job fails, how long does it take to raise an alert?**</span></span>

<span data-ttu-id="b551a-275">R.2 Se genera una alerta en menos de 20 minutos desde que se produce el error de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="b551a-275">A.2 An alert is raised within 20 mins of the Azure backup failure.</span></span>

<span data-ttu-id="b551a-276">**P3. ¿Hay algún caso en el que no se envíe ningún correo electrónico si se configuran las notificaciones?**</span><span class="sxs-lookup"><span data-stu-id="b551a-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="b551a-277">R3.</span><span class="sxs-lookup"><span data-stu-id="b551a-277">A3.</span></span> <span data-ttu-id="b551a-278">A continuación figuran los casos en los que no se enviará la notificación con el fin de reducir el ruido de las alertas:</span><span class="sxs-lookup"><span data-stu-id="b551a-278">Below are the cases when the notification will not be sent in order to reduce the alert noise:</span></span>

* <span data-ttu-id="b551a-279">Si se configuran las notificaciones por horas y se genera una alerta y esta se resuelve en menos de una hora.</span><span class="sxs-lookup"><span data-stu-id="b551a-279">If notifications are configured hourly and an alert is raised and resolved within the hour</span></span>
* <span data-ttu-id="b551a-280">Se canceló el trabajo.</span><span class="sxs-lookup"><span data-stu-id="b551a-280">Job is canceled.</span></span>
* <span data-ttu-id="b551a-281">Se produjo un error en el segundo trabajo de copia de seguridad porque el trabajo de copia de seguridad original está en curso.</span><span class="sxs-lookup"><span data-stu-id="b551a-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="b551a-282">Solución de problemas de supervisión</span><span class="sxs-lookup"><span data-stu-id="b551a-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="b551a-283">**Problema**: los trabajos y las alertas del agente de Azure Backup no aparecen en el portal.</span><span class="sxs-lookup"><span data-stu-id="b551a-283">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span></span>

<span data-ttu-id="b551a-284">**Pasos para solucionar problemas:** el proceso ```OBRecoveryServicesManagementAgent```, envía los datos de alerta y del trabajo para al servicio de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="b551a-284">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span></span> <span data-ttu-id="b551a-285">En ocasiones este proceso puede quedar atascado o apagado.</span><span class="sxs-lookup"><span data-stu-id="b551a-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="b551a-286">Para comprobar que el proceso no se está ejecutando, abra **Administrador de tareas** y compruebe si el proceso ```OBRecoveryServicesManagementAgent``` se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="b551a-286">To verify the process is not running, open **Task Manager** and check if the ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="b551a-287">Suponiendo que el proceso no se está ejecutando, abra el **Panel de Control** y examine la lista de servicios.</span><span class="sxs-lookup"><span data-stu-id="b551a-287">Assuming that the process is not running, open **Control Panel** and browse the list of services.</span></span> <span data-ttu-id="b551a-288">Inicie o reinicie el **agente de administración de Microsoft Azure Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="b551a-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="b551a-289">Para más información, examine los registros en:</span><span class="sxs-lookup"><span data-stu-id="b551a-289">For further information, browse the logs at:</span></span><br/><span data-ttu-id="b551a-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b551a-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="b551a-291">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b551a-291">Next steps</span></span>
* [<span data-ttu-id="b551a-292">Restauración de Windows Server o el cliente de Windows desde Azure</span><span class="sxs-lookup"><span data-stu-id="b551a-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="b551a-293">Para obtener más información sobre Azure Backup, consulte [Información general de Azure Backup](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="b551a-293">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="b551a-294">Visite el [Foro de Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="b551a-294">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
