---
title: "¿Qué es Azure Event Hubs y por qué usarlo? | Microsoft Docs"
description: "Información general e introducción a Azure Event Hubs: ingesta de telemetría de escala de nube desde sitios web, aplicaciones y dispositivos"
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
ms.openlocfilehash: 1a6bf0a0352e6d9e3a22586ac825558d12e1307a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="fa656-103">¿Qué es Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="fa656-103">What is Event Hubs?</span></span>

<span data-ttu-id="fa656-104">Azure Event Hubs es una plataforma de streaming de datos y servicio de ingesta de eventos de gran escalabilidad que es capaz de recibir y procesar millones de eventos por segundo.</span><span class="sxs-lookup"><span data-stu-id="fa656-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="fa656-105">Event Hubs puede procesar y almacenar eventos, datos o telemetría generados por dispositivos y software distribuido.</span><span class="sxs-lookup"><span data-stu-id="fa656-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="fa656-106">Los datos enviados a un centro de eventos se pueden transformar y almacenar con cualquier proveedor de análisis en tiempo real o adaptadores de procesamiento por lotes y almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fa656-106">Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="fa656-107">Con la capacidad para ofrecer [funcionalidades de publicación y suscripción](https://msdn.microsoft.com/library/aa560414.aspx), con una latencia baja y a gran escala, Event Hubs sirve como "vía de entrada" para los macrodatos.</span><span class="sxs-lookup"><span data-stu-id="fa656-107">With the ability to provide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as the "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="fa656-108">¿Por qué usar Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="fa656-108">Why use Event Hubs?</span></span>

<span data-ttu-id="fa656-109">Las funcionalidades de control de eventos y telemetría de Event Hubs lo hacen especialmente útil para:</span><span class="sxs-lookup"><span data-stu-id="fa656-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="fa656-110">Instrumentación de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="fa656-110">Application instrumentation</span></span>
* <span data-ttu-id="fa656-111">La experiencia del usuario o el procesamiento de flujos de trabajo</span><span class="sxs-lookup"><span data-stu-id="fa656-111">User experience or workflow processing</span></span>
* <span data-ttu-id="fa656-112">Escenarios de Internet de las cosas (IoT)</span><span class="sxs-lookup"><span data-stu-id="fa656-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="fa656-113">Por ejemplo, Event Hubs permite el seguimiento del comportamiento en aplicaciones móviles, la información sobre el tráfico de granjas de servidores web, la captura de eventos en juegos de consola o la recopilación de telemetría de máquinas industriales, vehículos conectados u otros dispositivos.</span><span class="sxs-lookup"><span data-stu-id="fa656-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="fa656-114">Información general de Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="fa656-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="fa656-115">La función habitual que Event Hubs desempeña en las arquitecturas de soluciones es la de actuar como la "puerta principal" de una canalización de eventos, conocida a menudo como un *consumidor de eventos*.</span><span class="sxs-lookup"><span data-stu-id="fa656-115">The common role that Event Hubs plays in solution architectures is the "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="fa656-116">Un consumidor de eventos es un componente o servicio que se encuentra entre los publicadores de eventos y los consumidores de eventos para desacoplar la producción de un flujo de eventos del consumo de esos eventos.</span><span class="sxs-lookup"><span data-stu-id="fa656-116">An event ingestor is a component or service that sits between event publishers and event consumers to decouple the production of an event stream from the consumption of those events.</span></span> <span data-ttu-id="fa656-117">En la siguiente ilustración se muestra esta arquitectura:</span><span class="sxs-lookup"><span data-stu-id="fa656-117">The following figure depicts this architecture:</span></span>

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="fa656-119">Event Hubs proporciona una funcionalidad de control del flujo de mensajes pero tiene características diferentes de la mensajería empresarial tradicional.</span><span class="sxs-lookup"><span data-stu-id="fa656-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="fa656-120">Las funcionalidades de Event Hubs se basan en un alto rendimiento y en escenarios de procesamiento de eventos.</span><span class="sxs-lookup"><span data-stu-id="fa656-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="fa656-121">Por lo tanto, Event Hubs es diferente de la mensajería de [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) y no implementa algunas de las funcionalidades que están disponibles para entidades de [mensajería de Service Bus](/azure/service-bus-messaging/), como los temas.</span><span class="sxs-lookup"><span data-stu-id="fa656-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of the capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="fa656-122">Características de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="fa656-122">Event Hubs features</span></span>

<span data-ttu-id="fa656-123">Event Hubs contiene los siguientes elementos clave:</span><span class="sxs-lookup"><span data-stu-id="fa656-123">Event Hubs contains the following key elements:</span></span>

- <span data-ttu-id="fa656-124">[**Productores/publicadores de eventos**](event-hubs-features.md#event-publishers): una entidad que envía datos a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="fa656-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data to an event hub.</span></span> <span data-ttu-id="fa656-125">Se publica un evento mediante AMQP 1.0 o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fa656-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="fa656-126">[**Capturar**](event-hubs-features.md#capture): permite capturar los datos de transmisión de Event Hubs y almacenarlos en una cuenta de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="fa656-126">[**Capture**](event-hubs-features.md#capture): Enables you to capture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="fa656-127">[**Particiones**](event-hubs-features.md#partitions): permite que cada consumidor lea solo un subconjunto específico, o partición, del flujo de eventos.</span><span class="sxs-lookup"><span data-stu-id="fa656-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer to only read a specific subset, or partition, of the event stream.</span></span>
- <span data-ttu-id="fa656-128">[**Tokens de SAS**](event-hubs-features.md#sas-tokens): identifica y autentica al publicador de eventos.</span><span class="sxs-lookup"><span data-stu-id="fa656-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates the event publisher.</span></span>
- <span data-ttu-id="fa656-129">[**Consumidores de eventos**](event-hubs-features.md#event-consumers): una entidad que lee datos de eventos procedentes de un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="fa656-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="fa656-130">Los consumidores de eventos se conectan a través de AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="fa656-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="fa656-131">[**Grupos de consumidores**](event-hubs-features.md#consumer-groups): proporciona a cada aplicación con varios consumidores una vista distinta del flujo de eventos, lo que permite a los consumidores actuar de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="fa656-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of the event stream, enabling those consumers to act independently.</span></span>
- <span data-ttu-id="fa656-132">[**Unidades de procesamiento**](event-hubs-features.md#capacity): unidades de capacidad adquiridas previamente.</span><span class="sxs-lookup"><span data-stu-id="fa656-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="fa656-133">Una partición individual tiene una escala máxima de una unidad de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="fa656-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="fa656-134">Para detalles técnicos sobre estas y otras características de Event Hubs, consulte [Event Hubs features overview](event-hubs-features.md) (Introducción a las características de Event Hubs).</span><span class="sxs-lookup"><span data-stu-id="fa656-134">For technical details about these and other Event Hubs features, see the [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fa656-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fa656-135">Next steps</span></span>

<span data-ttu-id="fa656-136">Para información detallada sobre los precios de Event Hubs, consulte [Precios de Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="fa656-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="fa656-137">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fa656-137">For more information about Event Hubs, visit the following links:</span></span>

* <span data-ttu-id="fa656-138">Empiece por un [tutorial de Event Hubs](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="fa656-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="fa656-139">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="fa656-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="fa656-140">Aplicaciones de ejemplo que usan Event Hubs</span><span class="sxs-lookup"><span data-stu-id="fa656-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

