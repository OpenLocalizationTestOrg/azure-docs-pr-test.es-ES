---
title: "Administración de directivas de copia de seguridad de StorSimple | Microsoft Docs"
description: "Explica cómo se puede usar el servicio Administrador de StorSimple para crear y administrar copias de seguridad manuales, programaciones de copia de seguridad y retención de copia de seguridad."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: c1e9d5d0450bab5d371aafb40fd7c5920d39dfdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies"></a><span data-ttu-id="cac08-103">Usar el servicio de Administrador de StorSimple para administrar directivas de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="cac08-103">Use the StorSimple Manager service to manage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="cac08-104">Información general</span><span class="sxs-lookup"><span data-stu-id="cac08-104">Overview</span></span>
<span data-ttu-id="cac08-105">Este tutorial explica cómo utilizar la página **Directivas de copia de seguridad** del  Servicio de Administrador de StorSimple para controlar los procesos de copia de seguridad y la retención de copias de seguridad de los volúmenes de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cac08-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="cac08-106">También describe cómo realizar copias de seguridad manuales.</span><span class="sxs-lookup"><span data-stu-id="cac08-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="cac08-107">La página **Directivas de copia de seguridad** permite administrar las directivas de copia de seguridad y programar instantáneas locales y en la nube.</span><span class="sxs-lookup"><span data-stu-id="cac08-107">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="cac08-108">(Las directivas de copia de seguridad se usan para configurar las programaciones de copia de seguridad y la retención de copias de seguridad de una colección de volúmenes). Las directivas de copia de seguridad le permiten tomar una instantánea de varios volúmenes simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="cac08-108">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="cac08-109">Esto significa que las copias de seguridad creadas por una directiva de copia de seguridad serán copias preparadas para bloqueos.</span><span class="sxs-lookup"><span data-stu-id="cac08-109">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="cac08-110">Esta página enumera las directivas de copia de seguridad, sus tipos, los volúmenes asociados, el número de copias de seguridad retenidas y la opción para habilitar estas directivas.</span><span class="sxs-lookup"><span data-stu-id="cac08-110">This page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="cac08-111">La página **Directivas de copia de seguridad** también permite filtrar las directivas de copia de seguridad existentes por uno, o varios, de los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="cac08-111">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="cac08-112">**Nombre de directiva** : el nombre asociado con la directiva.</span><span class="sxs-lookup"><span data-stu-id="cac08-112">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="cac08-113">Los distintos tipos de directivas incluyen:</span><span class="sxs-lookup"><span data-stu-id="cac08-113">The different types of policies include:</span></span>
  
  * <span data-ttu-id="cac08-114">Directivas programadas, que las crea explícitamente el usuario.</span><span class="sxs-lookup"><span data-stu-id="cac08-114">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="cac08-115">Directivas automáticas, que se crean al habilitar la copia de seguridad predeterminada de esta opción de volumen en el momento en que se creó dicho volumen.</span><span class="sxs-lookup"><span data-stu-id="cac08-115">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="cac08-116">Estas directivas se denominan VolumeName_Default, donde el nombre del volumen hace referencia al nombre del volumen de StorSimple que ha configurado el usuario en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="cac08-116">These policies are named as VolumeName_Default where Volume name refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="cac08-117">Las directivas automáticas generan instantáneas diarias en la nube a partir de las 22:30, hora del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cac08-117">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="cac08-118">Directivas importadas, que se crearon originalmente en el Administrador de instantáneas de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cac08-118">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="cac08-119">Dichas directivas tienen una etiqueta que describe el host de Administrador de instantáneas StorSimple del que se importaron las directivas.</span><span class="sxs-lookup"><span data-stu-id="cac08-119">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="cac08-120">**Volúmenes** : los volúmenes asociados a la directiva.</span><span class="sxs-lookup"><span data-stu-id="cac08-120">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="cac08-121">Cuando se crean copias de seguridad se agrupan todos los volúmenes asociados a una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cac08-121">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="cac08-122">**Última copia de seguridad correcta** : la fecha y hora de la última copia de seguridad correcta que se ha realizado con esta directiva.</span><span class="sxs-lookup"><span data-stu-id="cac08-122">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="cac08-123">**Siguiente copia de seguridad** : la fecha y hora de la siguiente copia de seguridad programada que iniciará esta directiva.</span><span class="sxs-lookup"><span data-stu-id="cac08-123">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="cac08-124">**Programaciones** : el número de programaciones asociadas a la directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cac08-124">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="cac08-125">Estas son las operaciones utilizadas con frecuencia que se pueden realizar desde esta página:</span><span class="sxs-lookup"><span data-stu-id="cac08-125">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="cac08-126">Incorporación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="cac08-126">Add a backup policy</span></span> 
* <span data-ttu-id="cac08-127">Incorporación o modificación de una programación</span><span class="sxs-lookup"><span data-stu-id="cac08-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="cac08-128">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="cac08-128">Delete a backup policy</span></span> 
* <span data-ttu-id="cac08-129">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="cac08-129">Take a manual backup</span></span> 
* <span data-ttu-id="cac08-130">Creación de una directiva de copia de seguridad personalizada con varios volúmenes y programaciones</span><span class="sxs-lookup"><span data-stu-id="cac08-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="cac08-131">Incorporación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="cac08-131">Add a backup policy</span></span>
<span data-ttu-id="cac08-132">Agregue una directiva de copia de seguridad para programar automáticamente sus copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="cac08-132">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="cac08-133">Realice los pasos siguientes en el Portal de Azure clásico para agregar una directiva de copia de seguridad para el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cac08-133">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="cac08-134">Después de agregar la directiva, puede definir una programación (vea [Incorporación o modificación de una programación](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="cac08-134">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="cac08-135">![Vídeo disponible](./media/storsimple-manage-backup-policies/Video_icon.png) **Vídeo disponible**</span><span class="sxs-lookup"><span data-stu-id="cac08-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="cac08-136">Para ver un vídeo en el que se muestra cómo crear una directiva de copia de seguridad local o en la nube, haga clic [aquí](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="cac08-136">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="cac08-137">Incorporación o modificación de una programación</span><span class="sxs-lookup"><span data-stu-id="cac08-137">Add or modify a schedule</span></span>
<span data-ttu-id="cac08-138">Es posible agregar o modificar una programación adjunta a una directiva de copia de seguridad de un dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cac08-138">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="cac08-139">Siga estos pasos en el Portal de Azure clásico para agregar o modificar una programación.</span><span class="sxs-lookup"><span data-stu-id="cac08-139">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="cac08-140">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="cac08-140">Delete a backup policy</span></span>
<span data-ttu-id="cac08-141">Realice los pasos siguientes en el Portal de Azure clásico para eliminar una directiva de copia de seguridad del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cac08-141">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="cac08-142">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="cac08-142">Take a manual backup</span></span>
<span data-ttu-id="cac08-143">Siga estos pasos en el Portal de Azure clásico para crear una copia de seguridad a petición (manual) de un único volumen.</span><span class="sxs-lookup"><span data-stu-id="cac08-143">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="cac08-144">Creación de una directiva de copia de seguridad personalizada con varios volúmenes y programaciones</span><span class="sxs-lookup"><span data-stu-id="cac08-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="cac08-145">Realice los pasos siguientes en el Portal de Azure clásico para crear una directiva de copia de seguridad personalizada que tenga varios volúmenes y programaciones.</span><span class="sxs-lookup"><span data-stu-id="cac08-145">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="cac08-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cac08-146">Next steps</span></span>
<span data-ttu-id="cac08-147">Obtenga más información sobre el [uso del servicio StorSimple Manager para administrar su dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="cac08-147">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

