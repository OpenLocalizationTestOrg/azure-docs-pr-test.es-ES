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
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a>Entorno de visión de la serie de tiempo de tooa de eventos con el concentrador de eventos de envío

Este tutorial le explica cómo toocreate Configurar centro de eventos y ejecutar un toopush de la aplicación de ejemplo de eventos. Si tiene un centro de eventos existente con eventos en formato JSON, pase por alto este tutorial y vea su entorno en [Time Series Insights](https://insights.timeseries.azure.com).

## <a name="configure-an-event-hub"></a>Configuración de un centro de eventos
1. toocreate un concentrador de eventos, siga las instrucciones de hello concentrador de eventos [documentación](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).

2. Asegúrese de crear un grupo de consumidores que sea utilizado exclusivamente por el origen de eventos de Time Series Insights.

  > [!IMPORTANT]
  > Asegúrese de que el grupo de consumidores no es utilizado por ningún otro servicio (como un trabajo de Stream Analytics u otro entorno de Time Series Insights). Si se usa el grupo de consumidores por otros servicios, lea la operación se ve afectada negativamente para este entorno y Hola otros servicios. Si usas "$Default" como grupo de consumidores de hello, puede provocar toopotential reutilización por otro lector.

  ![Selección del grupo de consumidores del centro de eventos](media/send-events/consumer-group.png)

3. En el centro de eventos de hello, cree "MySendPolicy" que es toosend usa eventos en el ejemplo de Hola a csharp.

  ![Seleccione Directivas de acceso compartido y haga clic en el botón Agregar](media/send-events/shared-access-policy.png)  

  ![Agregar nueva directiva de acceso compartido](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Creación de un origen de eventos de Time Series Insights
1. Si no ha creado un origen de eventos, siga [estas instrucciones](time-series-insights-add-event-source.md) toocreate un origen de eventos.

2. Especifique "deviceTimestamp" como nombre de propiedad de marca de tiempo de hello: esta propiedad se usa como Hola marca de tiempo real en el ejemplo de Hola a csharp. nombre de propiedad de marca de tiempo de Hello distingue mayúsculas de minúsculas y valores deben tener el formato de hello __aaaa-MM-ddTHH. FFFFFFFK__ cuando se envían como concentrador de tooevent JSON. Si Hola propiedad no existe en el caso de hello, a continuación, hello hora del evento concentrador en cola se utiliza.

  ![Creación de un origen de eventos](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a>Eventos de toopush de código de ejemplo
1. Vaya toohello política de concentrador de eventos "MySendPolicy" y copie la cadena de conexión de Hola con clave de la directiva de Hola.

  ![Copia de la cadena de conexión de MySendPolicy](media/send-events/sample-code-connection-string.png)

2. Ejecute hello después el código que toosend 600 los eventos por cada uno de los dispositivos de hello tres. Reemplace `eventHubConnectionString` por su cadena de conexión.

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
## <a name="supported-json-shapes"></a>Formas de JSON admitidas
### <a name="sample-1"></a>Ejemplo 1

#### <a name="input"></a>Entrada

Un objeto JSON simple.

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a>Salida: 1 evento

|id|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|

### <a name="sample-2"></a>Ejemplo 2

#### <a name="input"></a>Entrada
Una matriz JSON con dos objetos JSON. Cada objeto JSON será eventos tooan convertido.
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
#### <a name="output---2-events"></a>Salida: 2 eventos

|id|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|
|device2|2016-01-08T01:17:00Z|
### <a name="sample-3"></a>Ejemplo 3

#### <a name="input"></a>Entrada

Un objeto JSON con una matriz JSON anidada que contiene dos objetos JSON.
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
#### <a name="output---2-events"></a>Salida: 2 eventos
Tenga en cuenta que propiedad Hola "location" se copió tooeach de evento Hola.

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|device1|2016-01-08T01:08:00Z|
|WestUs|device2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>Ejemplo 4

#### <a name="input"></a>Entrada

Un objeto JSON con una matriz JSON anidada que contiene dos objetos JSON. Esta entrada muestra que las propiedades globales de hello pueden estar representadas por el objeto JSON complejo de Hola.

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
#### <a name="output---2-events"></a>Salida: 2 eventos

|location|manufacturer.name|manufacturer.location|events.id|events.timestamp|events.data.type|events.data.units|events.data.value|
|---|---|---|---|---|---|---|---|
|WestUs|manufacturer1|EastUs|device1|2016-01-08T01:08:00Z|pressure|psi|108.09|
|WestUs|manufacturer1|EastUs|device2|2016-01-08T01:17:00Z|vibration|abs G|217.09|

## <a name="next-steps"></a>Pasos siguientes

* Vea el entorno en el [portal de Time Series Insights](https://insights.timeseries.azure.com)
