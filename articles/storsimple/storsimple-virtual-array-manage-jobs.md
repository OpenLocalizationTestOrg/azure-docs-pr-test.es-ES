---
title: aaaView y administrar los trabajos de StorSimple Virtual Array | Documentos de Microsoft
description: "Describe la página de trabajos de servicio de administrador de dispositivos de StorSimple de Hola y cómo toouse se tootrack trabajos actuales y recientes de hello StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a><span data-ttu-id="7c478-103">Utilice trabajos de tooview de servicio de administrador de dispositivos de StorSimple de Hola para hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="7c478-103">Use hello StorSimple Device Manager service tooview jobs for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="7c478-104">Información general</span><span class="sxs-lookup"><span data-stu-id="7c478-104">Overview</span></span>
<span data-ttu-id="7c478-105">Hola **trabajos** hoja proporciona un solo portal central para ver y administrar trabajos que se inician en arreglos de discos virtuales que están conectado tooyour servicio de administrador de dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7c478-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="7c478-106">Puede ver los trabajos en ejecución, finalizados y con error de varios dispositivos virtuales.</span><span class="sxs-lookup"><span data-stu-id="7c478-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="7c478-107">Los resultados se presentan en un formato tabular.</span><span class="sxs-lookup"><span data-stu-id="7c478-107">Results are presented in a tabular format.</span></span>

![Hoja de trabajos](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="7c478-109">Puede buscar rápidamente los trabajos de Hola que le interesan filtrando en los campos, como:</span><span class="sxs-lookup"><span data-stu-id="7c478-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="7c478-110">**El intervalo de tiempo** – trabajos pueden ser el intervalo de fecha y hora de hello en función de filtrado.</span><span class="sxs-lookup"><span data-stu-id="7c478-110">**Time range** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="7c478-111">**Dispositivos** – trabajos se inician en un servicio de tooyour dispositivo conectado.</span><span class="sxs-lookup"><span data-stu-id="7c478-111">**Devices** – Jobs are initiated on a specific device connected tooyour service.</span></span> <span data-ttu-id="7c478-112">Hello trabajos filtrados se tabulan en función de hello siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="7c478-112">hello filtered jobs are then tabulated based on hello following attributes:</span></span>
  
  * <span data-ttu-id="7c478-113">**Nombre** : puede ser el nombre del trabajo de hello **todos los**, **copia de seguridad**, **clon**, **una conmutación por error**, **descargar actualizaciones** , o **instalar actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="7c478-113">**Name** – hello job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="7c478-114">**Estado**: los trabajos pueden **Todos**, **En curso**, **Correcto**, **Error** o **Cancelado**.</span><span class="sxs-lookup"><span data-stu-id="7c478-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="7c478-115">**Entidad** : Hola trabajos se pueden asociar con un volumen, un recurso compartido o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7c478-115">**Entity** – hello jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="7c478-116">**Dispositivo** : hello nombre de dispositivo de hello en qué Hola se inició el trabajo.</span><span class="sxs-lookup"><span data-stu-id="7c478-116">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="7c478-117">**Iniciado en** : tiempo de hello cuando se inició el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c478-117">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="7c478-118">**Duración** : hello duración de en qué trabajo Hola se ejecutó.</span><span class="sxs-lookup"><span data-stu-id="7c478-118">**Duration** – hello duration for on which hello job was run.</span></span>
* <span data-ttu-id="7c478-119">**Estado** : puede buscar todos los trabajos o los trabajos en ejecución, completados o con error.</span><span class="sxs-lookup"><span data-stu-id="7c478-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="7c478-120">**Tipo de trabajo** : tipo de trabajo de hello puede ser la copia de seguridad, restauración all, conmutación por error, descargar las actualizaciones o instalar actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="7c478-120">**Job type** – hello job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="7c478-121">lista de Hola de trabajos se actualiza cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="7c478-121">hello list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="7c478-122">Ver detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="7c478-122">View job details</span></span>
<span data-ttu-id="7c478-123">Realizar Hola pasos tooview Hola detalles de cualquier trabajo siguientes.</span><span class="sxs-lookup"><span data-stu-id="7c478-123">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="7c478-124">Detalles del trabajo tooview</span><span class="sxs-lookup"><span data-stu-id="7c478-124">tooview job details</span></span>
1. <span data-ttu-id="7c478-125">En hello **trabajos** hoja, trabajos de Hola de presentación que está interesado ejecutando una consulta con los filtros correspondientes.</span><span class="sxs-lookup"><span data-stu-id="7c478-125">On hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="7c478-126">Puede buscar los trabajos completados o en ejecución.</span><span class="sxs-lookup"><span data-stu-id="7c478-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="7c478-127">Seleccione un trabajo de la lista tabular de Hola de trabajos.</span><span class="sxs-lookup"><span data-stu-id="7c478-127">Select a job from hello tabular list of jobs.</span></span>
   
    ![Hoja de trabajos](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="7c478-129">En la parte inferior de Hola de página de hello, haga clic en **detalles**.</span><span class="sxs-lookup"><span data-stu-id="7c478-129">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="7c478-130">Hola **detalles** cuadro de diálogo, puede ver el estado, los detalles y las estadísticas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="7c478-130">In hello **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="7c478-131">Hello en la ilustración siguiente se muestra un ejemplo de Hola **detalles del trabajo de copia de seguridad** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c478-131">hello following illustration shows an example of hello **Backup Job Details** dialog box.</span></span>
   
    ![Detalles del trabajo](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a><span data-ttu-id="7c478-133">Errores en el trabajo cuando se pausa la máquina virtual de hello en el hipervisor de Hola</span><span class="sxs-lookup"><span data-stu-id="7c478-133">Job failures when hello virtual machine is paused in hello hypervisor</span></span>
<span data-ttu-id="7c478-134">Cuando un trabajo está en curso en la matriz Virtual de StorSimple y el dispositivo de hello (aprovisionado en el hipervisor de máquina virtual) se detiene durante más de 15 minutos, se produce un error en el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c478-134">When a job is in progress on your StorSimple Virtual Array and hello device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, hello job fails.</span></span> <span data-ttu-id="7c478-135">Esto es debido a tiempo de StorSimple Virtual Array tooyour dejen de estar sincronizado con la hora de Microsoft Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="7c478-135">This is due tooyour StorSimple Virtual Array time being out of sync with hello Microsoft Azure time.</span></span> 

<span data-ttu-id="7c478-136">Verá Hola siguiente error: "la hora del dispositivo no está sincronizada con el tiempo de Microsoft Azure hello en más de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="7c478-136">You will see hello following error: "Your device time is out of sync with hello Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="7c478-137">Asegúrese de que Hola hipervisor y las horas de dispositivo de Hola se sincronizan con un servidor NTP.</span><span class="sxs-lookup"><span data-stu-id="7c478-137">Ensure that hello hypervisor and hello device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="7c478-138">Compruebe que no haya ningún problema de conectividad.</span><span class="sxs-lookup"><span data-stu-id="7c478-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="7c478-139">problemas de conectividad de tootroubleshoot, ejecutar pruebas de diagnóstico de interfaz de usuario del dispositivo virtual de web local de hello."</span><span class="sxs-lookup"><span data-stu-id="7c478-139">tootroubleshoot connectivity issues, run diagnostic tests from hello local web UI of your virtual device."</span></span>

<span data-ttu-id="7c478-140">Estos errores aplican trabajos toobackup, restauración, actualización y conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="7c478-140">These failures apply toobackup, restore, update, and failover jobs.</span></span> <span data-ttu-id="7c478-141">Si la máquina virtual se aprovisiona en Hyper-V, máquina Hola sincroniza finalmente tiempo con el hipervisor.</span><span class="sxs-lookup"><span data-stu-id="7c478-141">If your virtual machine is provisioned in Hyper-V, hello machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="7c478-142">Cuando esto ocurra, puede reiniciar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="7c478-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c478-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c478-143">Next steps</span></span>
<span data-ttu-id="7c478-144">[Obtenga información acerca de cómo toouse Hola tooadminister de interfaz de usuario web local a la matriz Virtual de StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="7c478-144">[Learn how toouse hello local web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

