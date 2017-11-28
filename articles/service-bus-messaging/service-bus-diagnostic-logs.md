---
title: "registros de diagnóstico de Bus de servicio de aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset los registros de diagnóstico de Service Bus en Azure."
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
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="a3e3b-103">Registros de diagnóstico de Service Bus</span><span class="sxs-lookup"><span data-stu-id="a3e3b-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="a3e3b-104">Puede ver dos tipos de registros para Azure Service Bus:</span><span class="sxs-lookup"><span data-stu-id="a3e3b-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="a3e3b-105">**[Registros de actividad](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="a3e3b-106">Estos registros contienen información relativa a las operaciones realizadas en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="a3e3b-107">registros de Hello siempre están habilitados.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="a3e3b-108">**[Registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="a3e3b-109">Puede configurar registros de diagnóstico para obtener información más completa sobre todo lo que ocurre en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="a3e3b-110">Las actividades de la portada de registros de diagnóstico de tiempo de hello trabajo Hola se crea hasta que se elimina el trabajo de hello, incluidas las actualizaciones y las actividades que se producen mientras se ejecuta el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="a3e3b-111">Activación de los registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="a3e3b-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="a3e3b-112">Los registros de diagnóstico están inhabilitados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="a3e3b-113">registros de diagnóstico de tooenable, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a3e3b-113">tooenable diagnostic logs, perform hello following steps:</span></span>

1.  <span data-ttu-id="a3e3b-114">Hola [portal de Azure](https://portal.azure.com), en **supervisión + administración**, haga clic en **registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Registros de toodiagnostic de navegación de hoja](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="a3e3b-116">Haga clic en recurso de Hola que desee toomonitor.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-116">Click hello resource you want toomonitor.</span></span>  

3.  <span data-ttu-id="a3e3b-117">Haga clic en **Activar diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-117">Click **Turn on diagnostics**.</span></span>

    ![activar los registros de diagnósticos](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="a3e3b-119">En **Estado**, haga clic en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-119">For **Status**, click **On**.</span></span>

    ![cambiar el estado de los registros de diagnósticos](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="a3e3b-121">Destino de archivo de Hola de conjunto que desea; Por ejemplo, una cuenta de almacenamiento, un concentrador de eventos o análisis de registros de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-121">Set hello archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="a3e3b-122">Guardar la configuración de diagnósticos de hello nueva.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="a3e3b-123">La nueva configuración surte efecto en unos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="a3e3b-124">Después de eso, los registros aparecen en el destino de archivo hello configurado, en hello **registros de diagnóstico** hoja.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="a3e3b-125">Para obtener más información acerca de cómo configurar diagnósticos, vea hello [información general de los registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a3e3b-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="a3e3b-126">Esquema de registros de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="a3e3b-126">Diagnostic logs schema</span></span>

<span data-ttu-id="a3e3b-127">Todos los registros se almacenan en el formato de notación de objetos JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="a3e3b-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="a3e3b-128">Cada entrada tiene campos de cadena que utilizan el formato de hello descrito en hello pasos de la sección.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-128">Each entry has string fields that use hello format described in hello following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="a3e3b-129">Esquema de registros operativos</span><span class="sxs-lookup"><span data-stu-id="a3e3b-129">Operational logs schema</span></span>

<span data-ttu-id="a3e3b-130">Inicia sesión en hello **OperationalLogs** categoría capturar lo que sucede durante las operaciones de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-130">Logs in hello **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="a3e3b-131">En concreto, estos registros capturar el tipo de operación de hello, incluida la creación de cola, los recursos que usa y Hola estado de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3e3b-131">Specifically, these logs capture hello operation type, including queue creation, resources used, and hello status of hello operation.</span></span>

<span data-ttu-id="a3e3b-132">Las cadenas JSON de registro operativo incluyen elementos enumerados en hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="a3e3b-132">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="a3e3b-133">Nombre</span><span class="sxs-lookup"><span data-stu-id="a3e3b-133">Name</span></span> | <span data-ttu-id="a3e3b-134">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3e3b-134">Description</span></span>
------- | -------
<span data-ttu-id="a3e3b-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="a3e3b-135">ActivityId</span></span> | <span data-ttu-id="a3e3b-136">El identificador interno, usado con fines de seguimiento</span><span class="sxs-lookup"><span data-stu-id="a3e3b-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="a3e3b-137">EventName</span><span class="sxs-lookup"><span data-stu-id="a3e3b-137">EventName</span></span> | <span data-ttu-id="a3e3b-138">Nombre de la operación</span><span class="sxs-lookup"><span data-stu-id="a3e3b-138">Operation name</span></span>           
<span data-ttu-id="a3e3b-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="a3e3b-139">resourceId</span></span> | <span data-ttu-id="a3e3b-140">El identificador de recursos de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a3e3b-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="a3e3b-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a3e3b-141">SubscriptionId</span></span> | <span data-ttu-id="a3e3b-142">Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="a3e3b-142">Subscription ID</span></span>
<span data-ttu-id="a3e3b-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="a3e3b-143">EventTimeString</span></span> | <span data-ttu-id="a3e3b-144">Hora de la operación</span><span class="sxs-lookup"><span data-stu-id="a3e3b-144">Operation time</span></span>
<span data-ttu-id="a3e3b-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="a3e3b-145">EventProperties</span></span> | <span data-ttu-id="a3e3b-146">Propiedades de la operación</span><span class="sxs-lookup"><span data-stu-id="a3e3b-146">Operation properties</span></span>
<span data-ttu-id="a3e3b-147">Estado</span><span class="sxs-lookup"><span data-stu-id="a3e3b-147">Status</span></span> | <span data-ttu-id="a3e3b-148">Estado de la operación</span><span class="sxs-lookup"><span data-stu-id="a3e3b-148">Operation status</span></span>
<span data-ttu-id="a3e3b-149">Autor de llamada</span><span class="sxs-lookup"><span data-stu-id="a3e3b-149">Caller</span></span> | <span data-ttu-id="a3e3b-150">Autor de la llamada de la operación (Azure Portal o Management Client)</span><span class="sxs-lookup"><span data-stu-id="a3e3b-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="a3e3b-151">categoría</span><span class="sxs-lookup"><span data-stu-id="a3e3b-151">category</span></span> | <span data-ttu-id="a3e3b-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="a3e3b-152">OperationalLogs</span></span>

<span data-ttu-id="a3e3b-153">Este es un ejemplo de una cadena JSON de registro operativo:</span><span class="sxs-lookup"><span data-stu-id="a3e3b-153">Here's an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a3e3b-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3e3b-154">Next steps</span></span>

<span data-ttu-id="a3e3b-155">Visite Hola siguiendo vínculos toolearn más acerca de Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="a3e3b-155">Visit hello following links toolearn more about Service Bus:</span></span>

* [<span data-ttu-id="a3e3b-156">Introducción tooService Bus</span><span class="sxs-lookup"><span data-stu-id="a3e3b-156">Introduction tooService Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="a3e3b-157">Introducción a Service Bus</span><span class="sxs-lookup"><span data-stu-id="a3e3b-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
