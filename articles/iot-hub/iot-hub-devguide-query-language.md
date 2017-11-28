---
title: "Información sobre el lenguaje de consulta de IoT Hub de Azure | Microsoft Docs"
description: "Guía del desarrollador: descripción del lenguaje de consulta de IoT Hub de tipo SQL que se usa para recuperar información sobre los dispositivos gemelos y trabajos desde IoT Hub."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: a7650104eda58923558892f6f0f6666d16dbce28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="f4f3e-103">Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos, trabajos y enrutamiento de mensajes</span><span class="sxs-lookup"><span data-stu-id="f4f3e-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="f4f3e-104">IoT Hub proporciona un lenguaje eficaz de tipo SQL para recuperar información sobre [dispositivos gemelos][lnk-twins], [trabajos][lnk-jobs] y [enrutamiento de mensajes][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="f4f3e-104">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="f4f3e-105">Este artículo presenta:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-105">This article presents:</span></span>

* <span data-ttu-id="f4f3e-106">una introducción a las características principales del lenguaje de consulta de IoT Hub y</span><span class="sxs-lookup"><span data-stu-id="f4f3e-106">An introduction to the major features of the IoT Hub query language, and</span></span>
* <span data-ttu-id="f4f3e-107">una descripción más detallada del lenguaje.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-107">The detailed description of the language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="f4f3e-108">Introducción a las consultas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="f4f3e-108">Get started with device twin queries</span></span>
<span data-ttu-id="f4f3e-109">Los [dispositivos gemelos][lnk-twins] pueden contener objetos JSON arbitrarios como etiquetas y propiedades.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="f4f3e-110">IoT Hub permite consultar los dispositivos gemelos como un solo documento JSON que contiene toda la información de los dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-110">IoT Hub enables you to query device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="f4f3e-111">Por ejemplo, supongamos que los dispositivos gemelos de IoT Hub tienen la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-111">Assume, for instance, that your IoT hub device twins have the following structure:</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

<span data-ttu-id="f4f3e-112">IoT Hub expone los dispositivos gemelos como una colección de documentos denominada **devices**.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-112">IoT Hub exposes the device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="f4f3e-113">Por lo tanto, la consulta siguiente recupera el conjunto completo de dispositivos gemelos:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-113">So the following query retrieves the whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="f4f3e-114">Los [SDK IoT de Azure][lnk-hub-sdks] admiten la paginación de resultados de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="f4f3e-115">IoT Hub permite recuperar dispositivos gemelos filtrando por condiciones arbitrarias.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-115">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="f4f3e-116">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="f4f3e-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="f4f3e-117">recupera los dispositivos gemelos con la etiqueta **location.region** establecida en **US**.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-117">retrieves the device twins with the **location.region** tag set to **US**.</span></span>
<span data-ttu-id="f4f3e-118">También se admiten operadores booleanos y comparaciones aritméticas, por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="f4f3e-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="f4f3e-119">recupera todos los dispositivos gemelos ubicados en Estados Unidos configurados para enviar datos de telemetría con una frecuencia inferior a un minuto.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-119">retrieves all device twins located in the US configured to send telemetry less often than every minute.</span></span> <span data-ttu-id="f4f3e-120">Por comodidad, también es posible usar constantes de matriz con los operadores **IN** (En) y **NIN** (No en).</span><span class="sxs-lookup"><span data-stu-id="f4f3e-120">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="f4f3e-121">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="f4f3e-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="f4f3e-122">recupera todos los dispositivos gemelos que notificaron conectividad WiFi o con cable.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="f4f3e-123">A menudo, es necesario identificar a todos los dispositivos gemelos que contienen una propiedad concreta.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-123">It is often necessary to identify all device twins that contain a specific property.</span></span> <span data-ttu-id="f4f3e-124">IoT Hub admite la función `is_defined()` para esta finalidad.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-124">IoT Hub supports the function `is_defined()` for this purpose.</span></span> <span data-ttu-id="f4f3e-125">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="f4f3e-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="f4f3e-126">recupera todos los dispositivos gemelos que definen la propiedad notificada `connectivity`.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-126">retrieved all device twins that define the `connectivity` reported property.</span></span> <span data-ttu-id="f4f3e-127">Consulte la sección [Cláusula WHERE][lnk-query-where] para obtener la referencia completa de las funcionalidades de filtrado.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-127">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span></span>

<span data-ttu-id="f4f3e-128">También se admiten la agrupación y las agregaciones.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="f4f3e-129">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="f4f3e-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="f4f3e-130">devuelve el recuento de los dispositivos en cada estado de configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-130">returns the count of the devices in each telemetry configuration status.</span></span>

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

<span data-ttu-id="f4f3e-131">En el ejemplo anterior, se demuestra una situación en la que tres dispositivos notificaron una configuración correcta, dos aún están aplicándola y uno notificó un error.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-131">The preceding example illustrates a situation where three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="f4f3e-132">Ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="f4f3e-132">C# example</span></span>
<span data-ttu-id="f4f3e-133">El [SDK del servicio C#][lnk-hub-sdks] expone la funcionalidad de consulta en la clase **RegistryManager**.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-133">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span></span>
<span data-ttu-id="f4f3e-134">Este ejemplo corresponde a una consulta simple:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-134">Here is an example of a simple query:</span></span>

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

<span data-ttu-id="f4f3e-135">Observe cómo se crea una instancia del objeto **query** con un tamaño de página (hasta 1000) y después se pueden recuperar varias páginas llamando a los métodos **GetNextAsTwinAsync** varias veces.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-135">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="f4f3e-136">Tenga en cuenta que el objeto query expone varios elementos **next\***, según la opción de deserialización que requiera la consulta, como objetos de trabajo o dispositivo gemelo, o JSON sin formato que se usará cuando se utilicen proyecciones.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-136">Note that the query object exposes multiple **Next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="f4f3e-137">Ejemplo de Node.js</span><span class="sxs-lookup"><span data-stu-id="f4f3e-137">Node.js example</span></span>
<span data-ttu-id="f4f3e-138">El [SDK de servicios IoT de Azure para Node.js][lnk-hub-sdks] expone la funcionalidad de consulta en el objeto **Registry**.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-138">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span></span>
<span data-ttu-id="f4f3e-139">Este ejemplo corresponde a una consulta simple:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed to fetch the results: ' + err.message);
    } else {
        // Do something with the results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

<span data-ttu-id="f4f3e-140">Observe cómo se crea una instancia del objeto **query** con un tamaño de página (hasta 1000) y después se pueden recuperar varias páginas llamando a los métodos **nextAsTwin** varias veces.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-140">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="f4f3e-141">Tenga en cuenta que el objeto query expone varios elementos **next\***, según la opción de deserialización que requiera la consulta, como objetos de trabajo o dispositivo gemelo, o JSON sin formato que se usará cuando se utilicen proyecciones.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-141">Note that the query object exposes multiple **next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="f4f3e-142">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="f4f3e-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f4f3e-143">Los resultados de las consultas pueden demorarse unos minutos con respecto a los valores más recientes en los dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-143">Query results can have a few minutes of delay with respect to the latest values in device twins.</span></span> <span data-ttu-id="f4f3e-144">Si realiza consultas a dispositivos gemelos individuales por identificador, siempre resultará preferible utilizar la API de dispositivos gemelos de recuperación, que contendrá en todo momento los valores más recientes y cuenta con umbrales de limitación superiores.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-144">If querying individual device twins by id, it is always preferable to use the retrieve device twin API, which always contains the latest values and has higher throttling limits.</span></span>

<span data-ttu-id="f4f3e-145">Actualmente, las comparaciones solo se admiten entre tipos primitivos (no objetos), por ejemplo `... WHERE properties.desired.config = properties.reported.config` solo se admite si esas propiedades tienen valores primitivos.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="f4f3e-146">Introducción a las consultas de trabajos</span><span class="sxs-lookup"><span data-stu-id="f4f3e-146">Get started with jobs queries</span></span>
<span data-ttu-id="f4f3e-147">Los [trabajos][lnk-jobs] proporcionan una forma de ejecutar operaciones en conjuntos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-147">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span></span> <span data-ttu-id="f4f3e-148">Cada dispositivo gemelo contiene la información de los trabajos de los que forma parte en una colección denominada **jobs**.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-148">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="f4f3e-149">Lógicamente,</span><span class="sxs-lookup"><span data-stu-id="f4f3e-149">Logically,</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

<span data-ttu-id="f4f3e-150">Ahora, esta colección se puede consultar como **devices.jobs** en el lenguaje de consulta de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-150">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4f3e-151">Actualmente, la propiedad jobs no se devuelve nunca cuando se consulta a dispositivos gemelos (es decir, las consultas que contienen "FROM devices").</span><span class="sxs-lookup"><span data-stu-id="f4f3e-151">Currently, the jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="f4f3e-152">Solo es accesible directamente con las consultas que utilizan `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="f4f3e-153">Por ejemplo, para obtener todos los trabajos (pasados y programados) que afecten a un único dispositivo, puede usar la siguiente consulta:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-153">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="f4f3e-154">Observe cómo esta consulta proporciona el estado específico del dispositivo (y posiblemente la respuesta del método directo) para cada trabajo devuelto.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-154">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span></span>
<span data-ttu-id="f4f3e-155">También es posible filtrar por condiciones booleanas arbitrarias en todas las propiedades de objeto de la colección **devices.jobs**.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-155">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span></span>
<span data-ttu-id="f4f3e-156">Por ejemplo, la siguiente consulta:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-156">For instance, the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="f4f3e-157">recupera todos los trabajos de actualización de dispositivos gemelos completados para el dispositivo **myDeviceId** que se crearon después de septiembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="f4f3e-158">También es posible recuperar los resultados por dispositivo de un único trabajo.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-158">It is also possible to retrieve the per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="f4f3e-159">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="f4f3e-159">Limitations</span></span>
<span data-ttu-id="f4f3e-160">Actualmente, las consultas en **devices.jobs** no admiten:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="f4f3e-161">proyecciones, por lo tanto, solo `SELECT *` es posible.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="f4f3e-162">condiciones que hagan referencia al dispositivo gemelo, además de a las propiedades de trabajo (vea la sección anterior).</span><span class="sxs-lookup"><span data-stu-id="f4f3e-162">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span></span>
* <span data-ttu-id="f4f3e-163">realizar agregaciones, como count, avg, group by.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="f4f3e-164">Introducción a expresiones de consulta de rutas de mensajes de dispositivo a la nube</span><span class="sxs-lookup"><span data-stu-id="f4f3e-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="f4f3e-165">Con las [rutas de dispositivo a la nube][lnk-devguide-messaging-routes], puede configurar IoT Hub para enviar mensajes de dispositivo a la nube en diferentes puntos de conexión en función de expresiones evaluadas frente a mensajes individuales.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="f4f3e-166">La ruta [condición][lnk-query-expressions] utiliza el mismo lenguaje de consultas de IoT Hub como condiciones en consultas gemelas y de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-166">The route [condition][lnk-query-expressions] uses the same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="f4f3e-167">Las condiciones de enrutamiento se evalúan en el cuerpo y los encabezados del mensaje.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-167">Route conditions are evaluated on the message headers and body.</span></span> <span data-ttu-id="f4f3e-168">La expresión de consulta de enrutamiento puede implicar solo los encabezados del mensaje, solo el cuerpo del mensaje o tanto los encabezados como el cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-168">Your routing query expression may involve only message headers, only the message body, or both message headers and message body.</span></span> <span data-ttu-id="f4f3e-169">IoT Hub da por supuesto un esquema específico para los encabezados y el cuerpo del mensaje con el fin de enrutar mensajes, y las secciones siguientes describen los elementos que se necesitan para que IoT Hub realice correctamente el enrutamiento:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-169">IoT Hub assumes a specific schema for the headers and message body in order to route messages, and the following sections describe what is required for IoT Hub to properly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="f4f3e-170">Enrutamiento en los encabezados del mensaje</span><span class="sxs-lookup"><span data-stu-id="f4f3e-170">Routing on message headers</span></span>

<span data-ttu-id="f4f3e-171">IoT Hub da por supuesto la siguiente representación JSON de los encabezados del mensaje para el enrutamiento del mensaje:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-171">IoT Hub assumes the following JSON representation of message headers for message routing:</span></span>

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

<span data-ttu-id="f4f3e-172">Las propiedades del sistema de mensajes tienen como prefijo el símbolo `'$'`.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-172">Message system properties are prefixed with the `'$'` symbol.</span></span>
<span data-ttu-id="f4f3e-173">Siempre se accede a las propiedades de usuario con su nombre.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="f4f3e-174">Si sucede que un nombre de propiedad de usuario coincide con el de una propiedad del sistema (como `$to`), se recuperará la propiedad de usuario con la expresión `$to`.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-174">If a user property name happens to coincide with a system property (such as `$to`), the user property will be retrieved with the `$to` expression.</span></span>
<span data-ttu-id="f4f3e-175">Siempre puede acceder a la propiedad del sistema mediante corchetes `{}`: por ejemplo, puede usar la expresión `{$to}` para acceder a la propiedad del sistema `to`.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-175">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$to}` to access the system property `to`.</span></span> <span data-ttu-id="f4f3e-176">Los nombres de propiedad entre corchetes siempre permiten recuperar la propiedad del sistema correspondiente.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-176">Bracketed property names always retrieve the corresponding system property.</span></span>

<span data-ttu-id="f4f3e-177">Recuerde que los nombres de propiedad no distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="f4f3e-178">Todas las propiedades de mensaje son cadenas.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-178">All message properties are strings.</span></span> <span data-ttu-id="f4f3e-179">Las propiedades del sistema, como se describen en la [guía del desarrollador][lnk-devguide-messaging-format], no están disponibles para su uso en las consultas.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-179">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span></span>
>

<span data-ttu-id="f4f3e-180">Por ejemplo, si utiliza una propiedad `messageType`, puede enrutar toda la telemetría a un punto de conexión y todas las alertas a otro punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-180">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span></span> <span data-ttu-id="f4f3e-181">Puede escribir la siguiente expresión para enrutar la telemetría:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-181">You can write the following expression to route the telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="f4f3e-182">Y la siguiente expresión para enrutar los mensajes de alerta:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-182">And the following expression to route the alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="f4f3e-183">También se admiten las funciones y expresiones booleanas.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="f4f3e-184">Esta característica le permite distinguir entre el nivel de gravedad, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-184">This feature enables you to distinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="f4f3e-185">Consulte la sección [Expresiones y condiciones][lnk-query-expressions] para obtener la lista completa de funciones y operadores compatibles.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-185">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="f4f3e-186">Enrutamiento en los cuerpos del mensaje</span><span class="sxs-lookup"><span data-stu-id="f4f3e-186">Routing on message bodies</span></span>

<span data-ttu-id="f4f3e-187">IoT Hub solo puede realizar el enrutamiento según el contenido del cuerpo del mensaje si este tiene un formato JSON correcto codificado en UTF-8, UTF-16 o UTF-32.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-187">IoT Hub can only route based on message body contents if the message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="f4f3e-188">Debe establecer el tipo de contenido del mensaje en `application/json` y la codificación de contenido en una de las codificaciones UTF compatibles en los encabezados del mensaje para permitir que IoT Hub enrute el mensaje según el contenido del cuerpo.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-188">You must set the content type of the message to `application/json` and the content encoding to one of the supported UTF encodings in the message headers to allow IoT Hub to route the message based on the body contents.</span></span> <span data-ttu-id="f4f3e-189">Si no se especifica cualquiera de los encabezados, IoT Hub no intentará evaluar ninguna expresión de consulta que implique el cuerpo con respecto al mensaje.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-189">If either of the headers is not specified, IoT Hub will not attempt to evaluate any query expression involving the body against the message.</span></span> <span data-ttu-id="f4f3e-190">Si el mensaje no es un mensaje JSON o si no especifica el tipo de contenido ni la codificación de contenido, se puede seguir usando el enrutamiento de mensaje para enrutar el mensaje según los encabezados del mensaje.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-190">If your message is not a JSON message, or if the message does not specify the content type and content encoding, you may still use message routing to route the message based on the message headers.</span></span>

<span data-ttu-id="f4f3e-191">Puede usar `$body` en la expresión de consulta para enrutar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-191">You can use `$body` in the query expression to route the message.</span></span> <span data-ttu-id="f4f3e-192">Puede usar una referencia al cuerpo simple, una referencia a la matriz del cuerpo o varias referencias al cuerpo en la expresión de consulta.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-192">You can use a simple body reference, body array reference, or multiple body references in the query expression.</span></span> <span data-ttu-id="f4f3e-193">La expresión de consulta también puede combinar una referencia al cuerpo con una referencia al encabezado del mensaje.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="f4f3e-194">Por ejemplo, todas las expresiones siguientes son expresiones de consulta válidas:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-194">For example, the following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="f4f3e-195">Conceptos básicos de una consulta de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="f4f3e-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="f4f3e-196">Cada consulta de IoT Hub consta de cláusulas SELECT y FROM, y de cláusulas WHERE y GROUP BY opcionales.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="f4f3e-197">Cada consulta se ejecuta en una colección de documentos JSON, por ejemplo, dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="f4f3e-198">La cláusula FROM indica la colección de documentos en la que se va a iterar (**devices** o **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="f4f3e-198">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="f4f3e-199">Después se aplica el filtro en la cláusula WHERE.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-199">Then, the filter in the WHERE clause is applied.</span></span> <span data-ttu-id="f4f3e-200">Con las agregaciones, se agrupan los resultados de este paso como se especifica en la cláusula GROUP BY y, para cada grupo, se genera una fila como se especifica en la cláusula SELECT.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-200">With aggregations, the results of this step are grouped as specified in the GROUP BY clause and, for each group, a row is generated as specified in the SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="f4f3e-201">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="f4f3e-201">FROM clause</span></span>
<span data-ttu-id="f4f3e-202">La cláusula **FROM <from_specification>** solo puede suponer dos valores: **FROM devices**, para consultar dispositivos gemelos, o **FROM devices.jobs**, para consultar detalles por dispositivo del trabajo.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-202">The **FROM <from_specification>** clause can assume only two values: **FROM devices**, to query device twins, or **FROM devices.jobs**, to query job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="f4f3e-203">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="f4f3e-203">WHERE clause</span></span>
<span data-ttu-id="f4f3e-204">La cláusula **WHERE <filter_condition>** es opcional.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-204">The **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="f4f3e-205">Especifica una o varias condiciones que los documentos JSON en la colección FROM deben satisfacer para incluirse como parte del resultado.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-205">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span></span> <span data-ttu-id="f4f3e-206">Cualquier documento JSON debe evaluar las condiciones especificadas como "true" para que se incluya en el resultado.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-206">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span></span>

<span data-ttu-id="f4f3e-207">Las condiciones permitidas se describen en la sección [Expresiones y condiciones][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="f4f3e-207">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="f4f3e-208">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="f4f3e-208">SELECT clause</span></span>
<span data-ttu-id="f4f3e-209">La cláusula SELECT (**SELECT <select_list>**) es obligatoria y especifica qué valores se recuperan de la consulta.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-209">The SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from the query.</span></span> <span data-ttu-id="f4f3e-210">Especifica los valores JSON que se usarán para generar nuevos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-210">It specifies the JSON values to be used to generate new JSON objects.</span></span>
<span data-ttu-id="f4f3e-211">Para cada elemento del subconjunto filtrado (y, opcionalmente, agrupado) de la colección FROM, la fase de proyección genera un nuevo objeto JSON, construido con los valores especificados en la cláusula SELECT.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-211">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object, constructed with the values specified in the SELECT clause.</span></span>

<span data-ttu-id="f4f3e-212">Esta es la gramática de la cláusula SELECT:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-212">Following is the grammar of the SELECT clause:</span></span>

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

<span data-ttu-id="f4f3e-213">donde **attribute_name** hace referencia a cualquier propiedad del documento JSON en la colección FROM.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-213">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span> <span data-ttu-id="f4f3e-214">Puede ver algunos ejemplos de las cláusulas SELECT en la sección [Introducción a las consultas de gemelos][lnk-query-getstarted].</span><span class="sxs-lookup"><span data-stu-id="f4f3e-214">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="f4f3e-215">Actualmente, las cláusulas de selección distintas a **SELECT \*** solo se admiten en las consultas agregadas de dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="f4f3e-216">Cláusula GROUP BY</span><span class="sxs-lookup"><span data-stu-id="f4f3e-216">GROUP BY clause</span></span>
<span data-ttu-id="f4f3e-217">La cláusula **GROUP BY <group_specification>** es un paso opcional que se puede ejecutar después del filtro especificado en la cláusula WHERE y antes de la proyección especificada en la cláusula SELECT.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-217">The **GROUP BY <group_specification>** clause is an optional step that can be executed after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span></span> <span data-ttu-id="f4f3e-218">Agrupa los documentos según el valor de un atributo.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-218">It groups documents based on the value of an attribute.</span></span> <span data-ttu-id="f4f3e-219">Estos grupos se usan para generar valores agregados, como se especifica en la cláusula SELECT.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-219">These groups are used to generate aggregated values as specified in the SELECT clause.</span></span>

<span data-ttu-id="f4f3e-220">Un ejemplo de consulta con GROUP BY es:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="f4f3e-221">La sintaxis formal de GROUP BY es:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-221">The formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="f4f3e-222">donde **attribute_name** hace referencia a cualquier propiedad del documento JSON en la colección FROM.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-222">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span>

<span data-ttu-id="f4f3e-223">Actualmente, solo se admite la cláusula GROUP BY al consultar dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-223">Currently, the GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="f4f3e-224">Expresiones y condiciones</span><span class="sxs-lookup"><span data-stu-id="f4f3e-224">Expressions and conditions</span></span>
<span data-ttu-id="f4f3e-225">Brevemente, una *expresión*:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="f4f3e-226">Se evalúa como una instancia de tipo JSON (como booleano, número, cadena, matriz u objeto), y</span><span class="sxs-lookup"><span data-stu-id="f4f3e-226">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="f4f3e-227">Se define manipulando datos procedentes del documento JSON del dispositivo y constantes mediante funciones y operadores integrados.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-227">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="f4f3e-228">Las *condiciones* son expresiones que se evalúan como un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-228">*Conditions* are expressions that evaluate to a Boolean.</span></span> <span data-ttu-id="f4f3e-229">Cualquier constante diferente del booleano **true** se considera **false** (incluidos **null**, **undefined**, cualquier instancia de objeto o matriz, cualquier cadena y, obviamente, el booleano **false**).</span><span class="sxs-lookup"><span data-stu-id="f4f3e-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly the Boolean **false**).</span></span>

<span data-ttu-id="f4f3e-230">La sintaxis de las expresiones es:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-230">The syntax for expressions is:</span></span>

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

<span data-ttu-id="f4f3e-231">donde:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-231">where:</span></span>

| <span data-ttu-id="f4f3e-232">Símbolo</span><span class="sxs-lookup"><span data-stu-id="f4f3e-232">Symbol</span></span> | <span data-ttu-id="f4f3e-233">Definición</span><span class="sxs-lookup"><span data-stu-id="f4f3e-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="f4f3e-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="f4f3e-234">attribute_name</span></span> | <span data-ttu-id="f4f3e-235">Cualquier propiedad del documento JSON en la colección **FROM**.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-235">Any property of the JSON document in the **FROM** collection.</span></span> |
| <span data-ttu-id="f4f3e-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="f4f3e-236">binary_operator</span></span> | <span data-ttu-id="f4f3e-237">Cualquier operador binario que figure en la sección [Operadores](#operators).</span><span class="sxs-lookup"><span data-stu-id="f4f3e-237">Any binary operator listed in the [Operators](#operators) section.</span></span> |
| <span data-ttu-id="f4f3e-238">function_name</span><span class="sxs-lookup"><span data-stu-id="f4f3e-238">function_name</span></span>| <span data-ttu-id="f4f3e-239">Cualquier función que figure en la sección [Funciones](#functions).</span><span class="sxs-lookup"><span data-stu-id="f4f3e-239">Any function listed in the [Functions](#functions) section.</span></span> |
| <span data-ttu-id="f4f3e-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="f4f3e-240">decimal_literal</span></span> |<span data-ttu-id="f4f3e-241">Un valor float expresado en notación decimal.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="f4f3e-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="f4f3e-242">hexadecimal_literal</span></span> |<span data-ttu-id="f4f3e-243">Un número expresado por la cadena "0x" seguida de una cadena de dígitos hexadecimales.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-243">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="f4f3e-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="f4f3e-244">string_literal</span></span> |<span data-ttu-id="f4f3e-245">Los literales de cadena son cadenas Unicode representadas por una secuencia de cero o varios caracteres Unicode o secuencias de escape.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="f4f3e-246">Los literales de cadena se encierran entre comillas simples (apóstrofo: ') o comillas dobles (comillas: ").</span><span class="sxs-lookup"><span data-stu-id="f4f3e-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="f4f3e-247">Caracteres de escape permitidos: `\'`, `\"`, `\\`, `\uXXXX` para los caracteres Unicode definidos con 4 dígitos hexadecimales.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="f4f3e-248">Operadores</span><span class="sxs-lookup"><span data-stu-id="f4f3e-248">Operators</span></span>
<span data-ttu-id="f4f3e-249">Se admiten los siguientes operadores:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-249">The following operators are supported:</span></span>

| <span data-ttu-id="f4f3e-250">Familia</span><span class="sxs-lookup"><span data-stu-id="f4f3e-250">Family</span></span> | <span data-ttu-id="f4f3e-251">Operadores</span><span class="sxs-lookup"><span data-stu-id="f4f3e-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="f4f3e-252">Aritméticos</span><span class="sxs-lookup"><span data-stu-id="f4f3e-252">Arithmetic</span></span> |<span data-ttu-id="f4f3e-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="f4f3e-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="f4f3e-254">Lógicos</span><span class="sxs-lookup"><span data-stu-id="f4f3e-254">Logical</span></span> |<span data-ttu-id="f4f3e-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="f4f3e-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="f4f3e-256">De comparación</span><span class="sxs-lookup"><span data-stu-id="f4f3e-256">Comparison</span></span> |<span data-ttu-id="f4f3e-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="f4f3e-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="f4f3e-258">Funciones</span><span class="sxs-lookup"><span data-stu-id="f4f3e-258">Functions</span></span>
<span data-ttu-id="f4f3e-259">Cuando se consultan gemelos y trabajos, la única función admitida es:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-259">When querying twins and jobs the only supported function is:</span></span>

| <span data-ttu-id="f4f3e-260">Función</span><span class="sxs-lookup"><span data-stu-id="f4f3e-260">Function</span></span> | <span data-ttu-id="f4f3e-261">Descripción</span><span class="sxs-lookup"><span data-stu-id="f4f3e-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="f4f3e-262">IS_DEFINED(property)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="f4f3e-263">Devuelve un valor booleano que indica si se ha asignado un valor a la propiedad (incluido `null`).</span><span class="sxs-lookup"><span data-stu-id="f4f3e-263">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="f4f3e-264">En condiciones de rutas, se admiten las siguientes funciones matemáticas:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-264">In routes conditions, the following math functions are supported:</span></span>

| <span data-ttu-id="f4f3e-265">Función</span><span class="sxs-lookup"><span data-stu-id="f4f3e-265">Function</span></span> | <span data-ttu-id="f4f3e-266">Descripción</span><span class="sxs-lookup"><span data-stu-id="f4f3e-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="f4f3e-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-267">ABS(x)</span></span> | <span data-ttu-id="f4f3e-268">Devuelve el valor absoluto (positivo) de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-268">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| <span data-ttu-id="f4f3e-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-269">EXP(x)</span></span> | <span data-ttu-id="f4f3e-270">Devuelve el valor exponencial de la expresión numérica especificada (e^x).</span><span class="sxs-lookup"><span data-stu-id="f4f3e-270">Returns the exponential value of the specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="f4f3e-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-271">POWER(x,y)</span></span> | <span data-ttu-id="f4f3e-272">Devuelve el valor de la expresión especificada a la potencia especificada (x^y).</span><span class="sxs-lookup"><span data-stu-id="f4f3e-272">Returns the value of the specified expression to the specified power (x^y).</span></span>|
| <span data-ttu-id="f4f3e-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-273">SQUARE(x)</span></span> | <span data-ttu-id="f4f3e-274">Devuelve el cuadrado del valor numérico especificado.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-274">Returns the square of the specified numeric value.</span></span> |
| <span data-ttu-id="f4f3e-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-275">CEILING(x)</span></span> | <span data-ttu-id="f4f3e-276">Devuelve el valor entero más pequeño mayor o igual que la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-276">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| <span data-ttu-id="f4f3e-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-277">FLOOR(x)</span></span> | <span data-ttu-id="f4f3e-278">Devuelve el valor entero más grande menor o igual que la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-278">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| <span data-ttu-id="f4f3e-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-279">SIGN(x)</span></span> | <span data-ttu-id="f4f3e-280">Devuelve el signo positivo (+1), cero (0) o negativo (-1) de la expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-280">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>|
| <span data-ttu-id="f4f3e-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-281">SQRT(x)</span></span> | <span data-ttu-id="f4f3e-282">Devuelve el cuadrado del valor numérico especificado.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-282">Returns the square of the specified numeric value.</span></span> |

<span data-ttu-id="f4f3e-283">En condiciones de rutas, se admiten las funciones de conversión y comprobación de tipos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-283">In routes conditions, the following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="f4f3e-284">Función</span><span class="sxs-lookup"><span data-stu-id="f4f3e-284">Function</span></span> | <span data-ttu-id="f4f3e-285">Descripción</span><span class="sxs-lookup"><span data-stu-id="f4f3e-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="f4f3e-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="f4f3e-286">AS_NUMBER</span></span> | <span data-ttu-id="f4f3e-287">Convierte la cadena de entrada en un número.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-287">Converts the input string to a number.</span></span> <span data-ttu-id="f4f3e-288">`noop` si la entrada es un número; `Undefined` si la cadena no representa un número.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="f4f3e-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="f4f3e-289">IS_ARRAY</span></span> | <span data-ttu-id="f4f3e-290">Devuelve un valor booleano que indica si el tipo de la expresión especificada es una matriz.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-290">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span> |
| <span data-ttu-id="f4f3e-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="f4f3e-291">IS_BOOL</span></span> | <span data-ttu-id="f4f3e-292">Devuelve un valor booleano que indica si el tipo de la expresión especificada es un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-292">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span> |
| <span data-ttu-id="f4f3e-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="f4f3e-293">IS_DEFINED</span></span> | <span data-ttu-id="f4f3e-294">Devuelve un valor booleano que indica si se ha asignado un valor a la propiedad.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-294">Returns a Boolean indicating if the property has been assigned a value.</span></span> |
| <span data-ttu-id="f4f3e-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="f4f3e-295">IS_NULL</span></span> | <span data-ttu-id="f4f3e-296">Devuelve un valor booleano que indica si el tipo de la expresión especificada es nulo.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-296">Returns a Boolean value indicating if the type of the specified expression is null.</span></span> |
| <span data-ttu-id="f4f3e-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="f4f3e-297">IS_NUMBER</span></span> | <span data-ttu-id="f4f3e-298">Devuelve un valor booleano que indica si el tipo de la expresión especificada es un número.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-298">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span> |
| <span data-ttu-id="f4f3e-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="f4f3e-299">IS_OBJECT</span></span> | <span data-ttu-id="f4f3e-300">Devuelve un valor booleano que indica si el tipo de la expresión especificada es un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-300">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span> |
| <span data-ttu-id="f4f3e-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="f4f3e-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="f4f3e-302">Devuelve un valor booleano que indica si el tipo de la expresión especificada es un tipo primitivo (cadena, booleano, numérico o `null`).</span><span class="sxs-lookup"><span data-stu-id="f4f3e-302">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="f4f3e-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="f4f3e-303">IS_STRING</span></span> | <span data-ttu-id="f4f3e-304">Devuelve un valor booleano que indica si el tipo de la expresión especificada es una cadena.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-304">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span> |

<span data-ttu-id="f4f3e-305">En condiciones de rutas, se admiten las siguientes funciones de cadena:</span><span class="sxs-lookup"><span data-stu-id="f4f3e-305">In routes conditions, the following string functions are supported:</span></span>

| <span data-ttu-id="f4f3e-306">Función</span><span class="sxs-lookup"><span data-stu-id="f4f3e-306">Function</span></span> | <span data-ttu-id="f4f3e-307">Descripción</span><span class="sxs-lookup"><span data-stu-id="f4f3e-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="f4f3e-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-308">CONCAT(x, …)</span></span> | <span data-ttu-id="f4f3e-309">Devuelve una cadena que es el resultado de concatenar dos o más valores de cadena.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-309">Returns a string that is the result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="f4f3e-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-310">LENGTH(x)</span></span> | <span data-ttu-id="f4f3e-311">Devuelve el número de caracteres de la expresión de cadena especificada.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-311">Returns the number of characters of the specified string expression.</span></span>|
| <span data-ttu-id="f4f3e-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-312">LOWER(x)</span></span> | <span data-ttu-id="f4f3e-313">Devuelve una expresión de cadena después de convertir los datos de caracteres en mayúsculas a minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-313">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| <span data-ttu-id="f4f3e-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-314">UPPER(x)</span></span> | <span data-ttu-id="f4f3e-315">Devuelve una expresión de cadena después de convertir datos de caracteres en minúsculas a mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-315">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| <span data-ttu-id="f4f3e-316">SUBSTRING(string, start [, length])</span><span class="sxs-lookup"><span data-stu-id="f4f3e-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="f4f3e-317">Devuelve parte de una expresión de cadena a partir de la posición de base cero del carácter especificado y continúa hasta la longitud especificada, o hasta el final de la cadena.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-317">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span> |
| <span data-ttu-id="f4f3e-318">INDEX_OF(string, fragment)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="f4f3e-319">Devuelve la posición inicial de la primera aparición de la expresión de la segunda cadena dentro de la primera expresión de cadena especificada, o -1 si no se encuentra la cadena.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-319">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>|
| <span data-ttu-id="f4f3e-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="f4f3e-321">Devuelve un valor booleano que indica si la primera expresión de cadena empieza con la segunda.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-321">Returns a Boolean indicating whether the first string expression starts with the second.</span></span> |
| <span data-ttu-id="f4f3e-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="f4f3e-323">Devuelve un valor booleano que indica si la primera expresión de cadena finaliza con la segunda.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-323">Returns a Boolean indicating whether the first string expression ends with the second.</span></span> |
| <span data-ttu-id="f4f3e-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="f4f3e-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="f4f3e-325">Devuelve un valor booleano que indica si la primera expresión de cadena contiene la segunda.</span><span class="sxs-lookup"><span data-stu-id="f4f3e-325">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f4f3e-326">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4f3e-326">Next steps</span></span>
<span data-ttu-id="f4f3e-327">Aprenda a ejecutar consultas en sus aplicaciones mediante los [SDK IoT de Azure ][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="f4f3e-327">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
