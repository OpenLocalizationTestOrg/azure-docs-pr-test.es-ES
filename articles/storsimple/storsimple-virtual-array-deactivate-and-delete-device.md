---
title: aaaDeactivate y eliminar una matriz Virtual de Microsoft Azure StorSimple | Documentos de Microsoft
description: "Describe cómo el dispositivo de StorSimple tooremove de servicio, en primer lugar la desactivación y, a continuación, eliminarlo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="316cf-103">Desactivación y eliminación de una matriz virtual de StorSimple</span><span class="sxs-lookup"><span data-stu-id="316cf-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="316cf-104">Información general</span><span class="sxs-lookup"><span data-stu-id="316cf-104">Overview</span></span>

<span data-ttu-id="316cf-105">Al desactivar una matriz Virtual de StorSimple, se rompe conexión Hola entre dispositivos de Hola y el servicio de administrador de dispositivos de StorSimple correspondiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="316cf-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="316cf-106">Este tutorial explica cómo realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="316cf-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="316cf-107">Desactivación de un dispositivo</span><span class="sxs-lookup"><span data-stu-id="316cf-107">Deactivate a device</span></span> 
* <span data-ttu-id="316cf-108">Eliminación de un dispositivo desactivado</span><span class="sxs-lookup"><span data-stu-id="316cf-108">Delete a deactivated device</span></span>

<span data-ttu-id="316cf-109">información de Hello en este artículo aplica tooStorSimple arreglos de discos virtuales.</span><span class="sxs-lookup"><span data-stu-id="316cf-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="316cf-110">Para obtener información sobre la 8000 serie, vaya toohow demasiado[desactivar o eliminar un dispositivo](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="316cf-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="316cf-111">¿Cuando toodeactivate?</span><span class="sxs-lookup"><span data-stu-id="316cf-111">When toodeactivate?</span></span>

<span data-ttu-id="316cf-112">La desactivación es una operación permanente y no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="316cf-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="316cf-113">No se puede registrar un dispositivo desactivado con hello servicio Administrador de dispositivos de StorSimple de nuevo.</span><span class="sxs-lookup"><span data-stu-id="316cf-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="316cf-114">Puede necesita toodeactivate y eliminar una matriz Virtual de StorSimple en hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="316cf-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="316cf-115">**Conmutación por error planeada** : el dispositivo está en línea y tiene previsto toofail sobre el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="316cf-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="316cf-116">Si tiene previsto tooupgrade tooa mayor dispositivo, deberá toofail sobre el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="316cf-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="316cf-117">Después de que se transfiere la propiedad de los datos Hola y Hola conmutación por error, se elimina automáticamente el dispositivo de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="316cf-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="316cf-118">**Conmutación por error imprevista** : el dispositivo está sin conexión y necesite toofail en relación con el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="316cf-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="316cf-119">Esta situación puede producirse durante un desastre cuando hay una interrupción en el centro de datos de Hola y el dispositivo principal está inactivo.</span><span class="sxs-lookup"><span data-stu-id="316cf-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="316cf-120">Planear toofail durante hello tooa secundaria un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="316cf-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="316cf-121">Después de que se transfiere la propiedad de los datos Hola y Hola conmutación por error, se elimina automáticamente el dispositivo de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="316cf-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="316cf-122">**Retirar** : desee toodecommission Hola dispositivo.</span><span class="sxs-lookup"><span data-stu-id="316cf-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="316cf-123">Para ello, deberá toofirst desactivar Hola dispositivo y, a continuación, elimínelo.</span><span class="sxs-lookup"><span data-stu-id="316cf-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="316cf-124">Al desactivar un dispositivo, no podrá acceder a los datos almacenados localmente.</span><span class="sxs-lookup"><span data-stu-id="316cf-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="316cf-125">Puede que solo acceso y recuperar Hola los datos almacenados en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="316cf-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="316cf-126">Si tiene previsto tookeep los datos del dispositivo Hola tras la desactivación, debe tomar una instantánea de nube de todos los datos antes de desactivar un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="316cf-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="316cf-127">Esta instantánea de nube permite toorecover Hola a todos los datos en una fase posterior.</span><span class="sxs-lookup"><span data-stu-id="316cf-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="316cf-128">Desactivación de un dispositivo</span><span class="sxs-lookup"><span data-stu-id="316cf-128">Deactivate a device</span></span>

<span data-ttu-id="316cf-129">toodeactivate el dispositivo, realizar Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="316cf-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="316cf-130">dispositivo de hello toodeactivate</span><span class="sxs-lookup"><span data-stu-id="316cf-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="316cf-131">En el servicio, vaya demasiado**Administración > dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="316cf-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="316cf-132">Hola **dispositivos** hoja, haga clic en y dispositivo Hola select que desea toodeactivate.</span><span class="sxs-lookup"><span data-stu-id="316cf-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![Seleccione el dispositivo toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="316cf-134">En su **panel del dispositivo** hoja, haga clic en **... Más** y en la lista de hello, seleccione **desactivar**.</span><span class="sxs-lookup"><span data-stu-id="316cf-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![Clic en Desactivar](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="316cf-136">Hola **desactivar** hoja, nombre de dispositivo de tipo hello y, a continuación, haga clic en **desactivar**.</span><span class="sxs-lookup"><span data-stu-id="316cf-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![Confirmación de la desactivación](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="316cf-138">Hola desactivar el proceso comienza y toma toocomplete unos minutos.</span><span class="sxs-lookup"><span data-stu-id="316cf-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![Desactivación en curso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="316cf-140">Tras la desactivación, Hola lista de las actualizaciones de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="316cf-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![Desactivación completa](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="316cf-142">Ahora puede eliminar este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="316cf-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="316cf-143">Eliminar dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="316cf-143">Delete hello device</span></span>

<span data-ttu-id="316cf-144">Un dispositivo tiene toobe primera desactivado toodelete lo.</span><span class="sxs-lookup"><span data-stu-id="316cf-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="316cf-145">Eliminar un dispositivo, quita de la lista Hola de dispositivos conectados toohello servicio.</span><span class="sxs-lookup"><span data-stu-id="316cf-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="316cf-146">servicio Hello, a continuación, no podrá administrar dispositivos Hola eliminado.</span><span class="sxs-lookup"><span data-stu-id="316cf-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="316cf-147">datos de Hello asociados Hola dispositivo sin embargo permanecen en nube Hola.</span><span class="sxs-lookup"><span data-stu-id="316cf-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="316cf-148">A partir de ahí, estos datos acumulan cargos.</span><span class="sxs-lookup"><span data-stu-id="316cf-148">This data then accrues charges.</span></span>

<span data-ttu-id="316cf-149">dispositivo de hello toodelete, realizar Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="316cf-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="316cf-150">dispositivo de hello toodelete</span><span class="sxs-lookup"><span data-stu-id="316cf-150">toodelete hello device</span></span>

1. <span data-ttu-id="316cf-151">En el Administrador de dispositivos de StorSimple, vaya demasiado**Administración > dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="316cf-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="316cf-152">Hola **dispositivos** hoja, seleccione un dispositivo desactivado que desee toodelete.</span><span class="sxs-lookup"><span data-stu-id="316cf-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="316cf-153">Hola **panel del dispositivo** hoja, haga clic en **... Más** y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="316cf-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Seleccione el dispositivo toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="316cf-155">Hola **eliminar** hoja, escriba un nombre hello de la eliminación de dispositivos tooconfirm hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="316cf-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="316cf-156">Eliminar dispositivo hello no elimina datos en la nube Hola asociados con el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="316cf-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![Confirmar eliminación](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="316cf-158">eliminación de Hola se inicia y tarda unos toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="316cf-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![Eliminación en curso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="316cf-160">Después de elimina el dispositivo de hello, puede ver lista de hello actualizado de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="316cf-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="316cf-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="316cf-161">Next steps</span></span>

* <span data-ttu-id="316cf-162">Para obtener información acerca de cómo toofail sobre, vaya demasiado[conmutación por error y recuperación ante desastres de la matriz Virtual de StorSimple](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="316cf-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="316cf-163">toolearn Obtenga más información sobre cómo ir demasiado toouse Hola servicio de administrador de dispositivos de StorSimple,[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple la matriz Virtual de StorSimple](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="316cf-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

