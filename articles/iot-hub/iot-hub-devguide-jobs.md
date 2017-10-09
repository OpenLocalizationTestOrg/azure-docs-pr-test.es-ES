---
title: trabajos de centro de IoT de Azure aaaUnderstand | Documentos de Microsoft
description: "Guía del desarrollador - programar trabajos toorun en varios dispositivos conectados tooyour centro de IoT. Trabajos pueden actualizar las etiquetas y propiedades que desee y llamar a métodos directas en varios dispositivos."
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
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="cdb97-104">Programación de trabajos en varios dispositivos</span><span class="sxs-lookup"><span data-stu-id="cdb97-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="cdb97-105">Información general</span><span class="sxs-lookup"><span data-stu-id="cdb97-105">Overview</span></span>
<span data-ttu-id="cdb97-106">Como se describe en artículos anteriores, Azure IoT Hub permite un número de bloques de creación ([etiquetas y propiedades de dispositivos gemelos][lnk-twin-devguide] y [métodos directos][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="cdb97-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="cdb97-107">Por lo general, aplicaciones de back-end habilitar tooupdate de administradores y operadores de dispositivo e interactúan con dispositivos de IoT de forma masiva y a la hora programada.</span><span class="sxs-lookup"><span data-stu-id="cdb97-107">Typically, back-end apps enable device administrators and operators tooupdate and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="cdb97-108">Trabajos de encapsulan la ejecución de hello de dispositivo gemelas actualizaciones y métodos directos con un conjunto de dispositivos en un tiempo de programación.</span><span class="sxs-lookup"><span data-stu-id="cdb97-108">Jobs encapsulate hello execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="cdb97-109">Por ejemplo, un operador podría usar una aplicación de back-end que se inician y realizar un seguimiento de un tooreboot de trabajo un conjunto de dispositivos en la creación de 43 y floor 3 a la vez que no son perjudiciales toohello operaciones de creación de hello.</span><span class="sxs-lookup"><span data-stu-id="cdb97-109">For example, an operator would use a back-end app that would initiate and track a job tooreboot a set of devices in building 43 and floor 3 at a time that would not be disruptive toohello operations of hello building.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="cdb97-110">Cuando toouse</span><span class="sxs-lookup"><span data-stu-id="cdb97-110">When toouse</span></span>
<span data-ttu-id="cdb97-111">Considere la posibilidad de usar trabajos cuando: una solución back-end necesidades tooschedule y realizar un seguimiento de progreso cualquiera de hello actividades que siguen en un conjunto de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="cdb97-111">Consider using jobs when: a solution back end needs tooschedule and track progress any of hello following activities on a set of device:</span></span>

* <span data-ttu-id="cdb97-112">Actualizar las propiedades deseadas</span><span class="sxs-lookup"><span data-stu-id="cdb97-112">Update desired properties</span></span>
* <span data-ttu-id="cdb97-113">Actualizar etiquetas</span><span class="sxs-lookup"><span data-stu-id="cdb97-113">Update tags</span></span>
* <span data-ttu-id="cdb97-114">Invocar métodos directos</span><span class="sxs-lookup"><span data-stu-id="cdb97-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="cdb97-115">Ciclo de vida de trabajo</span><span class="sxs-lookup"><span data-stu-id="cdb97-115">Job lifecycle</span></span>
<span data-ttu-id="cdb97-116">Los trabajos se inicia back-end de soluciones de Hola y mantenidos por centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cdb97-116">Jobs are initiated by hello solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="cdb97-117">Puede iniciar un trabajo a través de un URI orientado a servicios (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) y una consulta para el progreso de un trabajo en ejecución a través de un URI orientado a servicios (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="cdb97-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="cdb97-118">Una vez que se inicia un trabajo, la consulta de trabajos permite estado de hello aplicaciones back-end toorefresh Hola de trabajos en ejecución.</span><span class="sxs-lookup"><span data-stu-id="cdb97-118">Once a job is initiated, querying for jobs enables hello back-end app toorefresh hello status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="cdb97-119">Cuando se inicia un trabajo, valores y nombres de propiedad solo pueden contener US-ASCII imprimible alfanumérico, excepto los Hola siguiendo conjunto: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="cdb97-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="cdb97-120">Temas de referencia:</span><span class="sxs-lookup"><span data-stu-id="cdb97-120">Reference topics:</span></span>
<span data-ttu-id="cdb97-121">Hola temas de referencia siguientes proporciona más información acerca del uso de trabajos.</span><span class="sxs-lookup"><span data-stu-id="cdb97-121">hello following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-tooexecute-direct-methods"></a><span data-ttu-id="cdb97-122">Métodos directos de trabajos tooexecute</span><span class="sxs-lookup"><span data-stu-id="cdb97-122">Jobs tooexecute direct methods</span></span>
<span data-ttu-id="cdb97-123">Hello aquí te mostramos detalles de la solicitud de hello HTTP 1.1 para ejecutar un [método directo] [ lnk-dev-methods] en un conjunto de dispositivos mediante un trabajo:</span><span class="sxs-lookup"><span data-stu-id="cdb97-123">hello following is hello HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="cdb97-124">condición de consulta de Hello también puede ser un Id. de dispositivo único o en una lista de identificadores de dispositivo tal y como se muestra a continuación</span><span class="sxs-lookup"><span data-stu-id="cdb97-124">hello query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="cdb97-125">**Ejemplos**</span><span class="sxs-lookup"><span data-stu-id="cdb97-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="cdb97-126">[Lenguaje de consulta de IoT Hub][lnk-query] aborda el lenguaje de consulta de IoT Hub con más detalle.</span><span class="sxs-lookup"><span data-stu-id="cdb97-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-tooupdate-device-twin-properties"></a><span data-ttu-id="cdb97-127">Propiedades de gemelas del dispositivo de tooupdate de trabajos</span><span class="sxs-lookup"><span data-stu-id="cdb97-127">Jobs tooupdate device twin properties</span></span>
<span data-ttu-id="cdb97-128">Hola te mostramos detalles de la solicitud de HTTP 1.1 Hola para actualizar las propiedades de dispositivo gemelas con un trabajo:</span><span class="sxs-lookup"><span data-stu-id="cdb97-128">hello following is hello HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="cdb97-129">Consulta del progreso de los trabajos</span><span class="sxs-lookup"><span data-stu-id="cdb97-129">Querying for progress on jobs</span></span>
<span data-ttu-id="cdb97-130">Hello aquí te mostramos Hola detalles de la solicitud de HTTP 1.1 para [consultar trabajos][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="cdb97-130">hello following is hello HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="cdb97-131">Hola continuationToken se proporciona de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-131">hello continuationToken is provided from hello response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="cdb97-132">Propiedades de trabajos</span><span class="sxs-lookup"><span data-stu-id="cdb97-132">Jobs Properties</span></span>
<span data-ttu-id="cdb97-133">Hola mostramos una lista de propiedades y las descripciones correspondientes, que pueden utilizarse al consultar para trabajos o los resultados del trabajo.</span><span class="sxs-lookup"><span data-stu-id="cdb97-133">hello following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="cdb97-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="cdb97-134">Property</span></span> | <span data-ttu-id="cdb97-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="cdb97-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cdb97-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="cdb97-136">**jobId**</span></span> |<span data-ttu-id="cdb97-137">Aplicación Id. proporcionado para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-137">Application provided ID for hello job.</span></span> |
| <span data-ttu-id="cdb97-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="cdb97-138">**startTime**</span></span> |<span data-ttu-id="cdb97-139">Hora de inicio de aplicación proporcionado (ISO-8601) para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-139">Application provided start time (ISO-8601) for hello job.</span></span> |
| <span data-ttu-id="cdb97-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="cdb97-140">**endTime**</span></span> |<span data-ttu-id="cdb97-141">Centro de IoT proporciona fecha (ISO-8601) de terminación del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-141">IoT Hub provided date (ISO-8601) for when hello job completed.</span></span> <span data-ttu-id="cdb97-142">Válido solo una vez trabajo Hola permanece hello 'completada'.</span><span class="sxs-lookup"><span data-stu-id="cdb97-142">Valid only after hello job reaches hello 'completed' state.</span></span> |
| <span data-ttu-id="cdb97-143">**type**</span><span class="sxs-lookup"><span data-stu-id="cdb97-143">**type**</span></span> |<span data-ttu-id="cdb97-144">Tipos de trabajos:</span><span class="sxs-lookup"><span data-stu-id="cdb97-144">Types of jobs:</span></span> |
| <span data-ttu-id="cdb97-145">**scheduledUpdateTwin**: un tooupdate de trabajo que se utiliza un conjunto de propiedades que desee o etiquetas.</span><span class="sxs-lookup"><span data-stu-id="cdb97-145">**scheduledUpdateTwin**: A job used tooupdate a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="cdb97-146">**scheduledDeviceMethod**: un tooinvoke de trabajo que se utiliza un método de dispositivo en un conjunto de: los gemelos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cdb97-146">**scheduledDeviceMethod**: A job used tooinvoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="cdb97-147">**estado**</span><span class="sxs-lookup"><span data-stu-id="cdb97-147">**status**</span></span> |<span data-ttu-id="cdb97-148">Estado actual del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-148">Current state of hello job.</span></span> <span data-ttu-id="cdb97-149">Posibles valores para el estado:</span><span class="sxs-lookup"><span data-stu-id="cdb97-149">Possible values for status:</span></span> |
| <span data-ttu-id="cdb97-150">**pendiente** : programada y espera toobe recogido por el servicio de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-150">**pending** : Scheduled and waiting toobe picked up by hello job service.</span></span> | |
| <span data-ttu-id="cdb97-151">**programado** : programada para una hora en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="cdb97-151">**scheduled** : Scheduled for a time in hello future.</span></span> | |
| <span data-ttu-id="cdb97-152">**running**: trabajo activo actualmente.</span><span class="sxs-lookup"><span data-stu-id="cdb97-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="cdb97-153">**cancelled**: el trabajo se ha cancelado.</span><span class="sxs-lookup"><span data-stu-id="cdb97-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="cdb97-154">**failed**: trabajo erróneo.</span><span class="sxs-lookup"><span data-stu-id="cdb97-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="cdb97-155">**completed**: el trabajo se ha completado.</span><span class="sxs-lookup"><span data-stu-id="cdb97-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="cdb97-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="cdb97-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="cdb97-157">Estadísticas sobre la ejecución del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-157">Statistics about hello job's execution.</span></span> |

<span data-ttu-id="cdb97-158">Propiedades **deviceJobStatistics**.</span><span class="sxs-lookup"><span data-stu-id="cdb97-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="cdb97-159">Propiedad</span><span class="sxs-lookup"><span data-stu-id="cdb97-159">Property</span></span> | <span data-ttu-id="cdb97-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="cdb97-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cdb97-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="cdb97-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="cdb97-162">Número de dispositivos de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-162">Number of devices in hello job.</span></span> |
| <span data-ttu-id="cdb97-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="cdb97-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="cdb97-164">Número de dispositivos que no se pudo trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-164">Number of devices where hello job failed.</span></span> |
| <span data-ttu-id="cdb97-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="cdb97-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="cdb97-166">Número de dispositivos donde se realizó correctamente el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-166">Number of devices where hello job succeeded.</span></span> |
| <span data-ttu-id="cdb97-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="cdb97-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="cdb97-168">Número de dispositivos que se están ejecutando trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-168">Number of devices that are currently running hello job.</span></span> |
| <span data-ttu-id="cdb97-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="cdb97-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="cdb97-170">Número de dispositivos que están pendientes de trabajo de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="cdb97-170">Number of devices that are pending toorun hello job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="cdb97-171">Material de referencia adicional</span><span class="sxs-lookup"><span data-stu-id="cdb97-171">Additional reference material</span></span>
<span data-ttu-id="cdb97-172">Otros temas de referencia en la Guía del desarrollador de centro de IoT Hola incluyen:</span><span class="sxs-lookup"><span data-stu-id="cdb97-172">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="cdb97-173">[Los extremos del centro de IoT] [ lnk-endpoints] describe Hola varios extremos que cada centro de IoT expone las operaciones de tiempo de ejecución y administración.</span><span class="sxs-lookup"><span data-stu-id="cdb97-173">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="cdb97-174">[Limitación y las cuotas] [ lnk-quotas] describe las cuotas de Hola que se aplican toohello servicio del centro de IoT y Hola limitación tooexpect de comportamiento cuando se usa el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-174">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="cdb97-175">[SDK de dispositivos y servicios de Azure IoT] [ lnk-sdks] listas Hola lenguaje varios SDK puede usar cuando se desarrollan aplicaciones de dispositivos y servicios que interactúan con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="cdb97-175">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="cdb97-176">[Lenguaje de consulta de centro de IoT para: los gemelos de dispositivo, los trabajos y el enrutamiento de mensajes] [ lnk-query] describe Hola lenguaje de consultas del centro de IoT puede usar información de tooretrieve centro de IoT de: los gemelos de dispositivo y trabajos.</span><span class="sxs-lookup"><span data-stu-id="cdb97-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="cdb97-177">[Compatibilidad de IoT Hub MQTT] [ lnk-devguide-mqtt] proporciona más información acerca del soporte técnico de centro de IoT para el protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="cdb97-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdb97-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cdb97-178">Next steps</span></span>
<span data-ttu-id="cdb97-179">Si desea que tootry algunos de los conceptos de hello descritos en este artículo, es posible que interesa Hola sigue tutorial del centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="cdb97-179">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="cdb97-180">[Schedule and broadcast jobs][lnk-jobs-tutorial] (Programación y difusión de trabajos)</span><span class="sxs-lookup"><span data-stu-id="cdb97-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
