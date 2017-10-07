---
title: "aaaStorSimple conmutación por error, recuperación ante desastres para dispositivos 8000 serie | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toofail sobre su toohello de dispositivo de StorSimple mismo dispositivo."
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
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a><span data-ttu-id="22208-103">Conmutar por error el dispositivo de toosame del dispositivo físico de StorSimple</span><span class="sxs-lookup"><span data-stu-id="22208-103">Fail over your StorSimple physical device toosame device</span></span>

## <a name="overview"></a><span data-ttu-id="22208-104">Información general</span><span class="sxs-lookup"><span data-stu-id="22208-104">Overview</span></span>

<span data-ttu-id="22208-105">Este tutorial describe Hola pasos necesarios toofail sobre un tooitself de dispositivo físico de StorSimple 8000 series si se produce un desastre.</span><span class="sxs-lookup"><span data-stu-id="22208-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooitself if there is a disaster.</span></span> <span data-ttu-id="22208-106">StorSimple usa datos toomigrate características de conmutación por error de dispositivo de Hola desde un dispositivo físico de origen en el dispositivo físico de hello datacenter tooanother.</span><span class="sxs-lookup"><span data-stu-id="22208-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="22208-107">Guía de Hello en este tutorial aplica a dispositivos físicos de tooStorSimple 8000 series con versiones de software Update 3 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="22208-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="22208-108">toolearn más información acerca de conmutación por error de dispositivo y su uso toorecover ante un desastre, vaya demasiado[conmutación por error y recuperación ante desastres para dispositivos de la serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="22208-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="22208-109">toofail a través de un dispositivo físico tooanother de dispositivo físico, vaya demasiado[una conmutación por error toohello mismo dispositivo físico StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="22208-109">toofail over a physical device tooanother physical device, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="22208-110">toofail a través de un tooa de dispositivo físico StorSimple Appliance en la nube de StorSimple, vaya demasiado[conmutar por error tooa dispositivo de nube de StorSimple](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="22208-110">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="22208-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="22208-111">Prerequisites</span></span>

- <span data-ttu-id="22208-112">Asegúrese de revisar las consideraciones de Hola para conmutación por error de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="22208-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="22208-113">Para obtener más información, consulte demasiado[consideraciones comunes para conmutación por error de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="22208-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-toofail-over-toohello-same-device"></a><span data-ttu-id="22208-114">Pasos toofail sobre toohello mismo dispositivo</span><span class="sxs-lookup"><span data-stu-id="22208-114">Steps toofail over toohello same device</span></span>

<span data-ttu-id="22208-115">Realizar Hola siguientes pasos si necesita toofail sobre toohello mismo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="22208-115">Perform hello following steps if you need toofail over toohello same device.</span></span>

1. <span data-ttu-id="22208-116">Tomar instantáneas de nube de todos los volúmenes de hello en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="22208-116">Take cloud snapshots of all hello volumes in your device.</span></span> <span data-ttu-id="22208-117">Para obtener más información, consulte demasiado[copias de seguridad de administrador de dispositivos de StorSimple de uso servicio toocreate](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="22208-117">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="22208-118">Restablecer los valores predeterminados toofactory del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="22208-118">Reset your device toofactory defaults.</span></span> <span data-ttu-id="22208-119">Siga Hola detallada instrucciones [la configuración predeterminada de tooreset un toofactory de dispositivo de StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="22208-119">Follow hello detailed instructions in [how tooreset a StorSimple device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="22208-120">Servicio de administrador de dispositivos de StorSimple toohello go y, a continuación, seleccione **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="22208-120">Go toohello StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="22208-121">Hola **dispositivos** hoja, dispositivo antiguo de hello debería aparecer como **sin conexión**.</span><span class="sxs-lookup"><span data-stu-id="22208-121">In hello **Devices** blade, hello old device should show as **Offline**.</span></span>

    ![Dispositivo de origen sin conexión](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="22208-123">Configure el dispositivo y vuelva a registrarlo con el servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="22208-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="22208-124">Hello dispositivo recién registrado debería ser **listo tooset seguridad**.</span><span class="sxs-lookup"><span data-stu-id="22208-124">hello newly registered device should show as **Ready tooset up**.</span></span> <span data-ttu-id="22208-125">nombre de dispositivo de Hello para el nuevo dispositivo de hello es hello igual que el dispositivo antiguo de hello pero le anexa un numeral tooindicate ese dispositivo Hola era restablecimiento toofactory predeterminada y vuelva a registrar.</span><span class="sxs-lookup"><span data-stu-id="22208-125">hello device name for hello new device is hello same as hello old device but appended with a numeral tooindicate that hello device was reset toofactory default and registered again.</span></span>

    ![Los dispositivos recién registrados listo tooset seguridad](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="22208-127">Para el nuevo dispositivo hello, complete la instalación de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="22208-127">For hello new device, complete hello device setup.</span></span> <span data-ttu-id="22208-128">Para obtener más información, consulte demasiado[paso 4: completar el programa de instalación mínima del dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="22208-128">For more information, go too[Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="22208-129">En hello **dispositivos** hoja, cambia de estado de hello de dispositivo de hello demasiado**Online**.</span><span class="sxs-lookup"><span data-stu-id="22208-129">On hello **Devices** blade, hello status of hello device changes too**Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="22208-130">**Completar la configuración mínima de hello en primer lugar, o puede producir un error en la recuperación ante desastres.**</span><span class="sxs-lookup"><span data-stu-id="22208-130">**Complete hello minimum configuration first, or your DR may fail.**</span></span>

    ![Dispositivo recién registrado en línea](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="22208-132">Seleccione el dispositivo antiguo de hello (estado sin conexión) y en la barra de comandos de hello, haga clic en **una conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="22208-132">Select hello old device (status offline) and from hello command bar, click **Fail over**.</span></span> <span data-ttu-id="22208-133">Hola **una conmutación por error** hoja, seleccione el dispositivo anterior como origen de Hola y especifique dispositivo de destino de hello según Hola recién registrado el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="22208-133">In hello **Fail over** blade, select old device as hello source and specify hello target device as hello newly registered device.</span></span>

    ![Resumen de la conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="22208-135">Para obtener instrucciones detalladas, consulte demasiado[conmutar por error dispositivo físico de tooanother](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="22208-135">For detailed instructions, refer too[Fail over tooanother physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="22208-136">Se crea un trabajo de restauración de dispositivo que puede supervisar desde hello **trabajos** hoja.</span><span class="sxs-lookup"><span data-stu-id="22208-136">A device restore job is created that you can monitor from hello **Jobs** blade.</span></span>

8. <span data-ttu-id="22208-137">Una vez se haya completado correctamente el trabajo de hello, acceder nuevo dispositivo de Hola y navegar toohello **contenedores de volúmenes** hoja.</span><span class="sxs-lookup"><span data-stu-id="22208-137">After hello job has successfully completed, access hello new device and navigate toohello **Volume containers** blade.</span></span> <span data-ttu-id="22208-138">Compruebe que todos los contenedores de volúmenes de hello de dispositivo antiguo de hello migraron toohello nuevo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="22208-138">Verify that all hello volume containers from hello old device have migrated toohello new device.</span></span>

   ![Contenedores de volúmenes migrados](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="22208-140">Una vez completada la conmutación por error de hello, puede desactivar y eliminar dispositivo antiguo de Hola desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="22208-140">After hello failover is complete, you can deactivate and delete hello old device from hello portal.</span></span> <span data-ttu-id="22208-141">Seleccione Hola antiguo dispositivo (sin conexión), menú contextual y, a continuación, seleccione **desactivar**.</span><span class="sxs-lookup"><span data-stu-id="22208-141">Select hello old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="22208-142">Después de desactiva el dispositivo hello, estado de hello de dispositivo de Hola se actualiza.</span><span class="sxs-lookup"><span data-stu-id="22208-142">After hello device is deactivated, hello status of hello device is updated.</span></span>

     ![Dispositivo de origen desactivado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="22208-144">Hola seleccione desactivado el dispositivo, menú contextual y, a continuación, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="22208-144">Select hello deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="22208-145">Esto elimina el dispositivo de hello en lista de Hola de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="22208-145">This deletes hello device from hello list of devices.</span></span>

    ![Dispositivo de origen eliminado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="22208-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="22208-147">Next steps</span></span>

* <span data-ttu-id="22208-148">Después de haber realizado una conmutación por error, puede que necesite demasiado[desactive o elimine el dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="22208-148">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="22208-149">Para obtener información acerca de cómo toouse Hola Administrador de dispositivos de StorSimple de servicio, vaya demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="22208-149">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

