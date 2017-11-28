---
title: "Administración del catálogo de copias de seguridad de StorSimple | Microsoft Docs"
description: "Explica cómo usar la página del catálogo de copias de seguridad del servicio StorSimple Device Manager para enumerar, seleccionar y eliminar conjuntos de copias de seguridad."
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
ms.openlocfilehash: ac2577c6cd350d6d437d55e61ec73d954cb24893
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="9c1f7-103">Uso del servicio StorSimple Device Manager para administrar su catálogo de copias de seguridad</span><span class="sxs-lookup"><span data-stu-id="9c1f7-103">Use the StorSimple Device Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="9c1f7-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9c1f7-104">Overview</span></span>
<span data-ttu-id="9c1f7-105">En la hoja **Catálogo de copias de seguridad** del servicio StorSimple Device Manager se muestran todos los conjuntos de copia de seguridad que se crean cuando se realizan copias de seguridad manuales o programadas.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-105">The StorSimple Device Manager service **Backup Catalog** blade displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="9c1f7-106">Puede usar esta página para enumerar todas las copias de seguridad para un volumen o una directiva de copia de seguridad, seleccionar o eliminar las copias de seguridad, o usar una copia de seguridad para restaurar o clonar un volumen.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="9c1f7-107">En este tutorial se explica cómo enumerar, seleccionar y eliminar un conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="9c1f7-108">Para obtener información sobre cómo restaurar su dispositivo de copia de seguridad, vaya a [Restaurar el dispositivo desde un conjunto de copia de seguridad](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="9c1f7-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="9c1f7-109">Para aprender cómo clonar un volumen, vaya a [Clonar un volumen de StorSimple](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="9c1f7-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Catálogo de Backup](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="9c1f7-111">La hoja **Catálogo de copias de seguridad** proporciona una consulta para restringir la selección de conjuntos de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-111">The **Backup Catalog** blade provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="9c1f7-112">Puede filtrar los conjuntos de copias de seguridad que se recuperan en función de los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="9c1f7-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="9c1f7-113">**Dispositivo** : dispositivo en el que se creó el conjunto de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="9c1f7-114">**Directiva de copia de seguridad o volumen**: directiva de copia de seguridad o volumen asociado a este conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-114">**Backup policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="9c1f7-115">**De y A** : el intervalo de fecha y hora en el que se creó el conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="9c1f7-116">A continuación, los conjuntos de copias de seguridad filtrados se presentan en forma de tabla en función de los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="9c1f7-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="9c1f7-117">**Nombre** : nombre de la directiva de copias de seguridad o del volumen asociado al conjunto de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="9c1f7-118">**Tamaño** : tamaño real del conjunto de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="9c1f7-119">**Creada en** : Fecha y hora en que se crearon las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="9c1f7-120">**Tipo** : los conjuntos de copias de seguridad pueden ser instantáneas locales o instantáneas en la nube.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="9c1f7-121">Una instantánea local es una copia de seguridad de todos los datos del volumen que se almacenan localmente en el dispositivo, mientras que una instantánea en la nube hace referencia a la copia de seguridad de los datos del volumen que residen en la nube.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="9c1f7-122">Las instantáneas locales proporcionan un acceso más rápido, mientras que las instantáneas en la nube son preferibles para la resistencia de los datos.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="9c1f7-123">**Iniciada por** : las copias de seguridad se pueden iniciar automáticamente por una programación o manualmente por el usuario.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="9c1f7-124">Puede usar una directiva de copia de seguridad para programar copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="9c1f7-125">Como alternativa, puede usar la opción **Realizar copia de seguridad** para crear una copia de seguridad manual.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="9c1f7-126">Mostrar conjuntos de copia de seguridad para una directiva de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9c1f7-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="9c1f7-127">Complete los pasos siguientes para enumerar todas las copias de seguridad para una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-127">Complete the following steps to list all the backups for a backup policy.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="9c1f7-128">Para enumerar los conjuntos de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9c1f7-128">To list backup sets</span></span>
1. <span data-ttu-id="9c1f7-129">Vaya al servicio StorSimple Device Manager y haga clic en **Catálogo de copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-129">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="9c1f7-130">Filtre las selecciones de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="9c1f7-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="9c1f7-131">Especifique el intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-131">Specify the time range.</span></span>
   2. <span data-ttu-id="9c1f7-132">Seleccione el dispositivo adecuado.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-132">Select the appropriate device.</span></span>
   3. <span data-ttu-id="9c1f7-133">Filtre por **Directiva de copia de seguridad** para ver las copias de seguridad correspondientes.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-133">Filter by **Backup policy** to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="9c1f7-134">En la lista desplegable de directivas de copia de seguridad, elija **Todas** para ver todas las copias de seguridad del dispositivo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-134">From the backup policy dropdown list, choose **All** to view all the backups on the selected device.</span></span>
   4. <span data-ttu-id="9c1f7-135">Haga clic en **Aplicar** para ejecutar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-135">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="9c1f7-136">Las copias de seguridad asociadas a la directiva de copia de seguridad seleccionada deben aparecer en la lista de conjuntos de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-136">The backups associated with the selected backup policy should appear in the list of backup sets.</span></span>

      ![Ir al catálogo de copia de seguridad](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="9c1f7-138">Seleccionar un conjunto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9c1f7-138">Select a backup set</span></span>
<span data-ttu-id="9c1f7-139">Complete los pasos siguientes para seleccionar un conjunto de copias de seguridad para un volumen o una directiva de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="9c1f7-140">Para seleccionar un conjunto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9c1f7-140">To select a backup set</span></span>
1. <span data-ttu-id="9c1f7-141">Vaya al servicio StorSimple Device Manager y haga clic en **Catálogo de copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-141">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="9c1f7-142">Filtre las selecciones de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="9c1f7-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="9c1f7-143">Especifique el intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-143">Specify the time range.</span></span> 
   2. <span data-ttu-id="9c1f7-144">Seleccione el dispositivo adecuado.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-144">Select the appropriate device.</span></span> 
   3. <span data-ttu-id="9c1f7-145">Filtre por el volumen o la directiva de copia de seguridad para la copia de seguridad que desea seleccionar.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-145">Filter by volume or backup policy for the backup that you wish to select.</span></span>
   4. <span data-ttu-id="9c1f7-146">Haga clic en **Aplicar** para ejecutar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-146">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="9c1f7-147">Las copias de seguridad asociadas al volumen o la directiva de copia de seguridad seleccionados deben aparecer en la lista de conjuntos de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-147">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>

      ![Ir al catálogo de copia de seguridad](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="9c1f7-149">Selecciona y expanda un conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-149">Select and expand a backup set.</span></span> <span data-ttu-id="9c1f7-150">Ahora ya puede ver los conjuntos de copia de seguridad desglosados por los volúmenes que contienen.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-150">You can now see the backup sets broken down by the volumes that it contains.</span></span> <span data-ttu-id="9c1f7-151">Las opciones **Restaurar** y **Eliminar** están disponibles mediante el menú contextual (haga clic con el botón derecho) del conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-151">The **Restore** and **Delete** options are available via the context menu (right-click) for the backup set.</span></span> <span data-ttu-id="9c1f7-152">Puede realizar cualquiera de estas acciones en el conjunto de copia de seguridad que haya seleccionado.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-152">You can perform either of these actions on the backup set that you selected.</span></span>

    ![Ir al catálogo de copia de seguridad](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="9c1f7-154">Eliminación de un conjunto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9c1f7-154">Delete a backup set</span></span>
<span data-ttu-id="9c1f7-155">Elimine una copia de seguridad cuando ya no desee conservar los datos asociados a ella.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-155">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="9c1f7-156">Realice los siguientes pasos para eliminar un conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-156">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="9c1f7-157">Para eliminar un conjunto de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="9c1f7-157">To delete a backup set</span></span>
 <span data-ttu-id="9c1f7-158">Vaya al servicio StorSimple Device Manager y haga clic en **Catálogo de copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-158">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="9c1f7-159">Filtre las selecciones de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="9c1f7-159">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="9c1f7-160">Especifique el intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-160">Specify the time range.</span></span> 
   2. <span data-ttu-id="9c1f7-161">Seleccione el dispositivo adecuado.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-161">Select the appropriate device.</span></span> 
   3. <span data-ttu-id="9c1f7-162">Filtre por el volumen o la directiva de copia de seguridad para la copia de seguridad que desea seleccionar.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-162">Filter by volume or backup policy for the backup that you wish to select.</span></span>
   4. <span data-ttu-id="9c1f7-163">Haga clic en **Aplicar** para ejecutar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-163">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="9c1f7-164">Las copias de seguridad asociadas al volumen o la directiva de copia de seguridad seleccionados deben aparecer en la lista de conjuntos de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-164">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>

      ![Ir al catálogo de copia de seguridad](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="9c1f7-166">Selecciona y expanda un conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-166">Select and expand a backup set.</span></span> <span data-ttu-id="9c1f7-167">Ahora ya puede ver los conjuntos de copia de seguridad desglosados por los volúmenes que contienen.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-167">You can now see the backup sets broken down by the volumes that it contains.</span></span> <span data-ttu-id="9c1f7-168">Las opciones **Restaurar** y **Eliminar** están disponibles mediante el menú contextual (haga clic con el botón derecho) del conjunto de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-168">The **Restore** and **Delete** options are available via the context menu (right-click) for the backup set.</span></span> <span data-ttu-id="9c1f7-169">Haga clic con el botón derecho en el conjunto de copia de seguridad seleccionado y, en el menú contextual, seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-169">Right-click the selected backup set and from the context menu, select **Delete**.</span></span>

    ![Ir al catálogo de copia de seguridad](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="9c1f7-171">Cuando se le pida confirmación, revise la información que aparece y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-171">When prompted for confirmation, review the displayed information and click **Delete**.</span></span> <span data-ttu-id="9c1f7-172">La copia de seguridad seleccionada se eliminará definitivamente.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-172">The selected backup is deleted permanently.</span></span>

    ![Ir al catálogo de copia de seguridad](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="9c1f7-174">Se le notificará cuando la eliminación esté en curso y cuando haya finalizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-174">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="9c1f7-175">Cuando finalice la eliminación, actualice la consulta en esta página.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-175">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="9c1f7-176">El conjunto de copia de seguridad eliminado ya no aparecerá en la lista de conjuntos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9c1f7-176">The deleted backup set will no longer appear in the list of backup sets.</span></span>

    ![Ir al catálogo de copia de seguridad](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="9c1f7-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c1f7-178">Next steps</span></span>
* <span data-ttu-id="9c1f7-179">Obtenga información sobre cómo usar el catálogo de copias de seguridad para [restaurar el dispositivo desde un conjunto de copias de seguridad](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="9c1f7-179">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="9c1f7-180">Aprenda a [usar el servicio StorSimple Device Manager para administrar el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="9c1f7-180">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

