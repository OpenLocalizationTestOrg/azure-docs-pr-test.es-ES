---
title: extremos personalizados de aaaUnderstand centro de IoT de Azure | Documentos de Microsoft
description: "Guía del desarrollador - usar el enrutamiento las reglas de los puntos de conexión de toocustom de tooroute mensajes del dispositivo a la nube."
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="3772d-103">Uso de rutas de mensajes y de puntos de conexión personalizados para mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="3772d-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="3772d-104">Centro de IoT permite tooroute [mensajes del dispositivo a la nube] [ lnk-device-to-cloud] tooIoT concentrador de extremos de servicio de acceso en función de propiedades de mensaje.</span><span class="sxs-lookup"><span data-stu-id="3772d-104">IoT Hub enables you tooroute [device-to-cloud messages][lnk-device-to-cloud] tooIoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="3772d-105">Enrutamiento proporcionan reglas Hola flexibilidad toosend mensajes que necesitan toogo sin Hola necesitan para mensajes de tooprocess de servicios adicionales o toowrite de código adicional.</span><span class="sxs-lookup"><span data-stu-id="3772d-105">Routing rules give you hello flexibility toosend messages where they need toogo without hello need for additional services tooprocess messages or toowrite additional code.</span></span> <span data-ttu-id="3772d-106">Cada regla de enrutamiento que configure tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="3772d-106">Each routing rule you configure has hello following properties:</span></span>

| <span data-ttu-id="3772d-107">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3772d-107">Property</span></span>      | <span data-ttu-id="3772d-108">Descripción</span><span class="sxs-lookup"><span data-stu-id="3772d-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="3772d-109">**Name**</span><span class="sxs-lookup"><span data-stu-id="3772d-109">**Name**</span></span>      | <span data-ttu-id="3772d-110">Hola nombre único que identifica regla Hola.</span><span class="sxs-lookup"><span data-stu-id="3772d-110">hello unique name that identifies hello rule.</span></span> |
| <span data-ttu-id="3772d-111">**Origen**</span><span class="sxs-lookup"><span data-stu-id="3772d-111">**Source**</span></span>    | <span data-ttu-id="3772d-112">origen de Hola de los datos de hello secuencia toobe ha actuado en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="3772d-112">hello origin of hello data stream toobe acted upon.</span></span> <span data-ttu-id="3772d-113">Por ejemplo, telemetría de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3772d-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="3772d-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="3772d-114">**Condition**</span></span> | <span data-ttu-id="3772d-115">expresión de consulta de Hello para la regla de enrutamiento de Hola que se ejecuta en los encabezados y el cuerpo del mensaje de bienvenida y usar toodetermine si es una coincidencia para el punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3772d-115">hello query expression for hello routing rule that is run against hello message's headers and body and used toodetermine whether it is a match for hello endpoint.</span></span> <span data-ttu-id="3772d-116">Para obtener más información sobre cómo crear una condición de ruta, consulte hello [referencia: lenguaje de consulta para: los gemelos de dispositivo y los trabajos][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="3772d-116">For more information about constructing a route condition, see hello [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="3772d-117">**Extremo**</span><span class="sxs-lookup"><span data-stu-id="3772d-117">**Endpoint**</span></span>  | <span data-ttu-id="3772d-118">nombre de Hola de extremo de Hola donde centro de IoT envía mensajes que coinciden con la condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="3772d-118">hello name of hello endpoint where IoT Hub sends messages that match hello condition.</span></span> <span data-ttu-id="3772d-119">Los extremos deben estar en hello misma región que el centro de IoT hello, en caso contrario, se le puede cobrar para escribe entre regiones.</span><span class="sxs-lookup"><span data-stu-id="3772d-119">Endpoints should be in hello same region as hello IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="3772d-120">Un solo mensaje puede coincidir con la condición de hello en varias reglas de enrutamientos, en el que caso centro de IoT entrega Hola mensaje toohello punto de conexión asociado con cada regla coincidente.</span><span class="sxs-lookup"><span data-stu-id="3772d-120">A single message may match hello condition on multiple routing rules, in which case IoT Hub delivers hello message toohello endpoint associated with each matched rule.</span></span> <span data-ttu-id="3772d-121">Centro de IoT deduplica automáticamente también entrega de mensajes, por lo que si un mensaje coincide con varias reglas que tengan Hola mismo destino, solo se escribe toothat destino una vez.</span><span class="sxs-lookup"><span data-stu-id="3772d-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have hello same destination, it is only written toothat destination once.</span></span>

<span data-ttu-id="3772d-122">Un centro de IoT tiene un [punto de conexión integrado][lnk-built-in] predeterminado.</span><span class="sxs-lookup"><span data-stu-id="3772d-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="3772d-123">Puede crear extremos personalizados tooroute mensajes tooby vincular otros servicios en el centro de toohello de suscripción.</span><span class="sxs-lookup"><span data-stu-id="3772d-123">You can create custom endpoints tooroute messages tooby linking other services in your subscription toohello hub.</span></span> <span data-ttu-id="3772d-124">IoT Hub admite actualmente Event Hubs, colas de Service Bus y temas de Service Bus como puntos de conexión personalizados.</span><span class="sxs-lookup"><span data-stu-id="3772d-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="3772d-125">Las colas y los temas de Service Bus con **Sesiones** o **Detección de duplicados** habilitadas no son compatibles como puntos de conexión personalizados.</span><span class="sxs-lookup"><span data-stu-id="3772d-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="3772d-126">Para más información sobre cómo crear puntos de conexión personalizados en IoT Hub, consulte [Referencia: Puntos de conexión de IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="3772d-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="3772d-127">Para obtener más información sobre la lectura de puntos de conexión personalizados, consulte:</span><span class="sxs-lookup"><span data-stu-id="3772d-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="3772d-128">Leer de [Event Hubs][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="3772d-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="3772d-129">Leer de [colas de Service Bus][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="3772d-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="3772d-130">Leer de [temas de Service Bus][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="3772d-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="3772d-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3772d-131">Next steps</span></span>

<span data-ttu-id="3772d-132">Para obtener más información sobre los puntos de conexión de IoT Hub, vea [Puntos de conexión de IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="3772d-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="3772d-133">Para obtener más información sobre el lenguaje de consulta de Hola utilizar reglas de enrutamiento de toodefine, consulte [lenguaje de consulta de centro de IoT para: los gemelos de dispositivo, los trabajos y el enrutamiento de mensajes][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="3772d-133">For more information about hello query language you use toodefine routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="3772d-134">Hola [mensajes de dispositivo a la nube del centro de IoT de proceso mediante las rutas de] [ lnk-d2c-tutorial] tutorial muestra cómo las reglas de enrutamiento toouse y extremos personalizados.</span><span class="sxs-lookup"><span data-stu-id="3772d-134">hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how toouse routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
