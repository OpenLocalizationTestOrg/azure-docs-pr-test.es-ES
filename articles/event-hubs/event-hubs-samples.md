---
title: Ejemplos de Azure Event Hubs | Microsoft Docs
description: Ejemplos de Azure Event Hubs
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ae9fbd97a1747d8f14c561f247a0973bb11fd039
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="5b9a6-103">Ejemplos de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5b9a6-103">Event Hubs samples</span></span> 

<span data-ttu-id="5b9a6-104">El conjunto de ejemplos de Event Hubs muestra las características clave de [Azure Event Hubs](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="5b9a6-104">The set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="5b9a6-105">En este artículo se categorizan y describen los ejemplos disponibles, con vínculos a cada uno.</span><span class="sxs-lookup"><span data-stu-id="5b9a6-105">This article categorizes and describes the samples available, with links to each.</span></span>

<span data-ttu-id="5b9a6-106">En el momento de redactar este artículo, los ejemplos de Event Hubs se encuentran en distintos lugares:</span><span class="sxs-lookup"><span data-stu-id="5b9a6-106">At the time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="5b9a6-107">Ejemplos de código para desarrolladores de MSDN</span><span class="sxs-lookup"><span data-stu-id="5b9a6-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="5b9a6-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="5b9a6-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="5b9a6-109">Para más información sobre las diferentes versiones de .NET Framework, consulte [Marcos y destinos](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="5b9a6-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="5b9a6-110">Se agregarán más ejemplos con el tiempo, así que revise este sitio con frecuencia para comprobar las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="5b9a6-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="5b9a6-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="5b9a6-111">.NET Standard</span></span>

<span data-ttu-id="5b9a6-112">Los ejemplos siguientes muestran cómo enviar y recibir eventos mediante el [cliente de Event Hubs](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) para la [biblioteca de .NET Standard](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="5b9a6-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="5b9a6-113">Envío de eventos</span><span class="sxs-lookup"><span data-stu-id="5b9a6-113">Send events</span></span> 

<span data-ttu-id="5b9a6-114">El ejemplo de [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) (Introducción al envío) muestra cómo escribir una aplicación de consola de .NET Core que envía eventos a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="5b9a6-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="5b9a6-115">Recepción de eventos</span><span class="sxs-lookup"><span data-stu-id="5b9a6-115">Receive events</span></span> 

<span data-ttu-id="5b9a6-116">El ejemplo de [introducción a la recepción con el host del procesador de eventos](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) es una aplicación de consola de .NET Core que recibe mensajes desde un centro de eventos mediante el host del procesador de eventos.</span><span class="sxs-lookup"><span data-stu-id="5b9a6-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="5b9a6-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5b9a6-117">.NET Framework</span></span>   

<span data-ttu-id="5b9a6-118">Estos ejemplos muestran otras características de Azure Event Hubs que tienen como destino la [biblioteca de .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="5b9a6-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="5b9a6-119">Notificación a los usuarios sobre los eventos recibidos</span><span class="sxs-lookup"><span data-stu-id="5b9a6-119">Notify users of events received</span></span>

<span data-ttu-id="5b9a6-120">El ejemplo de [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) muestra cómo notificar a los usuarios sobre los datos recibidos de los sensores o de otros sistemas.</span><span class="sxs-lookup"><span data-stu-id="5b9a6-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="5b9a6-121">Introducción a los Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="5b9a6-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="5b9a6-122">El ejemplo de [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) (Introducción a Event Hubs) muestra las funcionalidades básicas de Event Hubs, como la creación de un centro de eventos, el envío de eventos a un centro de eventos y el consumo de eventos mediante el [host del procesador de eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="5b9a6-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="5b9a6-123">Escalado horizontal del procesamiento de eventos</span><span class="sxs-lookup"><span data-stu-id="5b9a6-123">Scale out event processing</span></span> 

<span data-ttu-id="5b9a6-124">El ejemplo de [escalado horizontal del procesamiento de eventos](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) muestra cómo utilizar el [host del procesador de eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) para distribuir la carga de trabajo del consumo de flujo de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="5b9a6-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="5b9a6-125">Muestra cómo implementar los objetos **EventProcessor** y **EventProcessorFactory** para administrar el flujo de eventos.</span><span class="sxs-lookup"><span data-stu-id="5b9a6-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="5b9a6-126">Extracción de datos de SQL a un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="5b9a6-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="5b9a6-127">El ejemplo de [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) (Extracción de datos de SQL) muestra cómo extraer datos de una tabla SQL e insertarlos en un centro de eventos para usarlos como una entrada en las aplicaciones analíticas auxiliares.</span><span class="sxs-lookup"><span data-stu-id="5b9a6-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="5b9a6-128">Extracción de datos web a un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="5b9a6-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="5b9a6-129">El ejemplo de [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) (Importación de datos desde la web) muestra cómo extraer datos de fuentes públicas (como la información de tráfico del Departamento de transporte) e insertarlos en un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="5b9a6-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b9a6-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b9a6-130">Next steps</span></span>

<span data-ttu-id="5b9a6-131">Si desea conocer más información sobre las versiones de .NET Framework, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b9a6-131">Learn more about .NET Framework versions by visiting the following links:</span></span>

- [<span data-ttu-id="5b9a6-132">Marcos y destinos</span><span class="sxs-lookup"><span data-stu-id="5b9a6-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="5b9a6-133">.NET Framework 4.6 y 4.5</span><span class="sxs-lookup"><span data-stu-id="5b9a6-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="5b9a6-134">Si desea conocer más información acerca de Event Hubs, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="5b9a6-134">You can learn more about Event Hubs in the following articles:</span></span>

- [<span data-ttu-id="5b9a6-135">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5b9a6-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="5b9a6-136">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="5b9a6-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="5b9a6-137">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5b9a6-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)