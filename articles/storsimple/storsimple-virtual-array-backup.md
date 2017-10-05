---
title: Tutorial de copia de seguridad de Microsoft Azure StorSimple Virtual Array | Microsoft Docs
description: "Describe cómo realizar copias de seguridad de recursos compartidos y volúmenes de la matriz virtual de StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c926f0c80ce56cac3106ad97ec3ec2e18a8e2cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="1ce13-103">Copia de seguridad de recursos compartidos o volúmenes de la matriz virtual de StorSimple</span><span class="sxs-lookup"><span data-stu-id="1ce13-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="1ce13-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1ce13-104">Overview</span></span>

<span data-ttu-id="1ce13-105">La matriz virtual de StorSimple es un dispositivo virtual local de almacenamiento en nube híbrida que se puede configurar como servidor de archivos o servidor iSCSI.</span><span class="sxs-lookup"><span data-stu-id="1ce13-105">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="1ce13-106">La matriz virtual permite al usuario crear copias de seguridad programadas y manuales de todos los recursos compartidos o volúmenes del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1ce13-106">The virtual array allows the user to create scheduled and manual backups of all the shares or volumes on the device.</span></span> <span data-ttu-id="1ce13-107">Cuando se configura como servidor de archivos, también permite la recuperación a nivel de elemento.</span><span class="sxs-lookup"><span data-stu-id="1ce13-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="1ce13-108">Este tutorial describe cómo crear copias de seguridad programadas y manuales, y realizar la recuperación a nivel de elemento para restaurar un archivo eliminado en una matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="1ce13-108">This tutorial describes how to create scheduled and manual backups and perform item-level recovery to restore a deleted file on your virtual array.</span></span>

<span data-ttu-id="1ce13-109">Este tutorial se aplica solo a instancias de StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="1ce13-109">This tutorial applies to the StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="1ce13-110">Para obtener información sobre la serie 8000, vaya a [Creación de una copia de seguridad de un dispositivo de la serie 8000](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="1ce13-110">For information on 8000 series, go to [Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="1ce13-111">Crear copias de seguridad de los recursos compartidos y volúmenes</span><span class="sxs-lookup"><span data-stu-id="1ce13-111">Back up shares and volumes</span></span>

<span data-ttu-id="1ce13-112">Las copias de seguridad proporcionan seguridad a partir de un momento específico y mejoran la capacidad de recuperación, al mismo tiempo que reducen los tiempos de restauración de recursos compartidos y volúmenes.</span><span class="sxs-lookup"><span data-stu-id="1ce13-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="1ce13-113">Puede hacer una copia de seguridad de un recurso compartido o de un volumen de su dispositivo StorSimple de dos maneras: **Programada** o **Manual**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="1ce13-114">En las siguientes secciones se detallan cada uno de los métodos.</span><span class="sxs-lookup"><span data-stu-id="1ce13-114">Each of the methods is discussed in the following sections.</span></span>

## <a name="change-the-backup-start-time"></a><span data-ttu-id="1ce13-115">Cambio de la hora de inicio de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="1ce13-115">Change the backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="1ce13-116">En esta versión, se crean copias de seguridad programadas mediante una directiva predeterminada que se ejecuta diariamente a la hora especificada y hace una copia de seguridad de todos los recursos compartidos o volúmenes en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1ce13-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span></span> <span data-ttu-id="1ce13-117">No es posible crear directivas personalizadas para copias de seguridad programadas en este momento.</span><span class="sxs-lookup"><span data-stu-id="1ce13-117">It is not possible to create custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="1ce13-118">StorSimple Virtual Array tiene una directiva de copia de seguridad predeterminada que se inicia a una hora determinada del día (22:30) y hace una copia de seguridad de todos los recursos compartidos o volúmenes del dispositivo una vez al día.</span><span class="sxs-lookup"><span data-stu-id="1ce13-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span></span> <span data-ttu-id="1ce13-119">Puede cambiar la hora a la que se inicia la copia de seguridad, pero no puede cambiar la frecuencia y la retención (que especifica el número de copias de seguridad para conservar).</span><span class="sxs-lookup"><span data-stu-id="1ce13-119">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span></span> <span data-ttu-id="1ce13-120">En estas copias de seguridad, se copia todo el dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="1ce13-120">During these backups, the entire virtual device is backed up.</span></span> <span data-ttu-id="1ce13-121">Esto puede afectar potencialmente al rendimiento del dispositivo y a las cargas de trabajo implementadas en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1ce13-121">This could potentially impact the performance of the device and affect the workloads deployed on the device.</span></span> <span data-ttu-id="1ce13-122">Por lo tanto, es aconsejable que programe que las copias de seguridad se realicen en horas de poca actividad.</span><span class="sxs-lookup"><span data-stu-id="1ce13-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="1ce13-123">Para cambiar la hora de inicio predeterminada de las copias de seguridad, siga estos pasos en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1ce13-123">To change the default backup start time, perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-change-the-start-time-for-the-default-backup-policy"></a><span data-ttu-id="1ce13-124">Para cambiar la hora de inicio para la directiva de copia de seguridad predeterminada</span><span class="sxs-lookup"><span data-stu-id="1ce13-124">To change the start time for the default backup policy</span></span>

1. <span data-ttu-id="1ce13-125">Vaya a **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-125">Go to **Devices**.</span></span> <span data-ttu-id="1ce13-126">Se mostrará la lista de dispositivos registrados en el servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="1ce13-126">The list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![navegar a dispositivos](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="1ce13-128">Seleccione y haga clic en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1ce13-128">Select and click your device.</span></span> <span data-ttu-id="1ce13-129">Se mostrará la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-129">The **Settings** blade will be displayed.</span></span> <span data-ttu-id="1ce13-130">Vaya a **Administrar > Directivas de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-130">Go to **Manage > Backup policies**.</span></span>
   
    ![seleccionar un dispositivo](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="1ce13-132">En la hoja **Directivas de copia de seguridad**, la hora de inicio predeterminada es 22:30.</span><span class="sxs-lookup"><span data-stu-id="1ce13-132">In the **Backup policies** blade, the default start time is 22:30.</span></span> <span data-ttu-id="1ce13-133">La nueva hora de inicio de la programación diaria se puede especificar en la zona horaria del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1ce13-133">You can specify the new start time for the daily schedule in device time zone.</span></span>
   
    ![navegar a las directivas de copia de seguridad](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="1ce13-135">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="1ce13-136">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="1ce13-136">Take a manual backup</span></span>

<span data-ttu-id="1ce13-137">Además de las copias de seguridad programadas, es posible realizar una copia de seguridad manual (a petición) del dispositivo en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="1ce13-137">In addition to scheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="1ce13-138">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="1ce13-138">To create a manual backup</span></span>

1. <span data-ttu-id="1ce13-139">Vaya a **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-139">Go to **Devices**.</span></span> <span data-ttu-id="1ce13-140">Seleccione el dispositivo y haga clic con el botón derecho en **...** en el extremo derecho de la fila seleccionada.</span><span class="sxs-lookup"><span data-stu-id="1ce13-140">Select your device and right-click **...** at the far right in the selected row.</span></span> <span data-ttu-id="1ce13-141">En el menú contextual, seleccione **Hacer copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-141">From the context menu, select **Take backup**.</span></span>
   
    ![navegar para realizar copias de seguridad](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="1ce13-143">En la hoja **Hacer copia de seguridad**, haga clic en **Hacer copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-143">In the **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="1ce13-144">Así se realizará una copia de seguridad de todos los recursos compartidos del servidor de archivos o de todos los volúmenes de un servidor iSCSI.</span><span class="sxs-lookup"><span data-stu-id="1ce13-144">This will backup all the shares on the file server or all the volumes on your iSCSI server.</span></span> 
   
    ![inicio de la copia de seguridad](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="1ce13-146">Se inicia una copia de seguridad a petición y verá que se ha iniciado un trabajo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="1ce13-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![inicio de la copia de seguridad](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="1ce13-148">Una vez que el trabajo se haya completado correctamente, volverá a recibir una notificación.</span><span class="sxs-lookup"><span data-stu-id="1ce13-148">Once the job has successfully completed, you are notified again.</span></span> <span data-ttu-id="1ce13-149">Después, se inicia el proceso de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="1ce13-149">The backup process then starts.</span></span>
   
    ![trabajo de copia de seguridad creado](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="1ce13-151">Para realizar un seguimiento del progreso de las copias de seguridad y examinar los detalles del trabajo, haga clic en la notificación.</span><span class="sxs-lookup"><span data-stu-id="1ce13-151">To track the progress of the backups and look at the job details, click the notification.</span></span> <span data-ttu-id="1ce13-152">Esto le llevará a **Detalles del trabajo**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-152">This takes you to  **Job details**.</span></span>
   
     ![detalles del trabajo de copia de seguridad](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="1ce13-154">Una vez que se haya completado la copia de seguridad, vaya a **Administración > Catálogo de copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-154">After the backup is complete, go to **Management > Backup catalog**.</span></span> <span data-ttu-id="1ce13-155">Verá una instantánea en la nube de todos los recursos compartidos (o volúmenes) del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1ce13-155">You will see a cloud snapshot of all the shares (or volumes) on your device.</span></span>
   
    ![Copia de seguridad completada](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="1ce13-157">Ver copias de seguridad existentes</span><span class="sxs-lookup"><span data-stu-id="1ce13-157">View existing backups</span></span>
<span data-ttu-id="1ce13-158">Para ver las copias de seguridad existentes, siga estos pasos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1ce13-158">To view the existing backups, perform the following steps in the Azure portal.</span></span>

#### <a name="to-view-existing-backups"></a><span data-ttu-id="1ce13-159">Para ver copias de seguridad existentes</span><span class="sxs-lookup"><span data-stu-id="1ce13-159">To view existing backups</span></span>

1. <span data-ttu-id="1ce13-160">Vaya a la hoja **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-160">Go to **Devices** blade.</span></span> <span data-ttu-id="1ce13-161">Seleccione y haga clic en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1ce13-161">Select and click your device.</span></span> <span data-ttu-id="1ce13-162">En la hoja **Configuración**, vaya a **Administración > Catálogo de copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-162">In the **Settings** blade, go to **Management > Backup Catalog**.</span></span>
   
    ![Navegar al catálogo de copias de seguridad](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="1ce13-164">Especifique los criterios siguientes que se van a usar para los filtros:</span><span class="sxs-lookup"><span data-stu-id="1ce13-164">Specify the following criteria to be used for filtering:</span></span>
   
    - <span data-ttu-id="1ce13-165">**Intervalo de tiempo**: puede ser **Última hora**, **Últimas 24 horas**, **Últimos 7 días**, **Últimos 30 días**, **Último año** y **Fecha personalizada**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="1ce13-166">**Dispositivos**: selecciónelos en la lista de servidores de archivos o servidores iSCSI registrados en el servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="1ce13-166">**Devices** – select from the list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="1ce13-167">**Iniciado**: pueden ser **programados** automáticamente (por una directiva de copia de seguridad) o iniciados **manualmente** (por usted).</span><span class="sxs-lookup"><span data-stu-id="1ce13-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Filtrar copias de seguridad](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="1ce13-169">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-169">Click **Apply**.</span></span> <span data-ttu-id="1ce13-170">La lista filtrada de las copias de seguridad se muestra en la hoja **Catálogo de copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="1ce13-170">The filtered list of backups is displayed in the **Backup catalog** blade.</span></span> <span data-ttu-id="1ce13-171">Tenga en cuenta que no se pueden mostrar más de cien elementos de copia de seguridad en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="1ce13-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Catálogo de copias de seguridad actualizado](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="1ce13-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ce13-173">Next steps</span></span>

<span data-ttu-id="1ce13-174">Obtenga más información sobre la [administración de la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="1ce13-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

