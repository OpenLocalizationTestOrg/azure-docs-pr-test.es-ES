---
title: aaaAvailability y la coherencia en los centros de eventos de Azure | Documentos de Microsoft
description: "Cómo crea particiones de cantidad máxima de hello tooprovide de disponibilidad y la coherencia con el uso de los centros de eventos de Azure."
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
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="87677-103">Disponibilidad y coherencia en Event Hubs</span><span class="sxs-lookup"><span data-stu-id="87677-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="87677-104">Información general</span><span class="sxs-lookup"><span data-stu-id="87677-104">Overview</span></span>
<span data-ttu-id="87677-105">Centros de eventos de Azure usan un [particiones modelo](event-hubs-features.md#partitions) tooimprove disponibilidad y la ejecución en paralelo en un centro de eventos único.</span><span class="sxs-lookup"><span data-stu-id="87677-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) tooimprove availability and parallelization within a single event hub.</span></span> <span data-ttu-id="87677-106">Por ejemplo, si un centro de eventos tiene cuatro particiones y una de estas particiones se mueve desde un servidor tooanother en una operación de equilibrio de carga, puede enviar y recibir de tres otras particiones.</span><span class="sxs-lookup"><span data-stu-id="87677-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server tooanother in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="87677-107">Además, tener varias particiones permite toohave lectores simultáneos más procesamiento de los datos, mejorar el rendimiento global.</span><span class="sxs-lookup"><span data-stu-id="87677-107">Additionally, having more partitions enables you toohave more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="87677-108">Entender las implicaciones de Hola de particiones y el orden en un sistema distribuido es un aspecto crucial de diseño de la solución.</span><span class="sxs-lookup"><span data-stu-id="87677-108">Understanding hello implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="87677-109">toohelp explican equilibrio de hello entre la ordenación y la disponibilidad, vea hello [teorema CAP](https://en.wikipedia.org/wiki/CAP_theorem), también conocido como teorema de Brewer.</span><span class="sxs-lookup"><span data-stu-id="87677-109">toohelp explain hello trade-off between ordering and availability, see hello [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="87677-110">Este teorema describe elección Hola entre coherencia, la disponibilidad y tolerancia a la partición.</span><span class="sxs-lookup"><span data-stu-id="87677-110">This theorem discusses hello choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="87677-111">El teorema de Brewer define la coherencia y la disponibilidad de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="87677-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="87677-112">Tolerancia de partición: Hola capacidad de un toocontinue de sistema de procesamiento de datos de procesamiento de datos incluso si se produce un error de la partición.</span><span class="sxs-lookup"><span data-stu-id="87677-112">Partition tolerance: hello ability of a data processing system toocontinue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="87677-113">Disponibilidad: un nodo sin error devuelve una respuesta razonable en un plazo prudente (sin errores ni tiempos de espera).</span><span class="sxs-lookup"><span data-stu-id="87677-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="87677-114">: Una lectura se garantiza la coherencia tooreturn hello más reciente de escritura para un cliente determinado.</span><span class="sxs-lookup"><span data-stu-id="87677-114">Consistency: a read is guaranteed tooreturn hello most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="87677-115">Tolerancia a la partición</span><span class="sxs-lookup"><span data-stu-id="87677-115">Partition tolerance</span></span>
<span data-ttu-id="87677-116">Event Hubs se basa en un modelo de datos con particiones.</span><span class="sxs-lookup"><span data-stu-id="87677-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="87677-117">Puede configurar Hola número de particiones en el centro de eventos durante la instalación, pero no se puede cambiar este valor más adelante.</span><span class="sxs-lookup"><span data-stu-id="87677-117">You can configure hello number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="87677-118">Puesto que se deben utilizar particiones con concentradores de eventos, tiene una toomake una decisión sobre la disponibilidad y coherencia para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="87677-118">Since you must use partitions with Event Hubs, you have toomake a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="87677-119">Disponibilidad</span><span class="sxs-lookup"><span data-stu-id="87677-119">Availability</span></span>
<span data-ttu-id="87677-120">Hello tooget de manera más sencilla a trabajar con concentradores de eventos es el comportamiento predeterminado de toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="87677-120">hello simplest way tooget started with Event Hubs is toouse hello default behavior.</span></span> <span data-ttu-id="87677-121">Si crea un nuevo `EventHubClient` de objetos y usar hello `Send` método, los eventos se distribuyen automáticamente entre las particiones en el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="87677-121">If you create a new `EventHubClient` object and use hello `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="87677-122">Este comportamiento permite Hola mayor cantidad de tiempo de actividad.</span><span class="sxs-lookup"><span data-stu-id="87677-122">This behavior allows for hello greatest amount of up time.</span></span>

<span data-ttu-id="87677-123">Para los casos de uso que requieren el máximo de hello tiempo, este modelo es preferido.</span><span class="sxs-lookup"><span data-stu-id="87677-123">For use cases that require hello maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="87677-124">Coherencia</span><span class="sxs-lookup"><span data-stu-id="87677-124">Consistency</span></span>
<span data-ttu-id="87677-125">En algunos casos, puede ser importante Hola clasificación de eventos.</span><span class="sxs-lookup"><span data-stu-id="87677-125">In some scenarios, hello ordering of events can be important.</span></span> <span data-ttu-id="87677-126">Por ejemplo, puede que desee su tooprocess sistema back-end un comando de actualización antes de un comando de eliminación.</span><span class="sxs-lookup"><span data-stu-id="87677-126">For example, you may want your back-end system tooprocess an update command before a delete command.</span></span> <span data-ttu-id="87677-127">En este caso, puede establecer la clave de partición de hello en un evento, o usar un `PartitionSender` tooonly objeto enviar eventos tooa determinada partición.</span><span class="sxs-lookup"><span data-stu-id="87677-127">In this instance, you can either set hello partition key on an event, or use a `PartitionSender` object tooonly send events tooa certain partition.</span></span> <span data-ttu-id="87677-128">Este modo se asegura que si estos eventos se leen desde la partición de hello, se leen en orden.</span><span class="sxs-lookup"><span data-stu-id="87677-128">Doing so ensures that when these events are read from hello partition, they are read in order.</span></span>

<span data-ttu-id="87677-129">Con esta configuración, tenga en cuenta que si hello toowhich de partición determinada que está enviando no está disponible, recibirá una respuesta de error.</span><span class="sxs-lookup"><span data-stu-id="87677-129">With this configuration, keep in mind that if hello particular partition toowhich you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="87677-130">Como punto de comparación, si no tiene una partición única tooa de afinidad, Hola servicio de centros de eventos envía el evento toohello siguiente partición disponible.</span><span class="sxs-lookup"><span data-stu-id="87677-130">As a point of comparison, if you do not have an affinity tooa single partition, hello Event Hubs service sends your event toohello next available partition.</span></span>

<span data-ttu-id="87677-131">Tooensure de solución posible una ordenación, a la vez que también se minimiza el tiempo, sería tooaggregate eventos como parte de la aplicación de procesamiento de eventos.</span><span class="sxs-lookup"><span data-stu-id="87677-131">One possible solution tooensure ordering, while also maximizing up time, would be tooaggregate events as part of your event processing application.</span></span> <span data-ttu-id="87677-132">Hola tooaccomplish de manera más fácil esto es toostamp el evento con una propiedad de número de secuencia personalizada.</span><span class="sxs-lookup"><span data-stu-id="87677-132">hello easiest way tooaccomplish this is toostamp your event with a custom sequence number property.</span></span> <span data-ttu-id="87677-133">Hola siguiente código muestra un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="87677-133">hello following code shows an example:</span></span>

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="87677-134">Este ejemplo envía su tooone de eventos de particiones disponibles hello en el centro de eventos y establece el número de secuencia correspondiente de Hola desde su aplicación.</span><span class="sxs-lookup"><span data-stu-id="87677-134">This example sends your event tooone of hello available partitions in your event hub, and sets hello corresponding sequence number from your application.</span></span> <span data-ttu-id="87677-135">Esta solución requiere toobe estado mantenido por la aplicación de procesamiento, pero proporciona a las remitentes de un punto de conexión que es más probable que toobe disponible.</span><span class="sxs-lookup"><span data-stu-id="87677-135">This solution requires state toobe kept by your processing application, but gives your senders an endpoint that is more likely toobe available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87677-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="87677-136">Next steps</span></span>
<span data-ttu-id="87677-137">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="87677-137">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="87677-138">Información general sobre el servicio Event Hubs</span><span class="sxs-lookup"><span data-stu-id="87677-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="87677-139">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="87677-139">Create an event hub</span></span>](event-hubs-create.md)
