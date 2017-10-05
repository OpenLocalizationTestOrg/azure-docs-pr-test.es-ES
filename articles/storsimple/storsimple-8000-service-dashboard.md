---
title: Uso del resumen del dispositivo de la serie StorSimple 8000 | Microsoft Docs
description: "Describe la hoja del resumen del servicio de StorSimple y explica cómo se usa para supervisar el estado de la solución de StorSimple."
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
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: d987a4ae170f21532a886552cbe1eb5a0d25fc3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-summary-blade-for-storsimple-8000-series-device"></a><span data-ttu-id="3baf9-103">Uso de la hoja de resumen del servicio del dispositivo de la serie StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="3baf9-103">Use the service summary blade for StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="3baf9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="3baf9-104">Overview</span></span>

<span data-ttu-id="3baf9-105">La hoja del resumen del servicio StorSimple Device Manager proporciona una vista resumida de todos los dispositivos conectados al servicio StorSimple Device Manager y resalta los que requieren la atención del administrador del sistema.</span><span class="sxs-lookup"><span data-stu-id="3baf9-105">The StorSimple Device Manager service summary blade provides a summary view of all the devices that are connected to the StorSimple Device Manager service, highlighting those devices that need a system administrator's attention.</span></span> <span data-ttu-id="3baf9-106">En este tutorial se presenta la hoja de resumen del servicio, se explica el contenido y la función del panel y se describen las tareas que se pueden realizar desde esta página.</span><span class="sxs-lookup"><span data-stu-id="3baf9-106">This tutorial introduces the service summary blade, explains the dashboard content and function, and describes the tasks that you can perform from this page.</span></span>

![Resumen del servicio](./media/storsimple-8000-service-dashboard/service-summary1.png)


## <a name="management-commands"></a><span data-ttu-id="3baf9-108">Comandos de administración</span><span class="sxs-lookup"><span data-stu-id="3baf9-108">Management commands</span></span>

<span data-ttu-id="3baf9-109">En la hoja de resumen del servicio de StorSimple se ven las opciones para administrar tanto el servicio StorSimple Device Manager como los dispositivos de la serie StorSimple 8000 registrados en dicho servicio.</span><span class="sxs-lookup"><span data-stu-id="3baf9-109">In the StorSimple service summary blade, you see the options for managing your StorSimple Device Manager service and the StorSimple 8000 series devices registered to this service.</span></span> <span data-ttu-id="3baf9-110">Verá los comandos de administración en la parte superior de la hoja y en el lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="3baf9-110">You see the management commands across the top of the blade and on the left side.</span></span>

![Barra de comandos](./media/storsimple-8000-service-dashboard/service-summary2.png)

<span data-ttu-id="3baf9-112">Estas opciones se pueden usar para realizar diversas operaciones tales como agregar recursos compartidos o volúmenes, o supervisar los distintos trabajos que se ejecutan en los dispositivos de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3baf9-112">Use these options to perform various operations such as add shares or volumes, or monitor the various jobs running on the StorSimple devices.</span></span>


## <a name="essentials"></a><span data-ttu-id="3baf9-113">Essentials</span><span class="sxs-lookup"><span data-stu-id="3baf9-113">Essentials</span></span>

<span data-ttu-id="3baf9-114">El área de información esencial captura algunas de las propiedades importantes, como el grupo de recursos, la ubicación y la suscripción en la que se creó StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="3baf9-114">The essentials area captures some of the important properties such as, the resource group, location, and subscription in which your StorSimple Device Manager was created.</span></span>

![Essentials](./media/storsimple-8000-service-dashboard/service-summary3.png)

## <a name="storsimple-device-manager-service-summary"></a><span data-ttu-id="3baf9-116">Resumen del servicio StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="3baf9-116">StorSimple Device Manager service summary</span></span>

* <span data-ttu-id="3baf9-117">El icono **Alertas** (Alertas) proporciona una instantánea de todas las alertas activas en todos los dispositivos virtuales, agrupadas por gravedad.</span><span class="sxs-lookup"><span data-stu-id="3baf9-117">The **Alerts** tile provides a snapshot of all the active alerts across all devices, grouped by alert severity.</span></span>

    ![Icono Alerts (Alertas)](./media/storsimple-8000-service-dashboard/service-summary4.png)

    <span data-ttu-id="3baf9-119">Si hace clic en el icono, se abrirá la hoja **Alertas**, en la que puede hacer clic en una alerta individual para ver detalles adicionales acerca de ella, incluidas las acciones recomendadas.</span><span class="sxs-lookup"><span data-stu-id="3baf9-119">Clicking the tile opens the **Alerts** blade, where you can click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="3baf9-120">También puede desactivar la alerta si el problema se ha resuelto.</span><span class="sxs-lookup"><span data-stu-id="3baf9-120">You can also clear the alert if the issue has been resolved.</span></span>

    ![Hacer clic en el icono de alertas](./media/storsimple-8000-service-dashboard/service-summary8.png)

* <span data-ttu-id="3baf9-122">El icono **Capacidad** muestra tanto el almacenamiento principal que se aprovisiona como el restante que queda en todos los dispositivos, en comparación con el almacenamiento total disponible en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3baf9-122">The **Capacity** tile displays shows the primary storage that is provisioned and remaining across all devices relative to the total storage available across all devices.</span></span> <span data-ttu-id="3baf9-123">**Aprovisionado** hace referencia a la cantidad de almacenamiento que está preparada y asignada para su uso. **Restante** hace referencia a la capacidad restante que se puede aprovisionar en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3baf9-123">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across all devices.</span></span>

    ![Icono Capacity (Capacidad)](./media/storsimple-8000-service-dashboard/service-summary6.png)

    <span data-ttu-id="3baf9-125">La capacidad **en capas restante** es la capacidad disponible que se puede aprovisionar incluyendo la nube, mientras que la capacidad **local restante** es la capacidad que queda en los discos conectados a los dispositivos de la serie StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="3baf9-125">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to the StorSimple 8000 series devices.</span></span>


* <span data-ttu-id="3baf9-126">En el gráfico **Uso**, puede ver las métricas pertinentes para los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3baf9-126">In the **Usage** chart, you can see the relevant metrics for your devices.</span></span> <span data-ttu-id="3baf9-127">Puede ver el almacenamiento principal que se usa en todos los dispositivos, así como el almacenamiento en la nube que han consumido los dispositivos durante los últimos 7 días, el período de tiempo predeterminado.</span><span class="sxs-lookup"><span data-stu-id="3baf9-127">You can view the primary storage used across all devices, and the cloud storage consumed by devices over the past 7 days, the default time period.</span></span> 

    ![Icono de Uso](./media/storsimple-8000-service-dashboard/service-summary7.png) 

    <span data-ttu-id="3baf9-129">Para elegir otra escala de tiempo, ese la opción **Editar** de la esquina superior derecha del gráfico.</span><span class="sxs-lookup"><span data-stu-id="3baf9-129">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![Hacer clic en el icono de uso](./media/storsimple-8000-service-dashboard/service-summary10.png)

     ![Exportar datos de un gráfico](./media/storsimple-8000-service-dashboard/service-summary11.png)

* <span data-ttu-id="3baf9-132">El icono **Devices** (Dispositivos) proporciona un resumen del número de dispositivos de la serie StorSimple 8000 en StorSimple Device Manager agrupados por el estado del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3baf9-132">The **Devices** tile provides a summary of the number of StorSimple 8000 series devices in your StorSimple Device Manager grouped by device status.</span></span> 

    ![Icono Devices (Dispositivos)](./media/storsimple-8000-service-dashboard/service-summary5.png)

    <span data-ttu-id="3baf9-134">Haga clic en este icono para abrir la hoja de la lista **Dispositivos** y, a continuación, haga clic en un dispositivo individual para profundizar sobre el resumen específico del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3baf9-134">Click this tile to open the **Devices** list blade and then click an individual device to drill into the device summary specific to the device.</span></span> <span data-ttu-id="3baf9-135">También puede realizar acciones específicas del dispositivo desde una hoja de resumen de un dispositivo determinado.</span><span class="sxs-lookup"><span data-stu-id="3baf9-135">You can also perform device-specific actions from a given device summary blade.</span></span> <span data-ttu-id="3baf9-136">Para más información acerca de la hoja de resumen del dispositivo, vaya a [Hoja de resumen de dispositivo](storsimple-8000-device-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="3baf9-136">For more information about the device summary blade, go to [Device summary blade](storsimple-8000-device-dashboard.md).</span></span>

    ![Hacer clic en icono de dispositivos](./media/storsimple-8000-service-dashboard/service-summary9.png)

## <a name="view-the-activity-logs"></a><span data-ttu-id="3baf9-138">Visualizar los registros de actividad</span><span class="sxs-lookup"><span data-stu-id="3baf9-138">View the activity logs</span></span>

<span data-ttu-id="3baf9-139">Para ver las distintas operaciones que se llevan a cabo en StorSimple Device Manager, haga clic en el vínculo **Registros de actividad** en el lado izquierdo de la hoja de resumen del servicio StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3baf9-139">To view the various operations carried out within your StorSimple Device Manager, click the **Activity logs** link on the left side of your StorSimple service summary blade.</span></span> <span data-ttu-id="3baf9-140">Esto le llevará a la hoja **Registros de actividad**, donde puede ver un resumen de las operaciones recientes que se llevan a cabo.</span><span class="sxs-lookup"><span data-stu-id="3baf9-140">This takes you to the **Activity logs** blade, where you can see a summary of the recent operations carried out.</span></span>

![Registros de actividad](./media/storsimple-8000-service-dashboard/activity-logs1.png)
## <a name="next-steps"></a><span data-ttu-id="3baf9-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3baf9-142">Next steps</span></span>

* <span data-ttu-id="3baf9-143">Obtenga más información acerca de cómo [usar el servicio StorSimple Device Manager para administrar cualquier dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="3baf9-143">Learn more about how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

