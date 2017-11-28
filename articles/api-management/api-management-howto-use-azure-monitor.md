---
title: "aaaMonitor administración de API con el Monitor de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomonitor administración de API de Azure service mediante el Monitor de Azure."
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
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="68763-103">Supervisión de API Management con Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="68763-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="68763-104">Azure Monitor es un servicio de Azure que proporciona un único origen para la supervisión de todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="68763-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="68763-105">Con el Monitor de Azure, puede visualizar, consultar, enrutar, archivar y realizar acciones en las métricas de Hola y registros procedentes de recursos de Azure como la API de administración.</span><span class="sxs-lookup"><span data-stu-id="68763-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on hello metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="68763-106">Hola siguiendo el vídeo muestra cómo toomonitor administración de API con el Monitor de Azure.</span><span class="sxs-lookup"><span data-stu-id="68763-106">hello following video shows how toomonitor API Management using Azure Monitor.</span></span> <span data-ttu-id="68763-107">Para más información acerca de Azure Monitor, consulte [Introducción a Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="68763-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="68763-108">Métricas</span><span class="sxs-lookup"><span data-stu-id="68763-108">Metrics</span></span>
<span data-ttu-id="68763-109">Administración de API actualmente emite cinco métricas y tenemos previsto tooadd más en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="68763-109">API Management currently emits five metrics and we plan tooadd more in hello future.</span></span> <span data-ttu-id="68763-110">Estas métricas se emiten cada minuto, lo que le ofrece visibilidad en tiempo real en estado de Hola y el estado de sus API casi.</span><span class="sxs-lookup"><span data-stu-id="68763-110">These metrics are emitted every minute, giving you near real-time visibility into hello state and health of your APIs.</span></span> <span data-ttu-id="68763-111">Aquí te mostramos un resumen de las métricas de hello:</span><span class="sxs-lookup"><span data-stu-id="68763-111">Following is a summary of hello metrics:</span></span>
* <span data-ttu-id="68763-112">Nº total de puerta de enlace solicitudes: número de Hola de API de solicitudes en el período de Hola.</span><span class="sxs-lookup"><span data-stu-id="68763-112">Total Gateway Requests: hello number of API requests in hello period.</span></span> 
* <span data-ttu-id="68763-113">Solicitudes correctas de puerta de enlace: número de Hola de solicitudes de API que recibió correctamente códigos de respuesta HTTP como 304, 307 y nada más pequeño que 301 (por ejemplo, 200).</span><span class="sxs-lookup"><span data-stu-id="68763-113">Successful Gateway Requests: hello number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="68763-114">Puerta de enlace solicitudes con error: el número de Hola de solicitudes de API que recibió erróneos códigos de respuesta HTTP como 400 y cualquier valor mayor que 500.</span><span class="sxs-lookup"><span data-stu-id="68763-114">Failed Gateway Requests: hello number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="68763-115">Solicitudes no autorizadas de puerta de enlace: número de Hola de solicitudes de API que reciben los códigos de respuesta HTTP incluidos 401 y 403, 429.</span><span class="sxs-lookup"><span data-stu-id="68763-115">Unauthorized Gateway Requests: hello number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="68763-116">Otras solicitudes de puerta de enlace: número de Hola de solicitudes de API que reciben los códigos de respuesta HTTP que no pertenecen tooany de hello anteriores categorías (por ejemplo, 418).</span><span class="sxs-lookup"><span data-stu-id="68763-116">Other Gateway Requests: hello number of API requests that received HTTP response codes that do not belong tooany of hello preceding categories (for example, 418).</span></span>

<span data-ttu-id="68763-117">Puede acceder a métricas en el servicio API Management o a las métricas de todos los recursos de Azure en Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="68763-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="68763-118">métricas de tooview en el servicio de administración de API:</span><span class="sxs-lookup"><span data-stu-id="68763-118">tooview metrics in your API Management service:</span></span>
1. <span data-ttu-id="68763-119">Hola abrir portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="68763-119">Open hello Azure portal.</span></span>
2. <span data-ttu-id="68763-120">Servicio de administración de API de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="68763-120">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="68763-121">Haga clic en **Métricas**.</span><span class="sxs-lookup"><span data-stu-id="68763-121">Click **Metrics**.</span></span>

![Hoja Métricas][metrics-blade]

<span data-ttu-id="68763-123">Para obtener más información acerca de cómo toouse métricas, vea [información general de las métricas].</span><span class="sxs-lookup"><span data-stu-id="68763-123">For more information about how toouse Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="68763-124">Registros de actividad</span><span class="sxs-lookup"><span data-stu-id="68763-124">Activity Logs</span></span>
<span data-ttu-id="68763-125">Registros de actividad proporcionan una visión general de las operaciones de Hola que se realizaron en los servicios de administración de API.</span><span class="sxs-lookup"><span data-stu-id="68763-125">Activity logs provide insight into hello operations that were performed on your API Management services.</span></span> <span data-ttu-id="68763-126">Antes se los conocía como "registros de auditoría" o "registros operativos".</span><span class="sxs-lookup"><span data-stu-id="68763-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="68763-127">Utilizar registros de actividad, puede determinar Hola "qué, quién y cuándo" para las operaciones (PUT, POST, DELETE) realizadas en los servicios de administración de API de escritura.</span><span class="sxs-lookup"><span data-stu-id="68763-127">Using activity logs, you can determine hello "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="68763-128">Registros de actividad no incluyen las operaciones de lectura (GET) o las operaciones realizadas en Hola clásico Portal para desarrolladores o usar Hola original de las API de administración.</span><span class="sxs-lookup"><span data-stu-id="68763-128">Activity logs do not include read (GET) operations or operations performed in hello classic Publisher Portal or using hello original Management APIs.</span></span>

<span data-ttu-id="68763-129">Puede acceder a registros de actividad en el servicio API Management o a los registros de todos los recursos de Azure en Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="68763-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="68763-130">actividad de tooview se registra en el servicio de administración de API:</span><span class="sxs-lookup"><span data-stu-id="68763-130">tooview activity logs in your API Management service:</span></span>
1. <span data-ttu-id="68763-131">Hola abrir portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="68763-131">Open hello Azure portal.</span></span>
2. <span data-ttu-id="68763-132">Servicio de administración de API de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="68763-132">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="68763-133">Haga clic en **Registro de actividad**.</span><span class="sxs-lookup"><span data-stu-id="68763-133">Click **Activity log**.</span></span>

![Hoja Registro de actividad][activity-logs-blade]

<span data-ttu-id="68763-135">Para obtener más información acerca de cómo toouse métricas, vea [información general de los registros de actividad].</span><span class="sxs-lookup"><span data-stu-id="68763-135">For more information about how toouse Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="68763-136">Alertas</span><span class="sxs-lookup"><span data-stu-id="68763-136">Alerts</span></span>
<span data-ttu-id="68763-137">Puede configurar alertas de tooreceive basadas en métricas y registros de actividades.</span><span class="sxs-lookup"><span data-stu-id="68763-137">You can configure tooreceive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="68763-138">Monitor de Azure permite tooconfigure una alerta toodo hello las siguientes cuando se desencadena:</span><span class="sxs-lookup"><span data-stu-id="68763-138">Azure Monitor allows you tooconfigure an alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="68763-139">Enviar una notificación por correo electrónico</span><span class="sxs-lookup"><span data-stu-id="68763-139">Send an email notification</span></span>
* <span data-ttu-id="68763-140">Llamar a un webhook</span><span class="sxs-lookup"><span data-stu-id="68763-140">Call a webhook</span></span>
* <span data-ttu-id="68763-141">Invocar una aplicación lógica de Azure</span><span class="sxs-lookup"><span data-stu-id="68763-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="68763-142">Puede configurar reglas de alerta en el servicio API Management o en Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="68763-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="68763-143">tooconfigure en administración de API:</span><span class="sxs-lookup"><span data-stu-id="68763-143">tooconfigure them in API Management:</span></span> 
1. <span data-ttu-id="68763-144">Hola abrir portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="68763-144">Open hello Azure portal.</span></span>
2. <span data-ttu-id="68763-145">Servicio de administración de API de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="68763-145">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="68763-146">Haga clic en **Reglas de alerta**.</span><span class="sxs-lookup"><span data-stu-id="68763-146">Click **Alert rules**.</span></span>

![Hoja Reglas de alertas][alert-rules-blade]

<span data-ttu-id="68763-148">Para más información sobre el uso de alertas, consulte la [introducción a las alertas].</span><span class="sxs-lookup"><span data-stu-id="68763-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="68763-149">Registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="68763-149">Diagnostic Logs</span></span>
<span data-ttu-id="68763-150">Los registros de diagnóstico proporcionan información valiosa acerca de las operaciones y los errores que son importantes para la auditoría, así como para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="68763-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="68763-151">Los registros de diagnóstico son diferentes de los registros de actividad.</span><span class="sxs-lookup"><span data-stu-id="68763-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="68763-152">Registros de actividad proporcionan información sobre las operaciones de Hola que se realizaron en los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="68763-152">Activity logs provide insights into hello operations that were performed on your Azure resources.</span></span> <span data-ttu-id="68763-153">Los registros de diagnóstico proporcionan información detallada sobre las operaciones que el mismo recurso realiza.</span><span class="sxs-lookup"><span data-stu-id="68763-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="68763-154">Administración de API actualmente proporciona diagnósticos de registros (cada hora por lotes) sobre API individual solicitar a cada entrada de hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="68763-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having hello following structure:</span></span>

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

<span data-ttu-id="68763-155">Puede acceder a registros de diagnóstico en el servicio API Management o a los registros de todos los recursos de Azure en Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="68763-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="68763-156">tooview registros de diagnóstico en el servicio de administración de API:</span><span class="sxs-lookup"><span data-stu-id="68763-156">tooview diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="68763-157">Hola abrir portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="68763-157">Open hello Azure portal.</span></span>
2. <span data-ttu-id="68763-158">Servicio de administración de API de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="68763-158">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="68763-159">Haga clic en **Registro de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="68763-159">Click **Diagnostic log**.</span></span>

![Hoja Registros de diagnóstico][diagnostic-logs-blade]

<span data-ttu-id="68763-161">Para obtener más información acerca de cómo toouse métricas, vea [información general de registros de diagnóstico].</span><span class="sxs-lookup"><span data-stu-id="68763-161">For more information about how toouse Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="68763-162">siguiente paso</span><span class="sxs-lookup"><span data-stu-id="68763-162">Next Step</span></span>

* <span data-ttu-id="68763-163">[Introducción a Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="68763-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="68763-164">[información general de las métricas]</span><span class="sxs-lookup"><span data-stu-id="68763-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="68763-165">[información general de los registros de actividad]</span><span class="sxs-lookup"><span data-stu-id="68763-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="68763-166">[información general de registros de diagnóstico]</span><span class="sxs-lookup"><span data-stu-id="68763-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="68763-167">[introducción a las alertas]</span><span class="sxs-lookup"><span data-stu-id="68763-167">[Overview of Alerts]</span></span>

[Introducción a Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[información general de las métricas]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[información general de los registros de actividad]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[información general de registros de diagnóstico]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[introducción a las alertas]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
