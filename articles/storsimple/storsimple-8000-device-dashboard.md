---
title: Uso del resumen del dispositivo de la serie StorSimple 8000 | Microsoft Docs
description: "Describe el resumen del dispositivo del servicio StorSimple Device Manager y cómo usarlo para ver las métricas de almacenamiento y los iniciadores conectados y buscar el número de serie y el IQN."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 784d3ce9d8f926b00ac1c6fbf48a05c0b04f900a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="91b26-103">Uso del resumen del dispositivo del servicio StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="91b26-103">Use the device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="91b26-104">Información general</span><span class="sxs-lookup"><span data-stu-id="91b26-104">Overview</span></span>
<span data-ttu-id="91b26-105">La hoja de resumen del dispositivo StorSimple le ofrece una visión general sobre la información de un dispositivo StorSimple específico, a diferencia de la hoja de resumen del servicio, que le ofrece información sobre todos los dispositivos incluidos en la solución de Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91b26-105">The StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast to the service summary blade, which gives you information about all the devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="91b26-106">La hoja de resumen del dispositivo proporciona una vista de resumen de un dispositivo de la serie StorSimple 8000 que se registra con un determinado StorSimple Device Manager, y resalta los problemas en los dispositivos que necesitan la atención del administrador del sistema.</span><span class="sxs-lookup"><span data-stu-id="91b26-106">The device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="91b26-107">Este tutorial presenta la hoja de resumen de dispositivos, explica su contenido y su función, y describe las tareas que puede realizar desde esta hoja.</span><span class="sxs-lookup"><span data-stu-id="91b26-107">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="91b26-108">La hoja de resumen de dispositivos muestra la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="91b26-108">The device summary blade displays the following information:</span></span>

![Hoja de resumen del dispositivo](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="91b26-110">Barra de comandos de administración</span><span class="sxs-lookup"><span data-stu-id="91b26-110">Management command bar</span></span>

<span data-ttu-id="91b26-111">En la hoja de dispositivos de StorSimple, verá las opciones para administrar el dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91b26-111">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="91b26-112">Verá los comandos de administración en la parte superior de la hoja y en el lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="91b26-112">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="91b26-113">Utilice estas opciones para agregar recursos compartidos o volúmenes, o bien actualizar o conmutar por error el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91b26-113">Use these options to add shares or volumes, or update or fail over your device.</span></span>

![Barra de comandos de administración](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="91b26-115">Essentials</span><span class="sxs-lookup"><span data-stu-id="91b26-115">Essentials</span></span>

<span data-ttu-id="91b26-116">El área de información esencial captura algunas de las propiedades importantes, como el estado, el modelo, el IQN de destino y la versión del software.</span><span class="sxs-lookup"><span data-stu-id="91b26-116">The essentials area captures some of the important properties such as, the status, model, target IQN, and the software version.</span></span> 

![Información esencial de dispositivos](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="91b26-118">Supervisión</span><span class="sxs-lookup"><span data-stu-id="91b26-118">Monitoring</span></span>

* <span data-ttu-id="91b26-119">El icono **Alertas** proporciona una instantánea de todas las alertas activas para el dispositivo, agrupadas por gravedad.</span><span class="sxs-lookup"><span data-stu-id="91b26-119">The **Alerts** tile provides a snapshot of all the active alerts for your device, grouped by alert severity.</span></span>

    ![Icono Alertas](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="91b26-121">Haga clic en el icono para abrir la hoja **Alertas** y, a continuación, en una alerta concreta para ver detalles adicionales acerca de ella, incluidas las acciones recomendadas.</span><span class="sxs-lookup"><span data-stu-id="91b26-121">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="91b26-122">También puede desactivar la alerta si el problema se ha resuelto.</span><span class="sxs-lookup"><span data-stu-id="91b26-122">You can also clear the alert if the issue has been resolved.</span></span>

    ![Hacer clic en el icono Alertas](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="91b26-124">El icono **Estado y mantenimiento** proporciona información acerca del estado de los componentes de hardware de un dispositivo, incluido el estado del propio dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91b26-124">The **Status and health** tile provides insights into the hardware component health for a device including the device status.</span></span> <span data-ttu-id="91b26-125">El estado del dispositivo puede ser sin conexión, en línea, desactivado o listo para configurar.</span><span class="sxs-lookup"><span data-stu-id="91b26-125">The device status may be offline, online, deactivated, or ready to set up.</span></span>

    ![Icono Estado y mantenimiento](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="91b26-127">El icono **Volúmenes** proporciona un resumen del número de volúmenes del dispositivo, agrupados por estado.</span><span class="sxs-lookup"><span data-stu-id="91b26-127">The **Volumes** tile provides a summary of the number of volumes in your device grouped by status.</span></span>

    ![Icono Volúmenes](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="91b26-129">Haga clic en el icono para abrir la hoja de lista **Volúmenes** y, a continuación, en un recurso compartido o un volumen concreto para ver o modificar sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="91b26-129">Click the tile to open the **Volumes** list blade, and then click on an individual volume to view or modify its properties.</span></span>
    
    ![Hacer clic en el icono Volúmenes](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="91b26-131">Para más información, consulte cómo [administrar volúmenes](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="91b26-131">For more information, see how to [manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="91b26-132">En el gráfico **Uso**, puede ver el almacenamiento principal que se usa en su dispositivo y el almacenamiento en la nube consumido durante los últimos 7 días, el período predeterminado.</span><span class="sxs-lookup"><span data-stu-id="91b26-132">In the **Usage** chart, you can view the primary storage used across your device, and the cloud storage consumed over the past 7 days, the default time period.</span></span>

     ![Icono de Uso](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="91b26-134">Para elegir otra escala de tiempo, ese la opción **Editar** de la esquina superior derecha del gráfico.</span><span class="sxs-lookup"><span data-stu-id="91b26-134">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![Editar gráfico de uso](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="91b26-136">En este gráfico, puede ver las métricas del almacenamiento principal total (la cantidad de datos escritos por hosts en su dispositivo) y el almacenamiento en nube total consumido por su dispositivo durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="91b26-136">In this chart, you can view metrics for the total primary storage (the amount of data written by hosts to your device) and the total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="91b26-137">En este contexto, *almacenamiento principal* hace referencia a la cantidad total de los datos escritos por el host y se puede desglosar por tipo de volumen: el *almacenamiento principal en capas* incluye los datos almacenados localmente y en capas en la nube.</span><span class="sxs-lookup"><span data-stu-id="91b26-137">In this context, *primary storage* refers to the total amount of data written by the host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered to the cloud.</span></span> <span data-ttu-id="91b26-138">El *almacenamiento principal anclado localmente* incluye solo los datos almacenados localmente.</span><span class="sxs-lookup"><span data-stu-id="91b26-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="91b26-139">Por otro lado, *almacenamiento en la nube* es una medición de la cantidad total de datos almacenados en la nube.</span><span class="sxs-lookup"><span data-stu-id="91b26-139">*Cloud storage*, on the other hand, is a measurement of the total amount of data stored in the cloud.</span></span> <span data-ttu-id="91b26-140">Este almacenamiento incluye las copias de seguridad y los datos en niveles.</span><span class="sxs-lookup"><span data-stu-id="91b26-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="91b26-141">Los datos almacenados en la nube están desduplicados y comprimidos, mientras que el almacenamiento principal indica la cantidad de almacenamiento usado antes de que los datos estén desduplicados y comprimidos.</span><span class="sxs-lookup"><span data-stu-id="91b26-141">The data stored in the cloud is deduplicated and compressed, whereas primary storage indicates the amount of storage used before the data is deduplicated and compressed.</span></span> <span data-ttu-id="91b26-142">(Puede comparar estos dos números para hacerse una idea de la tasa de compresión). Para el almacenamiento principal y en la nube, las cantidades mostradas se basan en la frecuencia de seguimiento que configure.</span><span class="sxs-lookup"><span data-stu-id="91b26-142">(You can compare these two numbers to get an idea of the compression rate.) For both primary and cloud storage, the amounts shown are based on the tracking frequency you configure.</span></span> <span data-ttu-id="91b26-143">Por ejemplo, si elige una frecuencia de una semana, el gráfico mostrará datos para cada día de la semana anterior.</span><span class="sxs-lookup"><span data-stu-id="91b26-143">For example, if you choose a one week frequency, then the chart shows data for each day in the previous week.</span></span>

     <span data-ttu-id="91b26-144">Para ver la cantidad de almacenamiento en la nube consumido en el tiempo, seleccione la opción **ALMACENAMIENTO EN LA NUBE USADO** .</span><span class="sxs-lookup"><span data-stu-id="91b26-144">To see the amount of cloud storage consumed over time, select the **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="91b26-145">Para ver el almacenamiento total escrito por el host, seleccione las opciones **PRIMARY TIERED STORAGE USED** (Almacenamiento en capas principal usado) y **PRIMARY LOCALLY PINNED STORAGE USED** (Almacenamiento principal anclado localmente usado).</span><span class="sxs-lookup"><span data-stu-id="91b26-145">To see the total storage that has been written by the host, select the **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="91b26-146">Para más información, consulte [Uso del servicio StorSimple Device Manager para supervisar su dispositivo StorSimple](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="91b26-146">For more information, see [Use the StorSimple Device Manager service to monitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="91b26-147">El icono **Capacidad** muestra el almacenamiento principal que está aprovisionado y el almacenamiento restante que queda en el dispositivo, en relación con el almacenamiento total disponible para él.</span><span class="sxs-lookup"><span data-stu-id="91b26-147">The **Capacity** tile displays the primary storage that is provisioned and remaining across the device relative to the total storage available for the same.</span></span> <span data-ttu-id="91b26-148">**Aprovisionado** hace referencia a la cantidad de almacenamiento que está preparada y asignada para su uso. **Restante** hace referencia a la capacidad restante que se puede aprovisionar en este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91b26-148">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> 

    ![Icono de Uso](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="91b26-150">Haga clic en este icono para ver cómo se aprovisiona la capacidad a través de los volúmenes anclados localmente y en capas.</span><span class="sxs-lookup"><span data-stu-id="91b26-150">Click this tile to view how the capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="91b26-151">La capacidad **restante en capas** es la capacidad disponible que se puede aprovisionar, incluida la capacidad en la nube, mientras que la capacidad **restante en local** es la capacidad restante en los discos conectados a este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91b26-151">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this device.</span></span>

    ![Hacer clic en el gráfico de uso](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="91b26-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91b26-153">Next steps</span></span>
* <span data-ttu-id="91b26-154">Más información sobre la [hoja de resumen del servicio StorSimple](storsimple-8000-service-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="91b26-154">Learn more about the [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="91b26-155">Más información sobre el [uso del servicio StorSimple Device Manager para administrar su dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="91b26-155">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

