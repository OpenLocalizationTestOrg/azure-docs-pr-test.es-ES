---
title: Escalado de Azure IoT Hub | Microsoft Docs
description: "Cómo escalar el centro de IoT Hub para respaldar el rendimiento de los mensajes previsto. Incluye un resumen del rendimiento admitido para cada nivel y opciones de particionamiento."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2cb263103da05b10c24aab71d81c43eb25987565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="12207-104">Escalado de la solución de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="12207-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="12207-105">El Centro de IoT de Azure puede admitir hasta un millón de dispositivos conectados simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="12207-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span></span> <span data-ttu-id="12207-106">Para obtener más información, vea [Precios de IoT Hub][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="12207-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="12207-107">Cada unidad de IoT Hub permite un número determinado de mensajes diarios.</span><span class="sxs-lookup"><span data-stu-id="12207-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="12207-108">Para escalar correctamente su solución, debe tener en cuenta el uso particular que haga de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12207-108">To properly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="12207-109">En concreto, tenga en cuenta la capacidad de procesamiento máxima requerida para las siguientes categorías de operaciones:</span><span class="sxs-lookup"><span data-stu-id="12207-109">In particular, consider the required peak throughput for the following categories of operations:</span></span>

* <span data-ttu-id="12207-110">Mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="12207-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="12207-111">Mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="12207-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="12207-112">Operaciones de registro de identidad</span><span class="sxs-lookup"><span data-stu-id="12207-112">Identity registry operations</span></span>

<span data-ttu-id="12207-113">Además de esta información sobre la capacidad de procesamiento, vea [Cuotas y limitaciones de IoT Hub][IoT Hub quotas and throttles] y diseñe su solución en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="12207-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="12207-114">Capacidad de procesamiento para los mensajes de dispositivo a nube y de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="12207-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="12207-115">La mejor forma de dimensionar una solución de Centro de IoT es evaluar el tráfico en cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12207-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span></span>

<span data-ttu-id="12207-116">Los mensajes de dispositivo a nube siguen estas directrices de capacidad de procesamiento sostenida.</span><span class="sxs-lookup"><span data-stu-id="12207-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="12207-117">Nivel:</span><span class="sxs-lookup"><span data-stu-id="12207-117">Tier</span></span> | <span data-ttu-id="12207-118">Capacidad de procesamiento sostenida</span><span class="sxs-lookup"><span data-stu-id="12207-118">Sustained throughput</span></span> | <span data-ttu-id="12207-119">Velocidad de envío sostenida</span><span class="sxs-lookup"><span data-stu-id="12207-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12207-120">S1</span><span class="sxs-lookup"><span data-stu-id="12207-120">S1</span></span> |<span data-ttu-id="12207-121">Hasta 1111 KB/minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="12207-121">Up to 1111 KB/minute per unit</span></span><br/><span data-ttu-id="12207-122">(1,5 GB/día/unidad)</span><span class="sxs-lookup"><span data-stu-id="12207-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="12207-123">Promedio de 278 mensajes/minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="12207-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="12207-124">(400 000 mensajes/día por unidad)</span><span class="sxs-lookup"><span data-stu-id="12207-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="12207-125">S2</span><span class="sxs-lookup"><span data-stu-id="12207-125">S2</span></span> |<span data-ttu-id="12207-126">Hasta 16 MB/minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="12207-126">Up to 16 MB/minute per unit</span></span><br/><span data-ttu-id="12207-127">(22,8 GB/día/unidad)</span><span class="sxs-lookup"><span data-stu-id="12207-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="12207-128">Promedio de 4167 mensajes/minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="12207-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="12207-129">(6 millones de mensajes/día por unidad)</span><span class="sxs-lookup"><span data-stu-id="12207-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="12207-130">S3</span><span class="sxs-lookup"><span data-stu-id="12207-130">S3</span></span> |<span data-ttu-id="12207-131">Hasta 814 MB/minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="12207-131">Up to 814 MB/minute per unit</span></span><br/><span data-ttu-id="12207-132">(1144,4 GB/día/unidad)</span><span class="sxs-lookup"><span data-stu-id="12207-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="12207-133">Promedio de 208.333 mensajes/minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="12207-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="12207-134">(300 millones de mensajes/día por unidad)</span><span class="sxs-lookup"><span data-stu-id="12207-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="12207-135">Capacidad de procesamiento para las operaciones de registro de identidad</span><span class="sxs-lookup"><span data-stu-id="12207-135">Identity registry operation throughput</span></span>
<span data-ttu-id="12207-136">Las operaciones de registro de identidad de IoT Hub no deberían ser operaciones en tiempo de ejecución porque tienen que ver principalmente con el aprovisionamiento de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="12207-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span></span>

<span data-ttu-id="12207-137">Vea las cifras de rendimiento de ráfaga específicas en [Cuotas y limitaciones de IoT Hub][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="12207-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="12207-138">Clave de particionamiento</span><span class="sxs-lookup"><span data-stu-id="12207-138">Sharding</span></span>
<span data-ttu-id="12207-139">Aunque un único Centro de IoT puede escalarse a millones de dispositivos, a veces la solución requiere características de rendimiento específicas que un único Centro de IoT no puede garantizar.</span><span class="sxs-lookup"><span data-stu-id="12207-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="12207-140">En ese caso, se recomienda realizar particiones de los dispositivos en varios centros de IoT.</span><span class="sxs-lookup"><span data-stu-id="12207-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="12207-141">Varios centros de IoT suavizan las ráfagas de tráfico y obtienen el rendimiento necesario o las velocidades de funcionamiento necesarias.</span><span class="sxs-lookup"><span data-stu-id="12207-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12207-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12207-142">Next steps</span></span>
<span data-ttu-id="12207-143">Para explorar aún más las funcionalidades de IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="12207-143">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="12207-144">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="12207-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="12207-145">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="12207-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
