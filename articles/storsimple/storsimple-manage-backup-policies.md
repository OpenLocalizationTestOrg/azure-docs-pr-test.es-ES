---
title: aaaManage las directivas de copia de seguridad de StorSimple | Documentos de Microsoft
description: "Explica cómo puede utilizar toocreate de servicio de StorSimple Manager hello y administrar copias de seguridad manuales, las programaciones de copia de seguridad y retención de copia de seguridad."
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
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a><span data-ttu-id="4b356-103">Usar directivas de copia de seguridad toomanage del servicio de administrador de StorSimple de Hola</span><span class="sxs-lookup"><span data-stu-id="4b356-103">Use hello StorSimple Manager service toomanage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="4b356-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4b356-104">Overview</span></span>
<span data-ttu-id="4b356-105">Este tutorial le explica cómo toouse Hola el servicio StorSimple Manager **directivas de copia de seguridad** página procesos de copia de seguridad de toocontrol y retención de copia de seguridad de los volúmenes de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4b356-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="4b356-106">También se describe cómo toocomplete una copia de seguridad manual.</span><span class="sxs-lookup"><span data-stu-id="4b356-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="4b356-107">Hola **directivas de copia de seguridad** página permite las directivas de copia de seguridad de toomanage y programación local y en la nube.</span><span class="sxs-lookup"><span data-stu-id="4b356-107">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="4b356-108">(Las directivas de copia de seguridad son programaciones de copia de seguridad de tooconfigure usado y retención de copia de seguridad de un conjunto de volúmenes). Directivas de copia de seguridad le permiten tootake una instantánea de varios volúmenes simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="4b356-108">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="4b356-109">Esto significa que las copias de seguridad de hello creados por una directiva de copia de seguridad estará copias coherente para bloqueos.</span><span class="sxs-lookup"><span data-stu-id="4b356-109">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="4b356-110">Esta página enumera las directivas de copia de seguridad de hello, sus tipos, volúmenes Hola asociado, número de Hola de copias de seguridad retenidas y Hola tooenable opción estas directivas.</span><span class="sxs-lookup"><span data-stu-id="4b356-110">This page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="4b356-111">Hola **directivas de copia de seguridad** página también permite toofilter Hola copia de seguridad las directivas existentes por uno o varios de hello siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="4b356-111">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="4b356-112">**Nombre de la directiva** : hello nombre asociado con la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b356-112">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="4b356-113">Hola distintos tipos de directivas incluyen:</span><span class="sxs-lookup"><span data-stu-id="4b356-113">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="4b356-114">Directivas programadas, creadas explícitamente por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b356-114">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="4b356-115">Directivas automáticas, que se crean cuando se habilitó la copia de seguridad de hello predeterminado para esta opción de volumen en tiempo de Hola para crear un volumen.</span><span class="sxs-lookup"><span data-stu-id="4b356-115">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="4b356-116">Estas directivas se denominan Nombredevolumen_predeterminado donde el nombre de volumen hace referencia toohello nombre de volumen de StorSimple configurado por el usuario de hello en el portal de Azure clásico Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="4b356-116">These policies are named as VolumeName_Default where Volume name refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="4b356-117">directivas automáticas Hola dar lugar a instantáneas diarias en la nube empezando por hora del dispositivo 22:30.</span><span class="sxs-lookup"><span data-stu-id="4b356-117">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="4b356-118">Las directivas importadas, creadas originalmente en hello StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="4b356-118">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="4b356-119">Estas tienen una etiqueta que describe Hola Administrador de instantáneas StorSimple host que se importaron las directivas de Hola de.</span><span class="sxs-lookup"><span data-stu-id="4b356-119">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="4b356-120">**Volúmenes** : Hola volúmenes asociados con la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b356-120">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="4b356-121">Todos los volúmenes de hello asociados a una directiva de copia de seguridad se agrupan cuando se crean las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4b356-121">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="4b356-122">**Última copia de seguridad correcta** : Hola fecha y hora de hello última copia de seguridad correcta realizada con esta directiva.</span><span class="sxs-lookup"><span data-stu-id="4b356-122">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="4b356-123">**Siguiente copia de seguridad** : Hola fecha y hora de hello siguiente copia de seguridad programada iniciada por esta directiva.</span><span class="sxs-lookup"><span data-stu-id="4b356-123">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="4b356-124">**Programaciones** : Hola número de programaciones asociadas a la directiva de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b356-124">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="4b356-125">operaciones de Hola de uso frecuente que puede realizar desde esta página son:</span><span class="sxs-lookup"><span data-stu-id="4b356-125">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="4b356-126">Agregar una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="4b356-126">Add a backup policy</span></span> 
* <span data-ttu-id="4b356-127">Incorporación o modificación de una programación</span><span class="sxs-lookup"><span data-stu-id="4b356-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="4b356-128">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="4b356-128">Delete a backup policy</span></span> 
* <span data-ttu-id="4b356-129">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="4b356-129">Take a manual backup</span></span> 
* <span data-ttu-id="4b356-130">Creación de una directiva de copia de seguridad personalizada con varios volúmenes y programaciones</span><span class="sxs-lookup"><span data-stu-id="4b356-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="4b356-131">Agregar una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="4b356-131">Add a backup policy</span></span>
<span data-ttu-id="4b356-132">Agregar una programación de tooautomatically de directiva de copia de seguridad de las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4b356-132">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="4b356-133">Realizar Hola siguiendo los pasos de hello tooadd portal clásico una directiva de copia de seguridad para el dispositivo StorSimple de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b356-133">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="4b356-134">Después de Agregar directiva hello, puede definir una programación (vea [agregar o modificar una programación](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="4b356-134">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="4b356-135">![Vídeo disponible](./media/storsimple-manage-backup-policies/Video_icon.png)**Vídeo disponible**</span><span class="sxs-lookup"><span data-stu-id="4b356-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="4b356-136">Haga clic en un vídeo que muestra cómo toocreate una variable local o en la nube de copia de seguridad Directiva, toowatch [aquí](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="4b356-136">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="4b356-137">Incorporación o modificación de una programación</span><span class="sxs-lookup"><span data-stu-id="4b356-137">Add or modify a schedule</span></span>
<span data-ttu-id="4b356-138">Puede agregar o modificar una programación que está adjunto tooan directiva de copia de seguridad existente en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4b356-138">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="4b356-139">Realizar pasos de hello Azure tooadd portal clásico de Hola o modificar una programación.</span><span class="sxs-lookup"><span data-stu-id="4b356-139">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="4b356-140">Eliminación de una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="4b356-140">Delete a backup policy</span></span>
<span data-ttu-id="4b356-141">Realizar Hola siguiendo los pasos indicados en hello toodelete portal clásico una directiva de copia de seguridad de Azure en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4b356-141">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="4b356-142">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="4b356-142">Take a manual backup</span></span>
<span data-ttu-id="4b356-143">Realizar pasos de hello Azure toocreate portal clásico a petición (manual) copia de seguridad de un único volumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b356-143">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="4b356-144">Creación de una directiva de copia de seguridad personalizada con varios volúmenes y programaciones</span><span class="sxs-lookup"><span data-stu-id="4b356-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="4b356-145">Realizar Hola pasos de hello toocreate portal clásico una directiva de copia de seguridad personalizada que tiene varios volúmenes y programas de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b356-145">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="4b356-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b356-146">Next steps</span></span>
<span data-ttu-id="4b356-147">Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4b356-147">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

