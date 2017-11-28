---
title: "Administración de directivas de copia de seguridad de la serie StorSimple 8000 | Microsoft Docs"
description: "Explica cómo se puede usar el servicio StorSimple Device Manager para crear y administrar copias de seguridad manuales, programaciones de copia de seguridad y retención de copia de seguridad en un dispositivo de la serie StorSimple 8000."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 569dbfdeb7dcd526cb5a54b487ea1bfb59b13cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-in-azure-portal-to-manage-backup-policies"></a><span data-ttu-id="1da49-103">Uso del servicio StorSimple Device Manager de Azure Portal para administrar directivas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="1da49-103">Use the StorSimple Device Manager service in Azure portal to manage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="1da49-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1da49-104">Overview</span></span>

<span data-ttu-id="1da49-105">Este tutorial explica cómo utilizar la hoja **Directivas de copia de seguridad** del servicio StorSimple Device Manager para controlar los procesos de copia de seguridad y la retención de copias de seguridad de los volúmenes de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1da49-105">This tutorial explains how to use the StorSimple Device Manager service **Backup policy** blade to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="1da49-106">También describe cómo realizar copias de seguridad manuales.</span><span class="sxs-lookup"><span data-stu-id="1da49-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="1da49-107">Cuando realice una copia de un volumen, puede elegir crear una instantánea local o una instantánea de nube.</span><span class="sxs-lookup"><span data-stu-id="1da49-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="1da49-108">Si está realizando una copia de seguridad de un volumen anclado localmente, se recomienda que especifique una instantánea de nube.</span><span class="sxs-lookup"><span data-stu-id="1da49-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="1da49-109">La realización de un gran número de instantáneas de un volumen anclado localmente junto con un conjunto de datos que tenga una gran cantidad actividad dará como resultado una situación en la que podría quedarse rápidamente sin espacio local.</span><span class="sxs-lookup"><span data-stu-id="1da49-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="1da49-110">Si elige realizar instantáneas locales, se recomienda que realice menos instantáneas diarias para realizar una copia de seguridad del estado más reciente, conservarlas durante un día y eliminarlas.</span><span class="sxs-lookup"><span data-stu-id="1da49-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="1da49-111">Al realizar una instantánea en la nube de un volumen anclado localmente, se copian solo los datos modificados en la nube, donde se desduplican y se comprimen.</span><span class="sxs-lookup"><span data-stu-id="1da49-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span>

## <a name="the-backup-policy-blade"></a><span data-ttu-id="1da49-112">Hoja Directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="1da49-112">The Backup policy blade</span></span>

<span data-ttu-id="1da49-113">La hoja **Directiva de copia de seguridad** del dispositivo StorSimple le permite administrar las directivas de copia de seguridad y programar instantáneas locales y en la nube.</span><span class="sxs-lookup"><span data-stu-id="1da49-113">The **Backup policy** blade for your StorSimple device allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="1da49-114">Las directivas de copia de seguridad se usan para configurar las programaciones de copia de seguridad y la retención de copias de seguridad de una colección de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="1da49-114">Backup policies are used to configure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="1da49-115">Las directivas de copia de seguridad le permiten tomar una instantánea de varios volúmenes simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="1da49-115">Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="1da49-116">Esto significa que las copias de seguridad creadas por una directiva de copia de seguridad serán copias preparadas para bloqueos.</span><span class="sxs-lookup"><span data-stu-id="1da49-116">This means that the backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="1da49-117">La lista tabular de directivas de copia de seguridad también permite filtrar las directivas de copia de seguridad existentes por uno, o varios, de los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="1da49-117">The backup policies tabular listing also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="1da49-118">**Nombre de directiva** : el nombre asociado con la directiva.</span><span class="sxs-lookup"><span data-stu-id="1da49-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="1da49-119">Los distintos tipos de directivas incluyen:</span><span class="sxs-lookup"><span data-stu-id="1da49-119">The different types of policies include:</span></span>

  * <span data-ttu-id="1da49-120">Directivas programadas, que las crea explícitamente el usuario.</span><span class="sxs-lookup"><span data-stu-id="1da49-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="1da49-121">Directivas importadas, que se crearon originalmente en el Administrador de instantáneas de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1da49-121">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="1da49-122">Dichas directivas tienen una etiqueta que describe el host de Administrador de instantáneas StorSimple del que se importaron las directivas.</span><span class="sxs-lookup"><span data-stu-id="1da49-122">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1da49-123">La directivas de copia de seguridad automáticas o predeterminadas han dejado de habilitarse en el momento de la creación del volumen.</span><span class="sxs-lookup"><span data-stu-id="1da49-123">Automatic or default backup policies are no longer enabled at the time of volume creation.</span></span>

* <span data-ttu-id="1da49-124">**Última copia de seguridad correcta** : la fecha y hora de la última copia de seguridad correcta que se ha realizado con esta directiva.</span><span class="sxs-lookup"><span data-stu-id="1da49-124">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="1da49-125">**Siguiente copia de seguridad** : la fecha y hora de la siguiente copia de seguridad programada que iniciará esta directiva.</span><span class="sxs-lookup"><span data-stu-id="1da49-125">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="1da49-126">**Volúmenes** : los volúmenes asociados a la directiva.</span><span class="sxs-lookup"><span data-stu-id="1da49-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="1da49-127">Cuando se crean copias de seguridad se agrupan todos los volúmenes asociados a una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="1da49-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="1da49-128">**Programaciones** : el número de programaciones asociadas a la directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="1da49-128">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="1da49-129">Estas son las operaciones utilizadas con frecuencia que se pueden realizar con las directivas de copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="1da49-129">The frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="1da49-130">Incorporación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="1da49-130">Add a backup policy</span></span>
* <span data-ttu-id="1da49-131">Incorporación o modificación de una programación</span><span class="sxs-lookup"><span data-stu-id="1da49-131">Add or modify a schedule</span></span>
* <span data-ttu-id="1da49-132">Incorporación o eliminación de un volumen</span><span class="sxs-lookup"><span data-stu-id="1da49-132">Add or remove a volume</span></span>
* <span data-ttu-id="1da49-133">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="1da49-133">Delete a backup policy</span></span>
* <span data-ttu-id="1da49-134">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="1da49-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="1da49-135">Incorporación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="1da49-135">Add a backup policy</span></span>

<span data-ttu-id="1da49-136">Agregue una directiva de copia de seguridad para programar automáticamente sus copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="1da49-136">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="1da49-137">Cuando crea un volumen por primera vez, no hay ninguna directiva de copia de seguridad predeterminada asociada a este.</span><span class="sxs-lookup"><span data-stu-id="1da49-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="1da49-138">Debe agregar y asignar una directiva de copia de seguridad para proteger los datos del volumen.</span><span class="sxs-lookup"><span data-stu-id="1da49-138">You need to add and assign a backup policy to protect volume data.</span></span>

<span data-ttu-id="1da49-139">Realice los pasos siguientes en Azure Portal para agregar una directiva de copia de seguridad para el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1da49-139">Perform the following steps in the Azure portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="1da49-140">Después de agregar la directiva, puede definir una programación (vea [Incorporación o modificación de una programación](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="1da49-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="1da49-141">Incorporación o modificación de una programación</span><span class="sxs-lookup"><span data-stu-id="1da49-141">Add or modify a schedule</span></span>

<span data-ttu-id="1da49-142">Es posible agregar o modificar una programación adjunta a una directiva de copia de seguridad de un dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1da49-142">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="1da49-143">Siga estos pasos en Azure Portal para agregar o modificar una programación.</span><span class="sxs-lookup"><span data-stu-id="1da49-143">Perform the following steps in the Azure portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="1da49-144">Incorporación o eliminación de un volumen</span><span class="sxs-lookup"><span data-stu-id="1da49-144">Add or remove a volume</span></span>

<span data-ttu-id="1da49-145">Puede agregar o quitar un volumen asignado a una directiva de copia de seguridad en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1da49-145">You can add or remove a volume assigned to a backup policy on your StorSimple device.</span></span> <span data-ttu-id="1da49-146">Siga los pasos siguientes en Azure Portal para agregar o quitar un volumen.</span><span class="sxs-lookup"><span data-stu-id="1da49-146">Perform the following steps in the Azure portal to add or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="1da49-147">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="1da49-147">Delete a backup policy</span></span>

<span data-ttu-id="1da49-148">Realice los pasos siguientes en Azure Portal para eliminar una directiva de copia de seguridad del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1da49-148">Perform the following steps in the Azure portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="1da49-149">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="1da49-149">Take a manual backup</span></span>

<span data-ttu-id="1da49-150">Siga estos pasos en Azure Portal para crear una copia de seguridad a petición (manual) de un único volumen.</span><span class="sxs-lookup"><span data-stu-id="1da49-150">Perform the following steps in the Azure portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="1da49-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1da49-151">Next steps</span></span>

<span data-ttu-id="1da49-152">Más información sobre el [uso del servicio StorSimple Device Manager para administrar su dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1da49-152">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

