---
title: "registros de diagnóstico de los centros de eventos aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset los registros de diagnóstico de concentradores de eventos de Azure."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="cb32b-103">Registros de diagnósticos de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cb32b-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="cb32b-104">Puede ver dos tipos de registros para Event Hubs de Azure:</span><span class="sxs-lookup"><span data-stu-id="cb32b-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="cb32b-105">**[Registros de actividad](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="cb32b-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="cb32b-106">Estos registros contienen información sobre las operaciones realizadas en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="cb32b-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="cb32b-107">registros de Hello siempre están habilitados.</span><span class="sxs-lookup"><span data-stu-id="cb32b-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="cb32b-108">**[Registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="cb32b-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="cb32b-109">Puede configurar registros de diagnóstico para obtener una vista más completa de todo lo que ocurre con un trabajo.</span><span class="sxs-lookup"><span data-stu-id="cb32b-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="cb32b-110">Las actividades de la portada de registros de diagnóstico de tiempo de hello trabajo Hola se crea hasta que se elimina el trabajo de hello, incluidas las actualizaciones y las actividades que se producen mientras se ejecuta el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cb32b-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="cb32b-111">Activación de los registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="cb32b-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="cb32b-112">Los registros de diagnóstico están inhabilitados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cb32b-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="cb32b-113">registros de diagnóstico de tooenable:</span><span class="sxs-lookup"><span data-stu-id="cb32b-113">tooenable diagnostic logs:</span></span>

1.  <span data-ttu-id="cb32b-114">Hola [portal de Azure](https://portal.azure.com), en **supervisión + administración**, haga clic en **registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="cb32b-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Registros de toodiagnostic de navegación de hoja](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="cb32b-116">Haga clic en recurso de Hola que desee toomonitor.</span><span class="sxs-lookup"><span data-stu-id="cb32b-116">Click hello resource you want toomonitor.</span></span>

3.  <span data-ttu-id="cb32b-117">Haga clic en **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="cb32b-117">Click **Turn on diagnostics**.</span></span>

    ![Activación de los registros de diagnósticos](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="cb32b-119">En **Estado**, haga clic en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="cb32b-119">For **Status**, click **On**.</span></span>

    ![Cambiar estado de Hola de registros de diagnóstico](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="cb32b-121">Destino de archivo de Hola de conjunto que desea; Por ejemplo, una cuenta de almacenamiento, un concentrador de eventos o análisis de registros de Azure.</span><span class="sxs-lookup"><span data-stu-id="cb32b-121">Set hello archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="cb32b-122">Guardar la configuración de diagnósticos de hello nueva.</span><span class="sxs-lookup"><span data-stu-id="cb32b-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="cb32b-123">La nueva configuración surte efecto en unos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="cb32b-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="cb32b-124">Después de eso, los registros aparecen en el destino de archivo hello configurado, en hello **registros de diagnóstico** hoja.</span><span class="sxs-lookup"><span data-stu-id="cb32b-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="cb32b-125">Para obtener más información acerca de cómo configurar diagnósticos, vea hello [información general de los registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="cb32b-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="cb32b-126">Categorías de registros de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="cb32b-126">Diagnostic logs categories</span></span>
<span data-ttu-id="cb32b-127">Event Hubs captura registros de diagnósticos de dos categorías:</span><span class="sxs-lookup"><span data-stu-id="cb32b-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="cb32b-128">**ArchiveLogs**: registros relacionados con archivos de bases de datos centrales de tooEvent, específicamente, registra los errores de tooarchive relacionados.</span><span class="sxs-lookup"><span data-stu-id="cb32b-128">**ArchiveLogs**: logs related tooEvent Hubs archives, specifically, logs related tooarchive errors.</span></span>
* <span data-ttu-id="cb32b-129">**OperationalLogs**: información sobre lo que sucede durante las operaciones de los centros de eventos, en concreto, Hola tipo de operación, incluida la creación de concentrador de eventos, recursos que usa y Hola estado de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="cb32b-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, hello operation type, including event hub creation, resources used, and hello status of hello operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="cb32b-130">Esquema de registros de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="cb32b-130">Diagnostic logs schema</span></span>
<span data-ttu-id="cb32b-131">Todos los registros se almacenan en el formato de notación de objetos JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="cb32b-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="cb32b-132">Cada entrada tiene campos de cadena que usan formato Hola descrito en hello las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="cb32b-132">Each entry has string fields that use hello format described in hello following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="cb32b-133">Esquema de registros de archivo</span><span class="sxs-lookup"><span data-stu-id="cb32b-133">Archive logs schema</span></span>

<span data-ttu-id="cb32b-134">Las cadenas JSON de registro de archivo incluyen elementos enumerados en hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="cb32b-134">Archive log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="cb32b-135">Nombre</span><span class="sxs-lookup"><span data-stu-id="cb32b-135">Name</span></span> | <span data-ttu-id="cb32b-136">Descripción</span><span class="sxs-lookup"><span data-stu-id="cb32b-136">Description</span></span>
------- | -------
<span data-ttu-id="cb32b-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="cb32b-137">TaskName</span></span> | <span data-ttu-id="cb32b-138">Descripción de tarea de Hola que dieron error.</span><span class="sxs-lookup"><span data-stu-id="cb32b-138">Description of hello task that failed.</span></span>
<span data-ttu-id="cb32b-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="cb32b-139">ActivityId</span></span> | <span data-ttu-id="cb32b-140">El identificador interno, usado con fines de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="cb32b-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="cb32b-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="cb32b-141">trackingId</span></span> | <span data-ttu-id="cb32b-142">El identificador interno, usado con fines de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="cb32b-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="cb32b-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="cb32b-143">resourceId</span></span> | <span data-ttu-id="cb32b-144">Identificador de recursos de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb32b-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="cb32b-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="cb32b-145">eventHub</span></span> | <span data-ttu-id="cb32b-146">Nombre completo del centro de eventos (incluye el nombre del espacio de nombres).</span><span class="sxs-lookup"><span data-stu-id="cb32b-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="cb32b-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="cb32b-147">partitionId</span></span> | <span data-ttu-id="cb32b-148">La partición del centro de eventos en la que se escribe.</span><span class="sxs-lookup"><span data-stu-id="cb32b-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="cb32b-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="cb32b-149">archiveStep</span></span> | <span data-ttu-id="cb32b-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="cb32b-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="cb32b-151">startTime</span><span class="sxs-lookup"><span data-stu-id="cb32b-151">startTime</span></span> | <span data-ttu-id="cb32b-152">Hora de inicio del error.</span><span class="sxs-lookup"><span data-stu-id="cb32b-152">Failure start time.</span></span>
<span data-ttu-id="cb32b-153">errores</span><span class="sxs-lookup"><span data-stu-id="cb32b-153">failures</span></span> | <span data-ttu-id="cb32b-154">Número de veces que se ha producido el error.</span><span class="sxs-lookup"><span data-stu-id="cb32b-154">Number of times failure occurred.</span></span>
<span data-ttu-id="cb32b-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="cb32b-155">durationInSeconds</span></span> | <span data-ttu-id="cb32b-156">La duración del error.</span><span class="sxs-lookup"><span data-stu-id="cb32b-156">Duration of failure.</span></span>
<span data-ttu-id="cb32b-157">Mensaje</span><span class="sxs-lookup"><span data-stu-id="cb32b-157">message</span></span> | <span data-ttu-id="cb32b-158">Mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="cb32b-158">Error message.</span></span>
<span data-ttu-id="cb32b-159">categoría</span><span class="sxs-lookup"><span data-stu-id="cb32b-159">category</span></span> | <span data-ttu-id="cb32b-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="cb32b-160">ArchiveLogs</span></span>

<span data-ttu-id="cb32b-161">Hello código siguiente es un ejemplo de un cadena JSON de registro de archivo:</span><span class="sxs-lookup"><span data-stu-id="cb32b-161">hello following code is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="cb32b-162">Esquema de registros operativos</span><span class="sxs-lookup"><span data-stu-id="cb32b-162">Operational logs schema</span></span>

<span data-ttu-id="cb32b-163">Las cadenas JSON de registro operativo incluyen elementos enumerados en hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="cb32b-163">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="cb32b-164">Nombre</span><span class="sxs-lookup"><span data-stu-id="cb32b-164">Name</span></span> | <span data-ttu-id="cb32b-165">Descripción</span><span class="sxs-lookup"><span data-stu-id="cb32b-165">Description</span></span>
------- | -------
<span data-ttu-id="cb32b-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="cb32b-166">ActivityId</span></span> | <span data-ttu-id="cb32b-167">Identificador interno, utiliza tootrack propósito.</span><span class="sxs-lookup"><span data-stu-id="cb32b-167">Internal ID, used tootrack purpose.</span></span>
<span data-ttu-id="cb32b-168">EventName</span><span class="sxs-lookup"><span data-stu-id="cb32b-168">EventName</span></span> | <span data-ttu-id="cb32b-169">Nombre de la operación.</span><span class="sxs-lookup"><span data-stu-id="cb32b-169">Operation name.</span></span>  
<span data-ttu-id="cb32b-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="cb32b-170">resourceId</span></span> | <span data-ttu-id="cb32b-171">Identificador de recursos de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb32b-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="cb32b-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="cb32b-172">SubscriptionId</span></span> | <span data-ttu-id="cb32b-173">Id. de suscripción.</span><span class="sxs-lookup"><span data-stu-id="cb32b-173">Subscription ID.</span></span>
<span data-ttu-id="cb32b-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="cb32b-174">EventTimeString</span></span> | <span data-ttu-id="cb32b-175">Hora de la operación.</span><span class="sxs-lookup"><span data-stu-id="cb32b-175">Operation time.</span></span>
<span data-ttu-id="cb32b-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="cb32b-176">EventProperties</span></span> | <span data-ttu-id="cb32b-177">Propiedades de la operación.</span><span class="sxs-lookup"><span data-stu-id="cb32b-177">Operation properties.</span></span>
<span data-ttu-id="cb32b-178">Estado</span><span class="sxs-lookup"><span data-stu-id="cb32b-178">Status</span></span> | <span data-ttu-id="cb32b-179">Estado de la operación.</span><span class="sxs-lookup"><span data-stu-id="cb32b-179">Operation status.</span></span>
<span data-ttu-id="cb32b-180">Autor de llamada</span><span class="sxs-lookup"><span data-stu-id="cb32b-180">Caller</span></span> | <span data-ttu-id="cb32b-181">Autor de la llamada de la operación (Azure Portal o Management Client).</span><span class="sxs-lookup"><span data-stu-id="cb32b-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="cb32b-182">categoría</span><span class="sxs-lookup"><span data-stu-id="cb32b-182">category</span></span> | <span data-ttu-id="cb32b-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="cb32b-183">OperationalLogs</span></span>

<span data-ttu-id="cb32b-184">Hello código siguiente es un ejemplo de una cadena JSON de registro operativo:</span><span class="sxs-lookup"><span data-stu-id="cb32b-184">hello following code is an example of an operational log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="cb32b-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cb32b-185">Next steps</span></span>
* [<span data-ttu-id="cb32b-186">Introducción tooEvent centros</span><span class="sxs-lookup"><span data-stu-id="cb32b-186">Introduction tooEvent Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="cb32b-187">Introducción a la API de centros de eventos</span><span class="sxs-lookup"><span data-stu-id="cb32b-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="cb32b-188">Introducción a Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cb32b-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
