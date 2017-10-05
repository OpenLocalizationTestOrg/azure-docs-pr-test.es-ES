---
title: "Conmutación por error y recuperación ante desastres de StorSimple para dispositivos de la serie 8000| Microsoft Docs"
description: Aprenda a conmutar por error el dispositivo StorSimple en el mismo dispositivo.
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: acc8929dc3476e9590e8e4d9526b38b7c0719570
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-your-storsimple-physical-device-to-same-device"></a><span data-ttu-id="38c6c-103">Conmutación por error del dispositivo físico StorSimple en el mismo dispositivo</span><span class="sxs-lookup"><span data-stu-id="38c6c-103">Fail over your StorSimple physical device to same device</span></span>

## <a name="overview"></a><span data-ttu-id="38c6c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="38c6c-104">Overview</span></span>

<span data-ttu-id="38c6c-105">En este tutorial se describen los pasos necesarios para conmutar por error un dispositivo físico de la serie StorSimple 8000 en sí mismo en caso de desastre.</span><span class="sxs-lookup"><span data-stu-id="38c6c-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to itself if there is a disaster.</span></span> <span data-ttu-id="38c6c-106">StorSimple usa la característica de conmutación por error de dispositivos para migrar los datos desde un dispositivo físico de origen en el centro de datos a otro dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="38c6c-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="38c6c-107">Las instrucciones de este tutorial se aplican a los dispositivos físicos de la serie StorSimple 8000 que ejecutan las versiones de software Update 3 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="38c6c-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="38c6c-108">Para aprender más sobre la conmutación por error de dispositivos y cómo se usa para recuperarse de un desastre, vaya a [Conmutación por error y recuperación ante desastres para dispositivos de la serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="38c6c-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="38c6c-109">Para conmutar por error un dispositivo físico a otro dispositivo físico, vaya a [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md) (Conmutación por error al mismo dispositivo físico StorSimple).</span><span class="sxs-lookup"><span data-stu-id="38c6c-109">To fail over a physical device to another physical device, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="38c6c-110">Para conmutar por error un dispositivo físico StorSimple a un dispositivo StorSimple Cloud Appliance, vaya a [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md) (Conmutación por error a un dispositivo StorSimple Cloud Appliance).</span><span class="sxs-lookup"><span data-stu-id="38c6c-110">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="38c6c-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="38c6c-111">Prerequisites</span></span>

- <span data-ttu-id="38c6c-112">Asegúrese de haber revisado las consideraciones sobre la conmutación por error de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="38c6c-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="38c6c-113">Para más información, vaya a [Consideraciones comunes para la conmutación por error de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="38c6c-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-to-fail-over-to-the-same-device"></a><span data-ttu-id="38c6c-114">Pasos para conmutar por error al mismo dispositivo</span><span class="sxs-lookup"><span data-stu-id="38c6c-114">Steps to fail over to the same device</span></span>

<span data-ttu-id="38c6c-115">Realice los pasos siguientes si necesita conmutar por error al mismo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="38c6c-115">Perform the following steps if you need to fail over to the same device.</span></span>

1. <span data-ttu-id="38c6c-116">Tome instantáneas en la nube de todos los volúmenes del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="38c6c-116">Take cloud snapshots of all the volumes in your device.</span></span> <span data-ttu-id="38c6c-117">Para más información, vaya a [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md) (Uso del servicio StorSimple Device Manager para crear copias de seguridad).</span><span class="sxs-lookup"><span data-stu-id="38c6c-117">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="38c6c-118">Restablezca el dispositivo a los valores predeterminados de fábrica.</span><span class="sxs-lookup"><span data-stu-id="38c6c-118">Reset your device to factory defaults.</span></span> <span data-ttu-id="38c6c-119">Siga las instrucciones detalladas de [Cómo restablecer un dispositivo StorSimple a los valores predeterminados de fábrica](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="38c6c-119">Follow the detailed instructions in [how to reset a StorSimple device to factory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="38c6c-120">Vaya al servicio StorSimple Device Manager y, después, haga clic en **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="38c6c-120">Go to the StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="38c6c-121">En la hoja **Dispositivos**, el dispositivo antiguo debe aparecer como **Sin conexión**.</span><span class="sxs-lookup"><span data-stu-id="38c6c-121">In the **Devices** blade, the old device should show as **Offline**.</span></span>

    ![Dispositivo de origen sin conexión](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="38c6c-123">Configure el dispositivo y vuelva a registrarlo con el servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="38c6c-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="38c6c-124">El dispositivo recién registrado debe aparecer como **Listo para configurar**.</span><span class="sxs-lookup"><span data-stu-id="38c6c-124">The newly registered device should show as **Ready to set up**.</span></span> <span data-ttu-id="38c6c-125">El nombre del nuevo dispositivo es el mismo que el del dispositivo antiguo, pero se le ha anexado un número para indicar que el dispositivo se ha restablecido a sus valores predeterminados de fábrica y se ha registrado de nuevo.</span><span class="sxs-lookup"><span data-stu-id="38c6c-125">The device name for the new device is the same as the old device but appended with a numeral to indicate that the device was reset to factory default and registered again.</span></span>

    ![Dispositivo recién registrado y listo para configurar](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="38c6c-127">Para el nuevo dispositivo, complete la configuración del mismo.</span><span class="sxs-lookup"><span data-stu-id="38c6c-127">For the new device, complete the device setup.</span></span> <span data-ttu-id="38c6c-128">Para más información, vaya a [Paso 4: Completar la instalación mínima del dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="38c6c-128">For more information, go to [Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="38c6c-129">En la hoja **Dispositivos**, el estado del dispositivo cambia a **En línea**.</span><span class="sxs-lookup"><span data-stu-id="38c6c-129">On the **Devices** blade, the status of the device changes to **Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="38c6c-130">**Complete la configuración mínima primero, o se puede producir un error en la recuperación ante desastres**.</span><span class="sxs-lookup"><span data-stu-id="38c6c-130">**Complete the minimum configuration first, or your DR may fail.**</span></span>

    ![Dispositivo recién registrado en línea](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="38c6c-132">Seleccione el dispositivo antiguo (con el estado sin conexión) y, en la barra de comandos, haga clic en **Conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="38c6c-132">Select the old device (status offline) and from the command bar, click **Fail over**.</span></span> <span data-ttu-id="38c6c-133">En la hoja **Conmutación por error**, seleccione el dispositivo antiguo como origen y especifique el dispositivo de destino como el dispositivo recién registrado.</span><span class="sxs-lookup"><span data-stu-id="38c6c-133">In the **Fail over** blade, select old device as the source and specify the target device as the newly registered device.</span></span>

    ![Resumen de la conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="38c6c-135">Para obtener instrucciones detalladas, consulte [Conmutar por error a otro dispositivo físico](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="38c6c-135">For detailed instructions, refer to [Fail over to another physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="38c6c-136">Se crea un trabajo de restauración de dispositivo que puede supervisar desde la hoja **Trabajos**.</span><span class="sxs-lookup"><span data-stu-id="38c6c-136">A device restore job is created that you can monitor from the **Jobs** blade.</span></span>

8. <span data-ttu-id="38c6c-137">Después de que el trabajo se haya completado correctamente, acceda al dispositivo nuevo y navegue hasta la hoja **Contenedores de volúmenes**.</span><span class="sxs-lookup"><span data-stu-id="38c6c-137">After the job has successfully completed, access the new device and navigate to the **Volume containers** blade.</span></span> <span data-ttu-id="38c6c-138">Compruebe que todos los contenedores de volúmenes del dispositivo antiguo se han migrado al nuevo.</span><span class="sxs-lookup"><span data-stu-id="38c6c-138">Verify that all the volume containers from the old device have migrated to the new device.</span></span>

   ![Contenedores de volúmenes migrados](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="38c6c-140">Una vez completada la conmutación por error, puede desactivar y eliminar el dispositivo antiguo del portal.</span><span class="sxs-lookup"><span data-stu-id="38c6c-140">After the failover is complete, you can deactivate and delete the old device from the portal.</span></span> <span data-ttu-id="38c6c-141">Seleccione el dispositivo antiguo (sin conexión), haga clic con el botón derecho y, a continuación, seleccione **Desactivar**.</span><span class="sxs-lookup"><span data-stu-id="38c6c-141">Select the old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="38c6c-142">Una vez desactivado, se actualiza el estado del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="38c6c-142">After the device is deactivated, the status of the device is updated.</span></span>

     ![Dispositivo de origen desactivado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="38c6c-144">Seleccione el dispositivo desactivado, haga clic con el botón derecho y, a continuación, seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="38c6c-144">Select the deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="38c6c-145">Con ello, eliminará el dispositivo de la lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="38c6c-145">This deletes the device from the list of devices.</span></span>

    ![Dispositivo de origen eliminado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="38c6c-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="38c6c-147">Next steps</span></span>

* <span data-ttu-id="38c6c-148">Después de haber realizado una conmutación por error, puede que necesite [desactivar o eliminar el dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="38c6c-148">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="38c6c-149">Para más información sobre cómo usar el servicio StorSimple Device Manager, vaya a [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md) (Uso del servicio StorSimple Device Manager para administrar el dispositivo StorSimple).</span><span class="sxs-lookup"><span data-stu-id="38c6c-149">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

