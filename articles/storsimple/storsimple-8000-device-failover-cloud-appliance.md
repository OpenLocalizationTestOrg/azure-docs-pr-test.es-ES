---
title: "Conmutación por error y recuperación ante desastres de StorSimple en un dispositivo StorSimple Cloud Appliance | Microsoft Docs"
description: "Aprenda a conmutar por error el dispositivo físico de la serie StorSimple 8000 a un dispositivo de nube."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: ec8bebf2854e84a37e84b45564e80fc20b63d8d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-to-your-storsimple-cloud-appliance"></a><span data-ttu-id="2b76d-103">Conmutación por error a StorSimple Cloud Appliance</span><span class="sxs-lookup"><span data-stu-id="2b76d-103">Fail over to your StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="2b76d-104">Información general</span><span class="sxs-lookup"><span data-stu-id="2b76d-104">Overview</span></span>

<span data-ttu-id="2b76d-105">En este tutorial se describen los pasos necesarios para conmutar por error un dispositivo físico de la serie StorSimple 8000 a un dispositivo StorSimple Cloud Appliance en caso de desastre.</span><span class="sxs-lookup"><span data-stu-id="2b76d-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to a StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="2b76d-106">StorSimple usa la característica de conmutación por error de dispositivos para migrar los datos desde un dispositivo físico de origen en el centro de datos a un dispositivo de nube que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="2b76d-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to a cloud appliance running in Azure.</span></span> <span data-ttu-id="2b76d-107">Las instrucciones de este tutorial se aplican a los dispositivos físicos y dispositivos de nube de la serie StorSimple 8000 que ejecutan las versiones de software Update 3 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="2b76d-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="2b76d-108">Para aprender más sobre la conmutación por error de dispositivos y cómo se usa para recuperarse de un desastre, vaya a [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md) (Conmutación por error y recuperación ante desastres para dispositivos de la serie StorSimple 8000).</span><span class="sxs-lookup"><span data-stu-id="2b76d-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="2b76d-109">Para conmutar por error un dispositivo físico StorSimple a otro dispositivo físico, vaya a [Fail over to a StorSimple physical device](storsimple-8000-device-failover-physical-device.md) (Conmutación por error a un dispositivo físico StorSimple).</span><span class="sxs-lookup"><span data-stu-id="2b76d-109">To fail over a StorSimple physical device to another physical device, go to [Fail over to a StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="2b76d-110">Para conmutar por error un dispositivo a sí mismo, vaya a [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md) (Conmutación por error al mismo dispositivo físico StorSimple).</span><span class="sxs-lookup"><span data-stu-id="2b76d-110">To fail over a device to itself, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b76d-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2b76d-111">Prerequisites</span></span>

- <span data-ttu-id="2b76d-112">Asegúrese de haber revisado las consideraciones sobre la conmutación por error de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="2b76d-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="2b76d-113">Para más información, vaya a [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md) (Consideraciones comunes sobre la conmutación por error de dispositivos).</span><span class="sxs-lookup"><span data-stu-id="2b76d-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="2b76d-114">Antes de ejecutar este procedimiento, debe haber creado y configurado un dispositivo StorSimple Cloud Appliance.</span><span class="sxs-lookup"><span data-stu-id="2b76d-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="2b76d-115">Si ejecuta la versión de software Update 3 o posterior, considere la posibilidad de usar un dispositivo de nube 8020 para el DR.</span><span class="sxs-lookup"><span data-stu-id="2b76d-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for the DR.</span></span> <span data-ttu-id="2b76d-116">El modelo 8020 tiene 64 TB y usa Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="2b76d-116">The 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="2b76d-117">Para más información, vaya a [Implementación y administración de una instancia de StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="2b76d-117">For more information, go to [Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-to-fail-over-to-a-cloud-appliance"></a><span data-ttu-id="2b76d-118">Pasos para la conmutación por error a un dispositivo de nube</span><span class="sxs-lookup"><span data-stu-id="2b76d-118">Steps to fail over to a cloud appliance</span></span>

<span data-ttu-id="2b76d-119">Siga estos pasos para restaurar el dispositivo a un dispositivo StorSimple Cloud Appliance de destino.</span><span class="sxs-lookup"><span data-stu-id="2b76d-119">Perform the following steps to restore the device to a target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="2b76d-120">Compruebe que el contenedor de volúmenes que desea conmutar por error tiene asociadas instantáneas en la nube.</span><span class="sxs-lookup"><span data-stu-id="2b76d-120">Verify that the volume container you want to fail over has associated cloud snapshots.</span></span> <span data-ttu-id="2b76d-121">Para más información, vaya a [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md) (Uso del servicio StorSimple Device Manager para crear copias de seguridad).</span><span class="sxs-lookup"><span data-stu-id="2b76d-121">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="2b76d-122">Vaya al servicio Administrador de dispositivos de StorSimple y haga clic en **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="2b76d-122">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="2b76d-123">En la hoja **Dispositivos**, vaya a la lista de dispositivos conectados con su servicio.</span><span class="sxs-lookup"><span data-stu-id="2b76d-123">In the **Devices** blade, go to the list of devices connected with your service.</span></span>
    <span data-ttu-id="2b76d-124">![Seleccionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="2b76d-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="2b76d-125">Seleccione su dispositivo de origen y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="2b76d-125">Select and click your source device.</span></span> <span data-ttu-id="2b76d-126">El dispositivo de origen tiene los contenedores de volúmenes que desea conmutar por error.</span><span class="sxs-lookup"><span data-stu-id="2b76d-126">The source device has the volume containers that you want to fail over.</span></span> <span data-ttu-id="2b76d-127">Vaya a **Configuración > Contenedores de volúmenes**.</span><span class="sxs-lookup"><span data-stu-id="2b76d-127">Go to **Settings > Volume Containers**.</span></span>

    ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="2b76d-129">Seleccione un contenedor de volúmenes que desee conmutar por error a otro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b76d-129">Select a volume container that you would like to fail over to another device.</span></span> <span data-ttu-id="2b76d-130">Haga clic en el contenedor de volúmenes para mostrar la lista de volúmenes incluidos dentro de este contenedor.</span><span class="sxs-lookup"><span data-stu-id="2b76d-130">Click the volume container to display the list of volumes within this container.</span></span> <span data-ttu-id="2b76d-131">Seleccione un volumen, haga clic en él con el botón derecho y haga clic en **Desconectar** para desconectar el volumen.</span><span class="sxs-lookup"><span data-stu-id="2b76d-131">Select a volume, right-click, and click **Take Offline** to take the volume offline.</span></span>

    ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="2b76d-133">Repita este proceso para todos los volúmenes incluidos en el contenedor de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="2b76d-133">Repeat this process for all the volumes in the volume container.</span></span>

     ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="2b76d-135">Repita el paso anterior para todos los contenedores de volúmenes que le gustaría conmutar por error a otro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b76d-135">Repeat the previous step for all the volume containers you would like to fail over to another device.</span></span>

7. <span data-ttu-id="2b76d-136">Vuelva a la hoja **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="2b76d-136">Go back to the **Devices** blade.</span></span> <span data-ttu-id="2b76d-137">En la barra de comandos, haga clic en **Conmutar por error**.</span><span class="sxs-lookup"><span data-stu-id="2b76d-137">From the command bar, click **Fail over**.</span></span>

    ![Acción de hacer clic en Conmutar por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="2b76d-139">En la hoja **Conmutar por error**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2b76d-139">In the **Fail over** blade, perform the following steps:</span></span>
   
    1. <span data-ttu-id="2b76d-140">Haga clic en **Origen**.</span><span class="sxs-lookup"><span data-stu-id="2b76d-140">Click **Source**.</span></span> <span data-ttu-id="2b76d-141">Seleccione los contenedores de volúmenes para conmutar por error.</span><span class="sxs-lookup"><span data-stu-id="2b76d-141">Select the volume containers to fail over.</span></span> <span data-ttu-id="2b76d-142">**Solo se muestran los contenedores de volúmenes con volúmenes desconectados e instantáneas de nube asociadas.**</span><span class="sxs-lookup"><span data-stu-id="2b76d-142">**Only the volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="2b76d-143">![Seleccionar origen](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="2b76d-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="2b76d-144">Haga clic en **Destino**.</span><span class="sxs-lookup"><span data-stu-id="2b76d-144">Click **Target**.</span></span> <span data-ttu-id="2b76d-145">Seleccione un dispositivo de nube de destino en la lista desplegable de dispositivos disponibles.</span><span class="sxs-lookup"><span data-stu-id="2b76d-145">Select a target cloud appliance from the dropdown list of available devices.</span></span> <span data-ttu-id="2b76d-146">**Solo se muestran en la lista los dispositivos que tienen capacidad suficiente para alojar los contenedores de volúmenes de origen.**</span><span class="sxs-lookup"><span data-stu-id="2b76d-146">**Only the devices that have sufficient capacity to accommodate source volume containers are displayed in the list.**</span></span>

        ![Selección del destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="2b76d-148">Revise la configuración de conmutación por error en **Resumen** y seleccione la casilla de verificación que indica que los volúmenes de los contenedores de volumen seleccionados están sin conexión.</span><span class="sxs-lookup"><span data-stu-id="2b76d-148">Review the failover settings under **Summary** and select the checkbox indicating that the volumes in selected volume containers are offline.</span></span> 

        ![Revisión de la configuración de conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="2b76d-150">Se crea un trabajo de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="2b76d-150">A failover job is created.</span></span> <span data-ttu-id="2b76d-151">Para supervisar el trabajo de conmutación por error, haga clic en la notificación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2b76d-151">To monitor the failover job, click the job notification.</span></span>

    ![Supervisión del trabajo de conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="2b76d-153">Una vez completada la conmutación por error, vuelva a la hoja **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="2b76d-153">After the failover is completed, go back to the **Devices** blade.</span></span>

    1. <span data-ttu-id="2b76d-154">Seleccione el dispositivo que se usó como destino para la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="2b76d-154">Select the device that was used as the target for the failover.</span></span>

       ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="2b76d-156">Haga clic en **Contenedores de volúmenes**.</span><span class="sxs-lookup"><span data-stu-id="2b76d-156">Click **Volume Containers**.</span></span> <span data-ttu-id="2b76d-157">Deberían aparecer todos los contenedores de volúmenes, junto con los volúmenes del dispositivo antiguo.</span><span class="sxs-lookup"><span data-stu-id="2b76d-157">All the volume containers, along with the volumes from the old device, should be listed.</span></span>

       <span data-ttu-id="2b76d-158">Si el contenedor de volúmenes que ha conmutado por error ha anclado volúmenes localmente, esos volúmenes se conmutan por error como volúmenes en capas.</span><span class="sxs-lookup"><span data-stu-id="2b76d-158">If the volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="2b76d-159">Los volúmenes anclados localmente no se admiten en un dispositivo StorSimple Cloud Appliance.</span><span class="sxs-lookup"><span data-stu-id="2b76d-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Visualización de contenedores de volúmenes de destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="2b76d-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b76d-161">Next steps</span></span>

* <span data-ttu-id="2b76d-162">Después de haber realizado una conmutación por error, puede que necesite [desactivar o eliminar el dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="2b76d-162">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="2b76d-163">Para más información sobre cómo usar el servicio StorSimple Device Manager, vaya a [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md) (Uso del servicio StorSimple Device Manager para administrar el dispositivo StorSimple).</span><span class="sxs-lookup"><span data-stu-id="2b76d-163">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

