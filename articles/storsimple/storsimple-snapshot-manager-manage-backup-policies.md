---
title: "directivas de copia de seguridad de administrador de instantáneas aaaStorSimple | Documentos de Microsoft"
description: "Describe cómo toouse Hola instantáneas de StorSimple Manager MMC complemento toocreate y administrar directivas de copia de seguridad de Hola que controlan las copias de seguridad programadas."
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
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a><span data-ttu-id="a52b3-103">Use el Administrador de instantáneas StorSimple toocreate y administrar las directivas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="a52b3-103">Use StorSimple Snapshot Manager toocreate and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="a52b3-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a52b3-104">Overview</span></span>
<span data-ttu-id="a52b3-105">Una directiva de copia de seguridad crea una programación de copia de seguridad de datos del volumen localmente o en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a52b3-105">A backup policy creates a schedule for backing up volume data locally or in hello cloud.</span></span> <span data-ttu-id="a52b3-106">Cuando crea una directiva de copia de seguridad, también puede especificar una directiva de retención.</span><span class="sxs-lookup"><span data-stu-id="a52b3-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="a52b3-107">(Puede retener un máximo de 64 instantáneas). Para obtener más información sobre las directivas de copia de seguridad, consulte [Tipos de copia de seguridad](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) en [Serie StorSimple 8000: una solución de almacenamiento en la nube híbrida](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a52b3-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="a52b3-108">Este tutorial explica cómo realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a52b3-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="a52b3-109">Creación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="a52b3-109">Create a backup policy</span></span>
* <span data-ttu-id="a52b3-110">Edición de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="a52b3-110">Edit a backup policy</span></span>
* <span data-ttu-id="a52b3-111">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="a52b3-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="a52b3-112">Creación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="a52b3-112">Create a backup policy</span></span>
<span data-ttu-id="a52b3-113">Usar hello siguiendo el procedimiento toocreate una nueva directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="a52b3-113">Use hello following procedure toocreate a new backup policy.</span></span>

#### <a name="toocreate-a-backup-policy"></a><span data-ttu-id="a52b3-114">toocreate una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="a52b3-114">toocreate a backup policy</span></span>
1. <span data-ttu-id="a52b3-115">Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a52b3-115">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a52b3-116">Hola **ámbito** panel, haga clic en **directivas de copia de seguridad**y haga clic en **Crear directiva de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="a52b3-116">In hello **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Creación de una directiva de copia de seguridad](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="a52b3-118">Hola **crear una directiva** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a52b3-118">hello **Create a Policy** dialog box appears.</span></span>

    ![Creación de una directiva - pestaña General](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="a52b3-120">En hello **General** ficha, Hola completo siguiente información:</span><span class="sxs-lookup"><span data-stu-id="a52b3-120">On hello **General** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="a52b3-121">Hola **nombre** cuadro de texto, escriba un nombre para la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="a52b3-121">In hello **Name** text box, type a name for hello policy.</span></span>
   2. <span data-ttu-id="a52b3-122">Hola **grupo de volúmenes** cuadro de texto, escriba un nombre de grupo de volúmenes de hello asociado con la directiva de hello como Hola.</span><span class="sxs-lookup"><span data-stu-id="a52b3-122">In hello **Volume group** text box, type hello name of hello volume group associated with hello policy.</span></span>
   3. <span data-ttu-id="a52b3-123">Seleccione **Instantánea local** o **Instantánea de nube**.</span><span class="sxs-lookup"><span data-stu-id="a52b3-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="a52b3-124">Seleccione el número de Hola de tooretain de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="a52b3-124">Select hello number of snapshots tooretain.</span></span> <span data-ttu-id="a52b3-125">Si selecciona **todos los**, se conservarán 64 instantáneas (Hola máximo).</span><span class="sxs-lookup"><span data-stu-id="a52b3-125">If you select **All**, 64 snapshots will be retained (hello maximum).</span></span>
4. <span data-ttu-id="a52b3-126">Haga clic en hello **programación** ficha.</span><span class="sxs-lookup"><span data-stu-id="a52b3-126">Click hello **Schedule** tab.</span></span>

    ![Creación de una directiva - pestaña Programación](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="a52b3-128">En hello **programación** ficha, Hola completo siguiente información:</span><span class="sxs-lookup"><span data-stu-id="a52b3-128">On hello **Schedule** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="a52b3-129">Haga clic en hello **habilitar** casilla de verificación tooschedule Hola siguiente copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="a52b3-129">Click hello **Enable** check box tooschedule hello next backup.</span></span>
   2. <span data-ttu-id="a52b3-130">En **Configuración**, seleccione **Una vez**, **Diario**, **Semanal** o **Mensual**.</span><span class="sxs-lookup"><span data-stu-id="a52b3-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="a52b3-131">Hola **iniciar** cuadro de texto, haga clic en el icono del calendario de Hola y seleccione una fecha de inicio.</span><span class="sxs-lookup"><span data-stu-id="a52b3-131">In hello **Start** text box, click hello calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="a52b3-132">En **Configuración avanzada**, puede establecer programaciones de repetición opcionales y una fecha de finalización.</span><span class="sxs-lookup"><span data-stu-id="a52b3-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="a52b3-133">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a52b3-133">Click **OK**.</span></span>

<span data-ttu-id="a52b3-134">Después de crear una directiva de copia de seguridad, Hola siguiente información aparece en hello **resultados** panel:</span><span class="sxs-lookup"><span data-stu-id="a52b3-134">After you create a backup policy, hello following information appears in hello **Results** pane:</span></span>

* <span data-ttu-id="a52b3-135">**Nombre** : hello nombre de directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="a52b3-135">**Name** – hello name of backup policy.</span></span>
* <span data-ttu-id="a52b3-136">**Tipo** : instantánea local o instantánea de nube.</span><span class="sxs-lookup"><span data-stu-id="a52b3-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="a52b3-137">**Grupo de volúmenes** : hello grupo de volúmenes asociado con la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="a52b3-137">**Volume Group** – hello volume group associated with hello policy.</span></span>
* <span data-ttu-id="a52b3-138">**Retención** : hello conserva el número de instantáneas; Hola máximo es 64.</span><span class="sxs-lookup"><span data-stu-id="a52b3-138">**Retention** – hello number of snapshots retained; hello maximum is 64.</span></span>
* <span data-ttu-id="a52b3-139">**Crear** : fecha de Hola que se creó esta directiva.</span><span class="sxs-lookup"><span data-stu-id="a52b3-139">**Created** – hello date that this policy was created.</span></span>
* <span data-ttu-id="a52b3-140">**Habilitado** : indica si la directiva de hello está actualmente en vigor: **True** indica que está en vigor; **False** indica que no está en vigor.</span><span class="sxs-lookup"><span data-stu-id="a52b3-140">**Enabled** – whether hello policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="a52b3-141">Edición de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="a52b3-141">Edit a backup policy</span></span>
<span data-ttu-id="a52b3-142">Usar hello siguiendo el procedimiento tooedit una directiva de copia de seguridad existente.</span><span class="sxs-lookup"><span data-stu-id="a52b3-142">Use hello following procedure tooedit an existing backup policy.</span></span>

#### <a name="tooedit-a-backup-policy"></a><span data-ttu-id="a52b3-143">tooedit una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="a52b3-143">tooedit a backup policy</span></span>
1. <span data-ttu-id="a52b3-144">Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a52b3-144">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a52b3-145">Hola **ámbito** panel, haga clic en hello **directivas de copia de seguridad** nodo.</span><span class="sxs-lookup"><span data-stu-id="a52b3-145">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="a52b3-146">Todas las directivas de copia de seguridad de hello aparecen en hello **resultados** panel.</span><span class="sxs-lookup"><span data-stu-id="a52b3-146">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="a52b3-147">Haga clic en directiva de Hola que desee tooedit y, a continuación, haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="a52b3-147">Right-click hello policy that you want tooedit, and then click **Edit**.</span></span>

    ![Edición de una directiva de copia de seguridad](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="a52b3-149">Cuando Hola **crear una directiva de** ventana aparece, escriba los cambios y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a52b3-149">When hello **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="a52b3-150">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="a52b3-150">Delete a backup policy</span></span>
<span data-ttu-id="a52b3-151">Usar hello siguiendo el procedimiento toodelete una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="a52b3-151">Use hello following procedure toodelete a backup policy.</span></span>

#### <a name="toodelete-a-backup-policy"></a><span data-ttu-id="a52b3-152">toodelete una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="a52b3-152">toodelete a backup policy</span></span>
1. <span data-ttu-id="a52b3-153">Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a52b3-153">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a52b3-154">Hola **ámbito** panel, haga clic en hello **directivas de copia de seguridad** nodo.</span><span class="sxs-lookup"><span data-stu-id="a52b3-154">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="a52b3-155">Todas las directivas de copia de seguridad de hello aparecen en hello **resultados** panel.</span><span class="sxs-lookup"><span data-stu-id="a52b3-155">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="a52b3-156">Haga clic en directiva de copia de seguridad de Hola que desee toodelete y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="a52b3-156">Right-click hello backup policy that you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="a52b3-157">Cuando aparezca el mensaje de bienvenida de confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="a52b3-157">When hello confirmation message appears, click **Yes**.</span></span>

    ![Eliminación de la confirmación de una directiva de copia de seguridad](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="a52b3-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a52b3-159">Next steps</span></span>
* <span data-ttu-id="a52b3-160">Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooadminister su solución de StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="a52b3-160">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="a52b3-161">Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooview y administrar los trabajos de copia de seguridad](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="a52b3-161">Learn how too[use StorSimple Snapshot Manager tooview and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
