---
title: "almacenes de credenciales de copia de seguridad de Azure aaaManage y servidores Azure usando el modelo de implementación clásica de hello | Documentos de Microsoft"
description: "Use este tutorial toolearn cómo almacenes de credenciales toomanage copia de seguridad de Azure y los servidores."
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
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a><span data-ttu-id="e6b43-103">Administrar servidores mediante el modelo de implementación clásica de Hola y almacenes de copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="e6b43-103">Manage Azure Backup vaults and servers using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6b43-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e6b43-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="e6b43-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="e6b43-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="e6b43-106">En este artículo encontrará información general sobre las tareas de administración de copia de seguridad de hello disponibles a través del portal de Azure clásico de Hola y el agente de copia de seguridad de Microsoft Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b43-106">In this article you'll find an overview of hello backup management tasks available through hello Azure classic portal and hello Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6b43-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e6b43-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e6b43-108">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="e6b43-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e6b43-109">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b43-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6b43-110">Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e6b43-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="e6b43-111">Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="e6b43-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="e6b43-112">Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e6b43-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="e6b43-113">Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6b43-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="e6b43-114">**El 1 de noviembre de 2017**:</span><span class="sxs-lookup"><span data-stu-id="e6b43-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="e6b43-115">Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e6b43-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="e6b43-116">No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b43-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="e6b43-117">En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="e6b43-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="e6b43-118">Tareas del Portal de administración</span><span class="sxs-lookup"><span data-stu-id="e6b43-118">Management portal tasks</span></span>
1. <span data-ttu-id="e6b43-119">Inicie sesión en toohello [Portal de administración](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e6b43-119">Sign in toohello [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e6b43-120">Haga clic en **servicios de recuperación**, a continuación, haga clic en nombre de Hola de página de inicio rápido de almacén de copia de seguridad tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b43-120">Click **Recovery Services**, then click hello name of backup vault tooview hello Quick Start page.</span></span>

    ![Servicios de recuperación](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="e6b43-122">Seleccionando las opciones de hello al principio de Hola de página de inicio rápido de hello, puede ver las tareas de administración disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b43-122">By selecting hello options at hello top of hello Quick Start page, you can see hello available management tasks.</span></span>

![Administración de pestañas](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="e6b43-124">Panel</span><span class="sxs-lookup"><span data-stu-id="e6b43-124">Dashboard</span></span>
<span data-ttu-id="e6b43-125">Seleccione **panel** información general del uso de Hola de toosee para servidor hello.</span><span class="sxs-lookup"><span data-stu-id="e6b43-125">Select **Dashboard** toosee hello usage overview for hello server.</span></span> <span data-ttu-id="e6b43-126">Hola **información general del uso** incluye:</span><span class="sxs-lookup"><span data-stu-id="e6b43-126">hello **usage overview** includes:</span></span>

* <span data-ttu-id="e6b43-127">número de Hola de servidores de Windows registrados toocloud</span><span class="sxs-lookup"><span data-stu-id="e6b43-127">hello number of Windows Servers registered toocloud</span></span>
* <span data-ttu-id="e6b43-128">número de Hello máquinas virtuales de Azure protegidas en la nube</span><span class="sxs-lookup"><span data-stu-id="e6b43-128">hello number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="e6b43-129">almacenamiento total Hola usado en Azure</span><span class="sxs-lookup"><span data-stu-id="e6b43-129">hello total storage consumed in Azure</span></span>
* <span data-ttu-id="e6b43-130">estado de Hola de trabajos recientes</span><span class="sxs-lookup"><span data-stu-id="e6b43-130">hello status of recent jobs</span></span>

<span data-ttu-id="e6b43-131">Final de Hola de hello panel puede realizar Hola siguiente las tareas:</span><span class="sxs-lookup"><span data-stu-id="e6b43-131">At hello bottom of hello Dashboard you can perform hello following tasks:</span></span>

* <span data-ttu-id="e6b43-132">**Administrar certificado** : si un certificado era tooregister usado Hola servidor, siga este certificado de hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="e6b43-132">**Manage certificate** - If a certificate was used tooregister hello server, then use this tooupdate hello certificate.</span></span> <span data-ttu-id="e6b43-133">Si usa credenciales de almacén, no utilice **Administrar certificado**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="e6b43-134">**Eliminar** -almacén de copia de seguridad actual de eliminaciones Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b43-134">**Delete** - Deletes hello current backup vault.</span></span> <span data-ttu-id="e6b43-135">Si ya no se utiliza un almacén de copia de seguridad, puede eliminarla toofree liberar espacio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e6b43-135">If a backup vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="e6b43-136">**Eliminar** solo se habilita después de que todos los servidores registrados que se haya eliminado del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b43-136">**Delete** is only enabled after all registered servers have been deleted from hello vault.</span></span>

![Copia de seguridad de las tareas del panel](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="e6b43-138">Elementos registrados</span><span class="sxs-lookup"><span data-stu-id="e6b43-138">Registered items</span></span>
<span data-ttu-id="e6b43-139">Seleccione **elementos registrados** nombres de hello tooview de servidores de Hola que están registran toothis almacén.</span><span class="sxs-lookup"><span data-stu-id="e6b43-139">Select **Registered Items** tooview hello names of hello servers that are registered toothis vault.</span></span>

![Elementos registrados](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="e6b43-141">Hola **tipo** tooAzure Máquina Virtual de valores predeterminados de filtro.</span><span class="sxs-lookup"><span data-stu-id="e6b43-141">hello **Type** filter defaults tooAzure Virtual Machine.</span></span> <span data-ttu-id="e6b43-142">nombres de hello tooview servidores Hola almacén toothis registrados, seleccione **Windows server** de hello menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="e6b43-142">tooview hello names of hello servers that are registered toothis vault, select **Windows server** from hello drop down menu.</span></span>

<span data-ttu-id="e6b43-143">Desde aquí puede realizar Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e6b43-143">From here you can perform hello following tasks:</span></span>

* <span data-ttu-id="e6b43-144">**Permitir un nuevo registro** : cuando se selecciona esta opción para un servidor puede usar hello **Asistente para registro** en hello en copia de seguridad de Microsoft Azure agente tooregister Hola servidor local con el almacén de copia de seguridad de hello una segunda vez .</span><span class="sxs-lookup"><span data-stu-id="e6b43-144">**Allow Re-registration** - When this option is selected for a server you can use hello **Registration Wizard** in hello on-premises Microsoft Azure Backup agent tooregister hello server with hello backup vault a second time.</span></span> <span data-ttu-id="e6b43-145">Puede que tenga el registro toore debido a error de tooan en el certificado de Hola o si un servidor tuviera toobe vuelve a generar.</span><span class="sxs-lookup"><span data-stu-id="e6b43-145">You might need toore-register due tooan error in hello certificate or if a server had toobe rebuilt.</span></span>
* <span data-ttu-id="e6b43-146">**Eliminar** -elimina un servidor de almacén de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b43-146">**Delete** - Deletes a server from hello backup vault.</span></span> <span data-ttu-id="e6b43-147">Todos los datos de hello almacenado asociados con el servidor de Hola se elimina inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="e6b43-147">All of hello stored data associated with hello server is deleted immediately.</span></span>

    ![Tareas de elementos registrados](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="e6b43-149">Elementos protegidos</span><span class="sxs-lookup"><span data-stu-id="e6b43-149">Protected items</span></span>
<span data-ttu-id="e6b43-150">Seleccione **elementos protegidos** elementos de hello tooview que hayan copias de seguridad de los servidores de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b43-150">Select **Protected Items** tooview hello items that have been backed up from hello servers.</span></span>

![Elementos protegidos](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="e6b43-152">Configuración</span><span class="sxs-lookup"><span data-stu-id="e6b43-152">Configure</span></span>
<span data-ttu-id="e6b43-153">De hello **configurar** ficha puede seleccionar la opción de redundancia de almacenamiento adecuada de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6b43-153">From hello **Configure** tab you can select hello appropriate storage redundancy option.</span></span> <span data-ttu-id="e6b43-154">Hola mejor tiempo tooselect Hola almacenamiento redundancia opción es justo después de crear un almacén y antes de que todas las máquinas estén tooit registrado.</span><span class="sxs-lookup"><span data-stu-id="e6b43-154">hello best time tooselect hello storage redundancy option is right after creating a vault and before any machines are registered tooit.</span></span>

> [!WARNING]
> <span data-ttu-id="e6b43-155">Una vez que un elemento se ha registrado toohello almacén, opción de redundancia de almacenamiento de hello está bloqueado y no se puede modificar.</span><span class="sxs-lookup"><span data-stu-id="e6b43-155">Once an item has been registered toohello vault, hello storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Configuración](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="e6b43-157">Consulte este artículo para más información sobre la [redundancia de almacenamiento](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="e6b43-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="e6b43-158">Tareas del agente de Copia de seguridad de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e6b43-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="e6b43-159">Consola</span><span class="sxs-lookup"><span data-stu-id="e6b43-159">Console</span></span>
<span data-ttu-id="e6b43-160">Abra hello **agente de copia de seguridad de Microsoft Azure** (puede encontrarlo buscando en el equipo para *copia de seguridad de Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="e6b43-160">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Agente de copia de seguridad](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="e6b43-162">De hello **acciones** disponible en hello derecha de la consola de agente de copia de seguridad de hello puede realizar Hola después de las tareas de administración:</span><span class="sxs-lookup"><span data-stu-id="e6b43-162">From hello **Actions** available at hello right of hello backup agent console you can perform hello following management tasks:</span></span>

* <span data-ttu-id="e6b43-163">Registrar un servidor</span><span class="sxs-lookup"><span data-stu-id="e6b43-163">Register Server</span></span>
* <span data-ttu-id="e6b43-164">Programación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="e6b43-164">Schedule Backup</span></span>
* <span data-ttu-id="e6b43-165">Realizar una copia de seguridad en ese momento</span><span class="sxs-lookup"><span data-stu-id="e6b43-165">Back Up now</span></span>
* <span data-ttu-id="e6b43-166">Cambiar propiedades</span><span class="sxs-lookup"><span data-stu-id="e6b43-166">Change Properties</span></span>

![Acciones de la consola de agente](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="e6b43-168">demasiado**recuperar datos**, consulte [restaurar archivos tooa Windows server o el equipo cliente de Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="e6b43-168">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="e6b43-169">Modificación de una copia de seguridad existente</span><span class="sxs-lookup"><span data-stu-id="e6b43-169">Modify an existing backup</span></span>
1. <span data-ttu-id="e6b43-170">En el agente de copia de seguridad de Microsoft Azure hello, haga clic en **programar copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-170">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="e6b43-172">Hola **Asistente para la programación de copia de seguridad** deje hello **realizar cambios horas o los elementos de toobackup** opción seleccionada y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-172">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Modificación de una copia de seguridad programada](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="e6b43-174">Si desea tooadd o cambiar elementos en hello **seleccionar elementos tooBackup** pantalla haga clic en **agregar elementos**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-174">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="e6b43-175">También puede establecer **configuración de exclusión** desde esta página del Asistente para saludo.</span><span class="sxs-lookup"><span data-stu-id="e6b43-175">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="e6b43-176">Si desea que los archivos tooexclude o tipos de archivo leen el procedimiento de Hola para agregar [configuración de exclusión](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="e6b43-176">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="e6b43-177">Seleccione Hola archivos y carpetas que desee tooback seguridad y haga clic en **bien**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-177">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Agregar elementos](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="e6b43-179">Especificar hello **programar copia de seguridad** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-179">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="e6b43-180">Puede programar copias de seguridad diarias (un máximo de 3 veces al día) o semanales.</span><span class="sxs-lookup"><span data-stu-id="e6b43-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Especificación de la programación de copias de seguridad](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="e6b43-182">Especificar la programación de copia de seguridad de Hola se explica con detalle en esta [artículo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="e6b43-182">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="e6b43-183">Seleccione hello **directiva de retención** para copia de seguridad de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-183">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Selección de la directiva de retención](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="e6b43-185">En hello **confirmación** Hola revisar la información de la pantalla y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-185">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="e6b43-186">Una vez que el Asistente de hello finaliza la creación de hello **programar copia de seguridad**, haga clic en **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-186">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="e6b43-187">Después de modificar la protección, puede confirmar que las copias de seguridad se activan correctamente por van toohello **trabajos** ficha y confirmar que los cambios se reflejan en hello trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e6b43-187">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="e6b43-188">Habilitación de la limitación de la red</span><span class="sxs-lookup"><span data-stu-id="e6b43-188">Enable Network Throttling</span></span>
<span data-ttu-id="e6b43-189">agente de copia de seguridad de Azure Hola incluye una pestaña de limitación que permite toocontrol uso de ancho de banda de red durante la transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="e6b43-189">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="e6b43-190">Este control puede ser útil si necesita tooback los datos durante las horas laborables, pero no desea hello toointerfere de proceso de copia de seguridad con otro tráfico de internet.</span><span class="sxs-lookup"><span data-stu-id="e6b43-190">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="e6b43-191">Limitación de datos transferencia aplica tooback seguridad y restaurar las actividades.</span><span class="sxs-lookup"><span data-stu-id="e6b43-191">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="e6b43-192">tooenable limitación:</span><span class="sxs-lookup"><span data-stu-id="e6b43-192">tooenable throttling:</span></span>

1. <span data-ttu-id="e6b43-193">Hola **agente de copia de seguridad**, haga clic en **cambiar las propiedades de**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-193">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="e6b43-194">Seleccione hello **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="e6b43-194">Select hello **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Limitación de la red](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="e6b43-196">Una vez habilitada la limitación, especifique Hola permitido ancho de banda para transfirieron datos de copia de seguridad durante la **horas laborables** y **horas de descanso**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-196">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="e6b43-197">los valores de ancho de banda de Hello comienzan en 512 kilobytes por segundo (Kbps) y pueden crecer hasta too1023 megabytes por segundo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="e6b43-197">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="e6b43-198">También puede designar el inicio de Hola y de fin para **horas laborables**, y los días de la semana de Hola se consideran trabajo días.</span><span class="sxs-lookup"><span data-stu-id="e6b43-198">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="e6b43-199">tiempo de Hello fuera Hola designado horas laborables es considerada toobe horas de descanso.</span><span class="sxs-lookup"><span data-stu-id="e6b43-199">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
4. <span data-ttu-id="e6b43-200">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="e6b43-201">Configuración de exclusión</span><span class="sxs-lookup"><span data-stu-id="e6b43-201">Exclusion settings</span></span>
1. <span data-ttu-id="e6b43-202">Abra hello **agente de copia de seguridad de Microsoft Azure** (puede encontrarlo buscando en el equipo para *copia de seguridad de Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="e6b43-202">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Apertura del agente de copia de seguridad](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="e6b43-204">En el agente de copia de seguridad de Microsoft Azure hello, haga clic en **programar copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-204">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Programar una copia de seguridad de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="e6b43-206">Hola Asistente para la programación de copia de seguridad deje hello **realizar cambios horas o los elementos de toobackup** opción seleccionada y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-206">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Modificación de una programación](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="e6b43-208">Haga clic en **Configuración de exclusión**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-208">Click **Exclusions Settings**.</span></span>

    ![Selección de elementos tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="e6b43-210">Haga clic en **Agregar exclusión**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-210">Click **Add Exclusion**.</span></span>

    ![Adición de exclusiones](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="e6b43-212">Seleccionar ubicación de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-212">Select hello location and then, click **OK**.</span></span>

    ![Selección de una ubicación para la exclusión](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="e6b43-214">Agregar extensión de archivo de Hola Hola **tipo de archivo** campo.</span><span class="sxs-lookup"><span data-stu-id="e6b43-214">Add hello file extension in hello **File Type** field.</span></span>

    ![Exclusión por tipo de archivo](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="e6b43-216">Adición de una extensión .mp3</span><span class="sxs-lookup"><span data-stu-id="e6b43-216">Adding an .mp3 extension</span></span>

    ![Ejemplo de tipo de archivo](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="e6b43-218">tooadd otra extensión, haga clic en **Agregar exclusión** y escriba otra extensión de tipo de archivo (agregar una extensión de JPEG).</span><span class="sxs-lookup"><span data-stu-id="e6b43-218">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Otro ejemplo de tipo de archivo](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="e6b43-220">Cuando haya agregado todas las extensiones de hello, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-220">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="e6b43-221">Continuar a través de hello Asistente para la programación de copia de seguridad haciendo clic en **siguiente** hasta hello **página de confirmación**, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="e6b43-221">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Confirmación de exclusión](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="e6b43-223">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6b43-223">Next steps</span></span>
* [<span data-ttu-id="e6b43-224">Restauración de Windows Server o el cliente de Windows desde Azure</span><span class="sxs-lookup"><span data-stu-id="e6b43-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="e6b43-225">toolearn más información acerca de la copia de seguridad de Azure, consulte [información general sobre la copia de seguridad de Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="e6b43-225">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="e6b43-226">Visite hello [foro de copia de seguridad de Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="e6b43-226">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
