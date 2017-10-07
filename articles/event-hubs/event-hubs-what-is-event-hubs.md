---
title: "aaaWhat centros de eventos de Azure y por qué usarla | Documentos de Microsoft"
description: "Información general e introducción tooAzure centros de eventos - recopilación de telemetría de escala de nube de sitios Web, aplicaciones y dispositivos"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="7a3ca-103">¿Qué es Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="7a3ca-103">What is Event Hubs?</span></span>

<span data-ttu-id="7a3ca-104">Azure Event Hubs es una plataforma de streaming de datos y servicio de ingesta de eventos de gran escalabilidad que es capaz de recibir y procesar millones de eventos por segundo.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="7a3ca-105">Event Hubs puede procesar y almacenar eventos, datos o telemetría generados por dispositivos y software distribuido.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="7a3ca-106">Los datos se envían tooan concentrador de eventos se puede transformar y almacenado con cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento y procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-106">Data sent tooan event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="7a3ca-107">Con hello capacidad tooprovide [capacidades de publicación / suscripción](https://msdn.microsoft.com/library/aa560414.aspx) con una latencia baja y a escala masiva, los concentradores de eventos actúa como Hola "en rampa" para grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-107">With hello ability tooprovide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as hello "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="7a3ca-108">¿Por qué usar Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="7a3ca-108">Why use Event Hubs?</span></span>

<span data-ttu-id="7a3ca-109">Las funcionalidades de control de eventos y telemetría de Event Hubs lo hacen especialmente útil para:</span><span class="sxs-lookup"><span data-stu-id="7a3ca-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="7a3ca-110">Instrumentación de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7a3ca-110">Application instrumentation</span></span>
* <span data-ttu-id="7a3ca-111">La experiencia del usuario o el procesamiento de flujos de trabajo</span><span class="sxs-lookup"><span data-stu-id="7a3ca-111">User experience or workflow processing</span></span>
* <span data-ttu-id="7a3ca-112">Escenarios de Internet de las cosas (IoT)</span><span class="sxs-lookup"><span data-stu-id="7a3ca-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="7a3ca-113">Por ejemplo, Event Hubs permite el seguimiento del comportamiento en aplicaciones móviles, la información sobre el tráfico de granjas de servidores web, la captura de eventos en juegos de consola o la recopilación de telemetría de máquinas industriales, vehículos conectados u otros dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="7a3ca-114">Información general de los Centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="7a3ca-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="7a3ca-115">Hello rol común que los concentradores de eventos se reproduce en arquitecturas de soluciones es hello "puerta principal" para una canalización de eventos, se llama a menudo un *introductor de eventos*.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-115">hello common role that Event Hubs plays in solution architectures is hello "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="7a3ca-116">Un introductor de eventos es un componente o servicio que se encuentra entre los publicadores de eventos y producción de hello de toodecouple de los consumidores de eventos de una secuencia de eventos del consumo de Hola de esos eventos.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-116">An event ingestor is a component or service that sits between event publishers and event consumers toodecouple hello production of an event stream from hello consumption of those events.</span></span> <span data-ttu-id="7a3ca-117">Hello en la ilustración siguiente se muestra esta arquitectura:</span><span class="sxs-lookup"><span data-stu-id="7a3ca-117">hello following figure depicts this architecture:</span></span>

![Centros de eventos](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="7a3ca-119">Event Hubs proporciona una funcionalidad de control del flujo de mensajes pero tiene características diferentes de la mensajería empresarial tradicional.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="7a3ca-120">Las funcionalidades de Event Hubs se basan en un alto rendimiento y en escenarios de procesamiento de eventos.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="7a3ca-121">Por lo tanto, es diferente de los centros de eventos [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) de mensajería y no implementa algunas de las capacidades de Hola que están disponibles para [Bus de servicio de mensajería](/azure/service-bus-messaging/) entidades, como temas.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of hello capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="7a3ca-122">Características de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7a3ca-122">Event Hubs features</span></span>

<span data-ttu-id="7a3ca-123">Los concentradores de eventos contiene Hola siguientes elementos clave:</span><span class="sxs-lookup"><span data-stu-id="7a3ca-123">Event Hubs contains hello following key elements:</span></span>

- <span data-ttu-id="7a3ca-124">[**Los productores y los publicadores de eventos**](event-hubs-features.md#event-publishers): una entidad que envía el concentrador de eventos de tooan de datos.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data tooan event hub.</span></span> <span data-ttu-id="7a3ca-125">Se publica un evento mediante AMQP 1.0 o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="7a3ca-126">[**Capturar**](event-hubs-features.md#capture): permite los centros de eventos de toocapture transmisión de datos y almacenarla en una cuenta de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-126">[**Capture**](event-hubs-features.md#capture): Enables you toocapture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="7a3ca-127">[**Las particiones**](event-hubs-features.md#partitions): permite que cada consumidor tooonly lee un subconjunto específico, o partición, de hello secuencia de eventos.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer tooonly read a specific subset, or partition, of hello event stream.</span></span>
- <span data-ttu-id="7a3ca-128">[**Tokens de SAS**](event-hubs-features.md#sas-tokens): identifica y autentica el publicador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates hello event publisher.</span></span>
- <span data-ttu-id="7a3ca-129">[**Consumidores de eventos**](event-hubs-features.md#event-consumers): una entidad que lee datos de eventos procedentes de un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="7a3ca-130">Los consumidores de eventos se conectan a través de AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="7a3ca-131">[**Grupos de consumidores**](event-hubs-features.md#consumer-groups): proporciona cada múltiplo consumir la aplicación con una vista independiente de la secuencia de eventos de hello, habilitando esos tooact consumidores independientemente.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of hello event stream, enabling those consumers tooact independently.</span></span>
- <span data-ttu-id="7a3ca-132">[**Unidades de procesamiento**](event-hubs-features.md#capacity): unidades de capacidad adquiridas previamente.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="7a3ca-133">Una partición individual tiene una escala máxima de una unidad de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="7a3ca-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="7a3ca-134">Para obtener información técnica acerca de estas y otras características de los centros de eventos, vea hello [Introducción a características de los centros de eventos](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="7a3ca-134">For technical details about these and other Event Hubs features, see hello [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7a3ca-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7a3ca-135">Next steps</span></span>

<span data-ttu-id="7a3ca-136">Para información detallada sobre los precios de Event Hubs, consulte [Precios de Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="7a3ca-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="7a3ca-137">Para obtener más información acerca de los centros de eventos, visite Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="7a3ca-137">For more information about Event Hubs, visit hello following links:</span></span>

* <span data-ttu-id="7a3ca-138">Empiece por un [tutorial de Event Hubs](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="7a3ca-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="7a3ca-139">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7a3ca-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="7a3ca-140">Aplicaciones de ejemplo que usan Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7a3ca-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

