---
title: "Supervisión de API Management con Azure Monitor | Microsoft Docs"
description: Aprenda a supervisar el servicio Azure API Management con Azure Monitor.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 0f64947755c79739bb6f15325929bd074cfd7210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="0fbdb-103">Supervisión de API Management con Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="0fbdb-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="0fbdb-104">Azure Monitor es un servicio de Azure que proporciona un único origen para la supervisión de todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="0fbdb-105">Con Azure Monitor, puede visualizar, consultar, redirigir y archivar las métricas y los registros procedentes de recursos de Azure como API Management, así como tomar medidas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="0fbdb-106">En el vídeo siguiente se muestra cómo supervisar API Management con Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="0fbdb-107">Para más información acerca de Azure Monitor, consulte [Introducción a Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="0fbdb-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="0fbdb-108">Métricas</span><span class="sxs-lookup"><span data-stu-id="0fbdb-108">Metrics</span></span>
<span data-ttu-id="0fbdb-109">Actualmente, API Management emite cinco métricas y está previsto agregar más en el futuro.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="0fbdb-110">Estas métricas se emiten cada minuto, lo que le ofrece visibilidad casi en tiempo real sobre el estado y el mantenimiento de las API.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="0fbdb-111">A continuación, se presenta un resumen de las métricas:</span><span class="sxs-lookup"><span data-stu-id="0fbdb-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="0fbdb-112">Solicitudes de puerta de enlace en total: el número de solicitudes API en el período.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="0fbdb-113">Solicitudes de puerta de enlace correctas: el número de solicitudes API que recibieron correctamente códigos de respuesta HTTP, como 304, 307 y los menores de 301 (por ejemplo, 200).</span><span class="sxs-lookup"><span data-stu-id="0fbdb-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="0fbdb-114">Solicitudes de puerta de enlace con error: el número de solicitudes API que recibieron códigos de respuesta HTTP erróneos, como 400 y cualquiera mayor que 500.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="0fbdb-115">Solicitudes de puerta de enlace no autorizadas: el número de solicitudes API que recibieron códigos de respuesta HTTP, incluidos 401, 403 y 429.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="0fbdb-116">Otras solicitudes de puerta de enlace: el número de solicitudes API que recibieron códigos de respuesta HTTP que no pertenecen a ninguna de las categorías anteriores (por ejemplo, 418).</span><span class="sxs-lookup"><span data-stu-id="0fbdb-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="0fbdb-117">Puede acceder a métricas en el servicio API Management o a las métricas de todos los recursos de Azure en Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="0fbdb-118">Para ver métricas en el servicio API Management:</span><span class="sxs-lookup"><span data-stu-id="0fbdb-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="0fbdb-119">Abra Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="0fbdb-120">Vaya al servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="0fbdb-121">Haga clic en **Métricas**.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-121">Click **Metrics**.</span></span>

![Hoja Métricas][metrics-blade]

<span data-ttu-id="0fbdb-123">Para más información sobre cómo usar las métricas, consulte [Información general sobre las métricas].</span><span class="sxs-lookup"><span data-stu-id="0fbdb-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="0fbdb-124">Registros de actividad</span><span class="sxs-lookup"><span data-stu-id="0fbdb-124">Activity Logs</span></span>
<span data-ttu-id="0fbdb-125">Los registros de actividad proporcionan información sobre las operaciones llevadas a cabo en los servicios API Management.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="0fbdb-126">Antes se los conocía como "registros de auditoría" o "registros operativos".</span><span class="sxs-lookup"><span data-stu-id="0fbdb-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="0fbdb-127">Con los registros de actividades, puede determinar los interrogantes “qué, quién y cuándo” de las operaciones de escritura (PUT, POST, DELETE) llevadas a cabo en los servicios API Management.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="0fbdb-128">Los registros de actividad no incluyen las operaciones de lectura (GET) ni las realizadas en el portal para editores clásico o mediante las API de administración originales.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="0fbdb-129">Puede acceder a registros de actividad en el servicio API Management o a los registros de todos los recursos de Azure en Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="0fbdb-130">Para ver registros de actividad en el servicio API Management:</span><span class="sxs-lookup"><span data-stu-id="0fbdb-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="0fbdb-131">Abra Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="0fbdb-132">Vaya al servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="0fbdb-133">Haga clic en **Registro de actividad**.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-133">Click **Activity log**.</span></span>

![Hoja Registro de actividad][activity-logs-blade]

<span data-ttu-id="0fbdb-135">Para más información sobre cómo usar los registros de actividad, consulte [Información general sobre el registro de actividad].</span><span class="sxs-lookup"><span data-stu-id="0fbdb-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="0fbdb-136">Alertas</span><span class="sxs-lookup"><span data-stu-id="0fbdb-136">Alerts</span></span>
<span data-ttu-id="0fbdb-137">Puede configurar la recepción de alertas en función de métricas y registros de actividad.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="0fbdb-138">Azure Monitor permite configurar una alerta que haga lo siguiente cuando se desencadena:</span><span class="sxs-lookup"><span data-stu-id="0fbdb-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="0fbdb-139">Enviar una notificación por correo electrónico</span><span class="sxs-lookup"><span data-stu-id="0fbdb-139">Send an email notification</span></span>
* <span data-ttu-id="0fbdb-140">Llamar a un webhook</span><span class="sxs-lookup"><span data-stu-id="0fbdb-140">Call a webhook</span></span>
* <span data-ttu-id="0fbdb-141">Invocar una aplicación lógica de Azure</span><span class="sxs-lookup"><span data-stu-id="0fbdb-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="0fbdb-142">Puede configurar reglas de alerta en el servicio API Management o en Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="0fbdb-143">Para configurarlas en API Management:</span><span class="sxs-lookup"><span data-stu-id="0fbdb-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="0fbdb-144">Abra Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="0fbdb-145">Vaya al servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="0fbdb-146">Haga clic en **Reglas de alerta**.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-146">Click **Alert rules**.</span></span>

![Hoja Reglas de alertas][alert-rules-blade]

<span data-ttu-id="0fbdb-148">Para más información sobre el uso de alertas, consulte la [introducción a las alertas].</span><span class="sxs-lookup"><span data-stu-id="0fbdb-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="0fbdb-149">Registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="0fbdb-149">Diagnostic Logs</span></span>
<span data-ttu-id="0fbdb-150">Los registros de diagnóstico proporcionan información valiosa acerca de las operaciones y los errores que son importantes para la auditoría, así como para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="0fbdb-151">Los registros de diagnóstico son diferentes de los registros de actividad.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="0fbdb-152">Los registros de actividad proporcionan información sobre las operaciones llevadas a cabo en los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="0fbdb-153">Los registros de diagnóstico proporcionan información detallada sobre las operaciones que el mismo recurso realiza.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="0fbdb-154">Actualmente, API Management proporciona registros de diagnóstico (cada hora por lotes) sobre solicitudes API individuales con cada entrada que tenga la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fbdb-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="0fbdb-155">Puede acceder a registros de diagnóstico en el servicio API Management o a los registros de todos los recursos de Azure en Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="0fbdb-156">Para ver registros de diagnóstico en el servicio API Management:</span><span class="sxs-lookup"><span data-stu-id="0fbdb-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="0fbdb-157">Abra Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="0fbdb-158">Vaya al servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="0fbdb-159">Haga clic en **Registro de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="0fbdb-159">Click **Diagnostic log**.</span></span>

![Hoja Registros de diagnóstico][diagnostic-logs-blade]

<span data-ttu-id="0fbdb-161">Para más información sobre cómo usar los registros de diagnóstico, consulte la [introducción a los registros de diagnóstico].</span><span class="sxs-lookup"><span data-stu-id="0fbdb-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="0fbdb-162">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="0fbdb-162">Next Step</span></span>

* <span data-ttu-id="0fbdb-163">[Introducción a Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="0fbdb-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="0fbdb-164">[Información general sobre las métricas]</span><span class="sxs-lookup"><span data-stu-id="0fbdb-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="0fbdb-165">[Información general sobre el registro de actividad]</span><span class="sxs-lookup"><span data-stu-id="0fbdb-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="0fbdb-166">[introducción a los registros de diagnóstico]</span><span class="sxs-lookup"><span data-stu-id="0fbdb-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="0fbdb-167">[introducción a las alertas]</span><span class="sxs-lookup"><span data-stu-id="0fbdb-167">[Overview of Alerts]</span></span>

<span data-ttu-id="0fbdb-168">[Introducción a Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span><span class="sxs-lookup"><span data-stu-id="0fbdb-168">[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span></span>
<span data-ttu-id="0fbdb-169">[Información general sobre las métricas]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span><span class="sxs-lookup"><span data-stu-id="0fbdb-169">[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span></span>
<span data-ttu-id="0fbdb-170">[Información general sobre el registro de actividad]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span><span class="sxs-lookup"><span data-stu-id="0fbdb-170">[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span></span>
<span data-ttu-id="0fbdb-171">[introducción a los registros de diagnóstico]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span><span class="sxs-lookup"><span data-stu-id="0fbdb-171">[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span></span>
<span data-ttu-id="0fbdb-172">[introducción a las alertas]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span><span class="sxs-lookup"><span data-stu-id="0fbdb-172">[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span></span>



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
