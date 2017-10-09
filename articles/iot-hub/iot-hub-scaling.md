---
title: ajuste de escala de centro de IoT aaaAzure | Documentos de Microsoft
description: "Cómo tooscale su toosupport de centro de IoT el rendimiento de los mensajes previsto. Incluye un resumen de rendimiento de hello admitido para cada nivel y las opciones de particionamiento."
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
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="0eba3-104">Escalado de la solución de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0eba3-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="0eba3-105">Centro de IoT de Azure puede admitir la tooa millones de dispositivos conectados al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="0eba3-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="0eba3-106">Para obtener más información, vea [Precios de IoT Hub][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="0eba3-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="0eba3-107">Cada unidad de IoT Hub permite un número determinado de mensajes diarios.</span><span class="sxs-lookup"><span data-stu-id="0eba3-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="0eba3-108">tooproperly escalar su solución, considere la posibilidad de su uso particular del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0eba3-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="0eba3-109">En concreto, tenga en cuenta el rendimiento de máximo de hello necesario para hello siguientes categorías de operaciones:</span><span class="sxs-lookup"><span data-stu-id="0eba3-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="0eba3-110">Mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="0eba3-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="0eba3-111">Mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="0eba3-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="0eba3-112">Operaciones de registro de identidad</span><span class="sxs-lookup"><span data-stu-id="0eba3-112">Identity registry operations</span></span>

<span data-ttu-id="0eba3-113">En información de rendimiento de toothis de adición, vea [centro de IoT cuotas y aceleradores] [ IoT Hub quotas and throttles] y diseñar la solución según corresponda.</span><span class="sxs-lookup"><span data-stu-id="0eba3-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="0eba3-114">Capacidad de procesamiento para los mensajes de dispositivo a nube y de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="0eba3-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="0eba3-115">Hola mejor manera toosize una solución de centro de IoT es tráfico de hello tooevaluate según una por unidad.</span><span class="sxs-lookup"><span data-stu-id="0eba3-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="0eba3-116">Los mensajes de dispositivo a nube siguen estas directrices de capacidad de procesamiento sostenida.</span><span class="sxs-lookup"><span data-stu-id="0eba3-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="0eba3-117">Nivel:</span><span class="sxs-lookup"><span data-stu-id="0eba3-117">Tier</span></span> | <span data-ttu-id="0eba3-118">Capacidad de procesamiento sostenida</span><span class="sxs-lookup"><span data-stu-id="0eba3-118">Sustained throughput</span></span> | <span data-ttu-id="0eba3-119">Velocidad de envío sostenida</span><span class="sxs-lookup"><span data-stu-id="0eba3-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0eba3-120">S1</span><span class="sxs-lookup"><span data-stu-id="0eba3-120">S1</span></span> |<span data-ttu-id="0eba3-121">Seguridad too1111 KB por minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="0eba3-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="0eba3-122">(1,5 GB/día/unidad)</span><span class="sxs-lookup"><span data-stu-id="0eba3-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="0eba3-123">Promedio de 278 mensajes/minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="0eba3-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="0eba3-124">(400 000 mensajes/día por unidad)</span><span class="sxs-lookup"><span data-stu-id="0eba3-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="0eba3-125">S2</span><span class="sxs-lookup"><span data-stu-id="0eba3-125">S2</span></span> |<span data-ttu-id="0eba3-126">Seguridad too16 MB por minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="0eba3-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="0eba3-127">(22,8 GB/día/unidad)</span><span class="sxs-lookup"><span data-stu-id="0eba3-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="0eba3-128">Promedio de 4167 mensajes/minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="0eba3-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="0eba3-129">(6 millones de mensajes/día por unidad)</span><span class="sxs-lookup"><span data-stu-id="0eba3-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="0eba3-130">S3</span><span class="sxs-lookup"><span data-stu-id="0eba3-130">S3</span></span> |<span data-ttu-id="0eba3-131">Seguridad too814 MB por minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="0eba3-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="0eba3-132">(1144,4 GB/día/unidad)</span><span class="sxs-lookup"><span data-stu-id="0eba3-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="0eba3-133">Promedio de 208.333 mensajes/minuto por unidad</span><span class="sxs-lookup"><span data-stu-id="0eba3-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="0eba3-134">(300 millones de mensajes/día por unidad)</span><span class="sxs-lookup"><span data-stu-id="0eba3-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="0eba3-135">Capacidad de procesamiento para las operaciones de registro de identidad</span><span class="sxs-lookup"><span data-stu-id="0eba3-135">Identity registry operation throughput</span></span>
<span data-ttu-id="0eba3-136">Las operaciones del registro de identidad de centro de IoT no deberían toobe operaciones en tiempo de ejecución, ya que son principalmente aprovisionamiento toodevice relacionado.</span><span class="sxs-lookup"><span data-stu-id="0eba3-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="0eba3-137">Vea las cifras de rendimiento de ráfaga específicas en [Cuotas y limitaciones de IoT Hub][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="0eba3-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="0eba3-138">Clave de particionamiento</span><span class="sxs-lookup"><span data-stu-id="0eba3-138">Sharding</span></span>
<span data-ttu-id="0eba3-139">Mientras que un único centro de IoT puede escalar toomillions de dispositivos, a veces la solución necesita características de rendimiento específicas que no puede garantizar un único centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0eba3-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="0eba3-140">En ese caso, se recomienda realizar particiones de los dispositivos en varios centros de IoT.</span><span class="sxs-lookup"><span data-stu-id="0eba3-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="0eba3-141">Varios centros de IoT suavizar ráfagas de tráfico y obtener el rendimiento necesario Hola o los tipos de operación que se necesitan.</span><span class="sxs-lookup"><span data-stu-id="0eba3-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0eba3-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0eba3-142">Next steps</span></span>
<span data-ttu-id="0eba3-143">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="0eba3-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0eba3-144">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="0eba3-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="0eba3-145">[Simular un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="0eba3-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
