---
title: "aaaScheduler entidades, términos y conceptos | Documentos de Microsoft"
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
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="a39d9-104">Conceptos, terminología y jerarquía de entidades de Programador</span><span class="sxs-lookup"><span data-stu-id="a39d9-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="a39d9-105">Jerarquía de entidades del Programador</span><span class="sxs-lookup"><span data-stu-id="a39d9-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="a39d9-106">Hello tabla siguiente describe recursos principales de hello expuestos o utilizados por hello API del programador:</span><span class="sxs-lookup"><span data-stu-id="a39d9-106">hello following table describes hello main resources exposed or used by hello Scheduler API:</span></span>

| <span data-ttu-id="a39d9-107">Recurso</span><span class="sxs-lookup"><span data-stu-id="a39d9-107">Resource</span></span> | <span data-ttu-id="a39d9-108">Description</span><span class="sxs-lookup"><span data-stu-id="a39d9-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a39d9-109">**Colección de trabajos**</span><span class="sxs-lookup"><span data-stu-id="a39d9-109">**Job collection**</span></span> |<span data-ttu-id="a39d9-110">Una colección de trabajos contiene un grupo de trabajos y mantiene los valores, cuotas y aceleradores compartidos por los trabajos en la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="a39d9-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within hello collection.</span></span> <span data-ttu-id="a39d9-111">La colección de trabajos la crea el propietario de la suscripción y agrupa los trabajos en función de los límites de uso o de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a39d9-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="a39d9-112">Es región tooone restringida.</span><span class="sxs-lookup"><span data-stu-id="a39d9-112">It’s constrained tooone region.</span></span> <span data-ttu-id="a39d9-113">También permite cumplimiento Hola de cuotas de uso de hello tooconstrain de todos los trabajos en esa colección.</span><span class="sxs-lookup"><span data-stu-id="a39d9-113">It also allows hello enforcement of quotas tooconstrain hello usage of all jobs in that collection.</span></span> <span data-ttu-id="a39d9-114">las cuotas de Hello incluyen MaxJobs y MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="a39d9-114">hello quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="a39d9-115">**Trabajo**</span><span class="sxs-lookup"><span data-stu-id="a39d9-115">**Job**</span></span> |<span data-ttu-id="a39d9-116">Un trabajo define una única acción periódica, con estrategias simples o complejas para su ejecución.</span><span class="sxs-lookup"><span data-stu-id="a39d9-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="a39d9-117">Las acciones pueden incluir solicitudes HTTP, de cola de almacenamiento, de cola de bus de servicio o de tema de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="a39d9-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="a39d9-118">**Historial de trabajos**</span><span class="sxs-lookup"><span data-stu-id="a39d9-118">**Job history**</span></span> |<span data-ttu-id="a39d9-119">Un historial de trabajos representa los detalles de una ejecución de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="a39d9-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="a39d9-120">Contiene los trabajos realizados correctamente y los errores, así como los detalles de las respuestas.</span><span class="sxs-lookup"><span data-stu-id="a39d9-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="a39d9-121">Administración de entidades de Programador</span><span class="sxs-lookup"><span data-stu-id="a39d9-121">Scheduler entity management</span></span>
<span data-ttu-id="a39d9-122">En un nivel alto, programador de Hola y API de administración de servicios de hello exponen hello las siguientes operaciones en recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="a39d9-122">At a high level, hello scheduler and hello service management API expose hello following operations on hello resources:</span></span>

| <span data-ttu-id="a39d9-123">Capacidad</span><span class="sxs-lookup"><span data-stu-id="a39d9-123">Capability</span></span> | <span data-ttu-id="a39d9-124">Descripción y dirección URI</span><span class="sxs-lookup"><span data-stu-id="a39d9-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="a39d9-125">**Administración de la colección de trabajos**</span><span class="sxs-lookup"><span data-stu-id="a39d9-125">**Job collection management**</span></span> |<span data-ttu-id="a39d9-126">GET, PUT y DELETE permiten la creación y modificación de las colecciones de trabajos y trabajos de hello contenidos en él.</span><span class="sxs-lookup"><span data-stu-id="a39d9-126">GET, PUT, and DELETE support for creating and modifying job collections and hello jobs contained therein.</span></span> <span data-ttu-id="a39d9-127">Una colección de trabajos es un contenedor para trabajos y asigna tooquotas y la configuración compartida.</span><span class="sxs-lookup"><span data-stu-id="a39d9-127">A job collection is a container for jobs and maps tooquotas and shared settings.</span></span> <span data-ttu-id="a39d9-128">Ejemplos de cuotas, descritos más adelante, son el número máximo de trabajos y un intervalo menor de periodicidad.</span><span class="sxs-lookup"><span data-stu-id="a39d9-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="a39d9-129">PUT y DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="a39d9-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="a39d9-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="a39d9-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="a39d9-131">**Administración de trabajos**</span><span class="sxs-lookup"><span data-stu-id="a39d9-131">**Job management**</span></span> |<span data-ttu-id="a39d9-132">GET, PUT, POST, PATCH y DELETE permiten la creación y modificación de trabajos.</span><span class="sxs-lookup"><span data-stu-id="a39d9-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="a39d9-133">Todos los trabajos deben pertenecer a colección de trabajos de tooa que ya existe, así que no hay ninguna creación implícita.</span><span class="sxs-lookup"><span data-stu-id="a39d9-133">All jobs must belong tooa job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="a39d9-134">**Administración del historial de trabajos**</span><span class="sxs-lookup"><span data-stu-id="a39d9-134">**Job history management**</span></span> |<span data-ttu-id="a39d9-135">GET admite la recuperación de 60 días de historial de ejecución de trabajos, como el tiempo de trabajo transcurrido y los resultados de la ejecución del trabajo.</span><span class="sxs-lookup"><span data-stu-id="a39d9-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="a39d9-136">Agrega compatibilidad de parámetros de cadena de consulta para filtrar basándose en el estado y la situación.</span><span class="sxs-lookup"><span data-stu-id="a39d9-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="a39d9-137">Tipos de trabajo</span><span class="sxs-lookup"><span data-stu-id="a39d9-137">Job types</span></span>
<span data-ttu-id="a39d9-138">Hay varios tipos de trabajos: trabajos HTTP (incluidos trabajos HTTPS que admiten SSL), trabajos de cola de almacenamiento, trabajos de cola de bus de servicio y trabajos de tema de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="a39d9-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="a39d9-139">Los trabajos HTTP son perfectos si dispone de un extremo de una carga de trabajo o servicio existente.</span><span class="sxs-lookup"><span data-stu-id="a39d9-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="a39d9-140">Puede utilizar la cola trabajos toopost mensajes toostorage las colas de almacenamiento, por lo que dichos trabajos son ideales para cargas de trabajo que utilizan colas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a39d9-140">You can use storage queue jobs toopost messages toostorage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="a39d9-141">De forma similar, los trabajos de bus de servicio son ideales para cargas de trabajo que usan temas y colas de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="a39d9-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="hello-job-entity-in-detail"></a><span data-ttu-id="a39d9-142">entidad de "trabajo" Hello en detalle</span><span class="sxs-lookup"><span data-stu-id="a39d9-142">hello "job" entity in detail</span></span>
<span data-ttu-id="a39d9-143">En un nivel básico, un trabajo programado cuenta con varias partes:</span><span class="sxs-lookup"><span data-stu-id="a39d9-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="a39d9-144">Hola tooperform acción cuando se activa el temporizador de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="a39d9-144">hello action tooperform when hello job timer fires</span></span>  
* <span data-ttu-id="a39d9-145">Trabajo hello toorun Hola (opcional)</span><span class="sxs-lookup"><span data-stu-id="a39d9-145">(Optional) hello time toorun hello job</span></span>  
* <span data-ttu-id="a39d9-146">(Opcional) Cuándo y con qué frecuencia trabajo de hello toorepeat</span><span class="sxs-lookup"><span data-stu-id="a39d9-146">(Optional) When and how often toorepeat hello job</span></span>  
* <span data-ttu-id="a39d9-147">(Opcional) Un toofire de acción si se produce un error en la acción principal de Hola</span><span class="sxs-lookup"><span data-stu-id="a39d9-147">(Optional) An action toofire if hello primary action fails</span></span>  

<span data-ttu-id="a39d9-148">Internamente, un trabajo programado contiene también datos proporcionados por el sistema como Hola siguiente hora de ejecución programada.</span><span class="sxs-lookup"><span data-stu-id="a39d9-148">Internally, a scheduled job also contains system-provided data such as hello next scheduled execution time.</span></span>

<span data-ttu-id="a39d9-149">Hola siguiente código proporciona un ejemplo completo de un trabajo programado.</span><span class="sxs-lookup"><span data-stu-id="a39d9-149">hello following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="a39d9-150">En las secciones siguientes se proporcionan los detalles.</span><span class="sxs-lookup"><span data-stu-id="a39d9-150">Details are provided in subsequent sections.</span></span>

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
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
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

<span data-ttu-id="a39d9-151">Tal como se muestra en la anterior de trabajo programado de ejemplo de Hola, una definición de trabajo tiene varias partes:</span><span class="sxs-lookup"><span data-stu-id="a39d9-151">As seen in hello sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="a39d9-152">Hora de inicio ("startTime")</span><span class="sxs-lookup"><span data-stu-id="a39d9-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="a39d9-153">Acción ("action"), que incluye la acción del error ("errorAction")</span><span class="sxs-lookup"><span data-stu-id="a39d9-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="a39d9-154">Periodicidad ("recurrence")</span><span class="sxs-lookup"><span data-stu-id="a39d9-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="a39d9-155">Situación ("state")</span><span class="sxs-lookup"><span data-stu-id="a39d9-155">State (“state”)</span></span>  
* <span data-ttu-id="a39d9-156">Estado ("status")</span><span class="sxs-lookup"><span data-stu-id="a39d9-156">Status (“status”)</span></span>  
* <span data-ttu-id="a39d9-157">Directiva de reintentos (“retryPolicy”)</span><span class="sxs-lookup"><span data-stu-id="a39d9-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="a39d9-158">Examinemos cada uno de ellos en detalle:</span><span class="sxs-lookup"><span data-stu-id="a39d9-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="a39d9-159">startTime</span><span class="sxs-lookup"><span data-stu-id="a39d9-159">startTime</span></span>
<span data-ttu-id="a39d9-160">Hola "startTime" es la hora de inicio de Hola y permite Hola llamador toospecify una zona horaria de desplazamiento en el cable hello en [formato ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="a39d9-160">hello "startTime” is hello start time and allows hello caller toospecify a time zone offset on hello wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="a39d9-161">action y errorAction</span><span class="sxs-lookup"><span data-stu-id="a39d9-161">action and errorAction</span></span>
<span data-ttu-id="a39d9-162">Hola "action" es la acción de hello invocada cada vez y describe un tipo de invocación del servicio.</span><span class="sxs-lookup"><span data-stu-id="a39d9-162">hello “action” is hello action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="a39d9-163">acción de Hello es lo que se ejecutará en hello proporcionada programación.</span><span class="sxs-lookup"><span data-stu-id="a39d9-163">hello action is what will be executed on hello provided schedule.</span></span> <span data-ttu-id="a39d9-164">El Programador admite acciones HTTP, de cola de almacenamiento, de cola de bus de servicio y de tema de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="a39d9-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="a39d9-165">acción de Hello en el ejemplo de Hola anterior es una acción HTTP.</span><span class="sxs-lookup"><span data-stu-id="a39d9-165">hello action in hello example above is an HTTP action.</span></span> <span data-ttu-id="a39d9-166">A continuación se muestra un ejemplo de una acción de cola de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="a39d9-166">Below is an example of a storage queue action:</span></span>

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

<span data-ttu-id="a39d9-167">A continuación se muestra un ejemplo de una acción de tema de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="a39d9-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="a39d9-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="a39d9-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="a39d9-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="a39d9-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="a39d9-170">A continuación se muestra un ejemplo de una acción de cola de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="a39d9-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="a39d9-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="a39d9-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="a39d9-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="a39d9-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="a39d9-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="a39d9-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="a39d9-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="a39d9-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="a39d9-175">Hola "errorAction" es el controlador de errores de hello, acción de Hola se invoca cuando se produce un error en la acción principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a39d9-175">hello “errorAction” is hello error handler, hello action invoked when hello primary action fails.</span></span> <span data-ttu-id="a39d9-176">Puede usar esta variable toocall un punto de conexión de control de errores o enviar una notificación al usuario.</span><span class="sxs-lookup"><span data-stu-id="a39d9-176">You can use this variable toocall an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="a39d9-177">Esto se puede utilizar para llegar a un extremo secundario en caso de hello ese Hola principal no está disponible (p. ej., en caso de hello de un desastre en el sitio del punto de conexión de hello) o puede usarse para notificar a un punto de conexión de control de errores.</span><span class="sxs-lookup"><span data-stu-id="a39d9-177">This can be used for reaching a secondary endpoint in hello case that hello primary is not available (e.g., in hello case of a disaster at hello endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="a39d9-178">Igual que la acción principal de hello, acción de error de hello puede ser lógica sencilla o compuesta basada en otras acciones.</span><span class="sxs-lookup"><span data-stu-id="a39d9-178">Just like hello primary action, hello error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="a39d9-179">toolearn cómo toocreate un token de SAS, consulte demasiado[crear y usar una firma de acceso compartido](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="a39d9-179">toolearn how toocreate a SAS token, refer too[Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="a39d9-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="a39d9-180">recurrence</span></span>
<span data-ttu-id="a39d9-181">La periodicidad tiene varias partes:</span><span class="sxs-lookup"><span data-stu-id="a39d9-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="a39d9-182">Frecuencia: un minuto, hora, día, semana, mes, año</span><span class="sxs-lookup"><span data-stu-id="a39d9-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="a39d9-183">Intervalo: El intervalo en hello dada la frecuencia de repetición de Hola</span><span class="sxs-lookup"><span data-stu-id="a39d9-183">Interval: Interval at hello given frequency for hello recurrence</span></span>  
* <span data-ttu-id="a39d9-184">Programación prescrita: especifique minutos, horas, días de la semana, meses y días mes para de periodicidad de Hola</span><span class="sxs-lookup"><span data-stu-id="a39d9-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of hello recurrence</span></span>  
* <span data-ttu-id="a39d9-185">Recuento: número de repeticiones</span><span class="sxs-lookup"><span data-stu-id="a39d9-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="a39d9-186">Hora de finalización: trabajos se ejecutarán después de hello especifica hora de finalización</span><span class="sxs-lookup"><span data-stu-id="a39d9-186">End time: No jobs will execute after hello specified end time</span></span>  

<span data-ttu-id="a39d9-187">Un trabajo es periódico si tiene un objeto de periodicidad especificado en la definición de JSON.</span><span class="sxs-lookup"><span data-stu-id="a39d9-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="a39d9-188">Si se especifican el recuento y la hora de finalización, se respeta la regla de finalización Hola que ocurra primero.</span><span class="sxs-lookup"><span data-stu-id="a39d9-188">If both count and endTime are specified, hello completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="a39d9-189">state</span><span class="sxs-lookup"><span data-stu-id="a39d9-189">state</span></span>
<span data-ttu-id="a39d9-190">estado de Hello del trabajo de hello es uno de cuatro valores: habilitado, deshabilitado, completado o con errores.</span><span class="sxs-lookup"><span data-stu-id="a39d9-190">hello state of hello job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="a39d9-191">Puede colocar o revisión lo trabajos como tooupdate les toohello habilita o deshabilita el estado.</span><span class="sxs-lookup"><span data-stu-id="a39d9-191">You can PUT or PATCH jobs so as tooupdate them toohello enabled or disabled state.</span></span> <span data-ttu-id="a39d9-192">Si un trabajo se ha completado o con errores, que es un estado final que no se puede actualizar (aunque todavía se puede eliminar el trabajo de hello).</span><span class="sxs-lookup"><span data-stu-id="a39d9-192">If a job has been completed or faulted, that is a final state that cannot be updated (though hello job can still be DELETED).</span></span> <span data-ttu-id="a39d9-193">Un ejemplo de la propiedad state de hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="a39d9-193">An example of hello state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="a39d9-194">Los trabajos completados y con errores se eliminan después de 60 días.</span><span class="sxs-lookup"><span data-stu-id="a39d9-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="a39d9-195">status</span><span class="sxs-lookup"><span data-stu-id="a39d9-195">status</span></span>
<span data-ttu-id="a39d9-196">Cuando se inicia un trabajo del programador, se devolverá información sobre el estado actual de Hola de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a39d9-196">Once a Scheduler job has started, information will be returned about hello current status of hello job.</span></span> <span data-ttu-id="a39d9-197">Este objeto no es configurable por el usuario de hello: se establece por sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="a39d9-197">This object is not settable by hello user—it’s set by hello system.</span></span> <span data-ttu-id="a39d9-198">Sin embargo, se incluye en hello objeto de trabajo (en lugar de un recurso vinculado independiente) para que se pueda obtener estado de Hola de un trabajo fácilmente.</span><span class="sxs-lookup"><span data-stu-id="a39d9-198">However, it is included in hello job object (rather than a separate linked resource) so that one can obtain hello status of a job easily.</span></span>

<span data-ttu-id="a39d9-199">Estado del trabajo incluye el tiempo de Hola Hola anterior de la ejecución de (si existe) Hola momento de la siguiente ejecución programada hello (para los trabajos en curso) y el recuento de la ejecución del trabajo de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="a39d9-199">Job status includes hello time of hello previous execution (if any), hello time of hello next scheduled execution (for in-progress jobs), and hello execution count of hello job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="a39d9-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="a39d9-200">retryPolicy</span></span>
<span data-ttu-id="a39d9-201">Si se produce un error en un trabajo del programador, es posible toospecify un toodetermine de directiva de reintentos si y cómo se vuelve a intentar la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="a39d9-201">If a Scheduler job fails, it is possible toospecify a retry policy toodetermine whether and how hello action is retried.</span></span> <span data-ttu-id="a39d9-202">Esto viene determinado por hello **retryType** objeto: se establece demasiado**ninguno** si no hay ninguna directiva de reintentos, como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a39d9-202">This is determined by hello **retryType** object—it is set too**none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="a39d9-203">Establézcalo demasiado**fijo** si hay una directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="a39d9-203">Set it too**fixed** if there is a retry policy.</span></span>

<span data-ttu-id="a39d9-204">tooset una directiva de reintentos, se pueden especificar dos configuraciones adicionales: un intervalo de reintentos (**retryInterval**) y Hola número de reintentos (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="a39d9-204">tooset a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and hello number of retries (**retryCount**).</span></span>

<span data-ttu-id="a39d9-205">intervalo de reintento de Hello, especificado con hello **retryInterval** de objetos, es Hola intervalo entre reintentos.</span><span class="sxs-lookup"><span data-stu-id="a39d9-205">hello retry interval, specified with hello **retryInterval** object, is hello interval between retries.</span></span> <span data-ttu-id="a39d9-206">Su valor predeterminado es de 30 segundos, su valor configurable mínimo es de 15 segundos y su valor máximo es de 18 meses.</span><span class="sxs-lookup"><span data-stu-id="a39d9-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="a39d9-207">Los trabajos de las colecciones de trabajos gratis tienen un valor configurable mínimo de 1 hora.</span><span class="sxs-lookup"><span data-stu-id="a39d9-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="a39d9-208">Se define en formato ISO 8601 Hola.</span><span class="sxs-lookup"><span data-stu-id="a39d9-208">It is defined in hello ISO 8601 format.</span></span> <span data-ttu-id="a39d9-209">De forma similar, Hola de número de Hola de reintentos se expresa con hello **retryCount** objeto; es Hola número de veces que se realiza un reintento.</span><span class="sxs-lookup"><span data-stu-id="a39d9-209">Similarly, hello value of hello number of retries is specified with hello **retryCount** object; it is hello number of times a retry is attempted.</span></span> <span data-ttu-id="a39d9-210">Su valor predeterminado es 4, y su valor máximo es 20\.</span><span class="sxs-lookup"><span data-stu-id="a39d9-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="a39d9-211">Ambos **retryInterval** y **retryCount** son opcionales.</span><span class="sxs-lookup"><span data-stu-id="a39d9-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="a39d9-212">Tienen sus valores predeterminados si **retryType** se establece demasiado**fijo** y se especifica explícitamente ningún valor.</span><span class="sxs-lookup"><span data-stu-id="a39d9-212">They are given their default values if **retryType** is set too**fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="a39d9-213">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a39d9-213">See also</span></span>
 [<span data-ttu-id="a39d9-214">¿Qué es Programador?</span><span class="sxs-lookup"><span data-stu-id="a39d9-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="a39d9-215">Empezar a usar a Scheduler en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a39d9-215">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="a39d9-216">Planes y facturación en Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="a39d9-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="a39d9-217">¿Cómo se programa toobuild complejo y periodicidad avanzada con el programador de Azure</span><span class="sxs-lookup"><span data-stu-id="a39d9-217">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="a39d9-218">Referencia de API de REST de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="a39d9-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="a39d9-219">Referencia de cmdlets de PowerShell de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="a39d9-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="a39d9-220">Alta disponibilidad y confiabilidad de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="a39d9-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="a39d9-221">Límites, valores predeterminados y códigos de error de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="a39d9-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="a39d9-222">Autenticación de salida de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="a39d9-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

