---
title: "Visualización y administración de trabajos de StorSimple | Microsoft Docs"
description: "Describe la página Trabajos del servicio Administrador de StorSimple y cómo usarla para realizar un seguimiento de los trabajos de copia de seguridad programados, actuales y recientes."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 6df1b27ce76de7a781ecc40af8430114d80b20d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="4527c-103">Usar el servicio de Administrador de StorSimple para ver y administrar trabajos de StorSimple (Update 2)</span><span class="sxs-lookup"><span data-stu-id="4527c-103">Use the StorSimple Manager service to view and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="4527c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4527c-104">Overview</span></span>
<span data-ttu-id="4527c-105">En la página **Trabajos** se ofrece un único portal central para ver y administrar trabajos iniciados en dispositivos conectados a su servicio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="4527c-105">The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service.</span></span> <span data-ttu-id="4527c-106">Puede ver los trabajos programados, en ejecución, completados, cancelados y con error de varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4527c-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="4527c-107">Los resultados se presentan en un formato tabular.</span><span class="sxs-lookup"><span data-stu-id="4527c-107">Results are presented in a tabular format.</span></span> 

![Página de trabajos](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="4527c-109">Puede buscar rápidamente los trabajos que le interesan filtrando por campos como:</span><span class="sxs-lookup"><span data-stu-id="4527c-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="4527c-110">**Estado** : los trabajos pueden estar en ejecución, programados, con errores, cancelándose o completados con errores.</span><span class="sxs-lookup"><span data-stu-id="4527c-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="4527c-111">**Desde y Hasta** : los trabajos se pueden filtrar según el intervalo de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="4527c-111">**From and To** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="4527c-112">**Tipo** : el tipo de trabajo puede ser copia de seguridad, copia de seguridad manual, restaurar, clonar, conmutación por error de dispositivo, crear volumen anclado localmente, modificar volumen, actualizar, paquete de soporte o aprovisionamiento de dispositivos virtuales.</span><span class="sxs-lookup"><span data-stu-id="4527c-112">**Type** – The job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="4527c-113">**Dispositivos** : los trabajos se inician en un determinado dispositivo conectado a su servicio.</span><span class="sxs-lookup"><span data-stu-id="4527c-113">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  <span data-ttu-id="4527c-114">A continuación, los trabajos filtrados se tabulan en función de los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="4527c-114">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
  * <span data-ttu-id="4527c-115">**Tipo** : copia de seguridad, copia de seguridad manual, restaurar, clonar, conmutación por error de dispositivo, crear volumen anclado localmente, modificar volumen, actualizar, paquete de soporte o aprovisionamiento de dispositivos virtuales.</span><span class="sxs-lookup"><span data-stu-id="4527c-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="4527c-116">**Estado** : en ejecución, programados, con errores, cancelándose o completados con errores.</span><span class="sxs-lookup"><span data-stu-id="4527c-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="4527c-117">**Entidad** : los trabajos se pueden asociar a un volumen, una directiva de copia de seguridad o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4527c-117">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="4527c-118">Por ejemplo, un trabajo de clonación se asocia a un volumen, mientras que un trabajo de copia de seguridad programado está asociado a una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4527c-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="4527c-119">Se crea un trabajo de dispositivo como resultado de una recuperación ante desastres (DR) o una operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="4527c-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="4527c-120">**Dispositivo** : el nombre del dispositivo en el que se inició el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4527c-120">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="4527c-121">**Hora de inicio** : la hora a la que se inició el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4527c-121">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="4527c-122">**Progreso** : el porcentaje de finalización de un trabajo en ejecución.</span><span class="sxs-lookup"><span data-stu-id="4527c-122">**Progress** – The percentage completion of a running job.</span></span> <span data-ttu-id="4527c-123">Para un trabajo completado, este debe equivaler siempre al 100%.</span><span class="sxs-lookup"><span data-stu-id="4527c-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="4527c-124">La lista de trabajos se actualiza cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="4527c-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="4527c-125">Puede realizar las siguientes acciones relacionadas con el trabajo en esta página:</span><span class="sxs-lookup"><span data-stu-id="4527c-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="4527c-126">Ver detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="4527c-126">View job details</span></span>
* <span data-ttu-id="4527c-127">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="4527c-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="4527c-128">Ver detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="4527c-128">View job details</span></span>
<span data-ttu-id="4527c-129">Realice los pasos siguientes para ver los detalles de cualquier trabajo.</span><span class="sxs-lookup"><span data-stu-id="4527c-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="4527c-130">Para ver los detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="4527c-130">To view job details</span></span>
1. <span data-ttu-id="4527c-131">En la página **Trabajos** , para mostrar los trabajos en los que esté interesado, ejecute una consulta con los filtros adecuados.</span><span class="sxs-lookup"><span data-stu-id="4527c-131">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="4527c-132">Puede buscar trabajos completados, en ejecución o cancelados.</span><span class="sxs-lookup"><span data-stu-id="4527c-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="4527c-133">Seleccione un trabajo.</span><span class="sxs-lookup"><span data-stu-id="4527c-133">Select a job.</span></span>
3. <span data-ttu-id="4527c-134">En la parte inferior de la página, haga clic en **Detalles**.</span><span class="sxs-lookup"><span data-stu-id="4527c-134">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="4527c-135">En el cuadro de diálogo **Detalles del trabajo de copia de seguridad** , puede ver el estado, los detalles, así como las estadísticas de tiempo y de los datos.</span><span class="sxs-lookup"><span data-stu-id="4527c-135">In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![Página Detalles del trabajo](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="4527c-137">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="4527c-137">Cancel a job</span></span>
<span data-ttu-id="4527c-138">Realice los pasos siguientes para cancelar un trabajo en ejecución.</span><span class="sxs-lookup"><span data-stu-id="4527c-138">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="4527c-139">No se pueden cancelar algunos trabajos, como la modificación de un volumen para cambiar el tipo de volumen o expandir un volumen.</span><span class="sxs-lookup"><span data-stu-id="4527c-139">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="to-cancel-a-job"></a><span data-ttu-id="4527c-140">Para cancelar un trabajo</span><span class="sxs-lookup"><span data-stu-id="4527c-140">To cancel a job</span></span>
1. <span data-ttu-id="4527c-141">En la página **Trabajos** , para mostrar los trabajos en curso que quiere cancelar, ejecute una consulta con los filtros adecuados.</span><span class="sxs-lookup"><span data-stu-id="4527c-141">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="4527c-142">Seleccione el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4527c-142">Select the job.</span></span>
3. <span data-ttu-id="4527c-143">En la parte inferior de la página, haga clic en **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="4527c-143">At the bottom of the page, click **Cancel**.</span></span>
4. <span data-ttu-id="4527c-144">Cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="4527c-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="4527c-145">Ahora se cancelará este trabajo.</span><span class="sxs-lookup"><span data-stu-id="4527c-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4527c-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4527c-146">Next steps</span></span>
* <span data-ttu-id="4527c-147">Obtenga información sobre cómo [administrar las directivas de copia de seguridad de StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4527c-147">Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="4527c-148">Obtenga información sobre cómo [usar el servicio StorSimple Manager para administrar el dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4527c-148">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

