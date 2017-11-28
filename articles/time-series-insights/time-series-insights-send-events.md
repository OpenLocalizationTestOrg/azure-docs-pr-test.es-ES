---
title: "Envío de eventos al entorno de Azure Time Series Insights | Microsoft Docs"
description: "Este tutorial describe cómo se insertan eventos en el entorno de Time Series Insights"
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: b4ef96a045393f28b3cd750068fe82a5a8411afa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="send-events-to-a-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="667a7-103">Envío de eventos a un entorno de Time Series Insights mediante un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="667a7-103">Send events to a Time Series Insights environment using event hub</span></span>

<span data-ttu-id="667a7-104">Este tutorial explica cómo crear y configurar el centro de eventos y ejecutar una aplicación de ejemplo para insertar eventos.</span><span class="sxs-lookup"><span data-stu-id="667a7-104">This tutorial explains how to create and configure event hub and run a sample application to push events.</span></span> <span data-ttu-id="667a7-105">Si tiene un centro de eventos existente con eventos en formato JSON, pase por alto este tutorial y vea su entorno en [Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="667a7-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="667a7-106">Configuración de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="667a7-106">Configure an event hub</span></span>
1. <span data-ttu-id="667a7-107">Para crear un centro de eventos, siga las instrucciones de la [documentación](https://docs.microsoft.com/azure/event-hubs/event-hubs-create) de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="667a7-107">To create an event hub, follow instructions from the Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="667a7-108">Asegúrese de crear un grupo de consumidores que sea utilizado exclusivamente por el origen de eventos de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="667a7-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="667a7-109">Asegúrese de que el grupo de consumidores no es utilizado por ningún otro servicio (como un trabajo de Stream Analytics u otro entorno de Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="667a7-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="667a7-110">Si otros servicios utilizan el grupo de consumidores, la operación de lectura se ve afectada negativamente en este entorno y en los otros servicios.</span><span class="sxs-lookup"><span data-stu-id="667a7-110">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="667a7-111">Utilizar “$Default” como grupo de consumidores podría provocar que otros lectores lo reutilicen.</span><span class="sxs-lookup"><span data-stu-id="667a7-111">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

  ![Selección del grupo de consumidores del centro de eventos](media/send-events/consumer-group.png)

3. <span data-ttu-id="667a7-113">En el centro de eventos, cree "MySendPolicy", que se usa para enviar eventos en el ejemplo de csharp.</span><span class="sxs-lookup"><span data-stu-id="667a7-113">On the event hub, create “MySendPolicy” that is used to send events in the csharp sample.</span></span>

  ![Seleccione Directivas de acceso compartido y haga clic en el botón Agregar](media/send-events/shared-access-policy.png)  

  ![Agregar nueva directiva de acceso compartido](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="667a7-116">Creación de un origen de eventos de Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="667a7-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="667a7-117">Si no ha creado un origen de eventos, siga [estas instrucciones](time-series-insights-add-event-source.md) para crear un origen de eventos.</span><span class="sxs-lookup"><span data-stu-id="667a7-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) to create an event source.</span></span>

2. <span data-ttu-id="667a7-118">Especifique "deviceTimestamp" como nombre de la propiedad de marca de tiempo: esta propiedad se utiliza como marca de tiempo real en el ejemplo de csharp.</span><span class="sxs-lookup"><span data-stu-id="667a7-118">Specify “deviceTimestamp” as the timestamp property name – this property is used as the actual timestamp in the csharp sample.</span></span> <span data-ttu-id="667a7-119">El nombre de la propiedad timestamp distingue mayúsculas de minúsculas y los valores deben tener el formato __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ cuando se envían como JSON al centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="667a7-119">The timestamp property name is case-sensitive and values must follow the format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON to event hub.</span></span> <span data-ttu-id="667a7-120">Si la propiedad no existe en el evento, se utiliza la hora de puesta en la cola del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="667a7-120">If the property does not exist in the event, then the event hub enqueued time is used.</span></span>

  ![Creación de un origen de eventos](media/send-events/event-source-1.png)

## <a name="sample-code-to-push-events"></a><span data-ttu-id="667a7-122">Código de ejemplo para insertar eventos</span><span class="sxs-lookup"><span data-stu-id="667a7-122">Sample code to push events</span></span>
1. <span data-ttu-id="667a7-123">Vaya a la directiva del centro de eventos "MySendPolicy" y copie la cadena de conexión con la clave de directiva.</span><span class="sxs-lookup"><span data-stu-id="667a7-123">Go to the event hub policy “MySendPolicy” and copy the connection string with the policy key.</span></span>

  ![Copia de la cadena de conexión de MySendPolicy](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="667a7-125">Ejecute el código siguiente para enviar 600 eventos para cada uno de los tres dispositivos.</span><span class="sxs-lookup"><span data-stu-id="667a7-125">Run the following code that to send 600 events per each of the three devices.</span></span> <span data-ttu-id="667a7-126">Reemplace `eventHubConnectionString` por su cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="667a7-126">Update `eventHubConnectionString` with your connection string.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON to event hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="667a7-127">Formas de JSON admitidas</span><span class="sxs-lookup"><span data-stu-id="667a7-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="667a7-128">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="667a7-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="667a7-129">Entrada</span><span class="sxs-lookup"><span data-stu-id="667a7-129">Input</span></span>

<span data-ttu-id="667a7-130">Un objeto JSON simple.</span><span class="sxs-lookup"><span data-stu-id="667a7-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="667a7-131">Salida: 1 evento</span><span class="sxs-lookup"><span data-stu-id="667a7-131">Output - 1 event</span></span>

|<span data-ttu-id="667a7-132">id</span><span class="sxs-lookup"><span data-stu-id="667a7-132">id</span></span>|<span data-ttu-id="667a7-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="667a7-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="667a7-134">device1</span><span class="sxs-lookup"><span data-stu-id="667a7-134">device1</span></span>|<span data-ttu-id="667a7-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="667a7-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="667a7-136">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="667a7-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="667a7-137">Entrada</span><span class="sxs-lookup"><span data-stu-id="667a7-137">Input</span></span>
<span data-ttu-id="667a7-138">Una matriz JSON con dos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="667a7-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="667a7-139">Cada objeto JSON se convertirá en un evento.</span><span class="sxs-lookup"><span data-stu-id="667a7-139">Each JSON object will be converted to an event.</span></span>
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a><span data-ttu-id="667a7-140">Salida: 2 eventos</span><span class="sxs-lookup"><span data-stu-id="667a7-140">Output - 2 Events</span></span>

|<span data-ttu-id="667a7-141">id</span><span class="sxs-lookup"><span data-stu-id="667a7-141">id</span></span>|<span data-ttu-id="667a7-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="667a7-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="667a7-143">device1</span><span class="sxs-lookup"><span data-stu-id="667a7-143">device1</span></span>|<span data-ttu-id="667a7-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="667a7-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="667a7-145">device2</span><span class="sxs-lookup"><span data-stu-id="667a7-145">device2</span></span>|<span data-ttu-id="667a7-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="667a7-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="667a7-147">Ejemplo 3</span><span class="sxs-lookup"><span data-stu-id="667a7-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="667a7-148">Entrada</span><span class="sxs-lookup"><span data-stu-id="667a7-148">Input</span></span>

<span data-ttu-id="667a7-149">Un objeto JSON con una matriz JSON anidada que contiene dos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="667a7-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a><span data-ttu-id="667a7-150">Salida: 2 eventos</span><span class="sxs-lookup"><span data-stu-id="667a7-150">Output - 2 Events</span></span>
<span data-ttu-id="667a7-151">Tenga en cuenta que la propiedad "location" se copia en cada uno de los eventos.</span><span class="sxs-lookup"><span data-stu-id="667a7-151">Note that the property "location" is copied over to each of the event.</span></span>

|<span data-ttu-id="667a7-152">location</span><span class="sxs-lookup"><span data-stu-id="667a7-152">location</span></span>|<span data-ttu-id="667a7-153">events.id</span><span class="sxs-lookup"><span data-stu-id="667a7-153">events.id</span></span>|<span data-ttu-id="667a7-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="667a7-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="667a7-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="667a7-155">WestUs</span></span>|<span data-ttu-id="667a7-156">device1</span><span class="sxs-lookup"><span data-stu-id="667a7-156">device1</span></span>|<span data-ttu-id="667a7-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="667a7-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="667a7-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="667a7-158">WestUs</span></span>|<span data-ttu-id="667a7-159">device2</span><span class="sxs-lookup"><span data-stu-id="667a7-159">device2</span></span>|<span data-ttu-id="667a7-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="667a7-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="667a7-161">Ejemplo 4</span><span class="sxs-lookup"><span data-stu-id="667a7-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="667a7-162">Entrada</span><span class="sxs-lookup"><span data-stu-id="667a7-162">Input</span></span>

<span data-ttu-id="667a7-163">Un objeto JSON con una matriz JSON anidada que contiene dos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="667a7-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="667a7-164">Esta entrada muestra que las propiedades globales se pueden representar mediante el objeto JSON complejo.</span><span class="sxs-lookup"><span data-stu-id="667a7-164">This input demonstrates that the global properties may be represented by the complex JSON object.</span></span>

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a><span data-ttu-id="667a7-165">Salida: 2 eventos</span><span class="sxs-lookup"><span data-stu-id="667a7-165">Output - 2 Events</span></span>

|<span data-ttu-id="667a7-166">location</span><span class="sxs-lookup"><span data-stu-id="667a7-166">location</span></span>|<span data-ttu-id="667a7-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="667a7-167">manufacturer.name</span></span>|<span data-ttu-id="667a7-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="667a7-168">manufacturer.location</span></span>|<span data-ttu-id="667a7-169">events.id</span><span class="sxs-lookup"><span data-stu-id="667a7-169">events.id</span></span>|<span data-ttu-id="667a7-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="667a7-170">events.timestamp</span></span>|<span data-ttu-id="667a7-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="667a7-171">events.data.type</span></span>|<span data-ttu-id="667a7-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="667a7-172">events.data.units</span></span>|<span data-ttu-id="667a7-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="667a7-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="667a7-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="667a7-174">WestUs</span></span>|<span data-ttu-id="667a7-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="667a7-175">manufacturer1</span></span>|<span data-ttu-id="667a7-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="667a7-176">EastUs</span></span>|<span data-ttu-id="667a7-177">device1</span><span class="sxs-lookup"><span data-stu-id="667a7-177">device1</span></span>|<span data-ttu-id="667a7-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="667a7-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="667a7-179">pressure</span><span class="sxs-lookup"><span data-stu-id="667a7-179">pressure</span></span>|<span data-ttu-id="667a7-180">psi</span><span class="sxs-lookup"><span data-stu-id="667a7-180">psi</span></span>|<span data-ttu-id="667a7-181">108.09</span><span class="sxs-lookup"><span data-stu-id="667a7-181">108.09</span></span>|
|<span data-ttu-id="667a7-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="667a7-182">WestUs</span></span>|<span data-ttu-id="667a7-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="667a7-183">manufacturer1</span></span>|<span data-ttu-id="667a7-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="667a7-184">EastUs</span></span>|<span data-ttu-id="667a7-185">device2</span><span class="sxs-lookup"><span data-stu-id="667a7-185">device2</span></span>|<span data-ttu-id="667a7-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="667a7-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="667a7-187">vibration</span><span class="sxs-lookup"><span data-stu-id="667a7-187">vibration</span></span>|<span data-ttu-id="667a7-188">abs G</span><span class="sxs-lookup"><span data-stu-id="667a7-188">abs G</span></span>|<span data-ttu-id="667a7-189">217.09</span><span class="sxs-lookup"><span data-stu-id="667a7-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="667a7-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="667a7-190">Next steps</span></span>

* <span data-ttu-id="667a7-191">Vea el entorno en el [portal de Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="667a7-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
