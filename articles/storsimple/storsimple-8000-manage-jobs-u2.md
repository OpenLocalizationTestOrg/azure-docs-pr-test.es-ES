---
title: "Visualización y administración de trabajos para la serie StorSimple 8000 | Microsoft Docs"
description: "Describe la hoja Trabajos del servicio StorSimple Device Manager y cómo usarla para realizar un seguimiento de los trabajos de copia de seguridad programados, actuales y recientes."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: bf8038b7171053b75eeb9aed88bff4246e65a8a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="d6a86-103">Uso del servicio StorSimple Device Manager para ver y administrar trabajos (Versión Update 3 o posterior)</span><span class="sxs-lookup"><span data-stu-id="d6a86-103">Use the StorSimple Device Manager service to view and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="d6a86-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d6a86-104">Overview</span></span>
<span data-ttu-id="d6a86-105">En la hoja **Trabajos** se ofrece un único portal central para ver y administrar trabajos iniciados en dispositivos conectados a su servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="d6a86-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="d6a86-106">Puede ver los trabajos programados, en ejecución, completados, cancelados y con error de varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d6a86-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="d6a86-107">Los resultados se presentan en un formato tabular.</span><span class="sxs-lookup"><span data-stu-id="d6a86-107">Results are presented in a tabular format.</span></span>

![Hoja de trabajos](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="d6a86-109">Puede buscar rápidamente los trabajos que le interesan filtrando por campos como:</span><span class="sxs-lookup"><span data-stu-id="d6a86-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="d6a86-110">**Estado**: los trabajos pueden tener los siguientes estados: en curso, correcto, cancelado, erróneo, cancelando o se completó con errores.</span><span class="sxs-lookup"><span data-stu-id="d6a86-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="d6a86-111">**Intervalo de tiempo**: los trabajos se pueden filtrar según el intervalo de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="d6a86-111">**Time range** – Jobs can be filtered based on the date and time range.</span></span> <span data-ttu-id="d6a86-112">Los intervalos de tiempo pueden ser: última hora, últimas 24 horas, últimos 7 días, últimos 30 días, último año y fecha personalizada.</span><span class="sxs-lookup"><span data-stu-id="d6a86-112">The ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="d6a86-113">**Tipo**: los tipos pueden ser: copia de seguridad programada, copia de seguridad manual, restauración de copia de seguridad, clonación de volumen, conmutación por error de contenedores de volúmenes, creación de volúmenes anclados localmente, modificación de volumen, instalación de actualizaciones, recopilación de registros de soporte técnico y creación de dispositivos en la nube.</span><span class="sxs-lookup"><span data-stu-id="d6a86-113">**Type** – The job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="d6a86-114">**Dispositivos** : los trabajos se inician en un determinado dispositivo conectado a su servicio.</span><span class="sxs-lookup"><span data-stu-id="d6a86-114">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  
<span data-ttu-id="d6a86-115">A continuación, los trabajos filtrados se tabulan en función de los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="d6a86-115">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
* <span data-ttu-id="d6a86-116">**Nombre**: copia de seguridad programada, copia de seguridad manual, restauración de copia de seguridad, clonación de volumen, conmutación por error de contenedores de volúmenes, creación de volúmenes anclados localmente, modificación de volumen, instalación de actualizaciones, recopilación de registros de soporte técnico o creación de dispositivos en la nube.</span><span class="sxs-lookup"><span data-stu-id="d6a86-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="d6a86-117">**Estado** : en ejecución, programados, con errores, cancelándose o completados con errores.</span><span class="sxs-lookup"><span data-stu-id="d6a86-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="d6a86-118">**Entidad** : los trabajos se pueden asociar a un volumen, una directiva de copia de seguridad o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d6a86-118">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="d6a86-119">Por ejemplo, un trabajo de clonación se asocia a un volumen, mientras que un trabajo de copia de seguridad programado está asociado a una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d6a86-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="d6a86-120">Se crea un trabajo de dispositivo como resultado de una recuperación ante desastres (DR) o una operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="d6a86-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="d6a86-121">**Dispositivo** : el nombre del dispositivo en el que se inició el trabajo.</span><span class="sxs-lookup"><span data-stu-id="d6a86-121">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="d6a86-122">**Hora de inicio** : la hora a la que se inició el trabajo.</span><span class="sxs-lookup"><span data-stu-id="d6a86-122">**Started on** – The time when the job was started.</span></span>
* <span data-ttu-id="d6a86-123">**Duración**: el tiempo necesario para completar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="d6a86-123">**Duration** – The time required to complete the job.</span></span>

<span data-ttu-id="d6a86-124">La lista de trabajos se actualiza cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="d6a86-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="d6a86-125">Puede realizar las siguientes acciones relacionadas con el trabajo en esta página:</span><span class="sxs-lookup"><span data-stu-id="d6a86-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="d6a86-126">Ver detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="d6a86-126">View job details</span></span>
* <span data-ttu-id="d6a86-127">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="d6a86-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="d6a86-128">Ver detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="d6a86-128">View job details</span></span>
<span data-ttu-id="d6a86-129">Realice los pasos siguientes para ver los detalles de cualquier trabajo.</span><span class="sxs-lookup"><span data-stu-id="d6a86-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="d6a86-130">Para ver los detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="d6a86-130">To view job details</span></span>
1. <span data-ttu-id="d6a86-131">Vaya al servicio StorSimple Device Manager y, después, haga clic en **Trabajos**.</span><span class="sxs-lookup"><span data-stu-id="d6a86-131">Go to your StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="d6a86-132">En la hoja **Trabajos**, para mostrar los trabajos en los que esté interesado, ejecute una consulta con los filtros adecuados.</span><span class="sxs-lookup"><span data-stu-id="d6a86-132">In the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="d6a86-133">Puede buscar trabajos completados, en ejecución o cancelados.</span><span class="sxs-lookup"><span data-stu-id="d6a86-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Hoja de trabajos](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="d6a86-135">Seleccione y haga clic en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="d6a86-135">Select and click a job.</span></span>

    ![Hoja de trabajos](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="d6a86-137">En la hoja Detalles del trabajo, puede ver el estado, los detalles, así como las estadísticas de tiempo y de los datos.</span><span class="sxs-lookup"><span data-stu-id="d6a86-137">In the job details blade, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![Detalles del trabajo](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="d6a86-139">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="d6a86-139">Cancel a job</span></span>
<span data-ttu-id="d6a86-140">Realice los pasos siguientes para cancelar un trabajo en ejecución.</span><span class="sxs-lookup"><span data-stu-id="d6a86-140">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="d6a86-141">No se pueden cancelar algunos trabajos, como la modificación de un volumen para cambiar el tipo de volumen o expandir un volumen.</span><span class="sxs-lookup"><span data-stu-id="d6a86-141">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="to-cancel-a-job"></a><span data-ttu-id="d6a86-142">Para cancelar un trabajo</span><span class="sxs-lookup"><span data-stu-id="d6a86-142">To cancel a job</span></span>
1. <span data-ttu-id="d6a86-143">En la página **Trabajos** , para mostrar los trabajos en curso que quiere cancelar, ejecute una consulta con los filtros adecuados.</span><span class="sxs-lookup"><span data-stu-id="d6a86-143">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span> <span data-ttu-id="d6a86-144">Seleccione el trabajo.</span><span class="sxs-lookup"><span data-stu-id="d6a86-144">Select the job.</span></span>

2. <span data-ttu-id="d6a86-145">Haga clic con el botón derecho en el trabajo seleccionado para invocar el menú contextual y haga clic en **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="d6a86-145">Right-click on the selected job to invoke the context menu and click **Cancel**.</span></span>

    ![Detalles del trabajo](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="d6a86-147">Cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d6a86-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="d6a86-148">Ahora se cancelará este trabajo.</span><span class="sxs-lookup"><span data-stu-id="d6a86-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6a86-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6a86-149">Next steps</span></span>
* <span data-ttu-id="d6a86-150">Obtenga información sobre cómo [administrar las directivas de copia de seguridad de StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="d6a86-150">Learn how to [manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="d6a86-151">Aprenda a [usar el servicio StorSimple Device Manager para administrar el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d6a86-151">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

