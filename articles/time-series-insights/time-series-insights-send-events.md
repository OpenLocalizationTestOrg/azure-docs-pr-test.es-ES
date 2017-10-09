---
title: "entorno de visión de la serie de tiempo de aaaSend eventos tooAzure | Documentos de Microsoft"
description: "Este tutorial trata el entorno de visión de la serie de tiempo de hello pasos toopush eventos tooyour"
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
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="97b09-103">Entorno de visión de la serie de tiempo de tooa de eventos con el concentrador de eventos de envío</span><span class="sxs-lookup"><span data-stu-id="97b09-103">Send events tooa Time Series Insights environment using event hub</span></span>

<span data-ttu-id="97b09-104">Este tutorial le explica cómo toocreate Configurar centro de eventos y ejecutar un toopush de la aplicación de ejemplo de eventos.</span><span class="sxs-lookup"><span data-stu-id="97b09-104">This tutorial explains how toocreate and configure event hub and run a sample application toopush events.</span></span> <span data-ttu-id="97b09-105">Si tiene un centro de eventos existente con eventos en formato JSON, pase por alto este tutorial y vea su entorno en [Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97b09-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="97b09-106">Configuración de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="97b09-106">Configure an event hub</span></span>
1. <span data-ttu-id="97b09-107">toocreate un concentrador de eventos, siga las instrucciones de hello concentrador de eventos [documentación](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span><span class="sxs-lookup"><span data-stu-id="97b09-107">toocreate an event hub, follow instructions from hello Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="97b09-108">Asegúrese de crear un grupo de consumidores que sea utilizado exclusivamente por el origen de eventos de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="97b09-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="97b09-109">Asegúrese de que el grupo de consumidores no es utilizado por ningún otro servicio (como un trabajo de Stream Analytics u otro entorno de Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="97b09-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="97b09-110">Si se usa el grupo de consumidores por otros servicios, lea la operación se ve afectada negativamente para este entorno y Hola otros servicios.</span><span class="sxs-lookup"><span data-stu-id="97b09-110">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="97b09-111">Si usas "$Default" como grupo de consumidores de hello, puede provocar toopotential reutilización por otro lector.</span><span class="sxs-lookup"><span data-stu-id="97b09-111">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

  ![Selección del grupo de consumidores del centro de eventos](media/send-events/consumer-group.png)

3. <span data-ttu-id="97b09-113">En el centro de eventos de hello, cree "MySendPolicy" que es toosend usa eventos en el ejemplo de Hola a csharp.</span><span class="sxs-lookup"><span data-stu-id="97b09-113">On hello event hub, create “MySendPolicy” that is used toosend events in hello csharp sample.</span></span>

  ![Seleccione Directivas de acceso compartido y haga clic en el botón Agregar](media/send-events/shared-access-policy.png)  

  ![Agregar nueva directiva de acceso compartido](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="97b09-116">Creación de un origen de eventos de Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="97b09-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="97b09-117">Si no ha creado un origen de eventos, siga [estas instrucciones](time-series-insights-add-event-source.md) toocreate un origen de eventos.</span><span class="sxs-lookup"><span data-stu-id="97b09-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) toocreate an event source.</span></span>

2. <span data-ttu-id="97b09-118">Especifique "deviceTimestamp" como nombre de propiedad de marca de tiempo de hello: esta propiedad se usa como Hola marca de tiempo real en el ejemplo de Hola a csharp.</span><span class="sxs-lookup"><span data-stu-id="97b09-118">Specify “deviceTimestamp” as hello timestamp property name – this property is used as hello actual timestamp in hello csharp sample.</span></span> <span data-ttu-id="97b09-119">nombre de propiedad de marca de tiempo de Hello distingue mayúsculas de minúsculas y valores deben tener el formato de hello __aaaa-MM-ddTHH. FFFFFFFK__ cuando se envían como concentrador de tooevent JSON.</span><span class="sxs-lookup"><span data-stu-id="97b09-119">hello timestamp property name is case-sensitive and values must follow hello format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON tooevent hub.</span></span> <span data-ttu-id="97b09-120">Si Hola propiedad no existe en el caso de hello, a continuación, hello hora del evento concentrador en cola se utiliza.</span><span class="sxs-lookup"><span data-stu-id="97b09-120">If hello property does not exist in hello event, then hello event hub enqueued time is used.</span></span>

  ![Creación de un origen de eventos](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a><span data-ttu-id="97b09-122">Eventos de toopush de código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="97b09-122">Sample code toopush events</span></span>
1. <span data-ttu-id="97b09-123">Vaya toohello política de concentrador de eventos "MySendPolicy" y copie la cadena de conexión de Hola con clave de la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-123">Go toohello event hub policy “MySendPolicy” and copy hello connection string with hello policy key.</span></span>

  ![Copia de la cadena de conexión de MySendPolicy](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="97b09-125">Ejecute hello después el código que toosend 600 los eventos por cada uno de los dispositivos de hello tres.</span><span class="sxs-lookup"><span data-stu-id="97b09-125">Run hello following code that toosend 600 events per each of hello three devices.</span></span> <span data-ttu-id="97b09-126">Reemplace `eventHubConnectionString` por su cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="97b09-126">Update `eventHubConnectionString` with your connection string.</span></span>

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

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="97b09-127">Formas de JSON admitidas</span><span class="sxs-lookup"><span data-stu-id="97b09-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="97b09-128">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="97b09-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="97b09-129">Entrada</span><span class="sxs-lookup"><span data-stu-id="97b09-129">Input</span></span>

<span data-ttu-id="97b09-130">Un objeto JSON simple.</span><span class="sxs-lookup"><span data-stu-id="97b09-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="97b09-131">Salida: 1 evento</span><span class="sxs-lookup"><span data-stu-id="97b09-131">Output - 1 event</span></span>

|<span data-ttu-id="97b09-132">id</span><span class="sxs-lookup"><span data-stu-id="97b09-132">id</span></span>|<span data-ttu-id="97b09-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="97b09-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="97b09-134">device1</span><span class="sxs-lookup"><span data-stu-id="97b09-134">device1</span></span>|<span data-ttu-id="97b09-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="97b09-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="97b09-136">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="97b09-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="97b09-137">Entrada</span><span class="sxs-lookup"><span data-stu-id="97b09-137">Input</span></span>
<span data-ttu-id="97b09-138">Una matriz JSON con dos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="97b09-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="97b09-139">Cada objeto JSON será eventos tooan convertido.</span><span class="sxs-lookup"><span data-stu-id="97b09-139">Each JSON object will be converted tooan event.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="97b09-140">Salida: 2 eventos</span><span class="sxs-lookup"><span data-stu-id="97b09-140">Output - 2 Events</span></span>

|<span data-ttu-id="97b09-141">id</span><span class="sxs-lookup"><span data-stu-id="97b09-141">id</span></span>|<span data-ttu-id="97b09-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="97b09-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="97b09-143">device1</span><span class="sxs-lookup"><span data-stu-id="97b09-143">device1</span></span>|<span data-ttu-id="97b09-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="97b09-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="97b09-145">device2</span><span class="sxs-lookup"><span data-stu-id="97b09-145">device2</span></span>|<span data-ttu-id="97b09-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="97b09-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="97b09-147">Ejemplo 3</span><span class="sxs-lookup"><span data-stu-id="97b09-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="97b09-148">Entrada</span><span class="sxs-lookup"><span data-stu-id="97b09-148">Input</span></span>

<span data-ttu-id="97b09-149">Un objeto JSON con una matriz JSON anidada que contiene dos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="97b09-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="97b09-150">Salida: 2 eventos</span><span class="sxs-lookup"><span data-stu-id="97b09-150">Output - 2 Events</span></span>
<span data-ttu-id="97b09-151">Tenga en cuenta que propiedad Hola "location" se copió tooeach de evento Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-151">Note that hello property "location" is copied over tooeach of hello event.</span></span>

|<span data-ttu-id="97b09-152">location</span><span class="sxs-lookup"><span data-stu-id="97b09-152">location</span></span>|<span data-ttu-id="97b09-153">events.id</span><span class="sxs-lookup"><span data-stu-id="97b09-153">events.id</span></span>|<span data-ttu-id="97b09-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="97b09-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="97b09-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="97b09-155">WestUs</span></span>|<span data-ttu-id="97b09-156">device1</span><span class="sxs-lookup"><span data-stu-id="97b09-156">device1</span></span>|<span data-ttu-id="97b09-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="97b09-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="97b09-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="97b09-158">WestUs</span></span>|<span data-ttu-id="97b09-159">device2</span><span class="sxs-lookup"><span data-stu-id="97b09-159">device2</span></span>|<span data-ttu-id="97b09-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="97b09-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="97b09-161">Ejemplo 4</span><span class="sxs-lookup"><span data-stu-id="97b09-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="97b09-162">Entrada</span><span class="sxs-lookup"><span data-stu-id="97b09-162">Input</span></span>

<span data-ttu-id="97b09-163">Un objeto JSON con una matriz JSON anidada que contiene dos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="97b09-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="97b09-164">Esta entrada muestra que las propiedades globales de hello pueden estar representadas por el objeto JSON complejo de Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-164">This input demonstrates that hello global properties may be represented by hello complex JSON object.</span></span>

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
#### <a name="output---2-events"></a><span data-ttu-id="97b09-165">Salida: 2 eventos</span><span class="sxs-lookup"><span data-stu-id="97b09-165">Output - 2 Events</span></span>

|<span data-ttu-id="97b09-166">location</span><span class="sxs-lookup"><span data-stu-id="97b09-166">location</span></span>|<span data-ttu-id="97b09-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="97b09-167">manufacturer.name</span></span>|<span data-ttu-id="97b09-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="97b09-168">manufacturer.location</span></span>|<span data-ttu-id="97b09-169">events.id</span><span class="sxs-lookup"><span data-stu-id="97b09-169">events.id</span></span>|<span data-ttu-id="97b09-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="97b09-170">events.timestamp</span></span>|<span data-ttu-id="97b09-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="97b09-171">events.data.type</span></span>|<span data-ttu-id="97b09-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="97b09-172">events.data.units</span></span>|<span data-ttu-id="97b09-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="97b09-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="97b09-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="97b09-174">WestUs</span></span>|<span data-ttu-id="97b09-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="97b09-175">manufacturer1</span></span>|<span data-ttu-id="97b09-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="97b09-176">EastUs</span></span>|<span data-ttu-id="97b09-177">device1</span><span class="sxs-lookup"><span data-stu-id="97b09-177">device1</span></span>|<span data-ttu-id="97b09-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="97b09-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="97b09-179">pressure</span><span class="sxs-lookup"><span data-stu-id="97b09-179">pressure</span></span>|<span data-ttu-id="97b09-180">psi</span><span class="sxs-lookup"><span data-stu-id="97b09-180">psi</span></span>|<span data-ttu-id="97b09-181">108.09</span><span class="sxs-lookup"><span data-stu-id="97b09-181">108.09</span></span>|
|<span data-ttu-id="97b09-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="97b09-182">WestUs</span></span>|<span data-ttu-id="97b09-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="97b09-183">manufacturer1</span></span>|<span data-ttu-id="97b09-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="97b09-184">EastUs</span></span>|<span data-ttu-id="97b09-185">device2</span><span class="sxs-lookup"><span data-stu-id="97b09-185">device2</span></span>|<span data-ttu-id="97b09-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="97b09-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="97b09-187">vibration</span><span class="sxs-lookup"><span data-stu-id="97b09-187">vibration</span></span>|<span data-ttu-id="97b09-188">abs G</span><span class="sxs-lookup"><span data-stu-id="97b09-188">abs G</span></span>|<span data-ttu-id="97b09-189">217.09</span><span class="sxs-lookup"><span data-stu-id="97b09-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="97b09-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97b09-190">Next steps</span></span>

* <span data-ttu-id="97b09-191">Vea el entorno en el [portal de Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="97b09-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
