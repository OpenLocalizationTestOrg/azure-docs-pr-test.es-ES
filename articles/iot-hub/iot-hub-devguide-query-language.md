---
title: Hola aaaUnderstand lenguaje de consultas del centro de IoT de Azure | Documentos de Microsoft
description: "Guía del desarrollador - descripción del lenguaje de consulta similar a SQL centro de IoT hello usa tooretrieve saber: los gemelos de dispositivo y los trabajos desde el centro de IoT."
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
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="3cb83-103">Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos, trabajos y enrutamiento de mensajes</span><span class="sxs-lookup"><span data-stu-id="3cb83-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="3cb83-104">Centro de IoT proporciona una información de tooretrieve eficaz lenguaje similar a SQL con respecto a [: los gemelos de dispositivo] [ lnk-twins] y [trabajos][lnk-jobs]y [enrutamiento de mensajes][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="3cb83-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="3cb83-105">Este artículo presenta:</span><span class="sxs-lookup"><span data-stu-id="3cb83-105">This article presents:</span></span>

* <span data-ttu-id="3cb83-106">Una introducción toohello principales las funciones de lenguaje de consultas del centro de IoT, hello y</span><span class="sxs-lookup"><span data-stu-id="3cb83-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="3cb83-107">Hola descripción detallada del lenguaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="3cb83-108">Introducción a las consultas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="3cb83-108">Get started with device twin queries</span></span>
<span data-ttu-id="3cb83-109">Los [dispositivos gemelos][lnk-twins] pueden contener objetos JSON arbitrarios como etiquetas y propiedades.</span><span class="sxs-lookup"><span data-stu-id="3cb83-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="3cb83-110">Centro de IoT permite: los gemelos de tooquery dispositivo como un solo documento JSON que contiene toda la información de dispositivo gemelas.</span><span class="sxs-lookup"><span data-stu-id="3cb83-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="3cb83-111">Da por supuesto, por ejemplo, que su: los gemelos de IoT hub dispositivo Hola siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="3cb83-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

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

<span data-ttu-id="3cb83-112">Centro de IoT expone: los gemelos de hello dispositivo como una colección de documentos denominada **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="3cb83-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="3cb83-113">Por lo que Hola después de consulta recupera el conjunto completo de Hola de: los gemelos de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="3cb83-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="3cb83-114">Los [SDK IoT de Azure][lnk-hub-sdks] admiten la paginación de resultados de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="3cb83-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="3cb83-115">Centro de IoT le permite filtrar con condiciones arbitrarias de: los gemelos de tooretrieve dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3cb83-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="3cb83-116">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="3cb83-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="3cb83-117">Recupera Hola: los gemelos de dispositivo con hello **location.region** etiqueta establecido demasiado**US**.</span><span class="sxs-lookup"><span data-stu-id="3cb83-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="3cb83-118">También se admiten operadores booleanos y comparaciones aritméticas, por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="3cb83-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="3cb83-119">Recupera todos los gemelos de dispositivo ubicados en hello nos configurado toosend telemetría menor frecuencia que cada minuto.</span><span class="sxs-lookup"><span data-stu-id="3cb83-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="3cb83-120">Para su comodidad, también es posible toouse constantes de matriz con hello **IN** y **NEN** operadores (no en).</span><span class="sxs-lookup"><span data-stu-id="3cb83-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="3cb83-121">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="3cb83-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="3cb83-122">recupera todos los dispositivos gemelos que notificaron conectividad WiFi o con cable.</span><span class="sxs-lookup"><span data-stu-id="3cb83-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="3cb83-123">Es a menudo necesario tooidentify todos los gemelos de dispositivo que contienen una propiedad concreta.</span><span class="sxs-lookup"><span data-stu-id="3cb83-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="3cb83-124">Centro de IoT es compatible con la función de hello `is_defined()` para este propósito.</span><span class="sxs-lookup"><span data-stu-id="3cb83-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="3cb83-125">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="3cb83-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="3cb83-126">recuperar todos los gemelos de dispositivo que definen hello `connectivity` informa de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="3cb83-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="3cb83-127">Consulte toohello [cláusula WHERE] [ lnk-query-where] sección de referencia completa de Hola de hello capacidades de filtrado.</span><span class="sxs-lookup"><span data-stu-id="3cb83-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="3cb83-128">También se admiten la agrupación y las agregaciones.</span><span class="sxs-lookup"><span data-stu-id="3cb83-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="3cb83-129">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="3cb83-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="3cb83-130">Devuelve el recuento de Hola de dispositivos de hello en cada estado de la configuración de telemetría.</span><span class="sxs-lookup"><span data-stu-id="3cb83-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="3cb83-131">Hello en el ejemplo anterior se muestra una situación donde tres dispositivos notifican una configuración correcta, dos se sigue aplicando configuración hello y uno informó de un error.</span><span class="sxs-lookup"><span data-stu-id="3cb83-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="3cb83-132">Ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="3cb83-132">C# example</span></span>
<span data-ttu-id="3cb83-133">funcionalidad de consulta de Hola se expone mediante hello [C# SDK del servicio] [ lnk-hub-sdks] en hello **RegistryManager** clase.</span><span class="sxs-lookup"><span data-stu-id="3cb83-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="3cb83-134">Este ejemplo corresponde a una consulta simple:</span><span class="sxs-lookup"><span data-stu-id="3cb83-134">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="3cb83-135">Tenga en cuenta cómo Hola **consulta** se crea una instancia de objeto con un tamaño de página (arriba too1000) y, a continuación, se pueden recuperar varias páginas que realiza la llamada hello **GetNextAsTwinAsync** métodos varias veces.</span><span class="sxs-lookup"><span data-stu-id="3cb83-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="3cb83-136">Tenga en cuenta ese objeto de consulta de hello expone varios **siguiente\***, dependiendo de opción de deserialización Hola requeridos por la consulta de hello, como objetos de trabajo o gemelas del dispositivo, o sin formato toobe JSON que usar cuando se empleen las proyecciones.</span><span class="sxs-lookup"><span data-stu-id="3cb83-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="3cb83-137">Ejemplo de Node.js</span><span class="sxs-lookup"><span data-stu-id="3cb83-137">Node.js example</span></span>
<span data-ttu-id="3cb83-138">funcionalidad de consulta de Hola se expone mediante hello [servicio IoT de Azure SDK para Node.js] [ lnk-hub-sdks] en hello **registro** objeto.</span><span class="sxs-lookup"><span data-stu-id="3cb83-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="3cb83-139">Este ejemplo corresponde a una consulta simple:</span><span class="sxs-lookup"><span data-stu-id="3cb83-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
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

<span data-ttu-id="3cb83-140">Tenga en cuenta cómo Hola **consulta** se crea una instancia de objeto con un tamaño de página (arriba too1000) y, a continuación, se pueden recuperar varias páginas que realiza la llamada hello **nextAsTwin** métodos varias veces.</span><span class="sxs-lookup"><span data-stu-id="3cb83-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="3cb83-141">Tenga en cuenta ese objeto de consulta de hello expone varios **siguiente\***, dependiendo de opción de deserialización Hola requeridos por la consulta de hello, como objetos de trabajo o gemelas del dispositivo, o sin formato toobe JSON que usar cuando se empleen las proyecciones.</span><span class="sxs-lookup"><span data-stu-id="3cb83-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="3cb83-142">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="3cb83-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3cb83-143">Resultados de la consulta pueden tener unos minutos de retraso con valores más recientes de respeto toohello en: los gemelos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3cb83-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="3cb83-144">Si consulta: los gemelos de dispositivos individuales por Id., siempre es preferible toouse Hola recuperar dispositivo gemelas API, que siempre contiene valores más recientes de Hola y tiene el límite superior de límites.</span><span class="sxs-lookup"><span data-stu-id="3cb83-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="3cb83-145">Actualmente, las comparaciones solo se admiten entre tipos primitivos (no objetos), por ejemplo `... WHERE properties.desired.config = properties.reported.config` solo se admite si esas propiedades tienen valores primitivos.</span><span class="sxs-lookup"><span data-stu-id="3cb83-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="3cb83-146">Introducción a las consultas de trabajos</span><span class="sxs-lookup"><span data-stu-id="3cb83-146">Get started with jobs queries</span></span>
<span data-ttu-id="3cb83-147">[Trabajos] [ lnk-jobs] proporcionan una manera tooexecute operaciones en conjuntos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3cb83-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="3cb83-148">Cada gemelas dispositivo contiene información de Hola de trabajos de hello del cual forma parte de una colección denominada **trabajos**.</span><span class="sxs-lookup"><span data-stu-id="3cb83-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="3cb83-149">Lógicamente,</span><span class="sxs-lookup"><span data-stu-id="3cb83-149">Logically,</span></span>

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

<span data-ttu-id="3cb83-150">Actualmente, esta colección es consultable como **devices.jobs** Hola lenguaje de consultas del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="3cb83-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3cb83-151">Actualmente, la propiedad de trabajos de hello nunca se devuelve al consultar a: los gemelos de dispositivo (es decir, las consultas que contiene 'desde dispositivos').</span><span class="sxs-lookup"><span data-stu-id="3cb83-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="3cb83-152">Solo es accesible directamente con las consultas que utilizan `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="3cb83-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="3cb83-153">Por ejemplo, tooget todos los trabajos (pasados y programados) que afectan a un único dispositivo, puede usar Hola después de consulta:</span><span class="sxs-lookup"><span data-stu-id="3cb83-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="3cb83-154">Tenga en cuenta cómo esta consulta proporciona el estado específico del dispositivo de hello (y posiblemente Hola método directo respuesta) de cada trabajo que se devuelve.</span><span class="sxs-lookup"><span data-stu-id="3cb83-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="3cb83-155">También es posible toofilter con condiciones booleanas arbitrarias en todas las propiedades de objeto de hello **devices.jobs** colección.</span><span class="sxs-lookup"><span data-stu-id="3cb83-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="3cb83-156">Por ejemplo, Hola consulta siguiente:</span><span class="sxs-lookup"><span data-stu-id="3cb83-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="3cb83-157">recupera todos los trabajos de actualización de dispositivos gemelos completados para el dispositivo **myDeviceId** que se crearon después de septiembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="3cb83-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="3cb83-158">También es posible tooretrieve resultados de por dispositivo de Hola de un único trabajo.</span><span class="sxs-lookup"><span data-stu-id="3cb83-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="3cb83-159">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="3cb83-159">Limitations</span></span>
<span data-ttu-id="3cb83-160">Actualmente, las consultas en **devices.jobs** no admiten:</span><span class="sxs-lookup"><span data-stu-id="3cb83-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="3cb83-161">proyecciones, por lo tanto, solo `SELECT *` es posible.</span><span class="sxs-lookup"><span data-stu-id="3cb83-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="3cb83-162">Condiciones que hacen referencia a toohello gemelas de dispositivo en las propiedades de toojob de suma (vea la sección anterior de hello).</span><span class="sxs-lookup"><span data-stu-id="3cb83-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="3cb83-163">realizar agregaciones, como count, avg, group by.</span><span class="sxs-lookup"><span data-stu-id="3cb83-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="3cb83-164">Introducción a expresiones de consulta de rutas de mensajes de dispositivo a la nube</span><span class="sxs-lookup"><span data-stu-id="3cb83-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="3cb83-165">Usar [rutas de dispositivo para la nube][lnk-devguide-messaging-routes], puede configurar centro de IoT toodispatch dispositivo a la nube mensajes extremos de toodifferent basados en expresiones evaluadas en mensajes individuales.</span><span class="sxs-lookup"><span data-stu-id="3cb83-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="3cb83-166">ruta de Hello [condición] [ lnk-query-expressions] usa Hola mismo lenguaje de consultas del centro de IoT como condiciones en las consultas gemelas y trabajo.</span><span class="sxs-lookup"><span data-stu-id="3cb83-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="3cb83-167">Condiciones de ruta se evalúan en los encabezados de mensaje de Hola y cuerpo.</span><span class="sxs-lookup"><span data-stu-id="3cb83-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="3cb83-168">La expresión de consulta de enrutamiento puede implicar sólo los encabezados de mensaje, sólo cuerpo del mensaje hello, o ambos encabezados de mensaje y cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="3cb83-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="3cb83-169">Centro de IoT se da por supuesto un esquema específico para los encabezados de Hola y el cuerpo del mensaje en mensajes de pedido tooroute y hello las secciones siguientes describe lo que se requiere para la ruta de centro de IoT tooproperly:</span><span class="sxs-lookup"><span data-stu-id="3cb83-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="3cb83-170">Enrutamiento en los encabezados del mensaje</span><span class="sxs-lookup"><span data-stu-id="3cb83-170">Routing on message headers</span></span>

<span data-ttu-id="3cb83-171">Centro de IoT se da por supuesto Hola después de la representación JSON de encabezados de mensaje para enrutar el mensaje:</span><span class="sxs-lookup"><span data-stu-id="3cb83-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

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

<span data-ttu-id="3cb83-172">Propiedades de sistema de mensajes tienen el prefijo hello `'$'` símbolos.</span><span class="sxs-lookup"><span data-stu-id="3cb83-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="3cb83-173">Siempre se accede a las propiedades de usuario con su nombre.</span><span class="sxs-lookup"><span data-stu-id="3cb83-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="3cb83-174">Si un nombre de propiedad de usuario produce toocoincide con una propiedad del sistema (como `$to`), se recuperará la propiedad de usuario de hello con hello `$to` expresión.</span><span class="sxs-lookup"><span data-stu-id="3cb83-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="3cb83-175">Siempre puede tener acceso a propiedad de sistema de hello mediante corchetes `{}`: por ejemplo, puede utilizar la expresión de hello `{$to}` tooaccess Hola propiedad del sistema `to`.</span><span class="sxs-lookup"><span data-stu-id="3cb83-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="3cb83-176">Nombres de propiedad entre corchetes siempre recuperan la propiedad del sistema correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="3cb83-177">Recuerde que los nombres de propiedad no distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3cb83-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="3cb83-178">Todas las propiedades de mensaje son cadenas.</span><span class="sxs-lookup"><span data-stu-id="3cb83-178">All message properties are strings.</span></span> <span data-ttu-id="3cb83-179">Propiedades del sistema, como se describe en hello [Guía del desarrollador][lnk-devguide-messaging-format], no están actualmente disponible toouse en las consultas.</span><span class="sxs-lookup"><span data-stu-id="3cb83-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="3cb83-180">Por ejemplo, si utiliza un `messageType` propiedad, puede que desee tooroute todos los extremos de tooone de telemetría y el punto de conexión de todas las alertas tooanother.</span><span class="sxs-lookup"><span data-stu-id="3cb83-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="3cb83-181">Puede escribir Hola después de telemetría de hello tooroute de expresión:</span><span class="sxs-lookup"><span data-stu-id="3cb83-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="3cb83-182">Y Hola siguiendo los mensajes de alerta Hola expresión tooroute:</span><span class="sxs-lookup"><span data-stu-id="3cb83-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="3cb83-183">También se admiten las funciones y expresiones booleanas.</span><span class="sxs-lookup"><span data-stu-id="3cb83-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="3cb83-184">Esta característica permite toodistinguish entre el nivel de gravedad, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3cb83-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="3cb83-185">Consulte toohello [expresiones y condiciones] [ lnk-query-expressions] sección de la lista completa de Hola de funciones y operadores compatibles.</span><span class="sxs-lookup"><span data-stu-id="3cb83-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="3cb83-186">Enrutamiento en los cuerpos del mensaje</span><span class="sxs-lookup"><span data-stu-id="3cb83-186">Routing on message bodies</span></span>

<span data-ttu-id="3cb83-187">Centro de IoT solamente puede enrutar basado en el cuerpo del mensaje contenido si el cuerpo del mensaje Hola esté correctamente formado JSON codificado en UTF-8, UTF-16 o UTF-32.</span><span class="sxs-lookup"><span data-stu-id="3cb83-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="3cb83-188">Debe establecer el tipo de contenido de Hola de mensaje de saludo demasiado`application/json` y Hola contenido tooone de codificación de hello admite las codificaciones UTF en tooallow de encabezados de mensaje de Hola mensajes de bienvenida del centro de IoT tooroute según el contenido del cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="3cb83-189">Si no se especifica cualquiera de los encabezados de hello, centro de IoT no intentará tooevaluate cualquier expresión de consulta que contenga cuerpo hello en el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="3cb83-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="3cb83-190">Si el mensaje no es un mensaje JSON, o si no especifica mensajes de bienvenida del tipo de contenido de Hola y codificación de contenido, puede seguir utilizando tooroute mensaje de saludo en función de los encabezados de mensaje de Hola el enrutamiento de mensajes.</span><span class="sxs-lookup"><span data-stu-id="3cb83-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="3cb83-191">Puede usar `$body` en el mensaje de saludo de tooroute de expresión de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="3cb83-192">Puede usar una referencia de cuerpo simple, referencia de la matriz de cuerpo o varias referencias de cuerpo en la expresión de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="3cb83-193">La expresión de consulta también puede combinar una referencia al cuerpo con una referencia al encabezado del mensaje.</span><span class="sxs-lookup"><span data-stu-id="3cb83-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="3cb83-194">Por ejemplo, la siguiente Hola es todas las expresiones de consulta válida:</span><span class="sxs-lookup"><span data-stu-id="3cb83-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="3cb83-195">Conceptos básicos de una consulta de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3cb83-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="3cb83-196">Cada consulta de IoT Hub consta de cláusulas SELECT y FROM, y de cláusulas WHERE y GROUP BY opcionales.</span><span class="sxs-lookup"><span data-stu-id="3cb83-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="3cb83-197">Cada consulta se ejecuta en una colección de documentos JSON, por ejemplo, dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="3cb83-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="3cb83-198">cláusula FROM de Hello indica Hola documento colección toobe recorren en iteración en (**dispositivos** o **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="3cb83-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="3cb83-199">A continuación, Hola filtro Hola donde se aplica la cláusula.</span><span class="sxs-lookup"><span data-stu-id="3cb83-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="3cb83-200">Con agregaciones, se agrupan los resultados de Hola de este paso como se especifica en Hola de cláusula GROUP BY y, para cada grupo, se genera una fila según se haya especificado en la cláusula SELECT Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="3cb83-201">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="3cb83-201">FROM clause</span></span>
<span data-ttu-id="3cb83-202">Hola **de < from_specification >** cláusula puede asumir solo dos valores: **desde dispositivos**, tooquery: los gemelos de dispositivo, o **de devices.jobs**, trabajo tooquery por dispositivo detalles.</span><span class="sxs-lookup"><span data-stu-id="3cb83-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="3cb83-203">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="3cb83-203">WHERE clause</span></span>
<span data-ttu-id="3cb83-204">Hola **donde < filter_condition >** cláusula es opcional.</span><span class="sxs-lookup"><span data-stu-id="3cb83-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="3cb83-205">Especifica una o varias condiciones que deben satisfacer los documentos JSON de hello en la colección de hello FROM toobe incluido como parte del resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="3cb83-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="3cb83-206">Se debe evaluar cualquier documento JSON Hola especifica condiciones demasiado "true" toobe incluida en el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="3cb83-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="3cb83-207">Hola permite condiciones se describen en la sección [expresiones y condiciones][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="3cb83-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="3cb83-208">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="3cb83-208">SELECT clause</span></span>
<span data-ttu-id="3cb83-209">cláusula SELECT Hello (**seleccione < select_list >**) es obligatorio y especifica qué valores se recuperan de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="3cb83-210">Especifica Hola JSON valores toobe utiliza toogenerate nuevos objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="3cb83-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="3cb83-211">Para cada elemento de Hola subconjunto filtrado (y, opcionalmente, agrupado) del conjunto de FROM de hello, fase de proyección de hello genera un nuevo objeto JSON, construido con valores de hello especificados en la cláusula SELECT Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="3cb83-212">Aquí te mostramos gramática Hola de cláusula SELECT hello:</span><span class="sxs-lookup"><span data-stu-id="3cb83-212">Following is hello grammar of hello SELECT clause:</span></span>

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

<span data-ttu-id="3cb83-213">donde **attribute_name** hace referencia la propiedad tooany del documento JSON de hello en la colección de hello FROM.</span><span class="sxs-lookup"><span data-stu-id="3cb83-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="3cb83-214">Algunos ejemplos de las cláusulas SELECT pueden encontrarse en hello [Introducción a las consultas de dispositivo gemelas] [ lnk-query-getstarted] sección.</span><span class="sxs-lookup"><span data-stu-id="3cb83-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="3cb83-215">Actualmente, las cláusulas de selección distintas a **SELECT \*** solo se admiten en las consultas agregadas de dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="3cb83-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="3cb83-216">Cláusula GROUP BY</span><span class="sxs-lookup"><span data-stu-id="3cb83-216">GROUP BY clause</span></span>
<span data-ttu-id="3cb83-217">Hola **GROUP BY < group_specification >** cláusula es un paso opcional que se puede ejecutar después de filtro de hello especificado Hola de cláusula WHERE y antes de la proyección de hello especificada en hello seleccione.</span><span class="sxs-lookup"><span data-stu-id="3cb83-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="3cb83-218">Agrupa documentos basados en el valor de Hola de un atributo.</span><span class="sxs-lookup"><span data-stu-id="3cb83-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="3cb83-219">Estos grupos son utilizados toogenerate agregado valores tal como se especifica en la cláusula SELECT Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="3cb83-220">Un ejemplo de consulta con GROUP BY es:</span><span class="sxs-lookup"><span data-stu-id="3cb83-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="3cb83-221">sintaxis formal de Hola de GROUP BY es:</span><span class="sxs-lookup"><span data-stu-id="3cb83-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="3cb83-222">donde **attribute_name** hace referencia la propiedad tooany del documento JSON de hello en la colección de hello FROM.</span><span class="sxs-lookup"><span data-stu-id="3cb83-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="3cb83-223">Actualmente, solo se admite la cláusula GROUP BY Hola al consultar a: los gemelos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3cb83-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="3cb83-224">Expresiones y condiciones</span><span class="sxs-lookup"><span data-stu-id="3cb83-224">Expressions and conditions</span></span>
<span data-ttu-id="3cb83-225">Brevemente, una *expresión*:</span><span class="sxs-lookup"><span data-stu-id="3cb83-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="3cb83-226">Se evalúa como instancia de tooan de un tipo JSON (por ejemplo, un valor booleano, número, cadena, matriz u objeto), y</span><span class="sxs-lookup"><span data-stu-id="3cb83-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="3cb83-227">Se define mediante la manipulación de datos procedentes de documento JSON de dispositivo de Hola y constantes que se utilizan funciones y operadores integrados.</span><span class="sxs-lookup"><span data-stu-id="3cb83-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="3cb83-228">*Condiciones* son expresiones que se evalúan tooa un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="3cb83-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="3cb83-229">Cualquier constante diferente a un valor booleano **true** se considera como **false** (incluidos **null**, **indefinido**, cualquier instancia de objeto o matriz, cualquier cadena, claramente hello y un valor booleano **false**).</span><span class="sxs-lookup"><span data-stu-id="3cb83-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="3cb83-230">sintaxis de Hola de expresiones es:</span><span class="sxs-lookup"><span data-stu-id="3cb83-230">hello syntax for expressions is:</span></span>

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

<span data-ttu-id="3cb83-231">donde:</span><span class="sxs-lookup"><span data-stu-id="3cb83-231">where:</span></span>

| <span data-ttu-id="3cb83-232">Símbolo</span><span class="sxs-lookup"><span data-stu-id="3cb83-232">Symbol</span></span> | <span data-ttu-id="3cb83-233">Definición</span><span class="sxs-lookup"><span data-stu-id="3cb83-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="3cb83-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="3cb83-234">attribute_name</span></span> | <span data-ttu-id="3cb83-235">Cualquier propiedad de documento JSON de Hola Hola **FROM** colección.</span><span class="sxs-lookup"><span data-stu-id="3cb83-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="3cb83-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="3cb83-236">binary_operator</span></span> | <span data-ttu-id="3cb83-237">Cualquier operador binario enumerados en hello [operadores](#operators) sección.</span><span class="sxs-lookup"><span data-stu-id="3cb83-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="3cb83-238">function_name</span><span class="sxs-lookup"><span data-stu-id="3cb83-238">function_name</span></span>| <span data-ttu-id="3cb83-239">Cualquier función que se muestra en hello [funciones](#functions) sección.</span><span class="sxs-lookup"><span data-stu-id="3cb83-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="3cb83-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="3cb83-240">decimal_literal</span></span> |<span data-ttu-id="3cb83-241">Un valor float expresado en notación decimal.</span><span class="sxs-lookup"><span data-stu-id="3cb83-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="3cb83-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="3cb83-242">hexadecimal_literal</span></span> |<span data-ttu-id="3cb83-243">Un número expresado por cadena hello '0 x' seguido por una cadena de dígitos hexadecimales.</span><span class="sxs-lookup"><span data-stu-id="3cb83-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="3cb83-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="3cb83-244">string_literal</span></span> |<span data-ttu-id="3cb83-245">Los literales de cadena son cadenas Unicode representadas por una secuencia de cero o varios caracteres Unicode o secuencias de escape.</span><span class="sxs-lookup"><span data-stu-id="3cb83-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="3cb83-246">Los literales de cadena se encierran entre comillas simples (apóstrofo: ') o comillas dobles (comillas: ").</span><span class="sxs-lookup"><span data-stu-id="3cb83-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="3cb83-247">Caracteres de escape permitidos: `\'`, `\"`, `\\`, `\uXXXX` para los caracteres Unicode definidos con 4 dígitos hexadecimales.</span><span class="sxs-lookup"><span data-stu-id="3cb83-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="3cb83-248">Operadores</span><span class="sxs-lookup"><span data-stu-id="3cb83-248">Operators</span></span>
<span data-ttu-id="3cb83-249">se admite Hola siguientes operadores:</span><span class="sxs-lookup"><span data-stu-id="3cb83-249">hello following operators are supported:</span></span>

| <span data-ttu-id="3cb83-250">Familia</span><span class="sxs-lookup"><span data-stu-id="3cb83-250">Family</span></span> | <span data-ttu-id="3cb83-251">Operadores</span><span class="sxs-lookup"><span data-stu-id="3cb83-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="3cb83-252">Aritméticos</span><span class="sxs-lookup"><span data-stu-id="3cb83-252">Arithmetic</span></span> |<span data-ttu-id="3cb83-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="3cb83-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="3cb83-254">Lógicos</span><span class="sxs-lookup"><span data-stu-id="3cb83-254">Logical</span></span> |<span data-ttu-id="3cb83-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="3cb83-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="3cb83-256">De comparación</span><span class="sxs-lookup"><span data-stu-id="3cb83-256">Comparison</span></span> |<span data-ttu-id="3cb83-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="3cb83-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="3cb83-258">Functions</span><span class="sxs-lookup"><span data-stu-id="3cb83-258">Functions</span></span>
<span data-ttu-id="3cb83-259">Cuando se consultan hello: los gemelos y los trabajos solo admitido la función es:</span><span class="sxs-lookup"><span data-stu-id="3cb83-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="3cb83-260">Función</span><span class="sxs-lookup"><span data-stu-id="3cb83-260">Function</span></span> | <span data-ttu-id="3cb83-261">Descripción</span><span class="sxs-lookup"><span data-stu-id="3cb83-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="3cb83-262">IS_DEFINED(property)</span><span class="sxs-lookup"><span data-stu-id="3cb83-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="3cb83-263">Devuelve un valor booleano que indica si la propiedad de Hola se ha asignado un valor (incluido `null`).</span><span class="sxs-lookup"><span data-stu-id="3cb83-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="3cb83-264">En condiciones de rutas, se admite Hola siguientes funciones matemáticas:</span><span class="sxs-lookup"><span data-stu-id="3cb83-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="3cb83-265">Función</span><span class="sxs-lookup"><span data-stu-id="3cb83-265">Function</span></span> | <span data-ttu-id="3cb83-266">Descripción</span><span class="sxs-lookup"><span data-stu-id="3cb83-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="3cb83-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="3cb83-267">ABS(x)</span></span> | <span data-ttu-id="3cb83-268">Devuelve Hola valor absoluto (positivo) de hello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="3cb83-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="3cb83-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="3cb83-269">EXP(x)</span></span> | <span data-ttu-id="3cb83-270">Devuelve Hola valor exponencial de hello especifica la expresión numérica (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="3cb83-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="3cb83-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="3cb83-271">POWER(x,y)</span></span> | <span data-ttu-id="3cb83-272">Devuelve Hola valo Hola especificado expresión toohello potencia especificada (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="3cb83-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="3cb83-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="3cb83-273">SQUARE(x)</span></span> | <span data-ttu-id="3cb83-274">Hola devuelve cuadrado de hello especifica el valor numérico.</span><span class="sxs-lookup"><span data-stu-id="3cb83-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="3cb83-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="3cb83-275">CEILING(x)</span></span> | <span data-ttu-id="3cb83-276">Devuelve Hola valor entero más pequeño mayor o igual a, Hola expresión numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="3cb83-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="3cb83-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="3cb83-277">FLOOR(x)</span></span> | <span data-ttu-id="3cb83-278">Devuelve Hola mayor entero menor o igual toohello especifica la expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="3cb83-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="3cb83-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="3cb83-279">SIGN(x)</span></span> | <span data-ttu-id="3cb83-280">Devuelve Hola positivo (+ 1), cero (0), o signo negativo (-1) de hello especificado expresión numérica.</span><span class="sxs-lookup"><span data-stu-id="3cb83-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="3cb83-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="3cb83-281">SQRT(x)</span></span> | <span data-ttu-id="3cb83-282">Hola devuelve cuadrado de hello especifica el valor numérico.</span><span class="sxs-lookup"><span data-stu-id="3cb83-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="3cb83-283">En condiciones de rutas, se admite Hola después el tipo de comprobación y las funciones de conversión:</span><span class="sxs-lookup"><span data-stu-id="3cb83-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="3cb83-284">Función</span><span class="sxs-lookup"><span data-stu-id="3cb83-284">Function</span></span> | <span data-ttu-id="3cb83-285">Descripción</span><span class="sxs-lookup"><span data-stu-id="3cb83-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="3cb83-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="3cb83-286">AS_NUMBER</span></span> | <span data-ttu-id="3cb83-287">Convierte el número de tooa de cadena de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="3cb83-288">`noop` si la entrada es un número; `Undefined` si la cadena no representa un número.</span><span class="sxs-lookup"><span data-stu-id="3cb83-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="3cb83-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="3cb83-289">IS_ARRAY</span></span> | <span data-ttu-id="3cb83-290">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es una matriz.</span><span class="sxs-lookup"><span data-stu-id="3cb83-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="3cb83-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="3cb83-291">IS_BOOL</span></span> | <span data-ttu-id="3cb83-292">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="3cb83-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="3cb83-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="3cb83-293">IS_DEFINED</span></span> | <span data-ttu-id="3cb83-294">Devuelve un valor booleano que indica si la propiedad de Hola se ha asignado un valor.</span><span class="sxs-lookup"><span data-stu-id="3cb83-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="3cb83-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="3cb83-295">IS_NULL</span></span> | <span data-ttu-id="3cb83-296">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es null.</span><span class="sxs-lookup"><span data-stu-id="3cb83-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="3cb83-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="3cb83-297">IS_NUMBER</span></span> | <span data-ttu-id="3cb83-298">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un número.</span><span class="sxs-lookup"><span data-stu-id="3cb83-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="3cb83-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="3cb83-299">IS_OBJECT</span></span> | <span data-ttu-id="3cb83-300">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="3cb83-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="3cb83-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="3cb83-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="3cb83-302">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es un tipo primitivo (cadena, booleano, numérico o `null`).</span><span class="sxs-lookup"><span data-stu-id="3cb83-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="3cb83-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="3cb83-303">IS_STRING</span></span> | <span data-ttu-id="3cb83-304">Devuelve un valor booleano que indica si el tipo de saludo de hello especifica expresión es una cadena.</span><span class="sxs-lookup"><span data-stu-id="3cb83-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="3cb83-305">En condiciones de rutas, se admite Hola siguiendo las funciones de cadena:</span><span class="sxs-lookup"><span data-stu-id="3cb83-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="3cb83-306">Función</span><span class="sxs-lookup"><span data-stu-id="3cb83-306">Function</span></span> | <span data-ttu-id="3cb83-307">Descripción</span><span class="sxs-lookup"><span data-stu-id="3cb83-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="3cb83-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="3cb83-308">CONCAT(x, …)</span></span> | <span data-ttu-id="3cb83-309">Devuelve una cadena que es el resultado de hello de concatenar dos o más valores de cadena.</span><span class="sxs-lookup"><span data-stu-id="3cb83-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="3cb83-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="3cb83-310">LENGTH(x)</span></span> | <span data-ttu-id="3cb83-311">Devuelve el número de caracteres de Hola Hola especificado expresión de cadena.</span><span class="sxs-lookup"><span data-stu-id="3cb83-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="3cb83-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="3cb83-312">LOWER(x)</span></span> | <span data-ttu-id="3cb83-313">Devuelve una expresión de cadena después de convertir toolowercase de datos de caracteres en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="3cb83-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="3cb83-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="3cb83-314">UPPER(x)</span></span> | <span data-ttu-id="3cb83-315">Devuelve una expresión de cadena después de convertir toouppercase de datos de carácter en minúscula.</span><span class="sxs-lookup"><span data-stu-id="3cb83-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="3cb83-316">SUBSTRING(string, start [, length])</span><span class="sxs-lookup"><span data-stu-id="3cb83-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="3cb83-317">Devuelve parte de una expresión de cadena a partir de hello especifica la posición de base cero del carácter y continúa toohello especifica la longitud o toohello final de cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="3cb83-318">INDEX_OF(string, fragment)</span><span class="sxs-lookup"><span data-stu-id="3cb83-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="3cb83-319">Devuelve Hola a partir de la posición de la primera aparición de hello de la segunda expresión de cadena Hola dentro de la primera expresión de cadena especificada de hello, o -1 si no se encuentra la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cb83-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="3cb83-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="3cb83-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="3cb83-321">Devuelve un valor booleano que indica si primera expresión de cadena Hola empieza por hello en segundo lugar.</span><span class="sxs-lookup"><span data-stu-id="3cb83-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="3cb83-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="3cb83-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="3cb83-323">Devuelve un valor booleano que indica si primera expresión de cadena Hola termina con hello en segundo lugar.</span><span class="sxs-lookup"><span data-stu-id="3cb83-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="3cb83-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="3cb83-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="3cb83-325">Devuelve un valor booleano que indica si primera expresión de cadena hello contiene hello en segundo lugar.</span><span class="sxs-lookup"><span data-stu-id="3cb83-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3cb83-326">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3cb83-326">Next steps</span></span>
<span data-ttu-id="3cb83-327">Obtenga información acerca de cómo tooexecute las consultas en sus aplicaciones usando [SDK de Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="3cb83-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

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
