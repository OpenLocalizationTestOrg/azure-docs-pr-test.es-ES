---
title: Trabajos de copia de seguridad de StorSimple Snapshot Manager | Microsoft Docs
description: "Describe cómo usar el complemento MMC de Administrador de instantáneas StorSimple para ver y administrar trabajos de copia de seguridad programados, actualmente en ejecución y completados."
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
ms.openlocfilehash: 03e306b62250f2bb033cc14e856a59760b5406c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a><span data-ttu-id="95e85-103">Uso de Administrador de instantáneas StorSimple para ver y administrar trabajos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="95e85-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="95e85-104">Información general</span><span class="sxs-lookup"><span data-stu-id="95e85-104">Overview</span></span>
<span data-ttu-id="95e85-105">En el panel **Ámbito**, El nodo **Trabajos** muestra las tareas de copia de seguridad **Programada**, **Últimas 24 horas** y **En ejecución** que se han iniciado de forma interactiva o mediante una directiva configurada.</span><span class="sxs-lookup"><span data-stu-id="95e85-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="95e85-106">Este tutorial explica cómo se puede usar el nodo **Trabajos** para mostrar información sobre los trabajos de copia de seguridad programados, recientes y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="95e85-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="95e85-107">(La lista de trabajos y la información correspondiente aparecen en el panel **Resultados**). Además, puede es posible hacer clic en un trabajo de la lista y ver un menú contextual que enumera las acciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="95e85-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="95e85-108">Visualización de los trabajos programados</span><span class="sxs-lookup"><span data-stu-id="95e85-108">View scheduled jobs</span></span>
<span data-ttu-id="95e85-109">Use el procedimiento siguiente para ver los trabajos de copia de seguridad programados.</span><span class="sxs-lookup"><span data-stu-id="95e85-109">Use the following procedure to view scheduled backup jobs.</span></span>

#### <a name="to-view-scheduled-jobs"></a><span data-ttu-id="95e85-110">Para ver los trabajos programados</span><span class="sxs-lookup"><span data-stu-id="95e85-110">To view scheduled jobs</span></span>
1. <span data-ttu-id="95e85-111">Haga clic en el icono del escritorio para iniciar Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="95e85-111">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="95e85-112">En el panel **Ámbito**, expanda el nodo **Trabajos** y, después, haga clic en **Programado**.</span><span class="sxs-lookup"><span data-stu-id="95e85-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="95e85-113">La siguiente información aparece en el panel **Resultados** :</span><span class="sxs-lookup"><span data-stu-id="95e85-113">The following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="95e85-114">**Nombre** : el nombre de la instantánea programada</span><span class="sxs-lookup"><span data-stu-id="95e85-114">**Name** – the name of the scheduled snapshot</span></span>
   * <span data-ttu-id="95e85-115">**Siguiente ejecución** : la fecha y hora de la siguiente instantánea programada</span><span class="sxs-lookup"><span data-stu-id="95e85-115">**Next Run** – the date and time of the next scheduled snapshot</span></span>
   * <span data-ttu-id="95e85-116">**Última ejecución** : la fecha y hora de la instantánea programada más reciente</span><span class="sxs-lookup"><span data-stu-id="95e85-116">**Last Run** – the date and time of the most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="95e85-117">En las instantáneas que se realizan una sola vez, los valores de **Siguiente ejecución** y **Última ejecución** serán iguales.</span><span class="sxs-lookup"><span data-stu-id="95e85-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span></span>
     
     ![Trabajos de copia de seguridad programados](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="95e85-119">Para realizar acciones adicionales en un trabajo específico, haga clic con el botón derecho en el nombre del trabajo en el panel **Resultados** y realice su selección entre las opciones de menú.</span><span class="sxs-lookup"><span data-stu-id="95e85-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="95e85-120">Visualización de los trabajos recientes</span><span class="sxs-lookup"><span data-stu-id="95e85-120">View recent jobs</span></span>
<span data-ttu-id="95e85-121">Utilice el procedimiento siguiente para ver la copia de seguridad y restaurar trabajos que se completaron en las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="95e85-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span></span>

#### <a name="to-view-recent-jobs"></a><span data-ttu-id="95e85-122">Para ver los trabajos recientes</span><span class="sxs-lookup"><span data-stu-id="95e85-122">To view recent jobs</span></span>
1. <span data-ttu-id="95e85-123">Haga clic en el icono del escritorio para iniciar Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="95e85-123">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="95e85-124">En el panel **Ámbito**, expanda el nodo **Trabajos** y, luego, haga clic en **Últimas 24 horas**.</span><span class="sxs-lookup"><span data-stu-id="95e85-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="95e85-125">El panel **Resultados** muestra los trabajos de copia de seguridad de las últimas 24 horas (hasta un máximo de 64 trabajos).</span><span class="sxs-lookup"><span data-stu-id="95e85-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span></span> <span data-ttu-id="95e85-126">La siguiente información aparece en el panel **Resultados**, según las opciones de **Vista** que se hayan especificado:</span><span class="sxs-lookup"><span data-stu-id="95e85-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span></span>
   
   * <span data-ttu-id="95e85-127">**Nombre** : el nombre de la instantánea programada.</span><span class="sxs-lookup"><span data-stu-id="95e85-127">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="95e85-128">**Iniciado** : fecha y hora del comienzo de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="95e85-128">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="95e85-129">**Detenido** : fecha y hora de la finalización o la interrupción de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="95e85-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="95e85-130">**Transcurrido**: la cantidad de tiempo entre los horarios de **Iniciado** y **Detenido**.</span><span class="sxs-lookup"><span data-stu-id="95e85-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="95e85-131">**Estado** : el estado del trabajo completado recientemente.</span><span class="sxs-lookup"><span data-stu-id="95e85-131">**Status** – the state of the recently completed job.</span></span> <span data-ttu-id="95e85-132">**Éxito** indica que la copia de seguridad se creó correctamente.</span><span class="sxs-lookup"><span data-stu-id="95e85-132">**Success** indicates that the backup was created successfully.</span></span> <span data-ttu-id="95e85-133">**Error** indica que el trabajo no se ejecutó correctamente.</span><span class="sxs-lookup"><span data-stu-id="95e85-133">**Failed** indicates that the job did not run successfully.</span></span>
   * <span data-ttu-id="95e85-134">**Información** : el motivo del error.</span><span class="sxs-lookup"><span data-stu-id="95e85-134">**Information** – the reason for the failure.</span></span>
   * <span data-ttu-id="95e85-135">**Bytes procesados (MB)** : la cantidad de datos del grupo de volúmenes que se procesó (en MB).</span><span class="sxs-lookup"><span data-stu-id="95e85-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span></span> 
     
     ![Trabajos ejecutados en las últimas 24 horas](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="95e85-137">Para realizar acciones adicionales en un trabajo específico, haga clic con el botón derecho en el nombre del trabajo en el panel **Resultados** y realice su selección entre las opciones de menú.</span><span class="sxs-lookup"><span data-stu-id="95e85-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>
   
    ![Eliminación de un trabajo](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="95e85-139">Visualización de los trabajos en ejecución</span><span class="sxs-lookup"><span data-stu-id="95e85-139">View currently running jobs</span></span>
<span data-ttu-id="95e85-140">Utilice el procedimiento siguiente para ver los trabajos que se están ejecutando en el momento presente.</span><span class="sxs-lookup"><span data-stu-id="95e85-140">Use the following procedure to view jobs that are currently running.</span></span>

#### <a name="to-view-currently-running-jobs"></a><span data-ttu-id="95e85-141">Para ver los trabajos en ejecución</span><span class="sxs-lookup"><span data-stu-id="95e85-141">To view currently running jobs</span></span>
1. <span data-ttu-id="95e85-142">Haga clic en el icono del escritorio para iniciar Administrador de instantáneas StorSimple.</span><span class="sxs-lookup"><span data-stu-id="95e85-142">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="95e85-143">En el panel **Ámbito**, expanda el nodo **Trabajos** y haga clic en **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="95e85-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="95e85-144">Dependiendo de las opciones de **Vista** que se especifiquen, aparece la siguiente información en el panel **Resultados**:</span><span class="sxs-lookup"><span data-stu-id="95e85-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="95e85-145">**Nombre** : el nombre de la instantánea programada.</span><span class="sxs-lookup"><span data-stu-id="95e85-145">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="95e85-146">**Iniciado** : fecha y hora del comienzo de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="95e85-146">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="95e85-147">**Punto de control** : la acción actual de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="95e85-147">**Checkpoint** – the current action of the backup.</span></span>
   * <span data-ttu-id="95e85-148">**Estado** : el porcentaje de finalización.</span><span class="sxs-lookup"><span data-stu-id="95e85-148">**Status** – the percentage of completion.</span></span>
   * <span data-ttu-id="95e85-149">**Transcurrido** : la cantidad de tiempo que ha transcurrido desde que comenzó la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="95e85-149">**Elapsed** – the amount of time that has passed since the backup began.</span></span> 
   * <span data-ttu-id="95e85-150">**Rendimiento medio (MB)** : la relación del total de bytes de datos procesados con el tiempo total necesario para realizar el procesamiento (MB).</span><span class="sxs-lookup"><span data-stu-id="95e85-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="95e85-151">**Bytes procesados (MB)** : total de bytes de los datos procesados (en MB).</span><span class="sxs-lookup"><span data-stu-id="95e85-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="95e85-152">**Bytes escritos (MB)** : total de bytes de los datos escritos (en MB).</span><span class="sxs-lookup"><span data-stu-id="95e85-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="95e85-153">Incluye los datos, así como los metadatos y, por tanto, es normalmente mayor que los bytes procesados.</span><span class="sxs-lookup"><span data-stu-id="95e85-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span></span>
     
     ![Trabajos en ejecución](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="95e85-155">Para realizar acciones adicionales en un trabajo específico, haga clic con el botón derecho en el nombre del trabajo en el panel **Resultados** y realice su selección entre las opciones de menú.</span><span class="sxs-lookup"><span data-stu-id="95e85-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95e85-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95e85-156">Next steps</span></span>
* <span data-ttu-id="95e85-157">Obtenga más información sobre el [uso de Snapshot Manager de StorSimple para administrar la solución de StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="95e85-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="95e85-158">Obtenga más información sobre el [uso de Snapshot Manager de StorSimple para administrar el catálogo de copias de seguridad](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="95e85-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

