---
title: directivas de copia de seguridad aaaManage StorSimple 8000 series | Documentos de Microsoft
description: "Explica cómo puede utilizar toocreate de servicio del Administrador de dispositivos de StorSimple de Hola y administrar copias de seguridad manuales, las programaciones de copia de seguridad y retención de copia de seguridad en un dispositivo de la serie StorSimple 8000."
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
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a><span data-ttu-id="ce100-103">Usar el servicio de administrador de dispositivos de StorSimple de hello en las directivas de copia de seguridad de Azure toomanage portal</span><span class="sxs-lookup"><span data-stu-id="ce100-103">Use hello StorSimple Device Manager service in Azure portal toomanage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="ce100-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ce100-104">Overview</span></span>

<span data-ttu-id="ce100-105">Este tutorial le explica cómo toouse Hola servicio Administrador de dispositivos de StorSimple **directiva de copia de seguridad** procesos de copia de seguridad de toocontrol de hoja y retención de copia de seguridad de los volúmenes de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ce100-105">This tutorial explains how toouse hello StorSimple Device Manager service **Backup policy** blade toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="ce100-106">También se describe cómo toocomplete una copia de seguridad manual.</span><span class="sxs-lookup"><span data-stu-id="ce100-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="ce100-107">Al hacer copia de seguridad de un volumen, puede elegir toocreate una instantánea local o una instantánea en la nube.</span><span class="sxs-lookup"><span data-stu-id="ce100-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="ce100-108">Si está realizando una copia de seguridad de un volumen anclado localmente, se recomienda que especifique una instantánea de nube.</span><span class="sxs-lookup"><span data-stu-id="ce100-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="ce100-109">La realización de un gran número de instantáneas de un volumen anclado localmente junto con un conjunto de datos que tenga una gran cantidad actividad dará como resultado una situación en la que podría quedarse rápidamente sin espacio local.</span><span class="sxs-lookup"><span data-stu-id="ce100-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="ce100-110">Si elige tootake instantáneas locales, se recomienda que ocupan menos tooback instantáneas diarias estado más reciente de hello, mantenerlas durante un mismo día y eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="ce100-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="ce100-111">Al tomar una instantánea de nube de un volumen anclado localmente, copiar solo Hola cambiar datos toohello en la nube, donde se desduplican y comprimido.</span><span class="sxs-lookup"><span data-stu-id="ce100-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span>

## <a name="hello-backup-policy-blade"></a><span data-ttu-id="ce100-112">hoja de directiva de copia de seguridad de Hola</span><span class="sxs-lookup"><span data-stu-id="ce100-112">hello Backup policy blade</span></span>

<span data-ttu-id="ce100-113">Hola **directiva de copia de seguridad** hoja para el dispositivo StorSimple permite las directivas de copia de seguridad de toomanage y programación local y en la nube.</span><span class="sxs-lookup"><span data-stu-id="ce100-113">hello **Backup policy** blade for your StorSimple device allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="ce100-114">Directivas de copia de seguridad son programaciones de copia de seguridad utilizados tooconfigure y retención de copia de seguridad de un conjunto de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="ce100-114">Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="ce100-115">Directivas de copia de seguridad le permiten tootake una instantánea de varios volúmenes simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="ce100-115">Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="ce100-116">Esto significa que las copias de seguridad de hello creados por una directiva de copia de seguridad estará copias coherente para bloqueos.</span><span class="sxs-lookup"><span data-stu-id="ce100-116">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="ce100-117">lista tabular de directivas de copia de seguridad de Hola también permite toofilter Hola copia de seguridad las directivas existentes por uno o varios de hello después de campos:</span><span class="sxs-lookup"><span data-stu-id="ce100-117">hello backup policies tabular listing also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="ce100-118">**Nombre de la directiva** : hello nombre asociado con la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce100-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="ce100-119">Hola distintos tipos de directivas incluyen:</span><span class="sxs-lookup"><span data-stu-id="ce100-119">hello different types of policies include:</span></span>

  * <span data-ttu-id="ce100-120">Directivas programadas, creadas explícitamente por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce100-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="ce100-121">Las directivas importadas, creadas originalmente en hello StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="ce100-121">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="ce100-122">Estas tienen una etiqueta que describe Hola Administrador de instantáneas StorSimple host que se importaron las directivas de Hola de.</span><span class="sxs-lookup"><span data-stu-id="ce100-122">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ce100-123">Directivas de copia de seguridad automática o de forma predeterminada ya no están habilitadas en tiempo de Hola para crear un volumen.</span><span class="sxs-lookup"><span data-stu-id="ce100-123">Automatic or default backup policies are no longer enabled at hello time of volume creation.</span></span>

* <span data-ttu-id="ce100-124">**Última copia de seguridad correcta** : Hola fecha y hora de hello última copia de seguridad correcta realizada con esta directiva.</span><span class="sxs-lookup"><span data-stu-id="ce100-124">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="ce100-125">**Siguiente copia de seguridad** : Hola fecha y hora de hello siguiente copia de seguridad programada iniciada por esta directiva.</span><span class="sxs-lookup"><span data-stu-id="ce100-125">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="ce100-126">**Volúmenes** : Hola volúmenes asociados con la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce100-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="ce100-127">Todos los volúmenes de hello asociados a una directiva de copia de seguridad se agrupan cuando se crean las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ce100-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="ce100-128">**Programaciones** : Hola número de programaciones asociadas a la directiva de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce100-128">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="ce100-129">operaciones de Hola de uso frecuente que puede realizar para las directivas de copia de seguridad son:</span><span class="sxs-lookup"><span data-stu-id="ce100-129">hello frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="ce100-130">Agregar una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="ce100-130">Add a backup policy</span></span>
* <span data-ttu-id="ce100-131">Incorporación o modificación de una programación</span><span class="sxs-lookup"><span data-stu-id="ce100-131">Add or modify a schedule</span></span>
* <span data-ttu-id="ce100-132">Incorporación o eliminación de un volumen</span><span class="sxs-lookup"><span data-stu-id="ce100-132">Add or remove a volume</span></span>
* <span data-ttu-id="ce100-133">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="ce100-133">Delete a backup policy</span></span>
* <span data-ttu-id="ce100-134">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="ce100-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="ce100-135">Agregar una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="ce100-135">Add a backup policy</span></span>

<span data-ttu-id="ce100-136">Agregar una programación de tooautomatically de directiva de copia de seguridad de las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ce100-136">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="ce100-137">Cuando crea un volumen por primera vez, no hay ninguna directiva de copia de seguridad predeterminada asociada a este.</span><span class="sxs-lookup"><span data-stu-id="ce100-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="ce100-138">Es necesario tooadd y asignar una directiva de copia de seguridad tooprotect volumen de datos.</span><span class="sxs-lookup"><span data-stu-id="ce100-138">You need tooadd and assign a backup policy tooprotect volume data.</span></span>

<span data-ttu-id="ce100-139">Realizar pasos de hello tooadd portal Azure una directiva de copia de seguridad para el dispositivo StorSimple de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce100-139">Perform hello following steps in hello Azure portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="ce100-140">Después de Agregar directiva hello, puede definir una programación (vea [agregar o modificar una programación](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="ce100-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="ce100-141">Incorporación o modificación de una programación</span><span class="sxs-lookup"><span data-stu-id="ce100-141">Add or modify a schedule</span></span>

<span data-ttu-id="ce100-142">Puede agregar o modificar una programación que está adjunto tooan directiva de copia de seguridad existente en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ce100-142">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="ce100-143">Realizar Hola pasos de hello Azure tooadd portal o modificar una programación.</span><span class="sxs-lookup"><span data-stu-id="ce100-143">Perform hello following steps in hello Azure portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="ce100-144">Incorporación o eliminación de un volumen</span><span class="sxs-lookup"><span data-stu-id="ce100-144">Add or remove a volume</span></span>

<span data-ttu-id="ce100-145">Puede agregar o quitar un volumen asignado tooa directiva de copia de seguridad en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ce100-145">You can add or remove a volume assigned tooa backup policy on your StorSimple device.</span></span> <span data-ttu-id="ce100-146">Realizar Hola pasos de hello Azure tooadd portal o quitar un volumen.</span><span class="sxs-lookup"><span data-stu-id="ce100-146">Perform hello following steps in hello Azure portal tooadd or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="ce100-147">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="ce100-147">Delete a backup policy</span></span>

<span data-ttu-id="ce100-148">Realizar Hola siguiendo los pasos indicados en hello toodelete portal Azure una directiva de copia de seguridad en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ce100-148">Perform hello following steps in hello Azure portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="ce100-149">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="ce100-149">Take a manual backup</span></span>

<span data-ttu-id="ce100-150">Realizar pasos de hello toocreate portal Azure bajo demanda (manual) copia de seguridad de un único volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce100-150">Perform hello following steps in hello Azure portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="ce100-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce100-151">Next steps</span></span>

<span data-ttu-id="ce100-152">Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ce100-152">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

