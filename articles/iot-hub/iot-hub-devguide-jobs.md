---
title: Conceptos de trabajos de IoT Hub de Azure | Microsoft Docs
description: "Guía de desarrollador: programación de trabajos para su ejecución en varios dispositivos conectados al centro de IoT Hub. Trabajos pueden actualizar las etiquetas y propiedades que desee y llamar a métodos directas en varios dispositivos."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="4b183-104">Programación de trabajos en varios dispositivos</span><span class="sxs-lookup"><span data-stu-id="4b183-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="4b183-105">Información general</span><span class="sxs-lookup"><span data-stu-id="4b183-105">Overview</span></span>
<span data-ttu-id="4b183-106">Como se describe en artículos anteriores, Azure IoT Hub permite un número de bloques de creación ([etiquetas y propiedades de dispositivos gemelos][lnk-twin-devguide] y [métodos directos][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="4b183-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="4b183-107">Normalmente, las aplicaciones de back-end permiten a los administradores y operadores de dispositivos actualizar e interactuar con dispositivos de IoT de forma masiva y a la hora programada.</span><span class="sxs-lookup"><span data-stu-id="4b183-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="4b183-108">Los trabajos encapsulan la ejecución de actualizaciones del dispositivo gemelo y métodos directos con un conjunto de dispositivos a la hora programada.</span><span class="sxs-lookup"><span data-stu-id="4b183-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="4b183-109">Por ejemplo, un operador usaría una aplicación de back-end que se iniciaría y realizaría un seguimiento de un trabajo para reiniciar un conjunto de dispositivos en la creación del piso 43 y 3 en un momento en que no sería problemático para las operaciones del edificio.</span><span class="sxs-lookup"><span data-stu-id="4b183-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="4b183-110">Cuándo se deben usar</span><span class="sxs-lookup"><span data-stu-id="4b183-110">When to use</span></span>
<span data-ttu-id="4b183-111">Considere la posibilidad de usar trabajos cuando: solución back end necesite programar y realizar un seguimiento del progreso de cualquiera de las siguientes actividades en un conjunto de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="4b183-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="4b183-112">Actualizar las propiedades deseadas</span><span class="sxs-lookup"><span data-stu-id="4b183-112">Update desired properties</span></span>
* <span data-ttu-id="4b183-113">Actualizar etiquetas</span><span class="sxs-lookup"><span data-stu-id="4b183-113">Update tags</span></span>
* <span data-ttu-id="4b183-114">Invocar métodos directos</span><span class="sxs-lookup"><span data-stu-id="4b183-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="4b183-115">Ciclo de vida de trabajo</span><span class="sxs-lookup"><span data-stu-id="4b183-115">Job lifecycle</span></span>
<span data-ttu-id="4b183-116">Los trabajos se inician mediante el back-end de solución y se mantienen mediante IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4b183-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="4b183-117">Puede iniciar un trabajo a través de un URI orientado a servicios (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) y una consulta para el progreso de un trabajo en ejecución a través de un URI orientado a servicios (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="4b183-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="4b183-118">Una vez que se inicia un trabajo, la consulta de trabajos permitirá a la aplicación back-end actualizar el estado de trabajos en ejecución.</span><span class="sxs-lookup"><span data-stu-id="4b183-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="4b183-119">Cuando se inicia un trabajo, los valores y los nombres de propiedad solo pueden contener caracteres alfanuméricos US-ASCII imprimibles, excepto los del siguiente conjunto: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="4b183-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="4b183-120">Temas de referencia:</span><span class="sxs-lookup"><span data-stu-id="4b183-120">Reference topics:</span></span>
<span data-ttu-id="4b183-121">Los siguientes temas de referencia proporcionan más información sobre el uso de trabajos.</span><span class="sxs-lookup"><span data-stu-id="4b183-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="4b183-122">Trabajos para ejecutar métodos directos</span><span class="sxs-lookup"><span data-stu-id="4b183-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="4b183-123">A continuación se muestran los detalles de la solicitud HTTP 1.1 para ejecutar un [método directo][lnk-dev-methods] en un conjunto de dispositivos mediante un trabajo:</span><span class="sxs-lookup"><span data-stu-id="4b183-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
<span data-ttu-id="4b183-124">La condición de consulta puede estar también en un solo identificador de dispositivo o en una lista de identificadores de dispositivos, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="4b183-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="4b183-125">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="4b183-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="4b183-126">[Lenguaje de consulta de IoT Hub][lnk-query] aborda el lenguaje de consulta de IoT Hub con más detalle.</span><span class="sxs-lookup"><span data-stu-id="4b183-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="4b183-127">Trabajos para actualizar las propiedades del dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="4b183-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="4b183-128">A continuación se muestran los detalles de la solicitud HTTP 1.1 para la actualización de las propiedades del dispositivo gemelo con un trabajo:</span><span class="sxs-lookup"><span data-stu-id="4b183-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="4b183-129">Consulta del progreso de los trabajos</span><span class="sxs-lookup"><span data-stu-id="4b183-129">Querying for progress on jobs</span></span>
<span data-ttu-id="4b183-130">A continuación se muestran los detalles de la solicitud HTTP 1.1 para la [consulta de trabajos][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="4b183-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="4b183-131">Se proporciona el continuationToken de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="4b183-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="4b183-132">Propiedades de trabajos</span><span class="sxs-lookup"><span data-stu-id="4b183-132">Jobs Properties</span></span>
<span data-ttu-id="4b183-133">La siguiente es una lista de propiedades y las descripciones correspondientes, que se pueden utilizar al consultar trabajos o resultados de trabajos.</span><span class="sxs-lookup"><span data-stu-id="4b183-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="4b183-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="4b183-134">Property</span></span> | <span data-ttu-id="4b183-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="4b183-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b183-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="4b183-136">**jobId**</span></span> |<span data-ttu-id="4b183-137">Id. proporcionado de la aplicación para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4b183-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="4b183-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="4b183-138">**startTime**</span></span> |<span data-ttu-id="4b183-139">Hora de inicio proporcionada de la aplicación (ISO 8601) para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4b183-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="4b183-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="4b183-140">**endTime**</span></span> |<span data-ttu-id="4b183-141">Fecha proporcionada de IoT Hub (ISO 8601) cuando hay un trabajo completado.</span><span class="sxs-lookup"><span data-stu-id="4b183-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="4b183-142">Válido solo después de que el trabajo alcance el estado 'completado'.</span><span class="sxs-lookup"><span data-stu-id="4b183-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="4b183-143">**type**</span><span class="sxs-lookup"><span data-stu-id="4b183-143">**type**</span></span> |<span data-ttu-id="4b183-144">Tipos de trabajos:</span><span class="sxs-lookup"><span data-stu-id="4b183-144">Types of jobs:</span></span> |
| <span data-ttu-id="4b183-145">**scheduledUpdateTwin**: un trabajo que se usa para actualizar un conjunto de propiedades deseadas o etiquetas.</span><span class="sxs-lookup"><span data-stu-id="4b183-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="4b183-146">**scheduledDeviceMethod**: un trabajo que se utiliza para invocar un método de dispositivo en un conjunto de dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="4b183-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="4b183-147">**estado**</span><span class="sxs-lookup"><span data-stu-id="4b183-147">**status**</span></span> |<span data-ttu-id="4b183-148">Estado actual del trabajo.</span><span class="sxs-lookup"><span data-stu-id="4b183-148">Current state of the job.</span></span> <span data-ttu-id="4b183-149">Posibles valores para el estado:</span><span class="sxs-lookup"><span data-stu-id="4b183-149">Possible values for status:</span></span> |
| <span data-ttu-id="4b183-150">**pending**: programado y en espera para que lo recopile el servicio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4b183-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="4b183-151">**scheduled**: programado para una hora futura.</span><span class="sxs-lookup"><span data-stu-id="4b183-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="4b183-152">**running**: trabajo activo actualmente.</span><span class="sxs-lookup"><span data-stu-id="4b183-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="4b183-153">**cancelled**: el trabajo se ha cancelado.</span><span class="sxs-lookup"><span data-stu-id="4b183-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="4b183-154">**failed**: trabajo erróneo.</span><span class="sxs-lookup"><span data-stu-id="4b183-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="4b183-155">**completed**: el trabajo se ha completado.</span><span class="sxs-lookup"><span data-stu-id="4b183-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="4b183-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="4b183-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="4b183-157">Estadísticas sobre la ejecución del trabajo.</span><span class="sxs-lookup"><span data-stu-id="4b183-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="4b183-158">Propiedades **deviceJobStatistics**.</span><span class="sxs-lookup"><span data-stu-id="4b183-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="4b183-159">Propiedad</span><span class="sxs-lookup"><span data-stu-id="4b183-159">Property</span></span> | <span data-ttu-id="4b183-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="4b183-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b183-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="4b183-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="4b183-162">Número de dispositivos en el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4b183-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="4b183-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="4b183-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="4b183-164">Número de dispositivos en los que se ha producido un error del trabajo.</span><span class="sxs-lookup"><span data-stu-id="4b183-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="4b183-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="4b183-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="4b183-166">Número de dispositivos en los que se ha realizado correctamente el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4b183-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="4b183-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="4b183-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="4b183-168">Número de dispositivos que ejecutan actualmente el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4b183-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="4b183-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="4b183-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="4b183-170">Número de dispositivos pendientes de ejecutar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="4b183-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="4b183-171">Material de referencia adicional</span><span class="sxs-lookup"><span data-stu-id="4b183-171">Additional reference material</span></span>
<span data-ttu-id="4b183-172">Otros temas de referencia en la guía del desarrollador de IoT Hub son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="4b183-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="4b183-173">En [Puntos de conexión de IoT Hub][lnk-endpoints], se describen los diferentes puntos de conexión que expone cada centro de IoT Hub para las operaciones en tiempo de ejecución y de administración.</span><span class="sxs-lookup"><span data-stu-id="4b183-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="4b183-174">En [Cuotas y limitación][lnk-quotas], se describen las cuotas que se aplican al servicio IoT Hub y el comportamiento de limitación que se espera al usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="4b183-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="4b183-175">En [SDK de dispositivo y servicio IoT de Azure][lnk-sdks], se muestran los diversos SDK de lenguaje que puede usar para desarrollar aplicaciones para dispositivo y de servicio que interactúen con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4b183-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="4b183-176">En [Referencia: Lenguaje de consulta de IoT Hub para dispositivos gemelos, trabajos y enrutamiento de mensajes][lnk-query], se describe el lenguaje de consulta de IoT Hub que se puede usar para recuperar información de IoT Hub sobre los dispositivos gemelos y trabajos.</span><span class="sxs-lookup"><span data-stu-id="4b183-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="4b183-177">En [Compatibilidad con MQTT de IoT Hub][lnk-devguide-mqtt], se proporciona más información sobre la compatibilidad de IoT Hub con el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="4b183-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b183-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4b183-178">Next steps</span></span>
<span data-ttu-id="4b183-179">Si desea probar algunos de los conceptos descritos en este artículo, puede interesarle el siguiente tutorial de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="4b183-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="4b183-180">[Schedule and broadcast jobs][lnk-jobs-tutorial] (Programación y difusión de trabajos)</span><span class="sxs-lookup"><span data-stu-id="4b183-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
