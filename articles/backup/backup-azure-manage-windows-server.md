---
title: "almacenes y servidores de servicios de aaaManage recuperación de Azure | Documentos de Microsoft"
description: "Use este tutorial toolearn cómo los servicios de recuperación de Azure toomanage almacenes de credenciales y los servidores."
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
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="9586d-103">Supervisión y administración de almacenes y servidores de los Servicios de recuperación de Azure para máquinas Windows</span><span class="sxs-lookup"><span data-stu-id="9586d-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9586d-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9586d-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="9586d-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="9586d-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="9586d-106">En este artículo encontrará información general del programa Hola a copia de seguridad tareas de administración y supervisión disponibles a través de hello el agente de copia de seguridad de Microsoft Azure hello y portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9586d-106">In this article you'll find an overview of hello backup monitor and management tasks available through hello Azure portal and hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="9586d-107">En este artículo se asume que ya tiene una suscripción de Azure y que ha creado al menos un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="9586d-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="9586d-108">Apertura de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="9586d-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="9586d-109">panel de almacén de servicios de recuperación de Hello muestra detalles de Hola o los atributos de un almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="9586d-109">hello Recovery Services vault dashboard shows you hello details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="9586d-110">Inicie sesión en toohello [Portal de Azure](https://portal.azure.com/) con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9586d-110">Sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="9586d-111">En el menú del concentrador hello, haga clic en **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="9586d-111">On hello Hub menu, click **More Services**.</span></span>

    ![Apertura de la lista de almacenes de Recovery Services paso 1.](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="9586d-113">Desea tooopen un almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="9586d-113">You want tooopen a Recovery Services vault.</span></span> <span data-ttu-id="9586d-114">En el cuadro de diálogo de hello, comience a escribir **servicios de recuperación**.</span><span class="sxs-lookup"><span data-stu-id="9586d-114">In hello dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="9586d-115">Cuando empiece a escribir, se filtrará la lista de hello en función de los datos especificados.</span><span class="sxs-lookup"><span data-stu-id="9586d-115">As you begin typing, hello list will filter based on your input.</span></span> <span data-ttu-id="9586d-116">Haga clic en **servicios de recuperación de los almacenes de credenciales** toodisplay lista de hello de servicios de recuperación de los almacenes de credenciales en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="9586d-116">Click **Recovery Services vaults** toodisplay hello list of Recovery Services vaults in your subscription.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="9586d-118">Abre la lista de Hola de almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="9586d-118">hello list of Recovery Services vaults opens.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="9586d-120">En lista de Hola de almacenes de credenciales, seleccione nombre de Hola de hello almacén de servicios de recuperación que desee tooopen.</span><span class="sxs-lookup"><span data-stu-id="9586d-120">From hello list of vaults, select hello name of hello Recovery Services vault you want tooopen.</span></span> <span data-ttu-id="9586d-121">se abre la hoja de panel de almacén de servicios de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-121">hello Recovery Services vault dashboard blade opens.</span></span>

    ![panel del almacén de Servicios de recuperación](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="9586d-123">Ahora que ha abierto el almacén de servicios de recuperación de hello, lleve a cabo cualquiera de las tareas de supervisión o administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-123">Now that you have opened hello Recovery Services vault, try any of hello monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="9586d-124">Supervisión de trabajos y alertas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9586d-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="9586d-125">Supervisar trabajos y almacén de servicios de recuperación de las alertas de hello panel, donde verá:</span><span class="sxs-lookup"><span data-stu-id="9586d-125">You monitor jobs and alerts from hello Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="9586d-126">Detalles de las alertas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9586d-126">Backup alerts details</span></span>
* <span data-ttu-id="9586d-127">Archivos y carpetas, así como máquinas virtuales de Azure protegidas en la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="9586d-127">Files and folders, as well as Azure virtual machines protected in hello cloud</span></span>
* <span data-ttu-id="9586d-128">Almacenamiento total usado en Azure</span><span class="sxs-lookup"><span data-stu-id="9586d-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="9586d-129">Estado del trabajo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9586d-129">Backup job status</span></span>

![Copia de seguridad de las tareas del panel](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="9586d-131">Haga clic en información de hello en cada uno de estos iconos abrirá la hoja asociado de Hola donde administrar tareas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="9586d-131">Clicking hello information in each of these tiles will open hello associated blade where you manage related tasks.</span></span>

<span data-ttu-id="9586d-132">De arriba Hola de hello panel:</span><span class="sxs-lookup"><span data-stu-id="9586d-132">From hello top of hello Dashboard:</span></span>

* <span data-ttu-id="9586d-133">El icono de configuración proporciona acceso a las tareas de copia de seguridad disponibles.</span><span class="sxs-lookup"><span data-stu-id="9586d-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="9586d-134">Almacén de copia de seguridad: ayuda a realizar una copia de nuevos archivos y carpetas (o máquinas virtuales de Azure) servicios de recuperación de toohello.</span><span class="sxs-lookup"><span data-stu-id="9586d-134">Backup - helps you back up new files and folders (or Azure VMs) toohello Recovery Services vault.</span></span>
* <span data-ttu-id="9586d-135">Delete: si el almacén de servicios de recuperación ya no se está usando, puede eliminarla toofree liberar espacio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9586d-135">Delete - If a recovery services vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="9586d-136">Delete solo se habilita después de que todos los servidores protegidos que se haya eliminado del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-136">Delete is only enabled after all protected servers have been deleted from hello vault.</span></span>

![Copia de seguridad de las tareas del panel](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="9586d-138">Alertas de copias de seguridad mediante el agente de Azure Backup:</span><span class="sxs-lookup"><span data-stu-id="9586d-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="9586d-139">Nivel de alerta</span><span class="sxs-lookup"><span data-stu-id="9586d-139">Alert Level</span></span> | <span data-ttu-id="9586d-140">Alertas enviadas</span><span class="sxs-lookup"><span data-stu-id="9586d-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="9586d-141">Crítico</span><span class="sxs-lookup"><span data-stu-id="9586d-141">Critical</span></span> |<span data-ttu-id="9586d-142">Error de copia de seguridad, error de recuperación</span><span class="sxs-lookup"><span data-stu-id="9586d-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="9586d-143">Warning (Advertencia)</span><span class="sxs-lookup"><span data-stu-id="9586d-143">Warning</span></span> |<span data-ttu-id="9586d-144">Copia de seguridad completada con advertencias (si no se copian archivos de menos de cien debido a problemas de toocorruption y más de un millón de archivos se copia correctamente)</span><span class="sxs-lookup"><span data-stu-id="9586d-144">Backup completed with warnings (when fewer than one hundred files are not backed up due toocorruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="9586d-145">Informativo</span><span class="sxs-lookup"><span data-stu-id="9586d-145">Informational</span></span> |<span data-ttu-id="9586d-146">None</span><span class="sxs-lookup"><span data-stu-id="9586d-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="9586d-147">Administración de alertas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9586d-147">Manage Backup alerts</span></span>
<span data-ttu-id="9586d-148">Haga clic en hello **alertas de copia de seguridad** icono tooopen hello **alertas de copia de seguridad** hoja y administrar las alertas.</span><span class="sxs-lookup"><span data-stu-id="9586d-148">Click hello **Backup Alerts** tile tooopen hello **Backup Alerts** blade and manage alerts.</span></span>

![Alertas de copias de seguridad](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="9586d-150">mosaico muestra las alertas de copia de seguridad de Hola Hola número de:</span><span class="sxs-lookup"><span data-stu-id="9586d-150">hello Backup Alerts tile shows you hello number of:</span></span>

* <span data-ttu-id="9586d-151">alertas críticas sin resolver en las últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="9586d-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="9586d-152">alertas de advertencia sin resolver en las últimas 24 horas</span><span class="sxs-lookup"><span data-stu-id="9586d-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="9586d-153">Al hacer clic en cada uno de estos vínculos le toohello **alertas de copia de seguridad** hoja con una vista filtrada de estas alertas (críticas o de advertencia).</span><span class="sxs-lookup"><span data-stu-id="9586d-153">Clicking on each of these links takes you toohello **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="9586d-154">Desde la hoja de alertas de copia de seguridad de hello,:</span><span class="sxs-lookup"><span data-stu-id="9586d-154">From hello Backup Alerts blade, you:</span></span>

* <span data-ttu-id="9586d-155">Elija hello tooinclude de información adecuada con las alertas.</span><span class="sxs-lookup"><span data-stu-id="9586d-155">Choose hello appropriate information tooinclude with your alerts.</span></span>

    ![Elegir columnas](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="9586d-157">Filtrar alertas por gravedad, el estado y la hora de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="9586d-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filtrar alertas](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="9586d-159">Configure las notificaciones según la gravedad, la frecuencia y los destinatarios, y active o desactive las alertas.</span><span class="sxs-lookup"><span data-stu-id="9586d-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filtrar alertas](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="9586d-161">Si **por la alerta** se selecciona como hello **notificar** frecuencia se produce ninguna agrupación o la reducción de los correos electrónicos.</span><span class="sxs-lookup"><span data-stu-id="9586d-161">If **Per Alert** is selected as hello **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="9586d-162">Cada alerta generará una notificación.</span><span class="sxs-lookup"><span data-stu-id="9586d-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="9586d-163">Ésta es configuración predeterminada de hello y correo electrónico de resolución de hello también se envía inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="9586d-163">This is hello default setting and hello resolution email is also sent out immediately.</span></span>

<span data-ttu-id="9586d-164">Si **implícita por hora** se selecciona como hello **notificar** frecuencia un correo electrónico se envía el usuario toohello que les indica que hay no resuelta nuevas alertas generadas en hello última hora.</span><span class="sxs-lookup"><span data-stu-id="9586d-164">If **Hourly Digest** is selected as hello **Notify** frequency one email is sent toohello user telling them that there are unresolved new alerts generated in hello last hour.</span></span> <span data-ttu-id="9586d-165">Se envía un correo electrónico de resolución final Hola de hora de Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-165">A resolution email is sent out at hello end of hello hour.</span></span>

<span data-ttu-id="9586d-166">Las alertas se pueden enviar por hello siguientes niveles de gravedad:</span><span class="sxs-lookup"><span data-stu-id="9586d-166">Alerts can be sent for hello following severity levels:</span></span>

* <span data-ttu-id="9586d-167">Crítico</span><span class="sxs-lookup"><span data-stu-id="9586d-167">critical</span></span>
* <span data-ttu-id="9586d-168">Warning (Advertencia)</span><span class="sxs-lookup"><span data-stu-id="9586d-168">warning</span></span>
* <span data-ttu-id="9586d-169">informativo</span><span class="sxs-lookup"><span data-stu-id="9586d-169">information</span></span>

<span data-ttu-id="9586d-170">Desactivar alerta Hola con hello **desactivar** botón en la hoja de detalles del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-170">You inactivate hello alert with hello **inactivate** button in hello job details blade.</span></span> <span data-ttu-id="9586d-171">Al hacer clic en Desactivar, puede proporcionar notas de resolución.</span><span class="sxs-lookup"><span data-stu-id="9586d-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="9586d-172">Elegir columnas de hello desea tooappear como parte de la alerta de hello con hello **Elegir columnas** botón.</span><span class="sxs-lookup"><span data-stu-id="9586d-172">You choose hello columns you want tooappear as part of hello alert with hello **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="9586d-173">De hello **configuración** hoja, administrar alertas de copia de seguridad seleccionando **supervisión e informes > alertas y eventos > alertas de copia de seguridad** y, a continuación, haga clic en **filtro** o  **Configurar notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="9586d-173">From hello **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="9586d-174">Administración de elementos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9586d-174">Manage Backup items</span></span>
<span data-ttu-id="9586d-175">Administrar copias de seguridad local ahora está disponible en el portal de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-175">Managing on-premises backups is now available in hello management portal.</span></span> <span data-ttu-id="9586d-176">Sección de copia de seguridad de Hola de, en el panel de Hola Hola **elementos de copia de seguridad** icono muestra el número de Hola de elementos de copia de seguridad protegidos toohello almacén.</span><span class="sxs-lookup"><span data-stu-id="9586d-176">In hello Backup section of hello dashboard, hello **Backup Items** tile shows hello number of backup items protected toohello vault.</span></span>

<span data-ttu-id="9586d-177">Haga clic en **carpetas de archivos** Hola icono elementos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9586d-177">Click **File-Folders** in hello Backup Items tile.</span></span>

![Icono Elementos de copia de seguridad](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="9586d-179">Elementos de copia de seguridad de Hello hoja se abre con hello Filtrar conjunto tooFile-carpeta donde verá cada copia de seguridad específica artículo anotado.</span><span class="sxs-lookup"><span data-stu-id="9586d-179">hello Backup Items blade opens with hello filter set tooFile-Folder where you see each specific backup item listed.</span></span>

![Elementos de copia de seguridad](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="9586d-181">Si selecciona un elemento específico de copia de seguridad de la lista de hello, puede ver detalles esenciales de Hola para ese elemento.</span><span class="sxs-lookup"><span data-stu-id="9586d-181">If you select a specific backup item from hello list, you see hello essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="9586d-182">De hello **configuración** hoja, administrar archivos y carpetas mediante la selección **elementos protegidos > elementos de copia de seguridad** y, a continuación, seleccione **carpetas de archivos** de hello menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="9586d-182">From hello **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

![Elementos de copia de seguridad en la configuración](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="9586d-184">Administración de trabajos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9586d-184">Manage Backup jobs</span></span>
<span data-ttu-id="9586d-185">Trabajos de copia de seguridad local (al servidor local de hello es hacer una copia de seguridad tooAzure) y las copias de seguridad de Azure están visibles en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-185">Backup jobs for both on-premises (when hello on-premises server is backing up tooAzure) and Azure backups are visible in hello dashboard.</span></span>

<span data-ttu-id="9586d-186">En la sección de copias de seguridad del panel de Hola Hola, mosaico de trabajo de copia de seguridad de hello muestra número Hola de trabajos:</span><span class="sxs-lookup"><span data-stu-id="9586d-186">In hello Backup section of hello dashboard, hello Backup job tile shows hello number of jobs:</span></span>

* <span data-ttu-id="9586d-187">En curso</span><span class="sxs-lookup"><span data-stu-id="9586d-187">in progress</span></span>
* <span data-ttu-id="9586d-188">no se pudo Hola últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="9586d-188">failed in hello last 24 hours.</span></span>

<span data-ttu-id="9586d-189">toomanage los trabajos de copia de seguridad, haga clic en hello **trabajos de copia de seguridad** icono, que abre una hoja de trabajos de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-189">toomanage your backup jobs, click hello **Backup Jobs** tile, which opens hello Backup Jobs blade.</span></span>

![Elementos de copia de seguridad en la configuración](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="9586d-191">Modificar información de hello disponible en la hoja de trabajos de copia de seguridad de hello con hello **Elegir columnas** situado en la parte superior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-191">You modify hello information available in hello Backup Jobs blade with hello **Choose columns** button at hello top of hello page.</span></span>

<span data-ttu-id="9586d-192">Hola de uso **filtro** tooselect botón entre los archivos y carpetas y copia de seguridad de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9586d-192">Use hello **Filter** button tooselect between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="9586d-193">Si no ve la copia de seguridad de archivos y carpetas, haga clic en **filtro** situado en la parte superior de Hola de página de Hola y seleccione **archivos y carpetas** desde el menú de tipo de elemento de saludo.</span><span class="sxs-lookup"><span data-stu-id="9586d-193">If you don't see your backed up files and folders, click **Filter** button at hello top of hello page and select **Files and folders** from hello Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="9586d-194">De hello **configuración** hoja, administrar los trabajos de copia de seguridad seleccionando **supervisión e informes > trabajos > trabajos de copia de seguridad** y, a continuación, seleccione **carpetas de archivos** de colocación de Hola tecla menú.</span><span class="sxs-lookup"><span data-stu-id="9586d-194">From hello **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="9586d-195">Supervisión del uso de Copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9586d-195">Monitor Backup usage</span></span>
<span data-ttu-id="9586d-196">En la sección de copias de seguridad del panel de Hola Hola, icono de uso de copia de seguridad de hello muestra el almacenamiento de hello usado en Azure.</span><span class="sxs-lookup"><span data-stu-id="9586d-196">In hello Backup section of hello dashboard, hello Backup Usage tile shows hello storage consumed in Azure.</span></span> <span data-ttu-id="9586d-197">El uso de almacenamiento se proporciona para:</span><span class="sxs-lookup"><span data-stu-id="9586d-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="9586d-198">Uso de almacenamiento LRS asociada con el almacén de hello en la nube</span><span class="sxs-lookup"><span data-stu-id="9586d-198">Cloud LRS storage usage associated with hello vault</span></span>
* <span data-ttu-id="9586d-199">Uso de almacenamiento de nube GRS asociada con el almacén de Hola</span><span class="sxs-lookup"><span data-stu-id="9586d-199">Cloud GRS storage usage associated with hello vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="9586d-200">Administración de los servidores de producción</span><span class="sxs-lookup"><span data-stu-id="9586d-200">Manage your production servers</span></span>
<span data-ttu-id="9586d-201">Haga clic en los servidores de producción de toomanage **configuración**.</span><span class="sxs-lookup"><span data-stu-id="9586d-201">toomanage your production servers, click **Settings**.</span></span>

<span data-ttu-id="9586d-202">En Administrar, haga clic en **Infraestructura de copia de seguridad > Servidores de producción**.</span><span class="sxs-lookup"><span data-stu-id="9586d-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="9586d-203">listas de hoja de servidores de producción de Hello de todos los servidores de producción disponibles.</span><span class="sxs-lookup"><span data-stu-id="9586d-203">hello Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="9586d-204">Haga clic en un servidor en los detalles del servidor de hello lista tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-204">Click on a server in hello list tooopen hello server details.</span></span>

![Elementos protegidos](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a><span data-ttu-id="9586d-206">Agente de copia de seguridad de Azure Hola abierto</span><span class="sxs-lookup"><span data-stu-id="9586d-206">Open hello Azure Backup agent</span></span>
<span data-ttu-id="9586d-207">Abra hello **agente de copia de seguridad de Microsoft Azure** (encontrarlo buscando su equipo para *copia de seguridad de Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="9586d-207">Open hello **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="9586d-209">De hello **acciones** disponible en hello derecha de la consola de agente de copia de seguridad de hello realizar Hola después de las tareas de administración:</span><span class="sxs-lookup"><span data-stu-id="9586d-209">From hello **Actions** available at hello right of hello backup agent console you perform hello following management tasks:</span></span>

* <span data-ttu-id="9586d-210">Registrar un servidor</span><span class="sxs-lookup"><span data-stu-id="9586d-210">Register Server</span></span>
* <span data-ttu-id="9586d-211">Programación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9586d-211">Schedule Backup</span></span>
* <span data-ttu-id="9586d-212">Realizar una copia de seguridad en ese momento</span><span class="sxs-lookup"><span data-stu-id="9586d-212">Back Up now</span></span>
* <span data-ttu-id="9586d-213">Cambiar propiedades</span><span class="sxs-lookup"><span data-stu-id="9586d-213">Change Properties</span></span>

![Acciones de la consola del agente de Microsoft Azure Backup](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="9586d-215">demasiado**recuperar datos**, consulte [restaurar archivos tooa Windows server o el equipo cliente de Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="9586d-215">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-hello-backup-schedule"></a><span data-ttu-id="9586d-216">Modificar programación de copia de seguridad de Hola</span><span class="sxs-lookup"><span data-stu-id="9586d-216">Modify hello backup schedule</span></span>
1. <span data-ttu-id="9586d-217">En el agente de copia de seguridad de Microsoft Azure hello, haga clic en **programar copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="9586d-217">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="9586d-219">Hola **Asistente para la programación de copia de seguridad** deje hello **realizar cambios horas o los elementos de toobackup** opción seleccionada y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9586d-219">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="9586d-221">Si desea tooadd o cambiar elementos en hello **seleccionar elementos tooBackup** pantalla haga clic en **agregar elementos**.</span><span class="sxs-lookup"><span data-stu-id="9586d-221">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="9586d-222">También puede establecer **configuración de exclusión** desde esta página del Asistente para saludo.</span><span class="sxs-lookup"><span data-stu-id="9586d-222">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="9586d-223">Si desea que los archivos tooexclude o tipos de archivo leen el procedimiento de Hola para agregar [configuración de exclusión](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="9586d-223">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="9586d-224">Seleccione Hola archivos y carpetas que desee tooback seguridad y haga clic en **bien**.</span><span class="sxs-lookup"><span data-stu-id="9586d-224">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="9586d-226">Especificar hello **programar copia de seguridad** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9586d-226">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="9586d-227">Puede programar copias de seguridad diarias (un máximo de 3 veces al día) o semanales.</span><span class="sxs-lookup"><span data-stu-id="9586d-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="9586d-229">Especificar la programación de copia de seguridad de Hola se explica con detalle en esta [artículo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="9586d-229">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="9586d-230">Seleccione hello **directiva de retención** para copia de seguridad de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9586d-230">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Elementos para la copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="9586d-232">En hello **confirmación** Hola revisar la información de la pantalla y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="9586d-232">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="9586d-233">Una vez que el Asistente de hello finaliza la creación de hello **programar copia de seguridad**, haga clic en **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="9586d-233">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="9586d-234">Después de modificar la protección, puede confirmar que las copias de seguridad se activan correctamente por van toohello **trabajos** ficha y confirmar que los cambios se reflejan en hello trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9586d-234">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="9586d-235">Habilitación de la limitación de la red</span><span class="sxs-lookup"><span data-stu-id="9586d-235">Enable Network Throttling</span></span>

<span data-ttu-id="9586d-236">agente de copia de seguridad de Azure Hola incluye una pestaña de limitación que permite toocontrol uso de ancho de banda de red durante la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="9586d-236">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="9586d-237">Este control puede ser útil si necesita tooback los datos durante las horas laborables, pero no desea hello toointerfere de proceso de copia de seguridad con otro tráfico de internet.</span><span class="sxs-lookup"><span data-stu-id="9586d-237">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="9586d-238">Limitación de datos transferencia aplica tooback seguridad y restaurar las actividades.</span><span class="sxs-lookup"><span data-stu-id="9586d-238">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="9586d-239">tooenable limitación:</span><span class="sxs-lookup"><span data-stu-id="9586d-239">tooenable throttling:</span></span>

1. <span data-ttu-id="9586d-240">Hola **agente de copia de seguridad**, haga clic en **cambiar las propiedades de**.</span><span class="sxs-lookup"><span data-stu-id="9586d-240">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="9586d-241">En Hola ** limitación ficha, seleccione **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet**.</span><span class="sxs-lookup"><span data-stu-id="9586d-241">On hello **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Limitación de la red](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="9586d-243">Una vez habilitada la limitación, especifique Hola permitido ancho de banda para transfirieron datos de copia de seguridad durante la **horas laborables** y **horas de descanso**.</span><span class="sxs-lookup"><span data-stu-id="9586d-243">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="9586d-244">los valores de ancho de banda de Hello comienzan en 512 kilobytes por segundo (Kbps) y pueden crecer hasta too1023 megabytes por segundo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="9586d-244">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="9586d-245">También puede designar el inicio de Hola y de fin para **horas laborables**, y los días de la semana de Hola se consideran trabajo días.</span><span class="sxs-lookup"><span data-stu-id="9586d-245">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="9586d-246">tiempo de Hello fuera Hola designado horas laborables es considerada toobe horas de descanso.</span><span class="sxs-lookup"><span data-stu-id="9586d-246">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
3. <span data-ttu-id="9586d-247">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9586d-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="9586d-248">Administración de la configuración de exclusión</span><span class="sxs-lookup"><span data-stu-id="9586d-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="9586d-249">Abra hello **agente de copia de seguridad de Microsoft Azure** (puede encontrarlo buscando en el equipo para *copia de seguridad de Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="9586d-249">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="9586d-251">En el agente de copia de seguridad de Microsoft Azure hello, haga clic en **programar copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="9586d-251">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="9586d-253">Hola Asistente para la programación de copia de seguridad deje hello **realizar cambios horas o los elementos de toobackup** opción seleccionada y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9586d-253">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="9586d-255">Haga clic en **Configuración de exclusión**.</span><span class="sxs-lookup"><span data-stu-id="9586d-255">Click **Exclusions Settings**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="9586d-257">Haga clic en **Agregar exclusión**.</span><span class="sxs-lookup"><span data-stu-id="9586d-257">Click **Add Exclusion**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="9586d-259">Seleccionar ubicación de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9586d-259">Select hello location and then, click **OK**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="9586d-261">Agregar extensión de archivo de Hola Hola **tipo de archivo** campo.</span><span class="sxs-lookup"><span data-stu-id="9586d-261">Add hello file extension in hello **File Type** field.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="9586d-263">Adición de una extensión .mp3</span><span class="sxs-lookup"><span data-stu-id="9586d-263">Adding an .mp3 extension</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="9586d-265">tooadd otra extensión, haga clic en **Agregar exclusión** y escriba otra extensión de tipo de archivo (agregar una extensión de JPEG).</span><span class="sxs-lookup"><span data-stu-id="9586d-265">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="9586d-267">Cuando haya agregado todas las extensiones de hello, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9586d-267">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="9586d-268">Continuar a través de hello Asistente para la programación de copia de seguridad haciendo clic en **siguiente** hasta hello **página de confirmación**, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="9586d-268">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="9586d-270">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="9586d-270">Frequently asked questions</span></span>
<span data-ttu-id="9586d-271">**Q1. estado del trabajo de copia de seguridad de Hello muestra como completado en hello agente de copia de seguridad de Azure, ¿por qué no se obtener reflejan inmediatamente en el portal?**</span><span class="sxs-lookup"><span data-stu-id="9586d-271">**Q1. hello backup job status shows as completed in hello Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="9586d-272">R1.</span><span class="sxs-lookup"><span data-stu-id="9586d-272">A1.</span></span> <span data-ttu-id="9586d-273">No existe se en retraso máximo de 15 minutos entre el estado del trabajo de copia de seguridad de Hola refleja en el agente de copia de seguridad de Azure de Hola y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9586d-273">There is at maximum delay of 15 mins between hello backup job status reflected in hello Azure backup agent and hello Azure portal.</span></span>

<span data-ttu-id="9586d-274">**¿Q.2 cuando se produce un error en un trabajo de copia de seguridad, cuánto tiempo tarda tooraise una alerta?**</span><span class="sxs-lookup"><span data-stu-id="9586d-274">**Q.2 When a backup job fails, how long does it take tooraise an alert?**</span></span>

<span data-ttu-id="9586d-275">A.2 una alerta se genera en 20 minutos de hello Azure error de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9586d-275">A.2 An alert is raised within 20 mins of hello Azure backup failure.</span></span>

<span data-ttu-id="9586d-276">**P3. ¿Hay algún caso en el que no se envíe ningún correo electrónico si se configuran las notificaciones?**</span><span class="sxs-lookup"><span data-stu-id="9586d-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="9586d-277">R3.</span><span class="sxs-lookup"><span data-stu-id="9586d-277">A3.</span></span> <span data-ttu-id="9586d-278">A continuación se muestran casos de hello cuando no se enviará la notificación de hello en alertas irrelevantes de orden tooreduce hello:</span><span class="sxs-lookup"><span data-stu-id="9586d-278">Below are hello cases when hello notification will not be sent in order tooreduce hello alert noise:</span></span>

* <span data-ttu-id="9586d-279">Si se configuran las notificaciones por hora y una alerta se genera y resuelto durante la hora de Hola</span><span class="sxs-lookup"><span data-stu-id="9586d-279">If notifications are configured hourly and an alert is raised and resolved within hello hour</span></span>
* <span data-ttu-id="9586d-280">Se canceló el trabajo.</span><span class="sxs-lookup"><span data-stu-id="9586d-280">Job is canceled.</span></span>
* <span data-ttu-id="9586d-281">Se produjo un error en el segundo trabajo de copia de seguridad porque el trabajo de copia de seguridad original está en curso.</span><span class="sxs-lookup"><span data-stu-id="9586d-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="9586d-282">Solución de problemas de supervisión</span><span class="sxs-lookup"><span data-stu-id="9586d-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="9586d-283">**Problema:** trabajos y alertas desde el agente de copia de seguridad de Azure de hello no aparecen en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9586d-283">**Issue:** Jobs and/or alerts from hello Azure Backup agent do not appear in hello portal.</span></span>

<span data-ttu-id="9586d-284">**Pasos para solucionar problemas:** Hola proceso, ```OBRecoveryServicesManagementAgent```, envía Hola toohello de datos de alerta y el trabajo de servicio de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="9586d-284">**Troubleshooting steps:** hello process, ```OBRecoveryServicesManagementAgent```, sends hello job and alert data toohello Azure Backup service.</span></span> <span data-ttu-id="9586d-285">En ocasiones este proceso puede quedar atascado o apagado.</span><span class="sxs-lookup"><span data-stu-id="9586d-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="9586d-286">no se está ejecutando el proceso de hello tooverify, abra **el Administrador de tareas** y compruebe si hello ```OBRecoveryServicesManagementAgent``` proceso se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="9586d-286">tooverify hello process is not running, open **Task Manager** and check if hello ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="9586d-287">Suponiendo que no se está ejecutando el proceso de hello, abra **el Panel de Control** y examinar la lista de hello de servicios.</span><span class="sxs-lookup"><span data-stu-id="9586d-287">Assuming that hello process is not running, open **Control Panel** and browse hello list of services.</span></span> <span data-ttu-id="9586d-288">Inicie o reinicie el **agente de administración de Microsoft Azure Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="9586d-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="9586d-289">Para obtener más información, examine los registros de hello en:</span><span class="sxs-lookup"><span data-stu-id="9586d-289">For further information, browse hello logs at:</span></span><br/><span data-ttu-id="9586d-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9586d-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="9586d-291">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9586d-291">Next steps</span></span>
* [<span data-ttu-id="9586d-292">Restauración de Windows Server o el cliente de Windows desde Azure</span><span class="sxs-lookup"><span data-stu-id="9586d-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="9586d-293">toolearn más información acerca de la copia de seguridad de Azure, consulte [información general sobre la copia de seguridad de Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="9586d-293">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="9586d-294">Visite hello [foro de copia de seguridad de Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="9586d-294">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
