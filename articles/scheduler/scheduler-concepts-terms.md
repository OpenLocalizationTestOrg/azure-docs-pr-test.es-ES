---
title: "Conceptos, términos y entidades del programador | Microsoft Docs"
description: "Conceptos del Programador de Azure, terminología y jerarquía de entidades, incluidos trabajos y colecciones de trabajos.  Proporciona un ejemplo completo de un trabajo programado."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 0f035b58ccd140a5481703df7e184206da2ed651
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="313c5-104">Conceptos, terminología y jerarquía de entidades de Programador</span><span class="sxs-lookup"><span data-stu-id="313c5-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="313c5-105">Jerarquía de entidades del Programador</span><span class="sxs-lookup"><span data-stu-id="313c5-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="313c5-106">En la tabla siguiente se describen los recursos principales expuestos o utilizados por la API del Programador:</span><span class="sxs-lookup"><span data-stu-id="313c5-106">The following table describes the main resources exposed or used by the Scheduler API:</span></span>

| <span data-ttu-id="313c5-107">Recurso</span><span class="sxs-lookup"><span data-stu-id="313c5-107">Resource</span></span> | <span data-ttu-id="313c5-108">Description</span><span class="sxs-lookup"><span data-stu-id="313c5-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="313c5-109">**Colección de trabajos**</span><span class="sxs-lookup"><span data-stu-id="313c5-109">**Job collection**</span></span> |<span data-ttu-id="313c5-110">Una colección de trabajos contiene un grupo de trabajos y mantiene configuraciones, cuotas y aceleradores compartidos por los trabajos de la colección.</span><span class="sxs-lookup"><span data-stu-id="313c5-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within the collection.</span></span> <span data-ttu-id="313c5-111">La colección de trabajos la crea el propietario de la suscripción y agrupa los trabajos en función de los límites de uso o de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="313c5-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="313c5-112">Está limitado a una región.</span><span class="sxs-lookup"><span data-stu-id="313c5-112">It’s constrained to one region.</span></span> <span data-ttu-id="313c5-113">También permite la aplicación de cuotas para restringir el uso de todos los trabajos de la colección.</span><span class="sxs-lookup"><span data-stu-id="313c5-113">It also allows the enforcement of quotas to constrain the usage of all jobs in that collection.</span></span> <span data-ttu-id="313c5-114">Las cuotas incluyen MaxJobs y MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="313c5-114">The quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="313c5-115">**Trabajo**</span><span class="sxs-lookup"><span data-stu-id="313c5-115">**Job**</span></span> |<span data-ttu-id="313c5-116">Un trabajo define una única acción periódica, con estrategias simples o complejas para su ejecución.</span><span class="sxs-lookup"><span data-stu-id="313c5-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="313c5-117">Las acciones pueden incluir solicitudes HTTP, de cola de almacenamiento, de cola de bus de servicio o de tema de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="313c5-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="313c5-118">**Historial de trabajos**</span><span class="sxs-lookup"><span data-stu-id="313c5-118">**Job history**</span></span> |<span data-ttu-id="313c5-119">Un historial de trabajos representa los detalles de una ejecución de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="313c5-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="313c5-120">Contiene los trabajos realizados correctamente y los errores, así como los detalles de las respuestas.</span><span class="sxs-lookup"><span data-stu-id="313c5-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="313c5-121">Administración de entidades de Programador</span><span class="sxs-lookup"><span data-stu-id="313c5-121">Scheduler entity management</span></span>
<span data-ttu-id="313c5-122">En un nivel superior, el Programador y la API de administración de servicio exponen las operaciones siguientes en los recursos:</span><span class="sxs-lookup"><span data-stu-id="313c5-122">At a high level, the scheduler and the service management API expose the following operations on the resources:</span></span>

| <span data-ttu-id="313c5-123">Capacidad</span><span class="sxs-lookup"><span data-stu-id="313c5-123">Capability</span></span> | <span data-ttu-id="313c5-124">Descripción y dirección URI</span><span class="sxs-lookup"><span data-stu-id="313c5-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="313c5-125">**Administración de la colección de trabajos**</span><span class="sxs-lookup"><span data-stu-id="313c5-125">**Job collection management**</span></span> |<span data-ttu-id="313c5-126">GET, PUT y DELETE permiten la creación y modificación de las colecciones de trabajos y trabajos que contienen.</span><span class="sxs-lookup"><span data-stu-id="313c5-126">GET, PUT, and DELETE support for creating and modifying job collections and the jobs contained therein.</span></span> <span data-ttu-id="313c5-127">Una colección de trabajos es un contenedor para trabajos, asignaciones para cuotas y configuración compartida.</span><span class="sxs-lookup"><span data-stu-id="313c5-127">A job collection is a container for jobs and maps to quotas and shared settings.</span></span> <span data-ttu-id="313c5-128">Ejemplos de cuotas, descritos más adelante, son el número máximo de trabajos y un intervalo menor de periodicidad.</span><span class="sxs-lookup"><span data-stu-id="313c5-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="313c5-129">PUT y DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="313c5-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="313c5-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="313c5-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="313c5-131">**Administración de trabajos**</span><span class="sxs-lookup"><span data-stu-id="313c5-131">**Job management**</span></span> |<span data-ttu-id="313c5-132">GET, PUT, POST, PATCH y DELETE permiten la creación y modificación de trabajos.</span><span class="sxs-lookup"><span data-stu-id="313c5-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="313c5-133">Todos los trabajos deben pertenecer a una colección de trabajos que ya existe, así que no hay ninguna creación implícita.</span><span class="sxs-lookup"><span data-stu-id="313c5-133">All jobs must belong to a job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="313c5-134">**Administración del historial de trabajos**</span><span class="sxs-lookup"><span data-stu-id="313c5-134">**Job history management**</span></span> |<span data-ttu-id="313c5-135">GET admite la recuperación de 60 días de historial de ejecución de trabajos, como el tiempo de trabajo transcurrido y los resultados de la ejecución del trabajo.</span><span class="sxs-lookup"><span data-stu-id="313c5-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="313c5-136">Agrega compatibilidad de parámetros de cadena de consulta para filtrar basándose en el estado y la situación.</span><span class="sxs-lookup"><span data-stu-id="313c5-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="313c5-137">Tipos de trabajo</span><span class="sxs-lookup"><span data-stu-id="313c5-137">Job types</span></span>
<span data-ttu-id="313c5-138">Hay varios tipos de trabajos: trabajos HTTP (incluidos trabajos HTTPS que admiten SSL), trabajos de cola de almacenamiento, trabajos de cola de bus de servicio y trabajos de tema de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="313c5-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="313c5-139">Los trabajos HTTP son perfectos si dispone de un extremo de una carga de trabajo o servicio existente.</span><span class="sxs-lookup"><span data-stu-id="313c5-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="313c5-140">Puede usar trabajos de cola de almacenamiento para enviar mensajes a colas de almacenamiento, por lo que dichos trabajos son ideales para cargas de trabajo que utilizan colas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="313c5-140">You can use storage queue jobs to post messages to storage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="313c5-141">De forma similar, los trabajos de bus de servicio son ideales para cargas de trabajo que usan temas y colas de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="313c5-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="the-job-entity-in-detail"></a><span data-ttu-id="313c5-142">La entidad "Trabajo" en detalle</span><span class="sxs-lookup"><span data-stu-id="313c5-142">The "job" entity in detail</span></span>
<span data-ttu-id="313c5-143">En un nivel básico, un trabajo programado cuenta con varias partes:</span><span class="sxs-lookup"><span data-stu-id="313c5-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="313c5-144">La acción que se va a realizar cuando se activa el temporizador de trabajo</span><span class="sxs-lookup"><span data-stu-id="313c5-144">The action to perform when the job timer fires</span></span>  
* <span data-ttu-id="313c5-145">(Opcional) El tiempo para ejecutar el trabajo</span><span class="sxs-lookup"><span data-stu-id="313c5-145">(Optional) The time to run the job</span></span>  
* <span data-ttu-id="313c5-146">(Opcional) Cuándo y con qué frecuencia se debe repetir el trabajo</span><span class="sxs-lookup"><span data-stu-id="313c5-146">(Optional) When and how often to repeat the job</span></span>  
* <span data-ttu-id="313c5-147">(Opcional) Una acción que se desencadena si se produce un error en la acción principal</span><span class="sxs-lookup"><span data-stu-id="313c5-147">(Optional) An action to fire if the primary action fails</span></span>  

<span data-ttu-id="313c5-148">Internamente, un trabajo programado contiene también datos proporcionados por el sistema, como la siguiente hora de ejecución programada.</span><span class="sxs-lookup"><span data-stu-id="313c5-148">Internally, a scheduled job also contains system-provided data such as the next scheduled execution time.</span></span>

<span data-ttu-id="313c5-149">El código siguiente proporciona un ejemplo completo de un trabajo programado.</span><span class="sxs-lookup"><span data-stu-id="313c5-149">The following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="313c5-150">En las secciones siguientes se proporcionan los detalles.</span><span class="sxs-lookup"><span data-stu-id="313c5-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often to fire (default to 1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default to recur infinitely)
            "endTime": "2012-11-04",                     // optional (default to recur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="313c5-151">Como se muestra en el trabajo programado de ejemplo anterior, una definición de trabajo tiene varias partes:</span><span class="sxs-lookup"><span data-stu-id="313c5-151">As seen in the sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="313c5-152">Hora de inicio ("startTime")</span><span class="sxs-lookup"><span data-stu-id="313c5-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="313c5-153">Acción ("action"), que incluye la acción del error ("errorAction")</span><span class="sxs-lookup"><span data-stu-id="313c5-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="313c5-154">Periodicidad ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="313c5-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="313c5-155">Situación ("state")</span><span class="sxs-lookup"><span data-stu-id="313c5-155">State (“state”)</span></span>  
* <span data-ttu-id="313c5-156">Estado ("status")</span><span class="sxs-lookup"><span data-stu-id="313c5-156">Status (“status”)</span></span>  
* <span data-ttu-id="313c5-157">Directiva de reintentos (“retryPolicy”)</span><span class="sxs-lookup"><span data-stu-id="313c5-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="313c5-158">Examinemos cada uno de ellos en detalle:</span><span class="sxs-lookup"><span data-stu-id="313c5-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="313c5-159">startTime</span><span class="sxs-lookup"><span data-stu-id="313c5-159">startTime</span></span>
<span data-ttu-id="313c5-160">"startTime" es la hora de inicio y permite al que llama especificar un desplazamiento de zona horaria en el cable en [formato ISO-8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="313c5-160">The "startTime” is the start time and allows the caller to specify a time zone offset on the wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="313c5-161">action y errorAction</span><span class="sxs-lookup"><span data-stu-id="313c5-161">action and errorAction</span></span>
<span data-ttu-id="313c5-162">"action" es la acción que se invoca en cada repetición y describe un tipo de invocación del servicio.</span><span class="sxs-lookup"><span data-stu-id="313c5-162">The “action” is the action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="313c5-163">La acción es lo que se ejecutará en la programación especificada.</span><span class="sxs-lookup"><span data-stu-id="313c5-163">The action is what will be executed on the provided schedule.</span></span> <span data-ttu-id="313c5-164">El Programador admite acciones HTTP, de cola de almacenamiento, de cola de bus de servicio y de tema de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="313c5-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="313c5-165">La acción en el ejemplo anterior es una acción http.</span><span class="sxs-lookup"><span data-stu-id="313c5-165">The action in the example above is an HTTP action.</span></span> <span data-ttu-id="313c5-166">A continuación se muestra un ejemplo de una acción de cola de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="313c5-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="313c5-167">A continuación se muestra un ejemplo de una acción de tema de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="313c5-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="313c5-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="313c5-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="313c5-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="313c5-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="313c5-170">A continuación se muestra un ejemplo de una acción de cola de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="313c5-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="313c5-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="313c5-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="313c5-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="313c5-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="313c5-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="313c5-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="313c5-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="313c5-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="313c5-175">"errorAction" es el controlador de errores, la acción que se invoca cuando se produce un error en la acción primaria.</span><span class="sxs-lookup"><span data-stu-id="313c5-175">The “errorAction” is the error handler, the action invoked when the primary action fails.</span></span> <span data-ttu-id="313c5-176">Puede usar esta variable para llamar a un extremo de control de errores o para enviar una notificación al usuario.</span><span class="sxs-lookup"><span data-stu-id="313c5-176">You can use this variable to call an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="313c5-177">Esto puede usarse para llegar a un extremo secundario en caso de que el principal no esté disponible (por ejemplo, en caso de un desastre en el sitio del extremo) o se puede usar para notificar a un extremo de control de errores.</span><span class="sxs-lookup"><span data-stu-id="313c5-177">This can be used for reaching a secondary endpoint in the case that the primary is not available (e.g., in the case of a disaster at the endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="313c5-178">Igual que la acción primaria, la acción de error puede ser una lógica simple o compuesta basada en otras acciones.</span><span class="sxs-lookup"><span data-stu-id="313c5-178">Just like the primary action, the error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="313c5-179">Para obtener información sobre cómo crear un token de SAS, consulte [Crear y usar una firma de acceso compartido](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="313c5-179">To learn how to create a SAS token, refer to [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="313c5-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="313c5-180">recurrence</span></span>
<span data-ttu-id="313c5-181">La periodicidad tiene varias partes:</span><span class="sxs-lookup"><span data-stu-id="313c5-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="313c5-182">Frecuencia: un minuto, hora, día, semana, mes, año</span><span class="sxs-lookup"><span data-stu-id="313c5-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="313c5-183">Intervalo: el intervalo de frecuencia definido para la periodicidad</span><span class="sxs-lookup"><span data-stu-id="313c5-183">Interval: Interval at the given frequency for the recurrence</span></span>  
* <span data-ttu-id="313c5-184">Programación prescrita: especifique minutos, horas, días de la semana, meses y días de mes para de la periodicidad</span><span class="sxs-lookup"><span data-stu-id="313c5-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of the recurrence</span></span>  
* <span data-ttu-id="313c5-185">Recuento: número de repeticiones</span><span class="sxs-lookup"><span data-stu-id="313c5-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="313c5-186">Hora de finalización: ningún trabajo se ejecutará después de la hora de finalización especificada</span><span class="sxs-lookup"><span data-stu-id="313c5-186">End time: No jobs will execute after the specified end time</span></span>  

<span data-ttu-id="313c5-187">Un trabajo es periódico si tiene un objeto de periodicidad especificado en la definición de JSON.</span><span class="sxs-lookup"><span data-stu-id="313c5-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="313c5-188">Si se especifican a la vez count y endTime, se respeta la regla de finalización que se produzca primero.</span><span class="sxs-lookup"><span data-stu-id="313c5-188">If both count and endTime are specified, the completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="313c5-189">state</span><span class="sxs-lookup"><span data-stu-id="313c5-189">state</span></span>
<span data-ttu-id="313c5-190">La situación del trabajo es una de cuatro valores: habilitado, deshabilitado, completado o con errores.</span><span class="sxs-lookup"><span data-stu-id="313c5-190">The state of the job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="313c5-191">Puede utilizar PUT o PATCH para los trabajos para actualizarlos al estado habilitado o deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="313c5-191">You can PUT or PATCH jobs so as to update them to the enabled or disabled state.</span></span> <span data-ttu-id="313c5-192">Si un trabajo se ha completado o tiene errores, es el estado final el que no se puede actualizar (aunque todavía se pueda eliminar el trabajo).</span><span class="sxs-lookup"><span data-stu-id="313c5-192">If a job has been completed or faulted, that is a final state that cannot be updated (though the job can still be DELETED).</span></span> <span data-ttu-id="313c5-193">Un ejemplo de la propiedad state es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="313c5-193">An example of the state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="313c5-194">Los trabajos completados y con errores se eliminan después de 60 días.</span><span class="sxs-lookup"><span data-stu-id="313c5-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="313c5-195">status</span><span class="sxs-lookup"><span data-stu-id="313c5-195">status</span></span>
<span data-ttu-id="313c5-196">Una vez que se inició un trabajo de Programador, se devolverá información sobre el estado actual del trabajo.</span><span class="sxs-lookup"><span data-stu-id="313c5-196">Once a Scheduler job has started, information will be returned about the current status of the job.</span></span> <span data-ttu-id="313c5-197">Este objeto no es configurable por el usuario: lo establece el sistema.</span><span class="sxs-lookup"><span data-stu-id="313c5-197">This object is not settable by the user—it’s set by the system.</span></span> <span data-ttu-id="313c5-198">Sin embargo, se incluye en el objeto de trabajo (en lugar de un recurso vinculado independiente) para que se pueda obtener fácilmente el estado de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="313c5-198">However, it is included in the job object (rather than a separate linked resource) so that one can obtain the status of a job easily.</span></span>

<span data-ttu-id="313c5-199">El estado del trabajo incluye el tiempo de la ejecución anterior (si hay alguna), el tiempo de la siguiente ejecución programada (para los trabajos en curso) y el recuento de la ejecución del trabajo.</span><span class="sxs-lookup"><span data-stu-id="313c5-199">Job status includes the time of the previous execution (if any), the time of the next scheduled execution (for in-progress jobs), and the execution count of the job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="313c5-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="313c5-200">retryPolicy</span></span>
<span data-ttu-id="313c5-201">Si se produce un error en un trabajo de Programador, es posible especificar una directiva de reintentos para determinar cuándo y cómo se vuelve a intentar la acción.</span><span class="sxs-lookup"><span data-stu-id="313c5-201">If a Scheduler job fails, it is possible to specify a retry policy to determine whether and how the action is retried.</span></span> <span data-ttu-id="313c5-202">Esto viene determinado por el objeto **retryType**: está establecido en **none** si no hay ninguna directiva de reintentos, como se mostró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="313c5-202">This is determined by the **retryType** object—it is set to **none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="313c5-203">Establézcalo en **fixed** si hay una directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="313c5-203">Set it to **fixed** if there is a retry policy.</span></span>

<span data-ttu-id="313c5-204">Para establecer una directiva de reintentos, se pueden especificar dos configuraciones adicionales: un intervalo de reintento (**retryInterval**) y el número de reintentos (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="313c5-204">To set a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and the number of retries (**retryCount**).</span></span>

<span data-ttu-id="313c5-205">El intervalo de reintentos, especificado con el objeto **retryInterval** , es el intervalo entre reintentos.</span><span class="sxs-lookup"><span data-stu-id="313c5-205">The retry interval, specified with the **retryInterval** object, is the interval between retries.</span></span> <span data-ttu-id="313c5-206">Su valor predeterminado es de 30 segundos, su valor configurable mínimo es de 15 segundos y su valor máximo es de 18 meses.</span><span class="sxs-lookup"><span data-stu-id="313c5-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="313c5-207">Los trabajos de las colecciones de trabajos gratis tienen un valor configurable mínimo de 1 hora.</span><span class="sxs-lookup"><span data-stu-id="313c5-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="313c5-208">Se define en el formato ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="313c5-208">It is defined in the ISO 8601 format.</span></span> <span data-ttu-id="313c5-209">Del mismo modo, se especifica el valor del número de reintentos con el objeto **retryCount** ; es el número de veces que se realiza un reintento.</span><span class="sxs-lookup"><span data-stu-id="313c5-209">Similarly, the value of the number of retries is specified with the **retryCount** object; it is the number of times a retry is attempted.</span></span> <span data-ttu-id="313c5-210">Su valor predeterminado es 4, y su valor máximo es 20\.</span><span class="sxs-lookup"><span data-stu-id="313c5-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="313c5-211">Ambos **retryInterval** y **retryCount** son opcionales.</span><span class="sxs-lookup"><span data-stu-id="313c5-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="313c5-212">Obtienen sus valores predeterminados si **retryType** está establecido en **fixed** y no se especifican explícitamente los valores.</span><span class="sxs-lookup"><span data-stu-id="313c5-212">They are given their default values if **retryType** is set to **fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="313c5-213">Consulte también</span><span class="sxs-lookup"><span data-stu-id="313c5-213">See also</span></span>
 [<span data-ttu-id="313c5-214">¿Qué es Programador?</span><span class="sxs-lookup"><span data-stu-id="313c5-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="313c5-215">Introducción al uso de Programador de Azure en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="313c5-215">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="313c5-216">Planes y facturación en Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="313c5-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="313c5-217">Creación de programaciones complejas y periodicidad avanzada con Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="313c5-217">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="313c5-218">Referencia de API de REST de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="313c5-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="313c5-219">Referencia de cmdlets de PowerShell de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="313c5-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="313c5-220">Alta disponibilidad y confiabilidad de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="313c5-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="313c5-221">Límites, valores predeterminados y códigos de error de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="313c5-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="313c5-222">Autenticación de salida de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="313c5-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

