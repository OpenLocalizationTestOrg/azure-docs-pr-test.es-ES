---
title: "Información de los puntos de conexión personalizados de Azure IoT Hub | Microsoft Docs"
description: "Guía del desarrollador: mediante las reglas de enrutamiento para enrutar los mensajes de dispositivo a nube a puntos de conexión personalizados."
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
ms.openlocfilehash: a21f1c61f344f96e2e03422e41fd8c5f7f841a0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="ab7c6-103">Uso de rutas de mensajes y de puntos de conexión personalizados para mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="ab7c6-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="ab7c6-104">IoT Hub le permite enrutar [mensajes de dispositivo a nube][lnk-device-to-cloud] a puntos de conexión orientados al servicio de IoT Hub según las propiedades de mensaje.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="ab7c6-105">Las reglas de enrutamiento proporcionan la flexibilidad necesaria para enviar los mensajes donde deben ir sin la necesidad de servicios adicionales para procesar mensajes o escribir código adicional.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services to process messages or to write additional code.</span></span> <span data-ttu-id="ab7c6-106">Cada regla de enrutamiento que configure tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="ab7c6-106">Each routing rule you configure has the following properties:</span></span>

| <span data-ttu-id="ab7c6-107">Propiedad</span><span class="sxs-lookup"><span data-stu-id="ab7c6-107">Property</span></span>      | <span data-ttu-id="ab7c6-108">Descripción</span><span class="sxs-lookup"><span data-stu-id="ab7c6-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="ab7c6-109">**Name**</span><span class="sxs-lookup"><span data-stu-id="ab7c6-109">**Name**</span></span>      | <span data-ttu-id="ab7c6-110">Nombre único que identifica la regla.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-110">The unique name that identifies the rule.</span></span> |
| <span data-ttu-id="ab7c6-111">**Origen**</span><span class="sxs-lookup"><span data-stu-id="ab7c6-111">**Source**</span></span>    | <span data-ttu-id="ab7c6-112">El origen del flujo de datos sobre el que se debe actuar.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-112">The origin of the data stream to be acted upon.</span></span> <span data-ttu-id="ab7c6-113">Por ejemplo, telemetría de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="ab7c6-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="ab7c6-114">**Condition**</span></span> | <span data-ttu-id="ab7c6-115">La expresión de consulta para la regla de enrutamiento que se ejecuta en el cuerpo y los encabezados del mensaje y se usa para determinar si se trata de una coincidencia para el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-115">The query expression for the routing rule that is run against the message's headers and body and used to determine whether it is a match for the endpoint.</span></span> <span data-ttu-id="ab7c6-116">Para más información sobre cómo crear una condición de ruta, consulte [Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos y trabajos][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="ab7c6-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="ab7c6-117">**Extremo**</span><span class="sxs-lookup"><span data-stu-id="ab7c6-117">**Endpoint**</span></span>  | <span data-ttu-id="ab7c6-118">El nombre del punto de conexión donde IoT Hub envía mensajes que cumplen la condición.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span></span> <span data-ttu-id="ab7c6-119">Los puntos de conexión deben estar en la misma región que IoT Hub, ya que, de lo caso contrario, se puede cobrar por escrituras entre regiones.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="ab7c6-120">Un solo mensaje puede cumplir la condición en varias reglas de enrutamiento, en cuyo caso IoT Hub entrega el mensaje al punto de conexión asociado a cada regla coincidente.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span></span> <span data-ttu-id="ab7c6-121">IoT Hub también desduplica automáticamente la entrega de mensajes, por lo que si un mensaje cumple varias reglas que tienen el mismo destino, solo se escribe en ese destino una vez.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have the same destination, it is only written to that destination once.</span></span>

<span data-ttu-id="ab7c6-122">Un centro de IoT tiene un [punto de conexión integrado][lnk-built-in] predeterminado.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="ab7c6-123">Puede crear puntos de conexión personalizados a los que enrutar mensajes vinculando otros servicios de su suscripción al centro.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-123">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span></span> <span data-ttu-id="ab7c6-124">IoT Hub admite actualmente Event Hubs, colas de Service Bus y temas de Service Bus como puntos de conexión personalizados.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="ab7c6-125">Las colas y los temas de Service Bus con **Sesiones** o **Detección de duplicados** habilitadas no son compatibles como puntos de conexión personalizados.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="ab7c6-126">Para más información sobre cómo crear puntos de conexión personalizados en IoT Hub, consulte [Referencia: Puntos de conexión de IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="ab7c6-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="ab7c6-127">Para obtener más información sobre la lectura de puntos de conexión personalizados, consulte:</span><span class="sxs-lookup"><span data-stu-id="ab7c6-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="ab7c6-128">Leer de [Event Hubs][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="ab7c6-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="ab7c6-129">Leer de [colas de Service Bus][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="ab7c6-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="ab7c6-130">Leer de [temas de Service Bus][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="ab7c6-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="ab7c6-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab7c6-131">Next steps</span></span>

<span data-ttu-id="ab7c6-132">Para obtener más información sobre los puntos de conexión de IoT Hub, vea [Puntos de conexión de IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="ab7c6-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="ab7c6-133">Para obtener más información sobre el lenguaje de consulta que se usa para definir las reglas de enrutamiento, vea [Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos, trabajos y enrutamiento de mensajes][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="ab7c6-133">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="ab7c6-134">El tutorial [Procesamiento de mensajes de dispositivo a nube de IoT Hub mediante rutas][lnk-d2c-tutorial] muestra cómo usar las reglas de enrutamiento y los puntos de conexión personalizados.</span><span class="sxs-lookup"><span data-stu-id="ab7c6-134">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
