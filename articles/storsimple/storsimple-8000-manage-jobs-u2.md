---
title: aaaView y administrar los trabajos de la serie 8000 de StorSimple | Documentos de Microsoft
description: "Describe la hoja de trabajos de servicio de administrador de dispositivos de StorSimple de Hola y cómo toouse, trabajos de copia de tootrack recientes, actual y programada."
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
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="e64a5-103">Usar tooview de servicio del Administrador de dispositivos de StorSimple de Hola y administrar trabajos (actualización 3 y posterior)</span><span class="sxs-lookup"><span data-stu-id="e64a5-103">Use hello StorSimple Device Manager service tooview and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="e64a5-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e64a5-104">Overview</span></span>
<span data-ttu-id="e64a5-105">Hola **trabajos** hoja proporciona un solo portal central para ver y administrar los trabajos iniciados en dispositivos de servicio de administrador de dispositivos de StorSimple de tooyour conectado.</span><span class="sxs-lookup"><span data-stu-id="e64a5-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="e64a5-106">Puede ver los trabajos programados, en ejecución, completados, cancelados y con error de varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e64a5-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="e64a5-107">Los resultados se presentan en un formato tabular.</span><span class="sxs-lookup"><span data-stu-id="e64a5-107">Results are presented in a tabular format.</span></span>

![Hoja de trabajos](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="e64a5-109">Puede buscar rápidamente los trabajos de Hola que le interesan filtrando en los campos, como:</span><span class="sxs-lookup"><span data-stu-id="e64a5-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="e64a5-110">**Estado**: los trabajos pueden tener los siguientes estados: en curso, correcto, cancelado, erróneo, cancelando o se completó con errores.</span><span class="sxs-lookup"><span data-stu-id="e64a5-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="e64a5-111">**El intervalo de tiempo** – trabajos pueden ser el intervalo de fecha y hora de hello en función de filtrado.</span><span class="sxs-lookup"><span data-stu-id="e64a5-111">**Time range** – Jobs can be filtered based on hello date and time range.</span></span> <span data-ttu-id="e64a5-112">intervalos de Hello son después de 1 hora, últimas 24 horas, más allá de 7 días, últimos 30 días, año pasado o fecha personalizado.</span><span class="sxs-lookup"><span data-stu-id="e64a5-112">hello ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="e64a5-113">**Tipo de** : tipo de trabajo de Hola puede ser la copia de seguridad programada, la copia de seguridad manual, la copia de seguridad de la restauración, clonar volumen, conmutar por error contenedores de volúmenes, crear volumen anclado localmente, modificar el volumen, instalar actualizaciones, recopilar registros de soporte técnico y crear el dispositivo en la nube.</span><span class="sxs-lookup"><span data-stu-id="e64a5-113">**Type** – hello job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="e64a5-114">**Dispositivos** – trabajos se inician en un servicio determinado tooyour de dispositivo conectado.</span><span class="sxs-lookup"><span data-stu-id="e64a5-114">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  
<span data-ttu-id="e64a5-115">Hello trabajos filtrados se tabulan en función de Hola de hello siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="e64a5-115">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
* <span data-ttu-id="e64a5-116">**Nombre**: copia de seguridad programada, copia de seguridad manual, restauración de copia de seguridad, clonación de volumen, conmutación por error de contenedores de volúmenes, creación de volúmenes anclados localmente, modificación de volumen, instalación de actualizaciones, recopilación de registros de soporte técnico o creación de dispositivos en la nube.</span><span class="sxs-lookup"><span data-stu-id="e64a5-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="e64a5-117">**Estado** : en ejecución, programados, con errores, cancelándose o completados con errores.</span><span class="sxs-lookup"><span data-stu-id="e64a5-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="e64a5-118">**Entidad** : Hola trabajos se pueden asociar con un volumen, una directiva de copia de seguridad o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e64a5-118">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="e64a5-119">Por ejemplo, un trabajo de clonación se asocia a un volumen, mientras que un trabajo de copia de seguridad programado está asociado a una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e64a5-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="e64a5-120">Se crea un trabajo de dispositivo como resultado de una recuperación ante desastres (DR) o una operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="e64a5-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="e64a5-121">**Dispositivo** : hello nombre de dispositivo de hello en qué Hola se inició el trabajo.</span><span class="sxs-lookup"><span data-stu-id="e64a5-121">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="e64a5-122">**Iniciado en** : tiempo de hello cuando se inició el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e64a5-122">**Started on** – hello time when hello job was started.</span></span>
* <span data-ttu-id="e64a5-123">**Duración** : trabajo hello toocomplete necesario Hola.</span><span class="sxs-lookup"><span data-stu-id="e64a5-123">**Duration** – hello time required toocomplete hello job.</span></span>

<span data-ttu-id="e64a5-124">lista de Hola de trabajos se actualiza cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="e64a5-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="e64a5-125">Puede realizar Hola siguiente acciones relacionadas con el trabajo de esta página:</span><span class="sxs-lookup"><span data-stu-id="e64a5-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="e64a5-126">Ver detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="e64a5-126">View job details</span></span>
* <span data-ttu-id="e64a5-127">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="e64a5-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="e64a5-128">Ver detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="e64a5-128">View job details</span></span>
<span data-ttu-id="e64a5-129">Realizar Hola pasos tooview Hola detalles de cualquier trabajo siguientes.</span><span class="sxs-lookup"><span data-stu-id="e64a5-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="e64a5-130">Detalles del trabajo tooview</span><span class="sxs-lookup"><span data-stu-id="e64a5-130">tooview job details</span></span>
1. <span data-ttu-id="e64a5-131">Servicio de administrador de dispositivos de StorSimple tooyour y, a continuación, haga clic en **trabajos**.</span><span class="sxs-lookup"><span data-stu-id="e64a5-131">Go tooyour StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="e64a5-132">Hola **trabajos** hoja, trabajos de Hola de presentación que está interesado ejecutando una consulta con los filtros correspondientes.</span><span class="sxs-lookup"><span data-stu-id="e64a5-132">In hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="e64a5-133">Puede buscar trabajos completados, en ejecución o cancelados.</span><span class="sxs-lookup"><span data-stu-id="e64a5-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Hoja de trabajos](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="e64a5-135">Seleccione y haga clic en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="e64a5-135">Select and click a job.</span></span>

    ![Hoja de trabajos](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="e64a5-137">En la hoja de detalles del trabajo de hello, puede ver estado de hello, detalles, estadísticas de tiempo y las estadísticas de datos.</span><span class="sxs-lookup"><span data-stu-id="e64a5-137">In hello job details blade, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Detalles del trabajo](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="e64a5-139">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="e64a5-139">Cancel a job</span></span>
<span data-ttu-id="e64a5-140">Realizar Hola siguiendo los pasos toocancel un trabajo en ejecución.</span><span class="sxs-lookup"><span data-stu-id="e64a5-140">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="e64a5-141">No se puede cancelar algunos trabajos, como modificar un tipo de volumen de volumen toochange Hola o expandir un volumen.</span><span class="sxs-lookup"><span data-stu-id="e64a5-141">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="toocancel-a-job"></a><span data-ttu-id="e64a5-142">toocancel un trabajo</span><span class="sxs-lookup"><span data-stu-id="e64a5-142">toocancel a job</span></span>
1. <span data-ttu-id="e64a5-143">En hello **trabajos** página, mostrar hello trabajos en ejecución que desea que toocancel mediante la ejecución de una consulta con los filtros correspondientes.</span><span class="sxs-lookup"><span data-stu-id="e64a5-143">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span> <span data-ttu-id="e64a5-144">Seleccione el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e64a5-144">Select hello job.</span></span>

2. <span data-ttu-id="e64a5-145">Haga doble clic en el menú contextual de hello trabajo seleccionado tooinvoke hello y haga clic en **cancelar**.</span><span class="sxs-lookup"><span data-stu-id="e64a5-145">Right-click on hello selected job tooinvoke hello context menu and click **Cancel**.</span></span>

    ![Detalles del trabajo](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="e64a5-147">Cuando se le pida confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="e64a5-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="e64a5-148">Ahora se cancelará este trabajo.</span><span class="sxs-lookup"><span data-stu-id="e64a5-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e64a5-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e64a5-149">Next steps</span></span>
* <span data-ttu-id="e64a5-150">Obtenga información acerca de cómo demasiado[administrar las directivas de copia de seguridad de StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="e64a5-150">Learn how too[manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="e64a5-151">Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e64a5-151">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

