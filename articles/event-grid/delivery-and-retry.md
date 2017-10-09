---
title: "reintento y la entrega de la cuadrícula de eventos de aaaAzure"
description: "Describe cómo Azure Event Grid entrega eventos y cómo administra los mensajes no entregados."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="6c440-103">Entrega y reintento de entrega de mensajes de Event Grid</span><span class="sxs-lookup"><span data-stu-id="6c440-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="6c440-104">En este artículo se describe cómo Azure Event Grid administra los eventos cuando no se confirma la entrega.</span><span class="sxs-lookup"><span data-stu-id="6c440-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="6c440-105">Event Grid ofrece entrega duradera.</span><span class="sxs-lookup"><span data-stu-id="6c440-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="6c440-106">Entrega cada mensaje por lo menos una vez en cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="6c440-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="6c440-107">Eventos se envían inmediatamente webhook toohello registrado de cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="6c440-107">Events are sent toohello registered webhook of each subscription immediately.</span></span> <span data-ttu-id="6c440-108">Si un webhook no confirmar la recepción de un evento 60 segundos de entrega de hello primer intento, cuadrícula de eventos reintenta la entrega de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c440-108">If a webhook does not acknowledge receipt of an event within 60 seconds of hello first delivery attempt, Event Grid retries delivery of hello event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="6c440-109">Estado de entrega de mensajes</span><span class="sxs-lookup"><span data-stu-id="6c440-109">Message delivery status</span></span>

<span data-ttu-id="6c440-110">Cuadrícula de eventos usa HTTP respuesta códigos tooacknowledge la recepción de eventos.</span><span class="sxs-lookup"><span data-stu-id="6c440-110">Event Grid uses HTTP response codes tooacknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="6c440-111">Códigos de éxito</span><span class="sxs-lookup"><span data-stu-id="6c440-111">Success codes</span></span>

<span data-ttu-id="6c440-112">Hello códigos de respuesta HTTP siguientes indican que un evento se ha entregado correctamente tooyour webhook.</span><span class="sxs-lookup"><span data-stu-id="6c440-112">hello following HTTP response codes indicate that an event has been delivered successfully tooyour webhook.</span></span> <span data-ttu-id="6c440-113">Event Grid considera la entrega finalizada.</span><span class="sxs-lookup"><span data-stu-id="6c440-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="6c440-114">200 OK</span><span class="sxs-lookup"><span data-stu-id="6c440-114">200 OK</span></span>
- <span data-ttu-id="6c440-115">202 - Aceptado</span><span class="sxs-lookup"><span data-stu-id="6c440-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="6c440-116">Códigos de error</span><span class="sxs-lookup"><span data-stu-id="6c440-116">Failure codes</span></span>

<span data-ttu-id="6c440-117">Hola siguientes códigos de respuesta HTTP indica que un intento de entrega de evento no se pudo.</span><span class="sxs-lookup"><span data-stu-id="6c440-117">hello following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="6c440-118">Cuadrícula de eventos intenta de nuevo evento de hello toosend.</span><span class="sxs-lookup"><span data-stu-id="6c440-118">Event Grid tries again toosend hello event.</span></span> 

- <span data-ttu-id="6c440-119">400 - Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="6c440-119">400 Bad Request</span></span>
- <span data-ttu-id="6c440-120">401 No autorizado</span><span class="sxs-lookup"><span data-stu-id="6c440-120">401 Unauthorized</span></span>
- <span data-ttu-id="6c440-121">404 No encontrado</span><span class="sxs-lookup"><span data-stu-id="6c440-121">404 Not Found</span></span>
- <span data-ttu-id="6c440-122">408 - Tiempo de espera de solicitud</span><span class="sxs-lookup"><span data-stu-id="6c440-122">408 Request timeout</span></span>
- <span data-ttu-id="6c440-123">414 - URI de solicitud demasiado largo</span><span class="sxs-lookup"><span data-stu-id="6c440-123">414 URI Too Long</span></span>
- <span data-ttu-id="6c440-124">Error de servidor interno 500</span><span class="sxs-lookup"><span data-stu-id="6c440-124">500 Internal Server Error</span></span>
- <span data-ttu-id="6c440-125">Servicio no disponible 503</span><span class="sxs-lookup"><span data-stu-id="6c440-125">503 Service Unavailable</span></span>
- <span data-ttu-id="6c440-126">Tiempo de espera de puerta de enlace 504</span><span class="sxs-lookup"><span data-stu-id="6c440-126">504 Gateway Timeout</span></span>

<span data-ttu-id="6c440-127">Cualquier otro código de respuesta o la falta de respuesta indica un error.</span><span class="sxs-lookup"><span data-stu-id="6c440-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="6c440-128">Event Grid reintenta la entrega.</span><span class="sxs-lookup"><span data-stu-id="6c440-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="6c440-129">Intervalos de reintento</span><span class="sxs-lookup"><span data-stu-id="6c440-129">Retry intervals</span></span>

<span data-ttu-id="6c440-130">Event Grid usa una directiva de reintentos de retroceso exponencial para la entrega de eventos.</span><span class="sxs-lookup"><span data-stu-id="6c440-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="6c440-131">Si el webhook no responde o devuelve un código de error, cuadrícula de eventos reintenta la entrega en hello siguiente programación:</span><span class="sxs-lookup"><span data-stu-id="6c440-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on hello following schedule:</span></span>

1. <span data-ttu-id="6c440-132">10 segundos</span><span class="sxs-lookup"><span data-stu-id="6c440-132">10 seconds</span></span>
2. <span data-ttu-id="6c440-133">30 segundos</span><span class="sxs-lookup"><span data-stu-id="6c440-133">30 seconds</span></span>
3. <span data-ttu-id="6c440-134">1 minuto</span><span class="sxs-lookup"><span data-stu-id="6c440-134">1 minute</span></span>
4. <span data-ttu-id="6c440-135">5 minutos</span><span class="sxs-lookup"><span data-stu-id="6c440-135">5 minutes</span></span>
5. <span data-ttu-id="6c440-136">10 minutos</span><span class="sxs-lookup"><span data-stu-id="6c440-136">10 minutes</span></span>
6. <span data-ttu-id="6c440-137">30 minutos</span><span class="sxs-lookup"><span data-stu-id="6c440-137">30 minutes</span></span>
7. <span data-ttu-id="6c440-138">1 hora</span><span class="sxs-lookup"><span data-stu-id="6c440-138">1 hour</span></span>

<span data-ttu-id="6c440-139">Cuadrícula de eventos agrega un intervalos de reintento de selección aleatoria pequeño tooall.</span><span class="sxs-lookup"><span data-stu-id="6c440-139">Event Grid adds a small randomization tooall retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="6c440-140">Duración de reintentos</span><span class="sxs-lookup"><span data-stu-id="6c440-140">Retry duration</span></span>

<span data-ttu-id="6c440-141">Durante la vista previa de hello, cuadrícula de eventos de Azure caduca todos los eventos que no se entregan dentro de dos horas.</span><span class="sxs-lookup"><span data-stu-id="6c440-141">During hello preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="6c440-142">Antes de la disponibilidad General, este tiempo será mayor too24 horas.</span><span class="sxs-lookup"><span data-stu-id="6c440-142">Before General Availability, this time will be increased too24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6c440-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c440-143">Next steps</span></span>

* <span data-ttu-id="6c440-144">Para una cuadrícula de introducción tooEvent, consulte [acerca de la cuadrícula de eventos](overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c440-144">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="6c440-145">tooquickly Introducción al uso de la cuadrícula de eventos, vea [ruta y crear eventos personalizados con la cuadrícula de eventos de Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="6c440-145">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
