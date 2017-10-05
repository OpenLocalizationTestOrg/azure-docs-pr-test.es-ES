---
title: Entrega y reintento de entrega de Azure Event Grid
description: "Describe cómo Azure Event Grid entrega eventos y cómo administra los mensajes no entregados."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: e0f8afdfd84ea3c0c061459c27da285f6ae8957e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="28dbe-103">Entrega y reintento de entrega de mensajes de Event Grid</span><span class="sxs-lookup"><span data-stu-id="28dbe-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="28dbe-104">En este artículo se describe cómo Azure Event Grid administra los eventos cuando no se confirma la entrega.</span><span class="sxs-lookup"><span data-stu-id="28dbe-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="28dbe-105">Event Grid ofrece entrega duradera.</span><span class="sxs-lookup"><span data-stu-id="28dbe-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="28dbe-106">Entrega cada mensaje por lo menos una vez en cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="28dbe-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="28dbe-107">Los eventos se envían inmediatamente al webhook registrado de cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="28dbe-107">Events are sent to the registered webhook of each subscription immediately.</span></span> <span data-ttu-id="28dbe-108">Si un webhook no acusa recibo de un evento en los 60 segundos siguientes al primer intento, Event Grid reintenta la entrega del evento.</span><span class="sxs-lookup"><span data-stu-id="28dbe-108">If a webhook does not acknowledge receipt of an event within 60 seconds of the first delivery attempt, Event Grid retries delivery of the event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="28dbe-109">Estado de entrega de mensajes</span><span class="sxs-lookup"><span data-stu-id="28dbe-109">Message delivery status</span></span>

<span data-ttu-id="28dbe-110">Event Grid usa códigos de respuesta HTTP para acusar recibo de eventos.</span><span class="sxs-lookup"><span data-stu-id="28dbe-110">Event Grid uses HTTP response codes to acknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="28dbe-111">Códigos de éxito</span><span class="sxs-lookup"><span data-stu-id="28dbe-111">Success codes</span></span>

<span data-ttu-id="28dbe-112">Los siguientes códigos de respuesta HTTP response indican que un evento se ha entregado correctamente en el webhook.</span><span class="sxs-lookup"><span data-stu-id="28dbe-112">The following HTTP response codes indicate that an event has been delivered successfully to your webhook.</span></span> <span data-ttu-id="28dbe-113">Event Grid considera la entrega finalizada.</span><span class="sxs-lookup"><span data-stu-id="28dbe-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="28dbe-114">200 OK</span><span class="sxs-lookup"><span data-stu-id="28dbe-114">200 OK</span></span>
- <span data-ttu-id="28dbe-115">202 - Aceptado</span><span class="sxs-lookup"><span data-stu-id="28dbe-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="28dbe-116">Códigos de error</span><span class="sxs-lookup"><span data-stu-id="28dbe-116">Failure codes</span></span>

<span data-ttu-id="28dbe-117">Los siguientes códigos de respuesta HTTP indican que el intento de entrega de un evento no se ha realizado.</span><span class="sxs-lookup"><span data-stu-id="28dbe-117">The following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="28dbe-118">Event Grid intenta enviar de nuevo el evento.</span><span class="sxs-lookup"><span data-stu-id="28dbe-118">Event Grid tries again to send the event.</span></span> 

- <span data-ttu-id="28dbe-119">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="28dbe-119">400 Bad Request</span></span>
- <span data-ttu-id="28dbe-120">401 No autorizado</span><span class="sxs-lookup"><span data-stu-id="28dbe-120">401 Unauthorized</span></span>
- <span data-ttu-id="28dbe-121">404 No encontrado</span><span class="sxs-lookup"><span data-stu-id="28dbe-121">404 Not Found</span></span>
- <span data-ttu-id="28dbe-122">408 - Tiempo de espera de solicitud</span><span class="sxs-lookup"><span data-stu-id="28dbe-122">408 Request timeout</span></span>
- <span data-ttu-id="28dbe-123">414 - URI de solicitud demasiado largo</span><span class="sxs-lookup"><span data-stu-id="28dbe-123">414 URI Too Long</span></span>
- <span data-ttu-id="28dbe-124">Error de servidor interno 500</span><span class="sxs-lookup"><span data-stu-id="28dbe-124">500 Internal Server Error</span></span>
- <span data-ttu-id="28dbe-125">Servicio no disponible 503</span><span class="sxs-lookup"><span data-stu-id="28dbe-125">503 Service Unavailable</span></span>
- <span data-ttu-id="28dbe-126">Tiempo de espera de puerta de enlace 504</span><span class="sxs-lookup"><span data-stu-id="28dbe-126">504 Gateway Timeout</span></span>

<span data-ttu-id="28dbe-127">Cualquier otro código de respuesta o la falta de respuesta indica un error.</span><span class="sxs-lookup"><span data-stu-id="28dbe-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="28dbe-128">Event Grid reintenta la entrega.</span><span class="sxs-lookup"><span data-stu-id="28dbe-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="28dbe-129">Intervalos de reintento</span><span class="sxs-lookup"><span data-stu-id="28dbe-129">Retry intervals</span></span>

<span data-ttu-id="28dbe-130">Event Grid usa una directiva de reintentos de retroceso exponencial para la entrega de eventos.</span><span class="sxs-lookup"><span data-stu-id="28dbe-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="28dbe-131">Si el webhook no responde o devuelve un código de error, Event Grid reintenta la entrega según la siguiente programación:</span><span class="sxs-lookup"><span data-stu-id="28dbe-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on the following schedule:</span></span>

1. <span data-ttu-id="28dbe-132">10 segundos</span><span class="sxs-lookup"><span data-stu-id="28dbe-132">10 seconds</span></span>
2. <span data-ttu-id="28dbe-133">30 segundos</span><span class="sxs-lookup"><span data-stu-id="28dbe-133">30 seconds</span></span>
3. <span data-ttu-id="28dbe-134">1 minuto</span><span class="sxs-lookup"><span data-stu-id="28dbe-134">1 minute</span></span>
4. <span data-ttu-id="28dbe-135">5 minutos</span><span class="sxs-lookup"><span data-stu-id="28dbe-135">5 minutes</span></span>
5. <span data-ttu-id="28dbe-136">10 minutos</span><span class="sxs-lookup"><span data-stu-id="28dbe-136">10 minutes</span></span>
6. <span data-ttu-id="28dbe-137">30 minutos</span><span class="sxs-lookup"><span data-stu-id="28dbe-137">30 minutes</span></span>
7. <span data-ttu-id="28dbe-138">1 hora</span><span class="sxs-lookup"><span data-stu-id="28dbe-138">1 hour</span></span>

<span data-ttu-id="28dbe-139">Event Grid agrega una pequeña selección aleatoria a todos los intervalos de reintento.</span><span class="sxs-lookup"><span data-stu-id="28dbe-139">Event Grid adds a small randomization to all retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="28dbe-140">Duración de reintentos</span><span class="sxs-lookup"><span data-stu-id="28dbe-140">Retry duration</span></span>

<span data-ttu-id="28dbe-141">Durante la versión preliminar, Azure Event Grid expira todos los eventos que no se hayan entregado en dos horas.</span><span class="sxs-lookup"><span data-stu-id="28dbe-141">During the preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="28dbe-142">Antes de la disponibilidad general, este tiempo se <aumentará a 24.</span><span class="sxs-lookup"><span data-stu-id="28dbe-142">Before General Availability, this time will be increased to 24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="28dbe-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="28dbe-143">Next steps</span></span>

* <span data-ttu-id="28dbe-144">Para obtener una introducción a Event Grid, vea [Acerca de Event Grid](overview.md).</span><span class="sxs-lookup"><span data-stu-id="28dbe-144">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="28dbe-145">Para comenzar a usar rápidamente Event Grid, vea [Creación y enrutamiento de eventos personalizados con Azure Event Grid](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="28dbe-145">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>