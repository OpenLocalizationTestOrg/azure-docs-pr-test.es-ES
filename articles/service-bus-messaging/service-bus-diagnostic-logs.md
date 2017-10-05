---
title: "Registros de diagnóstico de Azure Service Bus | Microsoft Docs"
description: "Aprenda cómo configurar registros de diagnóstico para Service Bus en Azure."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: 72e18444c83b84c5191a0aab3dc6983517167dd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="e2f2a-103">Registros de diagnóstico de Service Bus</span><span class="sxs-lookup"><span data-stu-id="e2f2a-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="e2f2a-104">Puede ver dos tipos de registros para Azure Service Bus:</span><span class="sxs-lookup"><span data-stu-id="e2f2a-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="e2f2a-105">**[Registros de actividad](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="e2f2a-106">Estos registros contienen información relativa a las operaciones realizadas en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="e2f2a-107">Los registros están siempre habilitados.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-107">The logs are always enabled.</span></span>
* <span data-ttu-id="e2f2a-108">**[Registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="e2f2a-109">Puede configurar registros de diagnóstico para obtener información más completa sobre todo lo que ocurre en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="e2f2a-110">Los registros de diagnóstico incluyen la actividad desde el momento en que se crea el trabajo hasta que este se elimina, incluidas las actualizaciones y actividades que se realizan durante la ejecución del trabajo.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="e2f2a-111">Activación de los registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e2f2a-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="e2f2a-112">Los registros de diagnóstico están inhabilitados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="e2f2a-113">Para habilitarlos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e2f2a-113">To enable diagnostic logs, perform the following steps:</span></span>

1.  <span data-ttu-id="e2f2a-114">En [Azure Portal](https://portal.azure.com), en **Supervisión y administración**, haga clic en **Registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![navegación por la hoja a los registros de diagnósticos](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="e2f2a-116">Haga clic en el recurso que quiere supervisar.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-116">Click the resource you want to monitor.</span></span>  

3.  <span data-ttu-id="e2f2a-117">Haga clic en **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-117">Click **Turn on diagnostics**.</span></span>

    ![activar los registros de diagnósticos](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="e2f2a-119">En **Estado**, haga clic en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-119">For **Status**, click **On**.</span></span>

    ![cambiar el estado de los registros de diagnósticos](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="e2f2a-121">Establezca el destino de archivo que quiera; por ejemplo, una cuenta de almacenamiento, un centro de eventos o Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-121">Set the archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="e2f2a-122">Guarde la nueva configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="e2f2a-123">La nueva configuración surte efecto en unos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="e2f2a-124">Después, los registros aparecen en el destino de archivo configurado, en la hoja **Registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="e2f2a-125">Para obtener más información sobre el diagnóstico de configuraciones, consulte la [información general sobre los registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e2f2a-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="e2f2a-126">Esquema de registros de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="e2f2a-126">Diagnostic logs schema</span></span>

<span data-ttu-id="e2f2a-127">Todos los registros se almacenan en el formato de notación de objetos JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="e2f2a-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="e2f2a-128">Cada entrada tiene campos de cadena que usan el formato descrito en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-128">Each entry has string fields that use the format described in the following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="e2f2a-129">Esquema de registros operativos</span><span class="sxs-lookup"><span data-stu-id="e2f2a-129">Operational logs schema</span></span>

<span data-ttu-id="e2f2a-130">Los registros de la categoría **OperationalLogs** capturan lo que sucede durante las operaciones de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-130">Logs in the **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="e2f2a-131">En concreto, estos registros capturan el tipo de operación, incluida la creación de colas, los recursos usados y el estado de la operación.</span><span class="sxs-lookup"><span data-stu-id="e2f2a-131">Specifically, these logs capture the operation type, including queue creation, resources used, and the status of the operation.</span></span>

<span data-ttu-id="e2f2a-132">Las cadenas JSON de registros operativos incluyen elementos enumerados en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2f2a-132">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="e2f2a-133">Nombre</span><span class="sxs-lookup"><span data-stu-id="e2f2a-133">Name</span></span> | <span data-ttu-id="e2f2a-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="e2f2a-134">Description</span></span>
------- | -------
<span data-ttu-id="e2f2a-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="e2f2a-135">ActivityId</span></span> | <span data-ttu-id="e2f2a-136">El identificador interno, usado con fines de seguimiento</span><span class="sxs-lookup"><span data-stu-id="e2f2a-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="e2f2a-137">EventName</span><span class="sxs-lookup"><span data-stu-id="e2f2a-137">EventName</span></span> | <span data-ttu-id="e2f2a-138">Nombre de la operación</span><span class="sxs-lookup"><span data-stu-id="e2f2a-138">Operation name</span></span>           
<span data-ttu-id="e2f2a-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="e2f2a-139">resourceId</span></span> | <span data-ttu-id="e2f2a-140">El identificador de recursos de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e2f2a-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="e2f2a-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="e2f2a-141">SubscriptionId</span></span> | <span data-ttu-id="e2f2a-142">Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="e2f2a-142">Subscription ID</span></span>
<span data-ttu-id="e2f2a-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="e2f2a-143">EventTimeString</span></span> | <span data-ttu-id="e2f2a-144">Hora de la operación</span><span class="sxs-lookup"><span data-stu-id="e2f2a-144">Operation time</span></span>
<span data-ttu-id="e2f2a-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="e2f2a-145">EventProperties</span></span> | <span data-ttu-id="e2f2a-146">Propiedades de la operación</span><span class="sxs-lookup"><span data-stu-id="e2f2a-146">Operation properties</span></span>
<span data-ttu-id="e2f2a-147">Estado</span><span class="sxs-lookup"><span data-stu-id="e2f2a-147">Status</span></span> | <span data-ttu-id="e2f2a-148">Estado de la operación</span><span class="sxs-lookup"><span data-stu-id="e2f2a-148">Operation status</span></span>
<span data-ttu-id="e2f2a-149">Autor de llamada</span><span class="sxs-lookup"><span data-stu-id="e2f2a-149">Caller</span></span> | <span data-ttu-id="e2f2a-150">Autor de la llamada de la operación (Azure Portal o Management Client)</span><span class="sxs-lookup"><span data-stu-id="e2f2a-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="e2f2a-151">categoría</span><span class="sxs-lookup"><span data-stu-id="e2f2a-151">category</span></span> | <span data-ttu-id="e2f2a-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="e2f2a-152">OperationalLogs</span></span>

<span data-ttu-id="e2f2a-153">Este es un ejemplo de una cadena JSON de registro operativo:</span><span class="sxs-lookup"><span data-stu-id="e2f2a-153">Here's an example of an operational log JSON string:</span></span>

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="e2f2a-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2f2a-154">Next steps</span></span>

<span data-ttu-id="e2f2a-155">Visite los siguientes vínculos para más información acerca de Service Bus:</span><span class="sxs-lookup"><span data-stu-id="e2f2a-155">Visit the following links to learn more about Service Bus:</span></span>

* [<span data-ttu-id="e2f2a-156">Introducción a Service Bus</span><span class="sxs-lookup"><span data-stu-id="e2f2a-156">Introduction to Service Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="e2f2a-157">Introducción a Service Bus</span><span class="sxs-lookup"><span data-stu-id="e2f2a-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
