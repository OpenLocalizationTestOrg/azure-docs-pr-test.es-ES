---
title: "mensajería de aaaUnderstand centro de IoT de Azure | Documentos de Microsoft"
description: "Guía del desarrollador: mensajería de dispositivo a nube y de nube a dispositivo con IoT Hub Incluye información sobre los formatos de mensaje y protocolos de comunicación compatibles."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="9afa0-104">Mensajería de dispositivo a nube y de nube a dispositivo con IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9afa0-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="9afa0-105">Usar el centro de IoT mensajería toocommunicate con los dispositivos por:</span><span class="sxs-lookup"><span data-stu-id="9afa0-105">Use IoT Hub messaging toocommunicate with your devices by:</span></span>

* <span data-ttu-id="9afa0-106">Enviar [dispositivo a la nube] [ lnk-d2c] mensajes de la solución de tooyour dispositivos back-end.</span><span class="sxs-lookup"><span data-stu-id="9afa0-106">Sending [device-to-cloud][lnk-d2c] messages from your devices tooyour solution back end.</span></span>
* <span data-ttu-id="9afa0-107">Enviar [en la nube al dispositivo] [ lnk-c2d] mensajes de nuevo la solución Hola finalización tooyour dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9afa0-107">Sending [cloud-to-device][lnk-c2d] messages from hello solution back end tooyour devices.</span></span>

<span data-ttu-id="9afa0-108">Propiedades básicas de funcionalidad de mensajería del centro de IoT son Hola fiabilidad y durabilidad de los mensajes.</span><span class="sxs-lookup"><span data-stu-id="9afa0-108">Core properties of IoT Hub messaging functionality are hello reliability and durability of messages.</span></span> <span data-ttu-id="9afa0-109">Estas propiedades permiten conectividad toointermittent de resistencia en el lado del dispositivo de Hola y tooload tiene un pico en el lado de la nube de Hola de procesamiento de eventos.</span><span class="sxs-lookup"><span data-stu-id="9afa0-109">These properties enable resilience toointermittent connectivity on hello device side, and tooload spikes in event processing on hello cloud side.</span></span> <span data-ttu-id="9afa0-110">El Centro de IoT implementa *al menos una vez* garantías de entrega para la mensajería del dispositivo a la nube y de la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9afa0-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="9afa0-111">Para una introducción toohello las capacidades de centro de IoT, vea los artículos de hello [Azure y Internet de las cosas] [ lnk-azure-iot] y [información general de hello servicio del centro de IoT de Azure] [lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="9afa0-111">For an introduction toohello capabilities of IoT Hub, see hello articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of hello Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-toouse-iot-hub-messaging"></a><span data-ttu-id="9afa0-112">Cuando toouse centro de IoT mensajería</span><span class="sxs-lookup"><span data-stu-id="9afa0-112">When toouse IoT Hub messaging</span></span>

<span data-ttu-id="9afa0-113">Usar mensajes de dispositivo a la nube para enviar telemetría de series de tiempo y alertas desde la aplicación de dispositivo y los mensajes en la nube al dispositivo para notificaciones unidireccional tooyour del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9afa0-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications tooyour device app.</span></span>

* <span data-ttu-id="9afa0-114">Consulte demasiado[Guía de comunicación de dispositivos a la nube] [ lnk-d2c-guidance] si está en duda entre el uso de mensajes del dispositivo a la nube, las propiedades notificados o cargar el archivo.</span><span class="sxs-lookup"><span data-stu-id="9afa0-114">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="9afa0-115">Consulte demasiado[orientación para la comunicación en la nube para dispositivos] [ lnk-c2d-guidance] si está en duda entre el uso de mensajes en la nube al dispositivo, deseados propiedades o métodos directos.</span><span class="sxs-lookup"><span data-stu-id="9afa0-115">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9afa0-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9afa0-116">Next steps</span></span>

* <span data-ttu-id="9afa0-117">Obtenga más información acerca de la [mensajería de dispositivo a nube][lnk-d2c] de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9afa0-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="9afa0-118">Obtenga más información acerca de la [mensajería de nube a dispositivo][lnk-c2d] de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9afa0-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md