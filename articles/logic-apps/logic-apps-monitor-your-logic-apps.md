---
title: Comprobar el estado, configurar el registro y recibir alertas - Azure Logic Apps | Microsoft Docs
description: "Supervise el estado y el rendimiento de aplicaciones lógicas, registre datos de diagnóstico y configure alertas"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 4795f5728d4ce6ff21b97bc3fefd6a53e0c6a11b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="fc096-103">Supervisar el estado, configurar el registro de diagnósticos y activar alertas para Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="fc096-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="fc096-104">Después de [crear y ejecutar una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md), puede comprobar su historial de ejecuciones, historial de desencadenadores, estado y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="fc096-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="fc096-105">Para la supervisión de eventos en tiempo real y una depuración más rica, configure el [registro de diagnósticos](#azure-diagnostics) de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fc096-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="fc096-106">De este modo, puede [buscar y ver eventos](#find-events), como eventos de desencadenador, eventos de ejecución y eventos de acción.</span><span class="sxs-lookup"><span data-stu-id="fc096-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="fc096-107">También puede usar estos [datos de diagnóstico con otros servicios](#extend-diagnostic-data), como Azure Storage y Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="fc096-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="fc096-108">Para recibir notificaciones sobre errores u otros posibles problemas, configure [alertas](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="fc096-108">To get notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="fc096-109">Por ejemplo, puede crear una alerta que detecte "cuando se produzcan errores en más de cinco ejecuciones en una hora".</span><span class="sxs-lookup"><span data-stu-id="fc096-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="fc096-110">También puede configurar la supervisión, el seguimiento y el registro mediante programación con la [configuración de eventos y las propiedades de Azure Diagnostics](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="fc096-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="fc096-111">Visualización del historial de ejecuciones y desencadenadores de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="fc096-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="fc096-112">Para buscar la aplicación lógica en [Azure Portal](https://portal.azure.com), en el menú principal de Azure, elija **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="fc096-112">To find your logic app in the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **More services**.</span></span> <span data-ttu-id="fc096-113">En el cuadro de búsqueda, busque "aplicaciones lógicas" y elija **Aplicaciones lógicas**.</span><span class="sxs-lookup"><span data-stu-id="fc096-113">In the search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Búsqueda de la aplicación lógica](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="fc096-115">Azure Portal muestra todas las aplicaciones lógicas asociadas a la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc096-115">The Azure portal shows all the logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="fc096-116">Seleccione la aplicación lógica y luego elija **Información general**.</span><span class="sxs-lookup"><span data-stu-id="fc096-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="fc096-117">Azure Portal muestra el historial de ejecuciones y desencadenadores de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fc096-117">The Azure portal shows the runs history and trigger history for your logic app.</span></span> <span data-ttu-id="fc096-118">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fc096-118">For example:</span></span>

   ![Historial de ejecuciones e historial de desencadenadores de la aplicación lógica](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="fc096-120">**Historial de ejecuciones** muestra todas las ejecuciones de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fc096-120">**Runs history** shows all the runs for your logic app.</span></span> 
   * <span data-ttu-id="fc096-121">**Historial de desencadenadores** muestra toda la actividad de los desencadenadores de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fc096-121">**Trigger History** shows all the trigger activity for your logic app.</span></span>

   <span data-ttu-id="fc096-122">Para obtener descripciones de estado, vea [Diagnóstico de errores en las aplicaciones lógicas](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="fc096-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="fc096-123">Si no encuentra los datos que espera, en la barra de herramientas, elija **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="fc096-123">If you don't find the data that you expect, on the toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="fc096-124">Para ver los pasos de una ejecución concreta, en **Historial de ejecuciones**, seleccione esa ejecución.</span><span class="sxs-lookup"><span data-stu-id="fc096-124">To view the steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="fc096-125">La vista de supervisión muestra cada paso de esa ejecución.</span><span class="sxs-lookup"><span data-stu-id="fc096-125">The monitor view shows each step in that run.</span></span> <span data-ttu-id="fc096-126">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fc096-126">For example:</span></span>

   ![Acciones de una ejecución concreta](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="fc096-128">Para obtener más detalles sobre la ejecución, elija **Detalles de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="fc096-128">To get more details about the run, choose **Run Details**.</span></span> <span data-ttu-id="fc096-129">Esta información resume los pasos, el estado, las entradas y las salidas de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="fc096-129">This information summarizes the steps, status, inputs, and outputs for the run.</span></span> 

   ![Selección de "Detalles de ejecución"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="fc096-131">Por ejemplo, puede obtener el **Id. de correlación** de la ejecución, que podría necesitar al usar la [API de REST para aplicaciones lógicas](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="fc096-131">For example, you can get the run's **Correlation ID**, which you might need when you use the [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="fc096-132">Para obtener detalles sobre un paso concreto, elija ese paso.</span><span class="sxs-lookup"><span data-stu-id="fc096-132">To get details about a specific step, choose that step.</span></span> <span data-ttu-id="fc096-133">Ahora puede revisar detalles como las entradas, las salidas y los errores acontecidos en ese paso.</span><span class="sxs-lookup"><span data-stu-id="fc096-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="fc096-134">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fc096-134">For example:</span></span>

   ![Detalles del paso](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="fc096-136">Todos los eventos y los detalles de runtime se cifran en el servicio Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="fc096-136">All runtime details and events are encrypted within the Logic Apps service.</span></span> <span data-ttu-id="fc096-137">Solo se descifran cuando un usuario solicita ver esos datos.</span><span class="sxs-lookup"><span data-stu-id="fc096-137">They are decrypted only when a user requests to view that data.</span></span> <span data-ttu-id="fc096-138">Puede controlar el acceso a estos eventos con el [control de acceso basado en roles (RBAC) de Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="fc096-138">You can also control access to these events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="fc096-139">Para obtener detalles sobre un evento de desencadenador concreto, vuelva al panel **Información general**.</span><span class="sxs-lookup"><span data-stu-id="fc096-139">To get details about a specific trigger event, go back to the **Overview** pane.</span></span> <span data-ttu-id="fc096-140">En **Historial de desencadenadores**, seleccione el evento de desencadenador.</span><span class="sxs-lookup"><span data-stu-id="fc096-140">Under **Trigger history**, select the trigger event.</span></span> <span data-ttu-id="fc096-141">Ahora puede revisar detalles como las entradas y salidas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fc096-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Detalles de salida de evento de desencadenador](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="fc096-143">Activación del registro de diagnósticos de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="fc096-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="fc096-144">Para una depuración más rica con detalles y eventos de runtime, puede configurar el registro de diagnósticos con [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc096-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="fc096-145">Log Analytics es un servicio de [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) que supervisa los entornos local y de nube para ayudar a mantener su disponibilidad y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="fc096-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments to help you maintain their availability and performance.</span></span> 

<span data-ttu-id="fc096-146">Antes de empezar, necesita un área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="fc096-146">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="fc096-147">Aprenda [cómo crear un área de trabajo de OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fc096-147">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="fc096-148">En [Azure Portal](https://portal.azure.com), busque y seleccione la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fc096-148">In the [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="fc096-149">En el menú de la hoja de la aplicación lógica, en **Supervisión**, elija **Diagnóstico** > **Configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="fc096-149">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Supervisión, Diagnóstico, Configuración de diagnóstico](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="fc096-151">En **Configuración de diagnóstico**, elija **Activado**.</span><span class="sxs-lookup"><span data-stu-id="fc096-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Activación de los registros de diagnóstico](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="fc096-153">Ahora seleccione el área de trabajo de OMS y la categoría de evento para el registro como se muestra:</span><span class="sxs-lookup"><span data-stu-id="fc096-153">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="fc096-154">Seleccione **Enviar a Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="fc096-154">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="fc096-155">En **Log Analytics**, elija **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="fc096-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="fc096-156">En **Áreas de trabajo de OMS**, seleccione el área de trabajo de OMS que va a usar para el registro.</span><span class="sxs-lookup"><span data-stu-id="fc096-156">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="fc096-157">En **Registro**, seleccione la categoría **WorkflowRuntime**.</span><span class="sxs-lookup"><span data-stu-id="fc096-157">Under **Log**, select the **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="fc096-158">Elija el intervalo métrico.</span><span class="sxs-lookup"><span data-stu-id="fc096-158">Choose the metric interval.</span></span>
   6. <span data-ttu-id="fc096-159">Cuando termine, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fc096-159">When you're done, choose **Save**.</span></span>

   ![Selección del área de trabajo de OMS y los datos para el registro](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="fc096-161">Ahora puede buscar eventos y otros datos de los eventos de desencadenador, los eventos de ejecución y los eventos de acción.</span><span class="sxs-lookup"><span data-stu-id="fc096-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="fc096-162">Búsqueda de eventos y datos de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="fc096-162">Find events and data for your logic app</span></span>

<span data-ttu-id="fc096-163">Para buscar y ver eventos de la aplicación lógica, como eventos de desencadenador, eventos de ejecución y eventos de acción, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="fc096-163">To find and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="fc096-164">En el [Azure Portal](https://portal.azure.com), elija **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="fc096-164">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="fc096-165">Busque "log analytics" y luego elija **Log Analytics** como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="fc096-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Selección de "Log Analytics"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="fc096-167">En **Log Analytics**, busque y seleccione el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="fc096-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selección del área de trabajo de OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="fc096-169">En **Administración**, elija **Portal de OMS**.</span><span class="sxs-lookup"><span data-stu-id="fc096-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Selección de "Portal de OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="fc096-171">En la página principal de OMS, seleccione **Búsqueda de registros**.</span><span class="sxs-lookup"><span data-stu-id="fc096-171">On your OMS home page, choose **Log Search**.</span></span>

   ![Selección de "Búsqueda de registros" en la página principal de OMS](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="fc096-173">O bien</span><span class="sxs-lookup"><span data-stu-id="fc096-173">-or-</span></span>

   ![Selección de "Búsqueda de registros" en el menú OMS ](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="fc096-175">En el cuadro de búsqueda, especifique un campo que quiera buscar y pulse **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="fc096-175">In the search box, specify a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="fc096-176">Cuando empiece a escribir, OMS le mostrará posibles coincidencias y operaciones que puede usar.</span><span class="sxs-lookup"><span data-stu-id="fc096-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="fc096-177">Por ejemplo, para buscar los diez principales eventos que se han producido, escriba y seleccione esta consulta de búsqueda: **Category=WorkflowRuntime |top 10**</span><span class="sxs-lookup"><span data-stu-id="fc096-177">For example, to find the top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Especificación de cadena de búsqueda](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="fc096-179">Más información sobre [cómo buscar datos en Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="fc096-179">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="fc096-180">En la página de resultados, en la barra de la izquierda, elija el marco temporal que quiere ver.</span><span class="sxs-lookup"><span data-stu-id="fc096-180">On the results page, in the left bar, choose the timeframe that you want to view.</span></span>
<span data-ttu-id="fc096-181">Para refinar la consulta con un filtro, elija **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fc096-181">To refine your query by adding a filter, choose **+Add**.</span></span>

   ![Selección del marco temporal de los resultados de la consulta](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="fc096-183">En **Agregar filtros**, escriba el nombre del filtro para poder encontrar el que quiere.</span><span class="sxs-lookup"><span data-stu-id="fc096-183">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="fc096-184">Seleccione el filtro y elija **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fc096-184">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="fc096-185">En este ejemplo se usa la palabra "status" para buscar eventos con errores en **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="fc096-185">This example uses the word "status" to find failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="fc096-186">El filtro de **status_s** ya está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="fc096-186">Here the filter for **status_s** is already selected.</span></span>

   ![Selección de filtro](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="fc096-188">En la barra de la izquierda, seleccione el valor de filtro que quiere usar y elija **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="fc096-188">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   ![Selección del valor de filtro y de "Aplicar"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="fc096-190">Ahora vuelva a la consulta que está creando.</span><span class="sxs-lookup"><span data-stu-id="fc096-190">Now return to the query that you're building.</span></span> <span data-ttu-id="fc096-191">La consulta se ha actualizado con el filtro y el valor seleccionados.</span><span class="sxs-lookup"><span data-stu-id="fc096-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="fc096-192">Los resultados anteriores también se han filtrado.</span><span class="sxs-lookup"><span data-stu-id="fc096-192">Your previous results are now filtered too.</span></span>

   ![Consulta con los resultados filtrados](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="fc096-194">Para guardar la consulta para su uso futuro, elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fc096-194">To save your query for future use, choose **Save**.</span></span> <span data-ttu-id="fc096-195">Aprenda [cómo guardar la consulta](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="fc096-195">Learn [how to save your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="fc096-196">Uso de los datos de diagnóstico con otros servicios</span><span class="sxs-lookup"><span data-stu-id="fc096-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="fc096-197">Además de con Azure Log Analytics, puede usar los datos de diagnóstico de la aplicación lógica con otros servicios de Azure, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fc096-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="fc096-198">Archivar registros de Diagnósticos de Azure en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fc096-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="fc096-199">Transmitir registros de Diagnósticos de Azure a Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="fc096-199">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="fc096-200">Luego puede obtener supervisión en tiempo real mediante la telemetría y los análisis de otros servicios, como [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) y [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="fc096-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="fc096-201">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fc096-201">For example:</span></span>

* [<span data-ttu-id="fc096-202">Transmitir datos de Event Hubs a Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fc096-202">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="fc096-203">Analizar datos que se están transmitiendo con Stream Analytics y crear un panel de análisis en tiempo real en Power BI</span><span class="sxs-lookup"><span data-stu-id="fc096-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="fc096-204">Según las opciones que quiera configurar, primero asegúrese de [crear una cuenta de Azure Storage](../storage/common/storage-create-storage-account.md) o [crear un centro de eventos de Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="fc096-204">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="fc096-205">Luego seleccione las opciones para el envío de los datos de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="fc096-205">Then select the options for where you want to send diagnostic data:</span></span>

![Envío de los datos a una cuenta de Azure Storage o a un centro de eventos](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="fc096-207">Los períodos de retención solo se aplican cuando se usa una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fc096-207">Retention periods apply only when you choose to use a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="fc096-208">Configuración de alertas de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="fc096-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="fc096-209">Para supervisar métricas concretas o umbrales superados de la aplicación lógica, configure [alertas de Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="fc096-209">To monitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="fc096-210">Más información sobre [métricas de Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="fc096-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="fc096-211">Para configurar alertas sin [Azure Log Analytics](../log-analytics/log-analytics-overview.md), siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="fc096-211">To set up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="fc096-212">Para usar criterios y acciones de alerta más avanzados, [configure Log Analytics](#azure-diagnostics) también.</span><span class="sxs-lookup"><span data-stu-id="fc096-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="fc096-213">En el menú de la hoja de la aplicación lógica, en **Supervisión**, elija **Diagnóstico** > **Reglas de alerta** > **Agregar alerta** como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="fc096-213">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Adición de una alerta de la aplicación lógica](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="fc096-215">En la hoja **Agregar una regla de alerta**, cree la alerta como se muestra:</span><span class="sxs-lookup"><span data-stu-id="fc096-215">On the **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="fc096-216">En **Recurso**, seleccione la aplicación lógica si aún no está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="fc096-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="fc096-217">Proporcione un nombre y una descripción para la alerta.</span><span class="sxs-lookup"><span data-stu-id="fc096-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="fc096-218">Seleccione una **Métrica** o evento cuyo seguimiento quiera realizar.</span><span class="sxs-lookup"><span data-stu-id="fc096-218">Select a **Metric** or event that you want to track.</span></span>
   4. <span data-ttu-id="fc096-219">Seleccione una **Condición**, especifique un **Umbral** para la métrica y seleccione el **Periodo** para la supervisión de esta métrica.</span><span class="sxs-lookup"><span data-stu-id="fc096-219">Select a **Condition**, specify a **Threshold** for the metric, and select the **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="fc096-220">Seleccione si se va a enviar correo para la alerta.</span><span class="sxs-lookup"><span data-stu-id="fc096-220">Select whether to send mail for the alert.</span></span> 
   6. <span data-ttu-id="fc096-221">Especifique cualquier otra dirección de correo electrónico para enviar la alerta.</span><span class="sxs-lookup"><span data-stu-id="fc096-221">Specify any other email addresses for sending the alert.</span></span> 
   <span data-ttu-id="fc096-222">También puede especificar la dirección URL de un webhook al que quiera enviar la alerta.</span><span class="sxs-lookup"><span data-stu-id="fc096-222">You can also specify a webhook URL where you want to send the alert.</span></span>

   <span data-ttu-id="fc096-223">Por ejemplo, esta regla envía una alerta cuando hay errores en cinco o más ejecuciones en una hora:</span><span class="sxs-lookup"><span data-stu-id="fc096-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Creación de regla de alerta de métrica](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="fc096-225">Para ejecutar una aplicación lógica desde una alerta, puede incluir el [desencadenador de solicitud](../connectors/connectors-native-reqres.md) en el flujo de trabajo, lo que permite realizar tareas como estos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="fc096-225">To run a logic app from an alert, you can include the [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="fc096-226">Publicar en Slack</span><span class="sxs-lookup"><span data-stu-id="fc096-226">Post to Slack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="fc096-227">Enviar un texto</span><span class="sxs-lookup"><span data-stu-id="fc096-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="fc096-228">Agregar un mensaje a una cola</span><span class="sxs-lookup"><span data-stu-id="fc096-228">Add a message to a queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="fc096-229">Configuración de eventos y detalles de Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="fc096-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="fc096-230">Cada evento de diagnóstico incluye detalles sobre la aplicación lógica y ese evento, por ejemplo, el estado, la hora de inicio, la hora de finalización, etc.</span><span class="sxs-lookup"><span data-stu-id="fc096-230">Each diagnostic event has details about your logic app and that event, for example, the status, start time, end time, and so on.</span></span> <span data-ttu-id="fc096-231">Para configurar mediante programación la supervisión, el seguimiento y el registro, puede usar estos detalles con la [API de REST para Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) y la [API de REST para Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="fc096-231">To programmatically set up monitoring, tracking, and logging, ou can use these details with the [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and the [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="fc096-232">Por ejemplo, el evento `ActionCompleted` tiene las propiedades `clientTrackingId` y `trackedProperties` que puede usar para el seguimiento y la supervisión:</span><span class="sxs-lookup"><span data-stu-id="fc096-232">For example, the `ActionCompleted` event has the `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="fc096-233">`clientTrackingId`: si no se ha proporcionado, Azure genera automáticamente este identificador y correlaciona eventos en una ejecución de aplicación lógica, incluidos los flujos de trabajo anidados que se llamen desde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fc096-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from the logic app.</span></span> <span data-ttu-id="fc096-234">Puede especificar manualmente este identificador desde un desencadenador si pasa un encabezado `x-ms-client-tracking-id` con el valor de identificador personalizado en la solicitud de desencadenador.</span><span class="sxs-lookup"><span data-stu-id="fc096-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in the trigger request.</span></span> <span data-ttu-id="fc096-235">Puede usar un desencadenador de solicitud, un desencadenador HTTP o un desencadenador de webhook.</span><span class="sxs-lookup"><span data-stu-id="fc096-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="fc096-236">`trackedProperties`: para realizar el seguimiento de las entradas o salidas de los datos de diagnóstico se pueden agregar propiedades controladas a acciones en la definición de JSON de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="fc096-236">`trackedProperties`: To track inputs or outputs in diagnostics data, you can add tracked properties to actions in your logic app's JSON definition.</span></span> <span data-ttu-id="fc096-237">Las propiedades controladas solo pueden realizar el seguimiento de entradas y salidas de acciones individuales, aunque puede usar las propiedades `correlation` de los eventos para crear correlaciones entre las acciones de una ejecución.</span><span class="sxs-lookup"><span data-stu-id="fc096-237">Tracked properties can track only a single action's inputs and outputs, but you can use the `correlation` properties of events to correlate across actions in a run.</span></span>

  <span data-ttu-id="fc096-238">Para realizar el seguimiento de una o más propiedades, agregue la sección `trackedProperties` y las propiedades que quiera a la definición de la acción.</span><span class="sxs-lookup"><span data-stu-id="fc096-238">To track one or more properties, add the `trackedProperties` section and the properties you want to the action definition.</span></span> <span data-ttu-id="fc096-239">Por ejemplo, imagine que quiere realizar un seguimiento de datos como un "id. de pedido" en los datos de telemetría:</span><span class="sxs-lookup"><span data-stu-id="fc096-239">For example, suppose you want to track data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="fc096-240">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc096-240">Next steps</span></span>

* [<span data-ttu-id="fc096-241">Creación de plantillas para administrar la implementación y liberación de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="fc096-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="fc096-242">Escenarios B2B y comunicación con Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="fc096-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="fc096-243">Supervisión de mensajes B2B</span><span class="sxs-lookup"><span data-stu-id="fc096-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)