---
title: "mensajería de dispositivo para la nube de Azure IoT Hub aaaUnderstand | Documentos de Microsoft"
description: "Guía del desarrollador - cómo toouse dispositivo a la nube con el centro de IoT de mensajería. Incluye información sobre enviar datos de telemetría y no telemtry y el uso de enrutar los mensajes toodeliver."
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="0dede-104">Enviar mensajes del dispositivo a la nube tooIoT concentrador</span><span class="sxs-lookup"><span data-stu-id="0dede-104">Send device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="0dede-105">toosend telemetría de series temporales y las alertas de los dispositivos tooyour solución back-end, enviar mensajes de dispositivo a la nube desde el centro de IoT tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0dede-105">toosend time-series telemetry and alerts from your devices tooyour solution back end, send device-to-cloud messages from your device tooyour IoT hub.</span></span> <span data-ttu-id="0dede-106">Para obtener una explicación de otras opciones de dispositivo a nube compatibles con IoT Hub, consulte [Guía de comunicación de dispositivo a nube][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="0dede-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="0dede-107">Los mensajes del dispositivo a la nube se envían a través de un punto de conexión orientado al dispositivo (**/devices/{IdDeDispositivo}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="0dede-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="0dede-108">Reglas de enrutamiento, a continuación, enrutar el tooone de mensajes de extremos de acceso de servicio de hello en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0dede-108">Routing rules then route your messages tooone of hello service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="0dede-109">Las reglas de enrutamiento utilizan encabezados de Hola y el cuerpo de mensajes del dispositivo a la nube de Hola que fluyen a través de su toodetermine de base de datos central donde tooroute ellos.</span><span class="sxs-lookup"><span data-stu-id="0dede-109">Routing rules use hello headers and body of hello device-to-cloud messages flowing through your hub toodetermine where tooroute them.</span></span> <span data-ttu-id="0dede-110">De forma predeterminada, los mensajes son el punto de conexión de toohello enrutado integrados a nivel de servicio (**mensajes de eventos**), que es compatible con [centros de eventos][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="0dede-110">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="0dede-111">Por lo tanto, puede usar el estándar de [integración de los centros de eventos y los SDK] [ lnk-compatible-endpoint] tooreceive mensajes de dispositivo para la nube en la solución de back-end.</span><span class="sxs-lookup"><span data-stu-id="0dede-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] tooreceive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="0dede-112">IoT Hub implementa mensajería de dispositivo a nube mediante un patrón de mensajería de streaming.</span><span class="sxs-lookup"><span data-stu-id="0dede-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="0dede-113">Mensajes de dispositivo para la nube del centro de IoT son más parecidos a [centros de eventos] [ lnk-event-hubs] *eventos* de [Service Bus] [ lnk-servicebus] *mensajes* en que hay un gran volumen de eventos que se pasan a través del servicio Hola que puede leerse mediante varios lectores.</span><span class="sxs-lookup"><span data-stu-id="0dede-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through hello service that can be read by multiple readers.</span></span>

<span data-ttu-id="0dede-114">Dispositivo a la nube con el centro de IoT de mensajería tiene Hola siguientes características:</span><span class="sxs-lookup"><span data-stu-id="0dede-114">Device-to-cloud messaging with IoT Hub has hello following characteristics:</span></span>

* <span data-ttu-id="0dede-115">Mensajes del dispositivo a la nube son durables y retenido en valor predeterminado de un centro de IoT **mensajes de eventos** punto de conexión para los días de tooseven.</span><span class="sxs-lookup"><span data-stu-id="0dede-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up tooseven days.</span></span>
* <span data-ttu-id="0dede-116">Mensajes del dispositivo a la nube pueden ser como máximo de 256 KB y se pueden agrupar en lotes toooptimize envía.</span><span class="sxs-lookup"><span data-stu-id="0dede-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches toooptimize sends.</span></span> <span data-ttu-id="0dede-117">Los lotes pueden tener un tamaño máximo de 256 KB.</span><span class="sxs-lookup"><span data-stu-id="0dede-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="0dede-118">Como se explica en hello [tooIoT de acceso de Control concentrador] [ lnk-devguide-security] sección, centro de IoT habilita por dispositivo autenticación y control de acceso.</span><span class="sxs-lookup"><span data-stu-id="0dede-118">As explained in hello [Control access tooIoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="0dede-119">Centro de IoT permite toocreate too10 personalizado extremos.</span><span class="sxs-lookup"><span data-stu-id="0dede-119">IoT Hub allows you toocreate up too10 custom endpoints.</span></span> <span data-ttu-id="0dede-120">Los mensajes se entregan los puntos de conexión de toohello basados en rutas configuradas en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0dede-120">Messages are delivered toohello endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="0dede-121">Para obtener más información, consulte [Reglas de enrutamiento](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="0dede-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="0dede-122">IoT Hub habilita millones de dispositivos conectados al mismo tiempo (consulte [Cuotas y limitación][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="0dede-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="0dede-123">IoT Hub no permite el particionamiento arbitrario.</span><span class="sxs-lookup"><span data-stu-id="0dede-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="0dede-124">Los mensajes de dispositivo a nube se dividen en particiones en función de su valor de **deviceId**de origen.</span><span class="sxs-lookup"><span data-stu-id="0dede-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="0dede-125">Para obtener más información acerca de las diferencias de hello entre Hola centro de IoT y los servicios de los centros de eventos, vea [comparación al centro de IoT de Azure y concentradores de eventos de Azure][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="0dede-125">For more information about hello differences between hello IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="0dede-126">Envío de tráfico sin telemetría</span><span class="sxs-lookup"><span data-stu-id="0dede-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="0dede-127">A menudo, además los puntos de datos de tootelemetry, dispositivos la envían mensajes y las solicitudes que requieran la ejecución independiente y el control en hello solución back-end.</span><span class="sxs-lookup"><span data-stu-id="0dede-127">Often, in addition tootelemetry data points, devices send messages and requests that require separate execution and handling in hello solution back end.</span></span> <span data-ttu-id="0dede-128">Por ejemplo, las alertas críticas que deben desencadenar una acción específica en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="0dede-128">For example, critical alerts that must trigger a specific action in hello back end.</span></span> <span data-ttu-id="0dede-129">Puede escribir fácilmente un [regla de enrutamiento] [ lnk-devguide-custom] toosend estos tipos de punto de conexión de mensajes tooan dedicado procesamiento tootheir basado en cualquier un encabezado de mensaje de bienvenida o un valor en el cuerpo del mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dede-129">You can easily write a [routing rule][lnk-devguide-custom] toosend these types of messages tooan endpoint dedicated tootheir processing based on either a header on hello message or a value in hello message body.</span></span>

<span data-ttu-id="0dede-130">Para obtener más información acerca de tooprocess de manera mejor de hello este tipo de mensaje, vea hello [Tutorial: cómo tooprocess mensajes del dispositivo a la nube de centro de IoT] [ lnk-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="0dede-130">For more information about hello best way tooprocess this kind of message, see hello [Tutorial: How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="0dede-131">Enrutamiento de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="0dede-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="0dede-132">Tiene dos opciones para las aplicaciones de back-end de tooyour de enrutamiento mensajes del dispositivo a la nube:</span><span class="sxs-lookup"><span data-stu-id="0dede-132">You have two options for routing device-to-cloud messages tooyour back-end apps:</span></span>

* <span data-ttu-id="0dede-133">Usar Hola integrada [punto de conexión de concentrador de eventos-compatible con] [ lnk-compatible-endpoint] tooenable aplicaciones back-end tooread Hola dispositivo a la nube mensajes que recibe el concentrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dede-133">Use hello built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] tooenable back-end apps tooread hello device-to-cloud messages received by hello hub.</span></span> <span data-ttu-id="0dede-134">toolearn sobre Hola integrados concentrador de eventos-compatible con punto de conexión, consulte [leer los mensajes de dispositivo para la nube de punto de conexión integrados de hello][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="0dede-134">toolearn about hello built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from hello built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="0dede-135">Usar enrutamiento de los extremos de toocustom reglas toosend mensajes en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0dede-135">Use routing rules toosend messages toocustom endpoints in your IoT hub.</span></span> <span data-ttu-id="0dede-136">Extremos personalizados permiten que los mensajes de dispositivo para la nube de tooread de aplicaciones back-end con los concentradores de eventos, colas de Service Bus o temas de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="0dede-136">Custom endpoints enable your back-end apps tooread device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="0dede-137">toolearn acerca de los puntos de conexión de enrutamientos y personalizados, vea [usar extremos personalizados y las reglas de enrutamiento para mensajes del dispositivo a la nube][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="0dede-137">toolearn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="0dede-138">Propiedades contra la suplantación</span><span class="sxs-lookup"><span data-stu-id="0dede-138">Anti-spoofing properties</span></span>

<span data-ttu-id="0dede-139">tooavoid dispositivo de suplantación de identidad en mensajes de dispositivo a la nube, centro de IoT marcas de todos los mensajes con hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="0dede-139">tooavoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with hello following properties:</span></span>

* <span data-ttu-id="0dede-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="0dede-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="0dede-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="0dede-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="0dede-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="0dede-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="0dede-143">Hello primero dos contienen hello **deviceId** y **generationId** de hello procedentes de dispositivos, como por [propiedades de identidad de dispositivo][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="0dede-143">hello first two contain hello **deviceId** and **generationId** of hello originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="0dede-144">Hola **ConnectionAuthMethod** propiedad contiene un objeto JSON serializado, con hello propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="0dede-144">hello **ConnectionAuthMethod** property contains a JSON serialized object, with hello following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="0dede-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0dede-145">Next steps</span></span>

<span data-ttu-id="0dede-146">Para obtener información sobre SDK de hello puede utilizar mensajes de dispositivo a la nube de toosend, consulte [SDK de Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="0dede-146">For information about hello SDKs you can use toosend device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="0dede-147">Hola [Introducción] [ lnk-get-started] los tutoriales muestra cómo toosend dispositivo a la nube mensajes desde los dispositivos físicos y simulados.</span><span class="sxs-lookup"><span data-stu-id="0dede-147">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="0dede-148">Para obtener información más detallada, vea hello [mensajes de dispositivo a la nube del centro de IoT de proceso mediante las rutas de] [ lnk-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="0dede-148">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

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
