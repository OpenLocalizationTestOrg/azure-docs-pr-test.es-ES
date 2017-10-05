---
title: Disponibilidad y coherencia en Azure Event Hubs | Microsoft Docs
description: "Cómo proporcionar el máximo nivel de disponibilidad y coherencia con Azure Event Hubs mediante el uso de particiones."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 681a9d1636d547492f6f827461c6b2494b918778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="73d8b-103">Disponibilidad y coherencia en Event Hubs</span><span class="sxs-lookup"><span data-stu-id="73d8b-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="73d8b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="73d8b-104">Overview</span></span>
<span data-ttu-id="73d8b-105">Azure Event Hubs usa un [modelo de creación de particiones](event-hubs-features.md#partitions) para mejorar la disponibilidad y paralelización dentro de un solo centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="73d8b-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) to improve availability and parallelization within a single event hub.</span></span> <span data-ttu-id="73d8b-106">Por ejemplo, si un centro de eventos tiene cuatro particiones y una de ellas se mueve de un servidor a otro en una operación de equilibrio de carga, se puede enviar y recibir desde las otras tres.</span><span class="sxs-lookup"><span data-stu-id="73d8b-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server to another in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="73d8b-107">Además, tener un mayor número de particiones permite que más lectores simultáneos procesen los datos, lo que mejora el rendimiento agregado.</span><span class="sxs-lookup"><span data-stu-id="73d8b-107">Additionally, having more partitions enables you to have more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="73d8b-108">Conocer las implicaciones de la creación de particiones y la ordenación de un sistema distribuido es un aspecto fundamental del diseño de soluciones.</span><span class="sxs-lookup"><span data-stu-id="73d8b-108">Understanding the implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="73d8b-109">Para ayudar a explicar el equilibrio entre ordenación y disponibilidad, consulte el [teorema CAP](https://en.wikipedia.org/wiki/CAP_theorem), que también se conoce como teorema de Brewer.</span><span class="sxs-lookup"><span data-stu-id="73d8b-109">To help explain the trade-off between ordering and availability, see the [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="73d8b-110">Dicho teorema trata la elección entre coherencia, disponibilidad y tolerancia a la partición.</span><span class="sxs-lookup"><span data-stu-id="73d8b-110">This theorem discusses the choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="73d8b-111">El teorema de Brewer define la coherencia y la disponibilidad de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="73d8b-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="73d8b-112">Tolerancia a la partición: la capacidad de un sistema de procesamiento de datos de continuar procesando datos aunque se produzcan errores en una partición.</span><span class="sxs-lookup"><span data-stu-id="73d8b-112">Partition tolerance: the ability of a data processing system to continue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="73d8b-113">Disponibilidad: un nodo sin error devuelve una respuesta razonable en un plazo prudente (sin errores ni tiempos de espera).</span><span class="sxs-lookup"><span data-stu-id="73d8b-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="73d8b-114">Coherencia: se garantiza que una lectura devuelva la última escritura de un cliente determinado.</span><span class="sxs-lookup"><span data-stu-id="73d8b-114">Consistency: a read is guaranteed to return the most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="73d8b-115">Tolerancia a la partición</span><span class="sxs-lookup"><span data-stu-id="73d8b-115">Partition tolerance</span></span>
<span data-ttu-id="73d8b-116">Event Hubs se basa en un modelo de datos con particiones.</span><span class="sxs-lookup"><span data-stu-id="73d8b-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="73d8b-117">Se puede configurar el número de particiones en el centro de eventos durante la instalación, pero no se puede cambiar este valor más adelante.</span><span class="sxs-lookup"><span data-stu-id="73d8b-117">You can configure the number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="73d8b-118">Puesto que se deben utilizar particiones con Event Hubs, debe tomar una decisión con respecto a la disponibilidad y la coherencia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="73d8b-118">Since you must use partitions with Event Hubs, you have to make a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="73d8b-119">Disponibilidad</span><span class="sxs-lookup"><span data-stu-id="73d8b-119">Availability</span></span>
<span data-ttu-id="73d8b-120">La manera más sencilla de empezar a trabajar con Event Hubs es usar el comportamiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="73d8b-120">The simplest way to get started with Event Hubs is to use the default behavior.</span></span> <span data-ttu-id="73d8b-121">Si crea un objeto `EventHubClient` nuevo y usa el método `Send`, los eventos se distribuyen automáticamente entre las particiones del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="73d8b-121">If you create a new `EventHubClient` object and use the `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="73d8b-122">Este comportamiento permite disfrutar del máximo tiempo de actividad.</span><span class="sxs-lookup"><span data-stu-id="73d8b-122">This behavior allows for the greatest amount of up time.</span></span>

<span data-ttu-id="73d8b-123">Para los casos de uso que requieren el máximo tiempo de actividad, se prefiere este modelo.</span><span class="sxs-lookup"><span data-stu-id="73d8b-123">For use cases that require the maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="73d8b-124">Coherencia</span><span class="sxs-lookup"><span data-stu-id="73d8b-124">Consistency</span></span>
<span data-ttu-id="73d8b-125">En algunos escenarios, el orden de los eventos puede ser importante.</span><span class="sxs-lookup"><span data-stu-id="73d8b-125">In some scenarios, the ordering of events can be important.</span></span> <span data-ttu-id="73d8b-126">Por ejemplo, puede que prefiera el sistema back-end para procesar un comando de actualización antes que un comando de eliminación.</span><span class="sxs-lookup"><span data-stu-id="73d8b-126">For example, you may want your back-end system to process an update command before a delete command.</span></span> <span data-ttu-id="73d8b-127">En este caso, puede establecer la clave de partición en un evento, o usar un objeto `PartitionSender` para enviar eventos solo a una determinada partición.</span><span class="sxs-lookup"><span data-stu-id="73d8b-127">In this instance, you can either set the partition key on an event, or use a `PartitionSender` object to only send events to a certain partition.</span></span> <span data-ttu-id="73d8b-128">De esta forma, se garantiza que, cuando se lean eventos de la partición, la lectura siga un orden.</span><span class="sxs-lookup"><span data-stu-id="73d8b-128">Doing so ensures that when these events are read from the partition, they are read in order.</span></span>

<span data-ttu-id="73d8b-129">Con esta configuración, tenga en cuenta que si la partición concreta a la que se realiza el envío no se encuentra disponible, recibirá una respuesta de error.</span><span class="sxs-lookup"><span data-stu-id="73d8b-129">With this configuration, keep in mind that if the particular partition to which you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="73d8b-130">Como punto de comparación, si no tiene una afinidad para una sola partición, el servicio Event Hubs envía el evento a la siguiente partición disponible.</span><span class="sxs-lookup"><span data-stu-id="73d8b-130">As a point of comparison, if you do not have an affinity to a single partition, the Event Hubs service sends your event to the next available partition.</span></span>

<span data-ttu-id="73d8b-131">Una posible solución para garantizar el orden, mientras también se maximiza el tiempo de actividad, sería agregar eventos como parte de la aplicación de procesamiento de eventos.</span><span class="sxs-lookup"><span data-stu-id="73d8b-131">One possible solution to ensure ordering, while also maximizing up time, would be to aggregate events as part of your event processing application.</span></span> <span data-ttu-id="73d8b-132">La manera más fácil de lograr esto es marcar el evento con una propiedad de número de secuencia personalizada.</span><span class="sxs-lookup"><span data-stu-id="73d8b-132">The easiest way to accomplish this is to stamp your event with a custom sequence number property.</span></span> <span data-ttu-id="73d8b-133">El código siguiente muestra un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="73d8b-133">The following code shows an example:</span></span>

```csharp
// Get the latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="73d8b-134">Este ejemplo envía el evento a una de las particiones disponibles en el centro de eventos y establece el número de secuencia correspondiente a partir de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="73d8b-134">This example sends your event to one of the available partitions in your event hub, and sets the corresponding sequence number from your application.</span></span> <span data-ttu-id="73d8b-135">Esta solución requiere que la aplicación de procesamiento conserve el estado, pero proporciona a los remitentes un punto de conexión con más probabilidades de estar disponible.</span><span class="sxs-lookup"><span data-stu-id="73d8b-135">This solution requires state to be kept by your processing application, but gives your senders an endpoint that is more likely to be available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73d8b-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="73d8b-136">Next steps</span></span>
<span data-ttu-id="73d8b-137">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="73d8b-137">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="73d8b-138">Información general sobre el servicio Event Hubs</span><span class="sxs-lookup"><span data-stu-id="73d8b-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="73d8b-139">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="73d8b-139">Create an event hub</span></span>](event-hubs-create.md)
