---
title: "Información sobre la mensajería de IoT Hub de Azure | Microsoft Docs"
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
ms.openlocfilehash: f54398d7ac46bf178d2bb603669b399d25370736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="e4c87-104">Mensajería de dispositivo a nube y de nube a dispositivo con IoT Hub</span><span class="sxs-lookup"><span data-stu-id="e4c87-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="e4c87-105">Use la mensajería de IoT Hub para comunicarse con los dispositivos de los siguientes modos:</span><span class="sxs-lookup"><span data-stu-id="e4c87-105">Use IoT Hub messaging to communicate with your devices by:</span></span>

* <span data-ttu-id="e4c87-106">Enviando mensajes [de dispositivo a nube][lnk-d2c] desde los dispositivos al back-end de su solución.</span><span class="sxs-lookup"><span data-stu-id="e4c87-106">Sending [device-to-cloud][lnk-d2c] messages from your devices to your solution back end.</span></span>
* <span data-ttu-id="e4c87-107">Enviando mensajes [de nube a dispositivo][lnk-c2d] desde la solución de back-end a sus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e4c87-107">Sending [cloud-to-device][lnk-c2d] messages from the solution back end to your devices.</span></span>

<span data-ttu-id="e4c87-108">Las propiedades básicas de la funcionalidad de mensajería del Centro de IoT son la confiabilidad y durabilidad de los mensajes.</span><span class="sxs-lookup"><span data-stu-id="e4c87-108">Core properties of IoT Hub messaging functionality are the reliability and durability of messages.</span></span> <span data-ttu-id="e4c87-109">Estas propiedades permiten la resistencia a la conectividad intermitente en el dispositivo y a los picos de carga del procesamiento de eventos en la nube.</span><span class="sxs-lookup"><span data-stu-id="e4c87-109">These properties enable resilience to intermittent connectivity on the device side, and to load spikes in event processing on the cloud side.</span></span> <span data-ttu-id="e4c87-110">El Centro de IoT implementa *al menos una vez* garantías de entrega para la mensajería del dispositivo a la nube y de la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e4c87-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="e4c87-111">Para obtener una introducción a las funciones de IoT Hub, consulte los artículos [Azure y el Internet de las cosas][lnk-azure-iot] e [Introducción al servicio Azure IoT Hub][lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="e4c87-111">For an introduction to the capabilities of IoT Hub, see the articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of the Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-to-use-iot-hub-messaging"></a><span data-ttu-id="e4c87-112">Cuándo se debe usar la mensajería de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="e4c87-112">When to use IoT Hub messaging</span></span>

<span data-ttu-id="e4c87-113">Los mensajes de dispositivo a nube se utilizan para enviar telemetría y alertas de series temporales desde la aplicación para dispositivo y los mensajes de nube a dispositivo, para las notificaciones unidireccionales a su aplicación para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e4c87-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications to your device app.</span></span>

* <span data-ttu-id="e4c87-114">Si duda entre el uso de mensajes de dispositivo a nube, propiedades notificadas o carga de archivos, consulte la [Guía de comunicación de dispositivo a nube][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="e4c87-114">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="e4c87-115">Si duda entre el uso de mensajes de nube a dispositivo, propiedades deseadas o métodos directos, consulte la [Guía de comunicación de nube a dispositivo][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="e4c87-115">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4c87-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4c87-116">Next steps</span></span>

* <span data-ttu-id="e4c87-117">Obtenga más información acerca de la [mensajería de dispositivo a nube][lnk-d2c] de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e4c87-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="e4c87-118">Obtenga más información acerca de la [mensajería de nube a dispositivo][lnk-c2d] de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e4c87-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md