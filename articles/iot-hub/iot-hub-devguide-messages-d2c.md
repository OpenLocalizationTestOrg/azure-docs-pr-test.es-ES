---
title: "Información sobre la mensajería de dispositivo a nube de Azure IoT Hub | Microsoft Docs"
description: "Guía del desarrollador: cómo utilizar la mensajería de dispositivo a nube con IoT Hub. Incluye información acerca del envío de datos de telemetría y datos sin telemetría, y del uso del enrutamiento para entregar los mensajes."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: d856e26084ee79386a2e8e0e527804bda86b477b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="send-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="4c107-104">Envío de mensajes de dispositivo a nube a IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4c107-104">Send device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="4c107-105">Para enviar alertas y telemetría de series temporales desde los dispositivos a su back-end de soluciones, envíe mensajes de dispositivo a nube desde el dispositivo a su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4c107-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span></span> <span data-ttu-id="4c107-106">Para obtener una explicación de otras opciones de dispositivo a nube compatibles con IoT Hub, consulte [Guía de comunicación de dispositivo a nube][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="4c107-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="4c107-107">Los mensajes del dispositivo a la nube se envían a través de un punto de conexión orientado al dispositivo (**/devices/{IdDeDispositivo}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="4c107-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="4c107-108">Después, las reglas de enrutamiento enrutan los mensajes a uno de los puntos de conexión orientado al servicio en su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4c107-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="4c107-109">Las reglas de enrutamiento utilizan los encabezados y el cuerpo de los mensajes de dispositivo a nube que fluyen a través de su centro para determinar dónde enrutarlos.</span><span class="sxs-lookup"><span data-stu-id="4c107-109">Routing rules use the headers and body of the device-to-cloud messages flowing through your hub to determine where to route them.</span></span> <span data-ttu-id="4c107-110">De forma predeterminada, los mensajes se enrutan al punto de conexión orientado al servicio integrado (**/messages/events**), que es compatible con [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="4c107-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="4c107-111">Por lo tanto, puede usar [los SDK e integración de Event Hubs][lnk-compatible-endpoint] estándar para recibir mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="4c107-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="4c107-112">IoT Hub implementa mensajería de dispositivo a nube mediante un patrón de mensajería de streaming.</span><span class="sxs-lookup"><span data-stu-id="4c107-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="4c107-113">Los mensajes de dispositivo a nube de IoT Hub son más parecidos a *eventos* de [Event Hubs][lnk-event-hubs] que a *mensajes* de [Service Bus][lnk-servicebus] en que hay un gran volumen de eventos que se pasan a través del servicio que pueden leer varios lectores.</span><span class="sxs-lookup"><span data-stu-id="4c107-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span></span>

<span data-ttu-id="4c107-114">La mensajería de dispositivo a nube con IoT Hub tiene las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="4c107-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span></span>

* <span data-ttu-id="4c107-115">Los mensajes de dispositivo a nube son duraderos y se conservan en el punto de conexión **messages/events** predeterminado de una instancia de IoT Hub hasta siete días.</span><span class="sxs-lookup"><span data-stu-id="4c107-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span></span>
* <span data-ttu-id="4c107-116">Los mensajes de dispositivo a nube pueden tener como máximo 256 KB y se pueden agrupar en lotes para optimizar los envíos.</span><span class="sxs-lookup"><span data-stu-id="4c107-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span></span> <span data-ttu-id="4c107-117">Los lotes pueden tener un tamaño máximo de 256 KB.</span><span class="sxs-lookup"><span data-stu-id="4c107-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="4c107-118">Como se explica en la sección [Control del acceso a IoT Hub][lnk-devguide-security], IoT Hub habilita la autenticación y el control de acceso por dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4c107-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="4c107-119">IoT Hub le permite crear hasta 10 puntos de conexión personalizados.</span><span class="sxs-lookup"><span data-stu-id="4c107-119">IoT Hub allows you to create up to 10 custom endpoints.</span></span> <span data-ttu-id="4c107-120">Los mensajes se entregan a los puntos de conexión según las rutas configuradas en su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4c107-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="4c107-121">Para obtener más información, consulte [Reglas de enrutamiento](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="4c107-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="4c107-122">IoT Hub habilita millones de dispositivos conectados al mismo tiempo (consulte [Cuotas y limitación][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="4c107-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="4c107-123">IoT Hub no permite el particionamiento arbitrario.</span><span class="sxs-lookup"><span data-stu-id="4c107-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="4c107-124">Los mensajes de dispositivo a nube se dividen en particiones en función de su valor de **deviceId**de origen.</span><span class="sxs-lookup"><span data-stu-id="4c107-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="4c107-125">Para obtener más información acerca de las diferencias entre Azure IoT Hub y los servicios de Event Hubs, consulte [Comparación entre IoT Hub de Azure y Azure Event Hubs][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="4c107-125">For more information about the differences between the IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="4c107-126">Envío de tráfico sin telemetría</span><span class="sxs-lookup"><span data-stu-id="4c107-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="4c107-127">A menudo, además de los puntos de datos de telemetría, los dispositivos envían mensajes y solicitudes que requieren la ejecución y el control en el back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="4c107-127">Often, in addition to telemetry data points, devices send messages and requests that require separate execution and handling in the solution back end.</span></span> <span data-ttu-id="4c107-128">Por ejemplo, las alertas críticas que deben desencadenar una acción específica en el back-end.</span><span class="sxs-lookup"><span data-stu-id="4c107-128">For example, critical alerts that must trigger a specific action in the back end.</span></span> <span data-ttu-id="4c107-129">Puede escribir fácilmente una [regla de enrutamiento][lnk-devguide-custom] para enviar estos tipos de mensajes a un punto de conexión dedicado para su procesamiento según un encabezado en el mensaje o un valor en el cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="4c107-129">You can easily write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span></span>

<span data-ttu-id="4c107-130">Para más información sobre la mejor manera de procesar este tipo de mensaje, consulte [Tutorial: procesamiento de mensajes del dispositivo a la nube de IoT Hub][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="4c107-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="4c107-131">Enrutamiento de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="4c107-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="4c107-132">Tiene dos opciones para enrutar mensajes de dispositivo a nube a las aplicaciones del back-end:</span><span class="sxs-lookup"><span data-stu-id="4c107-132">You have two options for routing device-to-cloud messages to your back-end apps:</span></span>

* <span data-ttu-id="4c107-133">Use el [punto de conexión compatible con Event Hub][lnk-compatible-endpoint] integrado para permitir que las aplicaciones de back-end lean los mensajes de dispositivo a nube recibidos por el centro.</span><span class="sxs-lookup"><span data-stu-id="4c107-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span></span> <span data-ttu-id="4c107-134">Para obtener información sobre el punto de conexión compatible con Event Hub integrado, consulte [Lectura de mensajes de dispositivo a nube desde el punto de conexión integrado][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="4c107-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="4c107-135">Utilice reglas de enrutamiento para enviar mensajes a puntos de conexión personalizados en su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="4c107-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span></span> <span data-ttu-id="4c107-136">Los puntos de conexión personalizados permiten que las aplicaciones back-end lean mensajes de dispositivo a nube con Event Hubs, colas de Service Bus o temas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4c107-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="4c107-137">Para obtener información acerca de los puntos de conexión personalizados y de enrutamientos, consulte [Uso de puntos de conexión y reglas de enrutamiento personalizados para mensajes de dispositivos a la nube][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="4c107-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="4c107-138">Propiedades contra la suplantación</span><span class="sxs-lookup"><span data-stu-id="4c107-138">Anti-spoofing properties</span></span>

<span data-ttu-id="4c107-139">Para evitar la suplantación de dispositivos en los mensajes de dispositivo a nube, el Centro de IoT marca todos los mensajes con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="4c107-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span></span>

* <span data-ttu-id="4c107-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="4c107-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="4c107-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="4c107-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="4c107-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="4c107-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="4c107-143">Las dos primeras contienen los valores **deviceId** y **generationId** del dispositivo de origen, tal como se indicó en [Propiedades de identidad del dispositivo][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="4c107-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="4c107-144">La propiedad **ConnectionAuthMethod** contiene un objeto JSON serializado con las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="4c107-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="4c107-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4c107-145">Next steps</span></span>

<span data-ttu-id="4c107-146">Para obtener información sobre los SDK que puede utilizar para enviar mensajes de dispositivo a nube, consulte [SDK de Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="4c107-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="4c107-147">El tutorial de [Introducción][lnk-get-started] muestra cómo enviar mensajes de dispositivo a nube desde dispositivos físicos y simulados.</span><span class="sxs-lookup"><span data-stu-id="4c107-147">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="4c107-148">Para obtener más información, vea el tutorial [Procesamiento de mensajes de dispositivo a nube de IoT Hub mediante rutas][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="4c107-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
