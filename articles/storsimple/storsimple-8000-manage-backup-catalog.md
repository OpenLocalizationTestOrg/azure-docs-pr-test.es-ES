---
title: "aaaManage el catálogo de copia de seguridad de StorSimple | Documentos de Microsoft"
description: "Explica cómo toouse hello toolist de página de catálogo de copia de seguridad de servicio de administrador de dispositivos de StorSimple, seleccionar y eliminar conjuntos de copia de seguridad."
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
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="13d5e-103">Usar toomanage de servicio del Administrador de dispositivos de StorSimple de hello en el catálogo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="13d5e-103">Use hello StorSimple Device Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="13d5e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="13d5e-104">Overview</span></span>
<span data-ttu-id="13d5e-105">Hola servicio Administrador de dispositivos de StorSimple **catálogo de copia de seguridad** hoja muestra todos los conjuntos de copia de seguridad de Hola que se crean cuando se realizan copias de seguridad manuales o programados.</span><span class="sxs-lookup"><span data-stu-id="13d5e-105">hello StorSimple Device Manager service **Backup Catalog** blade displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="13d5e-106">Puede usar a este toolist página todas las copias de seguridad de Hola para una directiva de copia de seguridad o un volumen, seleccione o eliminar las copias de seguridad, o utilizar una copia de seguridad toorestore o clonar un volumen.</span><span class="sxs-lookup"><span data-stu-id="13d5e-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="13d5e-107">Este tutorial le explica cómo toolist, seleccionar y eliminar una copia de seguridad establecido.</span><span class="sxs-lookup"><span data-stu-id="13d5e-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="13d5e-108">toolearn cómo toorestore el dispositivo de copia de seguridad, vaya demasiado[restaurar el dispositivo desde un conjunto de copia de seguridad](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="13d5e-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="13d5e-109">toolearn cómo tooclone un volumen, vaya demasiado[clonar un volumen de StorSimple](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="13d5e-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Catálogo de copias de seguridad](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="13d5e-111">Hola **catálogo de copia de seguridad** hoja proporciona una consulta toonarrow la selección de conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-111">hello **Backup Catalog** blade provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="13d5e-112">Puede filtrar los conjuntos de copia de seguridad de Hola que se recuperan en función de hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="13d5e-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="13d5e-113">**Dispositivo** : dispositivo de hello en qué Hola se creó el conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="13d5e-114">**Directiva de copia de seguridad o el volumen** : Hola directiva de copia de seguridad o el volumen asociado a este conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-114">**Backup policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="13d5e-115">**FROM y To** : Hola intervalo de fecha y hora cuando se creó el conjunto de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="13d5e-116">Hello conjuntos de copia de seguridad filtrados se tabulan en función de los siguientes atributos de hello:</span><span class="sxs-lookup"><span data-stu-id="13d5e-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="13d5e-117">**Nombre** : hello nombre de directiva de copia de seguridad de Hola o volumen asociado con el conjunto de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="13d5e-118">**Tamaño** : Hola a tamaño real del conjunto de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="13d5e-119">**Fecha de creación de** : Hola fecha y la hora cuando se crearon las copias de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="13d5e-120">**Tipo** : los conjuntos de copias de seguridad pueden ser instantáneas locales o instantáneas en la nube.</span><span class="sxs-lookup"><span data-stu-id="13d5e-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="13d5e-121">Una instantánea local es una copia de seguridad de todos los datos de volumen almacenados localmente en el dispositivo de hello, mientras que una instantánea de nube hace referencia toohello copia de seguridad de datos del volumen que reside en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="13d5e-122">Las instantáneas locales proporcionan un acceso más rápido, mientras que las instantáneas en la nube son preferibles para la resistencia de los datos.</span><span class="sxs-lookup"><span data-stu-id="13d5e-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="13d5e-123">**Iniciado por** : las copias de seguridad de Hola se pueden iniciar automáticamente una programación o manualmente por el usuario.</span><span class="sxs-lookup"><span data-stu-id="13d5e-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="13d5e-124">Puede utilizar las copias de seguridad de un tooschedule de directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="13d5e-125">Como alternativa, puede usar hello **realizar copia de seguridad** opción tootake una copia de seguridad manual.</span><span class="sxs-lookup"><span data-stu-id="13d5e-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="13d5e-126">Mostrar conjuntos de copia de seguridad para una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="13d5e-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="13d5e-127">Hola completa siguientes pasos se toolist todas las copias de seguridad de Hola para una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-127">Complete hello following steps toolist all hello backups for a backup policy.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="13d5e-128">conjuntos de copia de seguridad de toolist</span><span class="sxs-lookup"><span data-stu-id="13d5e-128">toolist backup sets</span></span>
1. <span data-ttu-id="13d5e-129">Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **catálogo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="13d5e-129">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="13d5e-130">Filtrar las selecciones de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="13d5e-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="13d5e-131">Especifique el intervalo de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-131">Specify hello time range.</span></span>
   2. <span data-ttu-id="13d5e-132">Seleccionar dispositivo apropiados de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-132">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="13d5e-133">Filtrar por **directiva de copia de seguridad** tooview Hola copias de seguridad de hello correspondiente.</span><span class="sxs-lookup"><span data-stu-id="13d5e-133">Filter by **Backup policy** tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="13d5e-134">En lista de desplegable de directiva de copia de seguridad de hello, elija **todos los** tooview todos Hola copias de seguridad en hello seleccionado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="13d5e-134">From hello backup policy dropdown list, choose **All** tooview all hello backups on hello selected device.</span></span>
   4. <span data-ttu-id="13d5e-135">Haga clic en **aplicar** tooexecute esta consulta.</span><span class="sxs-lookup"><span data-stu-id="13d5e-135">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="13d5e-136">copias de seguridad de Hello asociadas con la directiva de copia de seguridad de hello seleccionado deben aparecer en lista de Hola de conjuntos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-136">hello backups associated with hello selected backup policy should appear in hello list of backup sets.</span></span>

      ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="13d5e-138">Seleccionar un conjunto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="13d5e-138">Select a backup set</span></span>
<span data-ttu-id="13d5e-139">Hola completa siguiendo los pasos tooselect una copia de seguridad establecido para una directiva de copia de seguridad o volumen.</span><span class="sxs-lookup"><span data-stu-id="13d5e-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="13d5e-140">tooselect un conjunto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="13d5e-140">tooselect a backup set</span></span>
1. <span data-ttu-id="13d5e-141">Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **catálogo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="13d5e-141">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="13d5e-142">Filtrar las selecciones de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="13d5e-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="13d5e-143">Especifique el intervalo de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-143">Specify hello time range.</span></span> 
   2. <span data-ttu-id="13d5e-144">Seleccionar dispositivo apropiados de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-144">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="13d5e-145">Filtrar por la directiva de copia de seguridad o volumen de copia de seguridad de Hola que desea tooselect.</span><span class="sxs-lookup"><span data-stu-id="13d5e-145">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="13d5e-146">Haga clic en **aplicar** tooexecute esta consulta.</span><span class="sxs-lookup"><span data-stu-id="13d5e-146">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="13d5e-147">Hello deben aparecer copias de seguridad asociadas con la directiva de copia de seguridad o volumen de hello seleccionado en lista de Hola de conjuntos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-147">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="13d5e-149">Selecciona y expanda un conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-149">Select and expand a backup set.</span></span> <span data-ttu-id="13d5e-150">Ahora puede ver conjuntos de copia de seguridad de hello desglosados por volúmenes de Hola que contiene.</span><span class="sxs-lookup"><span data-stu-id="13d5e-150">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="13d5e-151">Hola **restaurar** y **eliminar** opciones están disponibles a través del menú contextual de hello (ratón) para el conjunto de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-151">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="13d5e-152">Puede realizar cualquiera de estas acciones en el conjunto de copia de seguridad de Hola que haya seleccionado.</span><span class="sxs-lookup"><span data-stu-id="13d5e-152">You can perform either of these actions on hello backup set that you selected.</span></span>

    ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="13d5e-154">Eliminación de un conjunto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="13d5e-154">Delete a backup set</span></span>
<span data-ttu-id="13d5e-155">Eliminar una copia de seguridad cuando ya no desea datos de hello tooretain asociados con él.</span><span class="sxs-lookup"><span data-stu-id="13d5e-155">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="13d5e-156">Realizar Hola siguiendo los pasos toodelete un conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-156">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="13d5e-157">toodelete un conjunto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="13d5e-157">toodelete a backup set</span></span>
 <span data-ttu-id="13d5e-158">Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **catálogo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="13d5e-158">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="13d5e-159">Filtrar las selecciones de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="13d5e-159">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="13d5e-160">Especifique el intervalo de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-160">Specify hello time range.</span></span> 
   2. <span data-ttu-id="13d5e-161">Seleccionar dispositivo apropiados de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-161">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="13d5e-162">Filtrar por la directiva de copia de seguridad o volumen de copia de seguridad de Hola que desea tooselect.</span><span class="sxs-lookup"><span data-stu-id="13d5e-162">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="13d5e-163">Haga clic en **aplicar** tooexecute esta consulta.</span><span class="sxs-lookup"><span data-stu-id="13d5e-163">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="13d5e-164">Hello deben aparecer copias de seguridad asociadas con la directiva de copia de seguridad o volumen de hello seleccionado en lista de Hola de conjuntos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-164">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="13d5e-166">Selecciona y expanda un conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="13d5e-166">Select and expand a backup set.</span></span> <span data-ttu-id="13d5e-167">Ahora puede ver conjuntos de copia de seguridad de hello desglosados por volúmenes de Hola que contiene.</span><span class="sxs-lookup"><span data-stu-id="13d5e-167">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="13d5e-168">Hola **restaurar** y **eliminar** opciones están disponibles a través del menú contextual de hello (ratón) para el conjunto de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="13d5e-168">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="13d5e-169">Haga clic en el conjunto de copia de seguridad de hello seleccionado y en el menú contextual de hello, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="13d5e-169">Right-click hello selected backup set and from hello context menu, select **Delete**.</span></span>

    ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="13d5e-171">Cuando se le pida confirmación, revise la información de la muestra de Hola y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="13d5e-171">When prompted for confirmation, review hello displayed information and click **Delete**.</span></span> <span data-ttu-id="13d5e-172">copia de seguridad de Hello seleccionada se eliminará definitivamente.</span><span class="sxs-lookup"><span data-stu-id="13d5e-172">hello selected backup is deleted permanently.</span></span>

    ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="13d5e-174">Se le notificará cuando Hola eliminación está en curso y cuando haya finalizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="13d5e-174">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="13d5e-175">Después de realiza la eliminación de hello, actualizar la consulta de hello en esta página.</span><span class="sxs-lookup"><span data-stu-id="13d5e-175">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="13d5e-176">conjunto de copia de seguridad de Hello eliminado ya no aparecerá en la lista de Hola de conjuntos de copia de seguridad de.</span><span class="sxs-lookup"><span data-stu-id="13d5e-176">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

    ![Vaya toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="13d5e-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13d5e-178">Next steps</span></span>
* <span data-ttu-id="13d5e-179">Obtenga información acerca de cómo demasiado[uso Hola toorestore de catálogo de copia de seguridad, el dispositivo desde un conjunto de copia de seguridad](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="13d5e-179">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="13d5e-180">Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="13d5e-180">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

