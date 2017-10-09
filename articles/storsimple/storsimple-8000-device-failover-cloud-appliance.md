---
title: "aaaStorSimple conmutación por error, tooa de recuperación ante desastres dispositivo de StorSimple en la nube | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toofail sobre su tooa de dispositivo físico de StorSimple 8000 series en la nube de dispositivo."
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
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a><span data-ttu-id="679b7-103">Conmutar por error tooyour dispositivo de StorSimple en la nube</span><span class="sxs-lookup"><span data-stu-id="679b7-103">Fail over tooyour StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="679b7-104">Información general</span><span class="sxs-lookup"><span data-stu-id="679b7-104">Overview</span></span>

<span data-ttu-id="679b7-105">Este tutorial describe Hola pasos necesarios toofail sobre un dispositivo físico de serie StorSimple 8000 tooa dispositivo de StorSimple en la nube si se produce un desastre.</span><span class="sxs-lookup"><span data-stu-id="679b7-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooa StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="679b7-106">StorSimple usa datos toomigrate características de conmutación por error de dispositivo de Hola desde un dispositivo físico de origen de dispositivo de nube Hola datacenter tooa ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="679b7-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooa cloud appliance running in Azure.</span></span> <span data-ttu-id="679b7-107">Guía de Hello en este tutorial aplica a dispositivos físicos de tooStorSimple 8000 series y dispositivos en la nube con las versiones de software Update 3 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="679b7-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="679b7-108">toolearn más información acerca de conmutación por error de dispositivo y su uso toorecover ante un desastre, vaya demasiado[conmutación por error y recuperación ante desastres para dispositivos de la serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="679b7-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="679b7-109">toofail a través de un dispositivo físico de la tooanother de dispositivo físico StorSimple, vaya demasiado[conmutar por error el dispositivo físico StorSimple tooa](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="679b7-109">toofail over a StorSimple physical device tooanother physical device, go too[Fail over tooa StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="679b7-110">toofail a través de un dispositivo tooitself, vaya demasiado[una conmutación por error toohello mismo dispositivo físico StorSimple](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="679b7-110">toofail over a device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="679b7-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="679b7-111">Prerequisites</span></span>

- <span data-ttu-id="679b7-112">Asegúrese de revisar las consideraciones de Hola para conmutación por error de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="679b7-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="679b7-113">Para obtener más información, consulte demasiado[consideraciones comunes para conmutación por error de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="679b7-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="679b7-114">Antes de ejecutar este procedimiento, debe haber creado y configurado un dispositivo StorSimple Cloud Appliance.</span><span class="sxs-lookup"><span data-stu-id="679b7-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="679b7-115">Si actualiza la versión del software de 3 o más adelante, considere el uso de un dispositivo en la nube 8020 para ejecución Hola recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="679b7-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for hello DR.</span></span> <span data-ttu-id="679b7-116">modelo 8020 Hello tiene 64 TB y utiliza el almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="679b7-116">hello 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="679b7-117">Para obtener más información, consulte demasiado[implementar y administrar un dispositivo de nube de StorSimple](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="679b7-117">For more information, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-toofail-over-tooa-cloud-appliance"></a><span data-ttu-id="679b7-118">Pasos toofail sobre tooa dispositivo de nube</span><span class="sxs-lookup"><span data-stu-id="679b7-118">Steps toofail over tooa cloud appliance</span></span>

<span data-ttu-id="679b7-119">Realizar Hola siguiendo los pasos toorestore Hola dispositivo tooa destino dispositivo de StorSimple en la nube.</span><span class="sxs-lookup"><span data-stu-id="679b7-119">Perform hello following steps toorestore hello device tooa target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="679b7-120">Compruebe que desea toofail sobre el contenedor de volumen Hola tenga asociadas instantáneas en la nube.</span><span class="sxs-lookup"><span data-stu-id="679b7-120">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="679b7-121">Para obtener más información, consulte demasiado[copias de seguridad de administrador de dispositivos de StorSimple de uso servicio toocreate](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="679b7-121">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="679b7-122">Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="679b7-122">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="679b7-123">Hola **dispositivos** hoja, vaya toohello lista de dispositivos conectados con su servicio.</span><span class="sxs-lookup"><span data-stu-id="679b7-123">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="679b7-124">![Seleccionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="679b7-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="679b7-125">Seleccione su dispositivo de origen y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="679b7-125">Select and click your source device.</span></span> <span data-ttu-id="679b7-126">dispositivo de origen de Hello tiene contenedores de volúmenes de Hola que desea toofail sobre.</span><span class="sxs-lookup"><span data-stu-id="679b7-126">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="679b7-127">Vaya demasiado**configuración > contenedores de volúmenes**.</span><span class="sxs-lookup"><span data-stu-id="679b7-127">Go too**Settings > Volume Containers**.</span></span>

    ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="679b7-129">Seleccione un contenedor de volúmenes que desearía toofail sobre tooanother dispositivo.</span><span class="sxs-lookup"><span data-stu-id="679b7-129">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="679b7-130">Haga clic en lista hello toodisplay de contenedor de volúmenes de Hola de volúmenes dentro de este contenedor.</span><span class="sxs-lookup"><span data-stu-id="679b7-130">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="679b7-131">Seleccione un volumen, el menú contextual y haga clic en **desconectar** volumen tootake Hola.</span><span class="sxs-lookup"><span data-stu-id="679b7-131">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span>

    ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="679b7-133">Repita este proceso para todos los volúmenes de Hola Hola contenedor de volúmenes.</span><span class="sxs-lookup"><span data-stu-id="679b7-133">Repeat this process for all hello volumes in hello volume container.</span></span>

     ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="679b7-135">Paso anterior Hola repeticiones de Hola a todos los contenedores de volúmenes le gustaría toofail sobre tooanother dispositivo.</span><span class="sxs-lookup"><span data-stu-id="679b7-135">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>

7. <span data-ttu-id="679b7-136">Volver atrás toohello **dispositivos** hoja.</span><span class="sxs-lookup"><span data-stu-id="679b7-136">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="679b7-137">En la barra de comandos de hello, haga clic en **una conmutación por error**.</span><span class="sxs-lookup"><span data-stu-id="679b7-137">From hello command bar, click **Fail over**.</span></span>

    ![Acción de hacer clic en Conmutar por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="679b7-139">Hola **una conmutación por error** hoja, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="679b7-139">In hello **Fail over** blade, perform hello following steps:</span></span>
   
    1. <span data-ttu-id="679b7-140">Haga clic en **Origen**.</span><span class="sxs-lookup"><span data-stu-id="679b7-140">Click **Source**.</span></span> <span data-ttu-id="679b7-141">Seleccione toofail de contenedores de volumen de hello sobre.</span><span class="sxs-lookup"><span data-stu-id="679b7-141">Select hello volume containers toofail over.</span></span> <span data-ttu-id="679b7-142">**Solo Hola contenedores de volúmenes con instantáneas en la nube asociado y se muestran los volúmenes sin conexión.**</span><span class="sxs-lookup"><span data-stu-id="679b7-142">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="679b7-143">![Seleccionar origen](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="679b7-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="679b7-144">Haga clic en **Destino**.</span><span class="sxs-lookup"><span data-stu-id="679b7-144">Click **Target**.</span></span> <span data-ttu-id="679b7-145">Seleccione un dispositivo de destino de la nube de lista desplegable de Hola de dispositivos disponibles.</span><span class="sxs-lookup"><span data-stu-id="679b7-145">Select a target cloud appliance from hello dropdown list of available devices.</span></span> <span data-ttu-id="679b7-146">**Solo los dispositivos Hola que tienen contenedores de volúmenes de origen de tooaccommodate capacidad suficiente se muestran en la lista de Hola.**</span><span class="sxs-lookup"><span data-stu-id="679b7-146">**Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.**</span></span>

        ![Seleccionar destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="679b7-148">Revise la configuración de conmutación por error de hello en **resumen** y seleccione la casilla de verificación de hello, que indica que los volúmenes de hello en contenedores de volumen seleccionados están sin conexión.</span><span class="sxs-lookup"><span data-stu-id="679b7-148">Review hello failover settings under **Summary** and select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> 

        ![Revisar la configuración de conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="679b7-150">Se crea un trabajo de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="679b7-150">A failover job is created.</span></span> <span data-ttu-id="679b7-151">conmutación por error de toomonitor Hola de trabajo, haga clic en la notificación de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="679b7-151">toomonitor hello failover job, click hello job notification.</span></span>

    ![Supervisión del trabajo de conmutación por error](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="679b7-153">Una vez completada la conmutación por error de hello, vuelva atrás toohello **dispositivos** hoja.</span><span class="sxs-lookup"><span data-stu-id="679b7-153">After hello failover is completed, go back toohello **Devices** blade.</span></span>

    1. <span data-ttu-id="679b7-154">Seleccione el dispositivo de Hola que se usa como destino de Hola para hello conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="679b7-154">Select hello device that was used as hello target for hello failover.</span></span>

       ![Selección del dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="679b7-156">Haga clic en **Contenedores de volúmenes**.</span><span class="sxs-lookup"><span data-stu-id="679b7-156">Click **Volume Containers**.</span></span> <span data-ttu-id="679b7-157">Todos los contenedores de volúmenes de hello, junto con los volúmenes de hello de dispositivo antiguo de hello, deberían aparecer.</span><span class="sxs-lookup"><span data-stu-id="679b7-157">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       <span data-ttu-id="679b7-158">Si el contenedor de volúmenes de Hola que ha conmutado por error ha anclado localmente volúmenes, los volúmenes se conmutan por error como volúmenes en capas.</span><span class="sxs-lookup"><span data-stu-id="679b7-158">If hello volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="679b7-159">Los volúmenes anclados localmente no se admiten en un dispositivo StorSimple Cloud Appliance.</span><span class="sxs-lookup"><span data-stu-id="679b7-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Visualización de contenedores de volúmenes de destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="679b7-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="679b7-161">Next steps</span></span>

* <span data-ttu-id="679b7-162">Después de haber realizado una conmutación por error, puede que necesite demasiado[desactive o elimine el dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="679b7-162">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="679b7-163">Para obtener información acerca de cómo toouse Hola Administrador de dispositivos de StorSimple de servicio, vaya demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="679b7-163">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

