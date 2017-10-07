---
title: un volumen de StorSimple de copia de seguridad aaaRestore | Documentos de Microsoft
description: "Explica cómo toouse Hola toorestore de página de catálogo de copia de seguridad de servicio de administrador de StorSimple un volumen de StorSimple de un conjunto de copia de seguridad."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="12249-103">Restaurar un volumen de StorSimple de un conjunto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="12249-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="12249-104">Información general</span><span class="sxs-lookup"><span data-stu-id="12249-104">Overview</span></span>
<span data-ttu-id="12249-105">Hola **catálogo de copia de seguridad** página muestra todos los conjuntos de copia de seguridad de Hola que se crean cuando se realizan copias de seguridad manuales o automatizadas.</span><span class="sxs-lookup"><span data-stu-id="12249-105">hello **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="12249-106">Puede usar a este toolist página todas las copias de seguridad de Hola para una directiva de copia de seguridad o un volumen, seleccione o eliminar las copias de seguridad, o utilizar una copia de seguridad toorestore o clonar un volumen.</span><span class="sxs-lookup"><span data-stu-id="12249-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

 ![Página del catálogo de copias de seguridad](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="12249-108">Este tutorial le explica cómo hello toouse **catálogo de copia de seguridad** página toorestore un volumen en el dispositivo desde un conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="12249-108">This tutorial explains how toouse hello **Backup Catalog** page toorestore a volume on your device from a backup set.</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="12249-109">¿Cómo toouse Hola catálogo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="12249-109">How toouse hello backup catalog</span></span>
<span data-ttu-id="12249-110">Hola **catálogo de copia de seguridad** página proporciona una consulta que le ayuda a toonarrow la selección de conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="12249-110">hello **Backup Catalog** page provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="12249-111">Puede filtrar Hola conjuntos de copia que se recuperan en función de hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="12249-111">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="12249-112">**Dispositivo** : dispositivo de hello en qué Hola se creó el conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="12249-112">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="12249-113">**Directiva de copia de seguridad** o **volumen** : Hola directiva de copia de seguridad o el volumen asociado a este conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="12249-113">**Backup policy** or **volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="12249-114">**De** y **a** : Hola intervalo de fecha y hora cuando se creó el conjunto de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-114">**From** and **To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="12249-115">Hello conjuntos de copia de seguridad filtrados se tabulan en función de los siguientes atributos de hello:</span><span class="sxs-lookup"><span data-stu-id="12249-115">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="12249-116">**Nombre** : hello nombre de directiva de copia de seguridad de Hola o volumen asociado con el conjunto de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-116">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="12249-117">**Tamaño** : Hola a tamaño real del conjunto de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-117">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="12249-118">**Crear en** : Hola fecha y la hora cuando se crearon las copias de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-118">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="12249-119">**Tipo** : los conjuntos de copias de seguridad pueden ser instantáneas locales o instantáneas en la nube.</span><span class="sxs-lookup"><span data-stu-id="12249-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="12249-120">Una instantánea local es una copia de seguridad de todos los datos de volumen almacenados localmente en el dispositivo de hello, mientras que una instantánea de nube hace referencia toohello copia de seguridad de datos del volumen que reside en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-120">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="12249-121">Las instantáneas locales proporcionan un acceso más rápido, mientras que las instantáneas en la nube son preferibles para la resistencia de los datos.</span><span class="sxs-lookup"><span data-stu-id="12249-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="12249-122">**Iniciado por** : las copias de seguridad de Hola se pueden iniciar automáticamente según la programación de tooa o manualmente por el usuario.</span><span class="sxs-lookup"><span data-stu-id="12249-122">**Initiated by** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="12249-123">(Puede usar copias de seguridad de tooschedule de una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="12249-123">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="12249-124">Como alternativa, puede usar hello **realizar copia de seguridad** opción tootake una copia de seguridad interactiva.)</span><span class="sxs-lookup"><span data-stu-id="12249-124">Alternatively, you can use hello **Take backup** option tootake an interactive backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="12249-125">Cómo toorestore su volumen de StorSimple desde una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="12249-125">How toorestore your StorSimple volume from a backup</span></span>
<span data-ttu-id="12249-126">Puede usar hello **catálogo de copia de seguridad** página toorestore su volumen de StorSimple desde una copia de seguridad específica.</span><span class="sxs-lookup"><span data-stu-id="12249-126">You can use hello **Backup Catalog** page toorestore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="12249-127">Restaurar a partir de una copia de seguridad sustituirá los volúmenes existentes de copia de seguridad de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-127">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="12249-128">Esto puede provocar la pérdida de Hola de los datos que se escriben después de que se realizó la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-128">This may cause hello loss of any data that was written after hello backup was taken.</span></span>
> 
> 

<span data-ttu-id="12249-129">Antes de iniciar una restauración en un volumen, asegúrese de que el volumen de hello está sin conexión.</span><span class="sxs-lookup"><span data-stu-id="12249-129">Before you initiate a restore on a volume, ensure that hello volume is offline.</span></span> <span data-ttu-id="12249-130">Necesitará tootake Hola volumen sin conexión Hola host primero y, a continuación, Hola dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12249-130">You will need tootake hello volume offline on hello host first and then hello device.</span></span> <span data-ttu-id="12249-131">Siga los pasos de hello en [desconectar un volumen](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="12249-131">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="12249-132">Realizar Hola siguiendo los pasos toorestore un volumen de un conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="12249-132">Perform hello following steps toorestore a volume from a backup set.</span></span>

### <a name="toorestore-from-a-backup-set"></a><span data-ttu-id="12249-133">toorestore de un conjunto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="12249-133">toorestore from a backup set</span></span>
1. <span data-ttu-id="12249-134">En la página del servicio de administrador de StorSimple de hello, haga clic en hello **catálogo de copia de seguridad** ficha.</span><span class="sxs-lookup"><span data-stu-id="12249-134">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
   
    ![Catálogo de copias de seguridad](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="12249-136">Seleccione una copia de seguridad de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="12249-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="12249-137">Seleccionar dispositivo apropiados de Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-137">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="12249-138">En la lista desplegable de hello, elija la que desea tooselect de directiva de copia de seguridad o volumen de Hola para copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-138">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="12249-139">Especifique el intervalo de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-139">Specify hello time range.</span></span>
   4. <span data-ttu-id="12249-140">Haga clic en el icono de verificación de Hola</span><span class="sxs-lookup"><span data-stu-id="12249-140">Click hello check icon</span></span> ![icono de marca de verificación](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="12249-142">tooexecute esta consulta.</span><span class="sxs-lookup"><span data-stu-id="12249-142">tooexecute this query.</span></span>
      
      <span data-ttu-id="12249-143">Hello deben aparecer copias de seguridad asociadas con la directiva de copia de seguridad o volumen de hello seleccionado en lista de Hola de conjuntos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="12249-143">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="12249-144">Expandir tooview Hola asociado volúmenes de hello conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="12249-144">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="12249-145">Estos volúmenes deben realizarse sin conexión en el host de Hola y el dispositivo antes de que pueda restaurarlos al completo.</span><span class="sxs-lookup"><span data-stu-id="12249-145">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="12249-146">Siga los pasos de hello en [desconectar un volumen](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="12249-146">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="12249-147">Asegúrese de que haya desconectado Hola volúmenes en el host de hello en primer lugar, antes de poner sin conexión los volúmenes de hello en dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-147">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="12249-148">Si no se realiza sin conexión los volúmenes de hello en el host de hello, pudieron causar daños toodata.</span><span class="sxs-lookup"><span data-stu-id="12249-148">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="12249-149">Seleccione un conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="12249-149">Select a backup set.</span></span> <span data-ttu-id="12249-150">Haga clic en **restaurar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-150">Click **Restore** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="12249-151">Se le pedirá confirmación.</span><span class="sxs-lookup"><span data-stu-id="12249-151">You will be prompted for confirmation.</span></span> 
   
    ![Página de confirmación](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="12249-153">Revise la información de restauración de Hola y haga clic en el icono de verificación de hello ![icono de comprobación](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="12249-153">Review hello restore information and click hello check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="12249-154">Esto iniciará un trabajo de restauración que se puede ver mediante el acceso a hello **trabajos** página.</span><span class="sxs-lookup"><span data-stu-id="12249-154">This will initiate a restore job that you can view by accessing hello **Jobs** page.</span></span> 
7. <span data-ttu-id="12249-155">Una vez completada la restauración de hello, puede comprobar que el contenido de Hola de los volúmenes se reemplaza por volúmenes de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="12249-155">After hello restore is complete, you can verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>

<span data-ttu-id="12249-156">![Vídeo disponible](./media/storsimple-restore-from-backup-set/Video_icon.png)**Vídeo disponible**</span><span class="sxs-lookup"><span data-stu-id="12249-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="12249-157">Haga clic en un vídeo que muestra cómo puede usar clon hello y restaurar las características de StorSimple toorecover eliminar archivos, toowatch [aquí](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="12249-157">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="12249-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12249-158">Next steps</span></span>
* <span data-ttu-id="12249-159">Obtenga información acerca de cómo demasiado[StorSimple administrar volúmenes](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="12249-159">Learn how too[Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="12249-160">Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="12249-160">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

