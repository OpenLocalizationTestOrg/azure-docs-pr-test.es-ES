---
title: aaaView y administrar los trabajos de StorSimple | Documentos de Microsoft
description: "Describe la página de trabajos del servicio de administrador de StorSimple de Hola y cómo toouse, trabajos de copia de tootrack recientes, actual y programada."
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
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="f32cd-103">Usar tooview de servicio de StorSimple Manager hello y administrar los trabajos de StorSimple (actualización 2)</span><span class="sxs-lookup"><span data-stu-id="f32cd-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="f32cd-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f32cd-104">Overview</span></span>
<span data-ttu-id="f32cd-105">Hola **trabajos** página proporciona un solo portal central para ver y administrar los trabajos iniciados en los dispositivos conectados tooyour el servicio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="f32cd-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="f32cd-106">Puede ver los trabajos programados, en ejecución, completados, cancelados y con error de varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f32cd-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="f32cd-107">Los resultados se presentan en un formato tabular.</span><span class="sxs-lookup"><span data-stu-id="f32cd-107">Results are presented in a tabular format.</span></span> 

![Página de trabajos](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="f32cd-109">Puede buscar rápidamente los trabajos de Hola que le interesan filtrando en los campos, como:</span><span class="sxs-lookup"><span data-stu-id="f32cd-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="f32cd-110">**Estado** : los trabajos pueden estar en ejecución, programados, con errores, cancelándose o completados con errores.</span><span class="sxs-lookup"><span data-stu-id="f32cd-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="f32cd-111">**FROM y To** – trabajos pueden ser el intervalo de fecha y hora de hello en función de filtrado.</span><span class="sxs-lookup"><span data-stu-id="f32cd-111">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="f32cd-112">**Tipo de** : tipo de trabajo de hello puede ser la copia de seguridad, copia de seguridad manual, restauración, clonación, conmutación por error de dispositivo, crear volumen anclado localmente, modificar el volumen, actualizar, admite el paquete o el aprovisionamiento del dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="f32cd-112">**Type** – hello job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="f32cd-113">**Dispositivos** – trabajos se inician en un servicio determinado tooyour de dispositivo conectado.</span><span class="sxs-lookup"><span data-stu-id="f32cd-113">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  <span data-ttu-id="f32cd-114">Hello trabajos filtrados se tabulan en función de Hola de hello siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="f32cd-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
  * <span data-ttu-id="f32cd-115">**Tipo** : copia de seguridad, copia de seguridad manual, restaurar, clonar, conmutación por error de dispositivo, crear volumen anclado localmente, modificar volumen, actualizar, paquete de soporte o aprovisionamiento de dispositivos virtuales.</span><span class="sxs-lookup"><span data-stu-id="f32cd-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="f32cd-116">**Estado** : en ejecución, programados, con errores, cancelándose o completados con errores.</span><span class="sxs-lookup"><span data-stu-id="f32cd-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="f32cd-117">**Entidad** : Hola trabajos se pueden asociar con un volumen, una directiva de copia de seguridad o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f32cd-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="f32cd-118">Por ejemplo, un trabajo de clonación se asocia a un volumen, mientras que un trabajo de copia de seguridad programado está asociado a una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f32cd-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="f32cd-119">Se crea un trabajo de dispositivo como resultado de una recuperación ante desastres (DR) o una operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="f32cd-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="f32cd-120">**Dispositivo** : hello nombre de dispositivo de hello en qué Hola se inició el trabajo.</span><span class="sxs-lookup"><span data-stu-id="f32cd-120">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="f32cd-121">**Iniciado en** : tiempo de hello cuando se inició el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f32cd-121">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="f32cd-122">**Curso** : Hola porcentaje de finalización de un trabajo en ejecución.</span><span class="sxs-lookup"><span data-stu-id="f32cd-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="f32cd-123">Para un trabajo completado, este debe equivaler siempre al 100%.</span><span class="sxs-lookup"><span data-stu-id="f32cd-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="f32cd-124">lista de Hola de trabajos se actualiza cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="f32cd-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="f32cd-125">Puede realizar Hola siguiente acciones relacionadas con el trabajo de esta página:</span><span class="sxs-lookup"><span data-stu-id="f32cd-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="f32cd-126">Ver detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="f32cd-126">View job details</span></span>
* <span data-ttu-id="f32cd-127">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="f32cd-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="f32cd-128">Ver detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="f32cd-128">View job details</span></span>
<span data-ttu-id="f32cd-129">Realizar Hola pasos tooview Hola detalles de cualquier trabajo siguientes.</span><span class="sxs-lookup"><span data-stu-id="f32cd-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="f32cd-130">Detalles del trabajo tooview</span><span class="sxs-lookup"><span data-stu-id="f32cd-130">tooview job details</span></span>
1. <span data-ttu-id="f32cd-131">En hello **trabajos** página, muestre los trabajos de Hola que está interesado ejecutando una consulta con los filtros correspondientes.</span><span class="sxs-lookup"><span data-stu-id="f32cd-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="f32cd-132">Puede buscar trabajos completados, en ejecución o cancelados.</span><span class="sxs-lookup"><span data-stu-id="f32cd-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="f32cd-133">Seleccione un trabajo.</span><span class="sxs-lookup"><span data-stu-id="f32cd-133">Select a job.</span></span>
3. <span data-ttu-id="f32cd-134">En la parte inferior de Hola de página de hello, haga clic en **detalles**.</span><span class="sxs-lookup"><span data-stu-id="f32cd-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="f32cd-135">Hola **detalles del trabajo de copia de seguridad** cuadro de diálogo, puede ver el estado de hello, detalles, estadísticas de tiempo y las estadísticas de datos.</span><span class="sxs-lookup"><span data-stu-id="f32cd-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Página Detalles del trabajo](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="f32cd-137">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="f32cd-137">Cancel a job</span></span>
<span data-ttu-id="f32cd-138">Realizar Hola siguiendo los pasos toocancel un trabajo en ejecución.</span><span class="sxs-lookup"><span data-stu-id="f32cd-138">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="f32cd-139">No se puede cancelar algunos trabajos, como modificar un tipo de volumen de volumen toochange Hola o expandir un volumen.</span><span class="sxs-lookup"><span data-stu-id="f32cd-139">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="toocancel-a-job"></a><span data-ttu-id="f32cd-140">toocancel un trabajo</span><span class="sxs-lookup"><span data-stu-id="f32cd-140">toocancel a job</span></span>
1. <span data-ttu-id="f32cd-141">En hello **trabajos** página, mostrar hello trabajos en ejecución que desea que toocancel mediante la ejecución de una consulta con los filtros correspondientes.</span><span class="sxs-lookup"><span data-stu-id="f32cd-141">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="f32cd-142">Seleccione el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f32cd-142">Select hello job.</span></span>
3. <span data-ttu-id="f32cd-143">En la parte inferior de Hola de página de hello, haga clic en **cancelar**.</span><span class="sxs-lookup"><span data-stu-id="f32cd-143">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="f32cd-144">Cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="f32cd-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="f32cd-145">Ahora se cancelará este trabajo.</span><span class="sxs-lookup"><span data-stu-id="f32cd-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f32cd-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f32cd-146">Next steps</span></span>
* <span data-ttu-id="f32cd-147">Obtenga información acerca de cómo demasiado[administrar las directivas de copia de seguridad de StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f32cd-147">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="f32cd-148">Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f32cd-148">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

