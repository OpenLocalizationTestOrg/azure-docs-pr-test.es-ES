---
title: Hoja de resumen de dispositivos de StorSimple Virtual Array | Microsoft Docs
description: "Describe la hoja de resumen de dispositivos para StorSimple Device Manager y explica cómo usarla para supervisar el estado de StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 35413d597c3b6b1c7600241a78572b63f982d175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="ee25b-103">Uso de la hoja de resumen de dispositivos para StorSimple Device Manager conectado a StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="ee25b-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="ee25b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ee25b-104">Overview</span></span>

<span data-ttu-id="ee25b-105">La hoja de dispositivos de StorSimple Device Manager proporciona una vista de resumen de una instancia de StorSimple Virtual Array que se registra con un determinado StorSimple Device Manager, y resalta los problemas en los dispositivos que necesitan la atención del administrador del sistema.</span><span class="sxs-lookup"><span data-stu-id="ee25b-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="ee25b-106">Este tutorial presenta la hoja de resumen de dispositivos, explica su contenido y su función, y describe las tareas que puede realizar desde esta hoja.</span><span class="sxs-lookup"><span data-stu-id="ee25b-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="ee25b-107">La hoja de resumen de dispositivos muestra la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="ee25b-107">The device summary blade displays the following information:</span></span>

![Panel del dispositivo](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="ee25b-109">Administración</span><span class="sxs-lookup"><span data-stu-id="ee25b-109">Management</span></span>

<span data-ttu-id="ee25b-110">En la hoja de dispositivos de StorSimple, verá las opciones para administrar el dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ee25b-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="ee25b-111">Verá los comandos de administración en la parte superior de la hoja y en el lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="ee25b-111">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="ee25b-112">Utilice estas opciones para agregar recursos compartidos o volúmenes, o bien actualizar o conmutar por error la matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="ee25b-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="ee25b-113">El área de información esencial captura algunas de las propiedades importantes, como el estado, el modelo y la versión del software, así como un vínculo a la **interfaz de usuario web** de la matriz.</span><span class="sxs-lookup"><span data-stu-id="ee25b-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span></span> <span data-ttu-id="ee25b-114">Si se encuentra en una red interna, puede iniciar directamente la [IU web local](storsimple-ova-web-ui-admin.md) para administrar la matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="ee25b-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span></span>

![Información esencial de dispositivos](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="ee25b-116">Resumen de dispositivos de StorSimple</span><span class="sxs-lookup"><span data-stu-id="ee25b-116">StorSimple device summary</span></span>

* <span data-ttu-id="ee25b-117">El icono **Alertas** proporciona una instantánea de todas las alertas activas para la matriz virtual, agrupadas por gravedad.</span><span class="sxs-lookup"><span data-stu-id="ee25b-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="ee25b-118">Haga clic en el icono para abrir la hoja **Alertas** y, a continuación, en una alerta concreta para ver detalles adicionales acerca de ella, incluidas las acciones recomendadas.</span><span class="sxs-lookup"><span data-stu-id="ee25b-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="ee25b-119">También puede desactivar la alerta si el problema se ha resuelto.</span><span class="sxs-lookup"><span data-stu-id="ee25b-119">You can also clear the alert if the issue has been resolved.</span></span>

* <span data-ttu-id="ee25b-120">El icono **Capacidad** muestra el almacenamiento principal que está aprovisionado y el almacenamiento restante que queda en el dispositivo virtual, en relación con el almacenamiento total disponible para él.</span><span class="sxs-lookup"><span data-stu-id="ee25b-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span></span> <span data-ttu-id="ee25b-121">**Aprovisionado** hace referencia a la cantidad de almacenamiento que está preparada y asignada para su uso. **Restante** hace referencia a la capacidad restante que se puede aprovisionar en este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ee25b-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="ee25b-122">La capacidad **restante en capas** es la capacidad disponible que se puede aprovisionar, incluida la capacidad en la nube, mientras que la capacidad **restante en local** es la capacidad restante en los discos conectados a esta matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="ee25b-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span></span>

* <span data-ttu-id="ee25b-123">En el gráfico **Uso**, puede ver el almacenamiento principal que se usa en su matriz virtual, así como el almacenamiento en la nube consumido durante los últimos 7 días, el período predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ee25b-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span></span> <span data-ttu-id="ee25b-124">Use la opción **Editar** en la esquina superior derecha del gráfico para elegir una escala de tiempo diferente.</span><span class="sxs-lookup"><span data-stu-id="ee25b-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>

* <span data-ttu-id="ee25b-125">El icono **Recursos compartidos** o **Volúmenes** proporciona un resumen del número de recursos compartidos o de volúmenes en el dispositivo, agrupados por estado.</span><span class="sxs-lookup"><span data-stu-id="ee25b-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="ee25b-126">Haga clic en el icono para abrir la hoja de lista **Recursos compartidos** o **Volúmenes** y, a continuación, en un recurso compartido o un volumen concreto para ver o modificar sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="ee25b-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span></span> <span data-ttu-id="ee25b-127">Para más información, consulte cómo [administrar recursos compartidos](storsimple-virtual-array-manage-shares.md) o cómo [administrar volúmenes](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="ee25b-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee25b-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee25b-128">Next steps</span></span>
<span data-ttu-id="ee25b-129">Obtenga información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="ee25b-129">Learn how to:</span></span>
- [<span data-ttu-id="ee25b-130">Administrar recursos compartidos en una instancia de StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="ee25b-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="ee25b-131">Administrar volúmenes en una instancia de StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="ee25b-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

