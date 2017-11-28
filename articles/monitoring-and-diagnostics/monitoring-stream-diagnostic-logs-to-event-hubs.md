---
title: "Transmisión de registros de diagnóstico de Azure a un espacio de nombres de Event Hubs | Microsoft Docs"
description: "Aprenda a transmitir registros de diagnóstico de Azure a un espacio de nombres de Event Hubs."
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
ms.openlocfilehash: 01ba8ddfcf90e1368ac147296fd180f99420d96f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="stream-azure-diagnostic-logs-to-an-event-hubs-namespace"></a><span data-ttu-id="ba42e-103">Transmisión de registros de diagnóstico de Azure a un espacio de nombres de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ba42e-103">Stream Azure Diagnostic Logs to an Event Hubs Namespace</span></span>
<span data-ttu-id="ba42e-104">Los **[registros de diagnóstico de Azure](monitoring-overview-of-diagnostic-logs.md)** se pueden transmitir casi en tiempo real a cualquier aplicación mediante la opción "Exportar a Event Hubs" integrada en el Portal o habilitando el identificador de regla de Service Bus en una configuración de diagnóstico por medio de los cmdlets de Azure PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba42e-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time to any application using the built-in “Export to Event Hubs” option in the Portal, or by enabling the Service Bus Rule ID in a diagnostic setting via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="ba42e-105">Qué se puede hacer con registros de diagnóstico y Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ba42e-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="ba42e-106">Estas son solo algunas formas de usar la funcionalidad de streaming para registros de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="ba42e-106">Here are just a few ways you might use the streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="ba42e-107">**Streaming de registros a sistemas de registro y telemetría de terceros**: con el tiempo, el streaming de Event Hubs se convertirá en el mecanismo para canalizar los registros de diagnóstico a sistemas de información de seguridad y administración de eventos (SIEM) y soluciones de análisis de registro de terceros.</span><span class="sxs-lookup"><span data-stu-id="ba42e-107">**Stream logs to 3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your diagnostic logs in to third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="ba42e-108">**Visualización del estado del servicio mediante streaming de datos de "ruta de acceso frecuente" a PowerBI**: utilizando Event Hubs, Stream Analytics y Power BI, puede transformar fácilmente los datos de diagnóstico en información casi en tiempo real sobre los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba42e-108">**View service health by streaming “hot path” data to PowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in to near real-time insights on your Azure services.</span></span> <span data-ttu-id="ba42e-109">[En este artículo de documentación se ofrece una excelente introducción sobre cómo configurar Event Hubs, procesar datos con Stream Analytics y usar PowerBI como salida](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="ba42e-109">[This documentation article gives a great overview of how to set up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="ba42e-110">Estas son algunas recomendaciones para la configuración con los registros de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="ba42e-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="ba42e-111">Un centro de eventos para una categoría de registros de diagnóstico se crea automáticamente al seleccionar la opción en el portal o habilitarla mediante PowerShell, por lo que debería seleccionar el centro de eventos en el espacio de nombres con el nombre que empieza por **insights-**.</span><span class="sxs-lookup"><span data-stu-id="ba42e-111">An event hub for a category of diagnostic logs is created automatically when you check the option in the portal or enable it through PowerShell, so you want to select the event hub in the namespace with the name that starts with **insights-**.</span></span>
  * <span data-ttu-id="ba42e-112">El siguiente código SQL es una consulta de Stream Analytics de ejemplo que puede utilizar para analizar simplemente todos los datos de registro en una tabla de PowerBI:</span><span class="sxs-lookup"><span data-stu-id="ba42e-112">The following SQL code is a sample Stream Analytics query that you can use to parse all the log data in to a PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want to track]
    INTO
    [OutputSourceName – the PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="ba42e-113">**Creación de una plataforma personalizada de registro y telemetría** : si ya tiene una plataforma de telemetría personalizada o está pensando en crear una, la gran escalabilidad en cuanto a la suscripción y la publicación de los Centros de eventos permite introducir registros de diagnóstico de manera flexible.</span><span class="sxs-lookup"><span data-stu-id="ba42e-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="ba42e-114">[Consulte la guía de Dan Rosanova para usar Centros de eventos en una plataforma de telemetría de escala global aquí](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="ba42e-114">[See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="ba42e-115">Habilitación del streaming de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ba42e-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="ba42e-116">Puede habilitar el streaming de registros de diagnóstico mediante programación, a través del portal o mediante la [API de REST de Azure Monitor](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="ba42e-116">You can enable streaming of diagnostic logs programmatically, via the portal, or using the [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="ba42e-117">En cualquier caso, se crea una configuración de diagnóstico en la que se especifica un espacio de nombres de Event Hubs y las categorías de registro y métricas que se desea enviar al espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="ba42e-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and the log categories and metrics you want to send in to the namespace.</span></span> <span data-ttu-id="ba42e-118">Se crea un centro de eventos en el espacio de nombres para cada categoría de registro que se habilita.</span><span class="sxs-lookup"><span data-stu-id="ba42e-118">An event hub is created in the namespace for each log category you enable.</span></span> <span data-ttu-id="ba42e-119">Una **categoría de registro** de diagnóstico es un tipo de registro que un recurso puede recopilar.</span><span class="sxs-lookup"><span data-stu-id="ba42e-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="ba42e-120">La habilitación y streaming de registros de diagnóstico desde recursos de proceso (por ejemplo, máquinas virtuales o Service Fabric) [requiere ejecutar una serie de pasos distinta](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="ba42e-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="ba42e-121">El espacio de nombres de Event Hubs o Service Bus no tiene que estar en la misma suscripción que el recurso que emite los registros, siempre que el usuario que configura el ajuste tenga acceso RBAC adecuado a ambas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="ba42e-121">The Service Bus or Event Hubs namespace does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-the-portal"></a><span data-ttu-id="ba42e-122">Streaming de registros de diagnóstico mediante el portal</span><span class="sxs-lookup"><span data-stu-id="ba42e-122">Stream diagnostic logs using the portal</span></span>
1. <span data-ttu-id="ba42e-123">En el portal, desplácese a Azure Monitor y haga clic en **Configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="ba42e-123">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Sección de supervisión de Azure Monitor](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="ba42e-125">Si lo desea, filtre la lista por tipo de recurso o por grupo de recursos y, a continuación, haga clic en el recurso para el que desea establecer la configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ba42e-125">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="ba42e-126">Si no existe ninguna configuración en el recurso que ha seleccionado, se le pide que cree una.</span><span class="sxs-lookup"><span data-stu-id="ba42e-126">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="ba42e-127">Haga clic en "Activar diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="ba42e-127">Click "Turn on diagnostics."</span></span>

   ![Agregar configuración de diagnóstico: sin configuración actual](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="ba42e-129">Si hay una configuración actual en el recurso, verá una lista de opciones ya configuradas en este recurso.</span><span class="sxs-lookup"><span data-stu-id="ba42e-129">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="ba42e-130">Haga clic en "Agregar configuración de diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="ba42e-130">Click "Add diagnostic setting."</span></span>

   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="ba42e-132">Asigne un nombre a su configuración y active la casilla **Transmitir a un centro de eventos**; a continuación, seleccione un espacio de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ba42e-132">Give your setting a name and check the box for **Stream to an event hub**, then select an Event Hubs namespace.</span></span>
   
   ![Agregar configuración de diagnóstico: configuración actual](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="ba42e-134">En el espacio de nombres seleccionado será donde se cree el centro de eventos (si es la primera vez que transmite registros de diagnóstico) o a donde se transmitan (si ya hay recursos que estén transmitiendo esa categoría de registro a este espacio de nombres); la directiva define los permisos que tiene el mecanismo de streaming.</span><span class="sxs-lookup"><span data-stu-id="ba42e-134">The namespace selected will be where the event hub is created (if this is your first time streaming diagnostic logs) or streamed to (if there are already resources that are streaming that log category to this namespace), and the policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="ba42e-135">En la actualidad, para realizar streaming a un centro de eventos, se necesitan permisos de administración, envío y escucha.</span><span class="sxs-lookup"><span data-stu-id="ba42e-135">Today, streaming to an event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="ba42e-136">Puede crear o modificar las directivas de acceso compartido del espacio de nombres de Event Hubs en la pestaña Configurar del portal para su espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="ba42e-136">You can create or modify Event Hubs namespace shared access policies in the portal under the Configure tab for your namespace.</span></span> <span data-ttu-id="ba42e-137">Para actualizar uno de estas opciones de diagnóstico, el cliente tiene que tener el permiso ListKey en la regla de autorización de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ba42e-137">To update one of these diagnostic settings, the client must have the ListKey permission on the Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="ba42e-138">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ba42e-138">Click **Save**.</span></span>

<span data-ttu-id="ba42e-139">Transcurridos unos instantes, la nueva opción de configuración aparece en la lista de opciones para este recurso y los registros de diagnóstico se transmiten en esa cuenta de almacenamiento en cuanto se generan nuevos datos de eventos.</span><span class="sxs-lookup"><span data-stu-id="ba42e-139">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are streamed to that storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="ba42e-140">Mediante cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba42e-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="ba42e-141">Para habilitar el streaming mediante [cmdlets de Azure PowerShell](insights-powershell-samples.md), puede utilizar el cmdlet `Set-AzureRmDiagnosticSetting` con estos parámetros:</span><span class="sxs-lookup"><span data-stu-id="ba42e-141">To enable streaming via the [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use the `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="ba42e-142">El identificador de regla del Bus de servicio es una cadena con este formato: `{Service Bus resource ID}/authorizationrules/{key name}`, por ejemplo, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="ba42e-142">The Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="ba42e-143">Mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ba42e-143">Via Azure CLI</span></span>
<span data-ttu-id="ba42e-144">Para habilitar el streaming mediante la [CLI de Azure](insights-cli-samples.md), puede utilizar el comando `insights diagnostic set` del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ba42e-144">To enable streaming via the [Azure CLI](insights-cli-samples.md), you can use the `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="ba42e-145">Utilice el mismo formato para el identificador de regla del Bus de servicio, como se explicó para el cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba42e-145">Use the same format for Service Bus Rule ID as explained for the PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="ba42e-146">¿Cómo se consumen los datos de registro procedentes de centros de eventos?</span><span class="sxs-lookup"><span data-stu-id="ba42e-146">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="ba42e-147">Estos son datos de salida de ejemplo de Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="ba42e-147">Here is sample output data from Event Hubs:</span></span>

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

| <span data-ttu-id="ba42e-148">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="ba42e-148">Element Name</span></span> | <span data-ttu-id="ba42e-149">Description</span><span class="sxs-lookup"><span data-stu-id="ba42e-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ba42e-150">records</span><span class="sxs-lookup"><span data-stu-id="ba42e-150">records</span></span> |<span data-ttu-id="ba42e-151">Matriz de todos los eventos de registro de esta carga.</span><span class="sxs-lookup"><span data-stu-id="ba42e-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="ba42e-152">Twitter en tiempo</span><span class="sxs-lookup"><span data-stu-id="ba42e-152">time</span></span> |<span data-ttu-id="ba42e-153">Hora a la que se produjo el error.</span><span class="sxs-lookup"><span data-stu-id="ba42e-153">Time at which the event occurred.</span></span> |
| <span data-ttu-id="ba42e-154">categoría</span><span class="sxs-lookup"><span data-stu-id="ba42e-154">category</span></span> |<span data-ttu-id="ba42e-155">Categoría de registro para este evento.</span><span class="sxs-lookup"><span data-stu-id="ba42e-155">Log category for this event.</span></span> |
| <span data-ttu-id="ba42e-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="ba42e-156">resourceId</span></span> |<span data-ttu-id="ba42e-157">Id. de recurso del recurso que generó este evento.</span><span class="sxs-lookup"><span data-stu-id="ba42e-157">Resource ID of the resource that generated this event.</span></span> |
| <span data-ttu-id="ba42e-158">operationName</span><span class="sxs-lookup"><span data-stu-id="ba42e-158">operationName</span></span> |<span data-ttu-id="ba42e-159">Nombre de la operación.</span><span class="sxs-lookup"><span data-stu-id="ba42e-159">Name of the operation.</span></span> |
| <span data-ttu-id="ba42e-160">level</span><span class="sxs-lookup"><span data-stu-id="ba42e-160">level</span></span> |<span data-ttu-id="ba42e-161">Opcional.</span><span class="sxs-lookup"><span data-stu-id="ba42e-161">Optional.</span></span> <span data-ttu-id="ba42e-162">Indica el nivel de registro de eventos.</span><span class="sxs-lookup"><span data-stu-id="ba42e-162">Indicates the log event level.</span></span> |
| <span data-ttu-id="ba42e-163">propiedades</span><span class="sxs-lookup"><span data-stu-id="ba42e-163">properties</span></span> |<span data-ttu-id="ba42e-164">Propiedades del evento.</span><span class="sxs-lookup"><span data-stu-id="ba42e-164">Properties of the event.</span></span> |

<span data-ttu-id="ba42e-165">Puede ver una lista de todos los proveedores de recursos que admiten el streaming a Event Hubs [aquí](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ba42e-165">You can view a list of all resource providers that support streaming to Event Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="ba42e-166">Transmisión de datos de Recursos de proceso</span><span class="sxs-lookup"><span data-stu-id="ba42e-166">Stream data from Compute resources</span></span>
<span data-ttu-id="ba42e-167">También puede transmitir los registros de diagnóstico de los recursos de Compute mediante el agente de Microsoft Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="ba42e-167">You can also stream diagnostic logs from Compute resources using the Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="ba42e-168">[Consulte este artículo](../event-hubs/event-hubs-streaming-azure-diags-data.md) para ver cómo configurarlo.</span><span class="sxs-lookup"><span data-stu-id="ba42e-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how to set that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba42e-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba42e-169">Next steps</span></span>
* [<span data-ttu-id="ba42e-170">Más información sobre los registros de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="ba42e-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="ba42e-171">Introducción a los Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="ba42e-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

