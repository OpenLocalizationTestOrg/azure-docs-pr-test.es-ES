---
title: "las copias de seguridad implementado por el Administrador de recursos de máquina virtual de aaaManage | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las copias de seguridad implementado por el Administrador de recursos de máquina virtual toomanage y monitor"
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
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="46acc-103">Administración de copias de seguridad de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="46acc-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46acc-104">Administrar copias de seguridad de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="46acc-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="46acc-105">Administrar copias de seguridad de máquina virtual clásica</span><span class="sxs-lookup"><span data-stu-id="46acc-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="46acc-106">Este artículo proporciona instrucciones sobre cómo administrar las copias de seguridad de la máquina virtual y explica Hola información de alertas de copia de seguridad disponible en el panel del portal Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-106">This article provides guidance on managing VM backups, and explains hello backup alerts information available in hello portal dashboard.</span></span> <span data-ttu-id="46acc-107">Guía de Hello en este artículo aplica a las máquinas virtuales de toousing con almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="46acc-107">hello guidance in this article applies toousing VMs with Recovery Services vaults.</span></span> <span data-ttu-id="46acc-108">En este artículo no cubre la creación de hello de máquinas virtuales, ni explica cómo tooprotect las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="46acc-108">This article does not cover hello creation of virtual machines, nor does it explain how tooprotect virtual machines.</span></span> <span data-ttu-id="46acc-109">Para instrucciones detalladas sobre la protección de máquinas virtuales implementadas por el Administrador de recursos de Azure en Azure con un almacén de servicios de recuperación, consulte [primer vistazo: copia de seguridad del almacén de servicios de recuperación de tooa de máquinas virtuales](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="46acc-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="46acc-110">Administración de almacenes y máquinas virtuales protegidas</span><span class="sxs-lookup"><span data-stu-id="46acc-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="46acc-111">Hola portal de Azure, panel de almacén de servicios de recuperación de hello proporciona acceso tooinformation acerca de la inclusión de almacén de hello:</span><span class="sxs-lookup"><span data-stu-id="46acc-111">In hello Azure portal, hello Recovery Services vault dashboard provides access tooinformation about hello vault including:</span></span>

* <span data-ttu-id="46acc-112">Hola última copia de seguridad de instantánea, que también es el punto de restauración más reciente de Hola < br\></span><span class="sxs-lookup"><span data-stu-id="46acc-112">hello most recent backup snapshot, which is also hello latest restore point <br\></span></span>
* <span data-ttu-id="46acc-113">Directiva de copia de seguridad de Hola < br\></span><span class="sxs-lookup"><span data-stu-id="46acc-113">hello backup policy <br\></span></span>
* <span data-ttu-id="46acc-114">el tamaño total de todas las instantáneas de copia de seguridad <br\></span><span class="sxs-lookup"><span data-stu-id="46acc-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="46acc-115">número de máquinas virtuales que están protegidas con el almacén de Hola < br\></span><span class="sxs-lookup"><span data-stu-id="46acc-115">number of virtual machines that are protected with hello vault <br\></span></span>

<span data-ttu-id="46acc-116">Muchas tareas de administración con una copia de seguridad de la máquina virtual comienzan por abrir almacén de hello en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-116">Many management tasks with a virtual machine backup begin with opening hello vault in hello dashboard.</span></span> <span data-ttu-id="46acc-117">Sin embargo, dado que los almacenes pueden ser tooprotect usa varios elementos (o varias máquinas virtuales), tooview detalles sobre una máquina virtual concreta, abra Panel de elemento de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-117">However, because vaults can be used tooprotect multiple items (or multiple VMs), tooview details about a particular VM, open hello vault item dashboard.</span></span> <span data-ttu-id="46acc-118">Hello siguiente procedimiento muestra cómo hello tooopen *panel almacén* y, a continuación, continuar toohello *panel almacén de elemento*.</span><span class="sxs-lookup"><span data-stu-id="46acc-118">hello following procedure shows you how tooopen hello *vault dashboard* and then continue toohello *vault item dashboard*.</span></span> <span data-ttu-id="46acc-119">Hay "sugerencias" en ambos procedimientos que destacan cómo tooadd Hola almacén y almacén elemento toohello panel de Azure mediante Hola Pin toodashboard comando.</span><span class="sxs-lookup"><span data-stu-id="46acc-119">There are "tips" in both procedures that point out how tooadd hello vault and vault item toohello Azure dashboard by using hello Pin toodashboard command.</span></span> <span data-ttu-id="46acc-120">Toodashboard de PIN es una manera de crear un almacén de toohello de método abreviado o un elemento.</span><span class="sxs-lookup"><span data-stu-id="46acc-120">Pin toodashboard is a way of creating a shortcut toohello vault or item.</span></span> <span data-ttu-id="46acc-121">También puede ejecutar comandos comunes de acceso directo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-121">You can also execute common commands from hello shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="46acc-122">Si tiene varios paneles y abrir las hojas, use el control deslizante de azul oscuro de hello en parte inferior de Hola de Hola Hola de tooslide ventana Panel de Azure y hacia atrás.</span><span class="sxs-lookup"><span data-stu-id="46acc-122">If you have multiple dashboards and blades open, use hello dark-blue slider at hello bottom of hello window tooslide hello Azure dashboard back and forth.</span></span>
>
>

![Vista completa con control deslizante](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a><span data-ttu-id="46acc-124">Abra un almacén de servicios de recuperación en el panel de hello:</span><span class="sxs-lookup"><span data-stu-id="46acc-124">Open a Recovery Services vault in hello dashboard:</span></span>
1. <span data-ttu-id="46acc-125">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="46acc-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="46acc-126">En el menú del concentrador hello, haga clic en **examinar** y en la lista de Hola de recursos, escriba **servicios de recuperación**.</span><span class="sxs-lookup"><span data-stu-id="46acc-126">On hello Hub menu, click **Browse** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="46acc-127">Cuando empiece a escribir, Hola filtros de la lista con los datos especificados.</span><span class="sxs-lookup"><span data-stu-id="46acc-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="46acc-128">Haga clic en **Almacén de Servicios de recuperación**.</span><span class="sxs-lookup"><span data-stu-id="46acc-128">Click **Recovery Services vault**.</span></span>

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="46acc-130">se muestra la lista de Hola de almacenes de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="46acc-130">hello list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="46acc-131">Lista de almacenes de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="46acc-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="46acc-132">Si ancla un panel de Azure de almacén toohello, ese almacén está accesible inmediatamente cuando se abre Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="46acc-132">If you pin a vault toohello Azure Dashboard, that vault is immediately accessible when you open hello Azure portal.</span></span> <span data-ttu-id="46acc-133">toopin un panel de toohello de almacén, en la lista de almacén de hello, haga clic en el almacén de Hola y seleccione **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="46acc-133">toopin a vault toohello dashboard, in hello vault list, right-click hello vault, and select **Pin toodashboard**.</span></span>
   >
   >
3. <span data-ttu-id="46acc-134">En lista de Hola de almacenes de credenciales, seleccione Hola almacén tooopen su panel.</span><span class="sxs-lookup"><span data-stu-id="46acc-134">From hello list of vaults, select hello vault tooopen its dashboard.</span></span> <span data-ttu-id="46acc-135">Al seleccionar el almacén de hello, panel de almacén de Hola y Hola **configuración** hoja abierta.</span><span class="sxs-lookup"><span data-stu-id="46acc-135">When you select hello vault, hello vault dashboard and hello **Settings** blade open.</span></span> <span data-ttu-id="46acc-136">Hola después de la imagen, Hola **Contoso almacén** se resalta el panel.</span><span class="sxs-lookup"><span data-stu-id="46acc-136">In hello following image, hello **Contoso-vault** dashboard is highlighted.</span></span>

    ![Abrir el panel del almacén y la hoja Configuración](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="46acc-138">Apertura del panel de un elemento del almacén</span><span class="sxs-lookup"><span data-stu-id="46acc-138">Open a vault item dashboard</span></span>
<span data-ttu-id="46acc-139">En el procedimiento anterior de hello abrir Panel de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-139">In hello previous procedure you opened hello vault dashboard.</span></span> <span data-ttu-id="46acc-140">panel de elemento de almacén de Hola tooopen:</span><span class="sxs-lookup"><span data-stu-id="46acc-140">tooopen hello vault item dashboard:</span></span>

1. <span data-ttu-id="46acc-141">En panel de almacén de hello en hello **elementos de copia de seguridad** icono, haga clic en **máquinas virtuales de Azure**.</span><span class="sxs-lookup"><span data-stu-id="46acc-141">In hello vault dashboard, on hello **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Abrir el icono Elementos de copia de seguridad](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="46acc-143">Hola **elementos de copia de seguridad** hoja muestra el último trabajo de copia de seguridad Hola para cada elemento.</span><span class="sxs-lookup"><span data-stu-id="46acc-143">hello **Backup Items** blade lists hello last backup job for each item.</span></span> <span data-ttu-id="46acc-144">En este ejemplo, hay una máquina virtual, demovm-markgal, protegida por este almacén.</span><span class="sxs-lookup"><span data-stu-id="46acc-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Icono Elementos de copia de seguridad](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="46acc-146">Para facilitar el acceso, puede anclar un toohello de elemento de almacén panel de Azure.</span><span class="sxs-lookup"><span data-stu-id="46acc-146">For ease of access, you can pin a vault item toohello Azure Dashboard.</span></span> <span data-ttu-id="46acc-147">un elemento de almacén, en la lista de elementos del almacén de hello, elemento de menú contextual hello y seleccione toopin **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="46acc-147">toopin a vault item, in hello vault item list, right-click hello item and select **Pin toodashboard**.</span></span>
   >
   >
2. <span data-ttu-id="46acc-148">Hola **elementos de copia de seguridad** hoja, haga clic en panel de elemento de almacén de hello elemento tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-148">In hello **Backup Items** blade, click hello item tooopen hello vault item dashboard.</span></span>

    ![Icono Elementos de copia de seguridad](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="46acc-150">panel de elemento de almacén de Hola y su **configuración** hoja abierta.</span><span class="sxs-lookup"><span data-stu-id="46acc-150">hello vault item dashboard and its **Settings** blade open.</span></span>

    ![Panel Elementos de copia de seguridad con hoja Configuración](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="46acc-152">En el panel de elemento de almacén de hello, puede realizar muchas tareas de administración de claves, como:</span><span class="sxs-lookup"><span data-stu-id="46acc-152">From hello vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="46acc-153">cambiar de directiva o crear una directiva de copia de seguridad<br\></span><span class="sxs-lookup"><span data-stu-id="46acc-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="46acc-154">ver los puntos de restauración y su estado de coherencia <br\></span><span class="sxs-lookup"><span data-stu-id="46acc-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="46acc-155">copia de seguridad a petición de una máquina virtual <br\></span><span class="sxs-lookup"><span data-stu-id="46acc-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="46acc-156">detener la protección de máquinas virtuales <br\></span><span class="sxs-lookup"><span data-stu-id="46acc-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="46acc-157">reanudar la protección de una máquina virtual <br\></span><span class="sxs-lookup"><span data-stu-id="46acc-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="46acc-158">eliminar los datos de una copia de seguridad (o un punto de recuperación) <br\></span><span class="sxs-lookup"><span data-stu-id="46acc-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="46acc-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  &lt;br\></span><span class="sxs-lookup"><span data-stu-id="46acc-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="46acc-160">Para Hola procedimientos Hola punto de partida es panel de elemento de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-160">For hello following procedures, hello starting point is hello vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="46acc-161">Administrar directivas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="46acc-161">Manage backup policies</span></span>
1. <span data-ttu-id="46acc-162">En hello [panel almacén de elemento](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **toda la configuración de** tooopen hello **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="46acc-162">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** tooopen hello **Settings** blade.</span></span>

    ![Hoja Directiva de copia de seguridad](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="46acc-164">En hello **configuración** hoja, haga clic en **directiva de copia de seguridad** tooopen esa hoja.</span><span class="sxs-lookup"><span data-stu-id="46acc-164">On hello **Settings** blade, click **Backup policy** tooopen that blade.</span></span>

    <span data-ttu-id="46acc-165">Hola copia de seguridad frecuencia y retención intervalo detalles aparecen en la hoja de hello.</span><span class="sxs-lookup"><span data-stu-id="46acc-165">On hello blade, hello backup frequency and retention range details are shown.</span></span>

    ![Hoja Directiva de copia de seguridad](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="46acc-167">De hello **elegir la directiva de copia de seguridad** menú:</span><span class="sxs-lookup"><span data-stu-id="46acc-167">From hello **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="46acc-168">toochange directivas, seleccione una directiva diferente y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="46acc-168">toochange policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="46acc-169">nueva directiva de Hello es el almacén de toohello aplica inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="46acc-169">hello new policy is immediately applied toohello vault.</span></span> <span data-ttu-id="46acc-170"><br\></span><span class="sxs-lookup"><span data-stu-id="46acc-170"><br\></span></span>
   * <span data-ttu-id="46acc-171">toocreate una directiva, seleccione **crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="46acc-171">toocreate a policy, select **Create New**.</span></span>

     ![Copia de seguridad de máquina virtual](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="46acc-173">Si quiere instrucciones para crear una directiva de copia de seguridad, consulte [Definición de una directiva de copia de seguridad](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="46acc-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="46acc-174">Al administrar directivas de copia de seguridad, asegúrese de que hello toofollow [prácticas recomendadas](backup-azure-vms-introduction.md#best-practices) obtener el máximo rendimiento de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="46acc-174">While managing backup policies, make sure toofollow hello [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="46acc-175">Copia de seguridad a petición de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="46acc-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="46acc-176">Puede realizar una copia de seguridad a petición de una máquina virtual una vez que esta esté configurada para la protección.</span><span class="sxs-lookup"><span data-stu-id="46acc-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="46acc-177">Si está pendiente la copia de seguridad inicial de hello, copia de seguridad a petición crea una copia completa de la máquina virtual de Hola Hola que del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="46acc-177">If hello initial backup is pending, on-demand backup creates a full copy of hello virtual machine in hello Recovery Services vault.</span></span> <span data-ttu-id="46acc-178">Si se realiza una copia de seguridad inicial de hello, una copia de seguridad a petición sólo enviará cambios desde la instantánea anterior de hello, toohello el almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="46acc-178">If hello initial backup is completed, an on-demand backup will only send changes from hello previous snapshot, toohello Recovery Services vault.</span></span> <span data-ttu-id="46acc-179">Es decir, las copias de seguridad posteriores siempre son incrementales.</span><span class="sxs-lookup"><span data-stu-id="46acc-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="46acc-180">duración de retención de Hola para una copia de seguridad a petición es el valor de retención de hello especificado para el punto de copia de seguridad diaria de hello en la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-180">hello retention range for an on-demand backup is hello retention value specified for hello Daily backup point in hello policy.</span></span> <span data-ttu-id="46acc-181">Si no se selecciona ningún punto de copia de seguridad diaria, se utiliza el punto de copia de seguridad semanal Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-181">If no Daily backup point is selected, then hello weekly backup point is used.</span></span>
>
>

<span data-ttu-id="46acc-182">copia de seguridad de tootrigger una petición de una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="46acc-182">tootrigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="46acc-183">En hello [panel almacén de elemento](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **una copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="46acc-183">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Botón Realizar copia de seguridad ahora](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="46acc-185">portal de Hola se asegura de que desea toostart un trabajo de copia de seguridad a petición.</span><span class="sxs-lookup"><span data-stu-id="46acc-185">hello portal makes sure that you want toostart an on-demand backup job.</span></span> <span data-ttu-id="46acc-186">Haga clic en **Sí** trabajo de copia de seguridad de toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-186">Click **Yes** toostart hello backup job.</span></span>

    ![Botón Realizar copia de seguridad ahora](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="46acc-188">trabajo de copia de seguridad de Hello crea un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="46acc-188">hello backup job creates a recovery point.</span></span> <span data-ttu-id="46acc-189">duración de retención de Hola Hola del punto de recuperación es Hola igual a la duración de retención especificada en la directiva de hello asociado a la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-189">hello retention range of hello recovery point is hello same as retention range specified in hello policy associated with hello virtual machine.</span></span> <span data-ttu-id="46acc-190">progreso de hello tootrack de trabajo de hello, en panel de almacén de hello, haga clic en hello **trabajos de copia de seguridad** icono.</span><span class="sxs-lookup"><span data-stu-id="46acc-190">tootrack hello progress for hello job, in hello vault dashboard, click hello **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="46acc-191">Detener la protección de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="46acc-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="46acc-192">Si elige toostop proteger una máquina virtual, se le preguntará si desea que los puntos de recuperación de tooretain Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-192">If you choose toostop protecting a virtual machine, you are asked if you want tooretain hello recovery points.</span></span> <span data-ttu-id="46acc-193">Hay dos maneras en las máquinas virtuales de la protección toostop:</span><span class="sxs-lookup"><span data-stu-id="46acc-193">There are two ways toostop protecting virtual machines:</span></span>

* <span data-ttu-id="46acc-194">detener todos los trabajos futuros de copia de seguridad y eliminar todos los puntos de recuperación, o</span><span class="sxs-lookup"><span data-stu-id="46acc-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="46acc-195">detener todos los futuros trabajos de copia de seguridad, pero dejar Hola puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="46acc-195">stop all future backup jobs but leave hello recovery points</span></span> <br/>

<span data-ttu-id="46acc-196">Hay un costo asociado dejando Hola puntos de recuperación en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="46acc-196">There is a cost associated with leaving hello recovery points in storage.</span></span> <span data-ttu-id="46acc-197">Sin embargo, ventaja de Hola de dejar Hola puntos de recuperación es que puede restaurar la máquina virtual de hello más adelante, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="46acc-197">However, hello benefit of leaving hello recovery points is you can restore hello virtual machine later, if desired.</span></span> <span data-ttu-id="46acc-198">Para obtener información sobre el costo de Hola de dejar Hola puntos de recuperación, vea hello [detalles de precios](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="46acc-198">For information about hello cost of leaving hello recovery points, see hello  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="46acc-199">Si elige toodelete todos los puntos de recuperación, no puede restaurar la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-199">If you choose toodelete all recovery points, you cannot restore hello virtual machine.</span></span>

<span data-ttu-id="46acc-200">protección de toostop para una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="46acc-200">toostop protection for a virtual machine:</span></span>

1. <span data-ttu-id="46acc-201">En hello [panel almacén de elemento](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **Detener copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="46acc-201">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Botón Detener copia de seguridad](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="46acc-203">se abre la hoja de Hello Detener copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="46acc-203">hello Stop Backup blade opens.</span></span>

    ![Hoja Detener copia de seguridad](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="46acc-205">En hello **Detener copia de seguridad** hoja, elija si tooretain o delete Hola datos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="46acc-205">On hello **Stop Backup** blade, choose whether tooretain or delete hello backup data.</span></span> <span data-ttu-id="46acc-206">cuadro de información de Hello ofrece información detallada acerca de su elección.</span><span class="sxs-lookup"><span data-stu-id="46acc-206">hello information box provides details about your choice.</span></span>

    ![Detener protección](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="46acc-208">Si elige datos de copia de seguridad de hello tooretain, omitir toostep 4.</span><span class="sxs-lookup"><span data-stu-id="46acc-208">If you chose tooretain hello backup data, skip toostep 4.</span></span> <span data-ttu-id="46acc-209">Si elige datos de copia de seguridad de toodelete, confirme que desea trabajos de copia de seguridad de toostop hello y eliminar puntos de recuperación de hello - nombre de Hola de tipo de elemento de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-209">If you chose toodelete backup data, confirm that you want toostop hello backup jobs and delete hello recovery points - type hello name of hello item.</span></span>

    ![Comprobación de la detención](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="46acc-211">Si no está seguro del nombre del elemento de hello, mantenga el mouse sobre el nombre de hello marca de exclamación tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-211">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="46acc-212">Además, es nombre Hola de elemento de hello en **Detener copia de seguridad** en parte superior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-212">Also, hello name of hello item is under **Stop Backup** at hello top of hello blade.</span></span>
4. <span data-ttu-id="46acc-213">Opcionalmente, añada un valor a los campos **Motivo** o **Comentario**.</span><span class="sxs-lookup"><span data-stu-id="46acc-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="46acc-214">Haga clic en trabajo de copia de seguridad de hello toostop para el elemento actual de hello, ![botón de Detener copia de seguridad](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="46acc-214">toostop hello backup job for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="46acc-215">Un mensaje de notificación permite saber que se han detenido los trabajos de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-215">A notification message lets you know hello backup jobs have been stopped.</span></span>

    ![Confirmación de la detención de la protección](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="46acc-217">Reanudación de la protección de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="46acc-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="46acc-218">Si hello **conservar datos de copia de seguridad** opción se ha elegido cuando se detuvo la protección de máquina virtual de hello, es posible tooresume protección.</span><span class="sxs-lookup"><span data-stu-id="46acc-218">If hello **Retain Backup Data** option was chosen when protection for hello virtual machine was stopped, then it is possible tooresume protection.</span></span> <span data-ttu-id="46acc-219">Si hello **eliminar datos de copia de seguridad** se ha elegido la opción, a continuación, no se puede reanudar la protección de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-219">If hello **Delete Backup Data** option was chosen, then protection for hello virtual machine cannot resume.</span></span>

<span data-ttu-id="46acc-220">protección de tooresume para la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="46acc-220">tooresume protection for hello virtual machine</span></span>

1. <span data-ttu-id="46acc-221">En hello [panel almacén de elemento](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **Reanudar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="46acc-221">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Reanudar protección](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="46acc-223">se abre la hoja de la directiva de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-223">hello Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="46acc-224">Al volver a proteger máquinas virtuales de hello, puede elegir una directiva diferente a la directiva de hello con la que se protegió inicialmente máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="46acc-224">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="46acc-225">Siga los pasos de hello en [administrar directivas de copia de seguridad](backup-azure-manage-vms.md#manage-backup-policies) tooassign directiva de hello para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-225">Follow hello steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello policy for hello virtual machine.</span></span>

    <span data-ttu-id="46acc-226">Una vez que Directiva de copia de seguridad de hello es un equipo virtual toohello aplicada, vea Hola siguiente mensaje.</span><span class="sxs-lookup"><span data-stu-id="46acc-226">Once hello backup policy is applied toohello virtual machine, you see hello following message.</span></span>

    ![Máquina virtual protegida correctamente](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="46acc-228">Eliminación de datos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="46acc-228">Delete Backup data</span></span>
<span data-ttu-id="46acc-229">Puede eliminar los datos de copia de seguridad de hello asociados con una máquina virtual durante hello **Detener copia de seguridad** trabajo, o en cualquier momento después de hello ha completado el trabajo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="46acc-229">You can delete hello backup data associated with a virtual machine during hello **Stop backup** job, or anytime after hello backup job has completed.</span></span> <span data-ttu-id="46acc-230">Incluso puede ser beneficioso toowait días o semanas antes de eliminar los puntos de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-230">It may even be beneficial toowait days or weeks before deleting hello recovery points.</span></span> <span data-ttu-id="46acc-231">A diferencia de restaurar los puntos de recuperación, cuando se elimina una copia de seguridad, no puede elegir toodelete de puntos de recuperación concreto.</span><span class="sxs-lookup"><span data-stu-id="46acc-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points toodelete.</span></span> <span data-ttu-id="46acc-232">Si elige toodelete los datos de copia de seguridad, elimine todos los puntos de recuperación asociados con el elemento de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-232">If you choose toodelete your backup data, you delete all recovery points associated with hello item.</span></span>

<span data-ttu-id="46acc-233">Hello siguiente procedimiento se da por supuesto trabajo de copia de seguridad de hello para la máquina virtual de Hola se ha detenido o deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="46acc-233">hello following procedure assumes hello Backup job for hello virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="46acc-234">Una vez que se deshabilita el trabajo de copia de seguridad de hello, Hola **Reanudar copia de seguridad** y **copia de seguridad de Delete** opciones están disponibles en el panel de elemento de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-234">Once hello Backup job is disabled, hello **Resume backup** and **Delete backup** options are available in hello vault item dashboard.</span></span>

![Botones Reanudar y Eliminar](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="46acc-236">datos de copia de seguridad de toodelete en una máquina virtual con hello *deshabilitado de copia de seguridad*:</span><span class="sxs-lookup"><span data-stu-id="46acc-236">toodelete backup data on a virtual machine with hello *Backup disabled*:</span></span>

1. <span data-ttu-id="46acc-237">En hello [panel almacén de elemento](backup-azure-manage-vms.md#open-a-vault-item-dashboard), haga clic en **copia de seguridad de Delete**.</span><span class="sxs-lookup"><span data-stu-id="46acc-237">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="46acc-239">Hola **eliminar datos de copia de seguridad** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="46acc-239">hello **Delete Backup Data** blade opens.</span></span>

    ![Tipo de máquina virtual](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="46acc-241">Nombre del tipo hello de hello elemento tooconfirm desea puntos de recuperación de toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-241">Type hello name of hello item tooconfirm you want toodelete hello recovery points.</span></span>

    ![Comprobación de la detención](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="46acc-243">Si no está seguro del nombre del elemento de hello, mantenga el mouse sobre el nombre de hello marca de exclamación tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-243">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="46acc-244">Además, es nombre Hola de elemento de hello en **eliminar datos de copia de seguridad** en parte superior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="46acc-244">Also, hello name of hello item is under **Delete Backup Data** at hello top of hello blade.</span></span>
3. <span data-ttu-id="46acc-245">Opcionalmente, añada un valor a los campos **Motivo** o **Comentario**.</span><span class="sxs-lookup"><span data-stu-id="46acc-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="46acc-246">Haga clic en datos de copia de seguridad de hello toodelete para el elemento actual de hello, ![botón de Detener copia de seguridad](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="46acc-246">toodelete hello backup data for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="46acc-247">Un mensaje de notificación permite saber que se ha eliminado los datos de copia de seguridad de saludo.</span><span class="sxs-lookup"><span data-stu-id="46acc-247">A notification message lets you know hello backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46acc-248">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46acc-248">Next steps</span></span>
<span data-ttu-id="46acc-249">Para información sobre cómo volver a crear una máquina virtual a partir de un punto de recuperación, consulte [Restauración de máquinas virtuales en Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="46acc-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="46acc-250">Si necesita información sobre la protección de las máquinas virtuales, consulte [primer vistazo: copia de seguridad del almacén de servicios de recuperación de tooa de máquinas virtuales](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="46acc-250">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="46acc-251">Para más información sobre la supervisión de eventos, consulte [Supervisión de alertas de copias de seguridad de máquinas virtuales de Azure](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="46acc-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
