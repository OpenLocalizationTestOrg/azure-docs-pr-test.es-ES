---
title: tutorial de copia de seguridad de Azure StorSimple Virtual Array aaaMicrosoft | Documentos de Microsoft
description: "Describe cómo se comparte tooback de matriz Virtual de StorSimple y volúmenes."
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
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="fad01-103">Copia de seguridad de recursos compartidos o volúmenes de la matriz virtual de StorSimple</span><span class="sxs-lookup"><span data-stu-id="fad01-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="fad01-104">Información general</span><span class="sxs-lookup"><span data-stu-id="fad01-104">Overview</span></span>

<span data-ttu-id="fad01-105">Hola StorSimple Virtual Array es un híbrido en la nube local virtual dispositivo de almacenamiento que se pueden configurar como un servidor de archivos o un servidor de iSCSI.</span><span class="sxs-lookup"><span data-stu-id="fad01-105">hello StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="fad01-106">matriz virtual Hola permite a Hola usuario toocreate copias de seguridad programadas y manuales de todos los recursos compartidos de Hola o volúmenes en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fad01-106">hello virtual array allows hello user toocreate scheduled and manual backups of all hello shares or volumes on hello device.</span></span> <span data-ttu-id="fad01-107">Cuando se configura como servidor de archivos, también permite la recuperación a nivel de elemento.</span><span class="sxs-lookup"><span data-stu-id="fad01-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="fad01-108">Este tutorial describe cómo programar toocreate y copias de seguridad manuales y realizar la recuperación de nivel de elemento toorestore un archivo eliminado en la matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="fad01-108">This tutorial describes how toocreate scheduled and manual backups and perform item-level recovery toorestore a deleted file on your virtual array.</span></span>

<span data-ttu-id="fad01-109">Este tutorial aplica toohello StorSimple Virtual sólo arreglos de discos.</span><span class="sxs-lookup"><span data-stu-id="fad01-109">This tutorial applies toohello StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="fad01-110">Para obtener información sobre la 8000 serie, vaya demasiado[crear una copia de seguridad de dispositivo de la 8000 serie](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="fad01-110">For information on 8000 series, go too[Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="fad01-111">Crear copias de seguridad de los recursos compartidos y volúmenes</span><span class="sxs-lookup"><span data-stu-id="fad01-111">Back up shares and volumes</span></span>

<span data-ttu-id="fad01-112">Las copias de seguridad proporcionan seguridad a partir de un momento específico y mejoran la capacidad de recuperación, al mismo tiempo que reducen los tiempos de restauración de recursos compartidos y volúmenes.</span><span class="sxs-lookup"><span data-stu-id="fad01-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="fad01-113">Puede hacer una copia de seguridad de un recurso compartido o de un volumen de su dispositivo StorSimple de dos maneras: **Programada** o **Manual**.</span><span class="sxs-lookup"><span data-stu-id="fad01-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="fad01-114">Cada uno de los métodos de Hola se describe en las secciones siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="fad01-114">Each of hello methods is discussed in hello following sections.</span></span>

## <a name="change-hello-backup-start-time"></a><span data-ttu-id="fad01-115">Cambiar la hora de inicio de copia de seguridad de Hola</span><span class="sxs-lookup"><span data-stu-id="fad01-115">Change hello backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="fad01-116">En esta versión, se crean copias de seguridad programadas por una directiva predeterminada que se ejecuta diariamente a una hora especificada y copia todos los recursos compartidos de Hola o volúmenes en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fad01-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all hello shares or volumes on hello device.</span></span> <span data-ttu-id="fad01-117">No es posible toocreate directivas personalizadas de copias de seguridad programadas en este momento.</span><span class="sxs-lookup"><span data-stu-id="fad01-117">It is not possible toocreate custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="fad01-118">La matriz Virtual de StorSimple tiene una directiva de copia de seguridad predeterminada que se inicia en un momento determinado del día (22:30) y realiza una copia de todos los recursos compartidos de Hola o volúmenes en el dispositivo de hello una vez al día.</span><span class="sxs-lookup"><span data-stu-id="fad01-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all hello shares or volumes on hello device once a day.</span></span> <span data-ttu-id="fad01-119">Puede cambiar el tiempo de hello en qué copia de seguridad empieza a hello, pero hello y frecuencia de hello retención (que especifica el número de Hola de copias de seguridad tooretain) no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="fad01-119">You can change hello time at which hello backup starts, but hello frequency and hello retention (which specifies hello number of backups tooretain) cannot be changed.</span></span> <span data-ttu-id="fad01-120">Durante estas copias de seguridad, dispositivo virtual completa de Hola se copia.</span><span class="sxs-lookup"><span data-stu-id="fad01-120">During these backups, hello entire virtual device is backed up.</span></span> <span data-ttu-id="fad01-121">Potencialmente Esto podría afectar al rendimiento de hello de dispositivo de Hola y afectan a las cargas de trabajo de hello implementadas en dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fad01-121">This could potentially impact hello performance of hello device and affect hello workloads deployed on hello device.</span></span> <span data-ttu-id="fad01-122">Por lo tanto, es aconsejable que programe que las copias de seguridad se realicen en horas de poca actividad.</span><span class="sxs-lookup"><span data-stu-id="fad01-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="fad01-123">copia de seguridad predeterminada de toochange Hola hora de inicio, siga Hola siguiendo los pasos de hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fad01-123">toochange hello default backup start time, perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a><span data-ttu-id="fad01-124">Hola toochange hora de inicio de directiva de copia de seguridad de hello predeterminada</span><span class="sxs-lookup"><span data-stu-id="fad01-124">toochange hello start time for hello default backup policy</span></span>

1. <span data-ttu-id="fad01-125">Vaya demasiado**dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="fad01-125">Go too**Devices**.</span></span> <span data-ttu-id="fad01-126">se mostrará la lista de Hola de dispositivos registrados con el servicio de administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="fad01-126">hello list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![Navegue toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="fad01-128">Seleccione y haga clic en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fad01-128">Select and click your device.</span></span> <span data-ttu-id="fad01-129">Hola **configuración** hoja se mostrarán.</span><span class="sxs-lookup"><span data-stu-id="fad01-129">hello **Settings** blade will be displayed.</span></span> <span data-ttu-id="fad01-130">Vaya demasiado**administrar > directivas de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="fad01-130">Go too**Manage > Backup policies**.</span></span>
   
    ![seleccionar un dispositivo](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="fad01-132">Hola **directivas de copia de seguridad** hoja, hora de inicio de hello predeterminada es 22:30.</span><span class="sxs-lookup"><span data-stu-id="fad01-132">In hello **Backup policies** blade, hello default start time is 22:30.</span></span> <span data-ttu-id="fad01-133">Puede especificar la nueva hora de inicio Hola para programación diaria de hello en la zona horaria del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fad01-133">You can specify hello new start time for hello daily schedule in device time zone.</span></span>
   
    ![navegar por las directivas de toobackup](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="fad01-135">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fad01-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="fad01-136">Creación de una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="fad01-136">Take a manual backup</span></span>

<span data-ttu-id="fad01-137">Además tooscheduled copias de seguridad, puede realizar una copia de seguridad manual (a petición) de los datos del dispositivo en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="fad01-137">In addition tooscheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="fad01-138">toocreate una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="fad01-138">toocreate a manual backup</span></span>

1. <span data-ttu-id="fad01-139">Vaya demasiado**dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="fad01-139">Go too**Devices**.</span></span> <span data-ttu-id="fad01-140">Seleccione el dispositivo y haga clic en **...**  en hello más a la derecha de la fila seleccionada de Hola.</span><span class="sxs-lookup"><span data-stu-id="fad01-140">Select your device and right-click **...** at hello far right in hello selected row.</span></span> <span data-ttu-id="fad01-141">En el menú contextual de hello, seleccione **realizar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="fad01-141">From hello context menu, select **Take backup**.</span></span>
   
    ![navegar por la copia de seguridad de tootake](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="fad01-143">Hola **realizar copia de seguridad** hoja, haga clic en **realizar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="fad01-143">In hello **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="fad01-144">Todos los recursos compartidos de hello en el servidor de archivos de Hola o todos los volúmenes de hello en el servidor de iSCSI realizará copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fad01-144">This will backup all hello shares on hello file server or all hello volumes on your iSCSI server.</span></span> 
   
    ![inicio de la copia de seguridad](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="fad01-146">Se inicia una copia de seguridad a petición y verá que se ha iniciado un trabajo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fad01-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![inicio de la copia de seguridad](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="fad01-148">Una vez que se haya completado correctamente el trabajo de hello, se le notificará de nuevo.</span><span class="sxs-lookup"><span data-stu-id="fad01-148">Once hello job has successfully completed, you are notified again.</span></span> <span data-ttu-id="fad01-149">a continuación, inicia el proceso de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="fad01-149">hello backup process then starts.</span></span>
   
    ![trabajo de copia de seguridad creado](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="fad01-151">progreso de hello tootrack de copias de seguridad de Hola y busque en detalles del trabajo hello, haga clic en la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="fad01-151">tootrack hello progress of hello backups and look at hello job details, click hello notification.</span></span> <span data-ttu-id="fad01-152">Esto le llevará demasiado **detalles del trabajo**.</span><span class="sxs-lookup"><span data-stu-id="fad01-152">This takes you too **Job details**.</span></span>
   
     ![detalles del trabajo de copia de seguridad](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="fad01-154">Una vez completada la copia de seguridad de hello, vaya demasiado**Administración > catálogo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="fad01-154">After hello backup is complete, go too**Management > Backup catalog**.</span></span> <span data-ttu-id="fad01-155">Verá una instantánea en la nube de todos los recursos compartidos de hello (o volúmenes) en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fad01-155">You will see a cloud snapshot of all hello shares (or volumes) on your device.</span></span>
   
    ![Copia de seguridad completada](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="fad01-157">Ver copias de seguridad existentes</span><span class="sxs-lookup"><span data-stu-id="fad01-157">View existing backups</span></span>
<span data-ttu-id="fad01-158">copias de seguridad existentes de tooview hello, realizar Hola pasos de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fad01-158">tooview hello existing backups, perform hello following steps in hello Azure portal.</span></span>

#### <a name="tooview-existing-backups"></a><span data-ttu-id="fad01-159">tooview copias de seguridad existentes</span><span class="sxs-lookup"><span data-stu-id="fad01-159">tooview existing backups</span></span>

1. <span data-ttu-id="fad01-160">Vaya demasiado**dispositivos** hoja.</span><span class="sxs-lookup"><span data-stu-id="fad01-160">Go too**Devices** blade.</span></span> <span data-ttu-id="fad01-161">Seleccione y haga clic en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fad01-161">Select and click your device.</span></span> <span data-ttu-id="fad01-162">Hola **configuración** hoja, vaya demasiado**Administración > catálogo de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="fad01-162">In hello **Settings** blade, go too**Management > Backup Catalog**.</span></span>
   
    ![Navegar por catálogo toobackup](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="fad01-164">Especifique Hola después toobe criterios usado para filtrar:</span><span class="sxs-lookup"><span data-stu-id="fad01-164">Specify hello following criteria toobe used for filtering:</span></span>
   
    - <span data-ttu-id="fad01-165">**Intervalo de tiempo**: puede ser **Última hora**, **Últimas 24 horas**, **Últimos 7 días**, **Últimos 30 días**, **Último año** y **Fecha personalizada**.</span><span class="sxs-lookup"><span data-stu-id="fad01-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="fad01-166">**Dispositivos** : seleccione en lista de Hola de servidores de archivos o servidores iSCSI registrados con el servicio de administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="fad01-166">**Devices** – select from hello list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="fad01-167">**Iniciado**: pueden ser **programados** automáticamente (por una directiva de copia de seguridad) o iniciados **manualmente** (por usted).</span><span class="sxs-lookup"><span data-stu-id="fad01-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Filtrar copias de seguridad](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="fad01-169">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="fad01-169">Click **Apply**.</span></span> <span data-ttu-id="fad01-170">Hello lista filtrada de las copias de seguridad aparece en hello **catálogo de copia de seguridad** hoja.</span><span class="sxs-lookup"><span data-stu-id="fad01-170">hello filtered list of backups is displayed in hello **Backup catalog** blade.</span></span> <span data-ttu-id="fad01-171">Tenga en cuenta que no se pueden mostrar más de cien elementos de copia de seguridad en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="fad01-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Catálogo de copias de seguridad actualizado](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="fad01-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fad01-173">Next steps</span></span>

<span data-ttu-id="fad01-174">Obtenga más información sobre la [administración de la matriz virtual de StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="fad01-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

