---
title: "aaaStream registros de diagnóstico de Azure tooan Namespace de concentradores de eventos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toostream diagnóstico de Azure registra el espacio de nombres de tooan centros de eventos."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a><span data-ttu-id="e4278-103">Transmitir tooan Namespace de concentradores de eventos de registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="e4278-103">Stream Azure Diagnostic Logs tooan Event Hubs Namespace</span></span>
<span data-ttu-id="e4278-104">**[Registros de diagnóstico de Azure](monitoring-overview-of-diagnostic-logs.md)**  se puede transmitir cerca de la aplicación de tooany de en tiempo real mediante la opción "Exportación tooEvent concentradores" integrada Hola Hola Portal o habilitando Hola Id. de regla de Bus de servicio en una configuración de diagnóstico a través de hello Azure PowerShell CLI de Azure o cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e4278-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time tooany application using hello built-in “Export tooEvent Hubs” option in hello Portal, or by enabling hello Service Bus Rule ID in a diagnostic setting via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="e4278-105">Qué se puede hacer con registros de diagnóstico y Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e4278-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="e4278-106">Aquí se muestran unos pocos maneras puede usar Hola capacidad de streaming para registros de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="e4278-106">Here are just a few ways you might use hello streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="e4278-107">**Secuencia de registros de sistemas de registro y telemetría de terceros too3rd** – con el tiempo, los concentradores de eventos de transmisión por secuencias se convertirá en hello mecanismo toopipe los registros de diagnóstico de SIEM toothird terceros y soluciones de análisis de registro.</span><span class="sxs-lookup"><span data-stu-id="e4278-107">**Stream logs too3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your diagnostic logs in toothird-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="e4278-108">**Ver estado del servicio de transmisión por secuencias "ruta de acceso activa" datos tooPowerBI** : uso y centros de eventos, análisis de transmisiones, Power BI, puede transformar fácilmente los datos de diagnóstico en toonear de información en tiempo real en los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4278-108">**View service health by streaming “hot path” data tooPowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in toonear real-time insights on your Azure services.</span></span> <span data-ttu-id="e4278-109">[Este artículo de documentación ofrece una excelente introducción de cómo procesar datos con análisis de transmisiones tooset los concentradores de eventos y usar Power BI como una salida de](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="e4278-109">[This documentation article gives a great overview of how tooset up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="e4278-110">Estas son algunas recomendaciones para la configuración con los registros de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="e4278-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="e4278-111">Un concentrador de eventos para una categoría de registros de diagnóstico se crea automáticamente cuando compruebe la opción de hello en el portal de Hola o habilitarlo mediante PowerShell, por lo que desee tooselect concentrador de eventos de hello en hello espacio de nombres con el nombre de hello comienza con **visión**.</span><span class="sxs-lookup"><span data-stu-id="e4278-111">An event hub for a category of diagnostic logs is created automatically when you check hello option in hello portal or enable it through PowerShell, so you want tooselect hello event hub in hello namespace with hello name that starts with **insights-**.</span></span>
  * <span data-ttu-id="e4278-112">Hola después el código SQL es un ejemplo de análisis de transmisiones de consulta que puede usar todos los datos de registro de hello tooparse en la tabla de PowerBI tooa:</span><span class="sxs-lookup"><span data-stu-id="e4278-112">hello following SQL code is a sample Stream Analytics query that you can use tooparse all hello log data in tooa PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="e4278-113">**Crear una plataforma de registro y telemetría personalizada** : si ya dispone de una plataforma de telemetría personalizada o son solo pensar en uno, Hola altamente escalable publicación / suscripción de edificio naturaleza de los centros de eventos permite tooflexibly introducir diagnóstico registros.</span><span class="sxs-lookup"><span data-stu-id="e4278-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="e4278-114">[Consulte toousing de guía de Dan Rosanova centros de eventos en una plataforma de telemetría de escala global](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="e4278-114">[See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="e4278-115">Habilitación del streaming de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e4278-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="e4278-116">Puede habilitar la transmisión por secuencias de registros de diagnóstico mediante programación, mediante el portal de hello, o utilizando hello [API de REST de Azure Monitor](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="e4278-116">You can enable streaming of diagnostic logs programmatically, via hello portal, or using hello [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="e4278-117">En cualquier caso, cree una configuración de diagnóstico en el que puede especificar un espacio de nombres de los centros de eventos y categorías de registro de hello y métricas que desee toosend en el espacio de nombres de toohello.</span><span class="sxs-lookup"><span data-stu-id="e4278-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and hello log categories and metrics you want toosend in toohello namespace.</span></span> <span data-ttu-id="e4278-118">Un concentrador de eventos se crea en el espacio de nombres de Hola para cada categoría de registro que se habilita.</span><span class="sxs-lookup"><span data-stu-id="e4278-118">An event hub is created in hello namespace for each log category you enable.</span></span> <span data-ttu-id="e4278-119">Una **categoría de registro** de diagnóstico es un tipo de registro que un recurso puede recopilar.</span><span class="sxs-lookup"><span data-stu-id="e4278-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="e4278-120">La habilitación y streaming de registros de diagnóstico desde recursos de proceso (por ejemplo, máquinas virtuales o Service Fabric) [requiere ejecutar una serie de pasos distinta](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="e4278-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="e4278-121">Hola Bus de servicio o concentradores de eventos del espacio de nombres no tiene toobe en Hola misma suscripción como recurso de hello emitir registros como usuario de Hola que configura los valores de hello tiene suscripciones de tooboth de acceso RBAC adecuadas.</span><span class="sxs-lookup"><span data-stu-id="e4278-121">hello Service Bus or Event Hubs namespace does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="e4278-122">Registros de diagnóstico de la secuencia mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="e4278-122">Stream diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="e4278-123">En el portal de hello, navegue tooAzure Monitor y haga clic en **configuración de diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="e4278-123">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Sección de supervisión de Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="e4278-125">Si lo desea Hola lista Filtrar por tipo de recurso o grupo de recursos, a continuación, haga clic en el recurso de hello para el que le gustaría tooset una configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e4278-125">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="e4278-126">Si ninguna configuración existe en el recurso de Hola que ha seleccionado, son toocreate solicitada una configuración.</span><span class="sxs-lookup"><span data-stu-id="e4278-126">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="e4278-127">Haga clic en "Activar diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="e4278-127">Click "Turn on diagnostics."</span></span>

   ![Agregar configuración de diagnóstico: sin configuración actual](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="e4278-129">Si hay una configuración existente en el recurso de hello, verá una lista de configuraciones ya configurado en este recurso.</span><span class="sxs-lookup"><span data-stu-id="e4278-129">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="e4278-130">Haga clic en "Agregar configuración de diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="e4278-130">Click "Add diagnostic setting."</span></span>

   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="e4278-132">Asigne un nombre de su configuración y casilla hello para **concentrador de eventos de flujo tooan**, a continuación, seleccione un espacio de nombres de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="e4278-132">Give your setting a name and check hello box for **Stream tooan event hub**, then select an Event Hubs namespace.</span></span>
   
   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="e4278-134">Hello espacio de nombres seleccionado será donde se crea (si se trata de la primera vez que los registros de diagnóstico de streaming) o se transmiten demasiado concentrador de eventos de hello (si ya hay recursos que están transmitiendo por secuencias ese espacio de nombres de toothis de categoría de registro), y la directiva de hello define Hola permisos que tiene el mecanismo de transmisión por secuencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4278-134">hello namespace selected will be where hello event hub is created (if this is your first time streaming diagnostic logs) or streamed too(if there are already resources that are streaming that log category toothis namespace), and hello policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="e4278-135">En la actualidad, streaming tooan concentrador de eventos requiere permisos de administración, envío y escuchar.</span><span class="sxs-lookup"><span data-stu-id="e4278-135">Today, streaming tooan event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="e4278-136">Puede crear o modificar directivas de acceso de espacio de nombres compartido centros de eventos en el portal de hello en la ficha configurar de hello para el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="e4278-136">You can create or modify Event Hubs namespace shared access policies in hello portal under hello Configure tab for your namespace.</span></span> <span data-ttu-id="e4278-137">tooupdate uno de estos valores de diagnóstico, el cliente hello debe tener permiso de ListKey de hello en la regla de autorización de los centros de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4278-137">tooupdate one of these diagnostic settings, hello client must have hello ListKey permission on hello Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="e4278-138">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e4278-138">Click **Save**.</span></span>

<span data-ttu-id="e4278-139">Transcurridos unos instantes, nueva configuración de hello aparece en la lista de valores para este recurso y registros de diagnóstico se transmiten cuenta de almacenamiento toothat tan pronto como se generan nuevos datos de evento.</span><span class="sxs-lookup"><span data-stu-id="e4278-139">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are streamed toothat storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="e4278-140">Mediante cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4278-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="e4278-141">tooenable transmisión por secuencias a través de hello [Cmdlets de PowerShell de Azure](insights-powershell-samples.md), puede usar hello `Set-AzureRmDiagnosticSetting` cmdlet con estos parámetros:</span><span class="sxs-lookup"><span data-stu-id="e4278-141">tooenable streaming via hello [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use hello `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="e4278-142">Hola Id. de regla de Bus de servicio es una cadena con este formato: `{Service Bus resource ID}/authorizationrules/{key name}`, por ejemplo, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="e4278-142">hello Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="e4278-143">Mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e4278-143">Via Azure CLI</span></span>
<span data-ttu-id="e4278-144">tooenable transmisión por secuencias a través de hello [CLI de Azure](insights-cli-samples.md), puede usar hello `insights diagnostic set` comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="e4278-144">tooenable streaming via hello [Azure CLI](insights-cli-samples.md), you can use hello `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="e4278-145">Usar hello mismo formato para el Id. de regla de Bus de servicio, como se explica para hello Cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e4278-145">Use hello same format for Service Bus Rule ID as explained for hello PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="e4278-146">¿Cómo se puede consumir datos de registro de hello de centros de eventos?</span><span class="sxs-lookup"><span data-stu-id="e4278-146">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="e4278-147">Estos son datos de salida de ejemplo de Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="e4278-147">Here is sample output data from Event Hubs:</span></span>

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| <span data-ttu-id="e4278-148">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="e4278-148">Element Name</span></span> | <span data-ttu-id="e4278-149">Description</span><span class="sxs-lookup"><span data-stu-id="e4278-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e4278-150">records</span><span class="sxs-lookup"><span data-stu-id="e4278-150">records</span></span> |<span data-ttu-id="e4278-151">Matriz de todos los eventos de registro de esta carga.</span><span class="sxs-lookup"><span data-stu-id="e4278-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="e4278-152">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="e4278-152">time</span></span> |<span data-ttu-id="e4278-153">Hora en que hello evento se produjo.</span><span class="sxs-lookup"><span data-stu-id="e4278-153">Time at which hello event occurred.</span></span> |
| <span data-ttu-id="e4278-154">categoría</span><span class="sxs-lookup"><span data-stu-id="e4278-154">category</span></span> |<span data-ttu-id="e4278-155">Categoría de registro para este evento.</span><span class="sxs-lookup"><span data-stu-id="e4278-155">Log category for this event.</span></span> |
| <span data-ttu-id="e4278-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="e4278-156">resourceId</span></span> |<span data-ttu-id="e4278-157">Id. de recurso del recurso de Hola que generó este evento.</span><span class="sxs-lookup"><span data-stu-id="e4278-157">Resource ID of hello resource that generated this event.</span></span> |
| <span data-ttu-id="e4278-158">operationName</span><span class="sxs-lookup"><span data-stu-id="e4278-158">operationName</span></span> |<span data-ttu-id="e4278-159">Nombre de operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4278-159">Name of hello operation.</span></span> |
| <span data-ttu-id="e4278-160">level</span><span class="sxs-lookup"><span data-stu-id="e4278-160">level</span></span> |<span data-ttu-id="e4278-161">Opcional.</span><span class="sxs-lookup"><span data-stu-id="e4278-161">Optional.</span></span> <span data-ttu-id="e4278-162">Indica el nivel de registro de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4278-162">Indicates hello log event level.</span></span> |
| <span data-ttu-id="e4278-163">propiedades</span><span class="sxs-lookup"><span data-stu-id="e4278-163">properties</span></span> |<span data-ttu-id="e4278-164">Propiedades de evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4278-164">Properties of hello event.</span></span> |

<span data-ttu-id="e4278-165">Puede ver una lista de todos los proveedores de recursos que admiten la transmisión por secuencias concentradores tooEvent [aquí](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e4278-165">You can view a list of all resource providers that support streaming tooEvent Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="e4278-166">Transmisión de datos de Recursos de proceso</span><span class="sxs-lookup"><span data-stu-id="e4278-166">Stream data from Compute resources</span></span>
<span data-ttu-id="e4278-167">También puede transmitir los registros de diagnóstico de recursos de proceso con el agente de hello diagnósticos de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="e4278-167">You can also stream diagnostic logs from Compute resources using hello Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="e4278-168">[Consulte este artículo](../event-hubs/event-hubs-streaming-azure-diags-data.md) para saber cómo tooset esa copia.</span><span class="sxs-lookup"><span data-stu-id="e4278-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how tooset that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4278-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4278-169">Next steps</span></span>
* [<span data-ttu-id="e4278-170">Más información sobre los registros de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="e4278-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="e4278-171">Introducción a los Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="e4278-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

