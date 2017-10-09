---
title: "trabajos de copia de seguridad de administrador de instantáneas aaaStorSimple | Documentos de Microsoft"
description: "Describe cómo toouse Hola instantáneas de StorSimple Manager MMC complemento tooview y administrar trabajos de copia de seguridad programados, actualmente en ejecución y completados."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a><span data-ttu-id="03a84-103">Use el Administrador de instantáneas StorSimple tooview y administrar los trabajos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="03a84-103">Use StorSimple Snapshot Manager tooview and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="03a84-104">Información general</span><span class="sxs-lookup"><span data-stu-id="03a84-104">Overview</span></span>
<span data-ttu-id="03a84-105">Hola **trabajos** nodo Hola **ámbito** panel muestra hello **programada**, **últimas 24 horas**, y **ejecutando**copia de seguridad de las tareas que inició interactivamente o mediante una directiva configurada.</span><span class="sxs-lookup"><span data-stu-id="03a84-105">hello **Jobs** node in hello **Scope** pane shows hello **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="03a84-106">Este tutorial le explica cómo puede usar hello **trabajos** información del nodo toodisplay acerca de los trabajos de copia de seguridad programadas, recientes y que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="03a84-106">This tutorial explains how you can use hello **Jobs** node toodisplay information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="03a84-107">(lista de Hola de trabajos e información correspondiente aparece en hello **resultados** panel.) Además, puede es posible hacer clic en un trabajo de la lista y ver un menú contextual que enumera las acciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="03a84-107">(hello list of jobs and corresponding information appears in hello **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="03a84-108">Visualización de los trabajos programados</span><span class="sxs-lookup"><span data-stu-id="03a84-108">View scheduled jobs</span></span>
<span data-ttu-id="03a84-109">Hola uso siguiendo el procedimiento tooview programa trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="03a84-109">Use hello following procedure tooview scheduled backup jobs.</span></span>

#### <a name="tooview-scheduled-jobs"></a><span data-ttu-id="03a84-110">tooview programar trabajos</span><span class="sxs-lookup"><span data-stu-id="03a84-110">tooview scheduled jobs</span></span>
1. <span data-ttu-id="03a84-111">Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="03a84-111">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="03a84-112">Hola **ámbito** panel, expanda hello **trabajos** nodo y haga clic en **programada**.</span><span class="sxs-lookup"><span data-stu-id="03a84-112">In hello **Scope** pane, expand hello **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="03a84-113">Hello siguiente información aparece en hello **resultados** panel:</span><span class="sxs-lookup"><span data-stu-id="03a84-113">hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="03a84-114">**Nombre** : hello nombre de instantánea programada Hola</span><span class="sxs-lookup"><span data-stu-id="03a84-114">**Name** – hello name of hello scheduled snapshot</span></span>
   * <span data-ttu-id="03a84-115">**A continuación ejecute** : Hola fecha y hora de la siguiente instantánea programada de Hola</span><span class="sxs-lookup"><span data-stu-id="03a84-115">**Next Run** – hello date and time of hello next scheduled snapshot</span></span>
   * <span data-ttu-id="03a84-116">**Última ejecución** : Hola fecha y hora de instantánea programada más reciente de Hola</span><span class="sxs-lookup"><span data-stu-id="03a84-116">**Last Run** – hello date and time of hello most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="03a84-117">Para las instantáneas sola una sola vez, Hola **siguiente ejecución** y **última ejecución** será Hola igual.</span><span class="sxs-lookup"><span data-stu-id="03a84-117">For one-time only snapshots, hello **Next Run** and **Last Run** will be hello same.</span></span>
     
     ![Trabajos de copia de seguridad programados](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="03a84-119">tooperform acciones adicionales en un trabajo específico, haga clic en el nombre del trabajo Hola Hola **resultados** panel y seleccione Hola opciones del menú.</span><span class="sxs-lookup"><span data-stu-id="03a84-119">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="03a84-120">Visualización de los trabajos recientes</span><span class="sxs-lookup"><span data-stu-id="03a84-120">View recent jobs</span></span>
<span data-ttu-id="03a84-121">Usar hello después de la copia de seguridad de procedimiento tooview y restaura los trabajos que se completaron en hello últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="03a84-121">Use hello following procedure tooview backup and restore jobs that were completed in hello last 24 hours.</span></span>

#### <a name="tooview-recent-jobs"></a><span data-ttu-id="03a84-122">trabajos recientes tooview</span><span class="sxs-lookup"><span data-stu-id="03a84-122">tooview recent jobs</span></span>
1. <span data-ttu-id="03a84-123">Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="03a84-123">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="03a84-124">Hola **ámbito** panel, expanda hello **trabajos** nodo y haga clic en **últimas 24 horas**.</span><span class="sxs-lookup"><span data-stu-id="03a84-124">In hello **Scope** pane, expand hello **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="03a84-125">Hola **resultados** panel muestra los trabajos de copia de seguridad para hello últimas 24 horas (tooa máximo de 64 trabajos).</span><span class="sxs-lookup"><span data-stu-id="03a84-125">hello **Results** pane shows backup jobs for hello last 24 hours (tooa maximum of 64 jobs).</span></span> <span data-ttu-id="03a84-126">Hello siguiente información aparece en hello **resultados** panel, dependiendo de hello **vista** opciones especificadas:</span><span class="sxs-lookup"><span data-stu-id="03a84-126">hello following information appears in hello **Results** pane, depending on hello **View** options you specify:</span></span>
   
   * <span data-ttu-id="03a84-127">**Nombre** : hello nombre de instantánea programada Hola.</span><span class="sxs-lookup"><span data-stu-id="03a84-127">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="03a84-128">**Iniciar** : Hola fecha y la hora de inicio de instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="03a84-128">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="03a84-129">**Detenido** : Hola fecha y la hora cuando instantánea Hola se finalizó o canceló.</span><span class="sxs-lookup"><span data-stu-id="03a84-129">**Stopped** – hello date and time when hello snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="03a84-130">**Transcurrido** : Hola período de tiempo entre hello **iniciado** y **detenido** veces.</span><span class="sxs-lookup"><span data-stu-id="03a84-130">**Elapsed** – hello amount of time between hello **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="03a84-131">**Estado** : Hola estado de hello completado recientemente trabajo.</span><span class="sxs-lookup"><span data-stu-id="03a84-131">**Status** – hello state of hello recently completed job.</span></span> <span data-ttu-id="03a84-132">**Éxito** indica que copia de seguridad de Hola se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="03a84-132">**Success** indicates that hello backup was created successfully.</span></span> <span data-ttu-id="03a84-133">**No se pudo** indica que el trabajo de hello no se ha ejecutado correctamente.</span><span class="sxs-lookup"><span data-stu-id="03a84-133">**Failed** indicates that hello job did not run successfully.</span></span>
   * <span data-ttu-id="03a84-134">**Información** : Hola motivo Hola error.</span><span class="sxs-lookup"><span data-stu-id="03a84-134">**Information** – hello reason for hello failure.</span></span>
   * <span data-ttu-id="03a84-135">**Bytes procesados (MB)** : cantidad de Hola de datos del grupo de volúmenes de Hola que se procesó (en MB).</span><span class="sxs-lookup"><span data-stu-id="03a84-135">**Bytes processed (MB)** – hello amount of data from hello volume group that was processed (in MBs).</span></span> 
     
     ![Trabajos ejecutados en hello últimas 24 horas](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="03a84-137">tooperform acciones adicionales en un trabajo específico, haga clic en el nombre del trabajo Hola Hola **resultados** panel y seleccione Hola opciones del menú.</span><span class="sxs-lookup"><span data-stu-id="03a84-137">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>
   
    ![Eliminación de un trabajo](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="03a84-139">Visualización de los trabajos en ejecución</span><span class="sxs-lookup"><span data-stu-id="03a84-139">View currently running jobs</span></span>
<span data-ttu-id="03a84-140">Usar hello después de los trabajos de tooview de procedimiento que se están ejecutando actualmente.</span><span class="sxs-lookup"><span data-stu-id="03a84-140">Use hello following procedure tooview jobs that are currently running.</span></span>

#### <a name="tooview-currently-running-jobs"></a><span data-ttu-id="03a84-141">tooview trabajos en ejecución</span><span class="sxs-lookup"><span data-stu-id="03a84-141">tooview currently running jobs</span></span>
1. <span data-ttu-id="03a84-142">Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="03a84-142">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="03a84-143">Hola **ámbito** panel, expanda hello **trabajos** nodo y haga clic en **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="03a84-143">In hello **Scope** pane, expand hello **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="03a84-144">Función hello **vista** opciones que se especifiquen, Hola siguiente información aparece en hello **resultados** panel:</span><span class="sxs-lookup"><span data-stu-id="03a84-144">Depending on hello **View** options you specify, hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="03a84-145">**Nombre** : hello nombre de instantánea programada Hola.</span><span class="sxs-lookup"><span data-stu-id="03a84-145">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="03a84-146">**Iniciar** : Hola fecha y la hora de inicio de instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="03a84-146">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="03a84-147">**Punto de comprobación** : Hola acción actual de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="03a84-147">**Checkpoint** – hello current action of hello backup.</span></span>
   * <span data-ttu-id="03a84-148">**Estado** : Hola porcentaje de finalización.</span><span class="sxs-lookup"><span data-stu-id="03a84-148">**Status** – hello percentage of completion.</span></span>
   * <span data-ttu-id="03a84-149">**Transcurrido** : cantidad de Hola de tiempo que ha transcurrido desde que comenzó la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="03a84-149">**Elapsed** – hello amount of time that has passed since hello backup began.</span></span> 
   * <span data-ttu-id="03a84-150">**Rendimiento medio (MB)** : proporción del total de bytes de datos procesados toothat de tiempo total de procesamiento (MB).</span><span class="sxs-lookup"><span data-stu-id="03a84-150">**Average throughput (MB)** – ratio of total bytes of data processed toothat of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="03a84-151">**Bytes procesados (MB)** : total de bytes de los datos procesados (en MB).</span><span class="sxs-lookup"><span data-stu-id="03a84-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="03a84-152">**Bytes escritos (MB)** : total de bytes de los datos escritos (en MB).</span><span class="sxs-lookup"><span data-stu-id="03a84-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="03a84-153">Incluye datos de hello así como los metadatos de hello y, por lo que es normalmente mayor que Hola Bytes procesados.</span><span class="sxs-lookup"><span data-stu-id="03a84-153">It includes hello data as well as hello metadata and hence is typically greater than hello Bytes Processed.</span></span>
     
     ![Trabajos en ejecución](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="03a84-155">tooperform acciones adicionales en un trabajo específico, haga clic en el nombre del trabajo Hola Hola **resultados** panel y seleccione Hola opciones del menú.</span><span class="sxs-lookup"><span data-stu-id="03a84-155">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03a84-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03a84-156">Next steps</span></span>
* <span data-ttu-id="03a84-157">Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooadminister su solución de StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="03a84-157">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="03a84-158">Obtenga información acerca de cómo demasiado[usar el catálogo de copia de seguridad de administrador de instantáneas StorSimple toomanage hello](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="03a84-158">Learn how too[use StorSimple Snapshot Manager toomanage hello backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

