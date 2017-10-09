---
title: ejemplos de los centros de eventos aaaAzure | Documentos de Microsoft
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
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="32dee-103">Ejemplos de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="32dee-103">Event Hubs samples</span></span> 

<span data-ttu-id="32dee-104">conjunto de ejemplos de los centros de eventos de Azure Hello muestra las características claves de [centros de eventos de Azure](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="32dee-104">hello set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="32dee-105">En este artículo se clasifica y describe los ejemplos de hello disponibles, con vínculos tooeach.</span><span class="sxs-lookup"><span data-stu-id="32dee-105">This article categorizes and describes hello samples available, with links tooeach.</span></span>

<span data-ttu-id="32dee-106">En tiempo de Hola de redactar este artículo, los ejemplos de los centros de eventos se encuentran en distintos lugares:</span><span class="sxs-lookup"><span data-stu-id="32dee-106">At hello time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="32dee-107">Ejemplos de código para desarrolladores de MSDN</span><span class="sxs-lookup"><span data-stu-id="32dee-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="32dee-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="32dee-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="32dee-109">Para obtener más información sobre las diferentes versiones de .NET Framework de hello, consulte [marcos de trabajo y los destinos](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="32dee-109">For more information about different versions of hello .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="32dee-110">Se agregarán más ejemplos con el tiempo, así que revise este sitio con frecuencia para comprobar las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="32dee-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="32dee-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="32dee-111">.NET Standard</span></span>

<span data-ttu-id="32dee-112">Hello en los ejemplos siguientes se muestran cómo toosend y recibir eventos mediante hello [cliente de los centros de eventos](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) para hello [biblioteca estándar de .NET](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="32dee-112">hello following samples demonstrate how toosend and receive events using hello [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for hello [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="32dee-113">Envío de eventos</span><span class="sxs-lookup"><span data-stu-id="32dee-113">Send events</span></span> 

<span data-ttu-id="32dee-114">Hola [empezar a enviar](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) muestra cómo toowrite un núcleo de .NET consola aplicación que envía el concentrador de eventos de tooan de eventos.</span><span class="sxs-lookup"><span data-stu-id="32dee-114">hello [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how toowrite a .NET Core console application that sends events tooan event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="32dee-115">Recepción de eventos</span><span class="sxs-lookup"><span data-stu-id="32dee-115">Receive events</span></span> 

<span data-ttu-id="32dee-116">Hola [empezar a recibir con hello Host procesador de eventos](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) ejemplo es una aplicación de consola .NET Core que recibe los mensajes de un concentrador de eventos mediante Hola Host procesador de eventos.</span><span class="sxs-lookup"><span data-stu-id="32dee-116">hello [Get started receiving with hello Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using hello Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="32dee-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="32dee-117">.NET Framework</span></span>   

<span data-ttu-id="32dee-118">Estos ejemplos muestran varias otras características de los centros de eventos de Azure, como destino Hola [biblioteca de .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="32dee-118">These samples demonstrate various other features of Azure Event Hubs, targeting hello [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="32dee-119">Notificación a los usuarios sobre los eventos recibidos</span><span class="sxs-lookup"><span data-stu-id="32dee-119">Notify users of events received</span></span>

<span data-ttu-id="32dee-120">Hola [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) ejemplo notifica a los usuarios de los datos recibidos de sensores u otros sistemas.</span><span class="sxs-lookup"><span data-stu-id="32dee-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="32dee-121">Introducción a los Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="32dee-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="32dee-122">Hola [evento Introducción a concentradores](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) muestra capacidades básicas de Hola de centros de eventos, como cómo enviar concentrador de eventos de eventos tooan toocreate un centro de eventos y consumir eventos mediante hello [Host de procesador de eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="32dee-122">hello [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates hello basic capabilities of Event Hubs, such as how toocreate an event hub, send events tooan event hub, and consume events using hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="32dee-123">Escalado horizontal del procesamiento de eventos</span><span class="sxs-lookup"><span data-stu-id="32dee-123">Scale out event processing</span></span> 

<span data-ttu-id="32dee-124">Hola [escalar horizontalmente el procesamiento de eventos](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) ejemplo muestra cómo hello toouse [Host procesador de eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) carga de trabajo de toodistribute Hola de consumo de la secuencia de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="32dee-124">hello [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="32dee-125">Muestra cómo hello tooimplement **EventProcessor** y **EventProcessorFactory** flujo de eventos de objetos toomanage Hola.</span><span class="sxs-lookup"><span data-stu-id="32dee-125">It shows how tooimplement hello **EventProcessor** and **EventProcessorFactory** objects toomanage hello event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="32dee-126">Extracción de datos de SQL a un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="32dee-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="32dee-127">Hola [de datos de SQL de extracción](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) ejemplo muestra cómo toopull datos desde una instancia de SQL de la tabla y empújelo concentrador de eventos tooan, toouse como una entrada en aplicaciones analíticas siguen en la cadena.</span><span class="sxs-lookup"><span data-stu-id="32dee-127">hello [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how toopull data from a SQL table and push it tooan event hub, toouse as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="32dee-128">Extracción de datos web a un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="32dee-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="32dee-129">Hola [importar datos desde web hello](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) ejemplo muestra cómo toopull datos desde public fuentes (por ejemplo Hola información del departamento de transporte tráfico de fuentes de distribución) y empújelo tooan concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="32dee-129">hello [Import data from hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how toopull data from public feeds (such as hello Department of Transportation's traffic information feed) and push it tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32dee-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32dee-130">Next steps</span></span>

<span data-ttu-id="32dee-131">Más información acerca de las versiones de .NET Framework visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="32dee-131">Learn more about .NET Framework versions by visiting hello following links:</span></span>

- [<span data-ttu-id="32dee-132">Marcos y destinos</span><span class="sxs-lookup"><span data-stu-id="32dee-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="32dee-133">.NET Framework 4.6 y 4.5</span><span class="sxs-lookup"><span data-stu-id="32dee-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="32dee-134">Puede obtener más información acerca de los centros de eventos en hello siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="32dee-134">You can learn more about Event Hubs in hello following articles:</span></span>

- [<span data-ttu-id="32dee-135">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="32dee-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="32dee-136">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="32dee-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="32dee-137">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="32dee-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)