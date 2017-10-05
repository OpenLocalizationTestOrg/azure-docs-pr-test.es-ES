---
title: Directivas de copia de seguridad de StorSimple Snapshot Manager | Microsoft Docs
description: "Describe cómo usar el complemento MMC de Administrador de instantáneas StorSimple para crear y administrar las directivas de copia de seguridad que controlan las copias de seguridad programadas."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 218c89e403673c16c72da95aa2c1d685bbed5a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-backup-policies"></a><span data-ttu-id="99c5f-103">Use Administrador de instantáneas StorSimple para crear y administrar directivas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99c5f-103">Use StorSimple Snapshot Manager to create and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="99c5f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="99c5f-104">Overview</span></span>
<span data-ttu-id="99c5f-105">Una directiva de copia de seguridad crea una programación para realizar una copia de seguridad de los datos del volumen localmente o en la nube.</span><span class="sxs-lookup"><span data-stu-id="99c5f-105">A backup policy creates a schedule for backing up volume data locally or in the cloud.</span></span> <span data-ttu-id="99c5f-106">Cuando crea una directiva de copia de seguridad, también puede especificar una directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="99c5f-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="99c5f-107">(Puede retener un máximo de 64 instantáneas). Para obtener más información sobre las directivas de copia de seguridad, consulte [Tipos de copia de seguridad](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) en [Serie StorSimple 8000: una solución de almacenamiento en la nube híbrida](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99c5f-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="99c5f-108">Este tutorial explica cómo realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="99c5f-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="99c5f-109">Creación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99c5f-109">Create a backup policy</span></span>
* <span data-ttu-id="99c5f-110">Edición de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99c5f-110">Edit a backup policy</span></span>
* <span data-ttu-id="99c5f-111">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99c5f-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="99c5f-112">Creación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99c5f-112">Create a backup policy</span></span>
<span data-ttu-id="99c5f-113">Use el procedimiento siguiente para crear una nueva directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="99c5f-113">Use the following procedure to create a new backup policy.</span></span>

#### <a name="to-create-a-backup-policy"></a><span data-ttu-id="99c5f-114">Para crear una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99c5f-114">To create a backup policy</span></span>
1. <span data-ttu-id="99c5f-115">Haga clic en el icono del escritorio para iniciar Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="99c5f-115">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="99c5f-116">En el panel **Ámbito**, haga clic con el botón derecho en **Directivas de copia de seguridad** y haga clic en **Crear directiva de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="99c5f-116">In the **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Creación de una directiva de copia de seguridad](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="99c5f-118">Aparecerá el cuadro de diálogo **Crear una directiva** .</span><span class="sxs-lookup"><span data-stu-id="99c5f-118">The **Create a Policy** dialog box appears.</span></span>

    ![Creación de una directiva - pestaña General](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="99c5f-120">En la pestaña **General** , complete la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="99c5f-120">On the **General** tab, complete the following information:</span></span>

   1. <span data-ttu-id="99c5f-121">En el cuadro de texto **Nombre** , escriba un nombre para la directiva.</span><span class="sxs-lookup"><span data-stu-id="99c5f-121">In the **Name** text box, type a name for the policy.</span></span>
   2. <span data-ttu-id="99c5f-122">En el cuadro de texto **Grupo de volúmenes** , escriba el nombre del grupo de volúmenes asociado con la directiva.</span><span class="sxs-lookup"><span data-stu-id="99c5f-122">In the **Volume group** text box, type the name of the volume group associated with the policy.</span></span>
   3. <span data-ttu-id="99c5f-123">Seleccione **Instantánea local** o **Instantánea de nube**.</span><span class="sxs-lookup"><span data-stu-id="99c5f-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="99c5f-124">Seleccione el número de instantáneas que desea retener.</span><span class="sxs-lookup"><span data-stu-id="99c5f-124">Select the number of snapshots to retain.</span></span> <span data-ttu-id="99c5f-125">Si selecciona **Todas**, se retendrán 64 instantáneas (el número máximo).</span><span class="sxs-lookup"><span data-stu-id="99c5f-125">If you select **All**, 64 snapshots will be retained (the maximum).</span></span>
4. <span data-ttu-id="99c5f-126">Haga clic en la pestaña **Programar** .</span><span class="sxs-lookup"><span data-stu-id="99c5f-126">Click the **Schedule** tab.</span></span>

    ![Creación de una directiva - pestaña Programación](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="99c5f-128">En la pestaña **Programación** , complete la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="99c5f-128">On the **Schedule** tab, complete the following information:</span></span>

   1. <span data-ttu-id="99c5f-129">Haga clic en la casilla **Habilitar** para programar la siguiente copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="99c5f-129">Click the **Enable** check box to schedule the next backup.</span></span>
   2. <span data-ttu-id="99c5f-130">En **Configuración**, seleccione **Una vez**, **Diario**, **Semanal** o **Mensual**.</span><span class="sxs-lookup"><span data-stu-id="99c5f-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="99c5f-131">En el cuadro de texto **Inicio** , haga clic en el icono de calendario y seleccione una fecha de inicio.</span><span class="sxs-lookup"><span data-stu-id="99c5f-131">In the **Start** text box, click the calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="99c5f-132">En **Configuración avanzada**, puede establecer programaciones de repetición opcionales y una fecha de finalización.</span><span class="sxs-lookup"><span data-stu-id="99c5f-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="99c5f-133">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="99c5f-133">Click **OK**.</span></span>

<span data-ttu-id="99c5f-134">Después de crear una directiva de copia de seguridad, aparece la siguiente información en el panel **Resultados** :</span><span class="sxs-lookup"><span data-stu-id="99c5f-134">After you create a backup policy, the following information appears in the **Results** pane:</span></span>

* <span data-ttu-id="99c5f-135">**Nombre** : nombre de la directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="99c5f-135">**Name** – the name of backup policy.</span></span>
* <span data-ttu-id="99c5f-136">**Tipo** : instantánea local o instantánea de nube.</span><span class="sxs-lookup"><span data-stu-id="99c5f-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="99c5f-137">**Grupo de volúmenes** : grupo de volúmenes asociado a la directiva.</span><span class="sxs-lookup"><span data-stu-id="99c5f-137">**Volume Group** – the volume group associated with the policy.</span></span>
* <span data-ttu-id="99c5f-138">**Retención** : número de instantáneas retenidas; el número máximo es 64.</span><span class="sxs-lookup"><span data-stu-id="99c5f-138">**Retention** – the number of snapshots retained; the maximum is 64.</span></span>
* <span data-ttu-id="99c5f-139">**Creado** : fecha en que se creó esta directiva.</span><span class="sxs-lookup"><span data-stu-id="99c5f-139">**Created** – the date that this policy was created.</span></span>
* <span data-ttu-id="99c5f-140">**Habilitado**: si la directiva está actualmente en vigor. **True** indica que está en vigor; **False** indica que no está en vigor.</span><span class="sxs-lookup"><span data-stu-id="99c5f-140">**Enabled** – whether the policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="99c5f-141">Edición de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99c5f-141">Edit a backup policy</span></span>
<span data-ttu-id="99c5f-142">Use el procedimiento siguiente para editar una directiva de copia de seguridad existente.</span><span class="sxs-lookup"><span data-stu-id="99c5f-142">Use the following procedure to edit an existing backup policy.</span></span>

#### <a name="to-edit-a-backup-policy"></a><span data-ttu-id="99c5f-143">Para editar una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99c5f-143">To edit a backup policy</span></span>
1. <span data-ttu-id="99c5f-144">Haga clic en el icono del escritorio para iniciar Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="99c5f-144">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="99c5f-145">En el panel **Ámbito**, haga clic en el nodo **Directivas de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="99c5f-145">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="99c5f-146">Todas las directivas de copia de seguridad aparecen en el panel **Resultados** .</span><span class="sxs-lookup"><span data-stu-id="99c5f-146">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="99c5f-147">Haga clic con el botón derecho en la directiva que desee editar y después haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="99c5f-147">Right-click the policy that you want to edit, and then click **Edit**.</span></span>

    ![Edición de una directiva de copia de seguridad](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="99c5f-149">Cuando aparezca la ventana **Crear una directiva**, escriba los cambios y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="99c5f-149">When the **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="99c5f-150">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99c5f-150">Delete a backup policy</span></span>
<span data-ttu-id="99c5f-151">Use el procedimiento siguiente para eliminar una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="99c5f-151">Use the following procedure to delete a backup policy.</span></span>

#### <a name="to-delete-a-backup-policy"></a><span data-ttu-id="99c5f-152">Para eliminar una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99c5f-152">To delete a backup policy</span></span>
1. <span data-ttu-id="99c5f-153">Haga clic en el icono del escritorio para iniciar Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="99c5f-153">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="99c5f-154">En el panel **Ámbito**, haga clic en el nodo **Directivas de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="99c5f-154">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="99c5f-155">Todas las directivas de copia de seguridad aparecen en el panel **Resultados** .</span><span class="sxs-lookup"><span data-stu-id="99c5f-155">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="99c5f-156">Haga clic con el botón derecho en la directiva de copia de seguridad que desee eliminar y después haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="99c5f-156">Right-click the backup policy that you want to delete, and then click **Delete**.</span></span>
4. <span data-ttu-id="99c5f-157">Cuando aparezca el mensaje de confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="99c5f-157">When the confirmation message appears, click **Yes**.</span></span>

    ![Eliminación de la confirmación de una directiva de copia de seguridad](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="99c5f-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99c5f-159">Next steps</span></span>
* <span data-ttu-id="99c5f-160">Obtenga más información sobre el [uso de Snapshot Manager de StorSimple para administrar la solución de StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="99c5f-160">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="99c5f-161">Obtenga más información acerca de [uso de Snapshot Manager de StorSimple para ver y administrar trabajos de copia de seguridad](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="99c5f-161">Learn how to [use StorSimple Snapshot Manager to view and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
